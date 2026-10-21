#### What is Generative AI, and how is it different from traditional AI and machine learning?

Traditional AI and machine learning are commonly used to predict outcomes, classify data, detect anomalies or make recommendations. Generative AI produces new content, such as text, code, images and summaries, based on patterns learned during training.

For example, a traditional ML model might predict whether a loan applicant is high risk. A generative AI system could summarize the applicant's documents and explain the factors relevant to the assessment.

In an enterprise application, I would use traditional ML for well-defined prediction tasks and Generative AI for language-heavy tasks such as summarization, document understanding and natural-language interaction. These approaches can also be combined.

---
#### What is an LLM, and how does it generate responses?

A Large Language Model is a neural network trained on large amounts of data to predict and generate token sequences. Given an input prompt, it processes the context and generates a response token by token.

An LLM does not automatically know our latest internal business data. For that, we may need RAG, tools, or integration with enterprise systems.

---
#### What are tokens, tokenization, context windows and temperature?

- Tokens: Units of text processed by a model. A token may represent a word, part of a word or punctuation.
- Tokenization: The process of converting text into tokens.
- Context window: The maximum amount of input and output context a model can handle in a request, subject to that model's limits.
- Temperature: A sampling parameter that influences the variability of generated responses. Lower values generally produce more predictable output; higher values generally allow more variation.

For example, an agent processing a 300-page policy manual should not blindly send the entire document to the model on every request. RAG can retrieve only relevant sections, reducing unnecessary context and often lowering cost and latency.

---
#### What is the difference between Generative AI, an AI assistant, an AI agent and agentic AI?

- **Generative AI** is the underlying capability to generate content.
- An **AI assistant** provides an interface for helping users.
- An **AI agent** can select and execute tools to accomplish a task.
- **Agentic AI** describes systems that use **planning**, **decisions** and **actions** across one or more steps to pursue a **goal**.

---

#### What are the essential components of an AI agent?

A typical agent includes:
1. LLM: Interprets the request and selects an action.
2. Instructions: Define its role, objectives and constraints.
3. Tools: APIs, Lambda functions or other capabilities it can invoke.
4. State and memory: Preserve relevant task information and conversation context.
5. Orchestration: Controls execution, tool results, retries and stopping conditions.
6. Security controls: Enforce permissions, validate actions and protect data.
7. Observability: Records execution traces, errors, latency and cost.
For an HR assistant built with React and AWS Bedrock, the LLM interprets the employee's question, a retrieval tool searches authorized HR policies, and the application validates access before returning an answer.

Memory is optional; not every agent needs persistent memory. Similarly, some agents rely on deterministic workflows rather than open-ended planning.

---

#### How does an agent decide whether to answer directly or call a tool?

The model receives the user's request, its instructions, available tool descriptions and relevant context. It can generate a direct response or request a tool call.

For example, if the user asks, "What is our annual leave policy?", the agent might retrieve an HR policy document. If the user asks, "How many leave days remain in my account?", it needs to call an authorized HR API.

**The application—not the model itself—executes the requested function**, validates the result and returns it to the model if further processing is needed.

I would not rely solely on the model to determine whether a sensitive action is allowed. Authorization and business rules must be enforced independently.

---

#### What is the ReAct pattern?

ReAct stands for **Reasoning** and **Acting**. It is a pattern in which an LLM alternates between deciding what to do, invoking an action and using the returned observation to determine the next step.

For example:

1. The user reports an application outage.
2. The agent calls a monitoring API.
3. The results indicate a spike in errors.
4. The agent queries recent deployments.
5. It correlates the deployment with the incident and recommends a rollback.

In implementation, the orchestration layer manages the action-observation loop and enforces iteration limits.

---

For an enterprise policy assistant, I would usually begin with prompt engineering and RAG. If it must retrieve live leave balances, I would add a tool. Fine-tuning becomes a candidate when evaluations show a persistent need for specialized behavior that prompts and retrieval do not adequately address.

---

















