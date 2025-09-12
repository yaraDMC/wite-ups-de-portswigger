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

🛡️ Implicaciones de Seguridad y Prevención
Este ejercicio demostró cómo un atacante podría:

Acceder a datos sensibles de múltiples tablas

Comprometer todas las cuentas de usuario del sistema

Escalar privilegios hasta obtener control administrativo

Medidas de prevención que aprendí:

Implementar consultas parametrizadas para prevenir inyección

Aplicar el principio de mínimo privilegio en permisos de base de datos

Validar y sanitizar todas las entradas del usuario

Utilizar técnicas de ofuscación para errores de base de datos

Implementar controles de seguridad en capas (WAF, logging y monitoreo)

📈 Conclusión
La resolución de este laboratorio me permitió desarrollar habilidades avanzadas en:

Técnicas de explotación de SQL Injection con UNION

Análisis de estructura de bases de datos

Extracción sistemática de información sensible

Aplicación de medidas de prevención efectivas

Esta experiencia refuerza mi capacidad para identificar y mitigar vulnerabilidades críticas en aplicaciones web, aportando valor significativo en roles de seguridad informática y desarrollo seguro.


