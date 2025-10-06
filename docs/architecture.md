# System Architecture

## High-Level Design

graph TD
    A[Client - Neurologist] --> B[Cloud Run API Gateway]
    B --> C[Request Validation<br/>Rate Limiting<br/>Authentication]
    C --> D[Vertex AI Matching Engine<br/>Vector Search]
    C --> E[Vertex AI Endpoint<br/>MedGemma + LoRA]
    D --> F[Medical Knowledge Base<br/>Embeddings]
    E --> G[Fine-tuned Model<br/>Inference]
    D --> H[Response Generator]
    E --> H
    H --> I[BigQuery<br/>Logs & Metrics]
    I --> J[Vertex AI Monitoring<br/>Drift Detection & Alerts]
    
    style A fill:#e1f5ff
    style B fill:#fff4e1
    style D fill:#f0e1ff
    style E fill:#f0e1ff
    style I fill:#e1ffe1
    style J fill:#ffe1e1

## Component Details

### 1. RAG Pipeline
- **Embedding Model:** text-embedding-004 (Vertex AI)
- **Vector Store:** Matching Engine with HNSW index
- **Top-k Retrieval:** 5 most relevant documents
- **Context Window:** 2048 tokens

### 2. Fine-tuned Model
- **Base:** MedGemma 4B
- **Method:** LoRA (rank=16, alpha=32)
- **Training Data:** Curated Neurology cases
- **Epochs:** 3 with early stopping

### 3. Monitoring Stack
- **Drift Detection:** Jensen-Shannon divergence on input distributions
- **Performance Metrics:** Latency (p50, p95, p99), error rate
- **Alerting:** Cloud Monitoring → PagerDuty

## Infrastructure as Code

All resources provisioned via Terraform:
- Vertex AI resources
- Cloud Run services
- IAM policies
- Monitoring dashboards
