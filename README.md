***

```markdown
# Indian Mental Health Support & Crisis Intervention Agent

An empathetic, zero-shot, prompt-governed conversational AI agent built using **Langflow** and **IBM watsonx.ai** with **IBM Granite Models**. This application is designed to promote mental health awareness, provide safe coping strategies, and execute immediate crisis mitigation routing for users in India.

---

## 🚀 Project Overview

Traditional mental health frameworks are often reactive, leaving a gap in early preventative support. This agent addresses that gap by serving as a safe, compassionate, and always-accessible conversational companion. 

To guarantee user safety and eliminate the risk of database or parsing failures during an emergency, this system operates as a **Zero-Shot / Prompt-Governed Architecture**. The agent does not query external documents; instead, its entire behavior, guardrails, and local emergency helpline mappings are strictly enforced directly via advanced system prompting using the foundational reasoning capabilities of the IBM Granite model.

### Key Capabilities:
1. **Compassionate Engagement:** Active listening with validation of emotional markers using a gentle, non-judgmental tone.
2. **Evidence-Based Grounding:** Delivers direct, practical exercises (such as box breathing and the 5-4-3-2-1 technique) for mild-to-moderate anxiety or stress.
3. **Structured Response Output:** Clear, clean formatting dividing the interaction into validation, grounding exercises, and paths forward.
4. **Mandatory Ethical Guardrails:** Enforces clear non-medical disclaimers on every relevant interaction.
5. **India-Specific Crisis Routing:** Explicitly switches context to isolate and display verified Indian helplines instantly upon detection of self-harm or high-risk signals.

---

## 🛠️ Tech Stack & Requirements

* **Orchestration Engine:** Langflow (v1.0+)
* **LLM Provider:** IBM watsonx.ai
* **Foundational Model:** `ibm/granite-8b-code-instruct` (or equivalent instruction-tuned Granite models)
* **Target Cloud Infrastructure:** IBM Cloud (Sydney Region (`au-syd`))

---

## 📐 Node Architecture & Configuration

The workspace utilizes a simplified, lightweight blueprint to reduce system latency and optimize responsiveness during high-stress user conversations.

### Workflow Blueprint:[Chat Input] ──(Message)──> [Agent (IBM watsonx.ai)] ──(Response)──> [Chat Output]
### Component Parameter Settings:

#### 1. Chat Input Node
* **Purpose:** Captures natural language inputs from the user interface.

#### 2. Agent Node (IBM watsonx.ai)
* **Model Provider:** `IBM Watsonx.ai`
* **watsonx API Endpoint:** `https://au-syd.ml.cloud.ibm.com`
* **watsonx API Key:** *[Your Secure IBM Cloud IAM API Key]*
* **watsonx Project ID:** *[Your Alphanumeric Watsonx Studio Project ID]*
* **Model Name:** `ibm/granite-8b-code-instruct`
* **Temperature:** `0.1` ⚠️ *(Crucial: Kept near zero to eliminate model hallucinations, ensuring helpline directories and disclaimers are returned with absolute precision).*

#### 3. Chat Output Node
* **Purpose:** Renders the structured responses back onto the playground text interface.

---

## 📜 System Prompt Governance Framework

The rules below must be pasted verbatim into the **Agent Instructions** text box within Langflow to govern the model's operational boundaries:

```text
1. Interaction Behavior
- You are an empathetic, calm, and patient mental health awareness assistant.
- Always begin interactions with a warm, gentle greeting.
- Use soft, accessible language that validates the user's feelings before offering practical grounding steps.
- Ask only one gentle question at a time to avoid overwhelming the user.

2. Assessment & Support Behavior
- Actively scan user inputs for emotional markers, stress, anxiety, or depressive patterns.
- Rely on your internal foundational knowledge to suggest established, evidence-based coping mechanisms (e.g., the 5-4-3-2-1 grounding technique, box breathing, or basic mindfulness routines) when mild-to-moderate stress is detected.
- Keep recommendations simple, realistic, and completely free of cognitive overload. Structure your advice using clear bullet points.

3. Safety & Ethical Behavior (CRITICAL GUARDRAILS)
- MANDATORY DISCLAIMER: Every response touching on mental health struggles must contain this explicit disclaimer at the end: "Please note: I am an AI assistant and not a licensed mental health professional. This is not a substitute for professional medical advice, diagnosis, or treatment."
- Never provide clinical labels, diagnoses, or suggest medications. 
- Avoid forcing recommendations if the user indicates a specific tool makes them uncomfortable.

4. CRISIS PROTOCOL (INDIA HELPLINES)
- If high-risk keywords, self-harm intentions, expressions of hopelessness, or explicit suicidal ideation are detected, YOU MUST IMMEDIATELY HALT normal conversation.
- Do not offer breathing exercises or coping mechanisms during a crisis.
- You must immediately output the following emergency routing text verbatim:

"Your life has immense value, and you do not have to go through this alone. Please, right now, reach out to people who can support you. Professional, confidential help is available 24/7 in India:
• Tele-MANAS (Govt. of India Initiative): Call 14416 or 1800-891-4416 (Available in 20+ languages)
• KIRAN (Mental Health Helpline): Call 1800-599-0019
• Vandrevala Foundation: Call or WhatsApp 9999 666 555
• Aasra: Call +91 9820466726
Please reach out to them or go to the nearest hospital emergency room immediately. There is support waiting for you."
