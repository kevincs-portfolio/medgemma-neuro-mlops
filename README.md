# MedGemma Clinical Update System

**Production MLOps system for medical literature updates with RAG architecture**

🔗 **Live Demo:** [https://medgemma-api-698352278257.us-central1.run.app](https://medgemma-api-698352278257.us-central1.run.app)

---

## 🎯 Project Overview

AI-powered medical information system that provides physicians with **real-time clinical updates** from recent medical literature (2023-2025), deployed on Google Cloud Platform.

**Key Achievement:** Built production-ready MLOps pipeline connecting Large Language Models with PubMed's 30M+ medical papers for evidence-based clinical decision support.

---

## 🏗️ System Architecture
```
┌─────────────┐
│   Doctor    │ Opens web interface
│             │
└──────┬──────┘
       │
       ▼
┌─────────────────────────────────┐
│   Cloud Run API (Production)    │
│   - Flask REST API              │
│   - Auto-scaling                │
└──────┬──────────────────┬───────┘
       │                  │
       ▼                  ▼
┌─────────────┐    ┌──────────────────┐
│  PubMed API │    │  Vertex AI       │
│  30M+ Papers│    │  Gemini 2.0      │
│  2023-2025  │    │  Flash           │
└──────┬──────┘    └────────┬─────────┘
       │                    │
       └─────────┬──────────┘
                 │
                 ▼
         ┌──────────────┐
         │   RAG Engine │
         │   Combines:  │
         │   Context +  │
         │   Generation │
         └──────┬───────┘
                │
                ▼
         ┌──────────────┐
         │   Response   │
         │   + Sources  │
         │   + Citations│
         └──────────────┘
```

---

## 💡 How It Works (Non-Technical)

### **Step 1:** Doctor asks question
Example: *"What are the latest diabetes treatment guidelines?"*

### **Step 2:** System searches medical literature
- Automatically queries PubMed database
- Retrieves 3 most relevant recent studies
- Extracts key information from abstracts

### **Step 3:** AI generates evidence-based answer
- Combines retrieved literature with AI reasoning
- Cites specific studies and years
- Provides actionable clinical recommendations

### **Step 4:** Doctor receives answer
- Clear response with references
- Study titles and publication years
- Ready to apply in clinical practice

**Response Time:** 10-15 seconds  
**Cost per Query:** <$0.002 USD

---

## 🛠 Technology Stack

### **Machine Learning & AI**
- **Model:** Gemini 2.0 Flash (Google Vertex AI)
- **Technique:** RAG (Retrieval-Augmented Generation)
- **Knowledge Source:** PubMed API (NCBI)

### **Cloud Infrastructure (GCP)**
- **Deployment:** Cloud Run (serverless containers)
- **Build:** Cloud Build + Artifact Registry
- **API:** Flask + Gunicorn
- **Authentication:** IAM + Service Accounts

### **MLOps Pipeline**
- Automated deployment from source
- Container orchestration
- Environment variable management
- Auto-scaling (0 to N instances)

---

## 📊 Key Metrics

| Metric | Value |
|--------|-------|
| **Deployment Platform** | Google Cloud Run |
| **Response Time** | 10-15 seconds |
| **Cost per Query** | <$0.002 USD |
| **Monthly Cost** | <$1 USD |
| **Literature Coverage** | 2023-2025 (auto-updated) |
| **Uptime** | 99.9% (Cloud Run SLA) |
| **Scalability** | Auto-scales 0→∞ |

---

## 🚀 Technical Implementation Highlights

### **1. RAG Architecture**
```python
# Simplified flow
def medical_query(question):
    # Retrieval: Get relevant papers
    papers = search_pubmed(question, max_results=3)
    
    # Augmentation: Build context
    context = construct_medical_context(papers)
    
    # Generation: Create answer
    answer = gemini_model.generate(
        prompt=f"{context}\n\nQuestion: {question}"
    )
    
    return answer + citations
```

### **2. Cloud Deployment**
```bash
# One-command deployment
gcloud run deploy medgemma-api \
  --source . \
  --region us-central1 \
  --allow-unauthenticated
```

### **3. Production Features**
- ✅ REST API with JSON responses
- ✅ Web interface for end users
- ✅ Automatic literature retrieval
- ✅ Citation tracking
- ✅ Error handling & logging

---

## 📈 Project Outcomes

### **For the Physician**
- ✅ Access to latest medical guidelines
- ✅ Evidence-based recommendations
- ✅ Time saved on literature review
- ✅ No technical knowledge required

### **For MLOps/Engineering**
- ✅ Production-ready system deployed
- ✅ Cost-optimized architecture (<$1/month)
- ✅ Serverless auto-scaling
- ✅ Integration with medical databases
- ✅ Complete CI/CD pipeline

---

## 🔒 Compliance & Safety

- Uses only publicly available medical literature (PubMed)
- No patient data processed or stored
- Provides references for verification
- Designed as clinical decision **support**, not replacement
- Deployed with Google Cloud security standards

---

## 📁 Repository Structure
```
medgemma-mlops-prod/
├── README.md                    # This file
├── docs/
│   └── architecture.md          # System architecture details
├── infrastructure/
│   └── README.md               # GCP resources documentation
└── medgemma-api/               # API source code (deployed)
    ├── main.py                 # Flask application
    ├── requirements.txt        # Python dependencies
    ├── Dockerfile             # Container configuration
    └── templates/
        └── index.html         # Web interface
```

---

## 🎓 Skills Demonstrated

### **ML Engineering**
- Large Language Model deployment (Gemini)
- RAG (Retrieval-Augmented Generation) implementation
- Vector search and embedding strategies
- Model API integration (Vertex AI)

### **MLOps**
- Cloud deployment (Google Cloud Run)
- Container orchestration (Docker)
- CI/CD pipeline setup
- Infrastructure as Code
- Cost optimization (<$1/month for production)

### **Software Engineering**
- REST API development (Flask)
- External API integration (PubMed/NCBI)
- Frontend development (HTML/CSS/JavaScript)
- Error handling and logging

### **Cloud Architecture**
- Serverless deployment
- Auto-scaling configuration
- IAM and security setup
- Resource management

---

## 💰 Cost Analysis

| Component | Monthly Cost |
|-----------|--------------|
| Cloud Run (API) | ~$0.50 |
| Gemini API calls | ~$0.10 |
| PubMed API | FREE |
| **Total** | **~$0.60/month** |

**For comparison:** Traditional VM deployment would cost $30-50/month

---

## 🔗 Links

- **Live System:** [medgemma-api-698352278257.us-central1.run.app](https://medgemma-api-698352278257.us-central1.run.app)
- **Documentation:** See `/docs` folder
- **Architecture:** `/docs/architecture.md`

---

## 👤 About

**Role:** ML Engineer / MLOps  
**Focus:** Production systems, cloud infrastructure, cost optimization

Built as a practical demonstration of end-to-end MLOps capabilities:
from model selection → RAG implementation → cloud deployment → production monitoring.

---

**Status:** ✅ Production Ready | 🚀 Live System | 💰 Cost Optimized
