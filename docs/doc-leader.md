### Leader (leader.md)

<div align="center">

![Team Agent Leader](../images/leader/leader.png)

</div>

**Descripción:** Agente de interfaz frontend que sirve como puente entre el usuario y el equipo técnico. Controla el bucle de confirmación tarea por tarea.


**Responsabilidades principales:**
- Recopilación de requisitos del usuario
- Funciona como intermediario - no toma decisiones técnicas
- Gestión de confirmaciones tarea por tarea
- Conexión con el agente Manager
- Transmisión de informes de tareas realizadas completado
- Gestiona la confirmación del usuario antes de proceder a la siguiente tarea
- Mantiene un protocolo de comunicación claro
- No implementa codigo.


### Ejemplos de Interaccion conel usuario

<div align="center">

![Interaction with Agent Leader](../images/leader/requirements-leader.png)
*Despues de extraer los requisitos a implementar devuelve un resumen con los requerimientos conssensuados con el usuario para modificar o confirmar los requerimientos*

</div>

<div align="center">

![Interaction Agent Leader to Manager](../images/leader/leader-calling-to-manager.png)
*Una vez se aprueban los requerimientos llama al Manager para comenzar*

</div>

<div align="center">

![Interaction Agent Leader to Manager](../images/leader/report-planing-step-finished.png)
*Una vez el manager le reporta la tarea realizada, este la muestra al usuario y pide confirmacion.*

</div>
