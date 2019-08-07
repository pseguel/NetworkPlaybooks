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

 
