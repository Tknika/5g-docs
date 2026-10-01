  
**CONFIGURACIÓN DE LAS SIMs DE SYSMOCOM**

	Pasos para instalar el programa pySIM ([https://github.com/osmocom/pysim](https://github.com/osmocom/pysim)):

* Descargamos el código fuente a una carpeta local (en el ordenador en el que vayamos a conectar el lector de tarjetas SIM por USB):  
  * git clone [https://github.com/osmocom/pysim](https://github.com/osmocom/pysim)  
* Nos movemos a la carpeta correspondiente:  
  * cd pysim  
* Creamos un entorno virtual de Python (Virtual Environment) para aislar las dependencias y lo activamos:  
  * sudo apt-get install \--no-install-recommends pcscd libpcsclite-dev python3 python3-setuptools python3-pyscard python3-pip  
  * sudo apt install python3.8-venv  
  * python3 \-m venv venv  
  * source venv/bin/activate  
  * Nos aseguramos de que aparece el entorno activado (venv entre paréntesis) ![][image1]  
* Instalamos las dependencias definidas por el proyecto en el fichero requirements.txt:  
  * pip install \-r requirements.txt  
* Ejecutamos la shell del programa  
  * ./pySim-shell.py \-p 0 (el parámetro 0 es importante si se tiene más de un lector conectado en el ordenador)  
* Antes de nada, vamos a verificar que el ADM de la SIM introducida es la correcta:  
  * verify\_adm 38235251  
    * Si el comando no devuelve a nada, es que el ADM es correcto


  OPCIONES PARA PROGRAMAR:

  [https://osmocom.org/projects/pysim/wiki/PySim-prog](https://osmocom.org/projects/pysim/wiki/PySim-prog)


  apt install python3.12-venv


  

  

[image1]: img/sysmocom_image1.png