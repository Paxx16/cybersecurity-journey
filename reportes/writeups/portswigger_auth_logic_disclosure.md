# PortSwigger Academy Labs


# PortSwigger Web Security Academy: Labs Completed

## Summary
Completed 6 hands-on labs in PortSwigger Academy covering Authentication, Business Logic, and Information Disclosure vulnerabilities in realistic web application scenarios.

## Labs Completed

### Authentication

#### Lab 1: Username enumeration via different responses
**Objective:** Enumerate valid usernames and brute force password
**Technique:** Different error messages reveal valid usernames
- Invalid username: "Invalid username"
- Valid username: "Incorrect password"
**Result:** Found valid credentials and logged in successfully

#### Lab 2: 2FA simple bypass
**Objective:** Bypass two-factor authentication
**Steps:**
1. Login with victim credentials carlos:montoya
2. When prompted for 2FA code, change URL directly to /my-account
3. 2FA verification skipped
**Technique:** Application does not verify 2FA completion before granting access

### Business Logic

#### Lab 3: Flawed enforcement of business rules
**Objective:** Purchase expensive item for free using coupon logic flaw
**Coupons discovered:**
- NEWCUST5 (new customer discount)
- SIGNUP30 (newsletter signup discount)
**Technique:** Alternating coupons bypasses "coupon already applied" check
**Steps:**
1. Apply NEWCUST5
2. Apply SIGNUP30
3. Apply NEWCUST5 again
4. Repeat until price reaches $0
**Result:** Purchased $1337 jacket for free

### Information Disclosure

#### Lab 4: Information disclosure in error messages
**Objective:** Find sensitive information in error messages
**Payload:**
```
/product?productId=test
```
**Result:** Server returned stack trace revealing:
- Apache Struts 2 2.3.31
- Internal file paths
- Java exception details
**Impact:** Version disclosure enables targeted exploits

#### Lab 5: Information disclosure on debug page
**Objective:** Find SECRET_KEY in debug information
**Steps:**
1. View page source (Ctrl+U)
2. Found hidden comment: <!-- <a href=/cgi-bin/phpinfo.php>Debug</a> -->
3. Navigate to /cgi-bin/phpinfo.php
4. Search for SECRET_KEY
**Result:** Retrieved SECRET_KEY value from debug page

#### Lab 6: Source code disclosure via backup files
**Objective:** Find database password in backup files
**Steps:**
1. Check /robots.txt - found Disallow: /backup
2. Navigate to /backup
3. Download ProductTemplate.java.bak
4. Found hardcoded database password in ConnectionBuilder
**Result:** Retrieved PostgreSQL database password

## Key Learnings

1. Authentication: Different error messages can leak valid usernames
2. 2FA Bypass: Always verify authentication state server-side
3. Business Logic: Coupon systems need proper state management
4. Information Disclosure: Debug pages and error messages reveal sensitive data
5. Backup Files: Never leave backup files in production

## Tools Used
- Firefox Developer Tools
- View Page Source (Ctrl+U)
- PortSwigger Web Security Academy

---

# PortSwigger Web Security Academy: Laboratorios Completados

## Resumen
Se completaron 6 laboratorios practicos en PortSwigger Academy cubriendo vulnerabilidades de Autenticacion, Logica de Negocio y Divulgacion de Informacion en escenarios realistas de aplicaciones web.

## Laboratorios Completados

### Autenticacion

#### Lab 1: Enumeracion de usuarios via respuestas diferentes
**Objetivo:** Enumerar usuarios validos y fuerza bruta de contrasena
**Tecnica:** Mensajes de error diferentes revelan usuarios validos
- Usuario invalido: "Invalid username"
- Usuario valido: "Incorrect password"
**Resultado:** Credenciales validas encontradas e inicio de sesion exitoso

#### Lab 2: Bypass simple de 2FA
**Objetivo:** Evadir autenticacion de dos factores
**Pasos:**
1. Login con credenciales de victima carlos:montoya
2. Cuando pide codigo 2FA, cambiar URL directamente a /my-account
3. Verificacion 2FA evadida
**Tecnica:** La aplicacion no verifica que se complete 2FA antes de dar acceso

### Logica de Negocio

#### Lab 3: Aplicacion defectuosa de reglas de negocio
**Objetivo:** Comprar articulo caro gratis usando falla en logica de cupones
**Cupones descubiertos:**
- NEWCUST5 (descuento nuevo cliente)
- SIGNUP30 (descuento por suscripcion a newsletter)
**Tecnica:** Alternar cupones evade verificacion de "cupon ya aplicado"
**Pasos:**
1. Aplicar NEWCUST5
2. Aplicar SIGNUP30
3. Aplicar NEWCUST5 de nuevo
4. Repetir hasta que precio llegue a $0
**Resultado:** Chaqueta de $1337 comprada gratis

### Divulgacion de Informacion

#### Lab 4: Divulgacion de informacion en mensajes de error
**Objetivo:** Encontrar informacion sensible en mensajes de error
**Payload:**
```
/product?productId=test
```
**Resultado:** Servidor retorno stack trace revelando:
- Apache Struts 2 2.3.31
- Rutas internas de archivos
- Detalles de excepcion Java
**Impacto:** Divulgacion de version permite exploits dirigidos

#### Lab 5: Divulgacion de informacion en pagina de debug
**Objetivo:** Encontrar SECRET_KEY en informacion de debug
**Pasos:**
1. Ver codigo fuente (Ctrl+U)
2. Encontrado comentario oculto: <!-- <a href=/cgi-bin/phpinfo.php>Debug</a> -->
3. Navegar a /cgi-bin/phpinfo.php
4. Buscar SECRET_KEY
**Resultado:** Valor de SECRET_KEY obtenido de pagina de debug

#### Lab 6: Divulgacion de codigo fuente via archivos de backup
**Objetivo:** Encontrar contrasena de base de datos en archivos de backup
**Pasos:**
1. Revisar /robots.txt - encontrado Disallow: /backup
2. Navegar a /backup
3. Descargar ProductTemplate.java.bak
4. Encontrada contrasena de base de datos en ConnectionBuilder
**Resultado:** Contrasena de PostgreSQL obtenida

## Aprendizajes Clave

1. Autenticacion: Mensajes de error diferentes pueden filtrar usuarios validos
2. Bypass 2FA: Siempre verificar estado de autenticacion en servidor
3. Logica de Negocio: Sistemas de cupones necesitan manejo de estado apropiado
4. Divulgacion de Info: Paginas de debug y errores revelan datos sensibles
5. Archivos de Backup: Nunca dejar backups en produccion

## Herramientas Utilizadas
- Firefox Developer Tools
- Ver codigo fuente (Ctrl+U)
- PortSwigger Web Security Academy

---
**Autor / Author:** Francisco Escalante
**Fecha / Date:** Febrero / February 2026
**Plataforma / Platform:** PortSwigger Web Security Academy
**GitHub:** github.com/Paxx16/cybersecurity-journey
