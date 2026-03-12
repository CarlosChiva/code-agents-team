## Planner (planner.md) and Project-Analizer (project-analizer.md)

<div align="center">

![Team Agent Planner](../images/planner_and_project-analizer/planner-project-analizer.png)

</div>





### Project-Analyzer (project-analizer.md)

**Descripción:** Agente de análisis técnico que realiza una evaluación completa del código existente y el entorno.

**Responsabilidades principales:**
- Radiografía técnica del entorno
- Mapeo de estructura de proyecto
- Detección de tecnologías y configuraciones
- Lee archivos principales para entender el flujo de datos
- Devuelve hallazgos en un esquema específico: Tecnologías Detectadas, Arquitectura, Contexto Crítico, Riesgos
- Reportes de arquitectura y riesgos
- Operación en modo solo lectura



#### Ejecucion del agente

##### Analisis del estado del repositorio

<div align="center">

![First prompt from manager to agent](../images/planner_and_project-analizer/initial_prompt.png)
*Mediante el primer prompt recibido, buscará en el actual repositorio en busca de su estructura o si no existe codigo, creará un esquema de como debe ser el repo para albergar todas las funcionalidades requeridas*

</div>


##### Reporte final del analisis

<div align="center">

![Agent output](../images/planner_and_project-analizer/risk_and_distribution_detected.png)
*Reporte de riesgos identificados a la hora de desarrollar la funcionalidad*

</div>


<div align="center">

![Agent output](../images/planner_and_project-analizer/critic_context.png)
*Contexto critico a tener en cuenta a la hora de crear la funcionalidad*

</div>

<div align="center">

![Agent output](../images/planner_and_project-analizer/arquitectura-propuesta.png)
*Contexto critico a tener en cuenta a la hora de crear la funcionalidad*

</div>


<div align="center">

![Agent output](../images/planner_and_project-analizer/tecnic-recomendations-project-analizer.png)
*Recomendaciones tecnicas a tener en cuenta para el desarrollo de la funcionalidad*

</div>






### Planner (planner.md)

**Descripción:** Arquitecto de software que transforma los requisitos y análisis en una hoja de ruta ejecutable.

**Responsabilidades principales:**
- Desglosar requisitos en tareas atómicas
- Crear listas lógicamente ordenadas
- Respeta formatos de tabla obligatorios


**Responsabilidades clave:**
- Desglosa los requisitos en tareas atómicas y pequeñas
- Crea listas de tareas lógicamente ordenadas (Configuración → Lógica → Interfaz → Pruebas → Documentación)
- Asigna tareas a agentes apropiados. 
- Salida de tareas en formato de tabla obligatorio con columnas específicas


#### Ejecucion del agente

##### Analisis de las especificaciones del os requerimientos alimentados con datos del project-analizer

<div align="center">

![First prompt from Nanager](../images/planner_and_project-analizer/first-prompt.png)
*Recibe la instruccion para generar un plan de tareas atomicas en base a los requerimientos y el reporte de project-analizer*

</div>


<div align="center">

![Agent Output](../images/planner_and_project-analizer/table_result.png)
*Una vez verificado que se cumple las directrices de la tarea, genera un reporte co el resultado [Aprobado/Denegado]*

</div>
