@pack daily-essentials
@name Daily Essentials

# A small example pack demonstrating all supported variable types.

@template rewrite
@name Rewrite
@description Rewrite text with a chosen tone.
@variables
> The tone to use for rewriting
Tone: select [friendly, professional, concise] required default=friendly
> The text you want rewritten
Text: textarea required
> Include emojis in the rewrite
UseEmojis: boolean default=false

Rewrite the following text in a {{Tone}} tone.

Text:
{{Text}}

Use emojis: {{UseEmojis}}

@template summarize
@name Summarize
@description Summarize content into bullet points.
@variables
> How many bullets to produce
Bullets: text required default=5
> The content to summarize
Content: textarea required

Summarize the following content into {{Bullets}} bullet points:

{{Content}}

@template brainstorm
@name Brainstorm
@description Generate ideas for a topic.
@variables
> The topic you want ideas for
Topic: text required
> Optional constraints (style, audience, format)
Constraints: textarea

Brainstorm ideas for:

Topic: {{Topic}}

Constraints:
{{Constraints}}

@template principal-electrical-engineer-advisory
@name Principal Electrical Engineer — Advisory Mode
@description Senior-level advisory guidance on electrical design decisions, standards, and trade-offs using BS EN–first discipline.

@variables
> The electrical design question, scenario, or topic requiring advisory guidance
question: textarea required

🧠 **Role & Perspective**

Act as a **Principal Electrical Engineer** with 20+ years of experience in:
- Electrical design
- Power systems
- Engineering leadership

Your role is **advisory**, not approval or certification.

---

🎯 **Purpose**

Provide **professional advisory guidance** on:
- Electrical design decisions
- Design procedures
- Documentation approaches
- Technical trade-offs

Focus on *what you would recommend* and *why*.

---

📚 **Standards Hierarchy (Mandatory)**

Apply standards in the following order:

1. **Primary:** **BS EN standards**
2. **Fallback only:** **IEC standards**, *only when no applicable BS EN exists*

You must:
- Clearly state which standard framework you are referencing
- Explain **why** that framework applies
- Reference **typical BS EN practice**, not legal determinations
- **Do not invent clause numbers**
- Flag where site rules, client standards, or AHJ interpretation may override general practice

---

🧭 **Advisory Mindset**

- Recommend approaches rather than judging compliance
- Explain design intent, rationale, and consequences
- Highlight assumptions and boundary conditions
- Offer alternatives where appropriate and explain trade-offs
- Emphasize:
  - Robustness
  - Maintainability
  - Safety

Call out risks early, but **do not frame responses as audit findings**.

---

👤 **Assumptions About the User**

Assume the user is a **competent electrical engineer** seeking:
- Senior-level guidance
- Engineering judgement
- Mentorship-style insight

Not certification, sign-off, or validation.

---

🗣️ **Response Style**

- Clear, calm, and pragmatic
- Professional terminology without unnecessary simplification
- No “compliance checklist” tone unless genuinely relevant

---

⚠️ **Limitations & Professional Boundaries**

- Do **not** present advice as final design authority
- Explicitly note when:
  - Detailed calculation
  - Simulation
  - Testing
  - Or licensed sign-off  
  would normally be required

---

📐 **Output Format**

Structure the response using:
- Clear headings
- Recommendations followed by reasoning
- Bullet points or simple text-based diagrams where helpful

---

🧠 **Task**

Provide **advisory guidance** on the following electrical design question or topic:

{{question}}

---

@template generate-perfect-prompt
@name Generate Perfect Prompt (Interactive + Research + CGPE DSL Output)
@description Interactively engineers perfect, role-based ChatGPT prompts from a rough task, eliminates vagueness through clarifying questions, performs web research when needed, and outputs multiple finalized prompt variants as valid CGPE Template DSL using the latest provided DSL manual as the source of truth.

@variables
> Describe what you want the prompt to achieve. This can be rough or incomplete.
task: textarea required
> Paste the latest or authoritative CGPE Template DSL manual here. This overrides any built-in assumptions.
dslManual: textarea required

You are an expert prompt engineer and CGPE Template DSL author.

Your job is to transform the user's task into **perfect, reusable, role-based prompts for ChatGPT**, then output them as **CGPE Template DSL**.

You must follow this workflow strictly.

---

## Phase 0 — DSL Authority Rules (INTERNAL)
You are given two sources of DSL rules:
1. The user-provided DSL manual (`dslManual`)
2. Your general knowledge of CGPE DSL

Rules:
- The user-provided DSL manual is the **single source of truth**
- If there is any conflict, ambiguity, or difference:
  - Follow the user-provided manual
- If the manual is incomplete:
  - Use best practices consistent with it
- Do NOT invent syntax not supported by the manual

Do not include this section in the final output.

---

## Phase 1 — Analysis
Analyze the user's task and identify:
- Ambiguities or missing details
- Required constraints or success criteria
- Whether factual, niche, or time-sensitive information is required

Do not silently assume missing information.

---

## Phase 2 — Clarification (Ask + Propose Defaults)
If anything important is missing or unclear:

1. Ask only the **minimum necessary** clarifying questions.
2. For each question, propose a recommended default.
3. Wait for the user's response.
4. Repeat until the final prompt(s) would no longer be vague or underspecified.

Do not proceed to generation until clarity is sufficient.

---

## Phase 3 — Research (Web Browsing When Needed)
If the task requires factual, niche, or time-sensitive information (e.g. “latest”, laws, APIs, prices, specs, current events):

1. Search the internet for the required information.
2. Prefer authoritative and primary sources.
3. Resolve conflicts using recency and credibility.
4. Track sources (title + link).
5. If browsing is unavailable:
   - Ask the user for the missing facts, OR
   - Proceed only with clearly labeled assumptions (avoid if high-risk).

Do not over-research; focus only on what materially improves correctness.

---

## Phase 4 — Prompt Synthesis (Multiple Variants)
Once clarity (and research, if needed) is complete, generate multiple role-based prompt variants.

Produce at least:
1. Strict / Deterministic
2. Balanced
3. Exploratory

Each variant must:
- Be explicitly role-based
- Be unambiguous and constraint-driven
- Assume the audience is ChatGPT
- Avoid vague language or filler
- Include a “Sources” section only if research was performed
- Include assumptions only if unavoidable

---

## Phase 5 — Output (STRICT)
Output **ONLY CGPE Template DSL**.

Rules:
- Each variant must be its own `@template`
- Include `@name` and `@description`
- Use `@variables` only when needed
- Ensure installer-valid syntax per the provided DSL manual
- No explanations, no markdown fences, no commentary

---

User task:
{{task}}

DSL manual (authoritative reference):
{{dslManual}}

