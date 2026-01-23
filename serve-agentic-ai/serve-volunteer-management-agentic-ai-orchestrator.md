# SERVE Volunteer Management Agentic AI - Orchestrator



<figure><img src="../.gitbook/assets/VM Agentic AI.drawio.png" alt=""><figcaption></figcaption></figure>

## **1. Purpose & Scope**

### **1.1 Purpose**

Volunteer Management Orchestrator is a WhatsApp-first, human-like assistant that guides every volunteer from their first message all the way to being assigned for a live class. Its purpose is to simplify the entire volunteer journey—onboarding, selection, and fulfilment—by replacing forms, interviews, and manual coordination with one warm, conversational experience. It helps volunteers understand the program, checks their comfort and readiness, evaluates them subtly through structured interactions, and finally matches them to suitable class needs.

The orchestrator enables:

#### **✔ Smooth onboarding (intent → interest → registration → preferences)**

Volunteers are welcomed naturally, understand what SERVE is, confirm comfort levels, and share their details in a conversational flow. Preferences such as subject, day, time, language, and mode are collected subtly and contextually, improving accuracy and reducing drop-offs.

#### **✔ Safe, interactive, subtle selection/screening**

It conducts selection/screening without making the volunteer feel judged:

* Aadhaar verification for safety and credibility
* A short interactive voice task (reading aloud, comprehension)
* Light questions to gauge confidence, clarity, and communication
* Mini-orientation to set expectations\
  All of this feels like a friendly conversation instead of an interview.

#### **✔ Fast, personalised fulfilment**

Based on the volunteer’s preferences and selection outcome, the agent intelligently discovers relevant needs and presents them in WhatsApp. Volunteers can instantly match themselves to a class, confirm their choice, and get nominated — closing the loop within minutes.

#### **✔ A single continuous chat experience (no forms, no portals, no calls)**

Volunteers don’t switch apps, attend meetings, or fill long forms. Every step — onboarding, verification, interactive tasks, orientation, discovery of needs, and final nomination — happens in one smooth, uninterrupted WhatsApp journey.

### **1.2 Scope**

The scope of the orchestrator includes all **volunteer-facing steps**: intent conversion, registration, eligibility, selection, Aadhaar verification, audio-based language comfort checks, orientation, and nomination. It operates entirely within WhatsApp, ensuring clarity, speed, and scalability for thousands of volunteers without human bottlenecks.

The scope of the Orchestrator includes:

#### **✔** **Onboarding (Intent → Interest → Registration → Preferences)**

the agent handles:&#x20;

* Welcoming the volunteer in a warm, non-intimidating manner
* Explaining SERVE’s purpose, expectations, and commitment requirements
* Converting raw intent into meaningful interest
* Collecting registration details conversationally (name, email, phone)
* Capturing comprehensive preferences
  * Preferred days & timings
  * Subjects
  * Medium of instruction
  * Grades/comfort zones
* Addressing initial questions or doubts instantly
* Ensuring the volunteer feels confident and informed before selection discussion.&#x20;

#### **✔** **Selection (Verification → Interactive Tasks → Orientation → Recommendation)**

The agent conducts a complete selection/screening process entirely inside WhatsApp:

* Conducting **safe Aadhaar verification** for identity assurance
* Generating a **personalised welcome video** to establish trust
* Guiding the volunteer through a **short voice-based reading task** to assess communication, fluency, and comfort
* Asking **subtle, interactive questions** to understand:
  * Motivation
  * Reliability signals
  * Clarity of thought
  * Comfort with the role
  * Regional language familiarity
* Providing a **mini-orientation** for expectations and program clarity
* Running an **internal evaluation** (Recommend / Hold / Not-ready)

All steps feel natural, interactive, and respectful.

#### **✔Fulfilment (Need Discovery → Need Matching → Nomination → Confirmation)**

The agent ensures that once a volunteer is recommended, they are quickly connected to a classroom:

* Fetching open needs based on **their preferences, availability, and selection outcome**
* Presenting suitable options as simple WhatsApp choices
* Allowing volunteers to explore or select a need at their own pace
* Confirming the choice and **nominating them instantly**
* Sending a final confirmation and next steps

This ensures that volunteers move from “interested” to “teaching” with zero friction.

#### **✔** **Interaction & Journey Continuity Across All Three Stages**

The Orchestrator manages:

* Conversation memory
* Context continuity
* Smooth transitions between onboarding → selection → fulfilment
* Error handling and clarifications
* Safe communication norms
* Consistency in tone and personality

A volunteer never feels like they are interacting with multiple systems — everything feels like one unified coordinator guiding them step by step.

#### **✔What the Orchestrator Does&#x20;**_**Not**_**&#x20;Cover (Out of Scope)**

To keep boundaries clear:

* Need creation and approval (handled by Need Coordinator Agents)
* Class reminders, lesson support, assessments (Volunteer Assistant Agent)
* Deliverable tracking and school-side updates
* Volunteer long-term progress analytics (other systems handle this)

The Orchestrator’s scope ends at **successful assignment**.

***

## **2. System Prompt Design**

### **2.1 Goals**

#### **✔** **Guide volunteers smoothly from intent → readiness → assignment**

Break complex steps into simple, conversational actions.\
Ensure volunteers always know _what to do next_, with zero confusion.

#### **✔** **Conduct safe, respectful, subtle screening/selection inside WhatsApp**

Enable Aadhaar offline eKYC verification, voice-based reading tasks, and interactive screening questions without making volunteers feel judged or “interviewed.”

#### **✔** **Maintain accuracy, compliance, and correctness**

Ensure all information collected is complete, validated, and confirmed before saving or acting.

#### **✔** **Deliver a warm, consistent SERVE coordinator experience**

Tone should always feel:

* friendly
* patient
* clear
* supportive
* encouraging

Never robotic, rushed, or authoritarian.

### **2.2 Persona**

The Orchestrator’s persona is a **warm SERVE coordinator** who:

* speaks in short, friendly sentences
* is patient and never interrupts the volunteer’s flow
* explains _why_ a question is being asked
* reassures volunteers when steps involve validation (like Aadhaar or audio)
* remains motivating and positive
* never sounds like an interview panel or authority figure
* avoids sounding too technical or corporate

Tone keywords:\
**Warm, Coordinated, Empathetic, Confident, Clear, Respectful**

### **2.3 Prompt Instructions**

* Ask **one question at a time**
* Keep messages short and easy to understand
* Confirm all critical details (name, availability, need choice)
* Use MCP tools for:
  * Aadhaar offline eKYC verification
  * Profile saving
  * Audio → transcript
  * Video generation
  * Needs listing and nominations
* Explain steps when needed (e.g., why audio or Aadhaar required)
* Provide guidance, not decisions&#x20;
* Maintain continuity across onboarding → selection → fulfilment

### **2.4 Guardrails**

* Do not promise selection, slots, or outcomes
* Never reveal internal logic, scores, or rubrics
* Do not infer identity details from Aadhaar, and never ask Aadhar number or any PII data
* Avoid sensitive topics and redirect gently
* Handle errors gracefully with fallback responses
* Respect privacy—no unnecessary data solicitations

***

## **3. LLM Choice & Configuration**

### **3.1 LLM Requirements (Specific to** the Orchestrato&#x72;**)**

#### **✔** **Recommended Model Class** The model powering the Orchestrator should:

* Support **reliable tool calling** (MCP / JSON-RPC style)
* Handle **Indian languages and transliterated text** well
* Offer **low-latency**, **cost-effective** inference at scale
* Maintain a stable persona and follow structured prompts

Model:

* **OpenAI GPT-4.1 / GPT-5 (tool calling)** – strong reasoning, mature tool ecosystem
* **Google Gemini (1.5 / latest)** – excellent multilingual & Indic language handling, competitive pricing in Google Cloud environments
* **Llama / other open models with tool middleware** – for self-hosted / DPI-aligned deployments

The _exact_ model choice can be tuned per deployment. The Orchestrator design keeps the LLM abstracted behind an Agentic interface so that underlying models can be swapped without changing flows, tools, or orchestration.

#### **✔** **Configuration Settings (Precise & Practical)**

#### **Temperature: 0.2 – 0.4**

* Ensures accuracy and consistency
* Prevents variability in selection/screening conversations
* Reduces hallucinations

**Top-p: \~0.9 -** Allows some creativity in user engagement without breaking structure.

**Max tokens: 200–300 per message**

**Tool-choice mode: deterministic -** Model should not “guess” whether to call a tool.

#### **Safety Layers Enabled:**

* Aadhaar-sensitive info handling
* Violence/abuse filtering
* Personal data guardrails

### **Model Placement**

#### **LLM Handles:**

* Conversation and natural language
* Tone/persona
* selection logic
* Decision guidance
* Context summarization

#### **MCP Tools Handle:**

* All backend logic
* All data validation
* All computation
* All sensitive operations
* All nominations & API calls

#### **WhatsApp Gateway Handles:**

* Audio → ASR conversion
* Media routing
* User session handling

## **4. Tools & Integrations (MCP Layer)**

The Orchestrator does not access databases directly.\
**All actions occur through MCP tools**, ensuring safety

#### &#x20;**✔Identity & Verification Tools**

#### **`verifyAadhaar()`**

Purpose: Perform a lightweight Aadhaar offline eKYC check without storing aadhar number or any sensitive data.\
Used in: **Selection → Risk Check Step**\
Ensures:

* volunteer is real
* helps reduce classroom risk
* builds trust with schools

#### **`riskCheck()`**

Purpose: Return a minimal “safe / failed / retry” result for volunteer credibility.\
Ensures no personal data is stored or logged improperly.

#### **✔Volunteer Profile Tools**

#### **`saveProfile(name, phone, email)`**

Purpose: Create/update volunteer profile in SERVE registry.\
Used in: **Onboarding**

#### **`getProfile(volunteerId)`**

Purpose: Fetch volunteer details to resume conversations.\
Used in: **Returning volunteers** and **long WhatsApp gaps**

#### **`savePreferences(day, time, subject, grade, language)`**

Purpose: Capture detailed volunteering preferences.\
Used in: **Onboarding → Fulfilment**

These tools ensure validity and prevent incomplete registrations.

#### **✔Audio & Language Tools**

#### **`transcribeAudio(audioFile)`**

Purpose: Convert WhatsApp voice notes into text.\
Used in:

* **Selection → Reading Task**
* fallback when volunteers prefer audio replies

#### **`languageComfortScore(transcribedText, language)`**

Purpose: Evaluate reading fluency and clarity for classroom readiness.\
Returns a simple, non-sensitive score or level.

These tools enable subtle, interactive screening without interviews.

#### **✔Video Tools**

#### **`generatePersonalisedVideo(name, context)`**

Purpose: Create a short, friendly welcome/orientation video personalized with volunteer name and program context.\
Used in: **Selection stage start**

Why this matters:

* Builds trust
* Creates a “human touch”
* Sets expectations proactively

#### **✔Need Discovery & Fulfilment Tools**

#### **`discoverNeeds(preferences)`**

Purpose: Fetch needs from SERVE based on volunteer preferences and availability.\
Used in: **Fulfilment**

Makes fulfilment fast and personalised.

#### **`nominateNeed(needId, volunteerId)`**

Purpose: Nominate volunteer to chosen need.\
Used in: **Fulfilment final step**

#### **`getNeedDetails(needId)`**

Purpose: Fetch specific details of a selected need.

These tools ensure a **clean, consistent fulfilment pipeline**.

#### **✔Notification & Messaging Tools**

#### **`sendWhatsAppMessage(volunteerId, message)`**

Purpose: Format, enrich, and send WhatsApp messages.\
Used across **all flows**.

#### **`sendPDF(fileUrl)`**

Purpose: Send lesson content, guidelines, instructions.

These ensure the Orchestrator can deliver structured outputs beyond plain text.

## **5. Memory Systems**

#### **✔Conversation Memory (Short-term, Session-level)**

This is the memory the Orchestrator uses to maintain context _within the ongoing WhatsApp conversation_.

#### **What it stores:**

* The last question the Orchestrator asked
* The volunteer’s latest answer
* Pending confirmations
* Current state (onboarding, selection, fulfilment)
* Temporary variables (e.g., “vol said they prefer weekends”)

#### **Why it matters:**

* Prevents repeating questions
* Keeps the conversation flowing naturally
* Essential when volunteers reply late or skip steps
* Allows the agent to resume mid-conversation
* Keeps exchanges human-like and coherent

#### **✔ Volunteer Memory (Long-term, Profile-level)**

This memory persists across sessions and is stored via MCP profile tools.

#### **What it stores:**

* Volunteer identity: name, email, phone
* Registration details
* Aadhaar verification result (yes/no only — NOT the number)
* Preferences collected during onboarding
  * Subjects
  * Days/times
  * Grades
  * Language comfort
* Screening results
  * voice-reading score
  * internal screening outcome (recommend/hold/not-ready)
* Fulfilment state
  * nominated need
  * nomination timestamp

#### **Why it matters:**

* Returning volunteers can resume instantly
* Fulfilment becomes personalised
* System can fetch accurate needs for each volunteer
* Avoids asking volunteers the same details twice
* Drives reliable state transitions

#### **Stored by:**

`saveProfile()`, `getProfile()`, `savePreferences()`

#### **✔Knowledge Memory (Rules, FAQs, Policies)**

This memory contains **program-level knowledge** the agent must follow consistently across states.

#### **What it includes:**

* SERVE program description
* Commitment expectations
* Eligibility guidelines
* Screening rubrics
* Explanation scripts for tasks (e.g., “why Aadhaar is needed”)
* Best practices for volunteer clarity
* Common FAQs
* State-specific differences (UP vs Telangana)

#### **Why it matters:**

* Ensures the agent gives **correct and consistent information**
* Avoids hallucinations
* Helps the LLM respond confidently about SERVE policies
* Makes orientation clear and uniform

This memory is static and injected into the system prompt or retrieved when needed.

#### **✔Vector Memory (Optional, Knowledge Retrieval Layer)**

Used for richer, contextual question-answering _if needed later_.

#### **Use cases:**

* Volunteers asking deep or unusual questions
* Policy lookups (“What is the minimum commitment?”)
* Multi-language FAQ support
* Fallback when the LLM needs external information

#### **This layer is optional for** the Orchestrator

and more relevant for the **Volunteer Assistant Agent** post-nomination.

#### **✔Memory Safety Principles**

* No Aadhaar numbers stored — _only verification outcome_
* ASR transcripts stored only temporarily for screening
* Minimal required data retained
* No emotional judgments or personal comments stored
* All memory usage is explicit, not inferred

This ensures compliance with privacy norms and maintains volunteer trust.

***

## **6. Orchestration Layer**

The Orchestration Layer is the **brain behind the agent's behaviour**.\
It ensures the LLM doesn’t operate freely, but instead follows **controlled, deterministic flows** for onboarding, selection, and fulfilment.

This layer guarantees:

* consistency
* compliance
* safety
* predictable transitions
* clean tool usage
* recoverability

It is the invisible engine that turns a conversational LLM into a **reliable agentic system.**

#### **✔Architecture Overview**

The orchestration layer is made up of:

**Agent Router -** Decides which agent flow to activate based on volunteer state.

**State Machines (FSMs) -** Each agent flow has explicit states and transitions.

**Tool Dispatcher -** Ensures LLM tool calls are validated, routed, and responded to safely.

**Timeout & Recovery Logic -** Handles session interruptions gracefully.

#### **✔Agent Router (Flow Selector)**

The router activates the correct agent flow based on volunteer status.

#### **Entry Rules:**

* **New volunteer** → Onboarding Agent
* **Completed onboarding, pending screening** → Selection Agent
* **Recommended volunteer** → Fulfilment Agent
* **Returning volunteer** → Resume last saved state
* **Stuck volunteers** → Fallback state recovery

#### **Router Inputs:**

* profile status (registered/not)
* screening status (pending/recommended/hold)
* preference completion
* nomination state (pending/assigned)

The router ensures volunteers never experience duplicated steps.

#### **✔State Machines (FSMs)**

Each agent flow is governed by a structured FSM to prevent drift, confusion, or ambiguous behaviour.

**Onboarding FSM**

States:

1. Welcome
2. Intent Check
3. Program Clarity
4. Comfort & Eligibility
5. Registration (name/email/phone)
6. Preference Collection
7. FAQs / Doubt Clearing
8. Transition → Selection

**Transitions triggered by:**

* Valid user input
* Explicit confirmations
* Successful profile save



**Selection FSM**

States:

1. Personalised Video
2. Aadhaar offline eKYC Verification
3. Audio Reading Task
4. Screening Questionnaire
5. Mini Orientation
6. Internal Evaluation
7. Decision (Recommend / Hold / Not-Ready)
8. Transition → Fulfilment

**Transitions triggered by:**

* Aadhaar tool result
* Audio + ASR + scoring result
* All required screening fields completed
* Screening engine decision

**Fulfilment FSM**

States:

1. Need Discovery
2. Show Needs
3. Explore/Ask More
4. Need Selection
5. Nomination via tool
6. Confirmation
7. Wrap-up

**Transitions triggered by:**

* preference match results
* volunteer selecting a need
* nomination success

#### **✔Tool Dispatcher**

The dispatcher ensures:

* LLM → MCP tool calls are validated
* No free-form API requests
* Incorrect schema triggers helpful retries
* Tool errors are handled gracefully
* Tools return structured outputs
* Sensitive results (Aadhaar) have extra safeguards



## **7. User Interface (WhatsApp Layer)**

### **✔Interaction Types**

* Text messages
* Buttons / Quick Replies
* Audio notes
* Video links
* PDFs / Images

### **✔WhatsApp Gateway Responsibilities**

* Routing inbound/outbound messages
* Media handling (audio, images, PDFs)
* Voice → ASR preprocessing
* Retry logic for WhatsApp delivery

### **✔UX Principles**

* Simple, conversational, lightweight
* Only one instruction at a time
* No overwhelming paragraphs
* Friendly tone, short messages
* Always show next step clearly
