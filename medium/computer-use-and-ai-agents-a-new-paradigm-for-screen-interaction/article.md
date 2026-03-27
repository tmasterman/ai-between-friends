---
title: "Computer Use and AI Agents: A New Paradigm for Screen Interaction"
subtitle: "Exploring the future of multimodal AI Agents and the Impact of Screen Interaction"
authors:
  - name: "Tula Masterman"
    publication: "Tula Masterman"
    links:
      substack: "https://substack.com/@tulamasterman"
      linkedin: "https://www.linkedin.com/in/tula-masterman/"
      website: "https://tulamasterman.com/"
published: 2024-10-30
original_url: "https://medium.com/data-science/computer-use-and-ai-agents-a-new-paradigm-for-screen-interaction-b2dcbea0df5b"
license: "CC BY-NC 4.0"
---
## Summary

Explores multimodal AI agents, computer-use interfaces, and how screen interaction changes what effective agents require.

## Article

Exploring the future of multimodal AI Agents and the Impact of Screen Interaction

Image created by author using GPT4o

## Introduction: The ever-evolving AI Agent Landscape

Recent announcements from Anthropic, Microsoft, and Apple are changing the way we think about AI Agents. Today, the term “AI Agent” is oversaturated — nearly every AI-related announcement refers to agents, but their sophistication and utility vary greatly.

At one end of the spectrum, we have advanced agents that leverage multiple loops for planning, tool execution, and goal evaluation, iterating until they complete a task. These agents might even create and use memories, learning from their past mistakes to drive future successes. Determining what makes an effective agent is a very active area of AI research. It involves understanding what attributes make a successful agent (e.g., how should the agent plan, how should it use memory, how many tools should it use, how should it keep track of it’s task) and the best approach to configure a team of agents.

On the other end of the spectrum, we find AI agents that execute single purpose tasks that require little if any reasoning. These agents are often more workflow focused. For example, an agent that consistently summarizes a document and stores the result. These agents are typically easier to implement because the use cases are narrowly defined, requiring less planning or coordination across multiple tools and fewer complex decisions.

With the latest announcements from Anthropic, Microsoft, and Apple, we’rewitnessing a shift from text-based AI agents to multimodal agents. This opens up the potential to give an agent written or verbal instructions and allow it to seamlessly navigate your phone or computer to complete tasks.This has great potential to improve accessibility across devices, but also comes with significant risks.Anthropic’s computer use announcement highlights the risks of giving AI unfettered access to your screen, and provides risk mitigation tactics like running Claude in a dedicated virtual machine or container, limiting internet access to an allowlist of permitted domains, including human in the loop checks, and avoiding giving the model access to sensitive data. They note that no content submitted to the API will be used for training.

Key Announcements from Anthropic, Microsoft, and Apple:

Anthropic’s Claude 3.5 Sonnet: Giving AI the Power to Use Computers

- Overview: The goal of Computer Use is to give AI the ability to interact with a computer the same way a human would. Ideally Claude would be able to open and edit documents, click to various areas of the page, scroll and read pages, run and execute command line code, and more. Today, Claude can follow instructions from a human to move a cursor around the computer screen, click on relevant areas of the screen, and type into a virtual keyboard. Claude Scored 14.9% on theOSWorldbenchmark, which is higher than other AI models on the same benchmark, but still significantly behind humans (humans typically score 70–75%).

- How it works: Claude looks at user submitted screenshots and counts pixels to determine where it needs to move the cursor to complete the task. Researchers note that Claude was not given internet access during training for safety reasons, but that Claude was able to generalize from training tasks like using a calculator and text-editor to more complex tasks. It even retried tasks when it failed. Computer use includes three Anthropic defined tools: computer, text editor, and bash. The computer tool is used for screen navigation, text editor is used for viewing, creating, and editing text files, and bash is used to run bash shell commands.

- Challenges: Despite it’s promising performance, there’s still a long way to go for Claude’s computer use abilities. Today it struggles with scrolling, overall reliability, and is vulnerable to prompt injections.

- How to Use: Public beta available through the Anthropic API. Computer use can be combined with regular tool use.

Microsoft’s OmniParser & GPT-4V: Making Screens Understandable and Actionable for AI

- Overview: OmniParser is designed to parse screenshots of user interfaces and transform them into structured outputs. These outputs can be passed to a model like GPT-4V to generate actions based on the detected screen elements. OmniParser + GPT-4V were scored on a variety of benchmarks includingWindows Agent Arenawhich adapts the OSWorld benchmark to create Windows specific tasks. These tasks are designed to evaluate an agents ability to plan, understand the screen, and use tools, OmniParser & GPT-4V scored ~20%.

- How it Works: OmniParser combines multiple fine-tuned models to understand screens. It uses a finetuned interactable icon/region detection model (YOLOv8), a finetuned icon description model (BLIP-2orFlorence2), and an OCR module. These models are used to detect icons and text and generate descriptions before sending this output to GPT-4V which decides how to use the output to interact with the screen.

- Challenges: Today, when OmniParser detects repeated icons or text and passes them to GPT-4V, GPT-4V usually fails to click on the correct icon. Additionally, OmniParser is subject to OCR output so if the bounding box is off, the whole system might fail to click on the appropriate area for clickable links. There are also challenges with understanding certain icons since sometimes the same icon is used to describe different concepts (e.g., three dots for loading versus for a menu item).

- How to Use: OmniParser is available onGitHub&HuggingFaceyou will need to install the requirements and load the model from HuggingFace, next you can try running the demo notebooks to see how OmniParser breaks down images.

Apple’s Ferret-UI: Bringing Multimodal Intelligence to Mobile UIs

- Overview: Apple’s Ferret (Refer and Ground Anything Anywhere at Any Granularity) has been around since 2023, but recently Apple released Ferret-UI a MLLM (Multimodal Large Language Model) which can execute “referring, grounding, and reasoning tasks” on mobile UI screens. Referring tasks include actions like widget classification and icon recognition. Grounding tasks include tasks like find icon or find text. Ferret-UI can understand UIs and follow instructions to interact with the UI.

- How it Works: Ferret-UI is based on Ferret and adapted to work on finer grained images by training with “any resolution” so it can better understand mobile UIs. Each image is split into two sub-images which have their own features generated. The LLM uses the full image, both sub-images, regional features, and text embeddings to generate a response.

- Challenges: Some of the results cited in the Ferret-UI paper demonstrate instances where Ferret predicts nearby text instead of the target text, predicts valid words when presented with a screen that has misspelled words, it also sometimes misclassifies UI attributes.

- How to Use: Apple made the data and code available onGitHubfor research use only. Apple released two Ferret-UI checkpoints, one built on Gemma-2b and one built on Llama-3–8B. The Ferret-UI models are subject to the licenses for Gemma and Llama while the dataset allows non-commercial use.

Summary: Three Approaches to AI Driven Screen Navigation

In summary, each of these systems demonstrate a different approach to building multimodal agents that can interact with computers or mobile devices on our behalf.

Anthropic’s Claude 3.5 Sonnet focuses on general computer interaction where Claude counts pixels to appropriately navigate the screen. Microsoft’s OmniParser addresses specific challenges for breaking down user interfaces into structured outputs which are then sent to models like GPT-4V to determine actions. Apple’s Ferret-UI is tailored to mobile UI comprehension allowing it to identify icons, text, and widgets while also executing open-ended instructions related to the UI.

Across each system, theworkflow typically follows two key phases one for parsing the visual information and one for reasoning about how to interact with it. Parsing screens accurately is critical for properly planning how to interact with the screen and making sure the system reliably executes tasks.

## Conclusion: Building Smarter, Safer AI Agents

In my opinion, the most exciting aspect of these developments is howmultimodal capabilities and reasoning frameworks are starting to converge. While these tools offerpromising capabilities, they still lag significantly behind human performance. There are also significant AI safety concernswhich need to be addressed when implementing any agentic system with screen access.

One of the biggest benefits of agentic systems is their potential to overcome the cognitive limitations of individual models by breaking down tasks into specialized components.These systems can be built in many ways. In some cases, what appears to the user asa single agentmay, behind the scenes, consist ofa team of sub-agents— eachmanaging distinct responsibilitieslike planning, screen interaction, or memory management. For example, a reasoning agent might coordinate with another agent that specializes in parsing screen data, while a separate agent curates memories to enhance future performance.

Alternatively, these capabilities might becombined within one robust agent. In this setup, the agent could have multiple internal planning modules— one focused on planning the screen interactions and another focused on managing the overall task. The best approach to structuring agents remains to be seen, but the goal remains the same: to create agents that perform reliably overtime, across multiple modalities, and adapt seamlessly to the user’s needs.

References:

- Developing Computer Use(Anthropic)

- Introducing computer use, a new Claude 3.5 Sonnet, and Claude 3.5 Haiku(Anthropic)

- Computer Use Documentation(Anthropic)

- OSWorld GitHub

- Windows Agent Arena

- OmniParser for pure vision-based GUI agent

- OmniParser GitHub

- OmniParser HuggingFace

- OmniParser ArXiv

- Ferret GitHub

- Ferret-UI: Grounded Mobile UI Understanding with Multimodal LLMs

Interested in discussing further or collaborating? Reach out on LinkedIn!

Computer Use and AI Agents: A New Paradigm for Screen Interactionwas originally published inTDS Archiveon Medium, where people are continuing the conversation by highlighting and responding to this story.
