🎯 Laboratorio: Ataque de Inyección SQL para Consultar el Tipo y Versión de la Base de Datos en MySQL y Microsoft SQL Server.

Objetivo: Explotar una vulnerabilidad de inyección SQL para extraer la versión de la base de datos subyacente, demostrando cómo un atacante puede obtener información crítica del sistema.

🔍 ¿Por qué es importante?
La versión de la base de datos es información crucial para un atacante: permite identificar vulnerabilidades conocidas y planificar exploits específicos.

Este ataque es un primer paso común en una cadena de explotación más avanzada.

Demuestra tu capacidad para adaptar payloads según el tipo de base de datos, una habilidad técnica muy valorada.
🛠️ Proceso de Resolución (Paso a Paso)
1. Reconocimiento e Identificación de la Vulnerabilidad
La aplicación web tenía un parámetro vulnerable (ej: category en una URL de filtro).

Al injectar una comilla simple ('), observé un error de base de datos, confirmando la vulnerabilidad.

2. Determinación del Número de Columnas
Usé ORDER BY para hallar el número de columnas en la consulta original:

