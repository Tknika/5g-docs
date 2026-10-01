***INSTALAR open5gs CURSO2025/2026***  
\*\*Si la máquina la creamos en proxmox confirmar que Processor→Type→host   
1-Instalamos docker y portainer  
Accedemos a [https://github.com/Tknika/5g-kutxa-ansible/tree/portainer](https://github.com/Tknika/5g-kutxa-ansible/tree/portainer)  
Ejecutamos los pasos indicados:  
	Instalamos ansible: sudo apt update && sudo apt install \-y ansible git  
	Instalamos docker y portainer:   
sudo ansible-pull \-U https://github.com/Tknika/5g-kutxa-ansible.git \--checkout portainer \-i localhost,  
reboot(para meterlo en el grupo)  
Comprobamos que está correcto: docker ps o https://localhost:9443

2-Instalamos open5gs  
Accedemos: [https://github.com/herlesupreeth/docker\_open5gs](https://github.com/herlesupreeth/docker_open5gs)

Descargamos su repositorio:  
Instalar git: sudo apt install git  
Clonamos repositorio: git clone [https://github.com/herlesupreeth/docker\_open5gs](https://github.com/herlesupreeth/docker_open5gs)

Descargamos las imágenes: (En este caso solamente open5gs, no descargamos IMS…)  
docker pull ghcr.io/herlesupreeth/docker\_open5gs:master  
docker tag ghcr.io/herlesupreeth/docker\_open5gs:master docker\_open5gs

docker pull ghcr.io/herlesupreeth/docker\_grafana:master  
docker tag ghcr.io/herlesupreeth/docker\_grafana:master docker\_grafana

docker pull ghcr.io/herlesupreeth/docker\_metrics:master  
docker tag ghcr.io/herlesupreeth/docker\_metrics:master docker\_metrics

Levantamos el docker compose que necesitemos:  
1- Accedemos al .env para realizar los cambios necesarios:   
MNC, MCC, TAC  
DOCKER\_HOST\_IP: La IP del PC donde estamos realizando la instalación  
Para aplicar los cambios: Guardar y ejecutar:   
set \-a   
source .env   
2-Para levantar un 5G completo levantaremos el fichero sa-deploy.yaml:  
	docker compose \-f sa-deploy.yaml up \-d  
Comprobamos que está correcto: Acceder a portainer y visualizar todos los contenedores levantados.

***ROAMING open5gs CURSO2025/2026***

Para poder trabajar con varias radios en la misma aula:  
Trabajamos con el core y la radio en un PLMN(Ej. 00110\) pero nos conectamos con un movil en la 00101

1-Conectamos core y radio (PLMN:00110)  
2-Agregamos en webui el usuario: 00101 …  
3-Configuramos el nrf.yaml:  
![][image1]

***SEPARAR UPF open5gs CURSO2025/2026***

PC dónde teníamos el UPF instalado:  
1-Copiamos el fichero sa-deploy.yaml y le llamamos core-sinUPF.yaml  
En el fichero core-sinUPF.yaml: 

- Comentamos o borramos toda la parte de upf:  
- Agregamos “ports” “"8805:8805/udp” en el SMF

EN el fichero .env: 

- DOCKER\_HOST\_IP=IP del core  
- UPF\_IP=IP del UPF  
- UPF\_ADVERTISE\_IP=IP del UPF				

Levantamos el docker compose que necesitemos:  
	docker compose \-f core-sinUPF.yaml up \-d

PC dónde tendremos el UPF instalado:  
1-Copiamos el fichero sa-deploy.yaml y le llamamos UPF2.yaml  
En el fichero UPF2.yaml: 

- Comentamos o borramos todo menos la parte de upf:   
- En network lo ponemos modo host  
- Borramos la parte de  sysctls:

En el fichero .env: 

- DOCKER\_HOST\_IP=IP del UPF  
- UPF\_IP=IP del UPF  
- UPF\_ADVERTISE\_IP=IP del UPF  
- SMF\_IP=IP del core

Levantamos el docker compose que necesitemos:  
	docker compose \-f UPF2.yaml up \-d

[image1]: img/open5gs_image1.png