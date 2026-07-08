## Backend + AI Interview Preparation Roadmap

### Phase 1 — Python (Highest Priority) ⭐⭐⭐⭐⭐

* **Core Python :**
  - OOP
  - Classes vs Objects
  - Inheritance
  - Polymorphism
  - Abstraction
  - Encapsulation
  - Magic/Dunder methods

* **Advanced Python :**
  - Iterators
  - Generators
  - Decorators
  - Closures
  - Context Managers (with)
  - Lambda
  - List/Dict/Set Comprehensions
  - *args / **kwargs
  - Mutable vs Immutable
  - Shallow vs Deep Copy
  - Dataclasses
  - Type Hints
  - Exception Handling
  - Logging

* **Concurrency :**
  - GIL
  - Multithreading
  - Multiprocessing
  - AsyncIO
  - Async vs Sync
  - Thread safety

* **Memory :**
  - Reference counting
  - Garbage Collection
  - Memory management

* **Coding :**
  - Python coding questions
  - File handling
  - Collections module
  - Heapq
  - itertools

-----

### Phase 2 — FastAPI ⭐⭐⭐⭐⭐

* **Fundamentals :**
  - Request lifecycle
  - Routing
  - APIRouter
  - Dependency Injection
  - Middleware
  - Background Tasks

* **Request/Response :**
  - Request Models
  - Response Models
  - Validation
  - Pydantic
  - File Uploads
  - Streaming Responses

* **Error Handling :**
  - Exception handlers
  - Validation errors
  - Custom exceptions

* **Authentication :**
  - JWT
  - OAuth basics
  - Security utilities

* **Production :**
  - Async endpoints
  - Pagination
  - Logging
  - Testing
  - Project structure

-----

### Phase 3 — Django & DRF ⭐⭐⭐⭐⭐

* **Django :**
  - Models
  - ORM
  - Migrations
  - Signals
  - Transactions

* **Query Optimization :**
  - select_related
  - prefetch_related
  - annotate
  - aggregation
  - indexing

* **DRF :**
  - Serializers
  - ModelSerializer
  - ViewSets
  - GenericAPIView
  - Mixins
  - Routers
  - Permissions
  - Authentication

-----

### Phase 4 — SQL & PostgreSQL ⭐⭐⭐⭐⭐

* **Queries :**
  - SELECT
  - WHERE
  - GROUP BY
  - HAVING
  - ORDER BY
  - LIMIT
  - OFFSET

* **Joins :**
  - INNER JOIN
  - LEFT JOIN
  - RIGHT JOIN
  - FULL JOIN
  - SELF JOIN

* **Advanced :**
  - Window Functions
  - CTE
  - Subqueries

* **Database Concepts :**
  - Indexes
  - Composite Indexes
  - Clustered vs Non-clustered
  - Transactions
  - ACID
  - Isolation Levels
  - Locks
  - Deadlocks

-----

### Phase 5 — REST APIs ⭐⭐⭐⭐⭐

  - REST principles
  - HTTP methods
  - PUT vs PATCH
  - POST vs PUT
  - Idempotency
  - Status codes
  - Pagination
  - Filtering
  - Versioning
  - JWT
  - OAuth basics
  - Rate limiting
  - API security

----

### Phase 6 — Object-Oriented Design ⭐⭐⭐⭐⭐

* **SOLID :**
  - SRP
  - OCP
  - LSP
  - ISP
  - DIP

* **Design Patterns :**
  - Factory
  - Strategy
  - Singleton
  - Adapter
  - Repository
  - Dependency Injection

-----

### Phase 7 — Project Deep Dive ⭐⭐⭐⭐⭐
**AI-Powered Text Analyzer**

**Know every design decision.**

* **Architecture :**
  - FastAPI
  - ChromaDB
  - Sentence Transformers
  - Adapter Pattern
  - Multi-project support

* **AI :**
  - Embeddings
  - Semantic Search
  - Cosine Similarity
  - Chunking
  - Vector Search

* **Engineering :**
  - Duplicate-safe upserts
  - Incremental Sync
  - JIRA APIs
  - JQL
  - Performance optimization
  - Scaling to millions of records


* **Crash Triage :**
  - Overall architecture
  - ZIP streaming
  - In-memory parsing
  - Plugin architecture
  - Regex parsing
  - Resource management
  - Exception handling
  - Logging
  - Performance optimization
  - Why 20× faster

* **Restaurant Management System :**
  - Django architecture
  - REST APIs
  - Razorpay integration
  - Webhooks
  - Idempotency
  - Transactions
  - Redis caching
  - Pagination
  - Query optimization


* **RAG Project :**
  - Chunking
  - Embeddings
  - Retrieval
  - ChromaDB
  - LangChain
  - Similarity Search
  - Prompt Engineering
  - Hallucinations
  - Context Window
  - Why RAG

----
----

### Phase 8 — Machine Learning ⭐⭐⭐⭐☆

* **Supervised Learning :**
  - Linear Regression
  - Logistic Regression
  - Decision Trees
  - Random Forest
  - SVM
  - KNN
  - Naive Bayes

* **Evaluation :**
  - Precision
  - Recall
  - F1
  - ROC
  - Confusion Matrix

* **ML Concepts :**
  - Bias vs Variance
  - Overfitting
  - Underfitting
  - Cross Validation
  - Feature Engineering


### Phase 9 — LLMs & Generative AI ⭐⭐⭐⭐⭐

* **Fundamentals :**
  - Transformer
  - Attention
  - Self-Attention
  - Tokens
  - Tokenization
  - Embeddings

* **Inference :**
  - Temperature
  - Top-k
  - Top-p
  - Context Window
  - Hallucination

* **Prompt Engineering :**
  - Zero-shot
  - One-shot
  - Few-shot
  - Chain of Thought (conceptually)

* **Retrieval :**
  - RAG
  - Fine-tuning vs Prompting
  - Vector Databases


### Phase 10 — Backend Engineering ⭐⭐⭐⭐☆

* **Docker :**
  - Images
  - Containers
  - Volumes
  - Networks
  - Dockerfile
  - Docker Compose
  - Layers

* **Redis :**
  - Caching
  - TTL
  - Cache invalidation
  - Common use cases

* **Celery :**
  - Workers
  - Broker
  - Beat
  - Retry
  - Task queues
  - Result backend

* **Elasticsearch :**
  - Index
  - Documents
  - Mapping
  - Shards
  - Inverted Index
  - Aggregations
  - Full-text search

----

### Phase 11 — AWS ⭐⭐⭐☆☆

  - EC2
  - S3
  - RDS
  - EBS
  - VPC
  - CloudWatch
  - IAM basics
  - Security Groups

-----

### Phase 12 — System Design ⭐⭐⭐☆☆

* **Core Concepts :**
  - Scalability
  - Load Balancer
  - Caching
  - Database Scaling
  - Replication
  - Sharding
  - CAP theorem (basic)
  - API Gateway
  - Message Queues

* **Design Questions :**
  - URL Shortener
  - Notification System
  - Chat Application
  - Payment System
  - Ride Sharing

----

### Phase 13 — Data Structures & Algorithms ⭐⭐⭐⭐☆

- Arrays
- Strings
- Hash Maps
- Linked Lists
- Stack
- Queue
- Heap
- Trees
- Graphs
- Algorithms
  - BFS
  - DFS
  - Binary Search
  - Sliding Window
  - Two Pointers
  - Prefix Sum
  - Recursion
  - Backtracking (basic)
  - Dynamic Programming (basic)

Target: Medium-level interview problems.

**Suggested Preparation Order :**

- Python
- FastAPI
- SQL & PostgreSQL
- Django & DRF
- REST APIs
- Text Analyzer Project
- Crash Triage Project
- RAG / ChromaDB / LLM Fundamentals
- Docker
- Redis
- AWS
- System Design
- DSA
