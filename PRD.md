### `PRD.md` (Product Requirements Document)
# Product Requirements Document (PRD): Auto-CRM

| Versiyon | Tarih | Statü | Yazar |
| :--- | :--- | :--- | :--- |
| v1.0 | 05.12.2025 | Taslak | [Senin Adın] - İş Analisti |

## 1. Yönetici Özeti (Executive Summary)
Auto-CRM, şirketlerin müşteri iletişim süreçlerindeki manuel eforu minimize eden, yapay zeka tabanlı otonom bir CRM platformudur. Amacımız, müşteri taleplerine dönüş hızını (Response Time) %80 azaltmak ve müşteri memnuniyet skorunu (NPS) artırmaktır. Sistem, "Event-Driven" mimari kullanarak reaktif değil, proaktif bir yapı sunar.

## 2. Problem Tanımı (Problem Statement)
Mevcut piyasa koşullarında şirketlerin yaşadığı temel CRM sorunları:
* **Yavaş Dönüş Süreleri:** Müşteri formlarına dönüş ortalama 24-48 saati bulmaktadır.
* **Veri Siloları:** Müşteri mailleri, satış notları ve destek kayıtları farklı sistemlerde tutulmakta, bütüncül bir müşteri profili oluşturulamamaktadır.
* **Standart Yanıtlar:** Müşterilere bağlamdan kopuk, hazır şablon (copy-paste) cevaplar verilmektedir.
* **Manuel Efor:** Satış temsilcileri zamanlarının %40'ını veri girişine harcamaktadır.

## 3. Hedefler ve Başarı Kriterleri (Goals & KPIs)

| Hedef | Metrik (KPI) | Başarı Kriteri |
| :--- | :--- | :--- |
| Hızlı Yanıt | Average Response Time (ART) | < 2 Dakika (Draft oluşturma) |
| Veri Bütünlüğü | Data Entry Automation Rate | %90+ Otonom Giriş |
| Müşteri Memnuniyeti | Sentiment Score Improvement | Negatiften Pozitife dönüş oranı %30 artış |
| Sistem Dayanıklılığı | Uptime | %99.9 (Kubernetes sayesinde) |

## 4. Kullanıcı Personaları (User Personas)

* **Persona A: Satış Temsilcisi (Can):** Müşteriyi aradığında onun geçmişini, son mailindeki tonunu ve iade talebini tek ekranda görmek istiyor. Manuel not girmek istemiyor.
* **Persona B: Müşteri Hizmetleri Müdürü (Elif):** Ekibin yoğunluğunu, hangi konularda şikayet geldiğini anlık olarak Grafana üzerinden izlemek istiyor.
* **Persona C: Sistem Yöneticisi (DevOps):** Sistemin yoğun anlarda çökmemesini, Kafka kuyruğunun şişmemesini istiyor.

## 5. Fonksiyonel Gereksinimler (Functional Requirements)

### 5.1. Veri Alımı (Ingestion - Go & Kafka)
* **FR-01:** Sistem, Webhook, Email API ve Rest API üzerinden gelen verileri anlık olarak kabul etmelidir.
* **FR-02:** Gelen her veri, kaybolmaması için Apache Kafka kuyruğuna (Topic: `incoming_leads`) yazılmalıdır.
* **FR-03:** Go servisi, saniyede en az 10.000 isteği karşılayabilmelidir.

### 5.2. Yapay Zeka İşlemleri (AI Core - Python & CrewAI)
* **FR-04:** CrewAI ajanı, gelen mesajın dilini ve duygu durumunu (Sentiment) analiz etmelidir.
* **FR-05 (RAG):** Sistem, gelen soruya cevap vermek için Vector Database (Qdrant) üzerindeki şirket dokümanlarını taramalıdır (Retrieval).
* **FR-06:** LLM, bulunan dokümanlara dayanarak taslak bir cevap (Draft) oluşturmalıdır.

### 5.3. Çekirdek CRM İşlevleri (Core - Spring Boot & .NET)
* **FR-07:** İşlenen veriler ve AI sonuçları ilişkisel veritabanına kaydedilmelidir.
* **FR-08:** .NET servisi, ilgili satış temsilcisine bildirim göndermelidir.
* **FR-09:** Redis önbelleği, sık erişilen müşteri profillerini tutmalıdır.

### 5.4. Arama ve Raporlama (Analytics - Elasticsearch & Grafana)
* **FR-10:** Kullanıcılar, doğal dil ile (örn: "Geçen ay şikayet edenler") arama yapabilmelidir (Elasticsearch).
* **FR-11:** Yönetici paneli (Grafana), anlık veri akışını ve AI performansını görselleştirmelidir.

## 6. Teknik Gereksinimler (Non-Functional Requirements)

### 6.1. Performans ve Ölçeklenebilirlik
* **NFR-01 (Throughput):** Sistem saniyede 5.000 eşzamanlı isteği (RPS) karşılayabilmelidir. Bu durum **k6** yük testleri ile doğrulanacaktır.
* **NFR-02 (Latency):** Servisler arası iletişimde JSON yerine **gRPC (Protobuf)** kullanılarak veri serileştirme maliyeti minimize edilmelidir.
* **NFR-03 (Auto-Scaling):** Kubernetes HPA, CPU kullanımı %70'i aştığında otomatik olarak yeni pod başlatmalıdır.

### 6.2. Güvenilirlik ve Bakım (Reliability & Maintainability)
* **NFR-04 (IaC):** Altyapı kurulumu manuel yapılmamalı, **Terraform** scriptleri ile "Infrastructure as Code" prensibine uygun olarak versiyonlanmalıdır.
* **NFR-05 (Tracing):** Sistemdeki her işlem (Transaction) benzersiz bir `TraceID` taşımalı ve **Jaeger** üzerinden görselleştirilebilmelidir.

### 6.3. Kalite ve Güvenlik (DevSecOps)
* **NFR-06:** Kod kalitesi **SonarQube** Quality Gate'lerinden (Bugs: 0, Vulnerabilities: 0) geçmeden canlıya alınmamalıdır.
* **NFR-07:** Veritabanı şifreleri ve API anahtarları asla kod içinde (hardcoded) bulunmamalı, **HashiCorp Vault** üzerinden dinamik olarak çekilmelidir.

## 7. Kullanıcı Hikayeleri (User Stories - Örnek)

* **US-1:** *Bir Satış Temsilcisi olarak,* sisteme düşen yeni bir müşteri adayının (Lead) otomatik olarak analiz edilmesini ve bana bir özet sunulmasını istiyorum, *böylece* müşteriyi tanımak için saatlerce geçmiş mailleri okumak zorunda kalmam.
* **US-2:** *Bir Yönetici olarak,* hangi ürünle ilgili daha çok şikayet geldiğini ısı haritası (Heatmap) üzerinde görmek istiyorum, *böylece* ürün geliştirme ekibini uyarabilirim.

## 8. Varsayımlar ve Riskler
* **Risk:** LLM modelleri bazen yanlış bilgi (halüsinasyon) üretebilir.
    * *Mitigasyon:* RAG mimarisi ile cevaplar sadece şirket dokümanları ile sınırlandırılacaktır.
* **Varsayım:** Şirketin PDF ve Word formatındaki tüm dokümanları dijital ortamda erişilebilirdir.
