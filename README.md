# code-defensible-workflow

Plantilla del nivel **workflow**: las reglas y los archivos para tu forma de trabajar con un agente de IA en todo tu sistema, no en un proyecto concreto. Para el nivel de proyecto existe la plantilla hermana `code-defensible-project`.

Este repositorio es solo plantilla: no contiene datos personales. Copia lo que necesites a tu propio repositorio privado y rellénalo ahí.

## Qué contiene

| Ruta | Para qué sirve |
|---|---|
| `ESTRUCTURA.md` | Catálogo de archivos, con el disparador de cada uno. Se agrega un archivo cuando aparece su disparador, no antes. |
| `plantillas/` | Plantillas de `HANDOVER`, `DECISIONS`, `CONSTRAINTS`, `ALLOW-POLICY`, `ROLLBACK` y `DEFENSE`. |

## Cómo usarlo

1. Copia `ESTRUCTURA.md` a tu repositorio privado de workflow.
2. Copia solo las plantillas que tu trabajo pida ahora. Empieza por `ALLOW-POLICY.md` si usas un agente con permisos.
3. Escribe tus reglas reales en tu repositorio privado, nunca aquí.

## Decisiones de diseño

- **`DEFENSE.md`** es el resumen de una página para la pizarra. La prevención y la respuesta viven en `THREAT.md` y `FAILURE.md`.
- **`ALLOW-POLICY.md`** guarda los tres cubos (permitir, pausar, nunca). **`PERMISSIONS.md`** queda solo para trabajo con otras personas.
- Una sola carpeta `docs/` por proyecto.
- **`SPEC.md`** es el formato de especificación del nivel workflow. En los proyectos se usa Spec Kit, así que ahí no se crea `SPEC.md`.

## Origen

Adaptado de "Stop Clicking Allow" (Rohan Mistry, Medium, nov 2026), que se apoya en una guía de campo que no está publicada. Las adiciones y la organización son criterio propio y no están medidas.

## Licencia

MIT. Ver `LICENSE`.
