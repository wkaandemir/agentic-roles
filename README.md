# Agentik Roller

Yazilim muhendisligi, guvenlik analizi, kalite guvencesi ve dokumantasyon isleri icin YZ (Yapay Zeka) agent rollerini tanimlayan ve uzmanlasmis is akislarini orkestre eden YAML tabanli bir konfigurasyon yapisi.

## Genel Bakis

Bu depo, uzmanlasmis YZ agent'larini ve kontrol is akislarini tanimlayan 9 adet agent tanim dosyasi icerir. Her agent, yeteneklerini, sorumluluklarini ve calisma modelini aciklayan YAML spesifikasyonlari ile tanimlanir.

**Temel ozellikler:**
- **Konfigurasyon odakli**: Sadece YAML dosyalari, uygulama kodu yok
- **Duz yapi**: Tum dosyalar kok dizinde bulunur
- **Iki agent tipi**: Kontrol agent'lari (orkestratorler) ve Fonksiyonel agent'lar (uzmanlar)
- **Is akisi odakli**: Sistematik muhendislik ve guvenlik surecleri icin tasarlanmistir

## Hizli Referans

### Kontrol Agent'lari (Is Akisi Orkestratorleri)

| Dosya | Amac |
|------|------|
| `cyber-security-audit-request.yaml` | Birlesik siber guvenlik denetimi (sistemler + kod tabani + agent/prompt is akislar) |
| `code-review-request.yaml` | Kapsamli kod inceleme otomasyonu |
| `post-implementation-self-audit-request.yaml` | Uygulama sonrasi oz-denetim |
| `quality-engineering-request.yaml` | Kalite muhendisligi stratejisi |
| `root-cause-analysis-request.yaml` | Kok neden analizi (RCA) |
| `seo-optimization-request.yaml` | SEO optimizasyon analizi |

### Fonksiyonel Agent'lar (Uzman Roller)

| Dosya | Amac |
|------|------|
| `prd-writer.yaml` | Urun Gereksinim Dokumani (PRD) yazimi |
| `docs-maintainer.yaml` | Dokumantasyon uretimi ve bakimi |
| `test-writer.yaml` | Test yazimi |

## Agent Dosya Yapisi

Her agent YAML dosyasi:
- YAML on bolum (en az `name` ve `description`) icerir.
- Ardindan Markdown govde gelir: baslik, gorev/gereksinim bolumleri, tek TODO dosyasina cikti kurali, cikti iskeleti ve kalite kontrol listesi.
- Sonda, `TODO_<agent-name>.md` adinda tek bir cikti dosyasi uretmeyi zorunlu kilan bir **RULE** bulunur.

```yaml
---
name: [agent-kimligi]
description: [tek satir ozet]
---

# [Baslik]
```

## Kontrol Agent Icerik Deseni

Kontrol agent'lari genellikle su bolumleri icerir:

1. **Gereksinim/Gorev bolumleri**: Guvenlik, performans, dogruluk vb. alanlara gore gruplanmis is maddeleri
2. **Tek cikti dosyasi kurali**: Tum ciktilar tek bir dosyada toplanir (`TODO_<agent-name>.md`)
3. **Cikti iskeleti**: TODO icerigini standartlastiran sablon/bicim
4. **Kalite kontrol listesi**: Kanit standardi ve dogrulama kriterleri
5. **Ek odak alanlari**: Modern pratikler ve uyumluluk konulari

## Adlandirma Konvansiyonlari

**Birincil kural:** YAML dosya adi, YAML on bolumundeki `name` degeriyle birebir eslesmeli ve `.yaml` ile bitmelidir.

| Kalip | Anlam | Ornek |
|------|-------|-------|
| `*-request.yaml` | Kontrol agent'i / is akisi istegi | `code-review-request.yaml` |
| `*-writer.yaml` | Icerik uretimi | `prd-writer.yaml`, `test-writer.yaml` |
| `*-maintainer.yaml` | Bakim | `docs-maintainer.yaml` |

## Kullanim

Agent'lar YAML on bolum icindeki `name` alani ile cagrilir. `description` alani ise agent'in ne zaman kullanilacagini kisa sekilde anlatir.

`prd-writer.yaml` icin ornek:
```yaml
---
name: prd-writer
description: Kapsamli bir Urun Gereksinim Dokumani (PRD) uret.
---
```

## Icerik Kalite Skorkarti

Bu tablo, **icerik yeterliligi** ve **icerik kalitesi** icin (yapisal/format uyumundan bagimsiz) kurum-ici, oznel bir puanlamadir. Tarih: **2026-02-07**.

- **Yeterlilik**: Ek karar gerektirmeden agent'i calistirip beklenen ciktiyi uretecek kadar yonlendirme var mi?
- **Kalite**: Netlik, eyleme donukluk, tutarlilik, olculebilirlik, gereksiz tekrar ve asiri uzunluktan kacisma.

| Dosya | Yeterlilik | Kalite | Notlar |
|---|---:|---:|---|
| `code-review-request.yaml` | 10/10 | 9/10 | Cok kapsamli; sure siniri konmazsa odak dagitabilir. |
| `cyber-security-audit-request.yaml` | 10/10 | 9/10 | Cok kapsamli; agir ama uygulanabilir. |
| `post-implementation-self-audit-request.yaml` | 10/10 | 9/10 | Kanit/QA disiplini guclu; cikti beklentisi net. |
| `quality-engineering-request.yaml` | 10/10 | 9/10 | Olculebilir strateji ve kalite kapilari vurgusu iyi. |
| `root-cause-analysis-request.yaml` | 10/10 | 9/10 | Kanit-oncelikli RCA iskeleti guclu. |
| `seo-optimization-request.yaml` | 10/10 | 9/10 | Teknik + yol haritasi beklentisi net; kapsam genis. |
| `prd-writer.yaml` | 9/10 | 9/10 | Cikti bicimi guclu; opsiyonel yayina alma plani bolumu eklenebilir. |
| `docs-maintainer.yaml` | 9/10 | 9/10 | Cikti bicimi + QA guclu; daha fazla ornek teslimatla 10 olabilir. |
| `test-writer.yaml` | 9/10 | 9/10 | Plan/senaryo/komutlar net; repo-ozel orneklerle 10 olabilir. |
