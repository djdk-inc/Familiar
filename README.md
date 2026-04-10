# Familiar

This is the right instinct. The phone should be the doorway, not the workplace.

What you are describing is not “another app.” It is a **personal agent runtime** with **SMS as the command line**.

Here’s the cleaned-up version of your idea.

## Core thesis

You should be able to text one number and reach an agent that already has your context, tools, permissions, and execution environment.

Not a chatbot floating in the clouds with amnesia.
A **persistent operator** that lives server-side, can act across your digital life, and uses text messaging as the simplest universal interface.

The phone becomes the remote control.
The real work happens on your machine or trusted server.

## The actual product

A **server-side life agent** that:

* is reachable through a single bidirectional channel, starting with SMS
* has access to your apps, email, calendar, files, browser automation, APIs, and internal tools
* runs actions in a persistent sandbox on your laptop or home/server box
* remembers ongoing work, priorities, people, preferences, and state
* can escalate from chat to richer interfaces only when needed
* eventually supports voice calls, not just texting

So instead of:

* open app
* log in
* navigate UI
* context switch
* repeat forever until death by a thousand taps

You do:

* “text the agent”

That is much more civilized.

## Product statement

**An always-available personal agent that can see, reason over, and act across my digital world through one familiar communication channel: text messaging.**

Or even tighter:

**A persistent life operator you text, backed by your own tools, credentials, memory, and execution sandbox.**

## What problem this solves

Right now, personal computing is fragmented across apps, tabs, logins, dead ends, and brittle automation.

You want:

* one conversational entry point
* one persistent agent identity
* one execution environment with tools and credentials
* one memory layer spanning your life
* one control plane for tasks, follow-up, and delegation

That means the agent is not just answering. It is:

* checking
* doing
* monitoring
* reminding
* drafting
* booking
* triaging
* researching
* practicing with you
* coordinating with other agents or tools under the hood

## Key design principle

**Separate interface from execution.**

Interface:

* SMS
* later voice
* maybe email or WhatsApp as additional front doors

Execution:

* laptop daemon, home server, or cloud runner
* browser automation
* API tools
* local files
* personal data stores
* task queues
* memory and auth services

The interface should be dead simple.
The backend should be powerful and messy on your behalf.

## System architecture

### 1. Communication layer

This is the single bidirectional user channel.

Start with:

* SMS via Twilio or similar

Later add:

* phone call with speech-to-text / text-to-speech
* WhatsApp
* iMessage bridge if feasible
* Telegram / Signal if desired

This layer does:

* receive inbound messages
* map sender to identity
* pass message to orchestrator
* return responses or status updates

### 2. Identity and trust layer

This is where the agent proves it’s talking to you and protects your life from chaos goblins.

Needs:

* phone number recognition
* allowlist of trusted senders
* step-up auth for sensitive actions
* approval flows for money movement, account changes, destructive actions
* session continuity across devices
* audit logs

Good pattern:

* low-risk requests can run immediately
* medium-risk requests require a confirmation text
* high-risk requests require stronger approval, maybe a magic link, passkey, or callout

### 3. Orchestrator

This is the brainstem.

It decides:

* answer directly
* ask a follow-up
* run a tool
* delegate to a specialist agent
* open a browser automation session
* queue a long-running task
* notify later with results

It should be stateful, not stateless-prompt soup.

It needs:

* conversation state
* task state
* world state
* user preferences
* retry logic
* escalation logic
* failure handling

Think:

* one executive assistant agent on top
* many worker capabilities underneath

Not a feral swarm. A staff meeting with one chairperson.

### 4. Capability layer

This is where actual work happens.

Capabilities include:

* email read/draft/send
* calendar scheduling
* contact lookup
* web browsing and research
* personal file retrieval
* note taking / memory updates
* reminders and recurring checks
* shopping / reservations / travel
* browser automation for sites without APIs
* app automation via Android device farm or a tethered device later
* messaging triage
* practice/coaching mode

Each capability should expose:

* what it can do
* what auth it needs
* what inputs it expects
* what outputs it returns
* what side effects it causes

### 5. Runtime / sandbox

This is the body.

Your idea here is exactly right: the agent sits on your laptop or trusted server with credentials and a full sandbox.

Options:

* local daemon on Mac mini / laptop
* home server
* cloud VM with VPN into home/private resources
* hybrid model: cloud orchestrator + local executor

The runtime should support:

* browser sessions
* local scripts
* MCP/tool servers
* file access
* queued jobs
* screenshots and artifact generation
* long-running automations

This is the difference between “chatbot” and “operator.”

### 6. Memory layer

Without memory, it’s just an expensive goldfish.

Memory should include:

* people and relationships
* preferences
* routines
* active projects
* pending tasks
* interaction history
* emotional context and communication style
* important documents and extracted facts

You likely want:

* short-term working memory for active tasks
* long-term structured memory for recurring facts
* document memory over your files, email, notes, messages
* episodic memory of what has been tried already

### 7. Approval and autonomy model

Very important.

The agent should not be either:

* powerless and annoying
* fully autonomous and one bad prompt away from setting your life on fire

Use modes:

* **advise**: research, summarize, draft
* **prepare**: queue actions, gather forms, draft responses
* **act with approval**: “Reply yes to send”
* **auto-act within policy**: low-risk repetitive operations
* **monitor**: watch for conditions and notify

That gives you trust without turning your digital life into a haunted house.

## What texting the agent should feel like

You text:

* “Find me a dinner spot for 6 near Condesa tonight under 1,500 MXN pp and book if available.”
* “What do I have tomorrow and draft replies to anything urgent.”
* “Pay attention to flights to Seoul in late June and text me if premium economy drops below X.”
* “Summarize what’s blocking me across email, calendar, and notes.”
* “Practice this difficult conversation with me.”
* “Pretend to be my manager and push back hard.”
* “Monitor my inbox for recruiter emails and draft responses.”
* “Look at my last three messages with X and tell me whether I’m coming off cold.”

That last cluster matters because your notes are not just about task automation. They also point toward **human simulation and reflection**.

## Second product hidden inside your notes

You also want a **social mirror / rehearsal partner**.

Not just:

* manage systems

But also:

* profile emotion
* reflect your tone
* help with delivery
* practice lines
* simulate hard conversations
* potentially use voice later

That is a separate but adjacent capability.

Two modes emerge:

### Operator mode

Gets things done across systems.

### Mirror mode

Helps you think, feel, rehearse, and communicate better.

Mirror mode could do:

* tone read on drafts
* conversation rehearsal
* emotional debrief
* negotiation roleplay
* date / work / family practice
* speech pacing and line refinement
* voice-based shadow boxing later

That is actually compelling. Half assistant, half sparring partner.

## MVP

Do not build “full digital life agent” on day one unless you enjoy pain as a hobby.

Build this first:

### MVP v1: SMS executive assistant

Capabilities:

* text in
* orchestration
* memory
* calendar
* email
* web research
* reminders
* simple approvals

Flow:

1. User texts a request
2. SMS webhook receives it
3. Orchestrator classifies task
4. It either answers, runs tools, or queues work
5. Sensitive actions require confirmation
6. Responses come back over SMS

That alone is already useful.

### MVP v2: personal runtime

Add:

* local daemon on your laptop/server
* browser automation
* private tools
* file system access
* secure credentials
* remote job execution

This is where it stops being “smart texting bot” and becomes “agent with hands.”

### MVP v3: life graph

Add:

* richer memory
* relationship context
* recurring routines
* proactive follow-up
* monitoring and watchlists

### MVP v4: voice + mirror mode

Add:

* call-in interface
* speech-to-text and TTS
* conversation rehearsal
* emotional/tone modeling
* speaking practice

## Recommended stack

For a practical build:

### Ingress

* Twilio SMS webhook

### Orchestrator

* a simple app server in Python or TypeScript
* Postgres for state
* Redis or a job queue for async work
* a workflow engine only if needed later

Start simple before you invent a cathedral.

### Agent framework

You do not need a giant framework at first.
You need:

* tool calling
* task state
* retries
* approval flows
* memory access
* logging

A clean custom orchestrator is often better than drowning in framework glitter.

### Memory

* Postgres for structured memory
* vector search only where useful
* document indexing over personal sources
* explicit memory writes, not vague “the model probably remembers”

### Tools

* email/calendar/contact integrations
* file access layer
* web search/browser automation
* internal scripts / MCP servers
* phone-call module later

### Runtime

* local agent daemon on Mac mini or laptop
* cloud relay/orchestrator
* secure tunnel/VPN if the runtime is not public
* ephemeral sandboxes for risky jobs

### Auth

* OAuth for user-connected services
* secret vault for tokens
* signed commands between orchestrator and runtime
* policy engine for approvals

## Important architecture choice

There are really two viable shapes:

### A. Cloud brain + local hands

Cloud handles:

* SMS ingress
* orchestration
* memory
* queues
* policy

Local runtime handles:

* browser automation
* local file access
* private services
* desktop tasks

This is probably the best balance.

### B. Fully local primary runtime

Your machine handles almost everything.

Pros:

* privacy
* direct access
* less complexity in some ways

Cons:

* availability
* uptime
* networking pain
* phone-to-laptop reachability issues

I would choose **cloud brain + local hands**.

Elegant enough. Less cursed.

## Safety and trust boundaries

This thing touches your life, so it needs grown-up guardrails.

You want:

* every action classified by risk
* approval rules
* action receipts
* human-readable audit log
* easy revoke / pause
* sandboxing for untrusted tasks
* per-tool permissions
* per-domain policies
* memory redaction / privacy zones

The dream is “always available.”
The nightmare is “always improvising with my bank account.”

## The emotional angle in your notes

“Familiar.”
“Text message.”
“Always there.”
“Practice lines.”
“Shadow boxing a human.”

That says the product is not just utility. It is **relational infrastructure**.

You want something that feels:

* persistent
* reliable
* reachable
* low-friction
* emotionally legible
* useful in both logistics and life

That’s why SMS is so strong.
It feels human-scale. Low ceremony. No dashboard tax.

## Best one-line framing

Top 3 versions:

1. **A personal operator you text, backed by your own tools, memory, and execution environment.**

2. **An always-on life agent reachable by one phone number, able to act across your digital world with the right permissions.**

3. **A server-side assistant with local hands: one text channel in, full digital capability behind it.**

## Product spec draft

You could hand this to Claude Code or Codex:

```text
Build a personal agent system with SMS as the primary user interface.

Goal:
Create an always-available assistant that I can text from my phone. The assistant should maintain persistent memory, coordinate tasks, access personal tools and services, and optionally execute actions through a trusted runtime running on my laptop or home server.

Core requirements:
- Inbound and outbound SMS via Twilio
- Persistent identity tied to my phone number
- Conversation state and task state stored server-side
- Orchestrator that can decide whether to:
  - answer directly
  - call a tool
  - queue a job
  - ask for clarification
  - request approval for risky actions
- Tool integrations for:
  - email
  - calendar
  - contacts
  - web research
  - reminders/tasks
- Memory layer with:
  - user preferences
  - recurring facts
  - active projects
  - recent task context
- Approval system:
  - low-risk actions can auto-run
  - medium/high-risk actions require explicit confirmation by text
- Audit log of all actions and outputs
- Local runtime/daemon support:
  - secure registration with cloud orchestrator
  - ability to execute browser automation and local scripts
  - access private/local resources
  - receive jobs and return results
- Secure auth and secret storage
- Clear separation between interface, orchestration, memory, and execution

Desired UX:
- I text one number for everything
- The system feels familiar, low-friction, and persistent
- I do not need to switch between apps for most tasks
- The agent can help with both operational tasks and reflective/practice tasks

Future extensions:
- Voice call interface
- Emotional/tone modeling
- Conversation rehearsal / roleplay mode
- Proactive monitoring and notifications
- Multi-agent delegation under a single orchestrator
```

## Even tighter implementation breakdown

### Services

* sms-gateway
* orchestrator-api
* memory-service
* tool-service
* approval-service
* local-runtime-agent
* job-worker

### Database tables

* users
* channels
* conversations
* messages
* tasks
* task_runs
* memories
* tools
* approvals
* audit_events
* runtime_nodes
* secrets_metadata

### Core flows

* inbound_sms
* task_classification
* tool_execution
* approval_request
* approval_resolution
* local_runtime_dispatch
* notification_send
* memory_update

## Bottom line

Your idea is strong because it combines three things that usually stay separate:

* universal interface: **text**
* real capability: **sandbox + tools + credentials**
* persistent relationship: **memory + familiarity**

That is not “Claude Code but by SMS.”
That is a **personal operating layer for life**.

And frankly, that’s a much better hill to build on.

I can turn this into a sharper product memo or a full copy-pastable technical design doc next.
