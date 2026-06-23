**MANUAL**

**[1\. Configuración inicial:	2](#configuración-inicial:)**

[**2\. Información básica:	2**](#información-básica:)

[**3\. Configuración:	3**](#configuración:)

[3.1 Configuración radio	3](#3.1-configuración-radio)

[3.2 Configuración conexión a core	3](#3.2-configuración-conexión-a-core)

1. # **Configuración inicial:** {#configuración-inicial:}

Para acceder a la radio desde la LAN: accedemos desde 192.168.150.7  
Configuramos la WAN \-\> DHCP y recibimos una IP del router: 192.168.168.225  
(podemos acceder desde nuestra red por esta IP también)  
**![][image1]**

2. # **Información básica:** {#información-básica:}

Acceso rápido para el estado del gNB y de los UE conectados.

**![][image2]**

3. # **Configuración:** {#configuración:}

## ***3.1 Configuración radio*** {#3.1-configuración-radio}

Para configurar la radio accedemos a “Quick Setting”  
![][image3]

Configurar parámetros radio y del gNB

* Banda de trabajo  
* Ancho de banda  
* Frecuencia (ARFCN)  
* PCI: Physical Cell ID

## ***3.2 Configuración conexión a core*** {#3.2-configuración-conexión-a-core}

Para configurar la conexión con el core:   
NR Setting → Advanced → CU   
![][image4]

1- Egtpu Local IP: Agregamos la IP de la radio  
2- Le damos al “+” y conbfiguramos:![][image5]  
AMF IP: IP del core  
NGAP Local IP: IP de la radio  
PLMN: Elegimos la misma que tenemos en el core.   
\*Si no aparece tendremos que ir a pestaña PLMN  
Open→ Add  
Aquí también podemos configurar los slices  
![][image6]

*Podemos comprobar la conexión en la pestaña “Basic info”*

[image1]: img/manual_image1.png

[image2]: img/manual_image2.png

[image3]: img/manual_image3.png

[image4]: img/manual_image4.png

[image5]: img/manual_image5.png

[image6]: img/manual_image6.png