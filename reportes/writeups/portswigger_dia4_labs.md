# PortSwigger Academy Labs - Day 4 / Dia 4

## [ENGLISH]

# PortSwigger Web Security Academy: Labs Completed

## Summary
Completed 6 hands-on labs in PortSwigger Academy covering SQL Injection, Cross-Site Scripting (XSS), and OS Command Injection vulnerabilities in realistic web application scenarios.

## Labs Completed

### SQL Injection

#### Lab 1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
**Objective:** Retrieve hidden products from database
**Payload:**
```
' OR 1=1--
```
**Result:** Application displayed all products including unreleased items
**Technique:** Boolean-based injection to bypass WHERE clause filter

#### Lab 2: SQL injection vulnerability allowing login bypass
**Objective:** Login as administrator without knowing password
**Payload:**
```
Username: administrator'--
Password: x
```
**Result:** Successfully logged in as administrator
**Technique:** Comment injection to bypass password verification

### Cross-Site Scripting (XSS)

#### Lab 3: Reflected XSS into HTML context with nothing encoded
**Objective:** Execute alert() function via reflected XSS
**Payload:**
```
<script>alert(1)</script>
```
**Location:** Search field
**Result:** JavaScript executed, popup displayed
**Technique:** Direct script injection in unfiltered input

#### Lab 4: Stored XSS into HTML context with nothing encoded
**Objective:** Store malicious script in application database
**Payload:**
```
<script>alert(1)</script>
```
**Location:** Comment section
**Result:** Script stored and executed for all users viewing the page
**Technique:** Persistent XSS via comment functionality

#### Lab 5: DOM XSS in document.write sink using source location.search inside a select element
**Objective:** Execute JavaScript via DOM manipulation
**Payload:**
```
"></select><script>alert(1)</script>
```
**Location:** storeId URL parameter
**Result:** Script executed by breaking out of select element
**Technique:** DOM-based XSS exploiting document.write sink

### OS Command Injection

#### Lab 6: OS command injection, simple case
**Objective:** Execute arbitrary system commands
**Payload:**
```
1|whoami
```
**Location:** storeId parameter in stock check function
**Result:** Server executed whoami command, returned username
**Technique:** Pipe character to chain commands

## Key Learnings

1. SQL Injection: Comments (--) can bypass authentication logic
2. XSS Reflected: User input directly rendered without sanitization
3. XSS Stored: Persistent attacks affect all users
4. DOM XSS: Client-side JavaScript can be exploited
5. Command Injection: Special characters (|, ;, &) enable command chaining

## Tools Used
- Burp Suite Community Edition
- Firefox Developer Tools
- PortSwigger Web Security Academy

---

## [ESPANOL]

# PortSwigger Web Security Academy: Laboratorios Completados

## Resumen
Se completaron 6 laboratorios practicos en PortSwigger Academy cubriendo vulnerabilidades de Inyeccion SQL, Cross-Site Scripting (XSS) e Inyeccion de Comandos del SO en escenarios realistas de aplicaciones web.

## Laboratorios Completados

### Inyeccion SQL

#### Lab 1: Vulnerabilidad de inyeccion SQL en clausula WHERE permitiendo recuperacion de datos ocultos
**Objetivo:** Recuperar productos ocultos de la base de datos
**Payload:**
```
' OR 1=1--
```
**Resultado:** La aplicacion mostro todos los productos incluyendo items no publicados
**Tecnica:** Inyeccion basada en booleanos para evadir filtro de clausula WHERE

#### Lab 2: Vulnerabilidad de inyeccion SQL permitiendo bypass de login
**Objetivo:** Iniciar sesion como administrador sin conocer la contrasena
**Payload:**
```
Username: administrator'--
Password: x
```
**Resultado:** Sesion iniciada exitosamente como administrador
**Tecnica:** Inyeccion de comentario para evadir verificacion de contrasena

### Cross-Site Scripting (XSS)

#### Lab 3: XSS Reflejado en contexto HTML sin codificacion
**Objetivo:** Ejecutar funcion alert() via XSS reflejado
**Payload:**
```
<script>alert(1)</script>
```
**Ubicacion:** Campo de busqueda
**Resultado:** JavaScript ejecutado, popup mostrado
**Tecnica:** Inyeccion directa de script en entrada sin filtrar

#### Lab 4: XSS Almacenado en contexto HTML sin codificacion
**Objetivo:** Almacenar script malicioso en base de datos de la aplicacion
**Payload:**
```
<script>alert(1)</script>
```
**Ubicacion:** Seccion de comentarios
**Resultado:** Script almacenado y ejecutado para todos los usuarios que visitan la pagina
**Tecnica:** XSS persistente via funcionalidad de comentarios

#### Lab 5: DOM XSS en sink document.write usando source location.search dentro de elemento select
**Objetivo:** Ejecutar JavaScript via manipulacion del DOM
**Payload:**
```
"></select><script>alert(1)</script>
```
**Ubicacion:** Parametro storeId en URL
**Resultado:** Script ejecutado al romper el elemento select
**Tecnica:** XSS basado en DOM explotando sink document.write

### Inyeccion de Comandos del SO

#### Lab 6: Inyeccion de comandos del SO, caso simple
**Objetivo:** Ejecutar comandos arbitrarios del sistema
**Payload:**
```
1|whoami
```
**Ubicacion:** Parametro storeId en funcion de verificacion de stock
**Resultado:** Servidor ejecuto comando whoami, retorno nombre de usuario
**Tecnica:** Caracter pipe para encadenar comandos

## Aprendizajes Clave

1. Inyeccion SQL: Comentarios (--) pueden evadir logica de autenticacion
2. XSS Reflejado: Entrada de usuario renderizada directamente sin sanitizacion
3. XSS Almacenado: Ataques persistentes afectan a todos los usuarios
4. DOM XSS: JavaScript del lado cliente puede ser explotado
5. Inyeccion de Comandos: Caracteres especiales (|, ;, &) permiten encadenamiento de comandos

## Herramientas Utilizadas
- Burp Suite Community Edition
- Firefox Developer Tools
- PortSwigger Web Security Academy

---
**Autor / Author:** Francisco Escalante
**Fecha / Date:** Enero / January 2026
**Plataforma / Platform:** PortSwigger Web Security Academy
**GitHub:** github.com/Paxx16/cybersecurity-journey
