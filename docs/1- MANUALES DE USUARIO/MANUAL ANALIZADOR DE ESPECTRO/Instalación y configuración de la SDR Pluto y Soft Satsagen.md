

**Manual de instalación y configuración de la SDR Pluto y Soft Satsagen**

**Instalación de la SDR Pluto para uso con Windows:**

En primer lugar, antes de conectar la SDr al PC será necesario instalar los drivers:  
Driver para windows:  
[**PlutoSDR-M2k-USB-Drivers.exe**](https://github.com/analogdevicesinc/plutosdr-m2k-drivers-win/releases/download/v0.9/PlutoSDR-M2k-USB-Drivers.exe)

Una vez instalados los drivers, se conecta la SDR al PC y comprobamos que Windows reconoce el dispositivo y lo identifica.

**Instalación del sofware Satsagen para uso con Windows:**

Se procede a la descarga del software de la página:

[**http://www.albfer.com/satsagen-download-page/\#content**](http://www.albfer.com/satsagen-download-page/#content)

Y a continuación se ejecuta el instalador:

**![][image1]**

Se procede a su encendido (Pulsar “Power” y después “Spectrum”):

**![][image2]**

**![][image3]**

**Ampliación de frecuencias hasta 6GHz:**

1. Si aún no lo tiene, descargue el software de emulación de terminal PuTTY de  [putty.org](http://putty.org/) .  
2. Conecte su PlutoSDR en el puerto USB.  
3. Abra el Administrador de dispositivos de Windows y expanda la entrada Puertos (COM y LPT). Tome nota de qué puerto COM está utilizando la consola serie PlutoSDR. En la captura de pantalla, el nuestro está usando COM7. Cierre el administrador de dispositivos después.

![][image4]

4. Abra PuTTY y seleccione el botón 'serie'.  
5. En 'Línea serie', escriba el puerto COM que está utilizando PlutoSDR. En nuestro caso escribimos COM7.  
      
   ![][image5]  
6. Presiona Abrir y deberías ser recibido con una pantalla de inicio de sesión.

7. Inicie sesión con las credenciales de usuario: root, contraseña: analog.

![][image6]

**¿Cómo conocer la versión?.** Escribimos por comando:

**\#fw\_printenv attr\_name**

respuesta: attr\_name=compatible

**\# fw\_printenv attr\_val**

**respuesta: attr\_val=ad9364**

![][image7]

![][image8]  
Para cambiarlo a otra opción (ad9361 por ejemplo):  
\# **fw\_setenv attr\_name compatible**  
\# **fw\_setenv attr\_val ad9361**

**BÚSQUEDA DE FRECUENCIAS EN EL ESPECTRO:**  
Búsqueda de la radio o otra cosa:

Búsqueda de wifi en 2,4GHz:

![][image9]

Búsqueda de wifi en 5GHz:

![][image10]

[image1]: img/image1.png

[image2]: img/image2.png

[image3]: img/image3.png

[image4]: img/image4.png

[image5]: img/image5.png

[image6]: img/image6.png

[image7]: img/image7.png

[image8]: img/image8.png

[image9]: img/image9.png

[image10]: img/image10.png