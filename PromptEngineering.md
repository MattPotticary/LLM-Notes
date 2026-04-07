# Prompt engineering

[Home](outline.md)

- [Prompt engineering](#prompt-engineering)
  - [Prompt Engineering Terminology](#prompt-engineering-terminology)
  - [Techniques](#techniques)
  - [Components](#components)
  - [Testing and Evaluation](#testing-and-evaluation)
  - [Prompt Engineering Tools and Frameworks](#prompt-engineering-tools-and-frameworks)

## Prompt Engineering Terminology

- Prompt: Input text given to an LLM to elicit a response.
- Prompt Engineering: The art of crafting effective prompts for optimal LLM outputs.

## Techniques

- Zero-shot Prompting: asking the model to perform a task directly without providing examples.
- Few-shot Prompting: providing a small number of examples to show the desired input-output behavior.
- Chain-of-Thought (CoT): prompting the model to articulate intermediate reasoning steps before giving an answer.
- Tree-of-Thoughts (ToT): exploring multiple parallel reasoning paths and selecting the best conclusion.
- Self-Consistency: generating multiple reasoning traces and choosing the most frequent or consistent result.
- Instruction Tuning: fine-tuning models on datasets of instructions and desired outputs to improve task following.
- Retrieval-Augmented Prompting: adding externally retrieved context to the prompt to ground the model’s response.

## Components

- Instructions: Clear directives for the task.
- Context: Background information or examples.
- Examples: Sample inputs and outputs.
- Constraints: Limits on length, style, or content.
- Role Assignment: Specifying personas (e.g., "You are an expert...").

## Testing and Evaluation

- Metrics: Accuracy, Relevance, Coherence.
- Human-in-the-Loop: Manual review.
- Automated Tools: Benchmarks like HELM or custom scripts.

## Prompt Engineering Tools and Frameworks

- LangChain
- PromptFlow
- OpenAI Playground
- Hugging Face Transformers
