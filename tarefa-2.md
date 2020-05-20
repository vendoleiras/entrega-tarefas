# Instalación MySQL
1. Imos a [https://dev.mysql.com/downloads/windows/installer/8.0.html](https://dev.mysql.com/downloads/windows/installer/8.0.html) e descargamos o instalador de MySQL.
2. Unha vez descargado instalámolo, executando o .msi .
3. En "Choosing a setup type" eleximos Developer Default, que instalará automáticamente todo o necesario para poder crear e modificar bases de datos.
![Imaxe 1](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql1.PNG)
4. Continuamos dándolle a next, neste paso poderemos comprobar os productos que se instalarán.
![Imaxe 2](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql2.PNG)
5. Unha vez que termine de instalarse todo correctamente dámoslle a next.
![Imaxe 3](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql3.PNG)
6. En Group Replication seleccionamos Standalone MySQL Server/Classic MySQL Replication.
7. En Authentication Method seleccionamos Use Strong Password Encryption...
8. Agora deberemos especificar unha contraseña e añadir un usuario, dámoslle a next o terminar.
![Imaxe 4](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql4.PNG)
9. En Windows Service deixamos todo como está ou si queremos cambiámoslle o nome a Windows Service Name, dámoslle a next.
10. Dámoslle a Execute para executar os cambios, cando termine dámoslle a Finish.
![Imaxe 5](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql5.PNG)
11. En Connect to Server, abaixo deberemos por a contraseña que introducimos anteriormente, unha vez posta, dámoslle a check e mostrarásenos a seguinte mensaxe.
![Imaxe 6](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql6.PNG)
12. Cando rematemos, dámoslle a next e teranse que aplicar unhas novas configuracións, dámoslle a Execute.
![Imaxe 7](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql7.PNG)
13. Cando remate aparecerá unha nova ventá, dámoslle a next.
14. A instalación estará completa, dámoslle a Finish.
![Imaxe 8](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql8.PNG)
15. Agora podemos ir ao cmd a comprobar que temos mysql instalado, para eso escribimos `mysql --version`
16. É probable que nos salga o seguinte erro.
![Imaxe 9](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql9.PNG)
17. Para arreglalo, imos a Program Files>MySQL>MySQL Server 8.0>bin e copiamos a dirección.
18. Buscamos no Inicio "variables de entorno" para poder acceder ao editor de variables de entorno do sistema.
![Imaxe 10](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql10.PNG)
19. Seleccionamos Variables de Entorno.
20. Teremos que editar a variable PATH, e añadir a ruta que copiamos anteriormente onde se atopa o mySQL.
![Imaxe 11](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql11.PNG)
21. Gardamos todo e cerramos o editor das variables de entorno.
22. Se volvemos ao cmd e repetimos o paso número 15 mostrarásenos a versión.
![Imaxe 14](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql14.PNG)
23. Usamos `mysql -u root - p` donde root é o usuario, agora pediranos a contraseña, poñémola.
![Imaxe 12](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql12.PNG)
![Imaxe 13](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql13.PNG)
![Imaxe 14](https://raw.githubusercontent.com/vendoleiras/MySQL/master/images/mysql14.PNG)
  
  
