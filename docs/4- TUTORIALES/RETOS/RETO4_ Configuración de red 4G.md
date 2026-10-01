

**CURSO INSTALACIÓN Y CONFIGURACIÓN DE REDES 5G**

**“Configuración y comprobación de funcionamiento de una red privada 4G”**

**Situación:**

Se pretende **configurar y comprobar** el funcionamiento de una **red privada 4G** para un cliente que quiere cambiar su sistema inalámbrico basado en tecnología Wifi por otro que trabaje en frecuencias licenciadas para evitar cualquier mal funcionamiento por interferencias de otros servicios.

![][image1]  
**Imagen:** Red privada virtual 4G en fábrica de Renault desplegada por Telefónica

**Desarrollo del entrenamiento:**

Partiendo del equipamiento del Core, la radio eNB y los dispositivos de red y del terminal a entregar al cliente, se va a proceder a configurar los equipos para que se integren dentro de la red del cliente con una serie de parámetros que la identifiquen de forma única.

Los parámetros a configurar se recogen en el siguiente cuadro:

**EQUIPO1:**

1. **Parámetros a configurar en el Core 4G:**  
* **Nombre del Operador:**   
* **PLMN:**  
  * **MCC**:   
  * **MNC:**   
* **TAC:** 


2. **Parámetros a configurar en la radio eNB:**

* **Modo duplex:**   
* **Ancho de banda:**  
* **EARFCN:**  
* **Subframe Assigment:**   
* **Sector ID \= PCI (value between 0 – 553):**  
* **eNB ID (hex)=**   
* **ECI (value between 0 – 65535):**  
* **Potencia:**  
* **PLMN:**  
* **TAC**

**Se pide:**

1. **Haz un esquema (mapa lógico sencillo) indicando los elementos que intervienen en la red privada celular 4G y sus correspondientes parámetros de red. *(TABLA I*)**  
     
2. **Cumplimentar los apartados indicados en la tabla adjunta con los valores recogidos con las apps. *(TABLA II)***  
     
3. **Configurar la red privada celular 4G con los parámetros listados anteriormente.**  
     
4. **Comprueba el funcionamiento de la red privada celular 4G desde el lado del cliente haciendo uso de las herramientas necesarias para ello (Analizador espectral, Apps, test de velocidad, etc …)**  
     
5. **Realizar una tabla con las velocidades conseguidas, tras las modificaciones del ancho de banda y del subframe.**  
     
6. **Crear una nueva SIM para nuestra nueva red privada**  
   * **¿Qué APN has configurado?**  
       
7.  **¿Qué pasa si….**  
   * **Cambiamos solo el TAC o PLMN en la radio/core? Mostrar el fallo**  
   * **Paramos el contenedor del SGWU?**  
   * **Nos movemos y perdemos cobertura?**  
       
8. **Realizar una SIM con mismo MCC pero diferente MNC: Analiza que nos indica el móvil**

   

**EXTRA: Elaborar una documentación completa para el cliente, que tenga los siguientes apartados:**  
**PORTADA**	  
**ÍNDICE**  
**INSTALACIÓN DE LA RED PRIVADA: Datos necesarios para el cliente**  
**CAMBIOS EN LA CONFIGURACIÓN: Posibles modificaciones para mejora de velocidades, dependiendo del uso final.**  
**CONCLUSIONES: UEs conectados, troubleshooting**

**Enlaces de consulta:**  
[**https://5g-tools.com/4g-lte-cell-id-eci-calculator/**](https://5g-tools.com/4g-lte-cell-id-eci-calculator/)  
[**https://www.cellmapper.net/enbid?lang=es**](https://www.cellmapper.net/enbid?lang=es)

**CURSO INSTALACIÓN Y CONFIGURACIÓN DE REDES 5G**

*Tabla I*

| Elementos de la red privada Celular 4G |   |  |  |  |
| :---- | ----- | :---- | ----- | :---- |
| **Sistema radiante** |   |  |  |  |
| **RRU (Unidad de radio remota)** |   |  |  |  |
| **BBU (Unidad de banda base)** |   |  |  |  |
| **Core de la red** |   |  |  |  |
| **Identificación de las Ips de la red privada celular 4G** | ** ** |  |  |  |
| **Elemento** | **IP** | **Máscara** | **Puerta de enlace** | **DNS** |
| **eNB** |   |   |   |   |
| **Host del Core-físico** |   |   |   |   |
| **Core 4G** |   |   |   |   |
| **Terminal móvil** |   |   |   |   |

| Datos del Operador |  |  |  |  |
| ----- | ----- | ----- | ----- | ----- |
| **Operador** | **MCC** | **MNC** |  |  |
| ** ** | ** ** | ** ** |  |  |
| **Datos de la celda a la que está conectado el terminal** |  |  |  |  |
| **Tipo de celda/Tecnología** | **TAC** | **ECI** | **eNB ID** | **Physical Cell ID (PCI)** |
| ** ** | ** ** | ** ** | ** ** | ** ** |
| **EARFCN DOWN/UP** | **FREQ DOWN/UP** | **BANDA** | **FDD/TDD** |  |
| ** ** | ** ** | ** ** | ** ** |  |
| **Parámetros de Radiofrecuencia** |  |  |  |  |
| **RSSI** | **RSRP** | **RSRQ** | **SINR** | **ASU** |
| ** ** | ** ** | ** ** | ** ** | ** ** |
| **Posicionamiento terminal** |  |  |  |  |
| **Latitud** | **Longitud** |  |  |  |
| ** ** | ** ** |  |  |  |
| **Posicionamiento torre** |  |  |  |  |
| **Latitud** | **Longitud** |  |  |  |
| ** ** | ** ** |  |  |  |
| **Rendimiento de la red privada celular** |  |  |  |  |
| **Velocidad del downlink** | **Velocidad del uplink** | **Tiempo del ping** | **Jitter** |  |
|   |   |   |   |  |
| **Otros parámetros importantes** |  |  |  |  |
| **APN** | ** ** |  |  |  |
| **IMSI** | ** ** |  |  |  |

[image1]: img/reto4_image1.png