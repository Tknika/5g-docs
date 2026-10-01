

**CURSO INSTALACIÓN Y CONFIGURACIÓN DE REDES 5G**

**“Caso de uso:**   
**Retransmisión de eventos deportivos: gNB y UPF en San Mamés, Core en EiTB (Donostia)”**

**Situación:**

EiTB no solo produce contenidos en sus instalaciones, sino que también realiza **retransmisiones deportivas en directo**, por ejemplo partidos de fútbol en San Mamés.

En este escenario aparecen nuevos requisitos técnicos:

* Necesidad de **baja latencia** para vídeo en tiempo real.  
* Elevado tráfico de subida (uplink).  
* Evitar que todo el tráfico de usuario tenga que volver al Core central.  
* Mayor resiliencia y escalabilidad de la red.

Para cumplir estos requisitos, EiTB decide **separar el plano de control y el plano de usuario**, desplegando el **User Plane Function (UPF)** cerca del evento deportivo.

**Servicios del escenario:**  
La red debe dar servicio, al menos, a:

* **Terminal 1:**  
   Móvil del personal técnico del estadio.  
   Uso: comunicaciones y acceso a servicios corporativos.  
* **Terminal 2:**  
   Cámara de vídeo / router 5G para retransmisión en directo.  
   Uso: streaming de vídeo hacia la infraestructura de producción.

![][image1]  
**Imagen:** Red privada 5G para streaming deportivo

## 

## 

## 

## **Arquitectura de la red**

La red 5G se distribuye geográficamente del siguiente modo:

* **Core 5G (Open5GS sin UPF)**  
   Ubicación: instalaciones de EiTB en Donostia.  
   Funciones de control:

  * AMF  
  * SMF  
  * AUSF  
  * UDM  
  * NRF  
* **UPF (Open5GS)**  
   Ubicación: San Mamés (edge).  
   Función: encaminamiento del tráfico de usuario.

* **Radio gNB**  
   Ubicación: San Mamés.  
   Proporciona cobertura radio en el estadio.

* **VPN (Mikrotik)**  
   Interconecta:

  * Core 5G ↔ UPF  
     de forma segura a través de red IP.

## **Desarrollo del entrenamiento** 

A partir de una red privada 5G ya funcional (Día 1), se procederá a:

* Separar el **User Plane Function (UPF)** del Core.  
* Desplegar el UPF en una **ubicación remota**.  
* Asegurar la conectividad mediante una VPN.  
* Verificar el impacto de esta arquitectura en la latencia y el rendimiento.

## **Parámetros de configuración**

### **EQUIPO 1 – Core 5G (sin UPF)**

## Parámetros principales a revisar y adaptar:

* ## Dirección IP del Core.

* ## Interfaces N2 y N4.

* ## Asociación con SMF.

* ## Eliminación del UPF local.

* ## Definición de UPF remoto (IP, N4).

## 

### **EQUIPO 2 – UPF remoto**

* ## Dirección IP del UPF.

* ## Interfaz N4 hacia el SMF.

* ## Interfaz N3 hacia el gNB.

* ## Enrutamiento del tráfico de usuario.

* ## Salida hacia red local / Internet.

### **Parámetros a configurar en la VPN (Mikrotik)**

* ## Dirección IP local y remota.

* ## Tipo de VPN (IPsec / WireGuard).

* ## Rutas estáticas:

  * ## Core ↔ UPF

  * ## UPF ↔ gNB

* ## Comprobación de conectividad IP extremo a extremo.

### **Parámetros a revisar en la radio gNB**

* ## Dirección IP del AMF

* ## PLMN.

* ## TAC.

* ## gNB ID.

* ## Asociaciones N2 / N3.

### **1\. Esquema de red distribuida**

Realiza un **esquema lógico** donde se represente:

* Core 5G centralizado.  
* UPF en el edge.  
* gNB remoto.  
* VPN entre sedes.  
* Flujo del plano de control y del plano de usuario.

**Resultado esperado:**  
 Diagrama claro que muestre la separación CP / UP. 

### **2\. Separación del UPF**

Configura la red para que:

* El Core 5G deje de manejar tráfico de usuario.  
* El UPF remoto gestione el tráfico de datos.  
    
  .

### **3\. Verificación de funcionamiento**

Comprobar:

* Registro correcto del UE en red (NAS, AMF).  
* Establecimiento de sesión PDU.  
* Paso de tráfico IP a través del UPF remoto.

Herramientas recomendadas:

* Logs del Core y del UPF.  
* Ping desde el UE.  
* Traceroute.  
* Capturas de tráfico.

### **4\. Análisis de rendimiento y latencia**

* Medir latencia y velocidad con:  
  * UPF cercano (edge).  
* Comparar con:  
  * UPF centralizado (Día 1).

Registrar resultados en una **tabla comparativa**.

## **¿Qué pasa si…?**

Analiza y documenta el comportamiento de la red en los siguientes casos:

1. **Se pierde la VPN entre Core y UPF**  
   * ¿El UE sigue registrado?  
   * ¿Hay tráfico de datos?  
2. **Se detiene el UPF remoto**  
   * ¿Qué ocurre con la sesión PDU?  
   * ¿Qué mensajes aparecen en el SMF?  
3. **El gNB apunta a un UPF incorrecto**  
   * ¿Se registra el UE?  
   * ¿Hay conectividad IP?  
4. **Aumenta la latencia entre Core y UPF**  
   * Impacto en el servicio.  
   * Servicios más afectados (vídeo vs datos).

## **Conclusiones**

Responder y justificar:

* ¿Por qué es clave separar el UPF en escenarios de eventos?  
* ¿Qué ventajas aporta una arquitectura distribuida?  
* ¿Qué servicios se benefician más del edge computing?

## **EXTRA**

* Implementar un **radioenlace** (o simulación de enlace limitado) entre Core y UPF.  
* Repetir las pruebas observando el impacto en:  
  * Throughput.  
  * Latencia.  
  * Calidad del vídeo.

[image1]: img/reto2_image1.png