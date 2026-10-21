#### What is Generative AI, and how is it different from traditional AI and machine learning?

Traditional AI and machine learning are commonly used to predict outcomes, classify data, detect anomalies or make recommendations. Generative AI produces new content, such as text, code, images and summaries, based on patterns learned during training.

For example, a traditional ML model might predict whether a loan applicant is high risk. A generative AI system could summarize the applicant's documents and explain the factors relevant to the assessment.

In an enterprise application, I would use traditional ML for well-defined prediction tasks and Generative AI for language-heavy tasks such as summarization, document understanding and natural-language interaction. These approaches can also be combined.

---
#### What is an LLM, and how does it generate responses?
Answer:

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

- Generative AI is the underlying capability to generate content.
- An AI assistant provides an interface for helping users.
- An AI agent can select and execute tools to accomplish a task.
- Agentic AI describes systems that use **planning**, **decisions** and **actions** across one or more steps to pursue a **goal**.

---

