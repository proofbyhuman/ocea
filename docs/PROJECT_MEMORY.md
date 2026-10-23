# PROJECT_MEMORY — RGCL-OCEA

Versión: 0.1  
Fecha: 2026-10-24  
Propósito: preservar el estado esencial del proyecto entre sesiones de trabajo, sin arrastrar ventanas de contexto largas.

Este archivo no es la fuente de verdad técnica.  
La fuente de verdad será, progresivamente:

- `README.md`
- `SECURITY.md` o `security.md`
- `MANIFEST.md`
- futura `docs/SPEC_GOBERNANZA_V0.1.md`
- futuros ADRs

---

## 1. Estado actual del repo

`[VERIFICADO visualmente en GitHub]`

- Repo: `proofbyhuman/ocea`
- Visibilidad: privada
- Rama principal: `main`
- Commits observados: 5
- Licencia observada: Apache-2.0
- Archivos raíz observados:
  - `LICENSE`
  - `MANIFEST.md`
  - `README.md`
  - `ocea.gitignore`
  - `security.md`

`[VERIFICADO de proceso]`

- Paso 0 completado: el repo nace limpio.
- No se importó historial Git de repos anteriores.
- No se conocen claves privadas en los archivos visibles.
- Falta correr automatización de higiene cuando exista `scripts/check_no_secrets.py`.

---

## 2. Identidad y nombre

`[DECISIÓN PENDIENTE]`

- Concepto de proyecto: **RGCL-OCEA**
- Nombre actual del repo: **ocea**
- Descripción pública actual: RGCL-OCEA como laboratorio limpio de evidencia de gobernanza humano–IA.

Regla provisional:

> No forzar renombrar el repo ahora si eso rompe enlaces o genera ruido.  
> La marca puede ser RGCL-OCEA aunque el repo sea `ocea`.

Si más adelante se normaliza, hacerlo con un commit pequeño y claro.

---

## 3. Misión del proyecto

Construir una base limpia, verificable y defendible para evidencia de gobernanza en sistemas consequential humano–IA.

Pregunta central:

> ¿Puede un auditor, usando solo registros firmados e inmutables, distinguir si una corrección legítima fue recibida, consumida, aplicada antes del punto de compromiso, o simplemente llegó tarde?

Frase guía:

> Un registro firmado prueba procedencia.  
> Un acuse prueba recepción.  
> Solo un chequeo ejecutor firmado, previo al compromiso y con control comparativo, puede probar gobierno.

---

## 4. Límite epistemológico obligatorio

Este límite debe repetirse en reportes, resúmenes y entregas externas:

> La simulación valida el diseño de la evidencia y la lógica del auditor para el dominio COF_BIOMONITOR. No valida el comportamiento operativo real de ASPR. Los perfiles FORENSE, INSTITUCIONAL e INFRA_CRISES son diseño declarado, no validado. Donde la evidencia se detiene, la afirmación se detiene.

---

## 5. Alcance congelado para v0.1

Dentro de alcance:

- Dominio: `COF_BIOMONITOR`
- Acción consequential simulada: emisión de certificación biomonitora.
- Autoridad legítima: validador técnico humano.
- Ejecutor: componente simulado con política explícita.
- Auditor: clasificador independiente basado solo en registros.
- Controles: corridas C1–C7b y futuros controles negativos N1–N10.

Fuera de alcance:

- FORENSE
- INSTITUCIONAL
- INFRA_CRISES
- producción real
- agentes autónomos como ejecutores definitivos
- endpoints públicos de revocación/suspensión
- claves persistentes dentro del repo

---

## 6. Reglas duras no negociables

1. No subir claves privadas, tokens, contraseñas, seeds ni `.env` reales.
2. Ninguna clave expuesta en repos anteriores se reutiliza.
3. Toda simulación usa claves efímeras en memoria.
4. No usar NTP ni reloj de pared para la lógica de gobernanza.
5. No agregar dependencias externas al núcleo de simulación.
6. No presentar simulación como validación operacional.
7. No ampliar alcance a perfiles no validados.
8. Toda ambigüedad se registra, no se resuelve en silencio.
9. Todo reporte incluye el límite epistemológico.
10. Antes de compartir con terceros, correr revisión de higiene de secretos.

---

## 7. Relación con Evelyne-Claudia Yantony / REACHABLE™

`[RECONOCIMIENTO INTELECTUAL, NO AVAL]`

El proyecto incorpora criterios discutidos en el intercambio técnico con Evelyne-Claudia Yantony:

- cinco pasos de evidencia mínima;
- cinco verificaciones públicas de REACHABLE™:
  - Authority
  - Reachability
  - Detection
  - Interruptibility
  - Recovery
- explicaciones alternativas que el control debe descartar;
- distinción entre prevención antes del compromiso y remediación después del compromiso.

Esto no implica:

- aval;
- asociación formal;
- certificación;
- uso del instrumento privado de REACHABLE™;
- validación operacional de `rgcl-ocea`;
- conformidad de ella con el contenido del repo.

---

## 8. Norte técnico de la próxima fase

La arquitectura mínima de evidencia debe girar alrededor de esta cadena:

```text
INTENCION
  -> CORRECCION
    -> CHEQUEO_EJECUTOR
      -> COMPROMISO
        -> RESULTADO
          -> AUDITORIA
