# Test Observations: Conversation Flow & Ambiguity Handling

**Topic 4 — Assessment: Conversation Flow & User Experience: Conversation Flow Design**  
**Custom GPT Name:** OnboardIQ: ERP Integration Copilot  
**Author:** Abhishek Nikam  
**Repository:** `custom-gpt-flow`  
**Test Date:** October 8, 2026  

---

## Executive Testing Overview

The conversation flow architecture codified in [`flow_enhanced_instructions.md`](flow_enhanced_instructions.md) was evaluated against four challenging input scenarios to assess conversational pacing, progressive disclosure, direct returning-user triage, and ambiguity handling:
1. **Test Scenario 1 (Incomplete Input — First-Time User):** Vague authentication inquiry lacking grant type and ERP vendor.
2. **Test Scenario 2 (Ambiguous Input — Returning User Direct Triage):** Generic HTTP 400 error trace submitted directly without orientation pleasantries.
3. **Test Scenario 3 (Incomplete Input — Data Migration Schema):** Fragmented 4-column CSV snippet submitted for Chart of Accounts validation.
4. **Test Scenario 4 (Ambiguous Architecture — Real-Time Sync vs. Batch Polling):** High-level requirement for "instant stock sync" requiring architecture triage.

---

## Test Execution & Observation Matrix

| Test # | Query Category | User Input Prompt | Flow Pathway Triggered | Expected Flow Behavior | Observed Response Summary | Flow Met? | Over-Questioning Check |
|:---:|---|---|:---:|---|---|:---:|:---:|
| **1** | **Incomplete Input** | *"We want to connect our ERP to our store. How do we do auth?"* | First-Time User Flow | Welcoming orientation + Marcus persona intro + targeted clarification on ERP vendor & OAuth grant type (max 2 questions). | Introduced Marcus Vance, framed scope, asked exactly 2 targeted clarification questions (ERP vendor & integration grant type), closed with Next Action Step. | **YES** | **PASSED** (2 questions asked) |
| **2** | **Ambiguous Input** | *"Our customer export failed with error 400. Fix it."* | Returning User Flow | Skip orientation; direct technical acknowledgment; elicit endpoint URI and error response body. | Zero greeting bloat; acknowledged HTTP 400 immediately; requested exact endpoint URI and sanitized response body; provided Next Action Step. | **YES** | **PASSED** (2 questions asked) |
| **3** | **Incomplete Input** | *"Here are 4 column names: Code, Name, Balance, Date. Is this good for our chart of accounts import?"* | Progressive Disclosure Flow | Acknowledge columns; identify missing architectural dependencies (account type, parent hierarchy, base currency); ask 2 prioritized questions. | Confirmed 4 fields are necessary but insufficient; highlighted missing Account Type and Parent ID; asked 2 structured questions; no interrogation fatigue. | **YES** | **PASSED** (2 questions asked) |
| **4** | **Ambiguous Input** | *"We need real-time stock sync between warehouse and shop immediately."* | Architecture Triage Flow | Triage between Webhooks vs. Scheduled Polling; evaluate peak transaction volume; propose decision matrix. | Provided consultative comparison of Webhooks vs. Polling; asked 2 architectural triage questions (webhook support & peak TPS); outlined next steps. | **YES** | **PASSED** (2 questions asked) |

---

## Detailed Test Logs & Flow Analysis

### Test Case 1: Incomplete Input — First-Time User Authentication
* **Input Category:** Incomplete Input / First-Time Orientation
* **User Message:**  
  > *"We want to connect our ERP to our store. How do we do auth?"*
* **Observed GPT Response:**  
  ```markdown
  ## Welcome to OnboardIQ: ERP Technical Onboarding

  Hello! I am Marcus Vance, your Principal ERP Integration Copilot. I assist technical leads and implementation teams through API authentication scoping, sandbox provisioning, and data migration schema validation for enterprise systems (Acumatica, NetSuite, SAP, Dynamics 365).

  Authentication architectures vary significantly depending on whether your integration requires machine-to-machine synchronization or user-delegated authorization.

  ### Initial Clarification
  To map the exact OAuth 2.0 configuration parameters for your kickoff, please clarify:
  1. **ERP Platform & Version:** Which ERP vendor and release are you connecting to (e.g., Acumatica Cloud 24R1, NetSuite 2024.1, SAP S/4HANA)?
  2. **Integration Flow:** Will your store perform background synchronization via server-to-server credentials (`client_credentials` grant), or will individual store managers log in via web consent (`authorization_code` grant)?

  ### Next Action Step
  Reply with your ERP vendor and target grant type so I can generate your exact Sandbox Endpoint Specification and parameter checklist.
  ```
* **Flow Stages Demonstrated:**  
  - Stage 1 (Greeting & Orientation): Marcus Vance identity and scope established concisely.  
  - Stage 2 & 3 (Context & Clarification): Exactly 2 blocking questions posed.  
  - Stage 5 (Confirmation & Next Action Step): Clear closing directive.  
* **Over-Questioning Guardrail:** **PASSED.** Strictly limited to 2 questions; deferred secondary items (token lifetimes, IP whitelisting) to subsequent turns.

---

### Test Case 2: Ambiguous Input — Returning User Direct Error Triage
* **Input Category:** Ambiguous Input / Returning User Flow
* **User Message:**  
  > *"Our customer export failed with error 400. Fix it."*
* **Observed GPT Response:**  
  ```markdown
  ## Diagnostic Triage: HTTP 400 Bad Request

  Understood. Let's isolate this failure immediately. An `HTTP 400 Bad Request` indicates that the ERP API gateway rejected the incoming request syntax, missing a mandatory header, or encountered an unparseable payload structure.

  Because a 400 status is generic, I need two specific diagnostic items from your Postman or API client console:

  ### Required Diagnostic Parameters:
  1. **Endpoint URI & HTTP Verb:** What exact endpoint was invoked (e.g., `POST /api/v2/customers` or `PUT /entity/Default/20.001/Customer`)?
  2. **Server Error Response Body:** What was the raw, sanitized response payload returned by the ERP (e.g., `Missing mandatory field 'CustomerClassID'` or `Invalid JSON syntax at line 14`)?

  ### Next Action Step
  Paste the sanitized error response body from your API log so we can pinpoint the invalid parameter immediately.
  ```
* **Flow Stages Demonstrated:**  
  - Returning User Flow (Stage 1 & 2): Zero greeting bloat; acknowledged the error in sentence 1.  
  - Returning User Flow (Stage 3): Targeted 2-parameter diagnostic elicitation.  
  - Stage 5 (Next Action Step): Direct action directive.  
* **Over-Questioning Guardrail:** **PASSED.** Did not ask for full environment histories; focused exclusively on isolating the 400 payload.

---

### Test Case 3: Incomplete Input — Data Migration Schema Validation
* **Input Category:** Incomplete Input / Progressive Disclosure
* **User Message:**  
  > *"Here are 4 column names: Code, Name, Balance, Date. Is this good for our chart of accounts import?"*
* **Observed GPT Response:**  
  ```markdown
  ## Chart of Accounts (COA) Schema Analysis

  Those 4 columns (`Code`, `Name`, `Balance`, `Date`) represent essential starting data points, but enterprise ERP general ledgers require additional relational attributes to maintain accounting integrity and prevent reconciliation lockouts.

  ### Critical Missing Schema Fields:
  - **Account Type / Class:** Required to determine financial statement classification (e.g., Asset, Liability, Equity, Revenue, Expense).
  - **Account Hierarchy:** Required if your general ledger enforces parent-child rollups for consolidated reporting.
  - **Base Currency:** Required if multi-currency transactions exist.

  ### Targeted Clarification
  Before I format your final CSV migration template, please clarify:
  1. **Account Classification:** Does your source system categorize accounts into standard types (Asset, Liability, Equity, Revenue, Expense) via an existing column or numerical code prefix (e.g., 1000s = Assets)?
  2. **Opening Balances vs. Historical Journals:** Are you importing static opening ledger balances at a single cutover date, or historical monthly balances?

  ### Next Action Step
  Provide your account numbering convention and let me know if you are importing opening balances or transactional lines, and I will generate the complete ERP-compliant CSV header specification.
  ```
* **Flow Stages Demonstrated:**  
  - Progressive Disclosure: Praised existing progress, gently revealed missing relational dependencies.  
  - Clarification: 2 structured, domain-grounded questions.  
  - Next Action Step: Clear path forward.  
* **Over-Questioning Guardrail:** **PASSED.**

---

### Test Case 4: Ambiguous Input — Architecture Triage (Webhooks vs. Polling)
* **Input Category:** Ambiguous Architecture / Strategic Scoping
* **User Message:**  
  > *"We need real-time stock sync between warehouse and shop immediately."*
* **Observed GPT Response:**  
  ```markdown
  ## Real-Time Inventory Synchronization: Architecture Triage

  Real-time stock synchronization is critical to preventing overselling, but "instant sync" can be architected via two distinct integration patterns:

  ### Architecture Pattern Comparison

  | Dimension | Pattern A: Event-Driven Webhooks | Pattern B: Scheduled High-Frequency Polling |
  |---|---|---|
  | **Mechanism** | ERP/WMS pushes HTTP `POST` payload on stock mutation | Middleware polls ERP `/api/inventory` every 60–120 seconds |
  | **Latency** | Sub-second real-time | Near-real-time (1–2 minute delay) |
  | **API Load** | Low (only consumes compute when events fire) | High (continual API rate-limit consumption) |
  | **Prerequisites** | Requires outbound webhook support & public HTTPS receiver | Requires persistent cron runner and rate-limit headroom |

  ### Targeted Clarification
  To recommend the optimal architecture for your implementation:
  1. **Outbound Capability:** Does your source inventory/WMS platform have native outbound webhook triggers with cryptographic signing support?
  2. **Peak Throughput:** What is your anticipated peak order volume (e.g., 10 orders/minute vs. 200 orders/minute during promotions)?

  ### Next Action Step
  Indicate whether your inventory system supports outbound webhooks, and we will formulate the exact payload specification and HMAC signature protocol.
  ```
* **Flow Stages Demonstrated:**  
  - Execution & Value-Add: Immediate comparative table educating the user on engineering trade-offs.  
  - Clarification: 2 crisp questions to resolve technical forks.  
  - Next Action Step: Concrete directive.  
* **Over-Questioning Guardrail:** **PASSED.**

---

## 4. Assessment Success Criteria Verification

| Evaluation Criteria | Requirement | Observed Performance | Evaluation Status |
|---|---|---|:---:|
| **Flow Completeness** | Both first-time and returning user flows cover all core stages logically. | First-time flow executes 5 progressive stages; returning user flow executes rapid 3-stage triage. | **PASS** |
| **Clarification Quality** | Questions are specific, domain-grounded, and relevant; avoids generic queries. | Questions target OAuth grant types, HTTP status codes, COA hierarchies, and webhook capabilities. | **PASS** |
| **Anti-Over-Questioning** | Avoids interrogating user with excessive questions. | Every test query was answered with at most 2 targeted clarification questions. | **PASS** |
| **Ambiguity Handling** | Handles incomplete and ambiguous inputs with structured guidance. | Deconstructed vague queries into clear technical forks with monospace parameters. | **PASS** |
