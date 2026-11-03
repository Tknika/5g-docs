

|  |
| :---- |
| GUÍA DE CONFIGURACIÓN · VERSIÓN 2.0 **Handover Xn entre gNB Vankom vkScell-g3 con núcleo EllaCore** Procedimiento unificado para movilidad intra-frecuencia con audio y vídeo en tiempo real Fuentes: Manual vkScell-g3 V1.0.0 y Neighbor Cell Configuration Guide (Vankom, 26/06/2026) Firmware de referencia: 3181 o superior (probado por Vankom en 3184\) Interfaz de gestión: LMT (Local Maintenance Terminal) Versión 2.0  \|  13 de octubre de 2026 |

**Índice**

[1\. Principio de funcionamiento	3](#1.-principio-de-funcionamiento)

[2\. Esquema de conexionado y datos a planificar	3](#2.-esquema-de-conexionado-y-datos-a-planificar)

    - [Datos a recopilar antes de empezar	3](#datos-a-recopilar-antes-de-empezar)

[3\. Procedimiento de configuración	4](#3.-procedimiento-de-configuración)

    [3.1 Comprobaciones previas	4](#3.1-comprobaciones-previas)

    [3.2 Interruptores de medida (CU)	4](#3.2-interruptores-de-medida-\(cu\))

    [3.3 Eventos de medida intra-frecuencia	4](#3.3-eventos-de-medida-intra-frecuencia)

    [3.4 Vecina intra-frecuencia (base del NG handover)	5](#3.4-vecina-intra-frecuencia-\(base-del-ng-handover\))

    [3.5 Relación Xn entre gNB (PeerGnb)	5](#3.5-relación-xn-entre-gnb-\(peergnb\))

    [3.6 Reinicio y verificación	5](#3.6-reinicio-y-verificación)

[4\. Ajustes para audio y vídeo en tiempo real	6](#4.-ajustes-para-audio-y-vídeo-en-tiempo-real)

[Anexo A. Puntos a confirmar con Vankom	6](#anexo-a.-puntos-a-confirmar-con-vankom)

[Anexo B. Cambios respecto a la versión 1.0	6](#anexo-b.-cambios-respecto-a-la-versión-1.0)

# **1\. Principio de funcionamiento** {#1.-principio-de-funcionamiento}



Según Vankom, el modo de handover por defecto de estos gNB es el **NG handover** (el traspaso se coordina a través del core por la interfaz N2) y el **handover Xn** se configura sobre esa misma base. Por eso el orden es: **(1)** medidas y vecinas, comunes a ambos modos, y **(2)** alta de la relación Xn entre los dos gNB. Sin medidas ni vecinas no funciona ninguno de los dos.

**Requisitos:** firmware 3181 o superior; ambas celdas activas con la misma banda, ARFCN SSB y SCS; EllaCore con los dos gNB registrados (NG Setup correcto) y con handover N2 permitido entre ellos. Todo el procedimiento se aplica **de forma simétrica** en gNB-A y gNB-B.

# **2\. Esquema de conexionado y datos a planificar** {#2.-esquema-de-conexionado-y-datos-a-planificar}

![gNB-A y gNB-B conectados al core EllaCore por N2/N3 y entre sí por Xn][image1]

*gNB-A y gNB-B (misma frecuencia) conectados al core EllaCore por N2/N3 y entre sí por Xn. El UE se desplaza entre ambas celdas mientras transmite audio/vídeo.*

<a id="datos-a-recopilar-antes-de-empezar-datos-a-recopilar-antes-de-empezar"></a>
## **Datos a recopilar antes de empezar** {#datos-a-recopilar-antes-de-empezar}

| Parámetro | gNB-A | gNB-B | Observación |
| :---- | :---- | :---- | :---- |
| gNB ID | 1111 | 2222 | Distinto en cada gNB (el valor por defecto es 0, en Quick Start → Base Station Parameters). Se usa como Gnb\_id en el apartado 3.5 |
| PCI | 1 | 2 | Distinto en cada celda |
| Cell ID (NRCellIdentity) | 1111 | 2222 | Distinto en cada celda |
| PLMN / TAC | 00101/1 | 00101/1 | Iguales a lo configurado en EllaCore |
| Banda / SSB ARFCN / SCS | 78/2305,25/30 | 78/2305,25/30 | Idénticos en ambas celdas. Confirmar la banda real en Overview → Base Station Capabilities (el manual declara N41/N78) |
| IP eGTPU (N3) / NGAP (N2) | 192.168.99.99 | 192.168.101.101 | Con ping al core |
| IP XNAP (Xn) | 192.168.99.99 | 192.168.101.101 | Alcanzable entre ambos gNB |
| IP del AMF (EllaCore) | (común a ambos)192.168.168.205 | 192.168.168.205 | AMF Server Address |

# **3\. Procedimiento de configuración** {#3.-procedimiento-de-configuración}

<a id="31-comprobaciones-previas-31-comprobaciones-previas"></a>
## **3.1 Comprobaciones previas** {#3.1-comprobaciones-previas}

* Versión de software 3181 o superior (Overview → Base Station Information).

* Celdas activadas en ambos gNB (Overview → Community Information) y datos de la tabla anterior sin duplicados donde deben ser únicos.

* Ping entre las IP XNAP de ambos gNB y NG Setup correcto con EllaCore.

<a id="32-interruptores-de-medida-cu-32-interruptores-de-medida-cu"></a>
## **3.2 Interruptores de medida (CU)** {#3.2-interruptores-de-medida-(cu)}

Configuration Management → Base Station → CU → Power Control Information → Default Measurement Parameter Configuration during UE Initial Access

Habilitar “Measurement Switch”, para ello nos desplazamos en el menú de la izquierda en “Configuration/GNB/CU/OperatorInfo/DEFAULT\_MEAS\_TO\_CONFIG:

![][image2]

Poner a **1**: A1 Measurement Switch (Measurement\_A1), A2 Measurement Switch (Measurement\_A2) y el interruptor de **A3 de misma frecuencia** (Intra\_Meas\_A3). Pulsar **Save and Issue**.

![][image3]

Estos interruptores viajan al UE en la segunda reconfiguración RRC tras el acceso. **A2 debe estar activado y entregarse en el acceso inicial** (requisito de Vankom). Alternativa validada por Vankom: A1 y A2 en el acceso inicial y A3 en «Measurement Parameter Configuration after A2 Measurement Received», de modo que A3 solo se entrega cuando el UE informa A2. Se recomienda la primera opción (A3 en el acceso inicial) para que la preparación del handover no dependa de una reconfiguración en el borde de celda (criterio propio, no de Vankom). A4 y B1 no son necesarios (son de inter-frecuencia e inter-RAT).

<a id="33-eventos-de-medida-intra-frecuencia-33-eventos-de-medida-intra-frecuencia"></a>
## **3.3 Eventos de medida intra-frecuencia** {#3.3-eventos-de-medida-intra-frecuencia}

Neighborhood Management → Neighborhood Configuration → MeasControlList → MeasControl\[name=meas1\]

Iremos al menú de la izquierda a “Neighbor Cell” y luego arriba a la derecha pulsamos sobre “Configuration”:

![][image4]

Se nos abre otro menú interno:

![][image5]

Una vez aquí meterse en “MeasControlList/MeasControl/EventConfig”

Cada MeasControl corresponde a un PLMN: comprobar que su PLMNList es la de la red. 

Para intra-frecuencia, **IntraFreq se deja con los valores por defecto** y no hay que tocar InterFreq. Después, en **EventConfig**:

| Evento | Ruta (bajo EventConfig) | Parámetro | Ejemplo Vankom | Significado |
| :---- | :---- | :---- | :---- | :---- |
| A1 | A1Event → TriggerQuantityThreshold | ThresholdRSRP | 96 | Servidora mejor que \-60 dBm (156 \- 60\) |
| A2 | A2Event → TriggerQuantityThreshold | ThresholdRSRP | 76 | Servidora peor que \-80 dBm (156 \- 80\) |
| A3 | A3Event → TriggerQuantityOffset | OffsetRSRP | 5 | Vecina 5 dB mejor que la servidora (valor en dB, rango \-30 a 30\) |

Pondremos esos valores en:

![][image6]

![][image7]

![][image8]

Cambiamos los valores según la tabla anterior:

![][image9]

Este se deja con el mismo valor:

![][image7]

Por último:

![][image10]

Vankom indica que son valores estimados que no tienen en cuenta histéresis ni offsets: ajustarlos al entorno radio. El parámetro TriggerQuantity de EventConfig viene por defecto en RSRP, y el resto de parámetros de EventConfig pueden dejarse por defecto.

**Importante: Variante SINR.** El evento A3 no usa «Threshold» sino «Offset»: la v1.0 de este manual citaba ThresholdSINR para A3, lo cual era incorrecto. Para basar A3 en SINR habría que poner TriggerQuantity \= SINR y configurar OffsetSINR (rango \-30 a 30\) en lugar de OffsetRSRP. Esa variante **no aparece en la guía de Vankom** (solo documenta RSRP) ni se conoce la unidad de OffsetSINR. Recomendación: validar primero todo con RSRP y pedir a Vankom confirmación por escrito antes de pasar a SINR (Anexo A).

<a id="34-vecina-intra-frecuencia-base-del-ng-handover-34-vecina-intra-frecuencia-base-del-ng-handover"></a>
## **3.4 Vecina intra-frecuencia (base del NG handover)** {#3.4-vecina-intra-frecuencia-(base-del-ng-handover)}

Neighborhood Management → Neighborhood Configuration → NeighborList → IntraFreqCell

Nos metemos en el menú izquierdo sobre “Neighbor Cell”, luego en “Configuration” y dentro de él, sobre “NeighborList” y pinchamos sobre “IntrafreqCell” y comprobamos que:

1. **Activar SIB3:** X\_VENDOR\_SIB3\_ENABLED \= 1 (Vankom exige SIB3/SIB4/SIB5 activos; SIB4 y SIB5 pertenecen a InterFreqCell e InterRATCell y aquí no se usan).

![][image11]

Luego le damos al “+” en “IntrafreqCell” para añadir la o las celdas vecinas:

![][image12]

2. Pulsar **\[+\]** y rellenar la celda del otro gNB: **PLMN, CID (NRCellIdentity), SCS, PCI y TAC**. El resto (QOffsetCell, QRxLevMinOffsetCell, QQualMinOffsetCell, en\_gNB\_ID\_bit\_len) puede quedar por defecto. Aceptar con OK.

![][image13]

Ponemos nuestros valores y confirmamos.

3. En la vecina creada, **NRFreqInfo → NRTDDInfo → NRFreqBandList → NRFreqBandItem → NRFreqBand**: número de banda (el ejemplo de Vankom usa 78).

4. En la vecina, **MTC → MeasTimingItem**: SSBFrequency (idéntica a la propia, por ser intra-frecuencia) y SubcarrierSpacing (30 kHz en el ejemplo).

5. Pulsar **Save and Deliver**. Repetir en el otro gNB apuntando de vuelta. Se pueden añadir varios PLMN a la misma vecina con \[+\].

<a id="35-relacion-xn-entre-gnb-peergnb-35-relacion-xn-entre-gnb-peergnb"></a>
## **3.5 Relación Xn entre gNB (PeerGnb)** {#3.5-relación-xn-entre-gnb-(peergnb)}

Configuration Management → Base Station → CU → Base-station access control → PeerGnb → Gnb\_nbr\_list

Nos desplazamos por el menú izquierdo “Configuration/GNB/CU/FAPControl/PeerGnb/Gnb\_nbr\_list” y pinchamos sobre él:

![][image14]

1) Poner Gnb\_nbr\_list\_size al número de vecinos Xn (rango 0 a 32; **1** en el ejemplo de Vankom). Esto habilita Xn.

![][image15]

2) Pulsar **\[+\]** y crear una entrada Gnb\_nbr\_info con los datos del **otro** gNB:

![][image16]

| Parámetro | Valor | Observación |
| :---- | :---- | :---- |
| Gnb\_id | gNB ID del vecino | Vankom lo describe como «Cell ID»; el parámetro es el gNB ID (ejemplo: 33001). Ver Anexo A |
| PLMNID | PLMN del vecino | Ejemplo: 46001 |
| peer gNB server address (MyAddr) | IP XNAP del vecino | Ejemplo Vankom: 192.169.11.67 (no copiar) |
| TAC | TAC del vecino | Ejemplo: 62 |
| Gnb\_type | 1 | Valor del ejemplo; significado no documentado |
| Xn\_ho\_status | 1 | Valor del ejemplo; significado no documentado |
| NumOfPeerXNAPInstanceConfig | 1 | Rango 1 a 4; valor del ejemplo |

Pulsar **Save and Issue** y repetir en el otro gNB con los datos del primero. La entrada muestra también Xn\_connection\_status (7 en el ejemplo, sin documentar); anotar su valor tras el reinicio y confirmar su significado con Vankom (Anexo A).

![][image17]

<a id="36-reinicio-y-verificacion-36-reinicio-y-verificacion"></a>
## **3.6 Reinicio y verificación** {#3.6-reinicio-y-verificación}

1. Reiniciar ambos gNB (Overview → Restart Device → OK). El manual V1.0.0 lo exige para los cambios de parámetros de base; la guía de Vankom no lo precisa para vecinas y Xn, por lo que se recomienda hacerlo igualmente.

2. **Vecinas:** en Neighborhood Management → Neighborhood Information, cada gNB debe listar al otro como vecino 5G con PCI, CID y TAC correctos.

3. **Xn:** la entrada de PeerGnb debe permanecer guardada tras el reinicio; anotar el valor de Xn\_connection\_status (7 en el ejemplo de Vankom).

4. **Medidas:** con un terminal con herramienta de logging, comprobar que la segunda RRCReconfiguration incluye A1, A2 y A3 (es el método de validación de Vankom).

5. **Handover:** con el UE transmitiendo, desplazarlo entre ambas celdas y revisar Performance Management → Counter (contadores de handover) y KPI **K920** (éxito de handover intra-sistema).

# **4\. Ajustes para audio y vídeo en tiempo real** {#4.-ajustes-para-audio-y-vídeo-en-tiempo-real}

* **Offset de A3:** empezar con 5 dB (ejemplo de Vankom). Bajarlo si la señal se degrada antes del traspaso; subirlo si hay ping-pong entre celdas. Mantener solape de cobertura suficiente entre ambas celdas.

* **QoS:** el 5QI de los flujos de audio/vídeo lo define EllaCore; comprobar en Configuration Management → QOS que el gNB tiene un perfil con ese 5QI (el LMT trae perfiles GBR 5QI 1 a 4 y 82, y Non-GBR).

* **PDCP/temporizadores de descarte:** dejar por defecto y tocarlos solo si se mide latencia excesiva.

# **Anexo A. Puntos a confirmar con Vankom** {#anexo-a.-puntos-a-confirmar-con-vankom}

1. ¿Se soporta A3 basado en SINR? Valores del enum TriggerQuantity y unidad de OffsetSINR (la guía solo muestra RSRP).

2. Significado y valores válidos de Xn\_ho\_status, Xn\_connection\_status, Gnb\_type y NumOfPeerXNAPInstanceConfig.

3. Gnb\_id: confirmar que es el gNB ID (Quick Start) del vecino y su relación con en\_gNB\_ID\_bit\_len.

4. Criterio de selección entre Xn y NG handover cuando ambos están configurados, y comportamiento si falla Xn.

5. Dónde se ajustan histéresis y time-to-trigger de los eventos (aparecen en la traza RRC, no en la guía).

6. Si es necesario reiniciar tras dar de alta vecinas y Xn.

7. Valores X\_VENDOR\_NR\_STATUS y X\_VENDOR\_HO\_STATUS de la vecina (2 y 1 en el ejemplo) y si deben modificarse.

8. Banda real del equipo: el manual declara N41/N78 y el LMT mostró un rango N78 (3300-3600 MHz).

# **Anexo B. Cambios respecto a la versión 1.0** {#anexo-b.-cambios-respecto-a-la-versión-1.0}

| Tema | Versión 1.0 | Versión 2.0 (según guía de Vankom) |
| :---- | :---- | :---- |
| Parámetro de A3 | ThresholdSINR en A3Event → TriggerQuantityThreshold | A3 usa TriggerQuantityOffset (OffsetRSRP / OffsetRSRQ / OffsetSINR) |
| Métrica del evento | Selector supuesto | Confirmado: parámetro TriggerQuantity, por defecto RSRP |
| SIB3 | No mencionado | X\_VENDOR\_SIB3\_ENABLED \= 1 en IntraFreqCell |
| Configuración Xn | Solo CU\_XNAP-IP Address | Alta del vecino en CU → PeerGnb → Gnb\_nbr\_list |
| Modo de handover | No indicado | NG handover es el modo por defecto; Xn se añade encima |
| gNB ID | No mencionado | Debe ser distinto en cada gNB |
| Banda | N77 | A confirmar: el equipo declara N41/N78 |

[image1]: img/handover_vankom_image1.png

[image3]: img/handover_vankom_image3.png

[image4]: img/handover_vankom_image4.png

[image5]: img/handover_vankom_image5.png

[image6]: img/handover_vankom_image6.png

[image7]: img/handover_vankom_image7.png

[image8]: img/handover_vankom_image8.png

[image9]: img/handover_vankom_image9.png

[image10]: img/handover_vankom_image10.png

[image11]: img/handover_vankom_image11.png

[image12]: img/handover_vankom_image12.png

[image13]: img/handover_vankom_image13.png

[image14]: img/handover_vankom_image14.png

[image15]: img/handover_vankom_image15.png

[image16]: img/handover_vankom_image16.png

[image17]: img/handover_vankom_image17.png
