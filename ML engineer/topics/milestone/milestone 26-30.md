# M26 — RAG + Trusted Knowledge 📚🔎

M25-এ আমরা শিখেছি **AI-generated educational video কীভাবে evaluate করতে হয়**।

এখন M26-এর লক্ষ্য আরও গুরুত্বপূর্ণ:

> **AI যেন নিজের memory থেকে আন্দাজ করে educational content না বানিয়ে trusted knowledge থেকে তথ্য নিয়ে video তৈরি করে।**

অর্থাৎ:

```text id="m26arch"
User Prompt
     ↓
Knowledge Search
     ↓
Trusted Sources
     ↓
Relevant Information
     ↓
LLM
     ↓
Verified Educational Script
     ↓
Scene JSON
     ↓
Video Generation
     ↓
Evaluation
```

---

# 1. RAG কী?

**RAG = Retrieval-Augmented Generation**

সহজভাবে:

```text id="ragbasic"
Question
   ↓
Search Knowledge
   ↓
Relevant Documents
   ↓
LLM
   ↓
Answer
```

Normal LLM:

```text id="normalllm"
Question
   ↓
LLM
   ↓
Answer
```

RAG:

```text id="ragllm"
Question
   ↓
Retriever
   ↓
Knowledge Base
   ↓
Relevant Documents
   ↓
LLM
   ↓
Answer
```

---

# 2. কেন তোমার Educational Video AI-তে RAG দরকার?

ধরো user বলল:

> Explain Newton's second law.

LLM হয়তো সঠিকভাবে বলবে:

```text
F = ma
```

কিন্তু যদি user জিজ্ঞেস করে:

> Explain this specific university textbook chapter.

তখন শুধু LLM-এর internal knowledge যথেষ্ট নয়।

আমরা চাই:

```text id="x8wq7z"
Textbook / Trusted Source
       ↓
Retrieve relevant section
       ↓
LLM
       ↓
Explanation
```

---

# 3. RAG-এর Complete Architecture

```text id="7x1qaz"
                 USER
                  ↓
             User Prompt
                  ↓
          Query Understanding
                  ↓
             Query Rewrite
                  ↓
             ┌──────────┐
             │ Retriever│
             └────┬─────┘
                  ↓
            Vector Database
                  ↓
            Relevant Chunks
                  ↓
          Reranking / Filtering
                  ↓
             Context
                  ↓
                LLM
                  ↓
        Educational Content
                  ↓
            Fact Checking
                  ↓
             Scene Planner
                  ↓
              Video AI
```

---

# 4. Knowledge Base কী?

আমাদের trusted educational information যেখানে থাকবে।

উদাহরণ:

```text id="f5a8d2"
knowledge/
├── biology/
│   ├── photosynthesis.txt
│   ├── cell.txt
│   └── genetics.txt
│
├── physics/
│   ├── newton_laws.txt
│   └── electricity.txt
│
├── mathematics/
│   ├── algebra.txt
│   └── calculus.txt
│
└── computer_science/
    ├── algorithms.txt
    └── data_structures.txt
```

Production-এ PDF, HTML, DOCX, database records, curated documents ইত্যাদিও থাকতে পারে।

---

# 5. Trusted Source মানে কী?

সব source সমান trustworthy নয়।

আমাদের source hierarchy থাকতে পারে:

```text id="w6q7nx"
Tier 1
Official / primary / authoritative
        ↓
Tier 2
University / textbook / academic
        ↓
Tier 3
High-quality educational resources
        ↓
Tier 4
General web content
        ↓
Tier 5
Unknown / unverified
```

Educational system-এ important claims-এর জন্য higher-quality sources prefer করা উচিত।

---

# 6. RAG-এর 5টি Main Step

M26-এর সবচেয়ে গুরুত্বপূর্ণ অংশ:

```text id="8w8f3x"
1. Ingestion
2. Chunking
3. Embedding
4. Retrieval
5. Generation
```

এর সাথে production-এ:

```text id="bq9t8a"
Reranking
+
Citation
+
Verification
```

যোগ হবে।

---

# 7. Step 1 — Ingestion

Document:

```text id="7f1c6n"
PDF
 ↓
Text Extraction
 ↓
Clean Text
 ↓
Chunks
```

Example:

```text id="n1z5sx"
Newton's Second Law explains
the relationship between force,
mass and acceleration...
```

---

# 8. Step 2 — Chunking

পুরো textbook একসাথে LLM-কে দেওয়া যাবে না।

ধরো:

```text id="k3b2p7"
100-page PDF
```

এটা ছোট অংশে ভাগ করব:

```text id="w1j9a0"
Document
 ↓
Chunk 1
Chunk 2
Chunk 3
Chunk 4
...
Chunk 500
```

---

# 9. Chunk কেন দরকার?

User query:

> What is Newton's second law?

আমাদের পুরো textbook দরকার নেই।

শুধু relevant অংশ:

```text id="7r3v8m"
Newton's Second Law
...
F = ma
...
```

retrieve করলেই হবে।

---

# 10. Basic Chunking

```python id="8rj4tq"
def chunk_text(
    text,
    chunk_size=500,
    overlap=50
):

    words = text.split()

    chunks = []

    start = 0

    while start < len(words):

        end = start + chunk_size

        chunk = " ".join(
            words[start:end]
        )

        chunks.append(chunk)

        start += (
            chunk_size - overlap
        )

    return chunks
```

Example:

```python id="6j3m0p"
text = """
Newton's second law describes
the relationship between force,
mass and acceleration.
"""

chunks = chunk_text(
    text,
    chunk_size=10,
    overlap=2
)

for chunk in chunks:
    print(chunk)
```

---

# 11. Chunk Size

এখানে universal perfect number নেই।

Common starting idea:

```text id="t4z0pa"
300–800 tokens
```

এর মতো chunk size দিয়ে experiment করা যায়।

খুব ছোট:

```text id="zj4f7h"
Context হারাতে পারে
```

খুব বড়:

```text id="7j5r6e"
Retrieval কম precise হতে পারে
```

---

# 12. Overlap

ধরো:

```text id="k7s8m2"
Chunk 1:
A B C D E

Chunk 2:
E F G H I
```

`E` overlap।

এতে sentence/concept boundary হারানোর সম্ভাবনা কমে।

---

# 13. Step 3 — Embedding

এখন প্রত্যেক chunk-এর text কে vector-এ convert করব।

```text id="f5m0w2"
Text
 ↓
Embedding Model
 ↓
Vector
```

উদাহরণ:

```text id="8v5d1q"
"Binary search works on sorted data."
```

becomes conceptually:

```text id="n2a0wy"
[0.12, -0.42, 0.77, ...]
```

এই vector-এর dimension model অনুযায়ী পরিবর্তিত হয়।

---

# 14. Semantic Search

User:

> How does binary search reduce the search space?

Knowledge:

```text id="6j8s9a"
Binary search compares the target
with the middle element and eliminates
half of the remaining search space.
```

Keyword exact match না থাকলেও semantic similarity detect করা যায়।

```text id="m5d8q1"
Query Vector
     ↓
Similarity Search
     ↓
Relevant Chunk
```

---

# 15. Cosine Similarity

একটি common similarity measure:

```text id="q9m0g8"
             A · B
cosine = ─────────────
         |A| × |B|
```

Python:

```python id="4l7p3x"
import numpy as np

def cosine_similarity(a, b):

    a = np.array(a)
    b = np.array(b)

    return np.dot(a, b) / (
        np.linalg.norm(a)
        * np.linalg.norm(b)
    )
```

---

# 16. Vector Database

Embeddingগুলো কোথায় রাখব?

একটি vector database ব্যবহার করতে পারি।

Conceptually:

```text id="d9k4v1"
Knowledge Chunk
      ↓
Embedding
      ↓
Vector DB
```

Possible technologies:

```text id="3q6n8w"
FAISS
Chroma
pgvector
Milvus
Qdrant
```

তোমার existing Django/PostgreSQL architecture-এর জন্য **PostgreSQL + pgvector** খুব natural choice হতে পারে।

---

# 17. PostgreSQL + pgvector Architecture

তোমার project:

```text id="r6k4v2"
Django
  ↓
PostgreSQL
  ↓
pgvector
  ↓
Embeddings
```

Knowledge:

```text id="j8f3c0"
Document
 ↓
Chunks
 ↓
Embeddings
 ↓
PostgreSQL + pgvector
```

তারপর:

```text id="s4v9d2"
User Query
 ↓
Embedding
 ↓
pgvector similarity search
 ↓
Relevant chunks
```

---

# 18. Knowledge Record

আমরা metadata-ও রাখব।

```json id="9m7q2w"
{
  "id": "chunk_001",
  "document_id": "newton_laws_001",
  "subject": "Physics",
  "topic": "Newton's Second Law",
  "source": "physics_textbook",
  "page": 42,
  "text": "Newton's second law states...",
  "license": "licensed"
}
```

এটা খুব গুরুত্বপূর্ণ।

কারণ আমরা পরে citation দিতে পারব।

---

# 19. Django Model

Conceptually:

```python id="r8x3k7"
class KnowledgeDocument(models.Model):

    title = models.CharField(
        max_length=255
    )

    subject = models.CharField(
        max_length=100
    )

    source = models.CharField(
        max_length=500
    )

    license = models.CharField(
        max_length=100
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

Chunk:

```python id="c4m9z1"
class KnowledgeChunk(models.Model):

    document = models.ForeignKey(
        KnowledgeDocument,
        on_delete=models.CASCADE
    )

    chunk_index = models.IntegerField()

    text = models.TextField()

    page_number = models.IntegerField(
        null=True,
        blank=True
    )

    metadata = models.JSONField(
        default=dict
    )
```

pgvector ব্যবহার করলে embedding field-ও যোগ করা যাবে।

---

# 20. RAG Retriever Interface

আমরা abstraction রাখব:

```python id="a7k2m9"
from abc import ABC, abstractmethod


class Retriever(ABC):

    @abstractmethod
    def search(
        self,
        query,
        top_k=5
    ):
        pass
```

এতে পরে:

```text id="3j8x4m"
FAISS Retriever
Chroma Retriever
PgVector Retriever
Qdrant Retriever
```

সহজে replace করা যাবে।

---

# 21. Simple Mock Retriever

আগে architecture test করার জন্য:

```python id="v9c1w7"
class MockRetriever:

    def __init__(self, documents):
        self.documents = documents

    def search(
        self,
        query,
        top_k=3
    ):

        return self.documents[:top_k]
```

এটা actual semantic search নয়—pipeline testing-এর জন্য।

---

# 22. Retriever Output

আমরা শুধু text ফেরত দেব না।

বরং:

```json id="j2f8x6"
[
  {
    "text": "Binary search works on sorted data...",
    "score": 0.94,
    "document_id": "algo_001",
    "page": 12,
    "source": "Algorithms Textbook"
  },
  {
    "text": "The middle element is checked first...",
    "score": 0.91,
    "document_id": "algo_001",
    "page": 13,
    "source": "Algorithms Textbook"
  }
]
```

---

# 23. Top-K Retrieval

ধরো:

```text id="3n4x7s"
100,000 chunks
```

User query:

> Explain binary search.

Retriever:

```text id="r8m2c6"
Top 5
 ↓
Most relevant chunks
```

সাধারণত শুরুতে `top_k=3–10` range নিয়ে experiment করা যায়।

---

# 24. Reranking

Similarity search সবসময় perfect নয়।

তাই:

```text id="v6p1r8"
Query
 ↓
Vector Search
 ↓
Top 20
 ↓
Reranker
 ↓
Top 5
 ↓
LLM
```

এটা দুই-stage retrieval।

---

# 25. কেন Reranking দরকার?

ধরো vector search:

```text id="c4h8p0"
1. Binary search definition
2. Linear search
3. Binary tree
4. Binary number
5. Search algorithm
```

Reranker বুঝতে পারে:

```text id="q6m3s9"
Binary search definition
Search algorithm
```

সবচেয়ে relevant।

---

# 26. RAG Prompt

Retrieved knowledge LLM-এর context হিসেবে যাবে।

```python id="z8q2n6"
def build_rag_prompt(
    question,
    contexts
):

    context_text = "\n\n".join(
        context["text"]
        for context in contexts
    )

    return f"""
Answer the educational request
using ONLY the provided context.

Question:
{question}

Context:
{context_text}

Rules:

- Do not invent unsupported facts.
- If the context is insufficient, say so.
- Explain clearly for the target audience.
- Preserve important scientific facts.
- Return structured content when requested.
"""
```

---

# 27. Hallucination Control

এখানে সবচেয়ে গুরুত্বপূর্ণ rule:

```text id="k5n9p2"
Retrieved Evidence
        ↓
LLM
        ↓
Answer
```

LLM-এর instruction:

> If the retrieved evidence does not support a claim, do not invent it.

এতে hallucination কমানো যায়।

তবে:

**RAG hallucination completely eliminate করে না।**

তাই M25-এর evaluation system এখনও দরকার।

---

# 28. RAG + M25

এখন দুই milestone combine হবে:

```text id="n4v7c8"
RAG
 ↓
Generate
 ↓
M25 Evaluation
 ↓
Fact Check
```

অর্থাৎ:

```text id="x1m5q7"
Knowledge
 ↓
LLM
 ↓
Script
 ↓
Evaluation
 ↓
Video
```

---

# 29. Citation System

Educational AI-তে citation খুব useful।

Generated script:

```text id="j7s2m4"
Binary search works on sorted data.
```

Metadata:

```json id="m4k8p1"
{
  "source_id": "algo_001",
  "page": 12
}
```

Final response/video metadata:

```text id="b8r3z0"
Source:
Algorithms Textbook
Page 12
```

---

# 30. Video-এর ভিতরে Citation

Educational video-তে scene-এর bottom বা ending-এ:

```text id="q5m7x1"
Source:
Introduction to Algorithms
Chapter 2
```

অথবা:

```text id="g8n2v6"
Sources
• University lecture notes
• Open textbook
```

এটা subject এবং licensing-এর উপর নির্ভর করে।

---

# 31. Knowledge → Scene JSON

এখন আমাদের existing system-এর সাথে connect করি।

```text id="7j3k9m"
User:
"Explain photosynthesis"
          ↓
       RAG
          ↓
Trusted Knowledge
          ↓
        LLM
          ↓
Learning Objectives
          ↓
Script
          ↓
Scene JSON
```

Example:

```json id="p2v7n4"
{
  "topic": "Photosynthesis",
  "sources": [
    {
      "document_id": "bio_001",
      "page": 15
    }
  ],
  "scenes": [
    {
      "scene_id": 1,
      "narration": "Plants use light energy to drive photosynthesis.",
      "source_chunks": ["chunk_102"],
      "scene_type": "process"
    }
  ]
}
```

---

# 32. Source Tracking

এটা M26-এর advanced feature।

প্রতিটি claim-এর সাথে source রাখবে।

```text id="k1m8r5"
Claim
 ↓
Source Chunk
 ↓
Document
 ↓
Page
```

Example:

```json id="w9p3c6"
{
  "claim": "Binary search requires sorted data.",
  "source_chunks": [
    "algo_chunk_12"
  ],
  "confidence": 0.97
}
```

---

# 33. Claim-Level Verification

আরও advanced:

```text id="4k7m2x"
Generated Script
       ↓
Extract Claims
       ↓
Retrieve Evidence
       ↓
Compare Claim vs Evidence
       ↓
Supported / Unsupported
```

Example:

```text id="z3v6q8"
Claim:
Binary search has O(log n) time complexity.

Evidence:
Textbook says O(log n).

Result:
SUPPORTED
```

---

# 34. Unsupported Claim

```text id="j8n4p6"
Claim:
Binary search always takes exactly 5 comparisons.

Evidence:
No supporting information.

Result:
UNSUPPORTED
```

তখন:

```text id="s7m2k9"
Reject claim
OR
ask LLM to revise
```

---

# 35. Fact Checking Pipeline

এখন খুব powerful architecture:

```text id="r3c7m8"
User Prompt
     ↓
RAG
     ↓
Draft Script
     ↓
Claim Extraction
     ↓
Evidence Retrieval
     ↓
Claim Verification
     ↓
Corrected Script
     ↓
Scene Planner
```

---

# 36. RAG Confidence

প্রতিটি retrieved chunk-এর score থাকতে পারে:

```text id="q8m3v1"
0.95
0.91
0.88
0.54
0.42
```

আমরা threshold রাখতে পারি:

```python id="f2n8c5"
def filter_contexts(
    contexts,
    threshold=0.70
):

    return [
        context
        for context in contexts
        if context["score"] >= threshold
    ]
```

এটা শুধু baseline; real threshold retrieval model ও dataset অনুযায়ী tune করতে হবে।

---

# 37. No Evidence Case

যদি relevant information না পাওয়া যায়:

```text id="j5q7m2"
User Query
   ↓
Retriever
   ↓
No relevant evidence
```

LLM-কে hallucinate করতে দেওয়া যাবে না।

Return:

```text id="m8v3x1"
"I don't have enough trusted information
to confidently explain this topic."
```

অথবা system-এর policy অনুযায়ী broader trusted source search করা যাবে।

---

# 38. RAG-এর সবচেয়ে বড় ভুল

### ভুল ১

```text id="x1k7m9"
PDF
 ↓
LLM
```

এটা RAG নয়।

### ভুল ২

```text id="f8q2m4"
Retrieve random text
 ↓
LLM
```

এটাও যথেষ্ট নয়।

### সঠিক

```text id="g5n8r1"
Trusted Documents
 ↓
Clean
 ↓
Chunk
 ↓
Embedding
 ↓
Vector Search
 ↓
Rerank
 ↓
Evidence
 ↓
LLM
 ↓
Verification
```

---

# 39. RAG বনাম Fine-tuning

এটা M23 এবং M26-এর key difference।

### Fine-tuning

```text id="v8m2k5"
Training Data
 ↓
Model Parameters / Adapter
 ↓
Learn Behavior / Style
```

### RAG

```text id="j4p9x7"
Knowledge
 ↓
Retrieve at runtime
 ↓
LLM
```

---

# 40. কখন RAG?

যখন information:

```text id="r6k2m8"
changes frequently
+
needs citations
+
domain-specific
+
large knowledge base
```

তখন RAG useful।

---

# 41. কখন Fine-tuning?

যখন model-এর behavior/style পরিবর্তন করতে চাও:

```text id="q7m3n5"
Output format
Teaching style
Tone
Structured JSON
Visual style
```

তখন fine-tuning useful।

---

# 42. তোমার Project-এ দুটোই লাগবে

```text id="c9m4x2"
RAG
 ↓
Trusted Knowledge

LoRA
 ↓
Style / Behavior

Together
 ↓
Educational AI
```

অর্থাৎ:

```text id="v7n2k8"
Knowledge → RAG
Behavior → LoRA
```

---

# 43. M26 + M23

Final architecture:

```text id="p6k3m8"
                 Base LLM
                    +
              Educational LoRA
                    ↓
User Prompt → RAG → LLM
                    ↓
             Verified Script
                    ↓
                Scene JSON
```

---

# 44. RAG + VLM

শুধু text knowledge নয়।

কখনও knowledge source-এ image/diagram থাকতে পারে।

```text id="x8m4q1"
PDF
 ├── Text
 └── Images
      ↓
     VLM
```

তারপর:

```text id="k2p7v9"
Text Evidence
+
Visual Evidence
 ↓
Multimodal LLM
```

এটা তোমার Educational Video AI-এর জন্য future advanced feature।

---

# 45. RAG + Image Generation

ধরো source বলছে:

> Photosynthesis occurs primarily in chloroplasts.

LLM:

```text id="z4n8c2"
Create scene:
plant cell
+
chloroplast
+
sunlight
```

তারপর:

```text id="r7m3k9"
Scene JSON
 ↓
Visual Planner
 ↓
Image LoRA / Manim
```

অর্থাৎ trusted knowledge → correct visual plan।

---

# 46. RAG + M25 + M24

এখন তোমার system আরও powerful:

```text id="u5k8r3"
                USER
                  ↓
                 RAG
                  ↓
          Trusted Knowledge
                  ↓
          Educational LLM
                  ↓
        Educational LoRA
                  ↓
             Scene JSON
                  ↓
       ┌──────────┼──────────┐
       ↓          ↓          ↓
     Manim     Image LoRA   Video
       └──────────┼──────────┘
                  ↓
                 VLM
                  ↓
             M25 Evaluation
                  ↓
        PASS / REVIEW / FAIL
                  ↓
               TTS
                  ↓
             Subtitle
                  ↓
              FFmpeg
                  ↓
            FINAL VIDEO
```

---

# 47. RAG Service

Project structure:

```text id="j8v3m2"
educational_video_ai/
│
├── rag/
│   ├── __init__.py
│   ├── ingestion.py
│   ├── loader.py
│   ├── cleaner.py
│   ├── chunker.py
│   ├── embeddings.py
│   ├── retriever.py
│   ├── reranker.py
│   ├── prompt.py
│   ├── citation.py
│   ├── verifier.py
│   └── service.py
│
├── knowledge/
│
├── evaluation/
│
├── planner/
│
├── image/
│
└── ...
```

---

# 48. RAG Service Class

```python id="q7m2v9"
class RAGService:

    def __init__(
        self,
        retriever,
        llm
    ):

        self.retriever = retriever
        self.llm = llm

    def answer(
        self,
        query
    ):

        contexts = self.retriever.search(
            query,
            top_k=5
        )

        contexts = filter_contexts(
            contexts
        )

        prompt = build_rag_prompt(
            query,
            contexts
        )

        return self.llm.generate(
            prompt
        )
```

এটা basic version।

Production version-এ reranking, citation, verification, confidence, source tracking যোগ হবে।

---

# 49. Educational RAG Service

আমাদের project-specific version:

```python id="c4n8x2"
class EducationalRAGService:

    def __init__(
        self,
        retriever,
        reranker,
        llm,
        verifier
    ):

        self.retriever = retriever
        self.reranker = reranker
        self.llm = llm
        self.verifier = verifier

    def generate_content(
        self,
        query
    ):

        contexts = self.retriever.search(
            query,
            top_k=20
        )

        contexts = self.reranker.rank(
            query,
            contexts
        )

        contexts = contexts[:5]

        prompt = build_rag_prompt(
            query,
            contexts
        )

        draft = self.llm.generate(
            prompt
        )

        verified = self.verifier.verify(
            draft,
            contexts
        )

        return verified
```

---

# 50. RAG Output

আমরা plain text না দিয়ে structured output রাখব:

```json id="h7m2q4"
{
  "answer": "Binary search works on sorted data...",
  "sources": [
    {
      "document_id": "algo_001",
      "page": 12
    }
  ],
  "claims": [
    {
      "text": "Binary search requires sorted data.",
      "supported": true,
      "source": "algo_001"
    }
  ]
}
```

এটা পরে Scene Planner-এ যাবে।

---

# 51. Knowledge Versioning

Knowledge base পরিবর্তন হতে পারে।

তাই:

```json id="n3q8v6"
{
  "knowledge_version": "1.0.0",
  "document_id": "physics_001",
  "updated_at": "2026-09-06"
}
```

রাখা ভালো।

---

# 52. Source Provenance

প্রতিটি content-এর lineage:

```text id="k6m2p9"
Final Video
 ↓
Scene
 ↓
Narration
 ↓
Claim
 ↓
Knowledge Chunk
 ↓
Document
 ↓
Source
```

এটাকে বলা যায়:

**Content provenance**

এটা educational system-এর জন্য অত্যন্ত valuable।

---

# 53. M26 Mini Project 🎯

তোমার practical project:

## **Trusted Educational Knowledge Assistant**

Input:

```text id="p8v3m1"
"Explain binary search to a beginner."
```

Knowledge base:

```text id="m4q7x2"
Algorithms textbook
+
trusted CS notes
```

Pipeline:

```text id="n7k2v5"
User Question
      ↓
Embedding
      ↓
Vector Search
      ↓
Top 5 chunks
      ↓
Reranking
      ↓
LLM
      ↓
Structured Answer
      ↓
Citation
      ↓
Fact Verification
```

Output:

```json id="x5m8q3"
{
  "topic": "Binary Search",
  "explanation": "...",
  "learning_objectives": [
    "Understand sorted data",
    "Understand middle element",
    "Understand half elimination"
  ],
  "sources": [
    {
      "document": "Algorithms Textbook",
      "page": 12
    }
  ],
  "verified": true
}
```

---

# 54. M26 → Video Generation

Mini project complete হলে:

```text id="f8q2m6"
User
 ↓
RAG
 ↓
Verified Content
 ↓
Scene Planner
 ↓
Visual Planner
 ↓
Manim / Image LoRA
 ↓
TTS
 ↓
Subtitle
 ↓
FFmpeg
 ↓
Video
 ↓
M25 Evaluation
```

এখন তোমার system **knowledge-grounded educational video generator** হতে শুরু করবে।

---

# 55. M26 Completion Checklist

M26 complete হলে তোমার জানা উচিত:

* [ ] RAG কী
* [ ] Retrieval কী
* [ ] Knowledge base কী
* [ ] Document ingestion
* [ ] Chunking
* [ ] Chunk overlap
* [ ] Embedding
* [ ] Semantic search
* [ ] Cosine similarity
* [ ] Vector database
* [ ] pgvector
* [ ] Top-K retrieval
* [ ] Reranking
* [ ] RAG prompt
* [ ] Citation
* [ ] Source provenance
* [ ] Claim verification
* [ ] Hallucination control
* [ ] RAG vs Fine-tuning
* [ ] RAG + LoRA
* [ ] RAG + VLM
* [ ] RAG + M25 Evaluation
* [ ] Knowledge versioning

---

# 🔥 M26-এর Golden Architecture

এটা মনে রাখবে:

```text id="a7m3q8"
       TRUSTED KNOWLEDGE
              ↓
          CHUNKING
              ↓
          EMBEDDING
              ↓
        VECTOR DATABASE
              ↓
           RETRIEVAL
              ↓
          RERANKING
              ↓
           EVIDENCE
              ↓
             LLM
              ↓
       CLAIM VERIFICATION
              ↓
        EDUCATIONAL SCRIPT
              ↓
          SCENE JSON
              ↓
      VISUAL + AUDIO + VIDEO
              ↓
        M25 EVALUATION
              ↓
         FINAL VIDEO
```

### এখন তোমার AI system-এর intelligence তিন জায়গায় ভাগ হয়েছে:

```text
RAG       → "What facts should I use?"
LLM/LoRA  → "How should I teach them?"
Renderer  → "How should I show them?"
VLM       → "Did I show them correctly?"
Evaluator → "Is the final result good enough?"
```

এটাই তোমার project-কে সাধারণ **AI video generator** থেকে একটি **knowledge-grounded educational video generation system**-এ নিয়ে যাচ্ছে।

**Next: M27 — GPU Optimization** → এখানে আমরা GPU/VRAM, CUDA, mixed precision, quantization, batching, memory optimization, inference speed, model loading এবং তোমার নিজের PC বনাম cloud GPU-তে কোন workload চালানো উচিত—এসব নিয়ে practical architecture তৈরি করব।

---
# M27 — GPU Optimization for AI Educational Video Generator 🚀

M26 পর্যন্ত আমরা **RAG + Trusted Knowledge** তৈরি করেছি। এখন M27-এর লক্ষ্য হলো তোমার পুরো AI video pipeline-কে **GPU-efficient, faster এবং production-ready** করা।

আমাদের target:

```text
M26
RAG + LLM + VLM + Image/Video Generation
              ↓
             M27
        GPU Optimization
              ↓
 Faster + Less VRAM + Better Throughput
```

---

# 1. M27 কী শিখবে?

এই milestone-এ আমরা শিখব:

1. GPU কীভাবে কাজ করে
    
2. CPU vs GPU
    
3. CUDA
    
4. VRAM
    
5. PyTorch GPU detection
    
6. Model → GPU
    
7. Tensor → GPU
    
8. `torch.no_grad()`
    
9. `torch.inference_mode()`
    
10. FP32 vs FP16 vs BF16
    
11. Mixed Precision
    
12. Quantization
    
13. 8-bit / 4-bit inference
    
14. Gradient Accumulation
    
15. Gradient Checkpointing
    
16. Batch Size optimization
    
17. Memory monitoring
    
18. `torch.cuda.empty_cache()`
    
19. CPU/GPU data transfer
    
20. `pin_memory`
    
21. `non_blocking`
    
22. Model loading optimization
    
23. VLM optimization
    
24. Image generation optimization
    
25. Video generation optimization
    
26. GPU worker architecture
    
27. OOM handling
    
28. GPU benchmark
    
29. Complete optimization pipeline
    

---

# 2. কেন M27 দরকার?

তোমার system এখন:

```text
User
 ↓
RAG
 ↓
LLM
 ↓
Scene Planner
 ↓
VLM
 ↓
Image Generation
 ↓
Video Generation
 ↓
TTS
 ↓
Whisper
 ↓
Manim
 ↓
FFmpeg
```

এখানে অনেক কাজ GPU-intensive:

```text
LLM             → GPU
VLM             → GPU
Whisper         → GPU
Image Model     → GPU
Video Model     → GPU
LoRA Training   → GPU
```

GPU ঠিকভাবে ব্যবহার না করলে:

```text
Slow generation
       +
High VRAM usage
       +
CUDA OOM
       +
Low throughput
```

---

# 3. CPU vs GPU

### CPU

CPU সাধারণত:

```text
Few powerful cores
        ↓
Sequential/general tasks
```

উদাহরণ:

```python
json parsing
database
file management
FFmpeg
API
```

### GPU

GPU:

```text
Thousands of parallel cores
        ↓
Matrix operations
        ↓
Deep Learning
```

উদাহরণ:

```text
LLM
CNN
VLM
Diffusion
Video generation
```

---

# 4. CUDA কী?

NVIDIA GPU ব্যবহার করার জন্য সাধারণত:

```text
Python
 ↓
PyTorch
 ↓
CUDA
 ↓
NVIDIA GPU
```

উদাহরণ:

```python
import torch

print(torch.cuda.is_available())
```

যদি:

```text
True
```

তাহলে PyTorch CUDA GPU detect করেছে।

---

# 5. GPU Information

```python
import torch

if torch.cuda.is_available():

    print("GPU:", torch.cuda.get_device_name(0))

    print(
        "VRAM:",
        torch.cuda.get_device_properties(0).total_memory / 1024**3,
        "GB"
    )

else:
    print("CUDA GPU not available")
```

Example:

```text
GPU: NVIDIA GeForce RTX ...
VRAM: 12.0 GB
```

---

# 6. Device abstraction

আমাদের code-এ কখনো hardcode করা উচিত না:

```python
device = "cuda"
```

বরং:

```python
import torch

device = (
    "cuda"
    if torch.cuda.is_available()
    else "cpu"
)

print(device)
```

এখন:

```text
GPU থাকলে → CUDA
GPU না থাকলে → CPU
```

---

# 7. Tensor GPU-তে পাঠানো

CPU tensor:

```python
import torch

x = torch.tensor([1, 2, 3])

print(x.device)
```

Output:

```text
cpu
```

GPU:

```python
x = x.to("cuda")

print(x.device)
```

Output:

```text
cuda:0
```

---

# 8. Model GPU-তে পাঠানো

```python
model = model.to(device)
```

সম্পূর্ণ pattern:

```python
import torch

device = "cuda" if torch.cuda.is_available() else "cpu"

model = model.to(device)

x = x.to(device)

output = model(x)
```

খুব গুরুত্বপূর্ণ:

```text
Model → GPU
Input → GPU
```

দুটো একই device-এ থাকতে হবে।

---

# 9. CPU-GPU mismatch

এই error খুব common:

```text
Expected all tensors to be on the same device
```

কারণ:

```text
Model → CUDA
Input → CPU
```

সঠিক:

```python
model = model.to(device)
x = x.to(device)

output = model(x)
```

---

# 10. `no_grad()`

Inference করার সময় gradient দরকার নেই।

তাই:

```python
with torch.no_grad():
    output = model(x)
```

এতে memory কমে।

---

# 11. `inference_mode()`

Inference-এর জন্য আরও optimized:

```python
with torch.inference_mode():
    output = model(x)
```

তোমার inference pipeline-এ এটা ব্যবহার করতে পারো।

Example:

```python
def predict(model, x):

    model.eval()

    with torch.inference_mode():

        x = x.to(device)

        output = model(x)

    return output
```

---

# 12. `model.eval()`

Training:

```python
model.train()
```

Inference:

```python
model.eval()
```

Production AI video generation-এ inference করার সময়:

```python
model.eval()

with torch.inference_mode():
    output = model(x)
```

---

# 13. FP32

সাধারণভাবে neural network ব্যবহার করতে পারে:

```text
FP32
```

একটি floating point value:

```text
32 bits
```

Memory বেশি লাগে।

---

# 14. FP16

FP16:

```text
16 bits
```

অর্থাৎ FP32-এর তুলনায় কম memory।

Conceptually:

```text
FP32
 ↓
FP16
 ↓
Less VRAM
+
Often faster inference
```

---

# 15. Mixed Precision

সব calculation FP16 করার দরকার নেই।

কিছু operation:

```text
FP16
```

আর কিছু:

```text
FP32
```

এটাই:

**Mixed Precision**

PyTorch example:

```python
with torch.autocast(
    device_type="cuda",
    dtype=torch.float16
):
    output = model(x)
```

---

# 16. BF16

Modern NVIDIA GPUs-তে BF16 খুব useful।

```python
dtype = torch.bfloat16
```

তবে GPU support model এবং hardware অনুযায়ী check করতে হবে।

General idea:

```text
FP32 → highest precision
FP16 → lower memory
BF16 → good numerical range + lower memory
```

---

# 17. Quantization

আরেকটি powerful optimization:

```text
FP32
 ↓
FP16
 ↓
INT8
 ↓
INT4
```

এতে model memory অনেক কমানো যায়।

---

# 18. Example

ধরো model parameters-এর জন্য আনুমানিক:

```text
FP32 → 4 bytes/parameter
FP16 → 2 bytes/parameter
INT8 → 1 byte/parameter
INT4 → 0.5 byte/parameter
```

তাই large LLM-এর ক্ষেত্রে:

```text
FP32
  ↓
Huge VRAM

INT4
  ↓
Much lower VRAM
```

তবে quantization-এর trade-off আছে:

```text
Memory ↓
Speed may ↑
Quality may slightly ↓
```

---

# 19. LLM Quantization

Hugging Face ecosystem-এ 4-bit/8-bit loading-এর জন্য `bitsandbytes` ব্যবহার করা যায়।

Concept:

```python
from transformers import BitsAndBytesConfig

quant_config = BitsAndBytesConfig(
    load_in_4bit=True
)
```

তারপর model loading:

```python
model = AutoModelForCausalLM.from_pretrained(
    MODEL_NAME,
    quantization_config=quant_config,
    device_map="auto"
)
```

**Note:** exact arguments model/library version অনুযায়ী পরিবর্তিত হতে পারে।

---

# 20. `device_map="auto"`

Large model-এর ক্ষেত্রে:

```python
device_map="auto"
```

ব্যবহার করলে framework available hardware অনুযায়ী model placement করতে পারে।

Concept:

```text
Large Model
     ↓
device_map="auto"
     ↓
Available GPU / CPU
```

---

# 21. VRAM Monitoring

সবচেয়ে important commands:

```python
import torch

print(
    "Allocated:",
    torch.cuda.memory_allocated() / 1024**3,
    "GB"
)

print(
    "Reserved:",
    torch.cuda.memory_reserved() / 1024**3,
    "GB"
)
```

আরও useful:

```python
print(torch.cuda.memory_summary())
```

---

# 22. `empty_cache()`

কখনো unused cached memory release করতে:

```python
torch.cuda.empty_cache()
```

কিন্তু মনে রাখবে:

> `empty_cache()` model-এর actual allocated tensors delete করে না।

তাই এটাকে magic solution ভাববে না।

---

# 23. GPU Memory Flow

```text
Model
 ↓
VRAM
 ↓
Input Tensor
 ↓
VRAM
 ↓
Intermediate Activations
 ↓
VRAM
 ↓
Output
```

Training-এ আরও লাগে:

```text
Parameters
+
Gradients
+
Optimizer states
+
Activations
```

তাই training-এর memory requirement inference-এর চেয়ে অনেক বেশি হতে পারে।

---

# 24. Batch Size

ধরো:

```python
batch_size = 1
```

VRAM কম।

```python
batch_size = 8
```

VRAM বেশি।

Relationship:

```text
Batch Size ↑
     ↓
VRAM ↑
     ↓
Throughput may ↑
```

কিন্তু GPU memory limit আছে।

---

# 25. CUDA Out Of Memory

Common error:

```text
CUDA out of memory
```

প্রথমে:

```text
Batch Size ↓
```

তারপর:

```text
Resolution ↓
```

তারপর:

```text
FP16/BF16
```

তারপর:

```text
Quantization
```

তারপর:

```text
Gradient Checkpointing
```

Training হলে:

```text
Gradient Accumulation
```

---

# 26. Gradient Accumulation

ধরো GPU-তে:

```text
batch_size = 1
```

কিন্তু তুমি effective batch চাই:

```text
8
```

তাহলে:

```python
gradient_accumulation_steps = 8
```

Concept:

```text
Batch 1
 ↓
Gradient

Batch 2
 ↓
Gradient

...

Batch 8
 ↓
Update Model
```

Effective batch size:

```text
1 × 8 = 8
```

---

# 27. Gradient Checkpointing

Training-এর সময় intermediate activation সব store না করে কিছু recompute করা হয়।

```text
Normal Training
Memory ↑
Speed ↑

Checkpointing
Memory ↓
Computation ↑
```

Large LLM/VLM fine-tuning-এ খুব useful।

Concept:

```python
model.gradient_checkpointing_enable()
```

---

# 28. CPU → GPU Transfer

ধরো:

```python
x = x.to("cuda")
```

CPU থেকে GPU-তে data copy হয়।

এটা expensive হতে পারে।

তাই data pipeline optimize করতে হবে।

---

# 29. DataLoader Optimization

```python
loader = DataLoader(
    dataset,
    batch_size=8,
    pin_memory=True
)
```

তারপর:

```python
x = x.to(
    device,
    non_blocking=True
)
```

Concept:

```text
CPU RAM
 ↓
Pinned Memory
 ↓
GPU VRAM
```

Large training pipeline-এ useful।

---

# 30. GPU Optimization Strategy

তোমার Educational Video AI-তে আমরা optimization করব আলাদা আলাদা layer-এ।

```text
                GPU Optimization
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
      LLM             VLM          Diffusion
       │               │               │
    Quantization    FP16/BF16      FP16
    KV Cache        Batch          VAE optimization
       │               │               │
       └───────────────┼───────────────┘
                       ↓
                  GPU Scheduler
```

---

# 31. LLM Optimization

তোমার planner:

```text
RAG
 ↓
LLM
 ↓
Scene JSON
```

Optimization:

```text
LLM
 ↓
4-bit / 8-bit
 ↓
GPU
 ↓
Inference Mode
```

---

# 32. VLM Optimization

VLM:

```text
Frame
 ↓
Vision Encoder
 ↓
LLM
 ↓
Visual Understanding
```

Optimization:

```text
Frame sampling
+
Batch inference
+
FP16/BF16
+
Inference mode
```

সব frame GPU-তে পাঠাবে না।

ভুল:

```text
30 FPS
×
60 seconds
=
1800 frames
```

Better:

```text
1–2 frames/sec
```

তারপর candidate frames only।

---

# 33. Image Generation Optimization

Image generation সাধারণত:

```text
Prompt
 ↓
Diffusion
 ↓
Image
```

Optimization:

```text
FP16
+
Lower resolution during development
+
Efficient scheduler
+
Batch generation when appropriate
+
Model reuse
```

Development:

```text
512×512
```

Final:

```text
1280×720
```

এভাবে শুরু করলে development দ্রুত হয়।

---

# 34. Video Generation Optimization

Video generation সবচেয়ে expensive অংশগুলোর একটি।

তাই:

```text
60 sec video
```

একবারে generate না করে:

```text
Scene 1 → 5 sec
Scene 2 → 5 sec
Scene 3 → 5 sec
...
```

Architecture:

```text
60 sec
 ↓
12 × 5 sec
 ↓
Generate separately
 ↓
Evaluate
 ↓
Compose
```

এতে failed scene regenerate করা যায়।

---

# 35. GPU Worker Architecture

M28-এ আমরা Celery/Redis করব। কিন্তু M27 থেকেই architecture ঠিক করব।

```text
Django API
     ↓
Job
     ↓
GPU Worker
     ↓
Model
     ↓
Generate
     ↓
Output
```

GPU worker-এর মধ্যে model বারবার load করা যাবে না।

❌ Bad:

```text
Request
 ↓
Load model
 ↓
Generate
 ↓
Delete model

Request
 ↓
Load model
 ↓
Generate
```

এতে huge overhead।

---

# 36. Better

Worker startup:

```text
GPU Worker Starts
       ↓
Load Model
       ↓
Keep Model in VRAM
       ↓
Request 1
       ↓
Generate
       ↓
Request 2
       ↓
Generate
       ↓
Request 3
       ↓
Generate
```

এটাই production architecture-এর জন্য গুরুত্বপূর্ণ।

---

# 37. Model Manager

আমরা একটা abstraction তৈরি করতে পারি:

```python
class GPUModelManager:

    def __init__(self):
        self.models = {}

    def load(self, name, loader):
        if name not in self.models:
            self.models[name] = loader()

        return self.models[name]

    def get(self, name):
        return self.models.get(name)

    def unload(self, name):
        if name in self.models:
            del self.models[name]

            import torch
            torch.cuda.empty_cache()
```

ব্যবহার:

```python
manager = GPUModelManager()

model = manager.load(
    "planner",
    load_planner_model
)
```

পরের request-এ:

```python
model = manager.get("planner")
```

নতুন করে model load হবে না।

---

# 38. GPU Resource Manager

আরও advanced:

```python
class GPUResourceManager:

    def __init__(self):
        self.device = self.detect_device()

    def detect_device(self):

        if torch.cuda.is_available():
            return torch.device("cuda")

        return torch.device("cpu")

    def memory(self):

        if self.device.type != "cuda":
            return None

        return {
            "allocated": torch.cuda.memory_allocated(),
            "reserved": torch.cuda.memory_reserved(),
            "total": torch.cuda.get_device_properties(
                0
            ).total_memory
        }
```

---

# 39. Benchmark System

Optimization করলে measure করতে হবে।

শুধু:

> “মনে হচ্ছে faster”

এটা acceptable না।

Measure:

```text
Latency
VRAM
Throughput
Quality
```

---

# 40. Benchmark Decorator

```python
import time
import torch

def benchmark(func):

    def wrapper(*args, **kwargs):

        if torch.cuda.is_available():
            torch.cuda.synchronize()

        start = time.perf_counter()

        result = func(*args, **kwargs)

        if torch.cuda.is_available():
            torch.cuda.synchronize()

        end = time.perf_counter()

        print(
            f"{func.__name__}: "
            f"{end - start:.3f}s"
        )

        return result

    return wrapper
```

ব্যবহার:

```python
@benchmark
def generate_scene(model, input_data):

    with torch.inference_mode():

        return model(input_data)
```

---

# 41. Why `torch.cuda.synchronize()`?

GPU asynchronous ভাবে কাজ করতে পারে।

তাই:

```python
start = time.perf_counter()

output = model(x)

end = time.perf_counter()
```

সবসময় accurate GPU timing নাও দিতে পারে।

তাই:

```python
torch.cuda.synchronize()
```

দিয়ে GPU operation শেষ হওয়া নিশ্চিত করা হয়।

---

# 42. M27 Final Architecture

এখন তোমার complete system:

```text
                         USER
                           ↓
                      Django API
                           ↓
                         RAG
                           ↓
                    Educational LLM
                           ↓
                      Scene JSON
                           ↓
                ┌──────────┼──────────┐
                ↓          ↓          ↓
              Manim      VLM       Diffusion
                ↓          ↓          ↓
             CPU/GPU      GPU        GPU
                │          │          │
                └──────────┼──────────┘
                           ↓
                         TTS
                           ↓
                       Whisper
                           ↓
                       Subtitle
                           ↓
                        FFmpeg
                           ↓
                      Final MP4
```

GPU layer:

```text
                GPU RESOURCE MANAGER
                        │
        ┌───────────────┼────────────────┐
        ↓               ↓                ↓
       LLM             VLM          Diffusion
        ↓               ↓                ↓
   Quantization      FP16/BF16      FP16/BF16
        ↓               ↓                ↓
   Inference Mode    Batch          Memory Control
```

---

# 43. Recommended Optimization Order

তোমার project-এ আমি এই order follow করব:

### Level 1 — Basic GPU

```text
CUDA
 ↓
Device
 ↓
Model.to(device)
 ↓
Tensor.to(device)
```

### Level 2 — Inference

```text
eval()
 ↓
inference_mode()
```

### Level 3 — Precision

```text
FP32
 ↓
FP16/BF16
```

### Level 4 — Memory

```text
Batch Size
 ↓
Quantization
 ↓
Checkpointing
```

### Level 5 — Data

```text
pin_memory
 ↓
non_blocking
 ↓
Prefetch
```

### Level 6 — Architecture

```text
Persistent GPU Worker
 ↓
Model Manager
 ↓
GPU Queue
```

### Level 7 — Measurement

```text
Latency
+
VRAM
+
Throughput
+
Quality
```

---

# 44. M27 Mini Project

এখন তোমার practice project:

## GPU Inference Benchmark

Create:

```text
gpu_optimization/
│
├── device.py
├── memory.py
├── benchmark.py
├── inference.py
├── model_manager.py
└── main.py
```

### `device.py`

```python
import torch


def get_device():

    if torch.cuda.is_available():
        return torch.device("cuda")

    return torch.device("cpu")


def get_device_name():

    if torch.cuda.is_available():
        return torch.cuda.get_device_name(0)

    return "CPU"
```

---

### `memory.py`

```python
import torch


def get_gpu_memory():

    if not torch.cuda.is_available():
        return None

    return {
        "allocated_gb":
            torch.cuda.memory_allocated() / 1024**3,

        "reserved_gb":
            torch.cuda.memory_reserved() / 1024**3,

        "total_gb":
            torch.cuda.get_device_properties(
                0
            ).total_memory / 1024**3
    }
```

---

### `benchmark.py`

```python
import time
import torch


def benchmark(func, *args, **kwargs):

    if torch.cuda.is_available():
        torch.cuda.synchronize()

    start = time.perf_counter()

    result = func(*args, **kwargs)

    if torch.cuda.is_available():
        torch.cuda.synchronize()

    end = time.perf_counter()

    return result, end - start
```

---

### `inference.py`

```python
import torch


def run_inference(model, x, device):

    model.eval()

    x = x.to(device)

    with torch.inference_mode():

        output = model(x)

    return output
```

---

### `main.py`

```python
from device import get_device, get_device_name
from memory import get_gpu_memory


def main():

    device = get_device()

    print("Device:", device)

    print(
        "Device Name:",
        get_device_name()
    )

    print(
        "Memory:",
        get_gpu_memory()
    )


if __name__ == "__main__":
    main()
```

Run:

```bash
python main.py
```

---

# 45. M27 Completion Checklist

M27 complete হবে যখন তুমি নিজে explain করতে পারবে:

### GPU Basics

-  CPU vs GPU
    
-  CUDA
    
-  VRAM
    
-  CUDA device
    
-  GPU detection
    

### PyTorch

-  `torch.cuda.is_available()`
    
-  `.to(device)`
    
-  `model.eval()`
    
-  `torch.no_grad()`
    
-  `torch.inference_mode()`
    

### Precision

-  FP32
    
-  FP16
    
-  BF16
    
-  Mixed precision
    

### Memory

-  Batch size
    
-  Quantization
    
-  INT8
    
-  INT4
    
-  Gradient accumulation
    
-  Gradient checkpointing
    
-  CUDA OOM
    
-  `empty_cache()`
    

### Performance

-  `pin_memory`
    
-  `non_blocking`
    
-  GPU synchronization
    
-  Benchmarking
    
-  Latency
    
-  Throughput
    

### AI Video System

-  LLM GPU optimization
    
-  VLM optimization
    
-  Image generation optimization
    
-  Video generation optimization
    
-  Persistent GPU model
    
-  GPU Model Manager
    

---

# 46. M27-এর সবচেয়ে গুরুত্বপূর্ণ ধারণা

এই architecture-টা মনে রাখো:

```text
                 EDUCATIONAL VIDEO AI
                         │
                         ▼
                ┌─────────────────┐
                │   GPU Manager   │
                └────────┬────────┘
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
         LLM            VLM         Generation
          │              │              │
       Quantized       FP16/BF16      FP16/BF16
          │              │              │
          └──────────────┼──────────────┘
                         ↓
                  Inference Mode
                         ↓
                    GPU Memory
                         ↓
                     Output
```

**M27-এর golden rule:**

> **GPU শুধু ব্যবহার করলেই হবে না—VRAM, precision, batching, data transfer, model lifetime এবং inference latency—সবকিছু একসাথে optimize করতে হবে।**

এর পরের **M28 = Celery + Redis Distributed AI Pipeline**, যেখানে আমরা এই GPU-optimized components-গুলোকে **Django API → Redis Queue → CPU/GPU Workers → Job Status → Final Video** architecture-এ বসাব।

---
# M28 — Celery + Redis Distributed AI Pipeline 🚀

M27-তে আমরা **GPU Optimization** শিখেছি। এখন M28-তে সেই GPU-optimized AI components-গুলোকে একটি **asynchronous distributed pipeline**-এ বসাব।

এটা তোমার project-এর জন্য খুব গুরুত্বপূর্ণ, কারণ video generation একটি long-running কাজ। User request পাঠানোর পর Django server-কে 2–10 মিনিট আটকে রাখা যাবে না।

---

# 1. M28-এর মূল লক্ষ্য

আমরা এই architecture বানাব:

```text
User
 ↓
React
 ↓
Django API
 ↓
Create Video Job
 ↓
Redis Queue
 ↓
Celery Worker
 ↓
AI Pipeline
 ├── RAG
 ├── LLM
 ├── VLM
 ├── Image/Video Generation
 ├── TTS
 ├── Subtitle
 └── FFmpeg
 ↓
Final MP4
 ↓
Storage
 ↓
Job Status
 ↓
React
```

অর্থাৎ:

> **Django request গ্রহণ করবে, Celery background-এ কাজ করবে, Redis task queue হিসেবে কাজ করবে।**

---

# 2. কেন Celery দরকার?

ধরো user লিখল:

```text
Explain photosynthesis in 60 seconds.
```

Video generate করতে লাগতে পারে:

```text
LLM              5 sec
VLM             10 sec
Image generation 30 sec
TTS              10 sec
Rendering        20 sec
FFmpeg            5 sec
-----------------------
Total            80 sec
```

যদি Django সরাসরি সব কাজ করে:

```text
POST /generate
       ↓
Django
       ↓
80 seconds অপেক্ষা
       ↓
Response
```

এটা খারাপ architecture।

---

# 3. Celery ব্যবহার করলে

```text
POST /generate
       ↓
Django
       ↓
Create Job
       ↓
Redis
       ↓
Immediately response
```

Response:

```json
{
    "project_id": "abc123",
    "status": "queued"
}
```

তারপর:

```text
Celery Worker
      ↓
Generate Video
      ↓
completed
```

---

# 4. Redis কী?

Redis একটি খুব fast in-memory data store।

Celery-এর সাথে Redis ব্যবহার করে আমরা:

```text
Django
   ↓
Redis
   ↓
Celery Worker
```

করতে পারি।

Redis এখানে:

> **Message Broker / Queue**

হিসেবে কাজ করবে।

---

# 5. Celery কী?

Celery হলো distributed task queue system।

সহজভাবে:

```text
Django = Boss
Redis = Queue
Celery = Worker
```

উদাহরণ:

```text
Django:
"এই videoটা generate করো"

Redis:
"ঠিক আছে, job queue-তে রাখলাম"

Celery:
"আমি jobটা করছি"
```

---

# 6. M28 Architecture

```text
                  React
                    │
                    ▼
              Django REST API
                    │
                    ▼
              PostgreSQL
                    │
                    │ Job
                    ▼
                 Redis
                    │
             ┌──────┴──────┐
             ▼             ▼
        CPU Worker      GPU Worker
             │             │
             │             ├── LLM
             │             ├── VLM
             │             ├── Image
             │             └── Video
             │
             ├── FFmpeg
             ├── File handling
             └── Validation
                    │
                    ▼
               Final Video
```

---

# 7. M28-এ আমরা কী শিখব?

এই milestone-এ:

1. Background Task
2. Celery
3. Redis
4. Broker
5. Worker
6. Task
7. Task ID
8. Async Processing
9. Task States
10. Retry
11. Failure Handling
12. Time Limit
13. Task Queue
14. Multiple Workers
15. CPU Worker
16. GPU Worker
17. Queue Routing
18. Priority
19. Database Job Tracking
20. Progress Tracking
21. Django + Celery
22. React Job Polling
23. GPU Worker Architecture
24. Complete Video Generation Queue

---

# 8. Installation

Ubuntu:

```bash
sudo apt update
sudo apt install redis-server
```

Check:

```bash
redis-server --version
```

Redis start:

```bash
sudo systemctl start redis
```

Enable:

```bash
sudo systemctl enable redis
```

Check:

```bash
redis-cli ping
```

Expected:

```text
PONG
```

Python packages:

```bash
pip install celery redis
```

Django:

```bash
pip install django djangorestframework
```

---

# 9. Project Structure

M28-এ project structure হবে:

```text
educational_video_ai/
│
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── celery.py
│   └── wsgi.py
│
├── videos/
│   ├── __init__.py
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│   ├── urls.py
│   ├── tasks.py
│   └── services.py
│
├── planner/
├── rag/
├── vlm/
├── image/
├── video_generation/
├── tts/
├── subtitle/
├── renderer/
├── timeline/
├── composer/
│
├── workers/
│   ├── cpu_tasks.py
│   └── gpu_tasks.py
│
└── requirements.txt
```

---

# 10. Celery Configuration

`config/celery.py`

```python
import os

from celery import Celery


os.environ.setdefault(
    "DJANGO_SETTINGS_MODULE",
    "config.settings"
)


app = Celery(
    "educational_video_ai"
)


app.config_from_object(
    "django.conf:settings",
    namespace="CELERY"
)


app.autodiscover_tasks()
```

---

# 11. `config/__init__.py`

```python
from .celery import app as celery_app

__all__ = ("celery_app",)
```

এর ফলে Django project শুরু হলে Celery configuration load হবে।

---

# 12. Django Settings

`settings.py`:

```python
CELERY_BROKER_URL = "redis://localhost:6379/0"

CELERY_RESULT_BACKEND = "redis://localhost:6379/1"

CELERY_ACCEPT_CONTENT = ["json"]

CELERY_TASK_SERIALIZER = "json"

CELERY_RESULT_SERIALIZER = "json"

CELERY_TIMEZONE = "Asia/Dhaka"
```

এখানে:

```text
6379 = Redis port
0    = broker database
1    = result database
```

---

# 13. প্রথম Celery Task

`videos/tasks.py`

```python
from celery import shared_task


@shared_task
def hello_task(name):

    return f"Hello {name}"
```

এখন Celery worker start:

```bash
celery -A config worker --loglevel=info
```

অন্য terminal থেকে Django shell:

```bash
python manage.py shell
```

তারপর:

```python
from videos.tasks import hello_task

result = hello_task.delay("Atiar")
```

`delay()` task queue-তে পাঠায়।

---

# 14. Task ID

```python
result.id
```

Example:

```text
8d7c9b...
```

এই ID দিয়ে task track করা যায়।

```python
result.status
```

Possible:

```text
PENDING
STARTED
SUCCESS
FAILURE
RETRY
```

---

# 15. `.delay()` কী করছে?

এই:

```python
hello_task.delay("Atiar")
```

প্রায় equivalent:

```text
Python
 ↓
Celery
 ↓
Redis
 ↓
Worker
 ↓
hello_task()
```

কিন্তু:

```python
hello_task("Atiar")
```

সরাসরি function execute করে।

---

# 16. `apply_async()`

আরও control চাইলে:

```python
hello_task.apply_async(
    args=["Atiar"]
)
```

এখানে পরে আমরা ব্যবহার করব:

```python
countdown
eta
priority
queue
```

---

# 17. Django Model — Video Project

আমাদের database-এ job track করতে হবে।

`videos/models.py`

```python
from django.db import models


class VideoProject(models.Model):

    STATUS_CHOICES = [
        ("queued", "Queued"),
        ("planning", "Planning"),
        ("rendering", "Rendering"),
        ("generating_audio", "Generating Audio"),
        ("composing", "Composing"),
        ("completed", "Completed"),
        ("failed", "Failed"),
    ]

    project_id = models.CharField(
        max_length=100,
        unique=True
    )

    prompt = models.TextField()

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="queued"
    )

    progress = models.FloatField(
        default=0
    )

    output_path = models.CharField(
        max_length=500,
        blank=True,
        null=True
    )

    error_message = models.TextField(
        blank=True,
        null=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

Migration:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# 18. কেন Database + Celery দুটোই দরকার?

এটা খুব important।

Redis:

```text
Task Queue
```

PostgreSQL:

```text
Permanent Project State
```

তাই:

```text
Redis
→ temporary task communication

PostgreSQL
→ permanent job information
```

---

# 19. Video Generation Task

`videos/tasks.py`

```python
from celery import shared_task
from .models import VideoProject


@shared_task
def generate_video(project_id):

    project = VideoProject.objects.get(
        project_id=project_id
    )

    project.status = "planning"
    project.progress = 10
    project.save()

    # AI pipeline এখানে চলবে

    project.status = "rendering"
    project.progress = 40
    project.save()

    # Rendering

    project.status = "generating_audio"
    project.progress = 60
    project.save()

    # TTS

    project.status = "composing"
    project.progress = 80
    project.save()

    # FFmpeg

    project.status = "completed"
    project.progress = 100
    project.save()

    return {
        "project_id": project_id,
        "status": "completed"
    }
```

---

# 20. Pipeline Integration

এখন M16 pipeline এখানে ঢুকবে:

```text
Celery Task
     ↓
EducationalVideoPipeline
```

Example:

```python
@shared_task
def generate_video(project_id):

    project = VideoProject.objects.get(
        project_id=project_id
    )

    project.status = "planning"
    project.save()

    pipeline = EducationalVideoPipeline(
        planner=planner,
        renderer=renderer,
        tts=tts,
        subtitle=subtitle,
        composer=composer
    )

    result = pipeline.generate(
        project.prompt
    )

    project.output_path = result
    project.status = "completed"
    project.progress = 100
    project.save()

    return result
```

---

# 21. কিন্তু একটা সমস্যা আছে

পুরো pipeline যদি একটি task হয়:

```text
generate_video()
```

তাহলে:

```text
RAG
 ↓
LLM
 ↓
VLM
 ↓
Image
 ↓
Video
 ↓
TTS
 ↓
Subtitle
 ↓
FFmpeg
```

সব একই worker-এ চলবে।

এটা MVP-এর জন্য ঠিক আছে।

কিন্তু production-এ আমরা আলাদা tasks করতে পারি।

---

# 22. Advanced Task Pipeline

```text
generate_plan
      ↓
generate_visuals
      ↓
generate_audio
      ↓
generate_subtitles
      ↓
compose_video
      ↓
evaluate_video
```

Celery Canvas ব্যবহার করে:

```text
Task A
 ↓
Task B
 ↓
Task C
 ↓
Task D
```

---

# 23. Celery Chain

Concept:

```python
from celery import chain

workflow = chain(
    generate_plan.s(project_id),
    generate_visuals.s(),
    generate_audio.s(),
    compose_video.s()
)

workflow.apply_async()
```

এখানে:

```text
A output
 ↓
B input

B output
 ↓
C input

C output
 ↓
D input
```

---

# 24. আমাদের Educational Video Chain

```text
generate_plan
      ↓
generate_visuals
      ↓
generate_audio
      ↓
generate_subtitles
      ↓
compose_video
      ↓
evaluate_video
```

Architecture:

```text id="4g6e4r"
                  Video Job
                     ↓
                generate_plan
                     ↓
              generate_visuals
                     ↓
               generate_audio
                     ↓
             generate_subtitles
                     ↓
               compose_video
                     ↓
               evaluate_video
                     ↓
                 COMPLETED
```

---

# 25. Group — Parallel Tasks

ধরো 10টা scene:

```text
Scene 1
Scene 2
Scene 3
...
Scene 10
```

প্রতিটা independently generate করা যায়।

তাহলে:

```text
              Visual Generation
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    Scene 1       Scene 2       Scene 3
       ↓             ↓             ↓
    Worker        Worker        Worker
```

Celery `group()` ব্যবহার করতে পারি।

Concept:

```python
from celery import group

job = group(
    generate_scene.s(1),
    generate_scene.s(2),
    generate_scene.s(3),
)

job.apply_async()
```

---

# 26. Chord

Parallel tasks শেষ হওয়ার পর একটি final task চালাতে:

```text
Scene 1 ─┐
Scene 2 ─┼──→ Compose
Scene 3 ─┘
```

Celery `chord` useful।

Concept:

```python
from celery import chord

workflow = chord(
    [
        generate_scene.s(1),
        generate_scene.s(2),
        generate_scene.s(3),
    ]
)(
    compose_scenes.s()
)

workflow.apply_async()
```

এটা তোমার video generator-এর জন্য খুব useful।

---

# 27. CPU Worker vs GPU Worker

M27-এর knowledge এখানে কাজে লাগবে।

CPU tasks:

```text
FFmpeg
File management
JSON validation
Database
Subtitle formatting
```

GPU tasks:

```text
LLM
VLM
Diffusion
Video generation
Whisper GPU
```

আমরা queue আলাদা করতে পারি:

```text
CPU Queue
GPU Queue
```

---

# 28. Queue Architecture

```text
                    Redis
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
      CPU Queue               GPU Queue
          ↓                       ↓
     CPU Worker              GPU Worker
          │                       │
     FFmpeg                  LLM/VLM
     Subtitle                Diffusion
     Files                   Video AI
```

এটাই তোমার project-এর জন্য better architecture।

---

# 29. Queue Routing

Task:

```python
@shared_task(queue="gpu")
def generate_image():
    pass
```

CPU:

```python
@shared_task(queue="cpu")
def compose_video():
    pass
```

Worker:

CPU:

```bash
celery -A config worker \
    --loglevel=info \
    -Q cpu
```

GPU:

```bash
celery -A config worker \
    --loglevel=info \
    -Q gpu
```

---

# 30. GPU Worker-এর গুরুত্বপূর্ণ নিয়ম

GPU worker startup:

```text
Worker starts
      ↓
Load Model
      ↓
Keep Model in VRAM
      ↓
Receive tasks
      ↓
Generate
      ↓
Generate
      ↓
Generate
```

এটা M27-এর persistent model architecture।

---

# 31. Retry

AI API বা model generation মাঝে মাঝে fail করতে পারে।

Celery retry:

```python
@shared_task(
    bind=True,
    autoretry_for=(Exception,),
    retry_backoff=True,
    max_retries=3
)
def generate_scene(self, scene_id):

    return create_scene(scene_id)
```

Concept:

```text
Attempt 1
   ↓
FAIL
   ↓
Retry
   ↓
Attempt 2
   ↓
FAIL
   ↓
Retry
   ↓
Attempt 3
```

---

# 32. কেন Retry দরকার?

Possible failures:

```text
API timeout
CUDA error
Model temporarily unavailable
Network error
Disk error
```

কিন্তু সব error retry করা উচিত নয়।

যেমন:

```text
Invalid JSON
Invalid prompt
Missing file
```

এসব ক্ষেত্রে retry করার আগে error fix করা দরকার।

---

# 33. Better Error Handling

```python
@shared_task(bind=True, max_retries=3)
def generate_scene(self, scene_id):

    try:

        return create_scene(scene_id)

    except TimeoutError as exc:

        raise self.retry(
            exc=exc,
            countdown=10
        )

    except Exception as exc:

        raise exc
```

---

# 34. Progress Tracking

User React frontend-এ দেখতে চাইবে:

```text
Generating video...

████████████░░░░░░░░ 60%
```

তাই database:

```python
project.progress = 60
```

আর status:

```python
project.status = "generating_audio"
```

---

# 35. API Response

User:

```http
POST /api/videos/generate/
```

Request:

```json
{
    "prompt": "Explain binary search to a beginner",
    "duration": 30,
    "language": "en",
    "style": "clean_2d"
}
```

Response:

```json
{
    "project_id": "video_abc123",
    "status": "queued"
}
```

---

# 36. Django View

```python
import uuid

from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from .models import VideoProject
from .tasks import generate_video


class GenerateVideoView(APIView):

    def post(self, request):

        project_id = str(uuid.uuid4())

        project = VideoProject.objects.create(
            project_id=project_id,
            prompt=request.data["prompt"]
        )

        generate_video.delay(
            project_id
        )

        return Response(
            {
                "project_id": project_id,
                "status": "queued"
            },
            status=status.HTTP_202_ACCEPTED
        )
```

---

# 37. কেন `202 Accepted`?

কারণ request accepted হয়েছে:

```text
Job created
```

কিন্তু video এখনো তৈরি হয়নি।

তাই:

```text
200 OK
```

এর চেয়ে:

```text
202 Accepted
```

এখানে conceptually বেশি appropriate।

---

# 38. Status API

React periodically call করতে পারে:

```http
GET /api/videos/video_abc123/status/
```

Response:

```json
{
    "project_id": "video_abc123",
    "status": "rendering",
    "progress": 45
}
```

Complete:

```json
{
    "project_id": "video_abc123",
    "status": "completed",
    "progress": 100,
    "video_url": "/media/videos/final.mp4"
}
```

---

# 39. React Polling

Concept:

```text
POST generate
      ↓
project_id
      ↓
GET status
      ↓
GET status
      ↓
GET status
      ↓
completed
```

React:

```javascript
const checkStatus = async () => {

    const response = await axios.get(
        `/api/videos/${projectId}/status/`
    );

    setStatus(response.data.status);
    setProgress(response.data.progress);
};
```

তারপর:

```javascript
setInterval(checkStatus, 3000);
```

Production-এ পরে WebSocket ব্যবহার করতে পারো।

---

# 40. M28-এর Full Production Flow

```text
                       USER
                         │
                         ▼
                       React
                         │
                         ▼
                   Django API
                         │
                         ▼
                  Create Project
                         │
             ┌───────────┴──────────┐
             ▼                      ▼
        PostgreSQL                Redis
             │                      │
        Project State           Task Queue
                                    │
                    ┌───────────────┴───────────────┐
                    ▼                               ▼
                CPU Queue                       GPU Queue
                    │                               │
                    ▼                               ▼
               CPU Worker                     GPU Worker
                    │                               │
              ┌─────┼─────┐                 ┌──────┼──────┐
              ↓     ↓     ↓                 ↓      ↓      ↓
            FFmpeg Files Subtitle          LLM    VLM  Diffusion
                    │                               │
                    └──────────────┬────────────────┘
                                   ▼
                              Final Video
                                   │
                                   ▼
                                Storage
                                   │
                                   ▼
                              PostgreSQL
                                   │
                                   ▼
                                 React
```

---

# 41. M28 Project Structure — Final

```text
educational_video_ai/
│
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── celery.py
│   └── wsgi.py
│
├── videos/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── tasks.py
│   └── services.py
│
├── workers/
│   ├── cpu_tasks.py
│   └── gpu_tasks.py
│
├── planner/
├── rag/
├── vlm/
├── image/
├── video_generation/
├── tts/
├── subtitle/
├── renderer/
├── timeline/
├── composer/
│
├── media/
├── output/
│
├── requirements.txt
└── .env
```

---

# 42. M28-এর Real Pipeline

আমরা শেষ পর্যন্ত এইভাবে কাজ করব:

```text
POST /generate
       │
       ▼
Create VideoProject
       │
       ▼
Celery
       │
       ▼
generate_plan
       │
       ▼
RAG + LLM
       │
       ▼
Scene JSON
       │
       ▼
generate_scenes
       │
       ├─────────────┬─────────────┐
       ▼             ▼             ▼
    Scene 1       Scene 2       Scene 3
       │             │             │
       └─────────────┴─────────────┘
                     ▼
                  Compose
                     │
                     ▼
                   TTS
                     │
                     ▼
                Subtitles
                     │
                     ▼
                 Evaluation
                     │
              ┌──────┴──────┐
              ↓             ↓
            PASS           FAIL
              ↓             ↓
           Final MP4     Regenerate
```

---

# 43. M25 + M26 + M27 + M28

এখন আমাদের architecture অনেক powerful:

```text
M26
RAG
 ↓
Trusted Knowledge

M27
GPU Optimization
 ↓
Efficient AI

M28
Celery + Redis
 ↓
Distributed Processing
```

Together:

```text
Trusted Knowledge
       ↓
      RAG
       ↓
 Educational LLM
       ↓
   Scene JSON
       ↓
 GPU Workers
       ↓
VLM/Image/Video
       ↓
 CPU Workers
       ↓
FFmpeg/Subtitle
       ↓
 Evaluation
       ↓
 Final Video
```

---

# 44. M28 Mini Project

প্রথমে পুরো AI pipeline নয়।

### Step 1

একটি task:

```text
hello_task
```

### Step 2

Django থেকে task dispatch:

```text
POST
 ↓
Celery
 ↓
Redis
 ↓
Worker
```

### Step 3

Database job tracking:

```text
queued
 ↓
processing
 ↓
completed
```

### Step 4

Progress:

```text
0%
 ↓
25%
 ↓
50%
 ↓
75%
 ↓
100%
```

### Step 5

Real video pipeline:

```text
Prompt
 ↓
Mock Planner
 ↓
Mock Renderer
 ↓
Mock TTS
 ↓
Mock Composer
```

### Step 6

তারপর আসল:

```text
RAG
LLM
VLM
Manim
TTS
Whisper
FFmpeg
```

---

# 45. M28 Completion Checklist

### Celery

* [ ] Celery কী
* [ ] Task কী
* [ ] Worker কী
* [ ] `.delay()`
* [ ] `apply_async()`
* [ ] Task ID
* [ ] Task state
* [ ] Retry
* [ ] Chain
* [ ] Group
* [ ] Chord

### Redis

* [ ] Redis কী
* [ ] Broker
* [ ] Queue
* [ ] Result backend
* [ ] Redis connection

### Django

* [ ] Celery configuration
* [ ] Django task
* [ ] VideoProject model
* [ ] Job status
* [ ] Progress
* [ ] Status API
* [ ] Async API

### Distributed System

* [ ] CPU worker
* [ ] GPU worker
* [ ] CPU queue
* [ ] GPU queue
* [ ] Task routing
* [ ] Persistent model
* [ ] Failure handling

### Educational AI

* [ ] RAG task
* [ ] LLM task
* [ ] VLM task
* [ ] Image generation task
* [ ] Video generation task
* [ ] TTS task
* [ ] Subtitle task
* [ ] FFmpeg task
* [ ] Evaluation task

---

# 46. সবচেয়ে গুরুত্বপূর্ণ Concept

M28-এর পুরো বিষয়টি এই diagram-এ:

```text
                 DJANGO
                    │
                    │
                 "Generate"
                    │
                    ▼
                  REDIS
                    │
             ┌──────┴──────┐
             ▼             ▼
         CPU QUEUE      GPU QUEUE
             │             │
             ▼             ▼
        CPU WORKER      GPU WORKER
             │             │
       FFmpeg/File      LLM/VLM
       Subtitle         Image/Video
             │             │
             └──────┬──────┘
                    ▼
                FINAL VIDEO
                    │
                    ▼
                DATABASE
                    │
                    ▼
                  REACT
```

### M28 Golden Rule

> **Django should accept the job, Redis should queue the job, Celery should execute the job, PostgreSQL should track the job, and GPU/CPU workers should perform the actual AI work.**

এখন তোমার project-এর architecture আর শুধু একটি Python script নয়—এটা একটি **distributed AI video generation system** হয়ে যাচ্ছে।

**পরবর্তী M29:** `Django + React Production AI Video Generator` — authentication, project management, API design, job dashboard, progress UI, video history, storage, permissions এবং complete frontend/backend integration।


---
# M29 — Django + React Production AI Video Generator 🚀

M28 পর্যন্ত আমরা **Celery + Redis + CPU/GPU Worker** তৈরি করেছি। এখন M29-এ আমরা পুরো system-কে একটি ব্যবহারযোগ্য **production-style web application** বানাব।

Target:

```text
User
 ↓
React Frontend
 ↓
Django REST API
 ↓
PostgreSQL
 ↓
Redis
 ↓
Celery
 ↓
CPU/GPU Workers
 ↓
AI Video Pipeline
 ↓
Storage
 ↓
React Video Dashboard
```

---

# 1. M29-এর লক্ষ্য

M29 শেষে user যেন:

1. Register করতে পারে
    
2. Login করতে পারে
    
3. Dashboard দেখতে পারে
    
4. নতুন educational video request করতে পারে
    
5. Generation progress দেখতে পারে
    
6. Previous projects দেখতে পারে
    
7. Generated video play করতে পারে
    
8. Video download করতে পারে
    
9. Project details দেখতে পারে
    
10. Failed job দেখতে পারে
    
11. নিজের project অন্য user-এর থেকে আলাদা রাখতে পারে
    

---

# 2. Final Product কেমন হবে?

ধরো user লিখল:

```text
Explain binary search to a beginner in 30 seconds.
```

Frontend:

```text
┌──────────────────────────────────────┐
│       AI Educational Video           │
├──────────────────────────────────────┤
│                                      │
│ Topic / Prompt                       │
│ ┌──────────────────────────────────┐ │
│ │ Explain binary search...         │ │
│ └──────────────────────────────────┘ │
│                                      │
│ Duration: 30 sec                     │
│ Language: English                    │
│ Style: Clean 2D                      │
│                                      │
│       [ Generate Video ]             │
└──────────────────────────────────────┘
```

Generate চাপলে:

```text
Generating...

Planning             ✓
Generating scenes    ✓
Generating audio     ✓
Composing            ⏳

████████████░░░░ 70%
```

শেষে:

```text
✓ Video Completed

[▶ Watch Video]

[Download]

[View Details]
```

---

# 3. M29 Architecture

```text
                         USER
                           │
                           ▼
                    React Frontend
                           │
                     JWT Authentication
                           │
                           ▼
                    Django REST API
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
       Users           Projects          Videos
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                       PostgreSQL
                           │
                           ▼
                         Redis
                           │
                  ┌────────┴────────┐
                  ▼                 ▼
             CPU Worker         GPU Worker
                  │                 │
                  └────────┬────────┘
                           ▼
                  AI Video Pipeline
                           │
                           ▼
                     Video Storage
                           │
                           ▼
                    React Dashboard
```

---

# 4. M29 Technologies

Backend:

```text
Python
Django
Django REST Framework
PostgreSQL
JWT
Celery
Redis
```

Frontend:

```text
React
Axios
React Router
```

AI:

```text
RAG
LLM
VLM
Manim
Image Generation
Video Generation
TTS
Whisper
FFmpeg
```

---

# 5. Backend Structure

```text
backend/
│
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── celery.py
│   └── wsgi.py
│
├── accounts/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── permissions.py
│
├── projects/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── tasks.py
│   └── services.py
│
├── ai_pipeline/
│   ├── planner.py
│   ├── rag.py
│   ├── visual.py
│   ├── audio.py
│   ├── composer.py
│   └── pipeline.py
│
├── workers/
│   ├── cpu_tasks.py
│   └── gpu_tasks.py
│
├── media/
│
├── requirements.txt
└── .env
```

---

# 6. Frontend Structure

```text
frontend/
│
├── src/
│   │
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── Sidebar.jsx
│   │   ├── ProgressBar.jsx
│   │   ├── VideoCard.jsx
│   │   └── Loading.jsx
│   │
│   ├── pages/
│   │   ├── Login.jsx
│   │   ├── Register.jsx
│   │   ├── Dashboard.jsx
│   │   ├── CreateVideo.jsx
│   │   ├── VideoDetails.jsx
│   │   └── Profile.jsx
│   │
│   ├── services/
│   │   ├── api.js
│   │   ├── auth.js
│   │   └── videos.js
│   │
│   ├── context/
│   │   └── AuthContext.jsx
│   │
│   ├── routes/
│   │   └── ProtectedRoute.jsx
│   │
│   ├── App.jsx
│   └── main.jsx
│
└── package.json
```

---

# 7. Authentication

Production application-এ user system লাগবে।

Architecture:

```text
Register
   ↓
User
   ↓
Login
   ↓
JWT Access Token
   +
Refresh Token
```

JWT:

```text
Access Token
 ↓
API Requests
```

Refresh:

```text
Access Token expired
 ↓
Refresh Token
 ↓
New Access Token
```

---

# 8. Django JWT Installation

```bash
pip install djangorestframework-simplejwt
```

Settings:

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ],
}
```

---

# 9. JWT URLs

`config/urls.py`

```python
from django.urls import path
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)


urlpatterns = [

    path(
        "api/auth/token/",
        TokenObtainPairView.as_view()
    ),

    path(
        "api/auth/token/refresh/",
        TokenRefreshView.as_view()
    ),
]
```

Login:

```http
POST /api/auth/token/
```

Request:

```json
{
    "email": "user@example.com",
    "password": "password"
}
```

Response:

```json
{
    "access": "...",
    "refresh": "..."
}
```

তোমার existing custom-user setup থাকলে token serializer-এ email-based authentication অনুযায়ী adjustment করতে হবে।

---

# 10. Project Model

M28-এর `VideoProject`-কে আরও production-ready করি।

```python
from django.conf import settings
from django.db import models


class VideoProject(models.Model):

    STATUS_CHOICES = [
        ("queued", "Queued"),
        ("planning", "Planning"),
        ("generating", "Generating"),
        ("rendering", "Rendering"),
        ("audio", "Audio"),
        ("composing", "Composing"),
        ("evaluating", "Evaluating"),
        ("completed", "Completed"),
        ("failed", "Failed"),
    ]

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="video_projects"
    )

    project_id = models.UUIDField(
        unique=True,
        editable=False
    )

    prompt = models.TextField()

    duration = models.FloatField(
        default=30
    )

    language = models.CharField(
        max_length=20,
        default="en"
    )

    style = models.CharField(
        max_length=50,
        default="clean_2d"
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="queued"
    )

    progress = models.FloatField(
        default=0
    )

    output_path = models.CharField(
        max_length=500,
        blank=True,
        null=True
    )

    error_message = models.TextField(
        blank=True,
        null=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

---

# 11. Why `user` ForeignKey?

ধরো:

```text
User A
 ├── Binary Search
 ├── Photosynthesis
 └── Newton's Law

User B
 ├── Python
 └── Machine Learning
```

API-তে user A যেন user B-এর project দেখতে না পারে।

তাই:

```python
user = models.ForeignKey(...)
```

খুব গুরুত্বপূর্ণ।

---

# 12. Serializer

`projects/serializers.py`

```python
from rest_framework import serializers
from .models import VideoProject


class VideoProjectSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = VideoProject

        fields = [
            "project_id",
            "prompt",
            "duration",
            "language",
            "style",
            "status",
            "progress",
            "output_path",
            "error_message",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "project_id",
            "status",
            "progress",
            "output_path",
            "error_message",
            "created_at",
            "updated_at",
        ]
```

---

# 13. Create Video API

```python
import uuid

from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from .models import VideoProject
from .tasks import generate_video


class GenerateVideoView(APIView):

    def post(self, request):

        project = VideoProject.objects.create(

            user=request.user,

            project_id=uuid.uuid4(),

            prompt=request.data["prompt"],

            duration=request.data.get(
                "duration",
                30
            ),

            language=request.data.get(
                "language",
                "en"
            ),

            style=request.data.get(
                "style",
                "clean_2d"
            )
        )

        generate_video.delay(
            str(project.project_id)
        )

        return Response(
            {
                "project_id": str(
                    project.project_id
                ),
                "status": "queued"
            },
            status=status.HTTP_202_ACCEPTED
        )
```

---

# 14. Permission

এই API শুধু authenticated user-এর জন্য:

```python
from rest_framework.permissions import IsAuthenticated


class GenerateVideoView(APIView):

    permission_classes = [
        IsAuthenticated
    ]
```

---

# 15. Project List API

User শুধু নিজের projects দেখবে:

```python
from rest_framework.generics import ListAPIView
from rest_framework.permissions import IsAuthenticated

from .models import VideoProject
from .serializers import VideoProjectSerializer


class ProjectListView(ListAPIView):

    permission_classes = [
        IsAuthenticated
    ]

    serializer_class = VideoProjectSerializer

    def get_queryset(self):

        return VideoProject.objects.filter(
            user=self.request.user
        ).order_by("-created_at")
```

এখানে:

```python
user=self.request.user
```

security-এর জন্য অত্যন্ত important।

---

# 16. Project Details

```python
from rest_framework.generics import RetrieveAPIView


class ProjectDetailView(
    RetrieveAPIView
):

    permission_classes = [
        IsAuthenticated
    ]

    serializer_class = VideoProjectSerializer

    lookup_field = "project_id"

    def get_queryset(self):

        return VideoProject.objects.filter(
            user=self.request.user
        )
```

ফলে:

```text
User A → নিজের project
User A → User B project ❌
```

---

# 17. URLs

`projects/urls.py`

```python
from django.urls import path

from .views import (
    GenerateVideoView,
    ProjectListView,
    ProjectDetailView,
)


urlpatterns = [

    path(
        "generate/",
        GenerateVideoView.as_view()
    ),

    path(
        "",
        ProjectListView.as_view()
    ),

    path(
        "<uuid:project_id>/",
        ProjectDetailView.as_view()
    ),
]
```

---

# 18. Celery Task

এখন M28-এর task-কে actual pipeline-এর সাথে connect করব।

```python
from celery import shared_task

from .models import VideoProject


@shared_task(
    bind=True,
    max_retries=3
)
def generate_video(
    self,
    project_id
):

    project = VideoProject.objects.get(
        project_id=project_id
    )

    try:

        project.status = "planning"
        project.progress = 10
        project.save()

        # M26 RAG + M18/M19 LLM
        plan = create_plan(
            project.prompt,
            project.duration,
            project.language,
            project.style
        )

        project.progress = 25
        project.save()

        project.status = "generating"
        project.save()

        # M21/M22 visual generation
        scenes = generate_scenes(plan)

        project.progress = 50
        project.save()

        project.status = "audio"
        project.save()

        # M14/M15
        audio = generate_audio(
            plan
        )

        project.progress = 70
        project.save()

        project.status = "composing"
        project.save()

        # M13/M16
        video_path = compose_video(
            scenes,
            audio
        )

        project.progress = 90
        project.save()

        project.status = "evaluating"
        project.save()

        # M25
        evaluation = evaluate_video(
            video_path
        )

        if evaluation["score"] < 0.85:

            raise ValueError(
                "Video quality below threshold."
            )

        project.output_path = video_path
        project.status = "completed"
        project.progress = 100
        project.save()

        return {
            "project_id": str(
                project.project_id
            ),
            "status": "completed"
        }

    except Exception as exc:

        project.status = "failed"

        project.error_message = str(exc)

        project.save()

        raise
```

---

# 19. কিন্তু এখানে একটা গুরুত্বপূর্ণ Improvement

Production system-এ:

```text
generate_video()
```

এর মধ্যে সব কাজ রাখার বদলে আমরা M28-এর Celery chain ব্যবহার করব।

Better:

```text
Plan
 ↓
Scenes
 ↓
Audio
 ↓
Subtitle
 ↓
Compose
 ↓
Evaluate
```

এটাই পরবর্তী production architecture।

---

# 20. React Setup

Create:

```bash
npm create vite@latest frontend -- --template react
```

Install:

```bash
cd frontend
npm install
```

Axios:

```bash
npm install axios
```

React Router:

```bash
npm install react-router-dom
```

---

# 21. Axios Configuration

`services/api.js`

```javascript
import axios from "axios";

const api = axios.create({
    baseURL: "http://localhost:8000/api",
});

api.interceptors.request.use(
    (config) => {

        const token =
            localStorage.getItem("access_token");

        if (token) {

            config.headers.Authorization =
                `Bearer ${token}`;
        }

        return config;
    }
);

export default api;
```

এখন প্রতিটি API request-এ:

```text
Authorization:
Bearer TOKEN
```

যাবে।

---

# 22. Login

```javascript
import api from "./api";

export async function login(
    email,
    password
) {

    const response = await api.post(
        "/auth/token/",
        {
            email,
            password
        }
    );

    localStorage.setItem(
        "access_token",
        response.data.access
    );

    localStorage.setItem(
        "refresh_token",
        response.data.refresh
    );

    return response.data;
}
```

---

# 23. Create Video Service

```javascript
import api from "./api";


export async function generateVideo(data) {

    const response = await api.post(
        "/projects/generate/",
        data
    );

    return response.data;
}
```

Call:

```javascript
const result = await generateVideo({
    prompt:
        "Explain binary search to a beginner",
    duration: 30,
    language: "en",
    style: "clean_2d"
});
```

Response:

```json
{
    "project_id": "abc...",
    "status": "queued"
}
```

---

# 24. Create Video Page

```jsx
import { useState } from "react";
import { generateVideo } from "../services/videos";


export default function CreateVideo() {

    const [prompt, setPrompt] = useState("");
    const [loading, setLoading] = useState(false);

    async function handleGenerate() {

        setLoading(true);

        try {

            const result =
                await generateVideo({
                    prompt,
                    duration: 30,
                    language: "en",
                    style: "clean_2d"
                });

            console.log(result);

        } catch (error) {

            console.error(error);

        } finally {

            setLoading(false);
        }
    }

    return (

        <div>

            <h1>
                Create Educational Video
            </h1>

            <textarea
                value={prompt}
                onChange={(e) =>
                    setPrompt(e.target.value)
                }
                placeholder="Explain binary search..."
            />

            <button
                onClick={handleGenerate}
                disabled={loading}
            >
                {loading
                    ? "Submitting..."
                    : "Generate Video"
                }
            </button>

        </div>
    );
}
```

---

# 25. Dashboard

Dashboard API:

```javascript
import api from "./api";


export async function getProjects() {

    const response = await api.get(
        "/projects/"
    );

    return response.data;
}
```

React:

```jsx
import { useEffect, useState } from "react";
import { getProjects } from "../services/videos";


export default function Dashboard() {

    const [projects, setProjects] =
        useState([]);

    useEffect(() => {

        getProjects()
            .then(setProjects)
            .catch(console.error);

    }, []);

    return (

        <div>

            <h1>My Videos</h1>

            {projects.map(project => (

                <div key={project.project_id}>

                    <h3>
                        {project.prompt}
                    </h3>

                    <p>
                        Status:
                        {project.status}
                    </p>

                    <p>
                        Progress:
                        {project.progress}%
                    </p>

                </div>

            ))}

        </div>
    );
}
```

---

# 26. Progress Bar

```jsx
function ProgressBar({ progress }) {

    return (

        <div
            style={{
                width: "100%",
                background: "#ddd"
            }}
        >

            <div
                style={{
                    width: `${progress}%`,
                    height: "20px"
                }}
            />

        </div>
    );
}
```

Use:

```jsx
<ProgressBar
    progress={project.progress}
/>
```

---

# 27. Job Polling

M28-এর status API ব্যবহার করে React প্রতি কয়েক second-এ status check করতে পারে।

```javascript
useEffect(() => {

    const interval =
        setInterval(async () => {

            const response =
                await api.get(
                    `/projects/${projectId}/`
                );

            setProject(response.data);

            if (
                response.data.status ===
                "completed"
            ) {
                clearInterval(interval);
            }

            if (
                response.data.status ===
                "failed"
            ) {
                clearInterval(interval);
            }

        }, 3000);

    return () =>
        clearInterval(interval);

}, [projectId]);
```

Flow:

```text
React
 ↓
GET status
 ↓
3 sec
 ↓
GET status
 ↓
3 sec
 ↓
GET status
 ↓
completed
```

---

# 28. Better Production Approach

Polling কাজ করবে।

কিন্তু later:

```text
React
 ↓
WebSocket
 ↓
Django Channels
 ↓
Celery
```

তাহলে real-time:

```text
0%
 ↓
10%
 ↓
25%
 ↓
50%
 ↓
70%
 ↓
100%
```

frontend immediately update হবে।

এটা M30-এর advanced integration-এর অংশ হতে পারে।

---

# 29. Video Player

Completed হলে:

```jsx
{project.status === "completed" && (

    <video
        controls
        width="800"
    >
        <source
            src={project.output_path}
            type="video/mp4"
        />
    </video>

)}
```

---

# 30. Video Storage

Development:

```text
media/
└── videos/
    ├── video_001.mp4
    └── video_002.mp4
```

Production-এ local disk-এর পরিবর্তে object storage/CDN ব্যবহার করা ভালো:

```text
AI Worker
   ↓
Object Storage
   ↓
CDN
   ↓
React
```

উদাহরণ:

```text
Cloud storage
+
CDN
```

তোমার আগের Cloudinary experience থাকায় image/video asset storage-এর জন্য সেটার মতো object-storage/CDN service ব্যবহার করতে পারো; তবে generated large videos-এর জন্য storage cost ও bandwidth আগে হিসাব করবে।

---

# 31. Security

Production AI application-এ security খুব important।

### User isolation

```python
.filter(user=request.user)
```

### Authentication

```text
JWT
```

### Authorization

```text
Authenticated User
      ↓
Own Project
```

### Rate Limiting

একজন user:

```text
1000 video/day ❌
```

বরং:

```text
Free:
5 videos/day

Premium:
50 videos/day
```

ধরনের quota system রাখা যায়।

---

# 32. Prompt Validation

User arbitrary huge prompt পাঠাতে পারে।

তাই:

```python
prompt = serializers.CharField(
    max_length=2000
)
```

এবং:

```text
Empty prompt ❌
Too long ❌
Invalid duration ❌
Invalid style ❌
```

---

# 33. Allowed Styles

```python
ALLOWED_STYLES = [
    "clean_2d",
    "whiteboard",
    "scientific",
    "realistic",
    "cartoon"
]
```

Serializer:

```python
style = serializers.ChoiceField(
    choices=ALLOWED_STYLES
)
```

---

# 34. Duration Validation

```python
def validate_duration(value):

    if value < 10:
        raise serializers.ValidationError(
            "Minimum duration is 10 seconds."
        )

    if value > 300:
        raise serializers.ValidationError(
            "Maximum duration is 5 minutes."
        )

    return value
```

Production-এ user plan অনুযায়ী limit আলাদা হতে পারে।

---

# 35. API Design

তোমার application-এর core endpoints:

```text
AUTH
────────────────────────

POST   /api/auth/register/
POST   /api/auth/token/
POST   /api/auth/token/refresh/


PROJECTS
────────────────────────

GET    /api/projects/
POST   /api/projects/generate/

GET    /api/projects/{id}/

DELETE /api/projects/{id}/


VIDEO
────────────────────────

GET    /api/projects/{id}/video/

GET    /api/projects/{id}/evaluation/
```

---

# 36. Complete User Flow

```text
Register
   ↓
Login
   ↓
Dashboard
   ↓
Create Video
   ↓
Enter Prompt
   ↓
Generate
   ↓
202 Accepted
   ↓
Project Created
   ↓
Redis
   ↓
Celery
   ↓
AI Pipeline
   ↓
Progress Updates
   ↓
Evaluation
   ↓
Completed
   ↓
Video Storage
   ↓
Dashboard
   ↓
Watch Video
```

---

# 37. M26 → M29 Integration

এখন প্রতিটি milestone বাস্তবে connect হচ্ছে:

```text
M26
Trusted Knowledge
      ↓
     RAG
      ↓
M18/M19
LLM + Prompt Engineering
      ↓
Scene JSON
      ↓
M20
VLM
      ↓
M21
Image Generation
      ↓
M22
Video Generation
      ↓
M23/M24
LoRA
      ↓
M14/M15
TTS + Subtitle
      ↓
M25
Evaluation
      ↓
M27
GPU Optimization
      ↓
M28
Celery + Redis
      ↓
M29
Django + React
```

---

# 38. Production Architecture

এখন পুরো system:

```text
                         USER
                           │
                           ▼
                    ┌─────────────┐
                    │    React    │
                    └──────┬──────┘
                           │
                         HTTPS
                           │
                           ▼
                    ┌─────────────┐
                    │   Django    │
                    │     API     │
                    └──────┬──────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
        PostgreSQL       Redis        Storage
             │             │
             │             ▼
             │          Celery
             │             │
             │      ┌──────┴──────┐
             │      ▼             ▼
             │   CPU Worker    GPU Worker
             │      │             │
             │      │      ┌──────┼──────┐
             │      │      ▼      ▼      ▼
             │      │     LLM    VLM  Diffusion
             │      │
             │      └──────┬──────────────┘
             │             ▼
             │       TTS / FFmpeg
             │             │
             └─────────────┤
                           ▼
                      Final Video
                           │
                           ▼
                        Storage
                           │
                           ▼
                         React
```

---

# 39. Production Deployment Concept

Development:

```text
localhost
├── Django
├── React
├── PostgreSQL
├── Redis
└── Celery
```

Production:

```text
                     Internet
                        │
                        ▼
                      Nginx
                        │
                ┌───────┴────────┐
                ▼                ▼
             React             Django
                                  │
                     ┌────────────┼───────────┐
                     ▼            ▼           ▼
                 PostgreSQL     Redis      Storage
                                  │
                                  ▼
                              Celery
                                  │
                         ┌────────┴────────┐
                         ▼                 ▼
                     CPU Worker        GPU Worker
```

---

# 40. Docker Architecture

Later production deployment:

```text
docker-compose.yml
```

Services:

```text
frontend
backend
postgres
redis
celery_cpu
celery_gpu
nginx
```

Concept:

```yaml
services:

  backend:
    ...

  frontend:
    ...

  postgres:
    ...

  redis:
    ...

  celery_cpu:
    ...

  celery_gpu:
    ...
```

GPU worker-এর জন্য host NVIDIA/CUDA configuration আলাদাভাবে লাগবে।

---

# 41. M29 Testing

Backend test:

```text
Authentication
      ↓
API
      ↓
Database
      ↓
Celery
      ↓
Pipeline
```

Test cases:

```text
✓ Register
✓ Login
✓ Invalid login
✓ Create project
✓ Empty prompt rejected
✓ Invalid duration rejected
✓ User cannot access another user's project
✓ Task queued
✓ Progress updated
✓ Failed task recorded
✓ Completed video returned
```

---

# 42. সবচেয়ে গুরুত্বপূর্ণ Security Test

ধরো:

```text
Project A → User A
Project B → User B
```

User A request করল:

```http
GET /api/projects/PROJECT-B/
```

Response হওয়া উচিত:

```text
404 Not Found
```

বা appropriate permission response।

কখনো:

```text
Project B data
```

দেওয়া যাবে না।

---

# 43. M29 Mini Project

এখন তোমার assignment:

## Build "EduVideo AI"

### Backend

```text
Django
+
DRF
+
JWT
+
PostgreSQL
+
Celery
+
Redis
```

### Frontend

```text
React
+
Axios
+
React Router
```

### Features

```text
Register
Login
Dashboard
Create Video
Project Status
Progress Bar
Video Player
Project History
```

---

# 44. প্রথম MVP

প্রথম version-এ AI generation না দিলেও চলবে।

Mock pipeline:

```text
User Prompt
    ↓
Django
    ↓
PostgreSQL
    ↓
Celery
    ↓
5 second delay
    ↓
status = completed
```

তারপর:

```text
Mock Video
```

দেখাবে।

এতে frontend/backend/queue architecture আগে ঠিক হবে।

---

# 45. তারপর Real AI

Mock:

```text
Mock Planner
Mock Renderer
Mock TTS
```

replace করো:

```text
RAG
 ↓
LLM
 ↓
VLM
 ↓
Manim/Image/Video
 ↓
TTS
 ↓
Whisper
 ↓
FFmpeg
 ↓
Evaluation
```

---

# 46. M29 Completion Checklist

### Backend

-  Django production structure
    
-  DRF
    
-  JWT
    
-  User authentication
    
-  Project model
    
-  Project serializer
    
-  Generate API
    
-  List API
    
-  Detail API
    
-  Delete API
    
-  Permissions
    
-  User isolation
    

### Celery

-  Celery integration
    
-  Redis
    
-  Background task
    
-  Task status
    
-  Progress
    
-  Retry
    
-  CPU worker
    
-  GPU worker
    

### React

-  React setup
    
-  Axios
    
-  Login
    
-  Register
    
-  Protected routes
    
-  Dashboard
    
-  Create Video
    
-  Progress bar
    
-  Video player
    
-  Project history
    

### Production

-  Environment variables
    
-  PostgreSQL
    
-  Storage
    
-  Nginx
    
-  HTTPS
    
-  Docker
    
-  Logging
    
-  Error handling
    
-  Rate limiting
    

---

# 47. M29-এর Golden Architecture

এখন পুরো project-এর mental model:

```text
                     USER
                       │
                       ▼
                    REACT
                       │
                       ▼
                 DJANGO REST API
                       │
              ┌────────┴────────┐
              ▼                 ▼
          PostgreSQL          Redis
              │                 │
              │              Celery
              │                 │
              │        ┌────────┴────────┐
              │        ▼                 ▼
              │    CPU Worker        GPU Worker
              │        │                 │
              │        │       ┌─────────┼─────────┐
              │        │       ▼         ▼         ▼
              │        │      LLM       VLM    Diffusion
              │        │
              │        └─────────┬───────────────┘
              │                  ▼
              │             TTS/FFmpeg
              │                  │
              └──────────────────┤
                                 ▼
                              Storage
                                 │
                                 ▼
                              React
                                 │
                                 ▼
                           Final MP4 🎬
```

### M29 Golden Rule

> **React handles the user experience, Django handles the API and security, PostgreSQL stores persistent state, Redis/Celery handles long-running jobs, GPU workers handle AI generation, and object storage serves the final video.**

এখন তুমি **M1 → M29** পর্যন্ত গেলে একটি সাধারণ AI demo নয়—একটি **full-stack, RAG-grounded, multimodal, GPU-optimized, distributed educational video generation platform**-এর architecture বুঝে ফেলবে।

**M30 হবে Final Capstone — Complete AI Educational Video Generator:** M1–M29-এর সব component একসাথে integrate করে `Prompt → RAG → LLM → Scene JSON → VLM → Manim/Image/Video → LoRA → TTS → Subtitle → Evaluation → Celery/GPU → Storage → React → Final MP4` একটি complete project হিসেবে build করা।

---
# M30 — Complete AI Educational Video Generator 🎬🤖

এটাই আমাদের **Final Capstone Milestone**।

M1 থেকে M29 পর্যন্ত আমরা আলাদা আলাদা component তৈরি করেছি। M30-এ এগুলোকে একসাথে integrate করে একটি complete system বানাব:

```text id="8f0c2e"
USER PROMPT
     ↓
React Frontend
     ↓
Django REST API
     ↓
Celery + Redis
     ↓
RAG / Trusted Knowledge
     ↓
Educational LLM
     ↓
Scene JSON
     ↓
Visual Planner
     ↓
┌───────────────┬────────────────┐
↓               ↓                ↓
Manim          Image AI        Video AI
↓               ↓                ↓
└───────────────┴────────────────┘
                ↓
              VLM
                ↓
          Quality Check
                ↓
              TTS
                ↓
            Whisper
                ↓
            Subtitles
                ↓
             FFmpeg
                ↓
          Final Evaluation
                ↓
          Storage / CDN
                ↓
             React
                ↓
          🎬 FINAL MP4
```

---

# 1. আমাদের Final Product

User শুধু লিখবে:

```text
Explain binary search to a beginner in 30 seconds.
```

System automatically করবে:

```text
Understand Request
       ↓
Find Trusted Knowledge
       ↓
Create Learning Objectives
       ↓
Generate Script
       ↓
Create Scene Plan
       ↓
Plan Visuals
       ↓
Generate Animation
       ↓
Generate Voice
       ↓
Generate Subtitle
       ↓
Evaluate
       ↓
Compose
       ↓
Final Video
```

অর্থাৎ user-কে:

* Script লিখতে হবে না
* Scene বানাতে হবে না
* Animation code লিখতে হবে না
* Voice record করতে হবে না
* Subtitle বানাতে হবে না
* FFmpeg command চালাতে হবে না

---

# 2. Final Architecture

পুরো architecture-কে ৮টি layer-এ ভাগ করব।

```text id="1b2d8f"
LAYER 1
Frontend

LAYER 2
API

LAYER 3
Orchestration

LAYER 4
Educational Intelligence

LAYER 5
Visual Generation

LAYER 6
Audio + Subtitle

LAYER 7
Evaluation

LAYER 8
Storage
```

---

# 3. Layer 1 — React Frontend

Frontend-এর প্রধান pages:

```text id="cbzq13"
Login
Register
Dashboard
Create Video
Project Details
Video Player
Profile
```

Main flow:

```text id="2x3j0r"
Dashboard
    ↓
Create Video
    ↓
Prompt
    ↓
Options
    ↓
Generate
    ↓
Progress
    ↓
Video
```

---

# 4. Create Video UI

Final UI:

```text id="j6gq1w"
┌────────────────────────────────────────────┐
│              EduVideo AI                   │
├────────────────────────────────────────────┤
│                                            │
│ What do you want to learn?                 │
│                                            │
│ ┌────────────────────────────────────────┐ │
│ │ Explain binary search to a beginner   │ │
│ │ in 30 seconds.                        │ │
│ └────────────────────────────────────────┘ │
│                                            │
│ Duration                                   │
│ [ 30 seconds ▼ ]                           │
│                                            │
│ Language                                   │
│ [ English ▼ ]                              │
│                                            │
│ Visual Style                               │
│ [ Clean 2D ▼ ]                             │
│                                            │
│              [ Generate Video ]             │
│                                            │
└────────────────────────────────────────────┘
```

---

# 5. Layer 2 — Django API

Core API:

```text id="5xg7f9"
POST   /api/auth/register/
POST   /api/auth/token/

GET    /api/projects/
POST   /api/projects/generate/

GET    /api/projects/{id}/
DELETE /api/projects/{id}/

GET    /api/projects/{id}/evaluation/
```

Generate request:

```json id="yq2a6b"
{
    "prompt": "Explain binary search to a beginner",
    "duration": 30,
    "language": "en",
    "style": "clean_2d"
}
```

Response:

```json id="5j1hpo"
{
    "project_id": "550e8400-e29b",
    "status": "queued"
}
```

---

# 6. Layer 3 — Job Orchestration

M28-এর Celery এখানে পুরো system-এর backbone হবে।

```text id="m8r4vk"
Django
  ↓
Create Project
  ↓
Redis
  ↓
Celery
  ↓
AI Pipeline
```

আমরা pipeline-কে stages-এ ভাগ করব:

```text id="7i1u3z"
1. planning
2. retrieval
3. scripting
4. visual_planning
5. scene_generation
6. audio_generation
7. subtitle_generation
8. composition
9. evaluation
10. completed
```

---

# 7. Project State Machine

```text id="p1m8f3"
CREATED
   ↓
QUEUED
   ↓
PLANNING
   ↓
RETRIEVING
   ↓
SCRIPT_READY
   ↓
VISUAL_PLANNING
   ↓
GENERATING_SCENES
   ↓
AUDIO_GENERATING
   ↓
SUBTITLE_GENERATING
   ↓
COMPOSING
   ↓
EVALUATING
   ↓
COMPLETED
```

যেকোনো stage:

```text id="h4z9qa"
       ↓
     FAILED
```

---

# 8. Layer 4 — RAG

M26-এর RAG এখানে প্রথম intelligence layer।

User:

```text
Explain Newton's second law.
```

System:

```text id="w4r1gc"
User Query
    ↓
Query Understanding
    ↓
Retriever
    ↓
Vector Database
    ↓
Top 20
    ↓
Reranker
    ↓
Top 5
    ↓
Trusted Evidence
```

---

# 9. Knowledge Base

```text id="a7g4k1"
knowledge/
├── mathematics/
├── physics/
├── biology/
├── chemistry/
└── computer_science/
```

প্রতিটি chunk:

```json id="x0k3fj"
{
    "document_id": "physics_001",
    "topic": "Newton's Second Law",
    "text": "Newton's second law...",
    "page": 42,
    "source": "Physics Textbook",
    "license": "licensed"
}
```

---

# 10. RAG → LLM

এখন evidence LLM-এর কাছে যাবে:

```text id="p6v3kx"
User Request
     ↓
RAG
     ↓
Trusted Context
     ↓
Educational LLM
```

LLM-এর instruction:

```text
Use only the provided evidence.
Do not invent unsupported facts.
Explain for the requested audience.
Create clear learning objectives.
```

---

# 11. Layer 4 — Educational LLM

LLM-এর কাজ:

```text id="3d9k6v"
Prompt
 ↓
Topic
 ↓
Subject
 ↓
Audience
 ↓
Difficulty
 ↓
Learning Objectives
 ↓
Teaching Strategy
 ↓
Script
 ↓
Scene Plan
```

Example:

```json id="0w6f1p"
{
    "topic": "Binary Search",
    "subject": "Computer Science",
    "difficulty": "beginner",
    "duration": 30,
    "learning_objectives": [
        "Understand sorted data",
        "Understand the middle element",
        "Understand elimination of half the search space"
    ]
}
```

---

# 12. Final Scene JSON

এটাই system-এর **central intermediate representation (IR)**।

```json id="g2r7pv"
{
    "project_id": "abc123",
    "topic": "Binary Search",
    "duration": 30,
    "learning_objectives": [
        "Understand binary search",
        "Understand the middle element",
        "Understand half elimination"
    ],
    "scenes": [
        {
            "scene_id": 1,
            "start": 0,
            "end": 5,
            "narration": "Binary search is a fast way to find an item in sorted data.",
            "scene_type": "definition",
            "visual_description": "A sorted array appears."
        },
        {
            "scene_id": 2,
            "start": 5,
            "end": 10,
            "narration": "We begin by checking the middle element.",
            "scene_type": "algorithm",
            "visual_description": "The middle element is highlighted."
        }
    ]
}
```

এটাই সবচেয়ে গুরুত্বপূর্ণ architecture decision:

> **LLM সরাসরি renderer code তৈরি করবে না।**

LLM:

```text
Scene JSON
```

তৈরি করবে।

Renderer:

```text
Scene JSON → Visual
```

তৈরি করবে।

---

# 13. Layer 5 — Visual Planner

প্রতিটি scene-এর জন্য:

```text id="n4k0py"
Narration
    ↓
Visual Planner
    ↓
Visual Objects
    ↓
Animation
    ↓
Camera
    ↓
On-screen Text
```

Example:

```json id="7o2zpq"
{
    "scene_id": 2,
    "objects": [
        {
            "name": "array",
            "type": "array",
            "values": [10, 20, 30, 40, 50]
        },
        {
            "name": "middle",
            "type": "highlight"
        }
    ],
    "animation": [
        {
            "action": "highlight",
            "object": "middle",
            "duration": 2
        }
    ]
}
```

---

# 14. Intelligent Renderer

এখন M22-এর renderer selection ব্যবহার করব:

```python id="9l3r5m"
def choose_renderer(scene_type):

    if scene_type in [
        "algorithm",
        "equation",
        "code",
        "flowchart"
    ]:
        return "manim"

    if scene_type in [
        "real_world",
        "historical"
    ]:
        return "video"

    if scene_type in [
        "scientific_illustration",
        "process"
    ]:
        return "hybrid"

    return "image"
```

---

# 15. Hybrid Visual System

এটা final system-এর অন্যতম গুরুত্বপূর্ণ feature।

সবকিছুর জন্য AI video generation ব্যবহার করব না।

### Algorithm

```text
Manim
```

### Equation

```text
Manim MathTex
```

### Code

```text
Manim Code
```

### Scientific illustration

```text
Image AI
```

### Real-world scene

```text
Video AI
```

### Complex educational scene

```text
Image AI
+
Manim
+
Video AI
```

---

# 16. Final Visual Router

```text id="h8s1xq"
                  Scene
                    │
                    ▼
              Visual Router
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      Manim       Image       Video
        │           │           │
        ▼           ▼           ▼
      Exact      Creative     Motion
      Visual      Visual      Visual
```

---

# 17. M23/M24 LoRA Integration

যদি educational style LoRA trained থাকে:

```text id="t7r2bc"
Image Prompt
     +
Educational LoRA
     ↓
Consistent Educational Image
```

Similarly future video LoRA:

```text id="3x1q4a"
Video Prompt
     +
Educational Video LoRA
     ↓
Consistent Motion Style
```

---

# 18. Layer 6 — TTS

Scene narration:

```text id="h5f8e2"
"Binary search checks the middle element first."
```

TTS:

```text id="k7w4ps"
Text
 ↓
TTS Model
 ↓
scene_002.wav
```

প্রতিটি scene-এর audio আলাদা রাখা ভালো:

```text id="6k0b8d"
audio/
├── scene_001.wav
├── scene_002.wav
├── scene_003.wav
└── scene_004.wav
```

---

# 19. Audio Timing

প্রতিটি scene:

```text id="9c5h4x"
Scene Duration
     ↕
Audio Duration
```

যদি:

```text id="2q9j5e"
Scene = 5 sec
Audio = 7 sec
```

তাহলে mismatch।

System:

```text id="4b0m7a"
Detect
 ↓
Adjust narration
 ↓
Regenerate TTS
```

---

# 20. Layer 6 — Subtitle

TTS:

```text id="k1d9q6"
Audio
 ↓
Whisper
 ↓
Timestamp
 ↓
SRT
```

Example:

```text id="2m8y5c"
00:00:00,000 --> 00:00:03,200
Binary search is a fast search algorithm.

00:00:03,200 --> 00:00:06,000
It works on sorted data.
```

---

# 21. Layer 7 — Evaluation

M25-এর evaluator এখানে final gatekeeper।

```text id="f0s9k3"
Generated Video
      ↓
Evaluation
      ↓
┌─────┼─────┐
↓     ↓     ↓
Text Visual Audio
      ↓
Overall Score
```

Evaluation:

```text id="z7x2w5"
Content Accuracy
Educational Quality
Visual Quality
Audio Quality
Subtitle Quality
Synchronization
Technical Quality
Consistency
```

---

# 22. Quality Gate

```python id="3v5s8n"
def quality_status(score):

    if score >= 0.85:
        return "PASS"

    if score >= 0.70:
        return "REVIEW"

    return "FAIL"
```

Final pipeline:

```text id="j6k2w8"
Evaluation
    ↓
Score >= 0.85?
   / \
 YES  NO
 ↓     ↓
Done  Improve
       ↓
    Regenerate
```

---

# 23. Self-Correction

ধরো VLM বলল:

```text
Middle element is not clearly highlighted.
```

System:

```text id="0p8z6c"
Issue
 ↓
Prompt Improvement
 ↓
Regenerate Scene
 ↓
VLM Evaluation
```

Example:

```python id="j0r6sx"
def improve_prompt(
    original_prompt,
    issue
):
    return f"""
Improve this visual generation prompt.

Original:
{original_prompt}

Problem:
{issue}

Make the requested element
more visually clear.
"""
```

---

# 24. Scene-Level Regeneration

পুরো video regenerate করা যাবে না।

ধরো:

```text id="7m4s2p"
Scene 1 ✓
Scene 2 ✓
Scene 3 ✗
Scene 4 ✓
Scene 5 ✓
```

শুধু:

```text id="z6w8r1"
Scene 3
```

regenerate হবে।

এতে:

```text
Cost ↓
Time ↓
GPU usage ↓
```

---

# 25. Layer 8 — Final Composer

সব components:

```text id="e8t3y6"
Scene Videos
+
Audio
+
Subtitle
+
Transitions
```

FFmpeg:

```text id="q3r7k9"
        FFmpeg
           ↓
      final.mp4
```

Standard output:

```text id="9v1x6b"
1280 × 720
30 FPS
H.264
AAC
MP4
```

---

# 26. Final Project Directory

এটাই আমাদের complete project structure:

```text id="q4z8c1"
educational_video_ai/
│
├── backend/
│   ├── manage.py
│   │
│   ├── config/
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── celery.py
│   │   └── wsgi.py
│   │
│   ├── accounts/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   └── urls.py
│   │
│   ├── projects/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── tasks.py
│   │   └── services.py
│   │
│   ├── rag/
│   │   ├── ingestion.py
│   │   ├── chunker.py
│   │   ├── embeddings.py
│   │   ├── retriever.py
│   │   ├── reranker.py
│   │   ├── verifier.py
│   │   └── service.py
│   │
│   ├── planner/
│   │   ├── prompts.py
│   │   ├── schemas.py
│   │   ├── planner.py
│   │   └── validator.py
│   │
│   ├── vlm/
│   │   ├── client.py
│   │   ├── analyzer.py
│   │   └── evaluator.py
│   │
│   ├── renderer/
│   │   ├── factory.py
│   │   ├── interpreter.py
│   │   ├── timeline.py
│   │   ├── objects/
│   │   └── animations/
│   │
│   ├── image/
│   │   ├── client.py
│   │   ├── prompts.py
│   │   └── manager.py
│   │
│   ├── video_generation/
│   │   ├── client.py
│   │   ├── prompts.py
│   │   ├── continuity.py
│   │   └── evaluator.py
│   │
│   ├── tts/
│   │   ├── engine.py
│   │   └── duration.py
│   │
│   ├── subtitle/
│   │   ├── transcribe.py
│   │   ├── srt.py
│   │   └── formatter.py
│   │
│   ├── evaluation/
│   │   ├── technical.py
│   │   ├── content.py
│   │   ├── visual.py
│   │   ├── audio.py
│   │   └── service.py
│   │
│   └── workers/
│       ├── cpu_tasks.py
│       └── gpu_tasks.py
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── context/
│   │   └── routes/
│   │
│   └── package.json
│
├── knowledge/
├── models/
├── projects/
├── media/
├── output/
│
├── docker-compose.yml
├── .env
├── requirements.txt
└── README.md
```

---

# 27. Central Pipeline Class

সবকিছুর coordinator:

```python id="b4x8k2"
class EducationalVideoPipeline:

    def __init__(
        self,
        rag,
        planner,
        visual_planner,
        renderer,
        image_generator,
        video_generator,
        tts,
        subtitle,
        composer,
        evaluator
    ):

        self.rag = rag
        self.planner = planner
        self.visual_planner = visual_planner
        self.renderer = renderer
        self.image_generator = image_generator
        self.video_generator = video_generator
        self.tts = tts
        self.subtitle = subtitle
        self.composer = composer
        self.evaluator = evaluator
```

---

# 28. `generate()` Method

```python id="c2y7v5"
class EducationalVideoPipeline:

    def generate(self, request):

        # 1. Retrieve knowledge
        context = self.rag.retrieve(
            request.prompt
        )

        # 2. Create educational plan
        plan = self.planner.create_plan(
            request,
            context
        )

        # 3. Visual planning
        visual_plan = (
            self.visual_planner.create(
                plan
            )
        )

        # 4. Generate scenes
        scenes = self.renderer.render(
            visual_plan
        )

        # 5. Generate audio
        audio = self.tts.generate(
            plan
        )

        # 6. Generate subtitles
        subtitles = self.subtitle.generate(
            audio
        )

        # 7. Compose
        video = self.composer.compose(
            scenes,
            audio,
            subtitles
        )

        # 8. Evaluate
        evaluation = self.evaluator.evaluate(
            video,
            plan
        )

        return {
            "video": video,
            "evaluation": evaluation
        }
```

এটা conceptual orchestration। Production version-এ প্রতিটি stage আলাদা Celery task হবে।

---

# 29. Celery Production Pipeline

Final architecture:

```text id="g5y8p1"
                CREATE JOB
                    ↓
               Celery Chain
                    │
        ┌───────────┴────────────┐
        ↓                        ↓
   retrieve_knowledge       create_plan
                                  ↓
                           visual_planning
                                  ↓
                         ┌────────┴────────┐
                         ↓                 ↓
                    scene_1...         scene_N
                         │                 │
                         └────────┬────────┘
                                  ↓
                            generate_audio
                                  ↓
                           generate_subtitles
                                  ↓
                              compose
                                  ↓
                             evaluate
                                  ↓
                            quality_gate
                                  │
                         ┌────────┴────────┐
                         ↓                 ↓
                       PASS              FAIL
                         ↓                 ↓
                     COMPLETE         REGENERATE
```

---

# 30. Parallel Scene Generation

এটা খুব important।

ধরো 8 scenes:

```text id="d9s3v1"
Scene 1 ──┐
Scene 2 ──┤
Scene 3 ──┤
Scene 4 ──┼──→ Compose
Scene 5 ──┤
Scene 6 ──┤
Scene 7 ──┤
Scene 8 ──┘
```

GPU workers available থাকলে multiple scenes parallel generate করা যায়।

তবে একই GPU-তে parallel generation করলে VRAM contention হতে পারে। তাই actual concurrency hardware অনুযায়ী configure করতে হবে।

---

# 31. GPU Worker Strategy

ধরো GPU:

```text
12 GB VRAM
```

তাহলে:

```text
Worker concurrency = 1
```

দিয়ে শুরু করা নিরাপদ হতে পারে।

Large video model:

```text
Worker = 1
```

LLM ছোট হলে অন্য strategy possible।

Golden rule:

> **Celery concurrency blindly বাড়াবে না; VRAM এবং model memory অনুযায়ী concurrency determine করবে।**

---

# 32. Final `.env`

Secrets code-এর মধ্যে রাখবে না।

```env id="6b2m9r"
DEBUG=False

SECRET_KEY=your-secret-key

DATABASE_URL=...

REDIS_URL=redis://localhost:6379/0

LLM_API_KEY=...

MODEL_NAME=...

STORAGE_BUCKET=...

STORAGE_ACCESS_KEY=...

STORAGE_SECRET_KEY=...
```

---

# 33. Docker Services

Final deployment:

```text id="v4n8k0"
                Docker
                  │
     ┌────────────┼────────────┐
     ↓            ↓            ↓
  Django        React       PostgreSQL
     │
     ├──────────────┐
     ↓              ↓
   Redis         Celery
                    │
             ┌──────┴──────┐
             ↓             ↓
        CPU Worker     GPU Worker
```

---

# 34. Monitoring

Production-এ শুধু video generate করলেই হবে না।

Track:

```text id="b7c2m5"
Job ID
User ID
Start time
End time
Duration
GPU usage
VRAM
Model
Prompt
Status
Error
Quality score
```

Example:

```json id="k1q6s8"
{
    "project_id": "abc123",
    "status": "completed",
    "generation_time": 82.4,
    "gpu_memory": 10.2,
    "quality_score": 0.91
}
```

---

# 35. Cost Optimization

AI video generation expensive হতে পারে।

তাই:

```text id="n5k8v2"
RAG
 ↓
Better Prompt
 ↓
Fewer Regenerations
 ↓
Lower GPU Cost
```

আর:

```text id="x7m3q9"
Scene-level regeneration
```

ব্যবহার করলে পুরো video আবার generate করতে হয় না।

---

# 36. Development Strategy

একবারে পুরো system বানাবে না।

এই order follow করো:

### Phase 1

```text id="a1b2c3"
React
 ↓
Django
 ↓
Mock Video
```

### Phase 2

```text id="d4e5f6"
Django
 ↓
Celery
 ↓
Mock Pipeline
```

### Phase 3

```text id="g7h8i9"
Real LLM
 ↓
Scene JSON
 ↓
Manim
```

### Phase 4

```text id="j1k2l3"
TTS
 ↓
Subtitle
 ↓
FFmpeg
```

### Phase 5

```text id="m4n5o6"
RAG
 ↓
Trusted Content
```

### Phase 6

```text id="p7q8r9"
VLM
 ↓
Visual Evaluation
```

### Phase 7

```text id="s1t2u3"
Image/Video AI
```

### Phase 8

```text id="v4w5x6"
LoRA
```

### Phase 9

```text id="y7z8a9"
Production Deployment
```

---

# 37. Final MVP

প্রথম working version-এর জন্য আমি এই target দেব:

```text id="mvp01"
Prompt
 ↓
LLM
 ↓
Scene JSON
 ↓
Manim
 ↓
TTS
 ↓
SRT
 ↓
FFmpeg
 ↓
MP4
```

তারপর:

```text id="mvp02"
+ RAG
+ VLM
+ Image Generation
+ Video Generation
+ Evaluation
```

---

# 38. Final User Experience

শেষে user-এর experience হবে মাত্র:

```text id="user01"
1. Login

2. Enter:
   "Explain photosynthesis
    to a beginner in 60 seconds."

3. Click:
   Generate

4. Wait:
   Planning...
   Generating...
   Rendering...
   Evaluating...

5. Result:
   🎬 Educational Video

6. Watch / Download
```

User কখনো জানবেই না ভিতরে:

```text
RAG
LLM
VLM
LoRA
Celery
Redis
CUDA
Manim
Whisper
FFmpeg
```

চলছে।

এটাই ভালো product architecture।

---

# 39. তোমার 30-Milestone Journey

তুমি যে roadmap শেষ করলে:

```text id="journey"
M01  Foundation
M02  Video Processing
M03  Dataset Engineering
M04  Whisper
M05  Computer Vision
M06  Vision Models
M07  Multimodal Understanding
M08  Scene Planner
M09  Script Engine
M10  Visual Planner
M11  Animation Engine
M12  Generic Renderer
M13  Timeline
M14  TTS
M15  Subtitle
M16  End-to-End Pipeline
M17  Training Dataset
M18  LLM Integration
M19  Prompt Engineering
M20  VLM
M21  Image Generation
M22  Video Generation
M23  LoRA / PEFT
M24  Educational Style
M25  Evaluation
M26  RAG
M27  GPU Optimization
M28  Celery + Redis
M29  Django + React
M30  COMPLETE SYSTEM
```

---

# 40. Final AI Educational Video Generator

সবশেষে:

```text id="final01"
                         USER
                           │
                           ▼
                      REACT APP
                           │
                           ▼
                     DJANGO API
                           │
                           ▼
                    CELERY + REDIS
                           │
                           ▼
                 ┌───────────────────┐
                 │ EDUCATIONAL BRAIN │
                 └─────────┬─────────┘
                           │
                    ┌──────┴──────┐
                    ↓             ↓
                   RAG           LLM
                    ↓             ↓
                 Evidence     Scene JSON
                    └──────┬──────┘
                           ↓
                    VISUAL PLANNER
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
           MANIM         IMAGE          VIDEO
             │             │             │
             └─────────────┼─────────────┘
                           ↓
                          VLM
                           ↓
                     QUALITY CHECK
                           ↓
                          TTS
                           ↓
                        WHISPER
                           ↓
                       SUBTITLE
                           ↓
                        FFmpeg
                           ↓
                     FINAL EVALUATION
                           ↓
                     OBJECT STORAGE
                           ↓
                       REACT PLAYER
                           ↓
                     🎬 FINAL MP4
```

## 🏆 M30 Golden Rule

> **RAG determines what trusted knowledge to use → LLM determines how to teach it → Scene JSON defines what should happen → Manim/Image/Video models create the visuals → TTS creates the voice → Whisper creates timing → FFmpeg assembles everything → VLM/Evaluation checks the result → Celery/Redis makes the whole process scalable.**

এখন সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো **আর নতুন concept শেখার চেয়ে M30-কে actual coding project হিসেবে build করা**। তোমার জন্য ideal next step হবে **M30 Implementation Part 1: complete backend folder setup + Django project + PostgreSQL + JWT + VideoProject model + Generate API + Celery + Redis**, তারপর ধাপে ধাপে real AI components বসানো।




---
