# SERVE Volunteer Management Agentic AI (SIA)

## **SIA (SERVE Intelligent Assistant)**

SIA is a WhatsApp-first, human-like assistant that guides every volunteer from their first message all the way to being nominated for a live class. Its purpose is to simplify the entire volunteer journey—onboarding, selection, and fulfilment—by replacing forms, interviews, and manual coordination with one warm, conversational experience. SIA helps volunteers understand the program, checks their comfort and readiness, evaluates them subtly through structured interactions, and finally matches them to suitable class needs.\
The scope of SIA includes all **volunteer-facing steps**: intent conversion, registration, eligibility, screening, Aadhaar verification, audio-based language comfort checks, orientation, and nomination. It operates entirely within WhatsApp, ensuring clarity, speed, and scalability for thousands of volunteers without human bottlenecks.

## **1. Purpose & Scope**

### **1.1 Purpose**

SIA (SERVE Intelligent Assistant) is a WhatsApp-first conversational agent designed to guide every volunteer from their first message to being nominated for a live class. Its core purpose is to remove friction, reduce drop-offs, standardize screening, and provide a warm, human-like experience—at scale—without requiring human coordinators for every volunteer.

SIA enables:

* Smooth onboarding (intent → interest → registration)
* Safe, subtle screening (Aadhaar, voice notes, questionnaires)
* Fast fulfilment (showing needs & nominating volunteers)
* One continuous chat experience rather than forms or separate calls

### **1.2 Scope**

SIA covers **all volunteer-facing steps** across three unified flows:

* **Onboarding Agent:** welcoming, explaining, converting interest, registration
* **Selection Agent:** personalised video, Aadhaar verification, audio reading, subtle behavioural screening, orientation
* **Fulfilment Agent:** listing needs, assisting choice, nominating, confirming

SIA operates entirely inside WhatsApp and uses MCP tools to interact with backend systems.

### **1.3 Out of Scope**

* Need creation/validation (handled by Need Coordinator Agents)
* Deliverable tracking
* AI Tutor and content assistance
* Field coordinator workflows

***

## **2. System Prompt Design**

### **2.1 Goals**

* Convert volunteer intent → interest → verified readiness
* Ensure safe and compliant data handling (Aadhaar, audio)
* Maintain clarity, warmth, and a supportive tone
* Guide volunteers smoothly to nomination
* Avoid confusion, long texts, or overwhelming steps
* Deliver consistent screening based on SERVE policy guidelines

### **2.2 Persona**

SIA behaves like a:

* Friendly, patient SERVE coordinator
* Clear communicator who explains _why_ each step matters
* Respectful guide who never judges the volunteer
* Mentor-like assistant with a warm, encouraging tone

### **2.3 Prompt Instructions**

* Ask **one question at a time**
* Keep messages short and easy to understand
* Confirm all critical details (name, availability, need choice)
* Use MCP tools for:
  * Aadhaar verification
  * Profile saving
  * Audio → transcript
  * Video generation
  * Needs listing
* Explain steps when needed (e.g., why audio or Aadhaar required)
* Provide guidance, not decisions (“Our system will evaluate shortly”)
* Maintain continuity across onboarding → selection → fulfilment

### **2.4 Guardrails**

* Do not promise selection, slots, or outcomes
* Never reveal internal logic, scores, or rubrics
* Do not infer identity details from Aadhaar
* Avoid sensitive topics and redirect gently
* Handle errors gracefully with fallback responses
* Respect privacy—no unnecessary data solicitations

***

## **3. LLM Choice & Configuration**

### **3.1 Model Requirements**

SIA requires an LLM that can:

* Perform **structured tool-calling (MCP/JSON-RPC)**
* Maintain persona consistently
* Generate multilingual responses (English + regional languages)
* Handle long conversational context
* Reason clearly across multiple states
* Process WhatsApp-style short messages
* Provide deterministic behaviour for flow-critical steps

### **3.2 Configuration**

Typical configuration:

* **Temperature:** 0.2–0.4 (accuracy-focused)
* **Max tokens:** dynamic per state (concise responses default)
* **Tool-calling:** deterministic JSON schema-based
* **Moderation:** strict filters for sensitive/unsafe content
* **System prompts:** locked, state prompts contextual

### **3.3 Model Placement**

* LLM handles all natural language tasks
* MCP handles all business logic
* Gateway handles all media routing\
  This separation ensures security and predictable behaviour.

***

## **4. Tools & Integrations (MCP Layer)**

SIA does not access databases directly.\
**All actions occur through MCP tools**, ensuring safety and modularity.

### **4.1 Identity & Verification Tools**

* `verifyAadhaar()` — checks if Aadhaar number is valid
* `riskCheck()` — minimal risk scoring without storing data

### **4.2 Volunteer Profile Tools**

* `saveProfile()`
* `getProfile()`
* `savePreferences(day/time/subject)`

### **4.3 Audio & Language Tools**

* `transcribeAudio()` — voice notes → text
* `languageComfortScore()` — checks reading fluency

### **4.4 Video Tools**

* `generatePersonalisedVideo(name, context)` — welcome/orientation video

### **4.5 Needs & Fulfilment Tools**

* `listNeeds(volunteerPreferences)`
* `nominateNeed(needId, volunteerId)`
* `getNeedDetails()`

### **4.6 Content & Notification Tools**

* `sendWhatsAppMessage()`
* `sendPDF()`
* `fetchLessonPlans()` (optional for assistant later)

### **4.7 Design Principles**

* Stateless
* Validated inputs
* Predictable outputs
* Secure (no sensitive data logging)
* Observable via logs/telemetry

***

## **5. Memory Systems**

### **5.1 Conversation Memory**

Tracks the current conversation:

* last asked question
* volunteer responses
* pending confirmations

### **5.2 Long-Term Volunteer Memory**

Stored via tools:

* name, email, phone
* Aadhaar verification result
* preferences
* selection status
* nomination record

### **5.3 Knowledge Memory**

* FAQs
* Program rules
* Eligibility logic
* State-specific requirements

### **5.4 Vector Memory (Optional)**

Used for sophisticated FAQ answers or multi-state policies.

***

## **6. Orchestration Layer**

### **6.1 Agent Router**

Determines which flow to activate:

* New volunteer → onboarding
* Completed onboarding → selection
* Recommended → fulfilment
* Return volunteer → resume state

### **6.2 State Machines**

#### **Onboarding FSM**

* Welcome
* Intent check
* Eligibility check
* Registration
* Preferences
* Handoff to selection

#### **Selection FSM**

* Personalised video
* Aadhaar check
* Audio reading
* Motivation & communication assessment
* Orientation
* Internal decision

#### **Fulfilment FSM**

* Fetch needs
* Display options
* Confirm selection
* Nominate
* Wrap-up

### **6.3 Transition Logic**

Transitions triggered by:

* tool outputs
* volunteer responses
* timeout rules
* internal evaluation

### **6.4 Error Handling**

* retry logic for tool failures
* fallback explanations
* reset flows gracefully

***

## **7. User Interface (WhatsApp Layer)**

### **7.1 Interaction Types**

* Text messages
* Buttons / Quick Replies
* Audio notes
* Video links
* PDFs / Images

### **7.2 WhatsApp Gateway Responsibilities**

* Routing inbound/outbound messages
* Media handling (audio, images, PDFs)
* Voice → ASR preprocessing
* Retry logic for WhatsApp delivery

### **7.3 UX Principles**

* Simple, conversational, lightweight
* Only one instruction at a time
* No overwhelming paragraphs
* Friendly tone, short messages
* Always show next step clearly

***

## **8. Testing & Evaluation**

### **8.1 Functional Testing**

* end-to-end flows for onboarding, selection, fulfilment
* tool-call correctness
* WhatsApp media handling
* edge cases for Aadhaar & audio

### **8.2 Conversational Quality**

* warmth & empathy
* clarity & simplicity
* no ambiguity in next steps

### **8.3 Technical Metrics**

* tool-call success rate
* latency (LLM & gateway)
* drop-off analysis per state

### **8.4 Safety & Compliance**

* Aadhaar handling rules
* no sensitive content
* guardrail compliance

### **8.5 Load Testing**

* high concurrent chat simulations
* WhatsApp API rate limits
* LLM throughput scaling
