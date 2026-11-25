# 🤖 Agente Conversacional para WhatsApp Business (n8n + Groq + PostgreSQL)

Agente de Inteligencia Artificial con soporte de herramientas (*Tool Calling*) y memoria persistente integrado con **WhatsApp Cloud API**, orquestado mediante **n8n**, impulsado por **Groq LLM** y respaldado por **PostgreSQL** y **Google Sheets** para automatizar la atención al cliente y el agendamiento de citas.

🔗 **Portafolio Principal:** <https://aortegadevpa.github.io/Portafolio/>

---

## 🎯 Problema Resuelto

Los comercios locales reciben constantemente mensajes por WhatsApp consultando disponibilidad, servicios y horarios. Responder manualmente genera demoras, errores de doble reserva y pérdida de clientes fuera de horario laboral.

Este sistema automatiza toda la conversación manteniendo contexto histórico por usuario mediante **PostgreSQL** y ejecutando acciones reales sobre la agenda en **Google Sheets** gracias a un **AI Agent** conectado a **Groq**.

---

## 🏗️ Arquitectura del Workflow en n8n

```text
[WhatsApp Trigger]
       │
       ▼
[Filtro: Only Text Messages]
       │
       ▼
[AI Agent (n8n)]
  ├──► Chat Model: Groq LLM (Inferencia ultrarrápida + Tool Calling)
  ├──► Memory: Postgres Chat Memory (Historial conversacional persistente)
  ├──► Tool 1: consultar_agenda (Google Sheets - Read)
  └──► Tool 2: guardar_cita (Google Sheets - Append)
       │
       ▼
[Evaluación Condicional (If)] ──► [WhatsApp Send Message / Confirmación]
```

---

## ⚙️ Componentes Clave del Flujo

1. **WhatsApp Trigger & Filtro de Mensajes:** Escucha eventos entrantes de Meta Cloud API y filtra únicamente mensajes de texto válidos para evitar ejecuciones innecesarias.
2. **AI Agent + Groq Chat Model:** Procesa la intención del usuario con baja latencia y decide de forma autónoma cuándo consultar disponibilidad o registrar una reserva.
3. **Postgres Chat Memory:** Mantiene el contexto de la conversación de cada cliente en base de datos **PostgreSQL**, permitiendo diálogos naturales de múltiples turnos.
4. **Herramientas Conectadas (`Tool Calling`):**
   * `consultar_agenda`: Lee la hoja de cálculo en tiempo real para verificar horarios ocupados o disponibles.
   * `guardar_cita`: Registra los datos confirmados del cliente (nombre, fecha, hora y servicio) en Google Sheets.
5. **Enrutamiento Condicional (`If`) & Respuesta:** Valida la salida del agente y envía la respuesta o confirmación formateada directamente al WhatsApp del cliente.

---

## 🛠️ Stack Tecnológico

* **Orquestación:** n8n (AI Agent Workflow)
* **Modelo de Lenguaje (LLM):** Groq Chat Model
* **Memoria Conversacional:** PostgreSQL (`Postgres Chat Memory`)
* **Herramientas & Datos:** Google Sheets API (`read` / `append`)
* **Canal de Mensajería:** Meta Developers / WhatsApp Cloud API

---

## 📂 Contenido del Repositorio

* `flujo-agente-whatsapp-n8n.json` — Exportación completa del workflow de n8n.
* `README.md` — Documentación de arquitectura, memoria y herramientas del agente.

---

👤 **Desarrollado por:** [Angel Ortega](https://aortegadevpa.github.io/) — Desarrollo de Software & Automatización con IA (Panamá)
