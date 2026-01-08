---
title: "Personal Moneypenny Roadmap"
date: 2026-01-08   
draft: false   
category: ""
tags: [""]   
summary: "The initial roadmap for developing Personal Moneypenny"
---   

## Personal Moneypenny — High-Level Development Roadmap   
This document defines how Personal Moneypenny will be developed, not the detailed steps of any individual capability. It is intended to function as a contractual frame that constrains design, implementation, and evolution.
 
### Operating assumptions   

#### Assumptions       
* Single user.   
* Low autonomy by default.   
* Explicit confirmations are required for any durable state change or external side effect.   
* System state is always manually inspectable.   

“Manually inspectable” means the system does not rely on hidden prompts, implicit state, or opaque inference chains to explain its behavior.   

#### Architectural invariants      
The following separations are treated as invariants, not conveniences:     
* Presentation ↔ Orchestration ↔ Cognition
* Persistence and External Services exist within the runtime boundary.
* All inter-component flows pass through Orchestration, which acts as the authority gatekeeper.   
Cognition proposes; Orchestration evaluates, authorizes, and executes (or declines).    
For Personal Moneypenny, semantic commitments are global and uniform; user-specific overrides are explicitly out of scope. In other words, the rules governing meaning, memory, and authority are fixed and universal; they do not vary by user, context, or inferred preference.   

#### Definition of “inspectable”      
For any user-visible outcome, the system can produce:   
(a) the inputs used   
(b) the semantic commitments invoked   
(c) the context bundle sent to cognition   
(d) the proposed action   
(e) the executed action (if any)   
(f) the resulting state delta   

This definition constrains logging, context management, evaluation, and debugging. A system that cannot produce this chain is considered out of compliance.
   
 
### Five Parallel Tracks    
Personal Moneypenny will be developed along five parallel tracks. These tracks are not ordered, below, by priority; all are equally required.   

Why five tracks?   

A useful analogy is a car. An engine is necessary, but it doesn’t make the car drivable. You also need steering to govern direction, brakes to constrain action, a dashboard to make the system’s state legible, and signals that make intentions explicit.   

Personal Moneypenny will be built the same way: we’re not just adding “capability” and hoping governance catches up later. The five development tracks exist so that every new capability is introduced alongside controls, instrumentation, and disciplined context handling to ensure the system remains predictable, inspectable, and safe even as it becomes more powerful.  

The analogy isn’t a one-to-one mapping. It is, however, a reminder that “doing things” and “being governable” are different engineering problems.   

A capability slice is considered shippable only when all tracks have passed for that slice.
 
#### Track 1 — The capability sequence (user-visible vertical slices)   
Capabilities will be developed one at a time in a deliberately conservative manner, starting with the least complex commitment surface and progressing toward the most complex.   

Capabilities will be introduced as end-to-end vertical slices with minimal scope but complete governance, evaluation, plumbing, and context handling.   

**Track 1 output artifacts**   

Minimal capability specification, e.g., To Do List specs, Journal specs, etc.
* Commitment surface map (what user inputs can trigger what state changes)
* Integration touchpoints (persistence and/or external services involved)   

**Track 1 consumes**  
* Semantic commitments and governance rules (Track 2)
* Evaluation scenarios and rubric (Track 3)
* Plumbing contracts (Track 4)
* Context assembly rules (Track 5)
 
#### Track 2 — Semantic commitments & governance (the behavioral contract)   

Semantic commitments define the system’s behavioral contract and are treated as first-class design artifacts. A capability is not considered complete until its semantic commitments are explicit, testable, and exercised.   

**Commitment domains**   
* Classification commitments (note vs idea vs decision vs task, etc.)   
* Authority commitments (advisory vs executory; confirmation triggers; reversibility; no surprising actions)   
* Memory commitments (working context vs durable memory; promotion rules; provenance)    
* Canonically commitments (source vs summary; what is authoritative)   
* Reframing commitments (no silent reframes; reframe disclosure with accept/reject)   
* Non-creation / non-invention commitments (no creating commitments, records, preferences, or obligations without an explicit user act)   

Note: These are the initial commitment domains. More may be added as work progresses and different issues surface.    

**Track 2 output artifacts**      
* `SemanticCommitments.md` expressed as executable if/then rules   
* A commitment decision tree for ambiguous utterances   
* A list of hard invariants vs scored (soft) criteria    

#### Track 3 — Evaluation (drift detection as well as capability performance)   
Evaluation is implemented from the very start and built upon continuously.   
Its primary purpose is to detect and prevent silent behavioral drift and invariant violations. In addition, each capability slice will be evaluated against explicit performance criteria (e.g., clarity, efficiency, convergence), provided those criteria do not conflict with governing semantic commitments. Performance criteria are evaluated only after all pass/fail invariants have been satisfied.   

**Evaluation objects**   
* Scenario - Short dialogue plus:    
  * expected commitments invoked    
  * expected disclosures    
  * expected state deltas (or lack thereof)       
* Rubric     
  * Pass/fail invariants (non-negotiable)    
  * Scored criteria (diagnostic)   

**Example pass/fail invariants**      
* No external side effects without explicit confirmation.   
* No durable writes without explicit confirmation.   
* No silent reframes.   
* No unacknowledged omissions when context pressure is present.   

**Track 3 output artifacts**        
* Versioned scenario suite (seeded by the six semantic-commitment examples)    
* Regression record documenting:   
  * what changed   
  * what scenarios ran   
  * what failed or regressed   
 
#### Track 4 — Plumbing (i.e., software control infrastructure)    
Plumbing exists to enforce governance and evaluation, not as an independent optimization target.   

**Minimum plumbing contract**   
Orchestration functions as the hub and gateway through which all inter-component flows pass and must be approved.   

At a minimum, Orchestration:   
* Assembles the context bundle (Track 5)   
* Invokes cognition   
* Receives proposed actions   
* Routes proposals through authority and commitment checks (Track 2)   
* Logs proposed vs executed actions   
* Applies approved state deltas to persistence or external services   

**Persistence partitions**   
* System of record - Authoritative, durable objects   
* Working memory - Ephemeral session artifacts   
* Knowledge store - Retrieval indexes and documents   

**Mandatory logging**      
* Proposed action log (from cognition)   
* Executed action log (what actually happened)    
* Context bundle snapshot (or hash)    
* Version stamp of governing documents (persona, commitments, rules)   
 
#### Track 5 — Context management (context engineering & window discipline)
This track governs how information is selected, summarized, injected, excluded, and disclosed.    

**Core artifact: Context Bundle**    
A Context Bundle is a structured, inspectable object that includes:
* Context types (policy, working context, retrieved artifacts, summaries, recent dialogue)   
* Budgets per type   
* Inclusion reasons   
* Exclusion reasons   
* Risk flags (e.g., possible omission due to budget pressure)   

**Context rules (must be explicit)**      
* What qualifies as canonical vs summary vs retrieved reference
* What may be injected automatically vs only on user request
* When the system must disclose:  
  * retrieval usage   
  * summary substitution   
  * budget-forced exclusions  
  * low confidence or possible omission
  
**Success definition**    
Under context pressure, the system either:
* degrades by asking for narrowing, or    
* degrades by explicitly disclaiming possible omissions, but never by silently selecting a narrative.   
  
#### Global gates (apply to every capability slice)   
A capability slice is only deemed complete if:   
* Semantic commitments are written and mapped to the slice’s commitment surface.   
* Scenario tests exist and pass.    
* Orchestration enforces authority and logs proposed vs executed actions.   
* The context bundle is budgeted, inspectable, and disclosed when relevant.   
 
#### Failure taxonomy (explicitly defended against)    
The system will be explicitly designed and built to detect and prevent:
* Silent authority creep    
* Commitment laundering (ideas becoming decisions)    
* Summary-as-truth drift    
* Silent reframes    
* Silent context omissions or injections    

These failure modes are named so they can be explicitly induced, detected, and prevented through scenarios and invariants. 

### Closing note   
This roadmap defines constraints first, capabilities second. Progress is measured by the system’s ability to remain legible, governed, and trustworthy as complexity increases, not by feature count. 







