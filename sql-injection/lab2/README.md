Elusión de Inicio de Sesión mediante SQL Injection: Laboratorio 2 de PortSwigger

🎯 Objetivo del Laboratorio
El segundo laboratorio de SQL Injection de PortSwigger se centra en eludir un mecanismo de inicio de sesión mediante inyección SQL. El objetivo era acceder al área restringida de la aplicación como el usuario administrator sin conocer su contraseña, demostrando cómo una vulnerabilidad de seguridad puede comprometer por completo la autenticación.

🔍 Proceso de Resolución
1. Reconocimiento
Al abrir el laboratorio, me encontré con un formulario de inicio de sesión aparentemente estándar:
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab2/images/incio.png)
Analicé el comportamiento de la aplicación y determiné que el formulario era vulnerable a SQL Injection al:

Observar mensajes de error genéricos que sugerían una posible manipulación de consultas SQL

Identificar que los campos de entrada no sanitizaban caracteres especiales

Reconocer que la aplicación utilizaba una consulta SQL directa para verificar credenciales
y ponemos la credennciales junto con la SQL injection
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab2/images/sql-injection.png)

Utilicé el siguiente payload en el campo de usuario:
administrator'--

administrator : Nombre de usuario objetivo

' : Cierra la comilla simple en la consulta SQL original

-- : Comenta el resto de la consulta, ignorando la verificación de contraseña

y ingresamos:
![](https://github.com/yaraDMC/wite-ups-de-portswigger/blob/main/sql-injection/lab2/images/finish.png)
3. Resultado y Acceso Exitoso
Al enviar el formulario con el payload, la aplicación procesó la consulta manipulada:
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''

🛡️ Implicaciones de Seguridad y Prevención
Este ejercicio demostró cómo un atacante podría:

Acceder a información sensible sin autorización

Suplantar identidades de usuarios privilegiados

Comprometer la integrididad de los datos

Medidas de prevención que aprendí:

Implementar consultas parametrizadas (Prepared Statements)

Validar y sanitizar todas las entradas del usuario

Utilizar principios de mínimo privilegio en bases de datos

Implementar controles de seguridad en capas (WAF, rate limiting)

📈 Conclusión
Aunque utilicé pistas para resolver este laboratorio, el proceso me permitió desarrollar una comprensión práctica de:

Cómo se explotan las vulnerabilidades SQL Injection en entornos reales

La importancia de los controles de seguridad en el desarrollo de aplicaciones

Técnicas para identificar y prevenir vulnerabilidades comunes

Esta experiencia refuerza mi compromiso con el desarrollo seguro y mi capacidad para aportar valor en roles relacionados con la ciberseguridad y el desarrollo de software.
