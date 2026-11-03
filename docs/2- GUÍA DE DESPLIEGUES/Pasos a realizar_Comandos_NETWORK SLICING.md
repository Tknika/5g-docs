# NETWORK SLICING

SST= Qué es   
SD= Quién es

| Valor SST | Nombre | Descripción |
| :---- | :---- | :---- |
| **1** | **eMBB** | Banda ancha móvil mejorada (lo que usas para **Internet**). |
| **2** | **URLLC** | Comunicaciones de ultra-baja latencia (coches autónomos, cirugía remota). |
| **3** | **MIoT** | Internet de las cosas masivo (sensores de ciudades inteligentes). |
| **4** | **V2X** | Vehículo con todo (comunicaciones viales). |
| **5** | **HMTC** | Comunicaciones tipo máquina de alto rendimiento. |

Vamos a utilizar 2 SSTs pero podríamos usar el mismo SST y cambiar el SD.  
Vamos a realizar 3 prácticas:

1. **Velocidad y Ancho de Banda**  
2. **Latencia (Tiempo de respuesta)**  
3. **Seguridad**

**1\. Velocidad y Ancho de Banda**  
Para lograr que cada "rodaja" tenga capacidades de rendimiento distintas, debes configurar los parámetros de QoS (Quality of Service) y AMBR (Aggregate Maximum Bit Rate) dentro del núcleo de Open5GS.

En el repositorio de herlesupreeth, los archivos YAML ya separan el tráfico por SMF/UPF, pero la "magia" de las velocidades se define en la base de datos del suscriptor (HSS/UDM) a través de la WebUI. 

1\. Diferenciar Ancho de Banda (AMBR)

El AMBR limita la velocidad máxima total del usuario para esa sesión PDU. Para tu caso:

* Slice Internet: Configura un APN-AMBR alto en Downlink (ej. 100 Mbps) y moderado en Uplink (ej. 20 Mbps).  
* Slice Private (Streaming): Configura un APN-AMBR con prioridad en el Uplink (ej. 50 Mbps de subida) para soportar el flujo de las cámaras. 

Cómo hacerlo:

En la Open5GS WebUI, edita el suscriptor y en la sección de Slices, añade dos configuraciones de sesión distintas para cada S-NSSAI (SST/SD): 

* Slice 1 (Internet): SST 1-\> AMBR DL: 100Mbps, UL: 20Mbps.  
* Slice 2 (Private): SST 1-\> AMBR DL: 10Mbps, UL: 50Mbps.

**Al hacerlo desde webui no me funciona, entro en la consola de UPF y ejecuto:**

tc qdisc add dev ogstun root tbf rate 5mbit burst 32kbit lat 400ms

Consigo limitar: *Limitamos el tráfico que va hacia el móvil (Downlink) a 5Mbps para que se note el cambio*  
*\# 'ogstun' es la interfaz de túnel de Open5GS*  
**Si borro e inicializo el contenedor deja de tener efecto la limitación.**

**2\. Latencia (Tiempo de respuesta)**

**Diferenciar Latencia y Prioridad (5QI)**

La latencia se gestiona mediante el identificador 5QI (5G QoS Identifier). Cada valor de 5QI tiene estandarizados retardos máximos y prioridades: 

* Internet: Usa 5QI 9 (Tráfico por defecto, retardo admisible de 300ms).  
* Private/Streaming: Usa 5QI 4 (Garantizado, ideal para video streaming con retardo de 150ms) o incluso 5QI 1 si quieres simular servicios de misión crítica. 

***Implementación:***  
*Creamos dos casos el de APN internet (uso “normal”) y el de APN private (uso “Video Streaming”)*  
Paso 1: Configuración de Señalización (WebUI)  
Primero, definiremos los perfiles en el Core para que el móvil "sepa" qué tipo de tráfico está cursando.

1. Accede a la Open5GS WebUI.  
2. En el suscriptor (IMSI) de tus móviles, busca la sección de Slices:  
1. Slice Internet (SST:1): En la configuración de la sesión PDU, asegúrate de que el 5QI sea 9\. Este es el valor Non-GBR (prioridad baja) estándar para internet.  
2. Slice Private (SST:2): Cambia el 5QI a 4\. Este valor indica a la red que es tráfico de Video Streaming (Buffered) con mayor prioridad y menores requisitos de retardo.

Paso 2: Implementación de Latencia Real (UPF)  
Como vimos, la Baicells y los móviles podrían ignorar el 5QI a nivel físico. Para que el alumno vea la diferencia al hacer un ping, aplicaremos el retardo en el UPF.  
Accedemos a la consola del contenedor del upf-internet:  
tc qdisc add dev ogstun root netem delay 100ms 10ms  
Accedemos a la consola del contenedor del upf-private:  
tc qdisc add dev ogstun root netem delay 5ms

Paso 3: Verificación en el Curso (Móviles Reales)  
***Prueba de Latencia (Ping):***

* Desde el móvil en Slice Internet: ping 8.8.8.8 -\> Deberían ver latencias de \>150ms.  
* Desde el móvil en Slice Private: ping 8.8.8.8 -\> Deberían ver latencias mucho menores (la base de la radio \+ 5ms).

***Explicación:***

* En una red comercial, el 5QI 4 le diría a la Baicells que ese móvil tiene prioridad en la cola de radio frente al de 5QI 9\.  
* Al no tener un "Scheduler" activo en la radio que respete esto, el UPF con tc netem es nuestra herramienta para emular ese comportamiento de red extremo a extremo.

**3\. Aislamiento de Red (Seguridad del Slice)**

El objetivo es que el Móvil 1 (Internet) navegue “por todo el mundo” o zona que definamos, mientras que el Móvil 2 (Private) esté "atrapado" en un entorno seguro donde solo puede ver la cámara de streaming.

En el repositorio de Herle, cada slice tiene su propio contenedor UPF. Esto nos permite aplicar reglas de firewall (iptables) de forma independiente.

| Slice | Política de Seguridad | Resultado esperado |
| :---- | :---- | :---- |
| **Internet** | Open Policy | Navegación libre (Google, YouTube, etc.) |
| **Private** | Walled Garden | **Solo** acceso a la IP de la Cámara / Servidor. |

En el contenedor upf-private, bloquea el acceso a una IP externa (ej. Google) pero permite el acceso a tu servidor local de cámaras:  
bash  
*\# Dentro del contenedor upf-private*  
iptables \-A FORWARD \-d 8.8.8.8 \-j DROP 

El alumno verá que el móvil en el slice de internet puede hacer ping 8.8.8.8, pero el móvil en el slice de cámaras no, aunque ambos estén conectados a la misma antena Baicells.

