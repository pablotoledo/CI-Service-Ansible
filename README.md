# CI-Service-Ansible

Este proyecto es una continuación de [CI-Service](https://github.com/pablotoledo/CI-Service) y nace como evolución para perfeccionar el alcance del anterior proyecto. También trata de ejemplificar un sistema de integración contínua básico, pero, partiendo de que el aprovisionamiento de servicios se haga con Ansible, ofreciendo cierto grado de configuración de cara a facilitar la implantación de sistemas productivos basados en este modelo.

## Arquitectura (visión a alto nivel)
En CI-Service-Ansible se diseña siguiendo estos principios:

 - **Aprovisionamiento de infraestructura : Vagrant**: Mediante el uso de Vagrant se definirá un cluster de máquinas virtuales, que facilitarán una infraestructura limpia sobre la cual ejecutar el aprovisionamiento de servicios con Ansible.
 - **Aprovisionamiento de servicios : Ansible**: Mediante el uso de roles se definirá el criterio de instanciación de servicios en los distintos nodos del cluster, la intercomunicación de dichos servicios y la definición de una serie de ejemplos que permitan jugar y probar el funcionamiento de la plataforma. Los servicios instanciar serán los siguientes:
	 - GitLab CE
	 - Jenkins LTS
	 - Nodo slave en CentOS 7 para sentar las bases de una arquitectura de CI distribuida
	 - Nexus 3
	 - SonarQube


----------

## Listado de máquinas y credenciales
Las máquinas del cluster se han definido a nivel de red y credenciales de la siguiente forma:

|Hostname|IP|Usuario:Clave|
|--|--|--|
|jenkins.ciservice.int|192.168.60.100|vagrant:vagrant|
|gitlab.ciservice.int|192.168.60.101|vagrant:vagrant|
|sonarqube.ciservice.int|192.168.60.102|vagrant:vagrant|
|nexus.ciservice.int|192.168.60.103|vagrant:vagrant|
|slave.ciservice.int|192.168.60.104|vagrant:vagrant|

Al emplearse el plugin de vagrant-hostmanager se puede emplear desde la máquina host y desde los nodos del cluster tanto el hostname como la IP de la máquina virtual para acceder a cualquier nodo.

----------


# Como empezar

## Requisitos

### Requisitos de HW

 - CPU compatible con HiperV (Comprobar que el fichero /proc/cpuinfo contiene vmx ó svm)
 - El cluster declarado en Vagrant requiere de una disponibilidad de al menos 8 GB de RAM

### Requisitos de SW

 - Virtualbox : Como herramienta de virtualización para correr las máquinas del cluster
 - Vagrant : Como herramienta de definición declarativa de la infraestructura a instanciar
 - Ansible : Como herramienta de definición declarativa de los servicios a configurar en el cluster

## Iniciar CI-Service-Ansible

Tenemos 4 script para iniciar CI-Service-Ansible según las siguientes circunstancias:
### Sistema Operativo Windows

 - En el caso estandar ejecutamos "install-windows.bat"
 -  En caso de estár tras un firewall corporativo useramos "install-windows-withproxy.bat"
	 - Editamos el fichero incluyendo los datos del proxy corporativo
	 - Ejecutamos el script

### Sistema Operativo tipo Unix

 - En el caso estandar ejecutamos "install-unix.sh"
 -  En caso de estár tras un firewall corporativo useramos "install-unix-withproxy.sh"
	 - Editamos el fichero incluyendo los datos del proxy corporativo
	 - Ejecutamos el script


----------

### Autor
    Pablo Toledo