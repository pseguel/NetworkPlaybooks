# Ejemplos de Playbooks Ansible para Networking

## Pre-requisitos

Ya que Ansible utiliza conexiones SSH para conectarse
a los dispositivos, se necesita cumplir con algunos 
requisitos.

### IOS-XR

#### Verificar que instalación de paquetes k9 security 


Usar `show install active` y buscar paquetes "k9".


#### Verificar que un par de llaves RSA exista

De no existir llaves RSA, usar el comando
`crypto key generate rsa command` para generarlas.

#### Configurar el servidor SSH

Los siguientes comandos habilitan NETCONF y SSH:

    netconf agent tty
    !
    netconf-yang agent
    ssh
    !
    ssh server session-limit 10
    ssh server v2
    ssh server netconf vrf default

#### Autenticación basada en llaves a dispositivos IOS-XR

Para poder usar autenticación sin passwords en IOS-XR se deben
seguir varios pasos. En particular IOS-XR usa llaves en formato base64.
Se puede usar la herramienta *base64* en Linux y MacOS. Luego se debe copiar la llave al dispositivo e importarlo.

Generación de llaves en la máquina local (laptop):

    $ ssh-keygen -f id_rsa -q -N ""
    
    $ ls id_rsa* | grep id_rsa.pub
	id_rsa.pub

	$ cut -d" " -f2 id_rsa.pub | base64 -d > id_rsa_pub.b64

	$ ls -la | grep b64
	-rw-rw-r--  1 cisco cisco   535 Aug  6 10:43 id_rsa_pub.b64

En MacOS el comando `base64` es `base64 -D`.

Copiar e importar la llave:

	scp cisco@172.32.10.17:/disk0:/id_rsa_pub.b64 id_rsa_pub.b64
	
Validar que la llave está importada:

	show crypto key authentication rsa
	

