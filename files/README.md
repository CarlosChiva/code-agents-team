# Kit de subagentes para tareas largas en Claude Code

## Qué contiene

```
.claude/agents/context-scanner.md    → criba el codebase (solo lectura)
.claude/agents/change-proposer.md    → propone el plan de cambios (solo lectura)
.claude/agents/change-executor.md    → aplica el plan aprobado
.claude/agents/reviewer-tester.md    → testea/compila, o revisa a mano si no hay nada de eso
.claude/agents/task-documenter.md    → escribe el log de la tarea
.claude/tasks/TASKS.md               → plantilla del fichero de tareas
CLAUDE.md.footer.md                  → texto a pegar al final del CLAUDE.md del proyecto
```

## Instalación (repite en cada proyecto: frontend, mobile, backend)

1. Copia la carpeta `.claude/agents/` completa a la raíz del repo (o a `~/.claude/agents/`
   si quieres que estén disponibles en TODOS tus proyectos en vez de solo en uno).
2. Copia `.claude/tasks/TASKS.md` a la raíz del repo y rellena las tareas reales.
3. Pega el contenido de `CLAUDE.md.footer.md` al final del `CLAUDE.md` del proyecto
   (créalo si no existe).
4. Ajusta si hace falta:
   - En `reviewer-tester.md` no hace falta tocar nada — detecta solo si hay tests/build.
   - Si un proyecto no usa git, quita la mención a `git diff` en `reviewer-tester.md`.
   - Puedes cambiar `model: haiku` por `model: sonnet` en `context-scanner.md` o
     `task-documenter.md` si quieres más calidad a cambio de más coste (son los dos
     subagentes más "mecánicos", por eso van en haiku por defecto).

## Cómo se usa

Con las tareas en `TASKS.md` y el footer en `CLAUDE.md`, basta con decirle a Claude Code:

> "Procesa la siguiente tarea pendiente de TASKS.md"

Y seguirá el flujo: context-scanner → change-proposer → (tu aprobación) →
change-executor → reviewer-tester → task-documenter, devolviendo en cada paso
solo el resumen corto de ese subagente, sin inundar tu ventana de contexto principal.

## Por qué reportes tan cortos

Cada subagente tiene su propio formato de salida fijo y muy breve (definido al final
de cada `.md`). Así el orquestador (la conversación principal) solo maneja esos
bloques pequeños para decidir el siguiente paso, en vez de arrastrar todo el
razonamiento intermedio de cada subagente.
