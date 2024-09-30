# Overview

Epsilla offers an open-source vector database. Our focus is on ensuring scalability, high performance, and cost-effectiveness of vector search. Epsilla bridges the gap between information retrieval and memory retention in Large Language Models. We see ourselves as the **Hippocampus for AI**.

## Common use cases

Here are some common use cases of Epsilla vector database

### 1. Augmenting LLMs with Proprietary Data

**Problem:** LLMs don’t have latest knowledge about the world (e.g., GPT-4 has a knowledge cutoff of April 2023), and don’t have knowledge about any private data (e.g., your company's knowledge base)

**Our solution:** Augment LLMs by adding semantically similar information retrieved from vector database into the prompt (also known as [Retrieval Augmented Generation](https://ai.meta.com/blog/retrieval-augmented-generation-streamlining-the-creation-of-intelligent-natural-language-processing-models/)).

**Benefits:** Enable the LLMs to work for your own data and knowledge. Compare to using fine-tuning, RAG has a much faster time-to-value, is much cheaper for both engineering cost and hardware cost, and support real time knowledge updates.\


<figure><img src="../.gitbook/assets/Screenshot 2023-09-18 at 7.07.38 PM (1).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-02-14 at 4.35.55 PM.png" alt=""><figcaption><p>Example: Upload IRS tax publications</p></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-02-14 at 4.37.25 PM.png" alt=""><figcaption><p>Example: Build a tax assistant chatbot augmented by IRS publications</p></figcaption></figure>

### 2. Build Better Recommendation Systems

**Problem:** It’s really hard to improve recommendation result relevance, and even harder to build a scalable realtime recommendation system.

**Our Solution:** Use embedding as the bridge between incomparable data types to leverage the hidden relevance of user behavioral data during recommendation.

**Benefits:** Vector DB that leverages the hidden relevance improves recommendation recall. Epsilla’s low query latency is vital to building a realtime recommendation system.

<figure><img src="../.gitbook/assets/renchusong_draw_a_recommendation_system_with_input_product_imag_b9b02df5-bc55-4c5a-ac75-466bb16339be.png" alt="" width="563"><figcaption></figcaption></figure>

### 3. Find Hidden Insights From Unstructured Data

**Problem:** It’s really hard to analyze and query unstructured data (images, audios, videos) based on their content semantics.

**Our Solution:** Connect and index the unstructured data based on the semantic relevance of their content, and enable multimodal search and analytics.

**Benefits:** Multimodal search becomes as easy as text search. No need to manually label unstructured data and convert to structured data anymore.

<figure><img src="../.gitbook/assets/Recomendation System.drawio (1).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-09-26 at 12.36.44 PM.png" alt="" width="563"><figcaption></figcaption></figure>

