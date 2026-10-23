# 📌 Stage 1: Core LLM Fundamentals & Tokenization

- The goal of Stage 1 is to understand how large language models process
textual input and output at a mathematical level. You must understand token
dynamics to control API costs, mitigate context window limits, and optimize
system latency.

## Theoretical Foundations & Mathematics

### A. Tokenization & Vocabulary

- LLMs cannot directly understand words; they operate on numerical
sequences called **Token IDs.**

1. Byte Pair Encoding - BPE: Iteratively merges the most frequent pairs of
characters or byte sequences into unified tokens.

#### NOTE: The Agglutinative Language Disadvantage (Turkish vs English)

- English is an analytical language; words are stored directly as whole tokens
in the model's vocabulary(V).
- Turkish is an agglutinative language (words build up via suffix concatenation).
Tokenizers often fragment Turkish words into multiple smaller sub-words or
character-level byte chunks.
- Result: The exact same semantic statement consumes 30%–60% more tokens in
Turkish than in English. This directly increases latency and API consumption cost.

### B. Self-Attention Mechanics & Latency(O(N^2))

- In Transformer architectures, the Self-Attention calculation depends on Query(Q),
Key(K), and Value(V) matrices:
$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

- Quadratic Scaling: $QK^T$ scales with $O(N^2 \cdot d)$ complexity, where $N$ is the
sequence (token) length and 𝑑 is the hidden state dimension.

- When sequence length 𝑁 doubles, the computational cost of the attention step
quadruples. This explains why processing long contexts introduces non-linear
latency spikes.

### C. Financial & Latency Formulas

- Input Token cost:
$$\text{Cost}_{\text{input}} = \left(\frac{N_{\text{tokens}}}{1,000,000}\right) \times \text{Price}_{\text{per 1M input tokens}}$$

- Total Latency breakdown:
$$\text{Latency}_{\text{total}} = \text{TTFT (Time To First Token)} + (N_{\text{output tokens}} \times \text{TPOT (Time Per Output Token)})$$

## Core Technologies

1. *tiktoken* (OpenAI): High-performance BPE tokenizer written in Rust for Python. Key encodings:

    - o200k_base: Used for gpt-4o and gpt-4o-mini.
    - cl100k_base: Used for gpt-4, gpt-3.5-turbo, and embedding models.

2. Hugging Face tokenizers: Industrial tokenization library supporting WordPiece, Unigram, and BPE for open-source models (Llama, Mistral, Qwen).

3. Local Serving (vLLM / Ollama):

    - Ollama: Simple wrapper to run models locally via CPU/GPU.
    - vLLM: Production-grade engine using PagedAttention to optimize KV-cache memory allocation for high throughput and lower latency.
