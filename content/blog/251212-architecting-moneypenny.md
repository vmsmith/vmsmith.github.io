---
title: "Architecting Moneypenny"
date: 2025-12-12T08:05:53+01:00
draft: false
category: "meta-system"
tags: ["architecture"]
summary: "Moving on to the actual creation of Moneypenny"
---

I have reached a point with the Hugo website where "better is the enemy of good enough," and it's time to move on to the actual creation of Moneypenny. I will continue to tweak Hugo as necessary when the need for new functionality arises.

So today I developed a first iteration of a high-level view of the system architecture. It identifies the major components:

* Presentation Layer
* Orchestration Layer
* Cognition subsystem
* LLM
* Runtime environment, consisting of a persistence component and an external services component.

It also shows the interfaces between those commponents: APIs, MCPs, webhooks, function calls, etc.

A diagram and description are in the Architecture section of Hugo.  

