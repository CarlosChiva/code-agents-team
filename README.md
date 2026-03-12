# 📝 code-agents-team - Agente Configuración

Este repositorio contiene la configuración completa de un equipo de agentes especializados para la gestión automatizada de proyectos de desarrollo de software.

## ¿Qué es este proyecto?

code-agents-team es un sistema de agentes autónomos colaborativos diseñados para gestionar proyectos de desarrollo siguiendo un flujo de trabajo estructurado dentro de la herramienta OpenCode. Cada agente tiene un rol y responsabilidad específica, trabajando en secuencia para transformar requisitos de usuario en código funcional, manteniendo altos estándares de calidad y seguridad.

## 🏢 Equipo de Agentes

Este sistema consta de 6 agentes especializados:



<div align="center">

![Team Agent Configuration](images/team-image.png)


</div>


### 1. 🎯 Manager - Gestor Técnico del Proyecto

El líder técnico responsable de coordinar todas las operaciones del sistema. Administra el estado del proyecto a través del archivo `PROJECT_STATE.md`, delega tareas a los agentes apropiados y garantiza que el flujo de trabajo siga el ciclo INIT → PLANNING → EXECUTION.

[Documentacion Manager](docs/doc-manager.md)

### 2. ⚡ Coder - Ejecutor Técnico

El brazo de ejecución que implementa las tareas asignadas mediante la escritura o edición de archivos de código. Cumple estrictamente con los estilos de código existentes, prioriza las correcciones del agente de revisión y reporta detalladamente todos los cambios realizados.
[Documentacion Coder](docs/doc-coder.md)

### 3. 🔍 Coder-Reviewer - Guardián de Calidad del Código

El filtro final de calidad, revisando cada implementación del agente Coder para evaluar si debe ser aceptada o corregida. Proporciona retroalimentación técnica específica cuando el código no cumple con los estándares de calidad, seguridad, robustez y convenciones de código.
[Documentacion Coder-Reviewer](docs/doc-coder-reviewer.md)

### 4. 📋 Planner - Arquitecto de Software

Convierte los requisitos largos y complejos del usuario en una lista de tareas pequeñas, atómicas y lógicamente ordenadas. Utiliza formatos tabulares estructurados para organizar la ejecución desde configuración hasta documentación final.
[Documentacion Planner](docs/doc-planner-project-analizer.md#planner-plannermd)

### 5. 🔬 Project-Analyzer - Analista Técnico del Entorno

Realiza una radiografía técnica completa del entorno y estructura del proyecto existente. Mapea archivos, detecta tecnologías utilizadas, identifica arquitecturas y devuelve hallazgos críticos que sirven como base para la toma de decisiones técnicas.
[Documentacion Project-Analyzer ](docs/doc-planner-project-analizer.md#project-analyzer-project-analizermd)

### 6. 👤 Leader - Interfaz Usuario-Sistema

El puente humano-tecnológico que recopila los requisitos del usuario y conduce las confirmaciones tarea por tarea. Actúa como intermediario entre las necesidades humanas de los usuarios y la ejecución técnica, controlando el flujo de trabajo mediante confirmaciones claras.
[Documentacion Leader](docs/doc-leader.md)

---

## 🚀 Instalación

Este proyecto proporciona la configuración lista para usar de los agentes. Solo necesitas copiar los archivos al directorio de configuración apropiado.

### Pasos de instalación:

1. **Copiar archivos de configuración:**
```bash
cp -r agents/* ~/.config/opencode/agents/
```

2. **Configurar proveedores y modelos:**
Cada archivo de configuración debe ser editado para especificar el `provider` y el `model` que utilizarán. El formato es el siguiente:

```yaml
# Ejemplo de configuración de agente
name:  # nombre del modelo
description: # descripcion del modelo
mode: primary/subagent
# Configuración del proveedor (A EDITAR)
model: openai/gpt-4  # Cambiar según tu proveedor
temperature: 0.1 # cambiar a algun valor segun se pida ser mas estricto o creativo  
system_prompt: |
  Tu rol es administrar el estado del proyecto...
  

```

### Rutas de destino:

| Sistema Operativo | Ruta Destino |
|------------------|--------------|
| Linux/macOS | `~/.config/opencode/agents/` |

⚠️ **Importante:** No olvides editar cada archivo para configurar correctamente los valores de `provider` y `model` antes de usar los agentes.

---

## 📂 Estructura del Repositorio

```
code-agents-team/
├── agents/                    # Configuración de agentes
│   ├── orchestrator.md
│   ├── coder.md
│   ├── coder-reviewer.md
│   ├── planner.md
│   ├── project-analizer.md
│   └── senior.md
├── images/                     # Recursos visuales
│   └── ...
├── docs/        # Documentacion de cada agente
│   └── ...
└── README.md                   # Documentación
```

## 🔗 Flujo de Trabajo

El sistema funciona siguiendo un ciclo continuo:

```
Requisitos Usuario
        ↓
Senior (Interfaz) ← Consulta confirmación
        ↓
Orchestrator → Planner (Desglose)
        ↓
Coder (Implementación)
        ↓
Coder-Reviewer (Revisión)
        ↓
[Re-encoding si es necesario]
        ↓
Reporte de la tarea completada ✓
```

