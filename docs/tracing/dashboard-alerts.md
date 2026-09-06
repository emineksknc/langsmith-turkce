# Dashboard & Alerts

<span class="badge badge-orta">🟡 ORTA SEVİYE</span>

Trace'ler tek tek incelemek için değerli, ama production'da asıl ihtiyacınız olan şey **toplu görünüm**: "genel olarak sistem nasıl gidiyor?"

## Yerleşik proje dashboard'u

Her LangSmith projesi, otomatik olarak şu metrikleri gösteren bir dashboard'a sahiptir:

- **Request hacmi** — zaman içinde kaç çağrı yapıldı
- **Latency (gecikme)** — p50/p95/p99 yüzdelik dilimler
- **Hata oranı** — başarısız run yüzdesi
- **Token kullanımı** — girdi/çıktı token sayıları, model bazında kırılım
- **Maliyet** — model fiyatlandırmasına göre otomatik hesaplanan tahmini maliyet

## Özel dashboard oluşturma

Belirli metadata/tag kombinasyonlarına göre özel bir görünüm oluşturmak için:

1. Projenizde **Dashboards** sekmesine gidin
2. Bir chart ekleyin, filtre olarak metadata/tag koşulu tanımlayın (ör. `metadata.model_versiyonu = "v2"`)
3. Birden fazla chart'ı tek bir dashboard'da gruplayarak, ör. "v1 vs v2 karşılaştırması" gibi bir görünüm oluşturun

## Alerts (uyarılar)

Belirli bir eşik aşıldığında otomatik bildirim almak için proje ayarlarından alert kurabilirsiniz:

| Alert türü | Tipik eşik | Ne zaman tetiklenir |
|---|---|---|
| Hata oranı | %5 üzeri | Son N dakikada hata oranı eşiği aşarsa |
| Latency | p95 > 10sn | Yavaşlama tespit edilirse |
| Maliyet | Günlük $X üzeri | Beklenmeyen maliyet artışı |
| Feedback skoru | Ortalama < 0.7 | Kullanıcı memnuniyeti düşerse (bkz. [Human Feedback](../ileri-seviye/feedback-annotation.md)) |

Alert'ler Slack/e-posta entegrasyonu ile bildirim gönderebilir — proje ayarlarından webhook URL'i eklemeniz yeterlidir.

!!! tip "Dashboard'u LangGraph node'larıyla ilişkilendirme"
    [LangGraph](https://emineksknc.github.io/langgraph-turkce/) uygulamalarında her node ayrı bir run olarak görünür (bkz. [Run, Trace, Thread, Trajectory](../kavramlar/temel-terimler.md)) — bu sayede dashboard'da "hangi node en çok zaman/maliyet harcıyor" sorusuna node adına göre filtreleyerek cevap bulabilirsiniz.

---

Tracing bölümü burada tamamlanıyor. Sıradaki bölüm: [Evaluation — Dataset Oluşturma](../evaluation/dataset-olusturma.md).
