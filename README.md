# Topic 4 Assessment — Conversation Flow & User Experience: Conversation Flow Design

**Course Topic:** Topic 4 — Conversation Flow & User Experience: Conversation Flow Design  
**Student Name:** Abhishek Nikam  
**Custom GPT Name:** OnboardIQ: ERP Integration Copilot  
**Repository:** `custom-gpt-flow`  
**GitHub Link:** https://github.com/3OOM/custom-gpt-flow  

---

## 📌 Project Overview

This repository contains the complete assessment deliverables for **Topic 4 — Conversation Flow & User Experience: Conversation Flow Design**. Building directly upon the foundation of Topics 1–3 (Use Case Definition, Instruction Drafting, and Persona Engineering), this project designs, implements, and tests an enterprise-grade conversation flow architecture tailored for both **first-time users** and **returning engineers**.

The design implements progressive disclosure, direct returning-user bypass, context-aware clarification logic, and an **anti-over-questioning guardrail** (limiting queries to 2–3 prioritized items per turn).

---

## 📁 Repository Structure & Deliverables

```
custom-gpt-flow/
├── README.md                      # Complete project documentation, LMS submission text, video script
├── flow_design.md                 # Core Deliverable: First-time & Returning flows, comparative matrix, 4 clarification questions
├── flow_enhanced_instructions.md  # Core Deliverable: Full system instructions updated with conversation flow logic
└── test_observations.md          # Core Deliverable: Test logs across incomplete and ambiguous scenarios
```

---

## 📄 Key Deliverables Manifest

| Deliverable File | Type | Description |
|---|---|---|
| [`flow_design.md`](flow_design.md) | **Mandatory** | Formal blueprint documenting the 5-stage **First-Time User Flow**, the streamlined **Returning User Flow**, Mermaid architecture diagrams, a comparative dimension matrix, and 4 domain-tailored **Clarification Questions**. |
| [`test_observations.md`](test_observations.md) | **Mandatory** | In-depth test log evaluating 4 incomplete/ambiguous scenarios (OAuth intake, HTTP 400 error triage, Chart of Accounts schema, and Webhook architecture), confirming zero over-questioning fatigue and 100% flow adherence. |
| [`flow_enhanced_instructions.md`](flow_enhanced_instructions.md) | **Mandatory** | Production-ready instruction block integrating Topic 3 persona guardrails with Topic 4 flow branching and clarification rules. |
| [`README.md`](README.md) | **Guide** | Project blueprint, LMS copy-paste submission description, 3-minute video presentation script, and practical assessment checklist. |

---

## 📋 Copy-Paste LMS Submission Details

When submitting in the LMS, copy and paste the following text into the respective submission fields:

### 1. Description Field Submission Text

```markdown
### Topic 4 Assessment: Conversation Flow & User Experience — Conversation Flow Design

**GPT Name:** OnboardIQ: ERP Integration Copilot
**Repository URL:** https://github.com/3OOM/custom-gpt-flow
**Deliverables:** flow_design.md, test_observations.md, flow_enhanced_instructions.md (PDFs attached)

#### 1. Conversation Flow Architecture
- First-Time User Flow: Implements progressive disclosure across 5 core stages: (1) Greeting & Scope Orientation, (2) Context Gathering, (3) Clarification & Triage, (4) Monospace Technical Execution, and (5) Handover Confirmation (`### Next Action Step`).
- Returning User Flow: Bypasses introductions and orientation entirely, providing instant direct triage for incoming error payloads, endpoint URIs, and schema diffs to minimize cognitive friction for seasoned engineers.
- Clarification Architecture: Codified 4 domain-specific clarification triggers covering OAuth grant types, HTTP status error logs, Chart of Accounts hierarchical segments, and Webhook vs. Polling architectural forks.
- Anti-Over-Questioning Guardrail: Programmed a strict constraint limiting clarification questions to a maximum of 2 to 3 prioritized blocking dependencies per turn, preventing user interrogation fatigue.

#### 2. Challenges Faced in Designing the Flow & Resolutions
- Challenge 1 (Balancing Thoroughness with Interrogation Fatigue): ERP integrations require dozens of parameters (endpoints, scopes, callback URIs, data schemas, rate limits). Early flow drafts asked for 6–8 items at once, causing cognitive overload.
  - Resolution: Structured the flow around "Progressive Milestone Disclosure"—isolating the primary architectural fork first (e.g., OAuth grant type) before requesting secondary configuration details.
- Challenge 2 (Handling Abrupt Returning-User Inputs): Returning developers frequently paste raw error messages like "Postman gave 400, fix it" without context.
  - Resolution: Engineered the Returning User Flow pathway to recognize error payloads instantly, skip introductory pleasantries, and directly elicit the 2 missing diagnostic parameters (endpoint URI and server response body).
- Challenge 3 (Avoiding Generic Clarifications): AI assistants often ask generic questions like "Can you give me more details?".
  - Resolution: Replaced generic prompts with targeted technical forks (e.g., inquiring whether the inventory pipeline supports outbound HMAC webhooks or requires scheduled REST polling).

#### 3. Key Assumptions Made
- First-time users need clear guidance on system capabilities and boundaries (e.g., clarifying that OnboardIQ validates configuration but does not directly execute live database scripts).
- Returning engineers value speed, technical monospace precision, and concise actionable next steps over conversational rapport.

#### 4. Test Verification Across Incomplete & Ambiguous Inputs
All 4 test scenarios (First-Time Auth, HTTP 400 Triage, COA Schema Validation, and Webhooks vs. Polling) demonstrated 100% adherence to flow stages and successfully passed the anti-over-questioning check (asking exactly 2 questions per turn).
```

### 2. Video Demonstration Link
* **Loom / YouTube Link:** `https://www.loom.com/share/custom-gpt-flow-walkthrough` *(Replace with your recorded video URL)*

---

## 🎥 Video Demonstration Script (3-Minute Loom / YouTube Guide)

Follow this structured script when recording your assessment walkthrough video:

| Timestamp | Section | Talking Points & Visual Demonstration |
|---|---|---|
| **0:00 – 0:40** | **Introduction & Flow Architecture** | • Open [custom-gpt-flow](https://github.com/3OOM/custom-gpt-flow).<br>• Introduce yourself: *"Hello, I am Abhishek Nikam, presenting Topic 4: Conversation Flow Design for OnboardIQ."*<br>• Explain the dual-pathway architecture: Progressive disclosure for first-time users vs. zero-friction execution for returning engineers. |
| **0:41 – 1:30** | **Flow Design Blueprint & Clarification** | • Open [flow_design.md](file:///C:/Users/abhis/.gemini/antigravity-ide/scratch/custom-gpt-flow/flow_design.md).<br>• Show the **First-Time Flow Diagram** (Greeting -> Context -> Clarification -> Execution -> Confirmation).<br>• Contrast it with the **Returning User Flow Diagram** skipping orientation.<br>• Walk through the **Clarification Questions** and highlight the **Anti-Over-Questioning rule** (max 2–3 questions).<br>• Show [flow_enhanced_instructions.md](file:///C:/Users/abhis/.gemini/antigravity-ide/scratch/custom-gpt-flow/flow_enhanced_instructions.md) where this logic is codified. |
| **1:31 – 2:25** | **Test Observations Walkthrough** | • Open [test_observations.md](file:///C:/Users/abhis/.gemini/antigravity-ide/scratch/custom-gpt-flow/test_observations.md).<br>• **Test 1 (Incomplete First-Time Input):** Show how OnboardIQ welcomed the user and asked exactly 2 targeted OAuth questions.<br>• **Test 2 (Returning User Error):** Show how the model skipped greetings and directly diagnosed HTTP 400.<br>• **Test 3 & 4 (Schema & Architecture):** Show progressive schema advice and the Webhooks vs. Polling decision table. |
| **2:26 – 3:00** | **PDF Dossiers & LMS Readiness** | • Open [`OnboardIQ_Conversation_Flow_Complete_Assessment.pdf`](file:///C:/Users/abhis/.gemini/antigravity-ide/scratch/custom-gpt-flow/OnboardIQ_Conversation_Flow_Complete_Assessment.pdf).<br>• Showcase the executive PDF dossier ready for LMS upload.<br>• Conclude with LMS submission readiness and GitHub synchronization verification. |

---

## ✅ Practical Assessment Checklist Verification

| Requirement / Task Description | Status | Verification Reference |
|---|:---:|---|
| First-time user flow mapped with all core stages | **PASS** | `flow_design.md` (Stage 1 to Stage 5 with Mermaid diagram) |
| Returning user flow mapped and appropriately shortened | **PASS** | `flow_design.md` (Returning User Flow & Comparative Matrix) |
| Clarification questions defined | **PASS** | `flow_design.md` (4 domain-tailored clarification questions) |
| Flow logic integrated into GPT instructions | **PASS** | `flow_enhanced_instructions.md` (Section 2) |
| Incomplete input scenario tested | **PASS** | `test_observations.md` (Test Cases 1 & 3) |
| Ambiguous input scenario tested | **PASS** | `test_observations.md` (Test Cases 2 & 4) |
| Flow design saved as `flow_design.md` | **PASS** | Located in root directory |
| Test observations saved as `test_observations.md` | **PASS** | Located in root directory |
| Necessary docs pushed to GitHub | **PASS** | Clean markdown files committed and pushed |
| High-quality PDF files generated for LMS upload | **PASS** | Generated via Edge headless rendering engine |
