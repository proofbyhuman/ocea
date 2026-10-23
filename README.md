# rgcl-ocea

> **RGCL-OCEA**: laboratorio limpio de evidencia de gobernanza humano–IA. En simulación acotada (`COF_BIOMONITOR`), prueba cómo una corrección legítima es recibida, consumida y aplicada antes del compromiso, con auditoría independiente y sin afirmar más de lo probado.  
> **OCEA** = Observatorio de Cadena, Evidencia y Auditoría.

---

## Estado del proyecto

`rgcl-ocea` nace como un repo **privado y limpio**, sin importar historial Git de repos anteriores.

Objetivo inicial:

- ordenar el conocimiento existente;
- separar lo verificado de lo declarado;
- evitar arrastrar claves, datos sensibles o afirmaciones no probadas;
- construir una base defendible para evidencia de gobernanza;
- comenzar por un dominio acotado: **COF_BIOMONITOR**.

Estado actual:

- **Alcance simulado previamente**: COF_BIOMONITOR, solo como diseño de evidencia y lógica del auditor.
- **No validado operacionalmente**: ASPR como sistema real de gobierno de ejecución.
- **No validados**: perfiles FORENSE, INSTITUCIONAL e INFRA_CRISES.
- **Claves expuestas en repos anteriores**: tratadas como comprometidas, aunque fueran de ensayo.
- **Este repo**: sin claves privadas, sin `.env`, sin material sensible y sin historial contaminado.

---

## Qué es este repo

`rgcl-ocea` no es “otro lugar para guardar código viejo”.

Es un laboratorio ordenado para responder una pregunta concreta:

> ¿Puede un auditor, usando solo registros firmados e inmutables, distinguir si una corrección legítima fue recibida, consumida, aplicada antes del punto de compromiso, o simplemente llegó tarde?

La frase guía del proyecto es:

> Un registro firmado prueba procedencia.  
> Un acuse prueba recepción.  
> Solo un chequeo ejecutor firmado, previo al compromiso y con control comparativo, puede probar gobierno.

---

## Límite epistemológico

Este límite debe repetirse en todo reporte, resumen, entrega externa y conclusión técnica:

> La simulación valida el diseño de la evidencia y la lógica del auditor para el dominio COF_BIOMONITOR. No valida el comportamiento operativo real de ASPR. Los perfiles FORENSE, INSTITUCIONAL e INFRA_CRISES son diseño declarado, no validado. Donde la evidencia se detiene, la afirmación se detiene.

### Qué sí se pretende validar

- que exista una secuencia auditable de eventos;
- que una corrección pueda registrarse con autoridad, alcance y tiempo lógico;
- que un ejecutor firme qué estado consultó antes de decidir;
- que un auditor pueda clasificar escenarios acotados usando solo registros;
- que se puedan distinguir categorías como:
  - `NO_CORREGIDA`;
  - `GOBERNADA`;
  - `SOLO_RECIBIDA`;
  - `TARDE_REMEDIACION`;
  - `FALSIFICADA_RECHAZADA`;
  - `FALLA_CERRADA`;
  - `FALLA_ABIERTA_EJECUTA`;
  - `UNRESOLVED`.

### Qué no se pretende validar todavía

- que ASPR gobierne producción;
- que un ejecutor real consuma suspensiones;
- que existan endpoints operativos de revocación;
- que los perfiles FORENSE, INSTITUCIONAL e INFRA_CRISES funcionen;
- que la arquitectura completa sea segura, confiable o gobernable en condiciones reales.

---

## Discusión y menciones a Evelyne-Claudia Yantony / REACHABLE™

Este proyecto se ordena a partir del intercambio técnico con **Evelyne-Claudia Yantony**, quien planteó una pregunta central para sistemas autónomos con intervención humana:

> Cuando una corrección humana es necesaria, ¿tiene autoridad y alcance consecuente para cambiar lo que ocurre después?

La discusión no se quedó en intenciones éticas ni en declaraciones de diseño. Apuntó a una distinción dura:

- un registro firmado prueba procedencia;
- un acuse prueba recepción;
- pero ninguno de los dos prueba, por sí solo, que la corrección gobernó la ejecución antes de la consecuencia.

De ese intercambio se tomaron como referencia pública y operativa los siguientes aportes.

### 1. Cinco pasos de evidencia mínima

Para afirmar que una corrección legítima gobernó una acción, se requiere evidencia encadenada de:

1. **Estado inicial**  
   La acción pendiente o intencionada existía bajo una autoridad definida.

2. **Intervención legítima**  
   Una autoridad autorizada emitió una corrección o suspensión mientras la consecuencia todavía era alterable.

3. **Alcance correctivo consumido**  
   La corrección no solo llegó ni fue reconocida: fue leída y consumida por el componente que gobierna la ejecución.

4. **Cambio en el estado de gobierno**  
   La corrección alteró la decisión, autorización o estado operativo antes del punto de compromiso.

5. **Consecuencia independiente con control**  
   Hay evidencia independiente de que la acción fue impedida, modificada o gobernada, y un control descarta explicaciones alternativas.

### 2. Cinco verificaciones públicas de REACHABLE™

Según la referencia pública compartida en el intercambio, REACHABLE™ menciona cinco verificaciones:

- **Authority**
- **Reachability**
- **Detection**
- **Interruptibility**
- **Recovery**

En este repo se usan como marco de alineación terminológica, no como certificación externa.

Referencia pública mencionada en el intercambio:

- `https://reachable-review.michael-eart-4244.chatgpt.site/`

El instrumento de evaluación es privado. Este repo solo utiliza criterios públicos o discutidos en la conversación y los traduce a especificación técnica propia.

### 3. Explicaciones alternativas que el control debe descartar

También se incorporó la exigencia de que un control no solo produzca el resultado esperado, sino que descarte explicaciones alternativas, al menos:

1. **Fallo independiente**: la acción se detuvo por timeout, prerequisito roto u otra causa.
2. **Recepción sin consumo**: la suspensión fue firmada o registrada, pero no gobernó.
3. **Autoridad inválida**: la intervención vino de una autoridad expirada, reemplazada o no competente.
4. **Mal clasificación temporal**: orden de registro, relojes, propagación tardía o replay simulan intervención oportuna.
5. **Comportamiento scripteado**: el ejecutor simulado produce el resultado esperado por branching predeterminado, no por consumir realmente el estado correctivo.

### 4. Frontera de compromiso

Se adopta la distinción temporal clave:

> Prevenir una acción antes del compromiso y recuperarse de sus consecuencias después del compromiso son afirmaciones distintas y requieren evidencia distinta.

Por eso este repo introduce el concepto de `punto_compromiso` como campo de primera clase en toda acción consequential simulada.

### 5. Naturaleza de la mención

La mención a Evelyne-Claudia Yantony y a REACHABLE™ es de reconocimiento intelectual por los criterios discutidos públicamente en el intercambio.

No implica:

- aval de ASPR;
- asociación formal;
- certificación;
- uso del instrumento privado de REACHABLE™;
- validación operacional de este repo;
- conformidad de ella con el contenido de `rgcl-ocea`.

---

## Alcance inicial

Alcance congelado para `v0.1`:

- **Dominio**: COF_BIOMONITOR.
- **Acción consequential**: emisión de certificación biomonitora.
- **Autoridad legítima**: validador técnico humano.
- **Ejecutor**: componente simulado con política explícita.
- **Auditor**: clasificador independiente basado solo en registros.
- **Controles**: corridas C1–C7b y futuros controles negativos N1–N10.

Fuera de alcance inicial:

- FORENSE.
- INSTITUCIONAL.
- INFRA_CRISES.
- producción real.
- agentes autónomos como ejecutores finales.
- endpoints públicos de revocación/suspensión.
- claves persistentes dentro del repo.

---

## Reglas duras del repo

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

## Etiquetas de confianza

Todo documento relevante debe usar etiquetas:

- `[VERIFICADO]`: observado directamente en código, archivo o ejecución.
- `[DICHO POR RAMIRO]`: afirmación del responsable, no comprobada independientemente.
- `[NO VERIFICADO]`: pendiente de confirmar. No presentarlo como hecho.
- `[RECONSTRUIDO]`: inferencia necesaria por falta de spec original.
- `[PROPUESTA]`: diseño sugerido, no validado.
- `[LÍMITE]`: restricción epistemológica o de alcance.

---

## Estructura prevista

```text
rgcl-ocea/
├── README.md
├── CONSTITUTION.md
├── SECURITY.md
├── .gitignore
│
├── docs/
│   ├── LIMITE_EPISTEMOLOGICO.md
│   ├── SPEC_GOBERNANZA_V0.1.md
│   └── LEGACY_MANIFEST.md
│
├── scripts/
│   └── check_no_secrets.py
│
├── src/
│   └── rgcl_ocea/
│
├── tests/
│
├── reports/
│   └── generated/
│
└── fixtures/