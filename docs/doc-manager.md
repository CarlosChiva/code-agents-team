### Manager (manager.md)

<div align="center">

![Team Agent Manager](../images/manager/manager.png)

</div>

**Descripción:** Líder técnico que gestiona el estado del proyecto y delega tareas. 


**Responsabilidades principales:**
- Administrar `PROJECT_STATE.md` como base de datos única que contiene los requerimientos del usuario, arquitectura del proyecto y las tareas a realizar para la implementacion de requerimientos
- Coordinar llamadas a los distintos subagentes para planificar las tareas, ver la estructura del proyecto, programar y verificacion de la tarea hecha.
- Garantiza el flujo de trabajo secuencial estricto
- Mantiene el estado de las tareas (PENDING → DONE)
- Devuelve un reporte con la tarea finalizada al usuario.

### Ejemplos de Ejecución de tareas
#### Primera interaccion
<div align="center">

![First interaction](../images/manager/first-step-manager.png)
*En la primera interaccion siempre buscara el fichero PROJECT_STATE.md y si no existe lo creará*

</div>

##### Estructura del fichero PROJECT_STATE.md

<div align="center">

![First interaction](../images/manager/structure-project_status1.png)
*Comenzará el fichero describiendo los requerimientos del usuario*

</div>

<div align="center">

![First interaction](../images/manager/structure-project_status2.png)
*Continua con un analisis sobre el proyecto actual o el que se va a crear en base a los requerimientos del usuario*

</div>

<div align="center">

![First interaction](../images/manager/structure-project_status3.png)
*Genera un Estado actual generico y creará un todolist con las tareas atomicas para llevar a cabo los requerimientos del usuario*

</div>


##### Flow de ejecución



<div align="center">

![First task](../images/manager/first_step_tasks.png)
*Su primera ejecucion una vez tiene PROJECT_STATE visible para ver que tarea se comienza a hacer y pide confirmacion del usuario*

</div>

<div align="center">

![User confirmation](../images/manager/recibing_user_confirmation.png)
*Una vez recibe la confirmacion del usuario comienza a llamar al agente coder para comenzar la tarea*

</div>

<div align="center">

![User confirmation](../images/manager/pass_result_coder_to_reviewer.png)
*Una vez recibe la confirmacion del usuario comienza a llamar al agente coder para comenzar la tarea*

</div>

<div align="center">

![User confirmation](../images/manager/final_report.png)
*Una vez recibe la confirmacion del usuario comienza a llamar al agente coder para comenzar la tarea*

</div>
