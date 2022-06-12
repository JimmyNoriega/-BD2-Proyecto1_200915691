><img src="https://upload.wikimedia.org/wikipedia/commons/4/4a/Usac_logo.png" alt="drawing" width="75">
>
>Universidad San Carlos de Guatemala
>
>Facultad de Ingeniería 
>
>Escuela de Ciencias y Sistemas 
>
>Vacaciones Primer Semestre, 2022
>
>Laboratorio de Bases de Datos 2 Sección *N*
>
>Tutor: Jurgen Ramirez




Datos:

| Nombre                               | Carnet    |
| ------------------------------------ | --------- |
| <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRH6Uyi30Ty2WkMb0ZjuFLoXmkRwrrMObm-X2zztWtGbOgyA-i7mFzuiSKltN14HLAJDVM&usqp=CAU" alt="drawing" width="20"> &nbsp;Jimmy Yorbany Noriega Chávez         | 200915691 |

> \* ***Nota:*** El presente manual, presenta la configuración e implementacion de esquemas basicos, en base de datos Oracle.

# PROYECTO NO.1

<div id='content'/>

## Contenido

1. [Configuración Base de datos oracle, en GCP](#id1)
2. [Primer esquema, permisos, vistas](#id2)
3. [Segundo Esquema backup](#id3)


<div id='id1'/>

## 1. Configuración Base de datos oracle, en GCP [ ⇧](#content)

 La configuración requiere tener una cuenta en GCP (Google Cloud Plataform)
 <img src="https://cloud.google.com/_static/cloud/images/social-icon-google-cloud-1200-630.png?hl=es-es" alt="drawing" width="150"><br>

Pasos: 
</br>
<table>
<tr>
<td>
Paso 
</td>
<td>
Descripción
</td>
<td>
Detalle
</td>
</tr>
<tr>
<td>
Configurar Regla Firewall 
</td>
<td>
Configuramos la regla firewall, para esto vamos al menu firewall vpc, le asignamos un nombre caracteristico,
seleccionamos todo para entrada, y le asignamos la ip 0.0.0.0/0, para permitir todo el tráfico, y le indicamos que vamos a permitir peticiones
de http y https.
</td>
<td>
<img src="/images/paso1.png"/>  
</td>
</tr>
<tr>
<td>
Configurar Instancia VM
</td>
<td>
Luego nos vamos a compute engine, donde seleccionamos crear una instancia de vm, donde le asignamos el nombre que deseemos, para la resolución que necesita el proyecto esta bien una con el menor performance por tema de costos, pero lo importante es seleccionar el sistema operativo centos 8
</td>
<td>
<img src="/images/paso2.png"/>  
</td>
</tr>
<tr>
<td>
Levantar Instancia VM
</td>
<td>
Luego nos vamos a nuestro panel de instancias, y verificamos que se encuentre arriba la instancia, de no estarlo, se levanta, como opcional, se puede configurar un ip estatica o elastica, para no que permanezca la misma y no sea necesario cambiar todos los puntos de conexion.
</td>
<td>
<img src="/images/paso3.png"/>  
</td>
</tr>
<tr>
<td>
Instalar archivos necesarios
</td>
<td>
Archivos necesarios para poder descargar, configurar e instalar oracle 21c Express Edition
</td>
<td>
sudo yum install unzip libaio bc flex wget
</td>
</tr>
<tr>
<td>
Crear Archivos SWAP
</td>
<td>
Se crean los archivos swap para manejar los archivos de configuracion.
</td>
<td>
sudo dd if=/dev/zero of=/mnt/swapfile bs=1024 count=2097152
</td>
</tr>
<tr>
<td>
Permos Archivos SWAP
</td>
<td>
Se le asignan los permisos necesarios a los archivos swap para su manipulación
</td>
<td>
sudo chmod 777 /mnt/swapfile
</td>
</tr>
<tr>
<td>
Configurar Archivos SWAP
</td>
<td>
1. Seteamos el archivo </br> 
2. Lo asignamos como el archivo swap del sistema </br> 
3. Configurar para que se incie junto con la instancia, se puede hacer con vi o nano
</td>
<td>
1. sudo mkswap /mnt/swapfile </br> 
2. sudo su swapon /mnt/swapfile</br>
3. /mnt/swapfile swap swap defaults 0 0
</td>
</tr>
<tr>
<td>
Descargamos Oracle 21c EX
</td>
<td>
Procedemos a realizar la descarga de los archivos oficiales para la instalacion de oracle
</td>
<td>
wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm
</td>
</tr>
<tr>
<td>
Instalar Oracle 21c EX
</td>
<td>
1. Procedemos a instalar oracle </br>
2. Se configura las claves del usuario system </br>
3. En caso de detener la instancia o que se detenga la base datos usar:
</td>
<td> 
1. yum -y localinstall oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm </br>
2. /etc/init.d/oracle-xe-21c configure </br>
3. sudo /etc/init.d/oracle-xe-21c start
</td>
</tr>
<tr>
<td>
Conexión a la Base de datos
</td>
<td>
Para conectarnos a la base de datos, podemos usar programas como sql developer, donde usamos el usuario system y la contraseña que asginamos en el paso anterior 
asignamos nuestra ip externa, y damos conectar, nos lleva hacia nuestro entorno de trabajo
</td>
<td> 
<img src="/images/paso5.png"/>  
</td>
</tr>
</table>


<div id='id2'/>

## 2. Primer Esquema, permisos y vista [ ⇧](#content)
</br>
Pasos: 
</br>
<table>
<tr>
<td>
Paso 
</td>
<td>
Descripción
</td>
<td>
Detalle
</td>
</tr>
<tr>
<td>
Configurar Regla Firewall 
</td>
<td>
Configuramos la regla firewall, para esto vamos al menu firewall vpc, le asignamos un nombre caracteristico,
seleccionamos todo para entrada, y le asignamos la ip 0.0.0.0/0, para permitir todo el tráfico, y le indicamos que vamos a permitir peticiones
de http y https.
</td>
<td>
<img src="/images/paso1.png"/>  
</td>
</tr>
<tr>
<td>
Configurar Instancia VM
</td>
<td>
Luego nos vamos a compute engine, donde seleccionamos crear una instancia de vm, donde le asignamos el nombre que deseemos, para la resolución que necesita el proyecto esta bien una con el menor performance por tema de costos, pero lo importante es seleccionar el sistema operativo centos 8
</td>
<td>
<img src="/images/paso2.png"/>  
</td>
</tr>
<tr>
<td>
Levantar Instancia VM
</td>
<td>
Luego nos vamos a nuestro panel de instancias, y verificamos que se encuentre arriba la instancia, de no estarlo, se levanta, como opcional, se puede configurar un ip estatica o elastica, para no que permanezca la misma y no sea necesario cambiar todos los puntos de conexion.
</td>
<td>
<img src="/images/paso3.png"/>  
</td>
</tr>
<tr>
<td>
Instalar archivos necesarios
</td>
<td>
Archivos necesarios para poder descargar, configurar e instalar oracle 21c Express Edition
</td>
<td>
sudo yum install unzip libaio bc flex wget
</td>
</tr>
<tr>
<td>
Crear Archivos SWAP
</td>
<td>
Se crean los archivos swap para manejar los archivos de configuracion.
</td>
<td>
sudo dd if=/dev/zero of=/mnt/swapfile bs=1024 count=2097152
</td>
</tr>
<tr>
<td>
Permos Archivos SWAP
</td>
<td>
Se le asignan los permisos necesarios a los archivos swap para su manipulación
</td>
<td>
sudo chmod 777 /mnt/swapfile
</td>
</tr>
<tr>
<td>
Configurar Archivos SWAP
</td>
<td>
1. Seteamos el archivo </br> 
2. Lo asignamos como el archivo swap del sistema </br> 
3. Configurar para que se incie junto con la instancia, se puede hacer con vi o nano
</td>
<td>
1. sudo mkswap /mnt/swapfile </br> 
2. sudo su swapon /mnt/swapfile</br>
3. /mnt/swapfile swap swap defaults 0 0
</td>
</tr>
<tr>
<td>
Descargamos Oracle 21c EX
</td>
<td>
Procedemos a realizar la descarga de los archivos oficiales para la instalacion de oracle
</td>
<td>
wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm
</td>
</tr>
<tr>
<td>
Instalar Oracle 21c EX
</td>
<td>
1. Procedemos a instalar oracle </br>
2. Se configura las claves del usuario system </br>
3. En caso de detener la instancia o que se detenga la base datos usar:
</td>
<td> 
1. yum -y localinstall oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm </br>
2. /etc/init.d/oracle-xe-21c configure </br>
3. sudo /etc/init.d/oracle-xe-21c start
</td>
</tr>
<tr>
<td>
Conexión a la Base de datos
</td>
<td>
Para conectarnos a la base de datos, podemos usar programas como sql developer, donde usamos el usuario system y la contraseña que asginamos en el paso anterior 
asignamos nuestra ip externa, y damos conectar, nos lleva hacia nuestro entorno de trabajo
</td>
<td> 
<img src="/images/paso5.png"/>  
</td>
</tr>
</table>




<div id='id3'/>

## 3. Máquina virtual [ ⇧](#content)

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
