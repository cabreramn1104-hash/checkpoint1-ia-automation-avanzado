# Checkpoint 1 – Agente Base y Motor de Razonamiento

**Alumna:** Milagros Nazarena Cabrera
**Curso:** IA Automation Avanzado
**Archivo:** `checkpoint1_milagros_cabrera.json`

## Descripción
Agente "Asistente de Calificación de Leads" para NexoDigital (consultora ficticia de automatización con IA). Conversa con potenciales clientes, releva sus datos, los califica como CALIENTE, TIBIO o FRÍO y los registra en Google Sheets solo cuando corresponde.

## Arquitectura

```
[Chat de entrada] → [AI Agent · Tools Agent · máx. 7 iteraciones] → [Log de Observabilidad (Gmail)]
                          ├─ Chat Model: OpenAI GPT-4o
                          └─ Tool: Registrar Lead en Google Sheets
```

## Cumplimiento de la rúbrica

| Criterio | Implementación |
|---|---|
| System Prompt modular | Secciones Rol → Ámbito → Objetivo → Reglas → Lo que NO puede hacer → Escalamiento |
| Herramienta acoplada como Tool | Google Sheets Tool conectada al puerto *Tool* del agente, con Description de casos de uso y de no uso |
| Guardrail de iteraciones | Modo Tools Agent, `maxIterations = 7` |
| Log de observabilidad | Nodo final de Gmail con mensaje, respuesta, herramientas usadas y Execution Log (`intermediateSteps`) y estado "Tarea completada" |

## Planilla requerida
Hoja `Leads` con los encabezados:
`Fecha | Nombre | Email | Empresa | Necesidad | Presupuesto | Plazo | Calificacion | Motivo | Escalar_a_humano`

## Prompts de prueba
- **Usa la herramienta:** "Hola, soy Laura Gómez de Panadería El Trigal (laura@eltrigal.com). Quiero automatizar la toma de pedidos por WhatsApp, tengo USD 2000 de presupuesto y lo necesito en 2 meses."
- **No usa la herramienta:** "Hola, ¿qué hacen ustedes?"
