# Kaynaklar

Bu sayfa, rehberdeki her ana konunun **resmi LangSmith dokümantasyonundaki** karşılığına tek noktadan erişim sağlar.

!!! info "Neden her sayfada değil de burada?"
    Sayfa içlerine dağıtılmış onlarca link hem okuma akışını böler hem de resmi dokümantasyonun URL yapısı değiştiğinde bakımı zorlaştırır. Eşlemeyi tek bir yerde tutuyoruz — bkz. [LangGraph Türkçe Rehberi'ndeki](https://emineksknc.github.io/langgraph-turkce/kaynaklar/) aynı yaklaşım.

## Başlarken & Kavramlar

| Bu rehberde | Resmi kaynak |
|---|---|
| [Kurulum & API Key](baslangic/kurulum.md), [İlk Trace](baslangic/ilk-trace.md) | [Observability quickstart](https://docs.langchain.com/langsmith/observability-quickstart) |
| [Run, Trace, Thread, Trajectory](kavramlar/temel-terimler.md) | [Observability concepts](https://docs.langchain.com/langsmith/observability-concepts) |
| [Observability vs Evaluation](kavramlar/observability-vs-evaluation.md) | Resmi dokümanda ayrı bir sayfa yok — bu rehberin kendi kavramsal çerçevesi |

## Tracing

| Bu rehberde | Resmi kaynak |
|---|---|
| [Otomatik İzleme](tracing/otomatik-izleme.md) | [Annotate code for tracing](https://docs.langchain.com/langsmith/annotate-code) |
| [Metadata & Tag'ler](tracing/metadata-taglar.md) | [Add metadata and tags](https://docs.langchain.com/langsmith/add-metadata-tags) |
| [Filtreleme & Maskeleme](tracing/filtreleme-maskeleme.md) | [Filter traces](https://docs.langchain.com/langsmith/filter-traces-in-application), [Mask inputs/outputs](https://docs.langchain.com/langsmith/mask-inputs-outputs) |
| [Dashboard & Alerts](tracing/dashboard-alerts.md) | [Dashboards](https://docs.langchain.com/langsmith/dashboards), [Alerts](https://docs.langchain.com/langsmith/alerts) |

## Evaluation

| Bu rehberde | Resmi kaynak |
|---|---|
| [Dataset Oluşturma](evaluation/dataset-olusturma.md) | [Manage datasets programmatically](https://docs.langchain.com/langsmith/manage-datasets-programmatically) |
| [evaluate() ile Değerlendirme](evaluation/evaluate-fonksiyonu.md) | [Evaluate LLM applications](https://docs.langchain.com/langsmith/evaluate-llm-application) |
| [LLM-as-judge](evaluation/llm-as-judge.md) | [LLM-as-judge SDK](https://docs.langchain.com/langsmith/llm-as-judge-sdk) |
| [RAG Evaluation](evaluation/rag-evaluation.md) | Resmi dokümanda ayrı bir "RAG Evaluation" sayfası yok — [Evaluation concepts](https://docs.langchain.com/langsmith/evaluation-concepts) içindeki genel evaluator türlerine dayanır, bu rehberin kendi sentezi |
| [LangGraph Grafını Değerlendirme](evaluation/langgraph-degerlendirme.md) | Resmi dokümanda ayrı bir sayfa yok — bu rehberin LangGraph rehberiyle köprüsü |
| [Online Evaluation](evaluation/online-evaluation.md) | [Set up LLM-as-judge online evaluators](https://docs.langchain.com/langsmith/online-evaluations-llm-as-judge), [Set up online code evaluators](https://docs.langchain.com/langsmith/online-evaluations-code) |

## Prompts

| Bu rehberde | Resmi kaynak |
|---|---|
| [Prompt Hub](prompts/prompt-hub.md) | [Manage prompts programmatically](https://docs.langchain.com/langsmith/manage-prompts-programmatically) |

## İleri / Production

| Bu rehberde | Resmi kaynak |
|---|---|
| [Human Feedback & Annotation Queue](ileri-seviye/feedback-annotation.md) | [Annotation queues SDK](https://docs.langchain.com/langsmith/annotation-queues-sdk) |
| [CI/CD & Maliyet Takibi](ileri-seviye/cicd-maliyet.md) | Resmi dokümanda ayrı bir sayfa yok — bu rehberin kendi pratik önerileri |
| [Organizations, Erişim & Self-hosted Kararı](ileri-seviye/organizasyon-erisim.md) | [Administration overview](https://docs.langchain.com/langsmith/administration-overview), [Self-hosting with Docker](https://docs.langchain.com/langsmith/docker), [Deploy self-hosted full platform](https://docs.langchain.com/langsmith/deploy-self-hosted-full-platform), [Standalone Agent Servers](https://docs.langchain.com/langsmith/deploy-standalone-server) (kavram düzeyinde özetlenmiştir, deployment adımları hariç) |

## Kapsam dışı bıraktığımız konular

- **BYOC/Kubernetes self-hosted deployment adımları** — platform mühendisliğine ait, ayrı bir uzmanlık alanı
- **LLM Gateway** — ayrı bir ürün (model proxy/routing)
- **Fleet, Managed Deep Agents** — tamamen farklı ürünler (no-code agent builder)
- **Terraform ile altyapı yönetimi** — DevOps'a ait, sürekli değişen altyapı detayı

---

Resmi dokümantasyonun tamamı: [docs.langchain.com/langsmith](https://docs.langchain.com/langsmith)
