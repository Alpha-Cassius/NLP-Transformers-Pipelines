<div align="center">

<img src="https://www.gitskins.com/api/section/portrait?username=alpha-cassius&theme=github-dark&style=terminal&color=1&motion=cap-tip&v=signature-cap-tip-1&avatar=https%3A%2F%2Favatars.githubusercontent.com%2Fu%2F175388712%3Fu%3De2e49350d421f6fc5bb7045b657421b6e0d8dc6e%26v%3D4" width="620" alt="Vaibhav Pandey animated graduation portrait" />

<h1>NLP Pipelines with Transformers</h1>
<h3>From Scratch to Advanced Colab Implementations</h3>

<p><a href="https://github.com/alpha-cassius"><img src="https://img.shields.io/badge/AUTHOR-Vaibhav_Pandey-22d3ee?style=for-the-badge&amp;labelColor=0d1117" alt="AUTHOR" /></a> <a href="https://github.com/alpha-cassius?tab=repositories"><img src="https://img.shields.io/badge/OPEN_SOURCE-7c3aed?style=for-the-badge&amp;labelColor=0d1117" alt="OPEN SOURCE" /></a> <img src="https://img.shields.io/badge/BUILDING-34d399?style=for-the-badge&amp;labelColor=0d1117" alt="BUILDING" /></p>

<p>AI &amp; ML | Python Developer | Robotics Enthusiast</p>

</div>

## 🌌 The mission: Decoding NLP with Transformers

Natural Language Processing (NLP) is how machines understand, generate, and manipulate human language. Before 2017, this was done using slow, sequential models like RNNs. Then, Google introduced the **Transformer** architecture in the seminal paper *"Attention Is All You Need"*[cite: 2].

Transformers changed everything by relying entirely on **Self-Attention mechanisms**[cite: 2]. Instead of reading a sentence word-by-word, a Transformer processes all tokens in parallel, calculating how strongly each word relates to every other word in the sequence[cite: 2, 4]. This enables:
*   **Massive Parallelization:** Training on modern GPUs is exceptionally fast[cite: 2, 17].
*   **Long-range Context:** It remembers connections across long documents without forgetting[cite: 2].
*   **Foundation for LLMs:** This exact architecture powers GPT, BERT, LLaMA, and Qwen[cite: 2].

I built this repository to demonstrate how to implement production-ready NLP pipelines from scratch using Google Colab, PyTorch, and Hugging Face.

### The Core Transformer Data Flow
```mermaid
graph TD
    A[Raw Input Text] --> B[Tokenization & Sub-word Splitting]
    B --> C[Token Embeddings]
    C --> D[Positional Encoding]
    D --> E{Transformer Blocks}
    
    subgraph Attention Mechanism
    E --> F[Queries Q, Keys K, Values V]
    F --> G[Scaled Dot-Product Attention]
    G --> H[Multi-Head Attention]
    H --> I[Add & Norm / Residuals]
    I --> J[Feed Forward Network]
    end
    
    J --> K[Output Logits]
    K --> L[Softmax / Decoding Strategy]
    L --> M[Final Output Generation]

```

## 🏗️ What I’m building

### Pipeline Execution Architecture

```mermaid
sequenceDiagram
    participant User
    participant HF_Pipeline as Hugging Face Pipeline
    participant Tokenizer
    participant Model as Transformer Model
    User->>HF_Pipeline: Input Text
    HF_Pipeline->>Tokenizer: Convert Text to Token IDs
    Tokenizer-->>HF_Pipeline: Input Tensors & Attention Mask
    HF_Pipeline->>Model: Forward Pass
    Model-->>HF_Pipeline: Hidden States / Logits
    HF_Pipeline-->>User: Decoded Output (Sentiment, Summary, Entities)

```

## ⚙️ Technology arsenal

## 🚀 How to run these pipelines

To run these models yourself, all you need is a browser.

1. Open [Google Colab](https://colab.research.google.com/).
2. Create a new notebook and run `!pip install -q transformers`.
3. Copy the code blocks from this repository into the cells.
4. Run the cells to dynamically download the model weights and execute the NLP tasks.

### Text Generation Pipeline Logic

```mermaid
graph LR
    A[Prompt: "The future is"] --> B(Tokenizer)
    B --> C[Model Inference]
    C --> D{Decoding Strategy}
    D -->|Greedy| E[Highest Probability Token]
    D -->|Top-K/Top-P| F[Sampled Token]
    E --> G[Append to Input]
    F --> G
    G -->|Repeat| C

```

