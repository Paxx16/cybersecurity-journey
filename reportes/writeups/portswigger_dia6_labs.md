Authentication, Business Logic & Information Disclosure



### Resumen
Me enfoqué en vulnerabilidades de autenticación, fallos en la lógica de negocio y exposición de información sensible utilizando PortSwigger Academy.

### Labs Completados

1. **Username enumeration via different responses**
   - Análisis de sutiles diferencias en los tiempos de respuesta y mensajes de error para identificar nombres de usuario válidos.
   - Herramienta: Burp Suite Intruder.

2. **2FA simple bypass**
   - Explotación de una implementación deficiente de la autenticación de dos factores donde el sistema no validaba correctamente el estado de la sesión antes de solicitar el código.

3. **Flawed enforcement of business rules**
   - Manipulación de la lógica de cupones de descuento (NEWCUST5 y SIGNUP30) para aplicarlos de forma acumulativa o repetitiva contra la intención original del negocio.

4. **Information disclosure in error messages**
   - Identificación de la versión específica del framework (Apache Struts 2 2.3.31) a través de mensajes de error detallados generados por entradas malformadas.

5. **Information disclosure on debug page**
   - Localización de una página de depuración activa que expuso la variable SECRET_KEY, comprometiendo la integridad de la aplicación.

6. **Source code disclosure via backup files**
   - Descubrimiento de archivos temporales/backup (.bak) en el servidor que revelaron código fuente sensible y lógica interna.



### Summary
I focused on authentication vulnerabilities, business logic flaws, and sensitive information disclosure using PortSwigger Academy.

### Completed Labs

1. **Username enumeration via different responses**
   - Analyzed subtle differences in response times and error messages to identify valid usernames.
   - Tool: Burp Suite Intruder.

2. **2FA simple bypass**
   - Exploited a flawed 2FA implementation where the system failed to properly validate the session state before requesting the verification code.

3. **Flawed enforcement of business rules**
   - Manipulated discount coupon logic (NEWCUST5 and SIGNUP30) to apply them cumulatively or repetitively against the intended business rules.

4. **Information disclosure in error messages**
   - Identified specific framework versions (Apache Struts 2 2.3.31) through verbose error messages triggered by malformed input.

5. **Information disclosure on debug page**
   - Located an active debug page that exposed the SECRET_KEY variable, compromising the application's integrity.

6. **Source code disclosure via backup files**
   - Discovered temporary/backup files (.bak) on the server that revealed sensitive source code and internal logic.
