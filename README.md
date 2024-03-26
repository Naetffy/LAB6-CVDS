# LAB 6
# Despliega mi primera aplicación en Azure

## Mi primer despliegue en la nube

# Parte I - Despliegue app React (frontend) en Azure

1) Busca Azure for Students en tu buscador de preferencias e ingresa con el correo institucional.
2) Crea un budget de 1 dólar para la cuenta
    a. Una vez creada la cuenta.
     ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/9963c85c-c13e-42b8-9b78-3ed83ec4eb79)
    b. Escribimos budget, luego de entrar al apartado de budget le damos a add y seguimos los pasos para crear un budget.
     ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/97965319-a81a-4672-8032-bfc95307c460)
3) El profesor guía el resto de pasos
    a. Ahora entramos a static web app, y seguido a eso seguimos los pasos para crearlo.
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/74936400-63cd-47d3-bbe8-a6f58b1b1f00)
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/e6a30323-3df9-4157-8442-a40bbc78b43b)
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/475c1c62-4d47-402a-9e4f-291437542894)
       Ya en este punto le damos a resource
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/26ff3a11-2fef-479d-a527-719521b942c2)
   b. Ahora iremos al repositorio de github,
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/24deb3c2-9edc-4807-ab30-aefa5011ec91)
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/d73fbf76-1e16-43cb-9b74-c73e5007346d)
       Ya con esto podremos ver el workflow y tambien puedes volver a re ejecutar todos los trabajos dando clic en el botón "Re-run all jobs", al final de esta operación tendrás el enlace de tu aplicación,        o puedes volver a Azure y dar clic en el botón "View app in browser" .
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/5cd9022f-a6a7-4f2a-b347-16df5499a4cf)
       ![image](https://github.com/Naetffy/LAB6-CVDS/assets/112002572/9fe69997-d709-4847-8677-c4cfaddb8619)


# Parte II - Despliegue app web spring MVC (o spring-boot backend)
1) Inicie [Azure Cloud Shell](https://docs.microsoft.com/en-in/azure/cloud-shell/overview) desde el portal. Para implementar en un grupo de recursos, ingrese el siguiente comando
```shell
az group create --name MyResourceGroup --location westus
```
2) Para crear un plan de servicio de aplicaciones (App service plan)
```shell
az appservice plan create --resource-group MyResourceGroup --name MyPlan --sku F1
```
3) Finalmente, cree el servidor MySQL con un nombre de servidor único.
```shell
az mysql server create --resource-group MyResourceGroup --name mysqldbserver --admin-user mysqldbuser --admin-password P2ssw0rd@123 --sku-name Standard_B1ms
```
> Importante: Introduzca un nombre de servidor SQL único. Dado que el nombre de Azure SQL Server no admite las convenciones de nomenclatura de mayúsculas y minúsculas UPPER / Camel , utilice minúsculas para el valor del campo Nombre del servidor de base de datos. 
4) Navegue hasta el grupo de recursos que ha creado. Debería ver un servidor **Azure Database for MySQL server** aprovisionado. Seleccione el servidor de base de datos.

![image](https://github.com/PDSW-ECI/labs/assets/4140058/6eefacb6-31e5-47e3-b28d-4d1301c8d1e9)

5) Seleccione **Properties**. Guarde el **Server name** y el **Server admin login name** en un bloc de notas.

![image](https://github.com/PDSW-ECI/labs/assets/4140058/0a372f89-26da-4a44-ab5b-26e1238c3be8)

> En este ejemplo, el nombre del servidor es myshuttle-1-mysqldbserver.mysql.database.azure.com y el nombre de usuario administrador es mysqldbuser@myshuttle-1-mysqldbserver.
6) Seleccione **Connection security**. Habilite la opción **Allow access to Azure services** y guarde los cambios. Esto proporciona acceso a los servicios de Azure para todas las bases de datos de su servidor MySQL.

## Ejercicio 2: actualización de la configuración de la aplicación web
A continuación, navegue hasta la aplicación web que ha creado. Mientras implementa una aplicación Java, debe cambiar el contenedor web de la aplicación web a Apache Tomcat.
1) Seleccione **Configuration**. Establezca **Stack settings** como se muestra en la imagen a continuación y haga clic en Guardar.

![image](https://github.com/PDSW-ECI/labs/assets/4140058/2941dc04-5d50-4a71-a0ae-3e005397ab8f)

2) Seleccione Overview y click en Browse.

![image](https://github.com/PDSW-ECI/labs/assets/4140058/23e96cc7-473c-4457-aa2c-acce5c7b23ee)

3) La página web se verá como la imagen de abajo.

![image](https://github.com/PDSW-ECI/labs/assets/4140058/87db1d63-7179-4ce8-a013-a6a1c06056d8)

A continuación, debe actualizar las cadenas de conexión para que la aplicación web se conecte correctamente a la base de datos. Hay varias formas de hacerlo, pero para los fines de esta práctica de laboratorio, adoptará un enfoque simple actualizándolo directamente en Azure Portal.

4) Desde Azure Portal, seleccione la aplicación web que aprovisionó. Ir a Configuración | Configuración de la aplicación | Cadenas de conexión y haga clic en + Nueva cadena de conexión.

![image](https://github.com/PDSW-ECI/labs/assets/4140058/cccc9ce8-c19a-40c1-80b7-d82d278cc8db)

5) En la ventana Agregar/Editar cadena de conexión, agregue una nueva cadena de conexión MySQL con MyDatabase como nombre, pegue la siguiente cadena para el valor y reemplace MySQL Server Name, su nombre de usuario y su contraseña con los valores apropiados. Haga clic en Actualizar.
```java
jdbc:mysql://{MySQL Server Name}:3306/alm?useSSL=true&requireSSL=false&autoReconnect=true&user={your user name}&password={your password}
```

![image](https://github.com/PDSW-ECI/labs/assets/4140058/b0d5f0cf-949f-443e-8053-6e7ed2de7aed)

- Nombre del servidor MySQL: Valor que copió previamente de las Propiedades del servidor MySQL.
- su nombre de usuario: Valor que copió previamente de las Propiedades del servidor MySQL.
- su contraseña: valor que proporcionó durante la creación del servidor de base de datos MySQL.

7) Haga clic en Guardar para guardar la cadena de conexión.
> Nota: Las cadenas de conexión configuradas aquí estarán disponibles como variables de entorno, con el prefijo del tipo de conexión para aplicaciones Java (también para aplicaciones PHP, Python y Node). En el archivo DataAccess.java en la carpeta src/main/java/com/microsoft/example, recuperamos la cadena de conexión usando el siguiente código
```java
String conStr = System.getenv("MYSQLCONNSTR_MyDatabase");
```
Ahora ha instalado y configurado todos los recursos necesarios para implementar y ejecutar la aplicación MyApplication.

## Ejercicio 3: implementar los cambios en la aplicación web
1) Conectate con un cliente FTP y sube el jar de la aplicación Java https://github.com/PDSW-ECI/spring-mvc-with-bootstrap

## Entrega
- El enlace de la aplicación React y Spring MVC desplegada en Azure
