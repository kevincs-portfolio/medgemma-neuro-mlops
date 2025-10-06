# System Architecture

## High-Level Design

─────────────┐
│   Client    │
│  (Neurologist)│
└──────┬──────┘
│
▼

┌─────────────────────────────────────────┐
│          Cloud Run (API Gateway)         │
│  - Request validation                    │
│  - Rate limiting                         │
│  - Authentication                        │
└──────┬──────────────────────┬───────────┘
│                      │
▼                      ▼

┌──────────────────┐   ┌─────────────────────┐
│ Matching Engine  │   │  Vertex AI Endpoint │
│  (Vector Search) │   │  (MedGemma + LoRA)  │
│                  │   │                     │
│ - Medical KB     │   │ - Fine-tuned model  │
│ - Embeddings     │   │ - Inference         │
└──────┬───────────┘   └──────┬──────────────┘
│                      │
└──────────┬───────────┘
│
▼
┌────────────────┐
│   BigQuery     │
│ - Query logs   │
│ - Predictions  │
│ - Metrics      │
└────────┬───────┘
│
▼
┌────────────────────┐
│ Vertex AI Monitoring│
│ - Model drift       │
│ - Data drift        │
│ - Alerts            │
└─────────────────────┘

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
