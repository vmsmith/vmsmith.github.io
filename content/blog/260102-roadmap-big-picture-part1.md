---   
title: "Big Picture Roadmap - Part 1 - First Cut"
date: 260102
draft: false  
category: meta-systems
tags: ["roadmap"]
summary: "A first look at Part I of the roadmap from here to Cletho"
---   

## From Here to Cletho: A Risk-First Roadmap   

This is the first of three posts that will attempt to map out the path from here to Cletho. This post deals with two things: (1) the broad contextual issues, and (2) the approach to Personal Moneypenny. The second and third posts will deal with CTL Moneypenny and Cletho, respectively.   

This overall roadmap is not a contract. It is a working theory for how to make progress while keeping failure modes visible, localized, and correctable. As such, it will almost certainly evolve over time.   

If you come from any kind of system-development background, when you think about a roadmap you probably imagine developing a sequence of features. In the case of an AI system, you might think: memory first, then retrieval, then tools, then agents. That framing is understandable, and largely correct, but it is not the entire way to think about this project. Feature delivery is important—and there will be a development track for that—but the central challenge here is a bit different from a standard IT system.   

We are ultimately building a system that remembers, reasons, and influences how people think over time. The underlying technology—an AI language model—is inherently non-deterministic: the system will not behave identically every time, even under similar conditions. And it will be interacting with human users whose behavior is itself unpredictable.
Such a system must be dependable in its commitments from the start. By this, we don’t mean that it must always be correct. We mean that it must behave consistently with its stated role, boundaries, and trust contract, even when it is uncertain or mistaken. In this context, flawless behavior refers to process rather than outcome: asking for clarification when it should, or expressing uncertainty when uncertainty is present.   

When the system does fail, those failures must be visible, understandable, and correctable to the developer (rather than quietly accumulating), and the user’s trust must be maintained. Here, failure does not mean being wrong; it means a breakdown in the system’s behavioral guarantees. In other words, failure means deviating from expectations rather than producing an incorrect answer. Examples would include subtly reframing a user’s problem without making that reframing explicit or treating a prior summary as authoritative without saying so.   

Because the system itself is natively non-deterministic, and because the humans it interacts with are inherently unpredictable, neither side of the interaction can be fully specified in advance. The central challenge, then, is not achieving perfection or eliminating failure, but managing risk under uncertainty, so that Cletho both performs and fails in explicitly defined, acceptable ways.   

This post is the first of three that, together, lay out a roadmap from today’s start to a Cletho proof-of-concept, with two deliberate intermediate systems: Personal Moneypenny and CTL Moneypenny. In addition to fulfilling their stated roles as executive assistants, a key purpose of these intermediate systems is to develop, test, and refine the rules, boundaries, and recovery mechanisms that will ultimately govern Cletho itself.   

In that context, the two Moneypennys are not earlier versions of Cletho. They are environments in which different kinds of risk can be surfaced, understood, and constrained before Cletho exists at all.   
 
### The guiding principles   

Several principles govern this roadmap.   

** 1. Risk before capability**   

We prioritize confronting the riskiest unknowns early—especially those involving trust, memory, authority, and drift—before expanding the system’s capabilities. Risk does not disappear phase by phase; what changes is which risks dominate, and whether they are surfaced deliberately or allowed to emerge implicitly.   

The roadmap is structured to make the most consequential risks visible while they are still inexpensive to understand and correct.   

**2. Reusable components over one-off solutions**   

Every phase is designed to produce durable artifacts—specifications, schemas, policies, workflows, and evaluation criteria—that carry forward. These artifacts are not just implementation details; they are the mechanisms by which behavior, boundaries, and failure modes remain viable over time.   

**3. Early evaluations**   

Evaluation is treated as a critical component from the start, rather than a downstream concern to be addressed later. The same behavioral criteria used to define persona, boundaries, authority, memory semantics, failure handling, and other core system commitments in Personal Moneypenny will be used to evaluate those behaviors throughout the system’s evolution. As each system evolves, evaluation criteria will be developed, refined, and carried forward. What will change across phases is not what “good behavior” means, but the conditions under which it is exercised. This will allow evaluation to act as a stabilizer: making early decisions durable, later complexity testable, and subtle failures visible before they become entrenched.   
 
## Phase 1: Personal Moneypenny   

### Goal: Establish semantic commitments and governance in a forgiving environment   
Personal Moneypenny is functionally rich but architecturally conservative. It supports calendars, tasks, projects, journals, decision logs, research, reminders, and artifact indexing, but it does so in a context designed to be forgiving. For example:
* There is one user. 
* Autonomy is low. 
* Confirmations are explicit. 
* Failures are dealt with conversationally—between the system and the developer/user—rather than automatically by the system itself. 
* State is small enough to inspect and reason about manually.
Because this environment is intentionally forgiving, it can also create false confidence; some assumptions will appear sound here and fail later, which is precisely why they must be carried forward and tested again.
The contextual purpose of this phase is to minimize hidden interactions, i.e., cases where one action quietly changes how other parts of the system behave, without the user realizing it at the time. And a central aim is to make the system’s behavioral constraints as explicit as its functional capabilities.
Phase 1 answers questions such as:
* What counts as durable memory versus working context?
* What behaviors must always hold, regardless of task or prompt?
* How is uncertainty expressed?
* When the system proposes an action or a memory update, who has final authority?
* What must never happen, even if a prompt appears to invite it?
These are not implementation questions; they are semantic commitment questions. They ask what actions and statements mean, and what they obligate the system to do later.
Implementation questions ask:
* How is this stored?
* What API do we call?
* How often do we retry?
* What data structure do we use?
* What model or tool do we invoke?
Semantic commitment questions ask:
* Is this a note, a decision, or a tentative idea?
* Does this statement commit the system to future behavior?
* Can this be revised later, and by whom?
* Does storing this change how future reasoning should proceed?
* Is this advisory, descriptive, or prescriptive?
These are questions of what it means to do the thing at all, and again, they are important because they determine what the system is obligated to do later.
These distinctions only become clear in practice; representative examples are documented here and are treated as part of the roadmap itself: 
[Semantic commitment examples](link to a separate page) (e.g., decisions vs. notes, memory promotion, authority boundaries, summaries, and reframing)
### What risks Phase 1 is designed to surface
**Conceptual drift**
Without explicit identity, tone, and boundaries, systems become inconsistent. They answer similar questions differently on different days and overreach in subtle ways. Phase 1 forces these rules to be made explicit.
**Unbounded or accidental memory**   
Memory is one of the most consequential capabilities an AI system can have. Once information is treated as durable memory, it begins to shape future reasoning and behavior. Phase 1 defines what information may persist, under what conditions, and with what provenance. Without this, tentative or contextual information can quietly harden into assumed truth.
**Implicit authority**  
If it is unclear when the system is advising versus deciding, users lose agency without noticing. Phase 1 establishes clear lines: when the system must ask, when it may suggest, and when it must refuse.
### What Phase 1 produces
The contextual output of Phase 1 is not code. It is specifications:
* Persona and interaction principles
* Tone and boundary rules
* Memory semantics and lifecycle definitions
* Architectural responsibilities
* Core data schemas and provenance expectations
A core goal of Phase 1 is to understand Personal Moneypenny’s behavioral rules as clearly as its surface-level capabilities. That is to say, when it is as easy to explain what Personal Moneypenny is allowed to do, what it is not allowed to do, and how conflicts are resolved as it is to explain Personal Moneypenny’s functional capabilities. At that point, new capabilities can be deliberately added, rather than allowing new behaviors to emerge implicitly through implementation details.
Finally, it should be noted that because the developer and the primary user are the same person—to wit, me—this makes assumptions easier to surface but also easier to overlook. This will be something to watch carefully.
Parts II (CTL Moneypenny) and III (Cletho) to follow soon. 

