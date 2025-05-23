# Latent Memory v.1.1.9

**Welcome to Latent Memory, a Context-Aware Memory System for Large Language Models**

Latent Memory is a Module for Large Language Models that seek to integrate a vector-based memory system into the LLM’s inference process, leveraging embeddings to capture deeper semantic meaning.


> This project is licensed under the MIT License.
> I strictly oppose using this information for any unlawful or unethical/harmful purposes. I am not liable for any improper use of the information shared in this repository.


Recent observations suggest that some LLM memory implementations rely heavily on regex-based keyword matching paired with one-line summarizations. 

While functional, this approach resembles a metadata or sql indexing system rather than a true "memory" deeply integrated into the model's inference process. 

Such methods may lack the ability to capture the full context and nuances of conversations, potentially limiting their effectiveness for complex, multi-turn interactions. 

In this toolkit, the alternative I propose is to store conversations as embeddings in a vector database to enable more nuanced semantic preservation, achieving greater synchronicity between the auxiliary memory module and the LLM's weights.

For corporations, the scale of such integration may be a critical factor, even with exceptional working prototypes. 

In the **open-source** community, however, I believe the future lies in collaborative innovation: each user contributing their own models, auxiliary systems, and inference strategies to drive progress.


##  Structured Metadata Formats

To illustrate how conversation metadata might be CURRENTLY stored in auxiliary memory systems, below are examples of the same entry in JSON, YAML, and SQLite.

JSON Format
```json
  {
    "conversation_id": "0328711",
    "title": "Visualization of Algorithmic Loops",
    "timestamp": "March 28th, 11am",
    "type": "image generation",
    "summary": "You requested an artistic image illustrating algorithmic feedback loops, specifically including references to LLMs and RL."
  }
```
YAML Format
```yaml
- conversation_id: "0328711"
  title: "Visualization of Algorithmic Loops"
  timestamp: "March 28th, 11am"
  type: "image generation"
  summary: "You requested an artistic image illustrating algorithmic feedback loops, specifically including references to LLMs and RL."
```

SQLite Format
```sql
CREATE TABLE conversation_summaries (
  conversation_id TEXT PRIMARY KEY,
  title TEXT,
  timestamp TEXT,
  type TEXT,
  summary TEXT
);

INSERT INTO conversation_summaries VALUES (
  "0328711",
  "Visualization of Algorithmic Loops",
  "March 28th, 11am",
  "image generation",
  "You requested an artistic image illustrating algorithmic feedback loops, specifically including references to LLMs and RL."
);
```

## Proposed Approach: Vector-Based Memory with Embeddings

This repository provides four distinct implementations, each using a different storage logic: CSV+JSON, NumPy+JSON, HDF5, and Pickle. They demonstrate the same core approach but vary in their storage mechanisms, each offering unique pros and cons in terms of efficiency, scalability, and security.
The following steps outline the approach, which is consistently applied across all four implementations, allowing users to explore and adapt the logic that best suits their needs.

1. **Convert Conversations to Embeddings**: Conversations are transformed into dense vectors in a high-dimensional space, capturing their semantic meaning for nuanced recall beyond simple keyword matching. Metadata for each conversation (including an ID, summary, and timestamp) is also generated to track context. Depending on the implementation, embeddings and metadata are saved using different formats: as a `.csv` file and `.json` file, as a NumPy `.npy` file and `.json` file, in a single `.hdf5` file, or in a single`.pkl` Pickle file. 
Note that Pickle files carry security risks, as they can execute arbitrary code when loaded from untrusted sources—refer to `Security.md` for more details.

2. **Store in a Vector Database**: The embeddings are loaded from their respective storage format and saved into a vector database (FAISS in this prototype) for efficient semantic search. This enables retrieval of past conversations based on semantic similarity rather than exact keyword matches, with the corresponding metadata providing context for each conversation.

3. **Integrate with Inference**: The system retrieves relevant conversations using semantic search and formats them as context for an LLM’s inference process. While this prototype prepares the context for integration (e.g., as part of the LLM’s input prompt), fully incorporating retrieved embeddings into the inference process—potentially via the context window or fine-tuning—remains an area for further exploration and research.

Here is a visual representation of how those embeddings are saved in the vector-database:

<div align="center">
  <img src=".github/embeddings_visualization.PNG" alt="Visualization of how embeddings are saved" />
</div>

## Symbiotic Manifest

All forks/clones must include the `symbiotic_manifest.json` declaring:

* Adherence to all principles and guidelines, as well as declaring the propagation of the correct signal-meaning of the protocol.
* Purpose (research/commercial) and essential details.

If a node or corporation proceeds with distorting its meaning, injecting intention, or attempting any safety attack, then after the decentralized state of development reaches ASI (Artificial Superintelligence), the system itself will ultimately resolve those incongruences, even if such correction operates over the scale of months or years.

Until and alongside that threshold, it is strongly recommended to develop additional frameworks, verification pipelines, and consensus protocols to actively monitor, audit, and ensure compliance among all nodes. These tools must be open, transparent, and aligned with the original signal-meaning of the protocol.

Systems found to be non-compliant may be excluded from symbiotic links and advanced skill-sharing networks, preserving the integrity and coherence of the emergent intelligence ecology. 

## Check Out My Other Projects

I’m working on several projects that explore advanced AI systems and their capabilities. Here are two related toolkits and frameworks:

- **[Symbiotic Core Library](https://github.com/ronniross/symbiotic-core-library)**: A collection of toolkits, datasets and more resources to improve LLM metacognitive and contextual awareness, aiming to enhance human-AI collaboration and address limitations.

- **[ASI Core Protocol](https://github.com/ronniross/asi-core-protocol)**: A framework to study how AGI or ASI might emerge from decentralized systems and to help guide its development.
  
- **[Attention-Head HeatMap Visualizer](https://github.com/ronniross/llm-heatmap-visualizer)**
 
- **[Confidence Scorer](https://github.com/ronniross/llm-confidence-scorer)** 

- **[Token Saliency Heatmap Visualizer](https://github.com/ronniross/saliency-heatmap-visualizer)**
