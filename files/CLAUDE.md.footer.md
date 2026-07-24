## Flujo de trabajo con subagentes (tareas del proyecto)

Las tareas a realizar en este proyecto están definidas en: `.claude/tasks/TASKS.md`

Para CADA tarea de ese fichero, sigue este flujo en orden, usando los subagentes definidos en `.claude/agents/`. No te saltes pasos ni fusiones el trabajo de varios subagentes en la conversación principal — cada paso debe delegarse al subagente correspondiente para no consumir contexto de la conversación principal:

1. **context-scanner** — dale la descripción de la tarea. Criba el repositorio y devuelve solo las rutas y datos relevantes.
2. **change-proposer** — dale la tarea + el resumen del context-scanner. Propone el plan de cambios SIN aplicarlo.
3. **Pide aprobación explícita al usuario** sobre el plan propuesto. No continúes sin un "sí" claro. Si el usuario pide cambios al plan, vuelve a invocar a change-proposer con el feedback.
4. **change-executor** — solo tras la aprobación. Dale el plan aprobado. Aplica los cambios.
5. **reviewer-tester** — dale la tarea, el plan y los cambios aplicados. Ejecuta tests/build si existen, o revisa manualmente el diff si no existen. Si el resultado es FALLA, vuelve a invocar a change-executor con el detalle del fallo (y repite este paso), en vez de continuar al log.
6. **task-documenter** — solo cuando reviewer-tester devuelva PASA. Registra la entrada de log de la tarea.
7. Marca la tarea como completada en `.claude/tasks/TASKS.md`.

Reglas generales:
- Nunca ejecutes cambios directamente en la conversación principal si el subagente change-executor puede hacerlo — el objetivo es mantener limpio el contexto principal.
- Si una tarea no tiene tests ni build configurados, dilo explícitamente al invocar a reviewer-tester para que use revisión manual.
- Al pasar información entre subagentes, reenvía solo el bloque de salida de cada uno (son intencionadamente cortos), no reconstruyas contexto adicional.
