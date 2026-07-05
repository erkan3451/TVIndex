# TVIndex Architecture

Version: 1.0
Status: Draft

---

# 1. Genel Bakış

TVIndex;

- Televizyon modellerini keşfeden
- Teknik dökümanları toplayan
- PDF'leri analiz eden
- Parça ilişkilerini çıkaran
- Arızaları ilişkilendiren
- API üzerinden sunan

merkezi bir bilgi platformudur.

TVIndex tek bir uygulama değildir.

TVIndex;

Crawler +
Parser +
Knowledge Database +
Search +
AI

sistemlerinin birleşimidir.

---

# 2. Mimari

                    Dashboard
                         │
                  REST API / GraphQL
                         │
                Service Layer
                         │
──────────────────────────────────────────────

Discovery Module

Downloader Module

Parser Module

Knowledge Module

Search Module

AI Module

Image Module

Firmware Module

Fault Module

Import / Export Module

──────────────────────────────────────────────

PostgreSQL

OpenSearch

Redis

Object Storage

──────────────────────────────────────────────

Logs

Backups

Monitoring
