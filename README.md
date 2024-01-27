# CreacionDataSource
El objetivo de este repositorio es crear una guía de instalación de un Datasource con el server wildfly 19.0.1 para futuros usos.

1) Haber descargado el server wildfly 19.0.1 ( se usa esta versión ya que anteriormente usamos una versión superior y arrojó error en splap)
2) consejo: crear en Disco C:/ una carpeta (servers) y allí alojar el instalador

3) Crear un usuario:
   3.1) ir a la carpeta bin
   3.2) ejecutar add-user.bat  (windows)  /  add-user.sh (unix)
   3.3) presionar tecla a (management User)
   ![Alt text](https://github.com/NoelTejeda/CreacionDataSource/blob/main/paso1.png)
   imagen paso1

   3.4) agregar el usuario
   imagen paso2

   3.5) seleccionar un password (al escribir el password no se mostrará nada) (colocar un caracter alfanumerico si desea)
   imagen paso3

   3.6) si no se desea agregar el usuario a un grupo dejar en blanco esta opción y enter
   imagen paso4

   3.7) Enter 'yes' (ManagementRealm es el que se utiliza por defecto en la configuración, es importante dejar el nombre del ámbito como ManagementRealm, ya que este nombre debe coincidir con el nombre utilizado en la configuración del servidor)
   imagen paso5

   3.8) enter 'yes'
   imagen paso6

   3.9) nos dará un código ( Este paso es especialmente importante si planeas utilizar este usuario para permitir que un proceso de servidor WildFly se conecte a otro, como en una configuración de clúster ) (OBVIAR NO LO USAREMOS)
   https://www.eginnovations.com/documentation/WildFly/Creating-a-new-management.htm
    imagen paso7

   3.10) al presionar continuar se cierra la consola.

   
   
   4) En Netbeans:
      4.1) ir a services / servers / click derecho-mouse / add server
      imagen paso4.1

      4.2) seleccionar la opción "WildFly Application Server" y "Name" es aconsejable cambiar por "WildFly 19.0.1" para tener
           identificada la versión.
      imagen paso4.2

      4.3) seleccionar la ubicación y en server configuration automaticamente seleccionará el standalone-full.xml que se usará.
      imagen paso4.3

      4.4) importante colocar el user que se creó anteriormente en la consola de wildfly y su password.
      imagen paso 4.4

      4.5) levantar el servidor (start)
      imagen paso 4.5



   6) en localhost 9990
            

      
   
