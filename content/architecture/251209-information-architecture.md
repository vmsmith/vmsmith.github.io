---
title: "Information Architecture: Categories and Tags"
date: 2025-12-06T00:00:00
draft: false
category: ""
tags: [""]
summary: "An overview of the information architecture"
---

This document defines the controlled vocabulary of **categories** and **tags** used across this site.  
Its purpose is to support consistent retrieval, long-term knowledge management, and future integration with CTL Moneypenny and Cletho.

Categories are stable, high-level conceptual buckets.  
Tags are cross-cutting descriptors used sparingly to enhance findability.

My information architectures are always informed by the 1956 paper, "The Magical Number Seven, Plus or Minus Two: Some Limits on Our Capacity for Processing Information," by George Miller. As the title implies, there are average limits to how much people can process. With that in mind, I've deliberately kept the number of categories to nine or fewer, and the same with the number of tags in each category.  

Each post receives **one category** and a small number of meaningful tags.

A separate **Tag Index** is maintained here at [Tag Index](/tag-index/)  

---

## Categories

### **persistent-knowledge**
Long-lived information that must exist outside the LLM, including structured documents, storage formats, indexing methods, long-term memory, and knowledge-base schemas.  
**Example tags:** `vector-store`, `supabase`, `github`, `embeddings`, `kb-schema`, `google-workspace`

### **integrations**
Systems Moneypenny interacts with and the mechanisms of those interactions.  
**Example tags:** `mcp`, `api`, `webhooks`, `slack`, `gmail`, `calendar`, `google-drive`, `github-api`, `supabase-api`

### **orchestration-layer**
Workflow and execution logic: planning agents, retrieval pipelines, context selection, error handling, tool orchestration, and step-wise jobs.  
**Example tags:** `rag`, `retriever`, `chunking`, `chain-of-thought`, `workflow`, `agents`, `pipeline`

### **cognition-layer**
The reflective layer that reasons about thinking: framing, assumptions, tradeoffs, uncertainty, heuristics, conflict detection, probing questions, and criteria formation.  
**Example tags:** `assumptions`, `framing`, `risks`, `goals`, `heuristics`, `conflicts-of-goals`, `decision-quality`

### **llm-layer**
Topics related to the model itself: prompting, system messages, model selection, token use, safety constraints, evaluation, and guardrails.  
**Example tags:** `prompting`, `system-prompts`, `temperature`, `context-window`, `benchmarks`, `llm-evaluation`

### **dialog-scripts**
Interaction frameworks: dialogue policies, structured question flows, nudges, reframing strategies, turn-taking, and metacognitive cues.  
**Example tags:** `topic-scripts`, `nudges`, `reflections`, `decision-flow`, `framing-questions`

### **user-interface**
User-facing surfaces across text, voice, or graphics, and early research on how users engage with AI systems.  
**Example tags:** *(to be added as the UI matures)*

### **meta-systems**
Topics about the development of Moneypenny itself: process improvements, debugging, versioning notes, retrospectives, and system evaluations.  
**Example tags:** `system-design`, `versioning`, `refactoring`, `debugging`, `evaluation`, `logging`, `milestones`, `workflow-tuning`

---

This taxonomy provides the foundation for a coherent knowledge structure across the site and supports future reasoning, retrieval, and cross-linking capabilities in CTL Moneypenny and Cletho.

