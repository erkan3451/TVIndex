# TVIndex - 02_Architecture.md

Version: 1.0  
Status: Draft

## 1. Amaç

TVIndex; televizyon modelleri, elektronik kartlar, paneller, servis dökümanları,
arıza bilgileri ve parça ilişkilerini tek bir bilgi platformunda toplayan modüler
bir sistemdir.

## 2. Tasarım İlkeleri

- Modüler Monolith
- API First
- Event Driven Jobs
- Source Traceability
- Versioned Data
- Horizontal Scalability
- AI Assisted Parsing

## 3. Üst Seviye Mimari

```text
                 Web Dashboard
                      │
                 REST API
                      │
               Service Layer
                      │
 ┌────────────────────────────────────┐
 │ Discovery │ Downloader │ Parser    │
 │ Knowledge │ Search     │ AI        │
 │ Images    │ Firmware   │ Import    │
 └────────────────────────────────────┘
                      │
      PostgreSQL / Redis / OpenSearch
                      │
          Object Storage (PDF, Images)
```

## 4. Modüller

### Discovery
- Yeni model keşfi
- Marka eklentileri
- Kaynak takibi
- Tekilleştirme

### Downloader
- Servis manual
- Kullanım kılavuzu
- Firmware
- Görseller

### Parser
- PDF metni
- Tablo çıkarımı
- Parça tanıma
- Metadata

### Knowledge
Merkezi ilişki katmanı.

İlişkiler:
- Brand → Model
- Model → Mainboard
- Model → Panel
- Model → Power Board
- Model → T-CON
- Model → LED Strip
- Board → IC
- IC → Datasheet

### Search
Desteklenen sorgular:
- Model
- Parça kodu
- Panel
- Şase
- Arıza açıklaması

### AI
- PDF yorumlama
- Eksik veri önerisi
- Benzer model önerisi
- Arıza olasılık analizi

## 5. Veri Akışı

1. Discovery model bulur.
2. Kuyruğa eklenir.
3. Downloader dosyaları indirir.
4. Parser teknik bilgiyi çıkarır.
5. Knowledge veritabanına işler.
6. Search index güncellenir.
7. AI ilişkileri güçlendirir.

## 6. Queue Yapısı

- discovery_queue
- download_queue
- parser_queue
- image_queue
- ai_queue
- reindex_queue

## 7. Depolama

PostgreSQL:
- İlişkisel veriler

Redis:
- Cache
- İş durumu

OpenSearch:
- Tam metin arama

Object Storage:
- PDF
- Görsel
- Firmware

## 8. API İlkeleri

- REST
- JSON
- JWT
- Rate Limit
- Pagination

Örnek:

GET /api/v1/models/LG/42LB580V

## 9. Güvenlik

- HTTPS
- JWT
- API Key
- Audit Log
- Günlük yedek

## 10. Ölçeklenebilirlik

Başlangıç hedefi:
- 100.000 model
- 1.000.000 parça ilişkisi

Mimari; yeni marka eklentileri ve yeni veri kaynaklarının kod tabanını bozmadan
eklenebilmesini hedefler.

## 11. Teknoloji

- Python
- FastAPI
- SQLAlchemy
- PostgreSQL
- Redis
- OpenSearch
- Playwright
- PyMuPDF
- Docker

## 12. Sonraki Doküman

03_Database.md:
- ER diyagramı
- Tablo yapıları
- İlişkiler
- İndeks stratejileri
- Veri bütünlüğü
