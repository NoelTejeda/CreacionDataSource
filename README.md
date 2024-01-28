# CreacionDataSource
El objetivo de este repositorio es crear una guía de instalación de un Datasource con el server wildfly 19.0.1 para futuros usos.

------------------------------------------------------------------------------------------------------------------------------------------


1) Haber descargado el server wildfly 19.0.1 ( se usa esta versión ya que anteriormente usamos una versión superior y arrojó error en splap)
   
2) consejo: crear en Disco C:/ una carpeta (servers) y allí alojar el instalador

3) Crear un usuario:
   
   3.1) ir a la carpeta bin
   
   3.2) ejecutar add-user.bat  (windows)  /  add-user.sh (unix)
   
   3.3) presionar tecla a (management User)
   
   ![Alt text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso1.png)
 
   

   3.4) agregar el usuario

   ![Alt text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso2.png)
   

   3.5) seleccionar un password (al escribir el password no se mostrará nada) (colocar un caracter alfanumerico si desea)
   
   ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso3.png)

   3.6) si no se desea agregar el usuario a un grupo dejar en blanco esta opción y enter

   ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso4.png)
   
   3.7) Enter 'yes' (ManagementRealm es el que se utiliza por defecto en la configuración, es importante dejar el nombre del ámbito como ManagementRealm, ya que este nombre debe coincidir con el nombre 
        utilizado en la configuración del servidor)

   ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso5.png)

   3.8) enter 'yes'

   ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso6.png)

   3.9) nos dará un código ( Este paso es especialmente importante si planeas utilizar este usuario para permitir que un proceso de servidor WildFly se conecte a otro, como en una configuración de clúster ) 
        (OBVIAR NO LO USAREMOS)
         https://www.eginnovations.com/documentation/WildFly/Creating-a-new-management.htm

   ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso7.png)

   3.10) al presionar continuar se cierra la consola.


  -----------------------------------------------------------------------------


   
   4) En Netbeans:
  
      
      4.1) ir a services / servers / click derecho-mouse / add server

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso%204.1.png)   


      4.2) seleccionar la opción "WildFly Application Server" y "Name" es aconsejable cambiar por "WildFly 19.0.1" para tener
           identificada la versión.

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso4.2.png)


      4.3) seleccionar la ubicación y en server configuration automaticamente seleccionará el standalone-full.xml que se usará.

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso4.3.png)
      

      4.4) importante colocar el user que se creó anteriormente en la consola de wildfly y su password.

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso4.4.png)


      4.5) levantar el servidor (start)

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/paso4.5.png)



   5) agregar los drivers de postgresql en C:\wildfly-19.1.0.Final\modules\system\layers\base\com
      sitio de descarga: https://mvnrepository.com/artifact/org.postgresql/postgresql

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/GuardarDriversPostgres.png)

      Quedando así:
      
      C:\Servers\wildfly-19.1.0.Final\modules\system\layers\base\com\postgresql\main

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/QuedandoAs%C3%AD.png)
       
            

      En el module.xml debe quedar así:

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/module.xml.png)



  7)  configurar el datasource en el archivo de configuración de WildFly (como standalone.xml o 
       domain.xml ó standalone-full.xml)


      6.1) para saber que archivo se debe configurar revisamos en Netbeans servers/click-derecho/ Properties:

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/Standalone-full.png)


      6.2) en el archivo standalome-full.xml agregar las siguientes líneas:

           <!-- Inicio postgresql CONFIGURACION  datasources--> 

 
                <datasource jndi-name="java:jboss/datasources/testconexion" pool-name="testconexiones">   
                    <connection-url>jdbc:postgresql://localhost:5432/BDtestconexion</connection-url>   
                    <driver>postgresql</driver>   
                    <security>   
                        <user-name>postgres</user-name>   
                        <password>postgres</password>   
                    </security>   
                </datasource>

         <!--  Fin postgresql CONFIGURACION  datasources-->


   ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/ConfiguracionAgregadaalStandalone.png)



      jndi-name = RUTA que colocamos en el application.properties (backend)
      pool-name = es el NOMBRE que le colocaremos al datasource
      User-name = Usuario de postgres
      password  = contraseña de postgres



      En el application.properties (Backend) la ruta debe ser la misma que colocamos en el standalone-full.xml
      
      spring.datasource.jndi-name=java:jboss/datasources/testconexion


    
 ----------------------------------------------------------------------------------------------------------------------------------
 7) Ingresar a localhost:9990 (wildfly)

    7.1) colocar el usuario y la contraseña que se creo por la consola anteriormente (punto 3)

   
    ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/localhost9990.png)


    7.2) Agregar Datasource:

    paso 1:
    
    ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/AddDataSource1.png)

    paso 2:

    ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/AddDataSource2.png)

    
      
