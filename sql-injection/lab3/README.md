SQL Injection UNION Attack: Laboratorio 3 de PortSwigger

🎯 Objetivo del Laboratorio
El tercer laboratorio de SQL Injection de PortSwigger se enfoca en un ataque UNION para recuperar datos de otras tablas de la base de datos. El objetivo era extraer credenciales de usuarios de una tabla específica y utilizar esta información para acceder como administrator, demostrando cómo una vulnerabilidad de SQL Injection puede llevar a una compromiso completo de la confidencialidad de los datos.

🔍 Proceso de Resolución
1. Reconocimiento e Identificación del Punto de Inyección
Al abrir el laboratorio, me encontré con una aplicación web que mostraba productos filtrados por categoría. Al seleccionar una categoría, la URL incluía un parámetro category vulnerable a SQL Injection:
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab3/images/union.png)

2. Determinación del Número de Columnas

Para realizar un ataque UNION, primero necesitaba determinar el número de columnas en la consulta original. Utilicé dos métodos:
Método ORDER BY: Incrementé gradualmente el número de columna hasta obtener un error:
category=Gifts' ORDER BY 1--
category=Gifts' ORDER BY 2--
category=Gifts' ORDER BY 3--  // Error - por lo tanto, hay 2 columnas

Método UNION SELECT: Confirmé el número de columnas usando:
category=Gifts' UNION SELECT 'NULL','NULL' FROM dual--
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab3/images/union2.png)

La consulta se ejecutó sin errores, confirmando que la consulta original retornaba 2 columnas.

y ahora veremos la version de la base de asi mediante el payload:
<img width="1154" height="817" alt="image" src="https://github.com/user-attachments/assets/8a00b130-68a4-435b-8891-a64dba44c5b2" />

ya que tuvimos la pista en cheat-sheet de como podiamos buscar la version de la base de datos




