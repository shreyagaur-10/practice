# Understanding Large Language Models (LLMs): Tokens, Context Windows, and Hallucinations

## Table of Contents

1. Introduction
2. How Large Language Models Work
3. Tokens

   * What is a Token?
   * Why Tokens are Used
   * Tokenization Process
   * Types of Tokenization
   * Token Limits
   * Cost and Performance Impact
4. Context Window

   * Definition
   * How Context is Constructed
   * Importance
   * Limitations
   * Context Window vs Memory
5. Hallucinations

   * Definition
   * Why Hallucinations Occur
   * Types of Hallucinations
   * Examples
   * Mitigation Techniques
6. Relationship Between Tokens, Context Window, and Hallucinations
7. Interview Questions and Answers
8. Common Misconceptions
9. Key Takeaways
10. References

---

# 1. Introduction

Large Language Models (LLMs) are deep learning models trained on massive amounts of textual data to understand and generate human language.

Popular examples include:

* GPT series
* Claude
* Gemini
* Llama
* Mistral

LLMs are based on the Transformer architecture introduced in the paper:

**"Attention Is All You Need" (2017)**

Unlike traditional software systems that follow predefined rules, LLMs learn statistical patterns from data and generate responses by predicting the next most probable token.

To understand LLM behavior, three concepts are fundamental:

1. Tokens
2. Context Window
3. Hallucinations

---

# 2. How Large Language Models Work

At a high level, an LLM follows this pipeline:

```text
Input Text
     ↓
Tokenization
     ↓
Embedding Generation
     ↓
Transformer Layers
     ↓
Attention Mechanism
     ↓
Next Token Prediction
     ↓
Generated Response
```

When a user enters a prompt, the model:

1. Converts text into tokens.
2. Maps tokens to numerical vectors.
3. Processes relationships using self-attention.
4. Predicts the next token.
5. Repeats the process until a response is generated.

Important:

LLMs do not "think" like humans.

They generate output by estimating probability distributions over possible next tokens.

---

# 3. Tokens

## What is a Token?

A token is the smallest unit of text processed by a language model.

Tokens are not always words.

A token may represent:

* A complete word
* Part of a word
* Punctuation
* Numbers
* Symbols

Example:

Input:

```text
ChatGPT is amazing!
```

Possible tokens:

```text
["Chat", "GPT", " is", " amazing", "!"]
```

---

## Why Not Use Words Directly?

Using words as the smallest unit creates challenges:

* Large vocabulary sizes
* Unknown words
* Typographical variations
* Multilingual complexity

Tokenization solves these issues by breaking text into reusable sub-components.

Example:

```text
unhappiness
```

can become:

```text
["un", "happi", "ness"]
```

This allows the model to understand words it has never seen before.

---

## Tokenization Process

Tokenization converts raw text into model-readable units.

Example:

Input:

```text
Artificial Intelligence is changing the world.
```

Tokenization:

```text
["Artificial", " Intelligence", " is", " changing", " the", " world", "."]
```

The tokenizer creates a mapping:

```text
"Artificial" → 5231
"Intelligence" → 8129
"is" → 287
```

These token IDs become inputs to the neural network.

---

## Types of Tokenization

### Character-Level Tokenization

```text
Hello
```

becomes

```text
["H","e","l","l","o"]
```

Advantages:

* Small vocabulary

Disadvantages:

* Longer sequences

---

### Word-Level Tokenization

```text
I love AI
```

becomes

```text
["I","love","AI"]
```

Advantages:

* Simplicity

Disadvantages:

* Cannot handle unseen words well

---

### Subword Tokenization (Used in Modern LLMs)

Example:

```text
internationalization
```

becomes

```text
["international","ization"]
```

Popular algorithms:

* BPE (Byte Pair Encoding)
* WordPiece
* SentencePiece

---

## Token Limits

Every model has a maximum token capacity.

Examples:

| Model   | Context Window |
| ------- | -------------- |
| GPT-3.5 | 16K            |
| GPT-4   | 128K           |
| Claude  | 200K+          |
| Gemini  | 1M+            |

If the limit is exceeded:

* Older information may be removed
* Prompt truncation occurs
* Model performance degrades

---

## Why Tokens Matter

Tokens directly impact:

### Cost

API providers often charge per token.

### Speed

More tokens require more computation.

### Memory Usage

Longer token sequences consume more resources.

---

# 4. Context Window

## Definition

A context window is the maximum number of tokens a model can process simultaneously.

Think of it as the model's temporary working memory.

---

## What is Included in Context?

A context window may contain:

* System instructions
* User prompts
* Previous responses
* Retrieved documents
* Tool outputs

Everything inside the context influences future predictions.

---

## Example

Conversation:

```text
User: My favorite color is blue.
```

Later:

```text
User: What is my favorite color?
```

The model answers correctly because the information remains inside the context window.

---

## Why Context Windows Matter

Large context windows enable:

### Long Conversations

Maintaining discussion continuity.

### Large Codebases

Analyzing thousands of lines of code.

### Research Papers

Reading lengthy technical documents.

### Retrieval-Augmented Generation (RAG)

Combining retrieved documents with user prompts.

---

## Context Window vs Memory

Many interviewers ask this question.

| Context Window          | Memory           |
| ----------------------- | ---------------- |
| Temporary               | Persistent       |
| Exists during inference | Stored long-term |
| Token-limited           | Database-driven  |
| Lost after conversation | Retained         |

An LLM naturally has context, not human-style memory.

---

## Challenges of Large Context Windows

Even large windows face problems:

### Information Dilution

Important information can become harder to locate.

### Increased Cost

Attention computation grows significantly.

### Latency

Inference becomes slower.

---

# 5. Hallucinations

## Definition

Hallucination occurs when an LLM generates information that appears correct but is factually inaccurate or completely fabricated.

Example:

Question:

```text
Who won the FIFA World Cup in 2042?
```

Possible hallucinated response:

```text
Brazil won the 2042 World Cup.
```

The event has not occurred.

---

## Why Hallucinations Occur

The fundamental reason:

LLMs optimize for:

```text
Next Token Prediction
```

not

```text
Truth Verification
```

The model's objective is statistical accuracy, not factual accuracy.

---

## Major Causes

### 1. Knowledge Gaps

The required information was absent during training.

### 2. Ambiguous Queries

Poorly specified prompts.

### 3. Outdated Information

Events after training cutoff are unknown.

### 4. Missing Context

Important information was not provided.

### 5. Overconfidence

Probability-based generation can produce fluent nonsense.

---

## Types of Hallucinations

### Factual Hallucination

Incorrect facts.

Example:

```text
Sydney is the capital of Australia.
```

---

### Citation Hallucination

Fake research papers or references.

---

### Numerical Hallucination

Incorrect calculations.

---

### Logical Hallucination

Broken reasoning despite fluent language.

---

## Hallucination Mitigation

### Prompt Engineering

Provide clear instructions.

### Retrieval-Augmented Generation (RAG)

Retrieve trusted documents before generation.

### Tool Use

Search engines
Databases
Calculators

### Fine-Tuning

Improve domain-specific behavior.

### Human Feedback

RLHF improves response quality.

---

# 6. Relationship Between Tokens, Context Window, and Hallucinations

These concepts are interconnected.

```text
User Prompt
      ↓
Tokenization
      ↓
Context Construction
      ↓
Attention Processing
      ↓
Next Token Prediction
      ↓
Response Generation
```

Missing context often increases hallucinations.

Large context windows help reduce information loss.

Efficient tokenization improves model performance.

---

# 7. Interview Questions and Answers

### What is a token?

A token is the smallest text unit processed by an LLM.

### Why are tokens important?

They determine cost, context size, and computational requirements.

### What is a context window?

The maximum amount of information a model can process simultaneously.

### What happens if the context window is exceeded?

Older information is truncated or removed.

### What is hallucination?

Generation of inaccurate or fabricated information.

### Why do hallucinations happen?

Because LLMs predict probable text rather than verify facts.

### How does RAG reduce hallucinations?

RAG provides external knowledge during inference.

### Does a larger context window eliminate hallucinations?

No. It reduces information loss but does not guarantee factual correctness.

### What is the difference between memory and context?

Context is temporary; memory is persistent.

---

# 8. Common Misconceptions

### "LLMs understand language like humans."

False.

They learn statistical patterns from data.

### "LLMs store every fact."

False.

Knowledge is distributed across model parameters.

### "Bigger models never hallucinate."

False.

They generally hallucinate less but still make mistakes.

### "Context window equals memory."

False.

Context is temporary working information.

---

# 9. Key Takeaways

* Tokens are the fundamental units processed by LLMs.
* Tokenization converts text into machine-readable representations.
* Context windows determine how much information can be considered at once.
* Hallucinations arise because models optimize for prediction rather than truth.
* Retrieval-Augmented Generation helps reduce hallucinations.
* Understanding these concepts is essential for AI engineering, prompt engineering, RAG systems, and LLM interviews.

---

# 10. References

1. Attention Is All You Need (2017)
2. GPT Technical Reports
3. Transformer Architecture Papers
4. OpenAI Documentation
5. Anthropic Research
6. Google Gemini Technical Reports
7. Meta Llama Research Papers
