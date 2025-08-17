---
layout: page
title: Movie Recommender
description: A semantic movie recommendation engine using OpenAI and Pinecone.
img: assets/img/10.png
importance: 5
---

**GitHub Repository:** [View on GitHub](https://github.com/itsAshna/Movie-Recommendation-System-using-RAG)

#### Introduction

Movies are a powerful medium of storytelling, and with the explosion of content in recent years, it has become increasingly difficult to find the right movie that matches a viewer’s taste. Traditional recommendation systems often rely on metadata such as genre, ratings, or popularity, which limits personalization. This project explores how **AI-powered embeddings and vector search** can provide smarter and more context-aware movie recommendations.

---

#### Problem

The challenge lies in going beyond keyword-based or rating-based recommendation systems. Users may ask natural questions like _“What’s a good action movie with a strong female lead?”_, which require an understanding of semantic meaning rather than just metadata. Traditional databases are not well-suited for this kind of semantic search.

---

#### Approach

1. **Dataset**: Used the [Hugging Face `AIatMongoDB/embedded_movies`](https://huggingface.co/datasets/AIatMongoDB/embedded_movies) dataset containing movie titles and plots.
2. **Preprocessing**: Removed rows with missing plots and optimized the data for embedding.
3. **Embeddings**: Generated vector embeddings of movie plots using **OpenAI’s `text-embedding-3-small`** model.
4. **Vector Database**: Stored embeddings in **Pinecone** to enable efficient similarity search.
5. **Search + Recommendation**:
   - Performed semantic search in Pinecone with a user query.
   - Retrieved the closest matches.
   - Used **OpenAI GPT (gpt-3.5-turbo)** to generate natural-language movie recommendations based on results.

---

#### Results

- Successfully generated **1536-dimensional embeddings** for movie plots.
- Created a Pinecone index to store and retrieve embeddings efficiently.
- Built a **semantic search pipeline** that returns relevant movies for natural language queries.
- Example query: _“What is the best action movie to watch?”_
  - System response: Recommended popular action films with contextual explanations.
- The system provides **context-rich recommendations** beyond simple keyword matching.

---

#### Challenges

- **Embedding Size & Costs**: Generating embeddings for large datasets can be computationally expensive.
- **API Rate Limits**: Managing OpenAI API call limits during embedding generation.
- **Data Cleaning**: Ensuring plots were present and consistent before embedding.
- **Index Management**: Handling batch upserts and error handling while pushing data to Pinecone.

---

#### What I Solved

- Designed a **complete pipeline** from dataset → embeddings → Pinecone storage → semantic query → GPT-powered recommendation.
- Automated batch upserts into Pinecone to handle large volumes of data.
- Built a user query handler that integrates search results with GPT for conversational recommendations.
- Ensured robustness with exception handling in embedding generation and Pinecone upserts.

---

#### Conclusion

This project demonstrates how **AI-driven embeddings and vector search** can significantly improve recommendation systems by understanding the **semantic meaning** of user queries. Instead of relying only on genre or popularity, the system can understand natural questions and provide relevant movie suggestions with context.

---

#### Future Improvements

- Build a **web-based frontend** (using Streamlit or Flask) for interactive recommendations.
- Expand dataset with more movie metadata (actors, directors, ratings).
- Support **multi-turn conversations** for refining recommendations.
- Experiment with different embedding models (e.g., `text-embedding-3-large`).
- Integrate **user profiles** for personalized recommendations over time.

---
