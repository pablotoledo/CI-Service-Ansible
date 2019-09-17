Under construction!

# CI-Service-Ansible
This project is a continuation of [CI-Service](https://github.com/pablotoledo/CI-Service). And the main goal is provide a minimal DevOps environment to learn the 

## Architecture

The Ansible playbook defined will create an single environment with:
 - Gitlab CE
 - Jenkins
 - Nexus 3
 - SonarQube
 - K8s Slave

## Requirements
### Vagrant
In case you need to instance the cluster in a local environment, there is a Vagrantfile defined to facilitate the local instalation.
There are some vagrant plugins you will need to install before run "vagrant up":
	- VirtualBox Oracle VM VirtualBox Extension Pack
	- vagrant plugin install vagrant-hostmanager
	- vagrant plugin install vagrant-vbguest

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
|controller.ciservice.int|192.168.60.105|vagrant:vagrant|

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

### Author
    Pablo Toledo

### Reconocimientos a terceros
	Algunos roles son propiedad intelectual de otros autores:
		[geerlingguy.gitlab](https://github.com/geerlingguy/ansible-role-gitlab) 