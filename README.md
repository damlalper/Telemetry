# Auto-CRM: End-to-End AI & Microservice Ecosystem

Auto-CRM; is an **“Event-Driven” architecture** that, in the high-performance ingestion layer built with **Go** and **Apache Kafka**, handles **thousands of requests within seconds** and optimizes inter-service communication with the **gRPC protocol**.

While the **business logic** is managed by **Spring Boot (Java)** or **.NET microservices**; in the **data layer**, **PostgreSQL** is used for relational data, **Redis** for caching, and **Elasticsearch** is used in a hybrid manner for logs and text searches.

The **brain of the system**, the **Python-based CrewAI and LangChain agents**, make **hallucination-free, autonomous decisions** by being fed from the corporate memory thanks to the **RAG architecture** supported by **LlamaIndex** and **Vector Databases (Qdrant)**.

Behind the interface presented with **PHP** or modern **JS frameworks**; this structure, **containerized with Docker and Kubernetes** and brought up on **AWS** with **Terraform (IaC)**, provides **central identity management** with **Keycloak**, **secret security** with **HashiCorp Vault**, **distributed tracing** with **OpenTelemetry** and **Jaeger**, and **visualization** with **Grafana**.

All these processes are developed according to **“Enterprise” quality standards (DevSecOps)** by being subjected to **load tests with k6** and **static code analysis with SonarQube** before going live.


## 🏗️ Architecture & Tech Stack

This project is a hybrid architecture combining modern **Enterprise** and **AI-Native** technologies:

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Ingestion Layer** | **Go (Golang)** | Handles high-throughput external requests. |
| **Message Broker** | **Apache Kafka** | Asynchronous service communication & event streaming. |
| **Core Backend** | **Spring Boot (Java)** | Main customer data processing and transactional logic. |
| **Billing / Support Services** | **.NET Core** | Payment, billing, and auxiliary service operations. |
| **AI Agents** | **Python, LangChain, CrewAI** | Autonomous reasoning, NLP tasks, and workflow orchestration. |
| **Knowledge Base** | **LlamaIndex, Qdrant/Pinecone** | Vector database layer for RAG and enterprise memory. |
| **Search Engine** | **Elasticsearch** | Full-text search, logging, and analytics. |
| **Cache Layer** | **Redis** | High-performance caching and session storage. |
| **Frontend** | **PHP (Laravel/Symfony)** | End-user and admin dashboard interfaces. |
| **Monitoring** | **Grafana** | System health monitoring, KPIs, observability dashboards. |
| **Infrastructure** | **Docker, Kubernetes, AWS** | Containerization and cloud-native orchestration. |
| **Security** | **Keycloak & Vault** | Merkezi kimlik yönetimi (IAM) ve şifrelerin (Secrets) izolasyonu. |
| **Communication** | **gRPC (Protobuf)** | Mikroservisler arası iletişimde REST'e göre 10x daha hızlı veri transferi. |
| **Observability** | **OpenTelemetry & Jaeger** | Dağıtık sistemde hatanın kaynağını bulmak için uçtan uca izleme (Distributed Tracing). |
| **Testing** | **k6 & SonarQube** | Yük testi (Load Testing) ve Statik Kod Analizi (Quality Gates). |

---

## 🚀 Key Features

### **Multi-Agent Workflow**
One agent reads and analyzes the email, another retrieves customer data, and a third generates the response — all autonomously.

### **Sentiment Analysis**
Automatically detects message tone (**Angry**, **Neutral**, **Happy**) to prioritize urgent customer tickets.

### **Semantic Search**
Allows natural language queries such as:  
> “Customers who requested a refund last week”  
instead of relying only on strict IDs or exact keywords.

### **Scalable Microservices**
Auto-scaling with Kubernetes ensures stable performance under heavy load.

---

## 🧠 Mühendislik Yaklaşımı ve Mimari Kararlar (Engineering Philosophy)

Bu proje rastgele teknolojilerin bir araya gelmesiyle değil, belirli tasarım desenleri (Design Patterns) gözetilerek geliştirilmiştir:

1.  **Event-Driven Architecture (Olay Güdümlü Mimari):**
    Sistemi senkron (birbirini bekleyen) zincirler yerine asenkron tasarladım. Kafka sayesinde `Ingestion` servisi çökse bile `Core` servis çalışmaya devam eder. Sistem "Fault Tolerant" (Hataya Dayanıklı) yapıdadır.

2.  **Polyglot Persistence (Çoklu Veri Saklama):**
    "Her işe tek veritabanı" hatasına düşülmemiştir.
    * İlişkisel veriler (Müşteri kaydı) -> **PostgreSQL**
    * Önbellek (Hız) -> **Redis**
    * Arama (Log/Metin) -> **Elasticsearch**
    * Yapay Zeka Hafızası (Anlamsal) -> **Vector DB**

3.  **Observability First (Önce Gözlemlenebilirlik):**
    Mikroservis dünyasında "Kör uçuşu" yapmamak için **OpenTelemetry** ve **Jaeger** entegre edilmiştir. Bir isteğin hangi serviste kaç milisaniye harcadığı `TraceID` üzerinden takip edilebilir.

4.  **AI Reliability (Yapay Zeka Güvenilirliği):**
    AI sadece bir chatbot değil, bir "Karar Destek Sistemi"dir. Modelin halüsinasyon görmesini engellemek için **RAG (Retrieval Augmented Generation)** mimarisi kullanılmış, cevapların şirket dokümanlarına dayanması garanti edilmiştir.

---

## 🛠️ Local Development Setup

You can set up the system using **Docker Compose** or **Minikube**.

```bash
# Clone the project
git clone https://github.com/username/auto-crm.git

# Start infrastructure services (Kafka, Redis, Elastic, VectorDB)
docker-compose up -d infra

# Deploy microservices via Kubernetes
kubectl apply -f k8s/deployments/
```
