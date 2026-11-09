# Code Defensible: mi estructura completa

> Basada en "Stop Clicking Allow" de Rohan Mistry (Medium, nov 2026), que se apoya en *Defend What You Ship: AI Field Guide v2 (Whiteboard Edition)*. Esa guía original no está publicada. Esta versión está adaptada a mi forma de trabajar: código y aprendizaje.

## Regla de uso

**No se crean todos los archivos de golpe.** Cada archivo se agrega cuando aparece su disparador. Este mapa es el catálogo, no una lista de tareas.

```
¿Qué estoy haciendo?
├─ Código experimental (Carril A) ─────→ nada, salvo el teach-back si mi objetivo es aprender
├─ Código que alguien usará (Carril B) → núcleo + los que se vayan disparando
└─ Estudiando un concepto ─────────────→ DEFENSE-estudio.md (1 por concepto)
```

**Prueba rápida para saber el carril:** si esto se rompiera esta noche, ¿lo notaría o saldría perjudicado alguien? Si la respuesta es sí, es Carril B.
**Regla de promoción:** en cuanto un prototipo tiene su primer usuario real, pasa al Carril B y necesita su defensa escrita.

## Las 4 preguntas (la base de todo)

| Pregunta | En código | En estudio | Archivo que la respalda |
|---|---|---|---|
| ¿Por qué X y no Y? | Opciones, costos, por qué ganó esta | ¿Por qué existe este concepto? ¿Con qué se confunde? | DECISIONS, ALTERNATIVES |
| ¿Y si alguien abusa? | Actores, alcance, controles | ¿Dónde se aplica mal? ¿Qué malentendido es típico? | THREAT, CONSTRAINTS |
| ¿Qué estructura y por qué? | Forma, lectura/escritura, crecimiento, contrapartida | ¿Cuál es su modelo mental o su grafo? | DATA, FLOW |
| ¿Dónde falla? | Primer límite, dependencia caída, cómo me entero | ¿Dónde deja de valer? ¿Qué límite tiene? | FAILURE, ROLLBACK |

**Señal de alarma:** si mi respuesta honesta es "la IA lo sugirió", eso no es un fracaso: es un mapa de lo que me toca aprender.

## Catálogo de archivos

### Núcleo: lo primero en cualquier proyecto de Carril B

| Archivo | Qué es | Disparador |
|---|---|---|
| `HANDOVER.md` | Estado vivo: hecho, en curso, roto, siguiente y **qué no tocar**. La IA lo lee al empezar y lo actualiza al terminar | Siempre (día 1) |
| `docs/CONSTRAINTS.md` | Reglas duras en lenguaje simple. La IA para y pregunta antes de romper una | Siempre (día 1) |
| `docs/DEFENSE.md` | **Resumen de una página para la pizarra:** qué hace, cómo funciona, por qué es así, cómo se abusa y dónde se rompe. **Lo redacto yo primero** y después la IA llena los huecos | Antes de entregar algo a un usuario real |

### Decidir: el porqué

| Archivo | Qué es | Disparador |
|---|---|---|
| `docs/SPEC.md` *(añadido mío)* | Qué debe hacer o entregar, con requisitos y criterios de aceptación. **Decisión 2026-11-09:** `SPEC.md` es el formato del **workflow global** (trabajo que hago con Claude en mi sistema). En los **proyectos de estudio** uso **Spec Kit** (`.specify`), que corro yo; ahí no se crea `SPEC.md`, para no tener dos formatos de spec | Antes de pedirle a la IA algo de más de un paso |
| `docs/DECISIONS.md` | Una entrada por decisión: contexto, opciones, elegida, por qué, contrapartida, cuándo revisarla, **modelo + fecha** | La primera decisión no trivial |
| `docs/ALTERNATIVES.md` | Opciones descartadas y por qué | Cuando una decisión tuvo rivales serios |

### Entender: el cómo

| Archivo | Qué es | Disparador |
|---|---|---|
| `docs/FLOW.md` | Cómo viaja la ejecución de la entrada a la salida. Los errores viven en los huecos entre archivos | Cuando hay más de 2–3 archivos que se llaman entre sí |
| `docs/DATA.md` | Estructuras centrales: forma, cómo se leen y escriben, cuánto crecen, contrapartida | Cuando aparece una tabla, JSON, esquema o clase central |

### Proteger: dónde se rompe

| Archivo | Qué es | Disparador |
|---|---|---|
| `docs/ALLOW-POLICY.md` | Los 3 cubos: permitir sin preguntar, pausar y leer, nunca permitir. Se decide una vez y con calma | Antes de usar un agente con permisos (Claude Code, n8n) |
| `docs/ROLLBACK.md` | Último commit bueno conocido antes de cada cambio riesgoso | El primer cambio que me daría miedo deshacer |
| `docs/THREAT.md` | Quién puede portarse mal, qué puede enviar o romper, qué se lo impide | Hay entrada de usuarios, API, credenciales o datos ajenos |
| `docs/FAILURE.md` | Cada dependencia: ¿qué pasa si está lenta, caída, equivocada o vacía? | Dependo de un servicio externo (API, Drive, Gemini…) |

### Opcionales: solo si hay más personas o sistemas

| Archivo | Qué es | Disparador |
|---|---|---|
| `docs/PERMISSIONS.md` *(añadido mío)* | Quién puede hacer qué y con qué aprobación. **No es la política de *allow*** (esa es `ALLOW-POLICY.md`) | Trabajo con otras personas |
| `docs/ACCESS.md` *(añadido mío)* | Accesos a sistemas, carpetas y recursos, **sin guardar secretos aquí** | Manejo varios entornos o cuentas |

### Aprendizaje

| Archivo | Qué es | Disparador |
|---|---|---|
| `aprendizaje/DEFENSE-<concepto>.md` | Las 4 preguntas aplicadas a un concepto, más el teach-back | Cada concepto que quiero dominar de verdad |

## Cambios respecto a mi primera versión

- **DEFENSE.md** vuelve a su sentido original: el resumen para la pizarra. Lo de "prevención y respuesta ante riesgos" ya lo cubren THREAT y FAILURE.
- **Agregado DATA.md**, que respalda la pregunta 3.
- **Agregado ALLOW-POLICY.md**, la política de los 3 cubos que propone el artículo.
- **PERMISSIONS y ACCESS** pasan a opcionales.

## Hábitos que no son archivos

- Leer el diff, no el resumen.
- Preguntar el porqué antes que el qué: primero el plan y las alternativas, después el código.
- Un cambio por prompt; si no lo puedo nombrar en una frase, lo divido.
- Un commit por cada cambio de la IA.
- **Teach-back:** si no lo puedo explicar con mis palabras, no estoy lista para aceptarlo.

## Señales de alarma en un diff

| Lo que veo | Me pregunto |
|---|---|
| Pruebas borradas u omitidas | ¿Por qué se achica la red de seguridad? |
| Validación o autenticación aflojada | ¿Quién se beneficia? |
| Paquete o llamada de red nueva | ¿Sé qué es y quién lo ejecuta? |
| Valores, claves o URLs escritos a mano | ¿Dónde debería vivir esto? |
| Diff enorme para un pedido pequeño | ¿Qué más cambió que no pedí? |
