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

               <?xml version='1.0' encoding='UTF-8'?> 
          
         <module xmlns="urn:jboss:module:1.1" name="com.postgresql.driver"> 
          
             <resources> 
             <!--the name of your driver --> 
                 <resource-root path="postgresql-42.3.1.jar"/> 
             </resources> 
          
             <dependencies> 
                 <module name="javax.api"/> 
                 <module name="javax.transaction.api"/> 
             </dependencies> 
         </module>



  6)  Ir a Netbeans y levantar wildfly para poder realizar la configuración del datasource de manera gráfica a través del puerto 9990 (localhost:9990)
    

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/Standalone-full.png)


      6.1) Ir a Deployments

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/Deployment.png)

      6.2) Upload Deployment y elegir los drivers postgres ( jar )

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/Deployment2.png)

      6.3) cargar el jar (drivers postgres)
           recordar que anteriormente lo habiamos guardado en la ruta: C:\Servers\wildfly-19.1.0.Final\modules\system\layers\base\com\postgresql\main

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/Deployment3.png)


      6.4) el nombre del driver podriamos cambiarlo, pero creo que seria mejor dejarlo así, para saber la versión del drivers que estamos usando.

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/Deployment4.png)


      6.5) verificar que el deploy se realizó con éxito

       ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/finisDeployment.png)
      

      ![Alt Text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/datasource/finishDeployment2.png)

      
