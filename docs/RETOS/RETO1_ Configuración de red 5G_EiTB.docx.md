

**CURSO INSTALACIÓN Y CONFIGURACIÓN DE REDES 5G**

**“Caso de uso: Red privada 5G en las instalaciones de EiTB (Donosti)”**

**Situación:**

EiTB quiere sustituir su red WiFi tradicional por una **red privada 5G** con el objetivo de:

* Evitar interferencias.  
* Garantizar calidad de servicio.  
* Disponer de control total sobre usuarios y dispositivos.  
* Preparar la infraestructura para servicios críticos de comunicación y vídeo.

La red se desplegará inicialmente en una de sus instalaciones (sede / fábrica) en Donostia.

**Servicios iniciales:**  
La red debe dar servicio, al menos, a los siguientes dispositivos:

* **Terminal 1:**  
   Teléfono móvil de un trabajador de EiTB.  
   Uso: acceso a Internet y aplicaciones internas de gestión.  
* **Terminal 2:**  
   Router 5G o cámara IP conectada a la red privada.  
   Uso: videovigilancia dentro de la red de EiTB.

![][image1]  
**Imagen:** Red privada 5G para eitb Donosti

## **Arquitectura de la red**

La red privada 5G estará compuesta por los siguientes elementos:

* **Core 5G (Open5GS)**  
  Incluye funciones de control y usuario (AMF, SMF, UPF, etc.).  
    
* **Radio gNB**  
  Proporciona cobertura radio 5G dentro de las instalaciones.  
    
* **Dispositivo de red (Mikrotik)**  
  Encargado de:  
  * Salida a red local / Internet.  
  * NAT y encaminamiento.


* **OpenCell \+ SIMs**  
  Para la gestión y provisión de identidades de usuario (UEs).  
    
* **Equipos cliente (UEs)**  
  Teléfono móvil y router/cámara 5G.

## **Desarrollo del entrenamiento 05**

Partiendo del equipamiento proporcionado (Core 5G, radio gNB, dispositivos de red y terminales de cliente), se procederá a la **instalación y configuración de una red privada celular 5G**, asegurando que todos los elementos queden integrados correctamente dentro de la red del cliente (EiTB).

Cada grupo deberá configurar una red con **parámetros propios**, que la identifiquen de manera única y eviten interferencias con otras redes.

## **Parámetros de configuración**

### **EQUIPO 1**

### **Parámetros a configurar en el Core 5G**

* **Nombre del Operador:**  
* **PLMN:**  
  * **MCC:**  
  * **MNC:**  
* **TAC (Tracking Area Code):**

### **Parámetros a configurar en la radio gNB**

* **Modo dúplex:**  
* **Ancho de banda:**  
* **ARFCN:**  
* **Subframe Assignment:**  
* **Sector ID / PCI** (valor entre 0 – 553):  
* **gNB ID (hexadecimal):**  
* **Potencia de transmisión:**  
* **PLMN:**  
* **TAC:**

## 

## 

## 

## 

## 

## **Se pide**

### **1\. Esquema de red**

Realiza un **esquema lógico sencillo** en el que se indiquen:

* Elementos que intervienen en la red privada 5G.  
* Conexiones entre ellos.  
* Parámetros de red principales asociados a cada elemento.

**Resultado esperado:**  
Un mapa lógico claro de la red privada 5G de EiTB.  (**Tabla I**)

### **2\. Configuración de la red**

Configura la red privada celular 5G utilizando los parámetros listados anteriormente:

* Core 5G.  
* Radio gNB.  
* SIMs.  
* Dispositivos clientes.

### **3\. Verificación de funcionamiento**

Comprueba el funcionamiento de la red privada 5G desde el lado del cliente haciendo uso de las herramientas necesarias:

* Analizador espectral.  
* Aplicaciones del terminal.  
* Test de velocidad.  
* Ping / traceroute.  
* Logs del Core 5G.

### **4\. Medidas de rendimiento**

Realiza una **tabla de resultados** con:

* Velocidades de subida y bajada.  
* Latencia medida.


Posteriormente:

* Modifica el **ancho de banda**.  
* Modifica el **subframe assignment**  
  .

Vuelve a medir y compara resultados.

### **5\. Gestión de SIMs**

* Crea una **nueva SIM** para la red privada 5G.  
* Regístrala correctamente en el Core 5G.


**Pregunta:**

* ¿Qué **APN** has configurado para esta red privada?

## 

## 

## 

## **¿Qué pasa si…?**

Analiza y documenta el comportamiento de la red en los siguientes casos:

1. **Cambiamos solo el TAC o el PLMN** en:

   * El Core 5G.  
   * La radio gNB.

    Mostrar y explicar el fallo resultante.

2. **Paramos el contenedor del UPF**

   * ¿Qué ocurre con el tráfico de datos?  
   * ¿El terminal sigue registrado en red?  
       
3. **Nos desplazamos fuera de cobertura**

   * ¿Cómo responde la red?  
   * ¿Qué mensajes aparecen en el Core?

## **EXTRA – Documentación para el cliente**

Elabora una **documentación final para EiTB**, que incluya como mínimo:

### **PORTADA**

* Nombre del proyecto.  
* Cliente.  
* Fecha.  
* Equipo responsable.


### **ÍNDICE**

### **INSTALACIÓN DE LA RED PRIVADA**

* Descripción general.  
* Datos técnicos necesarios para el cliente.  
* Parámetros configurados.


### **CAMBIOS EN LA CONFIGURACIÓN**

* Posibles modificaciones para mejorar velocidades.  
* Ajustes según el uso final:  
  * Móviles.  
  * Cámaras.  
  * Routers.

### **CONCLUSIONES**

* UEs conectados.  
* Rendimiento observado.  
* Troubleshooting básico.

## **Enlaces de consulta**

[**https://5g-tools.com/**](https://5g-tools.com/)

[**https://www.cellmapper.net/enbid?lang=es**](https://www.cellmapper.net/enbid?lang=es)

| Elementos de la red privada Celular 5G |   |  |  |  |
| :---- | ----- | :---- | ----- | :---- |
| **Sistema radiante** |   |  |  |  |
| **RRU (Unidad de radio remota)** |   |  |  |  |
| **BBU (Unidad de banda base)** |   |  |  |  |
| **Core de la red** |   |  |  |  |
| **Identificación de las Ips de la red privada celular 5G** | ** ** |  |  |  |
| **Elemento** | **IP** | **Máscara** | **Puerta de enlace** | **DNS** |
| **gNB** |   |   |   |   |
| **Host del Core-físico** |   |   |   |   |
| **Core 5G** |   |   |   |   |
| **UPF** |  |  |  |  |
| **Terminal móvil** |   |   |   |   |

[image1]: img/reto1_image1.png