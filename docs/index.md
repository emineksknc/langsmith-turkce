# LangSmith Türkçe Rehber

Bu site, [LangSmith](https://docs.langchain.com/langsmith) — LLM/ajan uygulamaları için observability (izlenebilirlik) ve evaluation (değerlendirme) platformu — hakkında **sıfırdan senior seviyeye** kadar hazırlanmış, Türkçe kapsamlı bir kaynaktır.

> **Özetle:** LangSmith, bir LLM uygulamasının her çalıştırmasını (trace) kaydeden, bu çalıştırmaları filtreleyip inceleyebildiğin, ve uygulamanın kalitesini sabit test setleri (dataset) üzerinde ölçebildiğin bir platformdur — "üretimde ne oluyor?" ve "değişikliğim kaliteyi bozdu mu?" sorularının cevabı burada.

!!! info "Neden bu site?"
    LangSmith'in resmi dokümantasyonu geniş bir ürün ailesini (Deployment, Fleet, LLM Gateway, Managed Deep Agents gibi kurumsal/altyapı özellikleri dahil) kapsıyor. Bu site, **bir geliştiricinin günlük ihtiyaç duyacağı çekirdek konulara** — tracing, evaluation, prompt yönetimi — odaklanıyor. Bağımsız bir öğretim kaynağıdır, LangChain Inc. ile bağlantılı değildir.

!!! warning "Sürüm notu"
    Bu rehber güncel LangSmith SDK'sı (`langsmith` Python paketi) esas alınarak hazırlanmıştır. Ortam değişkenleri için hem yeni (`LANGSMITH_TRACING`, `LANGSMITH_API_KEY`) hem eski (`LANGCHAIN_TRACING_V2`, `LANGCHAIN_API_KEY`) isimler hâlâ çalışır — bu rehberde yeni isimler kullanılıyor.

!!! abstract "Yeni bir terimle mi karşılaştın?"
    Her terim ilk geçtiği sayfada kısaca (ve orijinal İngilizce karşılığıyla) açıklanıyor. Hepsinin toplu listesi için: [Sözlük](sozluk.md).

## Bu rehber neyi kapsıyor, neyi kapsamıyor?

**Kapsıyor:** Tracing (izleme), Evaluation (değerlendirme), Dataset yönetimi, Prompt Hub, temel Human Feedback/Annotation, CI/CD entegrasyonu, [LangGraph](https://emineksknc.github.io/langgraph-turkce/) uygulamalarını LangSmith ile izleme — bir AI/ML mühendisinin günlük ihtiyaç duyacağı çekirdek.

**Kapsamıyor (bilinçli olarak):** BYOC/Kubernetes self-hosted deployment adımları, LLM Gateway, Fleet, Managed Deep Agents, Terraform ile altyapı yönetimi — bunlar platform/DevOps mühendisliğine ait, ayrı bir uzmanlık alanı. Organizasyon/erişim kontrolü ve self-hosted **kararı** (nasıl kurulacağı değil, ne zaman gerektiği) [İleri / Production](ileri-seviye/organizasyon-erisim.md) bölümünde kavram düzeyinde ele alınıyor.

## Sıfırdan senior'a okuma sırası

1. 🟢 [Kurulum & API Key](baslangic/kurulum.md)
2. 🟢 [İlk Trace](baslangic/ilk-trace.md)
3. 🟢 [Run, Trace, Thread, Trajectory](kavramlar/temel-terimler.md)
4. 🟢 [Observability vs Evaluation](kavramlar/observability-vs-evaluation.md)
5. 🟡 [Otomatik İzleme (@traceable)](tracing/otomatik-izleme.md)
6. 🟡 [Metadata & Tag'ler](tracing/metadata-taglar.md)
7. 🟡 [Filtreleme & Hassas Veri Maskeleme](tracing/filtreleme-maskeleme.md)
8. 🟡 [Dashboard & Alerts](tracing/dashboard-alerts.md)
9. 🟡 [Dataset Oluşturma](evaluation/dataset-olusturma.md)
10. 🟡 [evaluate() ile Toplu Değerlendirme](evaluation/evaluate-fonksiyonu.md)
11. 🔴 [LLM-as-judge Evaluator Yazma](evaluation/llm-as-judge.md)
12. 🔴 [LangGraph Grafını Değerlendirme](evaluation/langgraph-degerlendirme.md)
13. 🔴 [Online Evaluation](evaluation/online-evaluation.md)
14. 🔴 [Prompt Hub](prompts/prompt-hub.md)
15. 🔴 [Human Feedback & Annotation Queue](ileri-seviye/feedback-annotation.md)
16. 🔴 [CI/CD & Maliyet Takibi](ileri-seviye/cicd-maliyet.md)
17. 🔴 [Organizations, Erişim & Self-hosted Kararı](ileri-seviye/organizasyon-erisim.md)
18. 🔴 [Örnek Proje — LangGraph Botunu İzleme & Değerlendirme](ornek-proje/langgraph-botu-izleme.md)

!!! tip "Öğrendiklerini test et"
    Her seviye için açılır-kapanır soru-cevap setleri: [Başlangıç](alistirmalar/baslangic-sorulari.md) · [Orta Seviye](alistirmalar/orta-seviye-sorulari.md) · [İleri Seviye](alistirmalar/ileri-seviye-sorulari.md)

## İndirilebilir Cheatsheet'ler (PDF)

Her seviye için, çevrimdışı da kullanabileceğin özet referans kartları:

<div class="grid cards" markdown>

- :material-file-pdf-box: **🟢 Başlangıç Cheatsheet**
  Kurulum, ilk trace, temel terimler, Observability vs Evaluation.
  [PDF indir](assets/cheatsheets/langsmith-baslangic-cheatsheet.pdf){ .md-button }

- :material-file-pdf-box: **🟡 Orta Seviye Cheatsheet**
  Metadata/Tag, filtreleme/maskeleme, dashboard/alerts, dataset, evaluate().
  [PDF indir](assets/cheatsheets/langsmith-orta-seviye-cheatsheet.pdf){ .md-button }

- :material-file-pdf-box: **🔴 İleri Seviye Cheatsheet**
  LLM-as-judge, online evaluation, Prompt Hub, feedback, CI/CD, organizasyon.
  [PDF indir](assets/cheatsheets/langsmith-ileri-seviye-cheatsheet.pdf){ .md-button }

</div>

## LangGraph Türkçe Rehberi ile ilişkisi

Bu site, [LangGraph Türkçe Rehberi](https://emineksknc.github.io/langgraph-turkce/)'nin doğal devamıdır — orada birden fazla yerde "LangSmith rehberi ayrı planlanıyor" notu vardı, bu site o notu karşılıyor. [Örnek Proje](ornek-proje/langgraph-botu-izleme.md) sayfası, LangGraph rehberindeki müşteri destek botunu doğrudan bu siteki tekniklerle izliyor ve değerlendiriyor.

## Katkıda bulunmak ister misin?

Bu site açık kaynak. Bir hata bulursan, eksik bir konu görürsen [GitHub reposundan](https://github.com/emineksknc/langsmith-turkce) pull request açabilirsin.

---

*LangSmith, LangChain Inc. tarafından geliştirilen bir platformdur. Kullanım şartları ve fiyatlandırma için [resmi site](https://www.langchain.com/langsmith)'yi ziyaret edin.*
