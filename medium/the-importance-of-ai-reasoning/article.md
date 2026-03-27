# The importance of AI reasoning

- **Author:** Tula Masterman
- **Original publication:** Medium
- **Original link:** https://medium.com/neudesic-innovation/the-importance-of-ai-reasoning
- **Published:** 2024-02-28
- **Imported to repo:** 2026-03-27

- **Subtitle:** Creating more effective AI systems through prompting, training/fine-tuning, and agent frameworks.

## Summary

Explains why reasoning is critical for AI systems that need to plan, adapt, and execute meaningful actions on behalf of users.

## Article

Creating more effective AI systems through prompting, training/fine-tuning, and agent frameworks.

Let’s take the question, “what occupation do the grandchildren of the Beatles hold?”. Although a seemingly simple question, there are lots of components we’d need to determine to answer correctly. For example:

- Who are all the members of the Beatles?

- For each member of the Beatles, who are their children (if any)?

- For each of the Beatles kids, do they have kids?

- Finally, for each of the grandkids identified, what do they do for work?

This is just one of many different search paths we could take to answer the question! So, how do models answer this today?

When asking ChatGPT (GPT-4) we get this response:

Image created by author 2/27/24

When asking Microsoft Copilot with Web enabled, we get this response:

Image created by author 2/27/24

Although both responses provide an answer to the question and conducted a search for information, neither returns the correct answer. The ChatGPT response focuses only on the Beatles’ children, while the Copilot response only touches on some of the grandchildren. This suggests the models did not perform comprehensive searches nor keep refining their plan until coming to the proper conclusion. Although this isn’t necessarily detrimental for this particular question, it can become a bigger challenge when, as a user, we need the model or Artificial Intelligence (AI) system to conduct exhaustive searches on our behalf.

To bridge this gap, the model would need a way to continuously revise its response and conduct new searches until it provides a conclusive answer or determines no information can be found to satisfy the question. This iterative process of evaluating and refining outputs is both a technical challenge and, if done correctly, a step towards more sophisticated and reliable AI systems. Improving a model’s ability to reason and execute goals effectively is, therefore, a huge area of research today.

What is AI reasoning?

In today’s day of increasingly sophisticated AI based systems, the ability for models to reason independently has become a critical component of their functionality. Today, Foundation Models (FMs) and Large Language Models (LLMs) are expected to not only return the correct outcome, but also come up with the right logic to get to that outcome. This reasoning journey is not linear or predefined, the model may need to adjust its plan based on new information it discovers and there might be many different routes a model can follow to get to the right solution.

Why do we need AI reasoning?

Improvements in model reasoning allow AI systems to take effective action on behalf of users and help push our interactions with tools like ChatGPT from a purely chat based experience to one where we have an AI partner working with us and helping us to achieve our goals. This can be simple tasks like conducting research or sending emails to more complex tasks like booking a vacation, or even preparing an environmental impact report for a new construction project.

To succeed in the report generation example, the AI system would need to not only pull information from a variety of sources such as scientific studies, regulatory documents, and internal data, but also synthesize all this context into a comprehensive, verifiable report. You can imagine creating such a report would require many steps and revisions, and there’s a variety of paths the system could take to get to an accurate, useful report.

So, how do we get to improved AI reasoning and ultimately better outputs?

Today there are three key approaches to improving reasoning and getting better outputs from AI: prompting, training or fine-tuning a model, and creatingAI agents or agent teams.

- Prompting: At inference time, instead of just sending the model a task or question, give the model clear instructions on how to break down a problem. For example, usingChain-of-Thought (CoT) prompting, even adding simple directions like “Let’s think step by step” before the task results in a significantly better output. Quality prompt engineering helps models likeGPT-4,Gemini,Llama-2, and more to take a question, decompose it into clear steps, and provide an answer either using their own knowledge or by leveraging tools they have access to.(Note: Model tools allow the model to access information beyond its training data e.g. an internet search tool, Expedia tool, X tool to post tweets, etc.).

- Training & Fine-Tuning: Companies like OpenAI and Google are consistently training and releasing LLMs like ChatGPT and PaLM 2 with improved reasoning capabilities. This reasoning improvement (as evaluated on many benchmarks) is attributed to both the datasets used and training methodology. There’s also many open-source LLMs and Small Language Models (SLMs) being trained by companies likeMistraland Meta. Meanwhile companies likeMicrosoft are fine-tuning models like Orca2with new techniques like prompt erasure to help create SLMs that can reason just as well as LLMs. Most models can be found onHuggingFacefrom both large tech companies and individual data scientists around the world working to train and improve models across many domains. By training and fine-tuning models, we can create a better base reasoner which can later be prompted and used in an agent framework to execute tasks.(Note: Training a model from scratch involves curating a dataset, developing a model architecture, and often spending lots of money on compute power. In comparison, fine-tuning allows us to take larger models and adapt them for specific purposes. The rise of SLMs has shown that models trained on less data with excellent quality can produce results nearly as compelling as their LLM counterparts).

- AI Agents/Agent Teams: AI agents are backed by models either large or small, and given a persona along with tools they can use to work on a task either independently or in a team of other agents. For example, we can create a team of research agents who collaborate on writing papers. One agent is responsible for assigning research tasks, one reads reports from Google Scholar, one reads reports from ArXiv, and one writes the final report based on all the information found.(Note: There are both single and multi-agent frameworks you can leverage. For example, theOpenAI Assistants APIleverages one Agent, while frameworks likeAutoGenorCrewAIinvoke multiple agents on a team).

Conclusion

Each of these strategies play an important role in improving AI reasoning. Prompting is the easiest place to get started and allows you to explore different mechanisms of directing the model without altering the underlying model architecture. Training and fine-tuning have a higher barrier to entry than prompting but can be incredibly effective ways to improve a model’s inherent capabilities. AI Agent frameworks allow a blended approach where you can use prompting, fine-tuned models, or multiple different models, all working together as a team to execute a task. In my opinion, the dynamic nature of AI Agent frameworks is the most promising path to dealing with complicated user goals. By dividing up tasks and working on them iteratively, agents can use their collective capability to solve highly complex problems not achievable through prompting or training alone.

Stay tuned for additional posts in this series where we’ll dive into prompting, fine-tuning/training, and AI Agent frameworks for improving AI reasoning in more detail!

Interested in discussing further or collaborating? Reach out onLinkedIn!

The importance of AI reasoningwas originally published inNeudesic Innovationon Medium, where people are continuing the conversation by highlighting and responding to this story.