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
Entidad relación
</td>
<td>
Entidad relación asociada para el las votaciones electorales
</td>
<td>
<img src="/images/paso6.png"/>  
</td>
</tr>
<tr>
<td>
Crear TableSpace y Usuario
</td>
<td>
Nos concectamos a nuestra base de datos con el usuario system y la contraseña asginada en la configuración, luego de estar ahi, debemos crear un tablespace con un nombre, un archivo para el mismo, el tamaño y si sera autoincremental, esto nos dara un trabajo personalizado de trabajo, luego de esto, debemos crear un usuario master para trabajar sobre el espacio de trabajo, debemos asignarlo los roles de DBA y de creación de usuarios.
</td>
<td>
<img src="/images/paso7.png"/>  
</td>
</tr>
<tr>
<td>
Login nuevo usuario
</td>
<td>
Luego nos logeamos con nuestro nuevo usuario master, para poder trabajar sobre nuestro tablespace creado
</td>
<td>
<img src="/images/PASO8.png"/>  
</td>
</tr>
<tr>
<td>
Creación de usuarios
</td>
<td>
Se crean los usuarios solicitados, con los roles de insert, update, delete, consulta, y creacion de usuarios y tabla, caracteristica especial, para no poner permiso por tabla, se puede colcar el comando any, dentro de la instruccion para que afecte todos los objetos de ese tipo.
</td>
<td>
<img src="/images/PASO9.png"/> 
</td>
</tr>
<tr>
<td>
Creacón de Tablas
</td>
<td>
Se crean las tablas según el entidad relación, parte 1
</td>
<td>
<img src="/images/paso10.png"/> 
</td>
</tr>
<tr>
<td>
Creación de Tablas
</td>
<td>
Se crean las tablas según el entidad relación, parte 2
</td>
<td>
<img src="/images/paso11.png"/> 
</td>
</tr>
<tr>
<td>
Carga de la información
</td>
<td>
Ejecutamos el script para poder cargar nuestros datos al esquema de base de datos
</td>
<td>
<img src="/images/paso12.png"/> 
</td>
</tr>
<tr>
<td>
Logeo para realizar la vista
</td>
<td>
  Nos logueamos con el usuario guest1, ya que al va a pertenecer la vista, sobre los datos, donde se necesita saber cuantos votos, tuvieron los partidos, por minicipio.
</td>
<td>
<img src="/images/paso13.png"/> 
</td>
</tr>
<tr>
<td>
Creación de la vista
</td>
<td>
Creamos la vista, para devolver la informacion solicitada dentro del usuario guest1.
</td>
<td> 
<img src="/images/paso14.png"/> 
</td>
</tr>
</table>




<div id='id3'/>

## 3[Segundo Esquema backup][ ⇧](#content)

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
Entidad relación
</td>
<td>
Entidad relación asociada parael control de ligas sofre futbol
</td>
<td>
<img src="/images/esq2.png"/>  
</td>
</tr>
<tr>
<td>
Crear Usuarios
</td>
<td>
Creamos tres usuarios, uno para controlar los esquemas de datos iniciales, y dos para poder migrar en uno solo el esquema y en otro esquema y datos.
</td>
<td>
<img src="/images/paso15.png"/>  
</td>
</tr>
<tr>
<td>
Login nuevo usuario y carga esquema
</td>
<td>
Luego nos logeamos con nuestro nuevo usuario master, para poder crear el esquema
</td>
<td>
<img src="/images/paso16.png"/>  
</td>
</tr>
<tr>
<td>
Carga de script de datos
</td>
<td>
Cargamos el script con la informacion de los datos que van a ser registrado en el sistema.
</td>
<td>
<img src="/images/paso17.png"/> 
</td>
</tr>
<tr>
<td>
Export datos
</td>
<td>
Para poder exportar nuestro esquema y datos respectivamente, debemos crear 2 archivos donde especificamos, el usuario que hara la exportacion, el directorio donde seran creados el archivo .dmp con el backup, donde regisraremos el log de la exportacion, las tablas que se van a exportar o realizar backup y en el content, si seran solo los esquemas o todo, se hace uno por cada tipo de backup solicitado
</td>
<td>
<img src="/images/paso18.png"/> 
</td>
</tr>
<tr>
<td>
Creación de Directorio
</td>
<td>
Creamos el directorio donse se van a ir a guardar nuestro archivos de backup y log, tomar en cuenta lo siguiente, todas las carpetas deben tener el permiso chmod 777, esto las marcara de color verde, esto es para poder acceder a el y manipular las carpetas
</td>
<td>
<img src="/images/paso19.png"/> 
</td>
</tr>
<tr>
<td>
 Exportamos la información
</td>
<td>
Para exportar la informacion, nos logeamos con nuestro usuario oracle, sino nos recodamos la contraseña, podemo hacer su oracle, y luego passwd oracle, esto nos permitira asginarle una nueva contraseña, si al momento de ejecutar la instrucción expdp nos diche comando no encontrado, debemos setearle a este usuario las variables de entorno de nuestra instancia de base de datos, para esto usamos source oraenv y colocamos nuestra versión de oracle, luego ejecutamos la instrucción expdp -parfile Nombre del archivo.par, este nos pedira ingresar la contraseña del usuario, que se coloco en el campo USERID
</td>
<td>
<img src="/images/paso20.png"/> 
</td>
</tr>
<tr>
<td>
Exportamos esquema y datos
</td>
<td>
  Para exportar con esquema de tablas y sus datos, colocamos en el content: ALL y ejecutamos la instruccion expdp -parfile Nombre del archivo.par
</td>
<td>
<img src="/images/paso21.png"/> 
</td>
</tr>
<tr>
<td>
Importamos información
</td>
<td>
Para importar o hacer un restore al backup creado, vamos a usar la instruccion impdp, colocamos el usuario / contraseña del usuario, directorio donde se encuentran los archivos para hacer el restore, el archivo que contiene el backup, un logfile donde vamos a registrar las salidas de la importacion, y un mapeo de un esquema de un usuario a otro
</td>
<td> 
<img src="/images/paso22.png"  width="388"/> 
</td>
</tr>
</table>


Resumen de características:
|Característica|Valor|
|--|--|
|**Plataforma**| <img src="https://cloud.google.com/_static/cloud/images/social-icon-google-cloud-1200-630.png?hl=es-es" alt="drawing" width="150"><br>Google Cloud Platform |
|**Tipo de instancia**|e2-nicro|
|**Sistema operativo**|<img src="https://netknights.it/wp-content/uploads/2016/01/centos-logo-light.png" alt="drawing" width="135"><br>Centos|
|**Versión**| 7|
|**Espacio en disco**| 10 GB|
|**Memoria RAM**| 2 GB|


