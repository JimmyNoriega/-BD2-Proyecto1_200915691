><img src="https://upload.wikimedia.org/wikipedia/commons/4/4a/Usac_logo.png" alt="drawing" width="75">
>
>Universidad San Carlos de Guatemala
>
>Facultad de Ingeniería 
>
>Escuela de Ciencias y Sistemas 
>
>Primer Semestre, 2022
>
>Laboratorio de Redes de Computadoras 1 Sección *N Impares*

### Grupo No.2

Integrantes:

| Nombre                               | Carnet    | Cliente* | 
| ------------------------------------ | --------- | -------- |
| <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRH6Uyi30Ty2WkMb0ZjuFLoXmkRwrrMObm-X2zztWtGbOgyA-i7mFzuiSKltN14HLAJDVM&usqp=CAU" alt="drawing" width="20"> &nbsp;Jimmy Yorbany Noriega Chávez         | 200915691 |  1       |
|  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQvke8Pr8T6xz52yM8v0ieg0oQy9L9SwfkO4hy4IKoRpxyQBKSGUWto7sWmzj9YYgm1VzU&usqp=CAU" alt="drawing" width="20"> &nbsp; Melyza Alejandra Rodríguez Contreras | 201314821 |  2       |
| <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRH6Uyi30Ty2WkMb0ZjuFLoXmkRwrrMObm-X2zztWtGbOgyA-i7mFzuiSKltN14HLAJDVM&usqp=CAU" alt="drawing" width="20"> &nbsp; Romael Isaac Pérez Godinez           | 201213545 |  3       |
| <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRH6Uyi30Ty2WkMb0ZjuFLoXmkRwrrMObm-X2zztWtGbOgyA-i7mFzuiSKltN14HLAJDVM&usqp=CAU" alt="drawing" width="20"> &nbsp; Josué Alfredo González Caal          | 201602489 |  4       |

> \* ***Nota:*** El apartado ***Cliente***, en la tabla anterior, identifica a cada miembro del grupo en la sección ***Conexión entre miembros del grupo*** presentada más adelante.

# Tarea No. 3

<div id='content'/>

## Contenido

1. [Configuración de la red privada](#id1)
2. [Conexión entre miembros del grupo](#id2)
3. [Configuración de _openVPN_ ](#id3)
4. [Grupo IAM](#id4)
5. [Máquina Virtual](#id5)

<div id='id1'/>

## 1. Configuración de la red privada  [ ⇧](#content)

Configuración de red ***VPN*** en instancia de máquina virtual.

Comandos utilizados: 

```sh
sudo wget https://cubaelectronica.com/OpenVPN/openvpn-install.sh

sudo bash openvpn-install.sh
```
- Configuración de ***IP***.

![ConfiguracionVPN](/images/config1.jpg "Configuración IP")

- Configuración de puerto y protocolo.

![ConfiguracionVPN](/images/config2.jpg "Configuración Puerto y Protocolo")

- Configuración de ***DNS***.

![ConfiguracionVPN](/images/config3.jpg "Configuración DNS")

- Generación de archivos ***.ovpn*** para conexión con clientes.

![ConfiguracionVPN](/images/config4.jpg "Generación de archivos OVPN")

<div id='id2'/>

## 2. Conexión entre miembros del grupo [ ⇧](#content)

Conexión de cada uno de los miembros del equipo con el resto de integrantes. 

### Cliente 1
```sh
IP: 10.8.0.2
```
![Client1IP](/images/ipJimmy.jpg "Client1 IP")

![Client1Ping](/images/pingJimmy.jpg "Client1 Ping")

### Cliente 2
```sh
IP: 10.8.0.3
```
![Client2IP](/images/melyza4.png "Client2 IP")

![Client2Ping](/images/melyza1.png "Client1 Ping")

![Client2Ping](/images/melyza2.png "Client1 Ping")

![Client2Ping](/images/melyza3.png "Client1 Ping")

### Cliente 3
```sh
IP: 10.8.0.4
```

### Cliente 4
```sh
IP: 10.8.0.5
```
![Client4IP](/images/201602489JosueGonzalezpingvpn.png "Client4 IP")

<div id='id3'/>

## 3. Configuración de _openVPN_  [ ⇧](#content)

- Descarga de software ***openVPN*** desde su sitio oficial.

```sh
https://openvpn.net/vpn-client/
```

![InstalacionOpenVPN](/images/open1.png "Descarga openVPN")

![InstalacionOpenVPN](/images/open2.png "Archivo openVPN")

- Ejecución del asistente de instalación

![InstalacionOpenVPN](/images/open3.png "Asistente")

![InstalacionOpenVPN](/images/open4.png "Asistente")

![InstalacionOpenVPN](/images/open5.png "Asistente")

![InstalacionOpenVPN](/images/open6.png "Asistente")

![InstalacionOpenVPN](/images/open7.png "Asistente")


- Ejecución del software instalado

![InstalacionOpenVPN](/images/open8.png "Ejecución")

- Conexión a servidor por medio de archivo generado

![InstalacionOpenVPN](/images/open9.png "Conexión")

![InstalacionOpenVPN](/images/open11.png "Conexión")

![InstalacionOpenVPN](/images/open10.png "Conexión")

![InstalacionOpenVPN](/images/open12.png "Conexión")

> \* ***Nota:*** El firewall debe estar desactivado para poder llevar a cabo la comunicación.
> 
> ![Firewall](/images/firewall.png "Firewall")

<div id='id4'/>

## 4. Grupo IAM [ ⇧](#content)
Grupo de ***IAM*** con todos los miembros del grupo.

![GrupoIAM](/images/iam.jpg "Grupo IAM")

<div id='id5'/>

## 5. Máquina virtual [ ⇧](#content)

Creación de instancia de máquina virtual en ***Google Cloud Platform***

![Virtual](/images/mv1.png "Maquina Virtual")

![Virtual](/images/mv2.png "Maquina Virtual")

![Virtual](/images/mv3.png "Maquina Virtual")

![Virtual](/images/instanciaVM.jpg "Maquina Virtual")

Resumen de características:
|Característica|Valor|
|--|--|
|**Plataforma**| <img src="https://cloud.google.com/_static/cloud/images/social-icon-google-cloud-1200-630.png?hl=es-es" alt="drawing" width="150"><br>Google Cloud Platform |
|**Tipo de instancia**|e2-small|
|**Sistema operativo**|<img src="https://anthoncode.com/wp-content/uploads/2019/01/ubuntu-logo-png.png" alt="drawing" width="135"><br>Ubuntu|
|**Versión**| 18.04 LTS|
|**Espacio en disco**| 10 GB|
|**Memoria RAM**| 2 GB|

> Adicionalmente se crearon dos reglas de ***firewall***, una de entrada y una de salida como se observa a continuación.
> 
> **Regla de entrada:**
> ![FirewallRules](/images/firewallvmin.png "Regla de Firewall - Entrada")
> **Regla de salida:**
> ![FirewallRules](/images/firewallvmout.png "Regla de Firewall - Salida")
