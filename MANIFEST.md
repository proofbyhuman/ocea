# LEGACY_MANIFEST — rgcl-ocea

Este documento registra qué se deja atrás, qué se rescata como referencia y qué se trata como no confiable.

No es una importación. Es una contención honesta del pasado.

Estado: v0.1  
Fecha: 2026-10-24  
Alcance: documentación de origen limpio para el repo `rgcl-ocea`  
Etiqueta general: mezcla de `[VERIFICADO]`, `[DICHO POR RAMIRO]`, `[NO VERIFICADO]` y `[RECONSTRUIDO]` según cada sección.

---

## 1. Principio rector

`rgcl-ocea` nace sin importar el historial Git de repos anteriores.

Motivo:

- evitar arrastrar claves expuestas;
- evitar arrastrar datos sensibles;
- evitar mezclar afirmaciones no verificadas;
- evitar heredar canonicalizaciones incompatibles;
- evitar presentar diseño declarado como validado.

Regla:

> El caos anterior no se borra fingiendo que no existió. Se ordena creando una base nueva donde cada afirmación tenga etiqueta, cada evidencia tenga artefacto y cada límite quede escrito.

---

## 2. Claves expuestas

### 2.1 Clave privada forense publicada

Origen:

- repo forense anterior, archivo `aspr_forense_protocol_security_endpoints/aspr_forensic_vault/forensic_private.pem`.

Hallazgo:

- `[VERIFICADO]` existía una clave privada Ed25519 publicada en el repo, sin contraseña, cuya clave pública derivada coincidía con `forensic_public.pem`.
- El contenido de la clave no se imprimió ni se guardó en este manifiesto.

Tratamiento en `rgcl-ocea`:

- comprometida;
- no reutilizar;
- rotar;
- revocar identidad asociada si existiera registro;
- marcar firmas legacy como `NO_CONFIABLE_CLAVE_EXPUESTA`;
- no usar como base de gobernanza actual.

Nota:

> Aunque fuera “de ensayo”, si estuvo expuesta, se trata como comprometida.

Estado de la rotación real:

- `[NO VERIFICADO]` si Ramiro ya realizó la rotación. Debe confirmarse antes de usar cualquier material relacionado.

### 2.2 Otras claves de ensayo

Cualquier clave que haya estado en repos públicos, chats, archivos compartidos o historiales Git se trata como expuesta.

Estados posibles:

| Estado | Significado |
|---|---|
| `EXPUESTA_POR_REPO` | Estuvo en historial público o compartido |
| `ENSAYO_REUTILIZADA` | Se usó en más de un entorno |
| `EFIMERA_SIMULACION` | Generada en memoria y destruida |
| `LEGADO_FIRMADO` | Bloques antiguos firmados con ella |
| `DESCARTADA` | No se usa más |

Regla:

> Ninguna clave expuesta se reutiliza en `rgcl-ocea`.

### 2.3 Claves de simulación

Las claves de la simulación previa (`sim_gobernanza.py`) fueron:

- efímeras;
- generadas en memoria con `secrets`;
- sobrescritas con ceros;
- destruidas al cerrar cada corrida.

`[VERIFICADO en reporte_gobernanza.json]`: `claves_efimeras_destruidas: true` en las 8 corridas.

No se requiere rotación porque nunca persistieron.

### 2.4 Claves reales de Ramiro

`[DICHO POR RAMIRO]` y regla de la spec: nunca se usan claves privadas reales de Ramiro en simulación ni en este repo.

---

## 3. Repos anteriores mencionados en contexto

Los siguientes repos o módulos aparecen en el análisis previo. Se listan como referencia histórica, no como base técnica.

| Repo / módulo | Rol histórico | Estado en `rgcl-ocea` |
|---|---|---|
| `camara-ecos-mit` / `eco_gardenerv1.py` | prototipo con LocIVault, CorrectionVerifier, GhostBalancer, ChallengeRegistry | referencia redactada |
| `ghost_balancer` | karma con piso 0.1 | hallazgo válido, no se importa código crudo |
| `aspr-gardener` | cadena live sin firmas | referencia histórica |
| `aspr-live_v1` / `ecos_crasher` | observador pasivo ICMP + ARP | candidato a adaptador futuro, no base actual |
| `coherencia-institucional-IA-humanby` | app Flask con aprobar/rechazar noticias | no validado |
| `genesis-carbon-silicon` | tesis Moltbook | referencia documental |
| repo forense | clave privada expuesta | comprometido / no confiable |
| `proyectosas` | venv, .env, config.env trackeados | no importar |
| `asprxgrok` (base forense con firma) | LocIVault con firma Ed25519 | referencia de esquema, no se importa código crudo |
| `aspr_live_v6` | GhostBalancer + LocIVault con nonce | referencia de lógica, no se importa código crudo |
| `certified_karma_gate` | doble puerta de karma | referencia de flujo, no se importa código crudo |

Observación:

- `[VERIFICADO en contexto §4.2]` el README de `analisi-d-eco-…` lista archivos (`correction_verifier.py`, `certified_karma_gate.py`, `update_guardian.py`, `layer2_ghost_balancer.py`, `demo_cluster_mit_karma.py`) que no existen como archivos independientes. La lógica del verificador está dentro de `eco_gardenerv1.py`.
- Esto se registra como lección: documentación y código no coincidían. En `rgcl-ocea` la spec y el código deben converger.

---

## 4. Hallazgos técnicos que sí se rescatan como lecciones

### 4.1 Canonicalización divergente

Hallazgo:

- `[VERIFICADO AMB-12 en reporte_gobernanza.json]` `asprxgrok.py` y `aspr_live_v6.py` calculaban `entry_hash` con canonicalizaciones distintas (`ensure_ascii=False` vs default `True`).

Lección:

- `rgcl-ocea` usará una única función `canon()` compartida y versionará el esquema de bloque.

### 4.2 Verificación tolerante

Hallazgo:

- `[VERIFICADO en informe_resultados.md §9.2]` `verify_full_integrity()` de la base forense validaba `entry_hash` pero no el encadenado `prev_hash` ni las firmas → bloques reordenados o eliminados no serían detectados por ese método.

Lección:

- `rgcl-ocea` exige verificación estricta: hash + encadenado + firma contra registro de génesis.

### 4.3 Delta de contexto débil

Hallazgo:

- `[VERIFICADO en contexto §5.1 e informe §9.4]` `_context_delta` comparaba hashes por distancia de bits: cualquier contexto distinto da ≈0.5 ≥ 0.05 → solo rechaza contextos idénticos (captura replay exacto, no distingue calidad de la corrección).

Lección:

- `rgcl-ocea` propone delta estructurado por campos semánticos, no distancia de bits entre hashes.

### 4.4 Validator_id sin firma

Hallazgo:

- `[VERIFICADO en contexto §5.3]` el `validator_id` (“jardinero”) era una cadena sin firma: cualquiera podía declararse humano.

Lección:

- identidad = clave registrada + firma Ed25519, no string.

### 4.5 Piso 0.1 del Ghost Score

Hallazgo:

- `[VERIFICADO en contexto §4.2 y tesis]` `score_floor=0.1`: el tráfico nunca llega a cero automáticamente → “corrección recibida” ≠ “corrección que gobernó”.

Lección:

- separar degradación suave (capa karma) de suspensión dura (capa gobernanza).

### 4.6 Claves efímeras rompen comparación por content_hash

Hallazgo:

- `[VERIFICADO AMB-16 en reporte_gobernanza.json]` en el control C7/C7b, los `content_hash` de los bloques OBSERVACION diferían entre brazos porque cada corrida genera claves efímeras nuevas y la clave pública del observador forma parte del data firmado.

Lección:

- comparar hash del mundo observado (payload), no hash de bloque, cuando hay rotación de claves.

### 4.7 Cadenas live sin firmas

Hallazgo:

- `[VERIFICADO en contexto §5.4]` las cadenas públicas de `aspr-gardener` y `aspr-live_v1` no llevaban firmas: son cadenas de hash que cualquiera puede recomputar.

Lección:

- el esquema de bloque de `rgcl-ocea` debe llevar firma por bloque desde el inicio.

### 4.8 Datos sensibles en cadenas antiguas

Hallazgo:

- `[VERIFICADO en contexto §6]` las cadenas de `aspr-gardener` y `aspr-live_v1` contienen direcciones MAC (3) e IPs privadas de la red local de Ramiro.

