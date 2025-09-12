🔍 Explicación de la Vulnerabilidad SQL Injection
La inyección SQL es una vulnerabilidad crítica que ocurre cuando una aplicación web no valida, filtra o sanitiza adecuadamente las entradas del usuario. Esto permite a un atacante inyectar código SQL malicioso en las consultas de la base de datos. Como resultado, el atacante puede manipular las consultas para acceder, modificar o eliminar datos sensibles, lo que puede comprometer la confidencialidad, integridad y disponibilidad de la información.

🧪 Explicación del Laboratorio 1/16 de PortSwigger
El laboratorio simula una aplicación de comercio electrónico que filtra productos por categoría. El objetivo era realizar un ataque de inyección SQL que forzara a la aplicación a mostrar productos no lanzados (normalmente ocultos para los usuarios).
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab1/images/lab1.png)

el laboratorio nos pide lo siguiente: "Para resolver el laboratorio, realice un ataque de inyección SQL que haga que la aplicación muestre uno o más productos no lanzados."
Al abrir el labotario nos sale esto:

![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab1/images/principal.png)
Proceso de Resolucion
1. RECONOCIMIENTO: existen varias categorias, que cambiaba la URL e incluia el parámetro category
2. IDENTIFICACIÓN DEL PARÁMETRO VULNERABLE: despues de probar varios parámetros identifique que la categoria "Pets" era vulnerable a SQL injection.
3. injection y ahora vamos interceptar con BurpSuite y modificar el parametro 'Category' utilizando el payload '+OR+1=1--, que significa:
   ' : cierra la comilla simple que envuelve la consulta 'AND released=1' que es la que filtra los productos no lanzados
   OR 1=1 :  agrega una condicion que siempre va a ser verdadera, lo que hace que devuelva todos los registros.
   -- : comneta el resto de la consulta ignorando la condicion 
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab1/images/pets.png)

Después de la inyección, se convirtió en:
SELECT * FROM products WHERE category = 'Pets' OR 1=1--' AND released = 1
devolviendo todos los productos los lanzados y los que no
4. Resultado: al enviar las solicitud modificada devolvera todos los productos los lanzados y los que no.
