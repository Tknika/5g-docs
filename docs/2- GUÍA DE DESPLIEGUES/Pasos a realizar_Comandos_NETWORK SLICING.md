# NETWORK SLICING

## Índice

- [1. Velocidad y Ancho de Banda](#1-velocidad-y-ancho-de-banda)
- [2. Latencia (Tiempo de respuesta)](#2-latencia-tiempo-de-respuesta)
- [3. Aislamiento de Red (Seguridad del Slice)](#3-aislamiento-de-red-seguridad-del-slice)

SST = Qué es  
SD = Quién es

| Valor SST | Nombre | Descripción |
|:----------|:--------|:------------|
| **1** | **eMBB** | Banda ancha móvil mejorada (lo que usas para Internet). |
| **2** | **URLLC** | Comunicaciones de ultra-baja latencia (coches autónomos, cirugía remota). |
| **3** | **MIoT** | Internet de las cosas masivo (sensores de ciudades inteligentes). |
| **4** | **V2X** | Vehículo con todo (comunicaciones viales). |
| **5** | **HMTC** | Comunicaciones tipo máquina de alto rendimiento. |

Vamos a utilizar dos SST diferentes, aunque también podríamos usar el mismo SST y diferenciar los servicios mediante el SD.

Vamos a realizar tres prácticas:

1. Velocidad y Ancho de Banda
2. Latencia (Tiempo de respuesta)
3. Seguridad

# 1. Velocidad y Ancho de Banda

Para lograr que cada "rodaja" tenga capacidades de rendimiento distintas, debemos configurar los parámetros de QoS (*Quality of Service*) y AMBR (*Aggregate Maximum Bit Rate*) dentro del núcleo de Open5GS.

En el repositorio de HerlesUpreeth, los ficheros YAML ya separan el tráfico por SMF y UPF, pero la diferenciación de velocidades se define realmente en la base de datos del suscriptor (HSS/UDM) mediante la WebUI de Open5GS.

## Diferenciar Ancho de Banda (AMBR)

El AMBR limita la velocidad máxima total permitida al usuario para una sesión PDU.

### Slice Internet

Configurar un APN-AMBR alto en descarga y moderado en subida:

- Downlink: 100 Mbps
- Uplink: 20 Mbps

### Slice Private (Streaming)

Configurar un APN-AMBR priorizando la subida para soportar el flujo procedente de cámaras:

- Downlink: 10 Mbps
- Uplink: 50 Mbps

## Configuración desde la WebUI

Editar el suscriptor y, dentro de la sección **Slices**, añadir dos configuraciones de sesión distintas para cada S-NSSAI.

### Slice Internet

```text
SST: 1
AMBR DL: 100 Mbps
AMBR UL: 20 Mbps
```

### Slice Private

```text
SST: 1
AMBR DL: 10 Mbps
AMBR UL: 50 Mbps
```

## Alternativa mediante tc

La limitación desde la WebUI puede no aplicarse correctamente dependiendo de la versión utilizada.

En ese caso, acceder a la consola del contenedor UPF y ejecutar:

```bash
tc qdisc add dev ogstun root tbf rate 5mbit burst 32kbit lat 400ms
```

Con ello se limita el tráfico de bajada (*Downlink*) hacia el móvil a 5 Mbps.

> `ogstun` es la interfaz de túnel utilizada por Open5GS.

> Si el contenedor UPF se elimina y vuelve a desplegarse, la configuración realizada mediante `tc` se perderá y deberá aplicarse nuevamente.

# 2. Latencia (Tiempo de respuesta)

## Diferenciar Latencia y Prioridad (5QI)

La latencia se gestiona mediante el identificador **5QI (5G QoS Identifier)**.

Cada valor de 5QI tiene asociados requisitos de prioridad y retardo.

### Slice Internet

Utilizar:

```text
5QI = 9
```

Características:

- Tráfico por defecto.
- Non-GBR.
- Retardo admisible de aproximadamente 300 ms.

### Slice Private / Streaming

Utilizar:

```text
5QI = 4
```

Características:

- Mayor prioridad.
- Adecuado para vídeo en streaming.
- Retardo aproximado de 150 ms.

También podría utilizarse:

```text
5QI = 1
```

para simular servicios de misión crítica.

## Implementación

Se crearán dos escenarios:

- APN Internet (uso normal).
- APN Private (Video Streaming).

### Paso 1. Configuración de señalización (WebUI)

Primero definiremos los perfiles correspondientes en el Core.

1. Acceder a la Open5GS WebUI.
2. Seleccionar el suscriptor (IMSI).
3. Localizar la sección **Slices**.

#### Slice Internet

```text
SST: 1
5QI: 9
```

#### Slice Private

```text
SST: 2
5QI: 4
```

### Paso 2. Implementación de latencia real (UPF)

Dado que la radio Baicells y algunos terminales pueden no aplicar el 5QI físicamente, introduciremos retardos utilizando `tc netem`.

#### UPF Internet

Acceder al contenedor:

```bash
tc qdisc add dev ogstun root netem delay 100ms 10ms
```

#### UPF Private

Acceder al contenedor:

```bash
tc qdisc add dev ogstun root netem delay 5ms
```

### Paso 3. Verificación

#### Prueba de latencia (Ping)

Desde un móvil conectado al Slice Internet:

```bash
ping 8.8.8.8
```

Se deberían observar latencias superiores a 150 ms.

Desde un móvil conectado al Slice Private:

```bash
ping 8.8.8.8
```

Se deberían observar latencias significativamente menores.

## Explicación

En una red comercial, un flujo con 5QI 4 tendría prioridad sobre uno con 5QI 9 en las colas de planificación de radio.

Al no disponer de un scheduler que aplique estas prioridades de forma efectiva en el entorno de laboratorio, utilizamos `tc netem` para emular el comportamiento extremo a extremo.

# 3. Aislamiento de Red (Seguridad del Slice)

El objetivo es que:

- El móvil conectado al Slice Internet tenga acceso libre a Internet o a la red que definamos.
- El móvil conectado al Slice Private permanezca aislado y solo pueda acceder a recursos autorizados, como una cámara IP o un servidor de streaming.

En el repositorio de HerlesUpreeth cada slice dispone de su propio contenedor UPF, lo que permite aplicar reglas de firewall independientes.

| Slice | Política de Seguridad | Resultado esperado |
|:-------|:---------------------|:-------------------|
| **Internet** | Open Policy | Navegación libre (Google, YouTube, etc.) |
| **Private** | Walled Garden | Solo acceso a la IP de la cámara o servidor autorizado |

## Ejemplo práctico

Dentro del contenedor `upf-private`, bloquear el acceso a una IP externa, por ejemplo `8.8.8.8`:

```bash
iptables -A FORWARD -d 8.8.8.8 -j DROP
```

## Resultado esperado

- El móvil conectado al Slice Internet podrá realizar ping a `8.8.8.8`.
- El móvil conectado al Slice Private no podrá realizar ping a `8.8.8.8`.
- Ambos móviles seguirán conectados a la misma antena y al mismo Core 5G.

Esto permite demostrar de forma práctica el aislamiento de tráfico entre slices utilizando una infraestructura Open5GS.

