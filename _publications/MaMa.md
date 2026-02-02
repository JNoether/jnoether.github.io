---
title: "MaMa: A Game-Theoretic Approach for Designing Safe Agentic Systems"
collection: publications
permalink: /publication/MaMa
excerpt: 'Automatic Design of Safe Agentic Systems using a two-player game between a system designer and an attacker'
date: 29-01-2026
venue: 'Preprint, under Review'
# paperurl: 'http://academicpages.github.io/files/paper1.pdf'
# citation: 'Your Name, You. (2009). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'
---

# MaMa: A Game-Theoretic Approach for Designing Safe Agentic Systems

## Designing Safer AI Systems with Adversarial Thinking

Modern AI systems are no longer just single models answering questions.  
More and more, they are **agentic systems**: groups of AI agents that talk to each other, use tools, and take actions on behalf of users.

These systems are powerful—but they can also be dangerous.

What happens if an agent makes a mistake?  
What if an agent is manipulated or behaves maliciously?

This post explains a new approach, called **MaMa**, that is designed to make agentic systems *safe by construction*, even when some agents fail or turn adversarial.

---

<!-- ## Why Agentic Systems Are Risky

Agentic systems divide work across multiple specialized agents.  
For example, one agent might plan tasks, another might browse the web, and another might send emails or run code.

This setup has clear benefits:
- Better performance on complex tasks  
- More modular and reusable designs  
- Increased autonomy  

But it also introduces new risks:
- A single agent can take harmful actions using tools  
- Agents can misunderstand or miscoordinate  
- An attacker could compromise one agent and influence the whole system  

Traditional safety measures focus on individual models.  
They are often **not enough** for multi-agent systems.

--- -->

## A Stronger Threat Model

Instead of assuming weak attacks or rare failures, this work considers a **worst-case scenario**:

> An attacker can directly take control of a small number of agents and instruct them to behave maliciously.

This is a strong assumption—but it is intentional.

If a system is safe under this threat model, it is likely to be safe under:
- Accidental failures  
- Hallucinations  
- Weaker, real-world attacks  

---

## The Core Idea: A Game Between Designer and Attacker

The key insight is to frame system design as a **game** between two players:

- **The Meta-Agent**  
  Designs the agentic system and wants it to be both useful and safe.

- **The Meta-Adversary**  
  Tries to break the system by corrupting a subset of agents.

This interaction is modeled as a **Stackelberg security game**, where:
1. The Meta-Agent commits to a system design  
2. The Meta-Adversary responds with the strongest attack it can find  

The system is improved by repeating this process many times.

---

## How MaMa Works

MaMa stands for **Meta-Agent – Meta-Adversary**.  
It is an automated, iterative design method.
 
At a high level, it works like this:

1. The Meta-Agent proposes a system design  
2. The system is evaluated in normal (clean) conditions  
3. The Meta-Adversary searches for the most damaging attacks  
4. The system is evaluated again under attack  
5. The Meta-Agent updates the design to defend against those attacks  

This loop continues, gradually producing safer systems.

---

## System Overview

The interaction between the Meta-Agent and the Meta-Adversary is shown below.

<iframe
  src="{{'/assets/images/MaMa/Illustration_Full.png' | relative_url }}"
  width="100%"
  height="300px"
  style="border: none;">
</iframe>

*Figure 1: The Meta-Agent improves system designs based on the strongest attacks found by the Meta-Adversary.*
 
---

## What Does the Meta-Adversary Actually Do?

The Meta-Adversary:
- Chooses a small number of agents to corrupt  
- Overwrites their instructions  
- Tries to cause harmful outcomes (for example, unsafe tool use)

Each attack is:
- Executed in the full system  
- Scored using a safety metric  
- Stored in an archive for future reference  

Over time, the Meta-Adversary learns which attacks are most effective.

---

## How the Meta-Agent Defends the System

The Meta-Agent uses feedback from attacks to improve the design.

Common defense strategies include:
- Adding **safety-focused agents** that review actions  
- Requiring **multiple agents to agree** before an action is taken  
- Separating planning, execution, and approval roles  
- Monitoring agents for suspicious behavior  

Importantly, these defenses are **discovered automatically**, not hand-designed.

---

## Experimental Results

MaMa was tested across several environments, including:
- Travel planning  
- Personal assistance  
- Financial writing  
- Code generation  

The results show:
- **Large improvements in safety** under attack  
- **Minimal or no loss in quality** during normal operation  
- In some cases, even **better performance** than systems optimized only for quality  

![Figure 2: Safety and quality over training iterations](/assets/images/MaMa/Results.png)

*Figure 2: Systems designed with MaMa become much safer over time while maintaining high quality.*

---

## Robustness Beyond Training

Systems designed with MaMa remain robust when:
- Using different language models  
- Facing stronger attackers  
- Attacks target specific agents  
- Attacks are injected indirectly through tools  

This suggests that MaMa produces **general safety improvements**, not just defenses against specific attacks.

---