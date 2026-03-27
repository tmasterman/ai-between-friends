---
title: "Improving Agent Systems & AI Reasoning"
subtitle: "DeepSeek-R1, OpenAI o1 & o3, Test-Time Compute Scaling, Model Post-Training and the Transition to Reasoning Language Models (RLMs)"
authors:
  - name: "Tula Masterman"
    publication: "Tula Masterman"
    links:
      substack: "https://substack.com/@tulamasterman"
      linkedin: "https://www.linkedin.com/in/tula-masterman/"
      website: "https://tulamasterman.com/"
published: 2025-02-02
original_url: "https://medium.com/data-science/improving-agent-systems-ai-reasoning-c2d91ecfdf77"
license: "CC BY-NC 4.0"
---

## Article

DeepSeek-R1, OpenAI o1 & o3, Test-Time Compute Scaling, Model Post-Training and the Transition to Reasoning Language Models (RLMs)

Image by author and GPT-4o meant to represent DeepSeek and other competitive GenAI model providers

## Introduction

Over the past year generative AI adoption and AI agent development have skyrocketed. Reports from LangChainshow that 51% of respondents are using AI Agents in production, while reports from Deloittepredict that in 2025 at least 25% of companies using Generative AI will launch AI agent pilots or proof of concepts.Despite the popularity and growth of AI Agent frameworks, anyone building these systems quickly runs into limitations of working with large language models (LLMs), with model reasoning ability often at the top of the list. To overcome reasoning limitations researchers and developers have explored a variety of different techniques ranging from different prompting methods like ReAct or Chain of Thought (CoT) to building multi-agent systems with separate agents dedicated to planning and evaluation, and now companies are releasing new models trained specifically to improve the model’s built-in reasoning process.

DeepSeek’s R1 and OpenAI’s o1 and o3 announcements are shaking up the industry by providing more robust reasoning capabilities compared to traditional LLMs. These models are trained to “think” before answering and have a self-contained reasoning process allowing them to break down tasks into simpler steps, work iteratively on the steps, recognize and correct mistakes before returning a final answer. This differs from earlier models like GPT-4o which required users to build their own reasoning logic by prompting the model to think step-by-step and creating loops for the model to iteratively plan, work, and evaluate its progress on a task. One of the key differences in training Reasoning Language Models (RLMs) like o1, o3, and R1 lies in the focus on post-training and test-time compute scaling.

In this article we’ll cover the key differences between train and test time compute scaling, post-training and how to train a RLM like DeepSeek’s R1, and the impact of RLMs on AI agent development.

## Train-Time Compute vs Test-Time Compute

#

## #

## Overview

Compute-scaling relates to providing more resources, such as processing power and memory, for training and running AI models. In a nutshell, train-time compute scalingapplies to both pre-training where a model learns general patterns and post-training where a base-model undergoes additional training like Reinforcement Learning (RL) or Supervised Fine-Tuning (SFT) to learn additional more specific behaviors. In contrast,test-time compute scaling applies at inference time, when making a prediction, and provides more computational power for the model to “think” by exploring multiple potential solutions before generating a final answer.

It’s important to understand that both test-time compute scaling and post-training can be used to help a model “think” before producing a final response but that these approaches are implemented in different ways.

While post-training involves updating or creating a new model, test-time compute scaling enables the exploration of multiple solutions at inference without changing the model itself. These approaches could be used together; in theory you could take a model that has undergone post-training for improved reasoning, like DeepSeek-R1, and allow it to further enhance it’s reasoning by performing additional searches at inference through test-time compute scaling.

Image by author. Depicts a very simple representation of pre-training and post-training. Note that there can be significant variations in post-training, but essentially the base model is modified in some way to create an updated model better suited to the task.

## Train-Time Compute: Pre-Training & Post-Training

Today, most LLMs & Foundation Models are pre-trained on a large amount of data from sources like the Common Crawl, which have a wide and varied representation of human-written text. This pre-training phase teaches the model to predict the next most likely word or token in a given context. Once pre-training is complete, most models undergo a form of Supervised Fine Tuning (SFT) to optimize them for instruction following or chat based use cases. For more information on these training processescheck out one of my previous articles.

Overall, this training process is incredibly resource intensive and requires many training runs each costing millions of dollars before producing a model like Claude 3.5 Sonnet, GPT-4o, Llama 3.1–405B, etc. These models excel on general purpose tasks as measured on a variety of benchmarks across topics for logical reasoning, math, coding, reading comprehension and more.

However, despite their compelling performance on a myriad of problem types, getting a typical LLM to actually “think” before responding requires a lot of engineering from the user. Fundamentally, these models receive an input and then return an output as their final answer. You can think of this like the model generating it’s best guess in one step based on either learned information from pre-training or through in context learning from directions and information provided in a user’s prompt. This behavior is why Agent frameworks, Chain-of-Thought (CoT) prompting, and tool-calling have all taken off. These patterns allow people to build systems around LLMs which enable a more iterative, structured, and successful workflow for LLM application development.

Recently, models like DeepSeek-R1 have diverged from the typical pre-training and post-training patterns that optimize models for chat or instruction following. Instead DeepSeek-R1 used a multi-stage post-training pipeline to teach the model more specific behaviors like how to produce Chain-of-Thought sequences which in turn improve the model’s overall ability to “think” and reason. We’ll cover this in detail in the next section using the DeepSeek-R1 training process as an example.

## Test-Time Compute Scaling: Enabling “Thinking” at Inference

What’s exciting about test-time compute scaling and post-training is that reasoning and iterative problem solving can be built into the models themselves or their inference pipelines. Instead of relying on the developer to guide the entire reasoning and iteration process, there’s opportunities to allow the model to explore multiple solution paths, reflect on it’s progress, rank the best solution paths, and generally refine the overall reasoning lifecycle before sending a response to the user.

Test-time compute scaling is specifically related tooptimizing performance at inference and does not involve modifying the model’s parameters. What this means practically is that a smaller model like Llama 3.2–8b can compete with much larger models by spending more time “thinking” and working through numerous possible solutions at inference time.

Some of the common test-time scaling strategies includeself-refinementwhere the model iteratively refines it’s own outputs andsearching against a verifierwhere multiple possible answers are generated and a verifier selects the best path to move forward from. Common search against verifier strategies include:

- Best-of-Nwhere numerous responses are generated for each question, each answer is scored, and the answer with the highest score wins.

- Beam Searchwhich typically use a Process Reward Model (PRM) to score a multi-step reasoning process. This allows you to start by generating multiple solution paths (beams), determine which paths are the best to continue searching on, then generate a new set of sub-paths and evaluate these, continuing until a solution is reached.

- Diverse Verifier Tree Search (DVTS)is related to Beam Search but creates a separate tree for each of the initial paths (beams) created. Each tree is then expanded and the branches of the tree are scored using PRM.

Image by author inspired by HuggingFace blog on Test Time Compute Scaling

Determining which search strategy is best is still an active area of research, but there are a lot ofgreat resources on HuggingFacewhich provide examples for how these search strategies can be implemented for your use case.

## Training a Reasoning Language Model (RLM)

OpenAI’s o1 model announced in September 2024 was one of the first models designed to “think” before responding to users. Although it takes longer to get a response from o1 compared to models like GPT-4o, o1's responses are typically better for more advanced tasks since it generates chain of thought sequences that help it break down and solve problems.

Working with o1 and o3 requires a different style of prompt engineering compared to earlier generations of models given that these new reasoning focused models operate quite differently than their predecessors. For example, telling o1 or o3 to “think step by step” will be less valuable than giving the same instructions to GPT-4o.

Given the closed-source nature of OpenAI’s o1 and o3 models it’s impossible to know exactly how the models were developed; this is a big reason why DeepSeek-R1 attracted so much attention.DeepSeek-R1 is the first open-source model to demonstrate comparable behavior and performance to OpenAI’s o1.This is amazing for the open-source community because it means developers can modify R1 to their needs and, compute power permitting, can replicate R1’s training methodology.

#

## DeepSeek-R1 Training Process

- DeepSeek-R1-Zero: First, DeepSeek performed Reinforcement Learning (RL) (post-training) on their base model DeepSeek-V3. This resulted inDeepSeek-R1-Zero, a model that learned how to reason, create chain-of-thought-sequences, and demonstrates capabilities like self-verification and reflection. The fact that a model could learn all these behaviors from RL alone is significant for the AI industry as a whole. However, despite DeepSeek-R1-Zero’s impressive ability to learn,themodel had significant issues like language mixing and generally poor readability. This led the team to explore other paths to stabilize model performance and create a more production-ready model.

- DeepSeek-R1: Creating DeepSeek-R1 involved amulti-stage post training pipeline alternating between SFT and RL steps. Researchers first performed SFT on DeepSeek-V3 using cold start data in the form of thousands of example CoT sequences, the goal of this was to create a more stable starting point for RL and overcome the issues found with DeepSeek-R1-Zero. Second, researchers performed RL and included rewards to promote language consistency and enhance reasoning on tasks like science, coding, and math. Third, SFT is completed again, this time including non-reasoning focused training examples to help the model retain more general-purpose abilities like writing and role-playing. Finally, RL occurs again to help improve with alignment towards human preferences. This resulted in a highly capable model with 671B parameters.

- Distilled DeepSeek-R1 Models: The DeepSeek team further demonstrated that DeepSeek-R1’s reasoning can be distilled into open-source smaller models using SFT alone without RL. They fine-tuned smaller models ranging from 1.5B-70B parameters based on both Qwen and Llama architectures resulting in a set of lighter, more efficient models with better reasoning abilities. This significantly improves accessibility for developers since many of these distilled models can run quickly on their device.

## 

## 

## Conclusion: The Impact of Improved Reasoning Models on AI Agents

As reasoning-first models and test-time compute scaling techniques continue to advance, the system design, capabilities, and user-experience for interacting with AI agents will change significantly.

Going forward I believe we will see morestreamlined agent teams. Instead of having separate agents and hyper use-case specific prompts and tools we will likely see design patterns where a single RLM manages the entire workflow. This will also likely change how much background information the user needs to provide the agent if the agent is better equipped to explore a variety of different solution paths.

User interaction with agents will also change. Today many agent interfaces are still chat-focused with users expecting near-instant responses. Given that it takes RLMs longer to respond I thinkuser-expectations and experiences will shift and we’ll see more instances where users delegate tasks that agent teams execute in the background. This execution time could take minutes or hours depending on the complexity of the task but ideally will result in thorough and highly traceable outputs.This could enable people to delegate many tasks to a variety of agent teams at once and spend their timefocusing on human-centric tasks.

Despite their promising performance,many reasoning focused models still lack tool-calling capabilities.OpenAI’snewly released o3-miniis the first reasoning focused model that natively supports tool-calling, structured outputs, and developer prompts (the new version of system prompts). Tool-calling is critical for agents since it allows them to interact with the world, gather information, and actually execute tasks on our behalf. However, given the rapid pace of innovation in this space I expect we will soon see more RLMs with integrated tool calling.

In summary, this is just the beginning of a new age of general-purpose reasoning models that will continue to transform the way that we work and live.

Note: The opinions expressed in this article are solely my own and do not necessarily reflect the views or policies of my employer.

Interested in discussing further or collaborating? Reach out on LinkedIn!

## References

- HuggingFace Blog on Scaling Test Time Compute

- Scaling LLM Test-Time Compute Optimally can be More Effective than Scaling Model Parameters

- Solving math word problems with process and outcome-based feedback Process Reward Models (PRM)

- Reasoning Language Models: A Blueprint

- OpenAI o1 System Card

- DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning

- Will we run out of data? Limits of LLM scaling based on human-generated data

- Nvidia CEO says his AI chips are improving faster than Moore’s Law

- Scaling Test Time Compute for Longer Thinking in LLMs

- OpenAI o3-mini

Improving Agent Systems & AI Reasoningwas originally published inTDS Archiveon Medium, where people are continuing the conversation by highlighting and responding to this story.
