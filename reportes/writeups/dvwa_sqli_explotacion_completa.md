## Crackeo de Hashes MD5

### Metodología de Crackeo

*Herramienta utilizada:* CrackStation.net (lookup tables precalculadas)

*Proceso:*
1. Extracción de hashes mediante SQL Injection
2. Identificación del algoritmo (MD5 - 32 caracteres hexadecimales)
3. Uso de base de datos de rainbow tables
4. Recuperación instantánea de contraseñas

### Resultados Completos

| Usuario | Hash MD5 | Password | Tiempo | Fuerza |
|---------|----------|----------|--------|--------|
| pablo | 0d107d09f5bbe40cade3de5c71e9e9b7 | letmein | <1s | ⚠️ Muy débil |
| 1337 | 8d3533d75ae2c3966d7e0d4fcc69216b | charley | <1s | ⚠️ Débil |
| gordonb | e99a18c428cb38d5f260853678922e03 | abc123 | <1s | ⚠️ Muy débil |
| admin | 5f4dcc3b5aa765d61d8327deb882cf99 | password | <1s | 🔴 Crítico |
| smithy | 5f4dcc3b5aa765d61d8327deb882cf99 | password | <1s | 🔴 Crítico |

*Observaciones críticas:*
- ✓ TODOS los hashes fueron crackeados exitosamente
- ✓ Tiempo total: menos de 1 segundo
- ⚠️ Las contraseñas son extremadamente comunes
- 🔴 "password" y "abc123" están en el Top 10 de peores contraseñas
- 🔴 Admin y smithy comparten la misma contraseña débil

### Análisis de Seguridad

*Por qué MD5 es inseguro:*
1. *Velocidad extrema:* Se pueden calcular miles de millones de hashes por segundo
2. *Rainbow tables:* Bases de datos precalculadas con billones de hashes
3. *Sin salt:* Los mismos passwords producen el mismo hash
4. *Colisiones conocidas:* Diferentes inputs pueden producir el mismo hash

*Comparación de tiempos de crackeo:*

| Algoritmo | Hashes/segundo (GPU RTX 3080) | Tiempo para crackear "password" |
|-----------|------------------------------|--------------------------------|
| MD5 | ~100 mil millones/s | <1 segundo |
| SHA1 | ~30 mil millones/s | <1 segundo |
| bcrypt (cost 10) | ~15,000/s | ~18 horas |
| Argon2id | ~1,000/s | ~11 días |

### Recomendaciones de Hashing Seguro

*NUNCA usar:*
- ❌ MD5
- ❌ SHA1
- ❌ SHA256 (sin salt y sin work factor)

*Algoritmos recomendados en 2026:*
- ✅ *Argon2id* (ganador de Password Hashing Competition 2015)
- ✅ *bcrypt* (work factor mínimo 12)
- ✅ *scrypt* (con parámetros altos)

*Implementación segura en PHP:*
```php
// Hashear (Argon2id es el estándar en PHP 7.4+)
$hash = password_hash($password, PASSWORD_ARGON2ID);

// Verificar
if (password_verify($input_password, $hash)) {
    // Password correcto
}
