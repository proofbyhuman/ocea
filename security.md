# SECURITY.md — rgcl-ocea

Este documento define la política de seguridad, higiene de secretos y manejo de material sensible del repo `rgcl-ocea`.

Estado: v0.1  
Tipo de repo: privado, nace limpio  
Alcance: laboratorio de evidencia de gobernanza para simulación acotada en `COF_BIOMONITOR`  
No aplica como política de producción de ASPR completo.

---

## 1. Principio rector

> Si una clave, token, contraseña, seed o credencial pudo ser vista por un tercero, se trata como comprometida.

Esto aplica incluso si el material era “de ensayo”, “de prueba”, “falso” o “ya no se usa”.

La razón no es solo criptográfica. También es de higiene, credibilidad y control de riesgo: un repo que alguna vez contuvo material sensible contaminado no debe seguir usándose como base de verdad.

---

## 2. Reglas duras

No se permite commitear, subir, pegar ni referenciar de forma reversible en este repo:

- claves privadas Ed25519;
- claves RSA, ECDSA, OpenSSH u otros formatos;
- archivos `.pem`, `.key`, `.p12`, `.pfx`, `.secret`, `.credentials`;
- seed phrases;
- tokens de acceso;
- API keys;
- contraseñas reales;
- `.env` reales;
- `config.env` con valores reales;
- credenciales de AWS, Bedrock, GitHub, Tailscale, email, dashboards o cualquier servicio;
- material criptográfico persistente;
- claves privadas de Ramiro;
- claves privadas de nodos ASPR;
- claves privadas forenses;
- claves privadas de Oracle;
- cadenas crudas con datos personales sensibles;
- MAC reales sin redactar;
- IPs privadas reales sin necesidad técnica;
- hostnames sensibles;
- correos personales innecesarios;
- logs crudos de red doméstica;
- reportes generados con material sensible sin redactar.

Si algo de esta lista entra al repo, se trata como incidente de seguridad.

---

## 3. Origen limpio

`rgcl-ocea` nace sin importar el historial Git de repos anteriores.

No se trae:

- historial antiguo;
- branches viejas;
- commits previos;
- archivos sensibles heredados;
- claves expuestas en repos anteriores;
- cadenas crudas con datos personales;
- `.env` antiguos;
- `venv/` versionados;
- reportes sin redactar.

El pasado se documenta como lección en:

- `docs/LEGACY_MANIFEST.md`

Pero no se usa como base técnica.

---

## 4. Claves expuestas en repos anteriores

Aunque fueran claves de ensayo, si estuvieron en un repo público, compartido, chat, archivo adjunto o historial Git, se consideran comprometidas.

Estados posibles:

| Estado | Significado | Acción |
|---|---|---|
| `EXPUESTA_POR_REPO` | Estuvo en historial público o compartido | Rotar/revocar |
| `ENSAYO_REUTILIZADA` | Se usó en más de un entorno | Tratar como comprometida |
| `EFIMERA_SIMULACION` | Generada en memoria y destruida | No requiere rotación si nunca persistió |
| `LEGADO_FIRMADO` | Bloques antiguos firmados con ella | Marcar como no confiable |
| `DESCARTADA` | No se usa más | Registrar motivo |

Regla:

> Ninguna clave expuesta en repos anteriores se reutiliza en `rgcl-ocea`.

---

## 5. Firmas legacy

Si existieran bloques, report