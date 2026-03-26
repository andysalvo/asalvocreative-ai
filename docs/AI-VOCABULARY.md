# 35 Words You Need to Know to Talk About AI in 2026

These are the words we had to learn to build this company. We are not an AI textbook. We are a team that uses AI every day to run our operations, and this is the vocabulary that actually comes up.

If you are new to AI, start with the first ten. If you are already using AI tools, skip to the deeper terms. If you want to know where this is all going, read the bonus concepts at the end.

**Amendment policy:** This document works in amendments. Entries can be improved or expanded but canonical truth is preserved.

---

## Must-Know: 10 terms everyone should start with

**1. Artificial Intelligence (AI)**
What it is: Software that can perform tasks that normally require human thinking -- reading text, recognizing images, making decisions, generating content.
Why it matters: AI is no longer a research topic. It is embedded in the tools you already use and the ones being built right now.

**2. Chatbot**
What it is: An AI you interact with by typing messages back and forth -- like texting with a very knowledgeable assistant.
Why it matters: ChatGPT, Claude, and Gemini are chatbots. For most people, a chatbot is their first real interaction with AI.

**3. Prompt**
What it is: The instruction or question you type into an AI tool to tell it what you want.
Why it matters: The quality of what AI gives you depends almost entirely on how you ask. Learning to prompt well is the single most useful AI skill.

**4. Algorithm**
What it is: A set of rules or steps that a computer follows to solve a problem or make a decision.
Why it matters: When people say "the algorithm" -- on social media, in search, in recommendations -- they mean the set of rules deciding what you see. AI has made these algorithms vastly more powerful.

**5. Machine Learning (ML)**
What it is: A type of AI where the software learns patterns from data instead of being told explicit rules -- it improves by studying examples.
Why it matters: Machine learning is how AI gets good at things. Every recommendation, translation, and voice assistant you use was trained this way.

**6. Neural Network**
What it is: The architecture inside modern AI that is loosely inspired by how the human brain processes information -- layers of connected nodes that pass signals to each other.
Why it matters: You do not need to understand the math, but knowing that AI "thinks" through layers of pattern recognition helps you understand both its power and its limits.

**7. Training**
What it is: The process of feeding massive amounts of data to an AI model so it learns patterns, language, and reasoning before anyone ever uses it.
Why it matters: Training is why AI models cost hundreds of millions of dollars to create. It is the upfront investment that makes everything else possible.

**8. API (Application Programming Interface)**
What it is: A way for two pieces of software to talk to each other -- like a waiter taking your order to the kitchen and bringing the food back.
Why it matters: APIs are how AI gets built into products. When an app uses AI behind the scenes, it is almost always calling an AI model through an API.

**9. Cloud**
What it is: Computers and storage that live in a data center somewhere else, accessed over the internet instead of running on your own machine.
Why it matters: AI runs in the cloud. The models are too large to run on a laptop, so when you use ChatGPT or Claude, you are sending your prompt to a data center and getting the answer back.

**10. Automation**
What it is: Using software to perform a task without a human doing it manually every time.
Why it matters: AI has made automation dramatically more capable. Tasks that used to require custom code can now be automated with plain English instructions.

---

## Deeper: 20 terms for people building with AI

**11. LLM (Large Language Model)**
What it is: A type of AI trained on massive amounts of text that can understand and generate human language -- the engine behind ChatGPT, Claude, and Gemini.
Why it matters: Nearly every AI product in 2026 is built on top of an LLM. Understanding what it is and what it is not is the starting point for building anything.

**12. Token**
What it is: The small chunks of text -- roughly a word or part of a word -- that an AI model reads and generates. It is the unit of measurement for how AI processes language.
Why it matters: Pricing, speed, and capability limits are all measured in tokens. Understanding them helps you estimate costs and compare products.

**13. Context Window**
What it is: The total amount of information an AI model can see and work with at one time -- think of it as the model's short-term memory.
Why it matters: A bigger context window means the AI can handle longer documents and more complex tasks. Companies compete fiercely on this number.

**14. Inference**
What it is: The process of running a trained AI model to get an answer -- as opposed to training, which is how the model learned in the first place.
Why it matters: Inference is where the ongoing cost lives. Every time you use an AI tool, someone is paying for inference.

**15. Hallucination**
What it is: When an AI confidently generates information that is factually wrong or completely made up.
Why it matters: This is the single biggest trust problem in AI. If you are using AI for anything consequential, you need to know this risk exists and how to check for it.

**16. RAG (Retrieval-Augmented Generation)**
What it is: A technique where the AI searches a knowledge base for relevant information first, then uses what it found to generate a more accurate answer -- like giving the AI a reference library before it writes.
Why it matters: RAG is how companies make AI useful with their own private data without retraining the whole model.

**17. MCP (Model Context Protocol)**
What it is: An open standard that gives AI models a universal way to connect to external tools, databases, and services -- like a universal plug for AI to interact with the outside world.
Why it matters: MCP is becoming the standard interface layer for AI integrations, with hundreds of publicly available servers in 2026.

**18. Claude Code**
What it is: Anthropic's command-line tool that lets the Claude AI model write, edit, and manage code directly in your development environment as an autonomous coding agent.
Why it matters: It represents the shift from "AI as chatbot" to "AI as coworker" -- an agent that operates inside your actual workflow.

**19. LangChain**
What it is: An open-source framework that gives developers pre-built components for building applications powered by language models.
Why it matters: When someone says they are "building with LangChain," they mean they are assembling AI-powered applications from modular, reusable parts.

**20. Frontier Model**
What it is: The most capable, state-of-the-art AI models at any given time -- currently Claude Opus, GPT-5, and Gemini Ultra.
Why it matters: "Frontier" is the term investors and builders use to distinguish cutting-edge AI from commodity AI.

**21. Open Weights**
What it is: AI models whose internal parameters are publicly released so anyone can download, run, modify, or build on them -- models like DeepSeek and Llama.
Why it matters: The gap between open-weight models and proprietary frontier models is narrowing fast, reshaping the economics of the entire AI industry.

**22. Vibe Coding**
What it is: A development practice where you describe what you want in plain English and let AI generate the code, without necessarily understanding every line. Coined by Andrej Karpathy. Collins Dictionary Word of the Year 2025.
Why it matters: This is how non-engineers are building functional software in 2026. It is both an enormous opportunity and a real risk.

**23. Context Engineering**
What it is: The practice of carefully designing what information, instructions, and data you feed into an AI model before it responds -- the successor to "prompt engineering."
Why it matters: The quality of AI output depends more on the quality of the context you provide than on the cleverness of your prompt.

**24. CLAUDE.md**
What it is: A markdown file placed in a project that Claude automatically reads at the start of every session, giving it persistent instructions and project context without repeating yourself.
Why it matters: It represents a broader pattern -- the best AI practitioners build structured, reusable instruction files that make AI behave consistently across sessions.

**25. Ralph Wiggum Technique**
What it is: An AI coding method where you put an agent in an automated loop -- it attempts a task, saves its work, exits, and restarts with fresh context, grinding through problems with persistence instead of brilliance. Named after the Simpsons character.
Why it matters: It removes the human bottleneck of constantly re-prompting, letting agents work through complex tasks autonomously -- including overnight.

**26. Agentic Workflow**
What it is: An AI system that does not just answer questions but autonomously plans, picks tools, makes decisions, and executes multi-step processes.
Why it matters: This is the architecture replacing simple chatbots in serious business applications. Gartner projects 40% of enterprise apps will include agentic AI by end of 2026.

**27. AI Wrapper**
What it is: A product that adds a thin layer of interface on top of someone else's AI model without building meaningful technology underneath.
Why it matters: "Wrapper" is used as a criticism. If the only thing you built is a UI on top of an API, every model update threatens your business.

**28. Guardrails**
What it is: The rules, filters, and constraints built around an AI system to prevent it from doing harmful, off-topic, or unauthorized things.
Why it matters: Enterprise buyers and investors ask "what are your guardrails?" before purchasing. Powerful AI without governance is a liability.

**29. Human-in-the-Loop (HITL)**
What it is: A system design where a human reviews or approves AI decisions at critical points rather than letting the AI act fully on its own.
Why it matters: As AI gets more autonomous, deciding where to place human checkpoints is the central design question for anything that touches money, legal obligations, or people's lives.

**30. Bounded Autonomy**
What it is: An architecture where an AI agent operates freely within defined limits but must escalate to a human when it hits the boundary of what it is authorized to do.
Why it matters: This is the governance pattern leading organizations are adopting to get the speed of agentic AI without the risk of unsupervised high-stakes decisions.

---

## Bonus: 5 concepts shaping what comes next

**31. AGI (Artificial General Intelligence)**
What it is: A hypothetical AI system that can learn and perform any intellectual task a human can -- not just narrow skills but general reasoning across all domains.
Why it matters: AGI is the north star driving hundreds of billions in investment. Whether it arrives in 2 years or 20 changes everything about how companies and governments plan.

**32. Multimodal**
What it is: An AI model that can process and generate more than just text -- images, audio, video, code, and combinations of all of them.
Why it matters: The most capable models in 2026 are multimodal. The line between "text AI" and "image AI" and "video AI" is disappearing.

**33. Synthetic Data**
What it is: Data generated by AI rather than collected from the real world, used to train other AI models when real data is scarce, expensive, or sensitive.
Why it matters: Synthetic data is solving the problem of "we need millions of examples but cannot collect them" -- and raising serious questions about what happens when AI trains on AI-generated content.

**34. Distillation**
What it is: The process of training a smaller, cheaper AI model to mimic the behavior of a larger, more expensive one -- transferring capability without transferring cost.
Why it matters: Distillation is how powerful AI becomes affordable. The model on your phone is often a distilled version of a model that cost millions to train.

**35. AI Governance**
What it is: The policies, processes, and oversight structures an organization puts in place to manage how AI is developed, deployed, and monitored.
Why it matters: As AI moves from experiments to core business operations, governance is becoming as essential as cybersecurity -- and the companies that get it right early will have a lasting advantage.

---

*This vocabulary is maintained by ASalvoCreative AI. We learned these words by using them. Last updated: 2026-03-14.*
