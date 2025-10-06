# System Architecture

## High-Level Design

## System Flow

**Request Path:**
1. **Client (Neurologist)** → Sends clinical query
2. **Cloud Run (API Gateway)** → Validates request, authenticates, rate limits
3. **Parallel Processing:**
   - **Vertex AI Matching Engine** → Retrieves top-5 relevant medical documents (RAG)
   - **Vertex AI Endpoint** → Loads fine-tuned MedGemma model
4. **Response Generation** → Combines RAG context + model inference
5. **BigQuery** → Logs query, prediction, latency
6. **Vertex AI Monitoring** → Analyzes logs for drift, triggers alerts

**Data Flow:**

Query → API Gateway → [RAG Retrieval || Model Inference] → Combined Response → Logging → Monitoring

**Key Integration Points:**
- Cloud Run orchestrates both RAG and model calls in parallel
- BigQuery acts as centralized data lake for all predictions
- Vertex AI Monitoring consumes BigQuery logs for drift detection



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
