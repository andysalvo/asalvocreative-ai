# AI Vocabulary Corpus

This is the canonical source for ASalvoCreative AI's vocabulary content. Every explanation here is written to be direct, accurate, and useful. The web-facing product pulls from this document.

**Amendment policy:** This document works in amendments. Entries can be improved or expanded but canonical truth is preserved. Every factual claim must be sourced.

**Voice:** Write like a tutor. Use analogies that any educated adult would understand. Do not show off. The goal is to make smart people think like AI engineers.

---

## 1. LLM (Large Language Model)

Every major AI tool -- ChatGPT, Claude, Gemini -- is powered by an LLM. An LLM is a program that has read essentially the entire public internet and learned the patterns of how language works. It does not "know" things the way a person does. It predicts what word comes next based on everything it has ever read.

The reason it feels intelligent is that predicting language well turns out to require understanding context, logic, and reasoning. The "large" part refers to the number of parameters -- internal variables the model can adjust during training. GPT-3 had 175 billion parameters, and OpenAI published that number openly in their research paper. By the time GPT-4 came around, they stopped sharing. They cited the "competitive environment" as the reason, which tells you something about how fast the stakes changed between 2020 and 2023.

What has been reported, though not officially confirmed by OpenAI, is that GPT-4 uses roughly 1.76 trillion parameters through something called a Mixture of Experts architecture. The way that works is that instead of one massive model doing everything, there are eight separate "expert" sub-models, each around 220 billion parameters. When you send a query, a routing layer decides which experts are the right ones to handle it -- not all eight fire on every question. Think of it like a hospital where triage sends you to the right specialists rather than having every doctor in the building look at every patient. It is a way to get the benefits of a huge model without paying the full cost of running all of it every single time.

But more parameters does not automatically mean smarter. Google DeepMind showed this clearly with their Chinchilla model -- it had 70 billion parameters, less than half of GPT-3's 175 billion, and it outperformed GPT-3 on benchmarks. The difference was that Chinchilla was trained on significantly more and better data. How you train the model matters at least as much as how large you make it, which is why the current competition between AI labs is not just about building bigger models but about finding better data and better training methods.

LLMs are the foundation layer of the current AI era. Almost every AI product on the market in 2026 is built on top of one.

**Sources:**
- Brown, Tom, et al. "Language Models Are Few-Shot Learners." arXiv:2005.14165, 2020. (GPT-3 175B parameter count published openly)
- Hoffmann, Jordan, et al. "Training Compute-Optimal Large Language Models." arXiv:2203.15556, 2022. (Chinchilla 70B outperforming GPT-3 175B)
- Reported GPT-4 architecture details (eight experts, ~220B each, ~1.76T total) sourced from Semafor, March 24, 2023. Summarized by The Decoder: https://the-decoder.com/gpt-4-has-a-trillion-parameters/

---

## 2. Token

LLMs do not process words the way we read them. They process tokens, which are small chunks of text that the model treats as individual units. On average in English a token is roughly three-quarters of a word, so "the" is one token, "hamburger" is two tokens, "AI" is one token, and a short sentence runs about 10 tokens.

The way these tokens get created is through something called byte-pair encoding. Before a model is ever trained, the developers build a fixed vocabulary by scanning massive amounts of text and repeatedly merging the most common pairs of characters. Common words like "the" or "and" end up as single tokens because they appear so frequently. Less common words get split into pieces that the model can still recognize, so "tokenization" becomes "token" plus "ization" as two separate tokens. Rare or technical words get broken down even further into smaller fragments. Once this vocabulary is locked in, it stays fixed for the life of the model. Every conversation the model ever has uses the same token dictionary.

This creates a real problem for languages other than English. Because the training data and the vocabulary-building process are heavily weighted toward English, Latin-script languages get packed efficiently at roughly one token per 0.75 words. But non-Latin scripts like Chinese, Japanese, Korean, and Arabic often require two to four times as many tokens to express the same meaning. So if you ask the exact same question in Korean instead of English, it costs more money to process and it takes up more of the model's context window, which means you have less room left for the rest of your conversation. The tokenizer was built on English-dominant data and every other language pays a tax for that.

Tokens matter practically because they are the unit that everything in AI is priced and limited by. When a model advertises a 200,000-token context window, that is roughly 150,000 English words, about the length of two novels. When a model responds slowly, it is because it generates tokens one at a time, sequentially, each one requiring its own round of computation. And when companies charge for API access, they charge per token, with a split that is important to understand: input tokens, meaning everything you send to the model, are priced separately from output tokens, meaning everything the model sends back. Output tokens cost two to four times more than input tokens because generating new text requires significantly more computation than reading existing text. For flagship models like GPT-4o or Claude Sonnet as of early 2026, input runs about $3 per million tokens and output runs about $15 per million tokens. Smaller and faster models like Haiku or GPT-4o mini charge between $0.25 and $0.80 per million input tokens and $1 to $4 per million output tokens. To put that in perspective, sending an entire novel as input to a flagship model costs roughly 40 cents.

**Sources:**
- OpenAI tokenizer documentation: https://platform.openai.com/tokenizer
- Byte-pair encoding explained: Hugging Face NLP Course, "Byte-Pair Encoding tokenization." https://huggingface.co/learn/nlp-course/en/chapter6/5
- Token cost disparities across languages: Petrov et al., "Language Model Tokenizers Introduce Unfairness Between Languages," NeurIPS 2023. https://arxiv.org/abs/2305.15425
- Model pricing: Anthropic API pricing page, https://www.anthropic.com/pricing; OpenAI API pricing page, https://openai.com/api/pricing

---

## 3. Context Window

The context window is the total amount of information an AI model can hold and work with at one time. Everything you paste in, everything you type, everything it says back -- all of that lives inside the context window. When it fills up, the model starts forgetting earlier parts of the conversation. Not because it is broken. Because it literally cannot see them anymore.

The easiest way to think about it is a desk. You can only spread out so many papers before things start falling off the edges. A bigger desk means more documents open at once. A smaller desk means you are constantly shuffling things in and out.

The numbers help make this concrete. 128,000 tokens is roughly 50,000 words. That is about the length of *The Great Gatsby*. So a model with a 128K context window can hold an entire novel and answer questions about it. Move up to 1,000,000 tokens and you can fit a full codebase or an entire semester of lecture transcripts. The newest models -- Gemini 3 Pro, Llama 4 Scout -- go to 10 million tokens, which is small library territory.

As of early 2026, the main frontier models look like this. Claude offers up to 1 million tokens. GPT-4.1 supports 1 million tokens. Gemini 2.5 Pro supports 1 million tokens. Those are the advertised numbers.

But here is the part most people do not talk about: advertised capacity and effective capacity are not the same thing. Most models perform best when you use roughly 60 to 70 percent of their stated maximum. Performance holds steady up to that point, then it drops off sharply. The reason is something researchers call the "lost in the middle" problem. Models pay the most attention to what is at the beginning and at the end of the context. The middle gets blurry. It is like reading a 300-page report -- you remember the opening and the conclusion, but page 158 is a blur. Claude 4 Sonnet is a notable exception here, with less than 5 percent accuracy loss across its full context range, but that is not the norm.

Cost is the other thing worth understanding. Context is not free. Every token you send in and every token the model sends back costs money. The range is enormous. DeepSeek V3 charges $0.27 per million tokens. Claude Opus 4.5 charges $25 per million tokens. That is nearly a 100x difference. In practice, a lot of teams use a hybrid approach -- routing simple queries to smaller, cheaper models and saving the expensive models for tasks that actually need them. That kind of routing can cut costs 40 to 60 percent.

**Sources:**
- Elvex, "Context Length Comparison: AI Models 2026," January 16, 2026. https://www.elvex.com/blog/context-length-comparison-ai-models-2026

---

## 4. Inference

Training is when an AI model learns. Inference is when it answers.

Every time you send a message to ChatGPT or Claude, the system runs billions of calculations on GPUs in a data center to generate your response. That process is called inference. It happens every single time anyone uses the product.

This is why AI costs money on an ongoing basis. Training happens once. You spend a huge amount upfront to build the model. But inference happens millions of times a day, and the bill scales directly with usage.

Here is what that looks like in practice. Anthropic spent $4.1 billion on training compute in 2025 and $2.7 billion on inference. Inference was already 40 percent of their total compute spend, and it is the number that keeps growing as more people use the product. OpenAI spent $8.7 billion on inference through Azure in just the first three quarters of 2025. These are not small line items. Across the industry, compute -- training and inference combined -- accounts for 54 to 62 percent of total costs. It dwarfs everything else, including AI researcher salaries.

Three forces are pushing inference costs up at the same time. First, more people are using AI every month. Second, models are getting larger, which means more computation per query. Third, new patterns like multi-step reasoning and always-on agents multiply the number of calls per task. A single user request that used to take one inference call might now take five or ten.

The labs are fighting back on cost. They distill large models into smaller, cheaper ones that run faster. They cache common responses so the system does not have to regenerate them from scratch. Google built TPUs and Amazon built Trainium -- specialized chips designed to run inference more efficiently than general-purpose GPUs.

But here is the part that matters most right now. Every major AI lab is currently unprofitable. They are spending two to three times more than they bring in as revenue. Anthropic does not project profitability before 2028. That means AI is being subsidized. The prices users pay today are artificially low. The $20 per month subscription is not covering the actual cost of generating your responses. That price will either go up or the economics will have to change significantly before this industry is self-sustaining.

**Sources:**
- Sam Altman on GPT-4 training cost: Fortune, April 4, 2024. https://fortune.com/2024/04/04/ai-training-costs-how-much-is-too-much-openai-gpt-anthropic-microsoft/
- AI company cost breakdowns: Epoch AI, "Compute accounts for the majority of expenses of AI companies," 2025. https://epoch.ai/data-insights/company-spending-breakdown
- OpenAI $8.7B inference spend: The Register, November 12, 2025. https://www.theregister.com/2025/11/12/openai_spending_report/

---

## 5. Hallucination

AI does not know what it does not know. When an LLM lacks a good answer, it does not say "I am not sure." It generates something that sounds right based on language patterns, even if it is completely false. That is a hallucination. An AI model will cite papers that do not exist, quote people who never said the attributed words, and state fabricated statistics with complete confidence.

This is not a bug that will be fixed in a future update. It is a fundamental property of how these models work, and once you understand the training process, you can see why.

During training, models get scored on accuracy with a simple system: one point for a right answer, zero points for "I don't know." Under that math, guessing always beats abstaining. If you get one point for being right and zero for saying nothing, there is no reason to ever say nothing. The model learns that producing some answer -- any answer -- is always the better move. It never gets rewarded for honesty about its own uncertainty.

That scoring problem is only part of it. Even models trained on perfectly clean data still hallucinate. If a fact appears only once in the training data -- researchers call it a "singleton" -- the model cannot distinguish that fact from noise. It has no way to tell whether something it saw once is true or whether it was an error in the data. If 20 percent of a given fact type appears only once in training data, you should expect at least a 20 percent hallucination rate on questions about that type. The math is that direct.

This is why models are more reliable on well-known topics and more dangerous on niche ones. A question about World War II has thousands of overlapping, reinforcing sources in the training data. A question about a specific local business or an obscure academic paper might have one source or none. The thinner the training data, the more the model is guessing, and the less you can tell from the output that it is guessing.

There is a proposed fix that makes intuitive sense: change the scoring system to penalize wrong answers more than it rewards right ones. For example, wrong answer gets negative nine points, right answer gets positive one, and "I don't know" gets zero. Under that math, guessing becomes expensive and abstaining becomes rational. This is the same logic behind medical licensing exams that penalize guessing -- when the cost of being wrong is high enough, you want the test-taker to admit uncertainty instead of gambling. That research is still early, but it shows the problem is at least understood at the structural level.

The practical skill this creates is knowing when to trust AI output and when to verify it independently. Any fact that matters should be checked against a primary source. And you should be more skeptical the more niche the topic is -- that is exactly where the model has the least data and the most reason to fill in gaps with plausible-sounding language.

**Sources:**
- Kalai et al., "Calibrated Language Models Must Hallucinate," arXiv:2311.14648, OpenAI Research. Updated September 2025.

---

## 6. RAG (Retrieval-Augmented Generation)

An LLM is trained on data up to a certain date. It does not know what happened yesterday. It does not have access to your company's internal documents, your customer database, or anything proprietary. So if you ask it a question that depends on any of that, it either guesses or tells you it does not know.

RAG fixes this. RAG stands for Retrieval-Augmented Generation. The idea is straightforward: before the model answers your question, it goes and looks up the relevant information first, then uses what it found to write the answer.

Here is how it actually works, step by step.

**Step 1: Prepare the knowledge base.** You take your documents -- could be PDFs, help articles, legal filings, whatever -- and break them into chunks. Each chunk gets converted into a mathematical fingerprint called an embedding. That embedding captures what the chunk means, not just what words it contains. All of these embeddings get stored in a vector database.

**Step 2: Process the question.** When someone asks a question, the system converts that question into its own embedding using the same method.

**Step 3: Retrieve.** The system compares the question's embedding against every chunk in the database and pulls the ones with the closest meaning. Those top results get placed into the context window alongside the original question.

**Step 4: Generate.** The model now writes its answer grounded in both its training and the specific material it just retrieved. It is not guessing from memory. It has the reference material right in front of it.

**The chunk-context problem.** There is a real limitation in step one. When you chop a document into chunks, each chunk loses its surrounding context. A chunk that says "revenue grew 3%" is useless on its own -- which company? Which quarter? Which product line? The retrieval system might pull that chunk because it is semantically close to the question, but without context it can mislead the answer.

Anthropic published a technique called contextual retrieval in September 2024 that addresses this. Before indexing, the system uses the model to prepend a brief explainer to each chunk -- something like "This chunk is from Acme Corp's Q3 2024 earnings report, discussing North American operations." That way the chunk carries its own context. This alone reduced retrieval failures by 35%. When they combined it with BM25 keyword matching and a reranking step, retrieval failures dropped by 67%.

**RAG vs. fine-tuning.** People sometimes ask why you would not just fine-tune the model on your data instead. Fine-tuning changes the model's weights -- it rewires the model itself. That is expensive, slow, and hard to update when your data changes. RAG leaves the model completely untouched. You are just feeding it reference material at the time of the question. The documents are swappable. You can update your knowledge base tonight and every answer tomorrow reflects the change.

For most enterprise use cases -- customer support, legal research, internal tools -- RAG is the right starting point. Fine-tuning makes sense when you need to change how the model behaves or writes. RAG makes sense when you need to change what the model knows.

**Sources:**
- Anthropic, "Introducing Contextual Retrieval," September 19, 2024. https://www.anthropic.com/news/contextual-retrieval
- Anthropic Help Center, "Retrieval augmented generation (RAG) for projects." https://support.claude.com/en/articles/11473015-retrieval-augmented-generation-rag-for-projects

---

## 7. Context Engineering

A prompt is the instruction you type into an AI tool. Context engineering is everything around that instruction -- the practice of designing what information, examples, and constraints the model sees before it generates a response.

Here is the difference. A prompt is "write a blog post." Context engineering is providing the brand voice guide, the target audience, three examples of posts that performed well, the specific topic, and constraints on length and tone -- and then asking the model to write. Same underlying request. Dramatically different output.

The AI research community landed on an important finding in 2025: the quality of what an AI produces depends more on the quality of the context you give it than on how cleverly you phrase the question. Andrej Karpathy, one of the original architects of OpenAI, put it directly: people think of prompts as the short task descriptions you type into a chatbot day to day. But the real work is everything else you set up around that instruction. A CLAUDE.md file -- a document that tells an AI agent who it is working for, what the project is, and how to behave -- is a practical example of context engineering.

This matters even more when AI is not just answering a single question but acting as an agent -- taking multiple steps, calling tools, making decisions across a longer task. An agent might run dozens of steps to complete a job. Every piece of information it carries competes for attention in a fixed context window. As that window fills up, the model's ability to recall earlier information drops. Anthropic, the company behind Claude, calls this "context rot." It is one of the core failure modes in agent systems.

The practical techniques are specific. Write system prompts at what Anthropic calls "the right altitude" -- specific enough to actually guide behavior, flexible enough that they do not break when conditions change. Use few-shot examples liberally, meaning you show the model two or three concrete examples of what good output looks like before asking it to produce its own. Design tools so they are self-contained with clear inputs, because the model has to understand what each tool does from its description alone. Use just-in-time retrieval -- pull in relevant information right when the model needs it instead of stuffing everything into the context upfront. When contexts get long, compress them through summarization, external memory stores, or handing sub-tasks off to separate agents that report back with only the result.

The shift from "prompt engineering" to "context engineering" as the standard term marks the moment the field recognized that the hard part is not writing the instruction. It is designing everything around it. It is a systems design problem, not a copywriting problem. The people who get the best results from AI are not writing better sentences. They are building better environments for the model to work inside.

**Sources:**
- Andrej Karpathy, X (Twitter), June 25, 2025. https://x.com/karpathy/status/1937902205765607626
- Anthropic Applied AI Team, "Effective context engineering for AI agents," September 29, 2025. https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

---

## 8. Agentic Workflow

A chatbot answers one question at a time. You type something, it responds, you type the next thing. An agent is different. You give it a goal, and it figures out the steps.

Here is what that looks like in practice. Say you tell an agent to fix a bug in your code. It reads the codebase. It finds the problem. It searches the documentation for the right fix. It edits the file. It runs the tests to make sure the fix works. It commits the change. You gave one instruction. The agent decided what tools to use, what order to do things in, and when the job was done.

The distinction that matters is between a chatbot that waits for you to tell it what to do next and an agent that figures out the next step on its own.

Gartner projects that 40% of enterprise applications will have task-specific AI agents by the end of 2026. In 2025, that number was under 5%. Going from 5% to 40% in a single year is one of the fastest enterprise technology shifts since public cloud adoption.

The word "task-specific" is doing real work in that sentence. Gartner is not talking about general-purpose thinking machines. They mean agents that handle one well-defined job -- scanning network traffic, resolving IT support tickets, managing customer service cases from start to finish. The pattern in the earliest deployments is consistent: high volume, well-documented processes, clear success criteria. That is where agents work right now.

Gartner also warns about "agentwashing" -- vendors taking simple AI assistants and rebranding them as autonomous agents. The test is straightforward: if the system waits for a human to tell it what to do at each step, it is an assistant, not an agent.

Not everyone is moving at the same speed. Regulated industries like healthcare, financial services, and government are going slower because the liability question is unresolved. If an agent makes a decision that causes harm, who is responsible? Nobody has a clean answer yet.

The longer timeline projections give a sense of where this is heading. By 2028, Gartner expects one-third of user interfaces to shift to agentic front ends. By 2029, half of knowledge workers will need skills to create or manage agents. By 2035, agentic AI could drive $450 billion in enterprise software revenue, roughly 30% of the total market, up from 2% today.

**Sources:**
- Gartner, "Gartner Predicts 40 Percent of Enterprise Apps Will Feature Task-Specific AI Agents by 2026," August 26, 2025. https://www.gartner.com/en/newsroom/press-releases/2025-08-26-gartner-predicts-40-percent-of-enterprise-apps-will-feature-task-specific-ai-agents-by-2026-up-from-less-than-5-percent-in-2025

---

## 9. Guardrails

An AI model, left unconstrained, will attempt almost anything it is asked to do. Guardrails are the technical boundaries set to keep it operating within acceptable limits. Some are built into the model by its creators. But most are set by the organizations deploying the AI.

There are three layers to how guardrails actually work.

The first layer is input filters. Before the model even sees a prompt, filters screen what goes in. They flag things like Social Security numbers or disguised prompts trying to trick the model into ignoring its rules.

The second layer is output validation. After the model generates a response, checks run on what comes out. These can block toxic language, catch hallucinated facts, or hold any response that leaks private data before it reaches the user.

The third layer is scope limitation. This defines what the AI is allowed to touch -- which databases, which tools, which dollar amounts. A bank might configure its AI so it can answer questions about account balances but can never authorize a transaction. Or it might set a rule that any transaction over $100,000 routes to a human automatically.

These three layers matter more now because of agents. A chatbot generates text. If it hallucinates, someone reads a wrong answer. An agent acts -- it executes transactions, sends emails, updates records. The stakes are different. And static filters are not enough because agents can chain tools together in ways that bypass any single checkpoint. Agentic AI requires continuous, deterministic controls: check every action before it executes, log every decision in a searchable audit trail, and never rely on one model to judge whether another model is being honest.

One distinction worth understanding: guardrails and governance are not the same thing. Guardrails are technical enforcement -- code-level controls that stop specific behaviors. Governance is the organizational layer -- the policies, the review board, the accountability structure that decides what the controls should be and whether they are working. You need both. Guardrails without governance means you have controls running but no one deciding if they are the right controls. Governance without guardrails means you have a handbook that no one follows.

**Sources:**
- CIO, "Guardrails and governance: A CIO's blueprint for responsible AI," 2025. https://www.cio.com/article/4094586/guardrails-and-governance-a-cios-blueprint-for-responsible-generative-and-agentic-ai.html

---

## 10. Human-in-the-Loop (HITL)

Human-in-the-loop means a human reviews, approves, or overrides what the AI does at specific points in a process. Instead of letting the AI run start to finish on its own, you build in checkpoints where a person looks at the output before it moves forward.

A code review before deployment is human-in-the-loop. An approval step before sending an AI-drafted email is human-in-the-loop. A manager reading an AI-generated report before it goes to a client is human-in-the-loop. The pattern is the same every time: AI does the work, human checks the work, then it ships.

The question every organization has to answer is where to place these checkpoints. Too many and you lose the speed advantage of using AI in the first place. Too few and you have an unsupervised system making decisions that involve money, legal obligations, or reputation.

Right now, most organizations are getting this wrong. Only 27 percent of organizations using generative AI say their employees review all AI-generated content before it reaches customers. A similar share admits that 20 percent or less of their AI output gets checked at all. That means most AI-generated content is going out the door with no human eyes on it.

The consequences show up in the data. 51 percent of organizations using AI have experienced at least one negative consequence. Nearly a third of those trace the problem back to inaccuracy -- the AI got something wrong and nobody caught it. That is not an AI failure. That is an oversight failure. The AI did what AI does. Nobody was watching.

McKinsey found that high-performing organizations handle this differently. Instead of reviewing AI outputs after the fact, they shift oversight earlier in the process. They are nearly twice as likely to involve their legal function early and to build risk reviews into the development stage, not the deployment stage. They decide where the checkpoints go before the system is live, not after something breaks.

But the governance structures behind all of this are still thin across the board. Only 28 percent of organizations say their CEO oversees AI governance. Just 17 percent give that responsibility to the board. 13 percent have hired AI compliance specialists. Only 6 percent have hired AI ethics specialists. Most organizations are deploying AI faster than they are building the oversight structures to manage it.

**Sources:**
- McKinsey & Company, "The state of AI in 2025: Agents, innovation, and transformation," March 2025. https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai
- McKinsey & Company, "The state of AI: How organizations are rewiring to capture value." https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai-how-organizations-are-rewiring-to-capture-value

---

*This corpus is maintained by ASalvoCreative AI. Last updated: 2026-03-14.*
