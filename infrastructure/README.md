# Infrastructure

## GCP Resources

### Vertex AI
- **Model Registry:** MedGemma-Neuro versions
- **Endpoints:** Production endpoint with autoscaling (min: 1, max: 5 replicas)
- **Matching Engine:** HNSW index with 10K medical documents
- **Model Monitoring:** Drift detection jobs (daily schedule)

### Cloud Run
- **Service:** medgemma-api
- **CPU:** 2 vCPU
- **Memory:** 4 GB
- **Concurrency:** 80 requests/instance
- **Timeout:** 300s

### BigQuery
- **Dataset:** medgemma_logs
- **Tables:**
  - `predictions` - All model inferences
  - `rag_retrievals` - Retrieved documents per query
  - `performance_metrics` - Latency and error rates

### IAM & Security
- Service account with least-privilege access
- Workload Identity for Kubernetes (if applicable)
- Private IP for Vertex AI endpoints

## Deployment
```bash
# Setup GCP project
export PROJECT_ID="your-project-id"
export REGION="us-central1"

# Deploy Vertex AI endpoint
gcloud ai endpoints create --region=$REGION --display-name=medgemma-neuro

# Deploy Cloud Run service
gcloud run deploy medgemma-api \
  --region=$REGION \
  --min-instances=1 \
  --max-instances=5 \
  --memory=4Gi

Monitoring Dashboards

Cloud Monitoring: Custom dashboard for latency, errors, QPS
Vertex AI Console: Model drift metrics and distribution comparisons
