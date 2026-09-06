# Hızlı Referans Tablosu

!!! tip "PDF olarak indir"
    Bu tablonun ve ilgili konuların özet kartları: [🟢 Başlangıç](../assets/cheatsheets/langsmith-baslangic-cheatsheet.pdf) · [🟡 Orta Seviye](../assets/cheatsheets/langsmith-orta-seviye-cheatsheet.pdf) · [🔴 İleri Seviye](../assets/cheatsheets/langsmith-ileri-seviye-cheatsheet.pdf)

| Kavram | Ne işe yarar | Import / Kullanım |
|---|---|---|
| `LANGSMITH_TRACING` | İzlemeyi açar | Ortam değişkeni (`true`/`false`) |
| `LANGSMITH_API_KEY` | Kimlik doğrulama | Ortam değişkeni |
| `LANGSMITH_PROJECT` | Trace'lerin gruplanacağı proje | Ortam değişkeni |
| `@traceable` | Fonksiyonu izlenebilir yapar | `langsmith` |
| `wrap_openai` | OpenAI istemcisini otomatik izler | `langsmith.wrappers` |
| `Client` | LangSmith API'sine erişim | `langsmith` |
| `client.create_dataset` | Dataset oluşturur | `Client` metodu |
| `client.create_examples` | Dataset'e toplu örnek ekler | `Client` metodu |
| `client.evaluate` / `client.aevaluate` | Dataset üzerinde toplu değerlendirme | `Client` metodu |
| `client.list_runs` | Trace/run sorgulama, filtreleme | `Client` metodu |
| `client.create_feedback` | Bir run'a insan/model geri bildirimi ekler | `Client` metodu |
| `client.create_feedback_config` | Organizasyon çapında feedback şeması tanımlar | `Client` metodu |
| `client.create_annotation_queue` | İnceleme kuyruğu oluşturur | `Client` metodu |
| `client.push_prompt` / `client.pull_prompt` | Prompt Hub'a gönder / oradan çek | `Client` metodu |
| `hide_inputs` / `hide_outputs` | Hassas veriyi maskeler | `Client` parametresi |
| `anonymizer` | Kural bazlı (regex) maskeleme | `Client` parametresi |
| `experiment_prefix` | Bir değerlendirme çalıştırmasını adlandırır | `evaluate()` parametresi |
| Automation Rule | Filtre + örnekleme + aksiyon (online eval, annotation queue'ya ekleme vb.) | UI üzerinden yapılandırılır |

## Sık yapılan hatalar

!!! failure "Her invoke'ta aynı thread_id kullanmak (evaluation sırasında)"
    [LangGraph grafını değerlendirirken](../evaluation/langgraph-degerlendirme.md) her test örneği için farklı bir `thread_id` kullanmazsanız, checkpointer sayesinde ardışık örnekler birbirinin konuşma geçmişini görür ve sonuçlar kirlenir.

!!! failure "pull_prompt'u node içinde her seferinde çağırmak"
    [Prompt Hub](../prompts/prompt-hub.md)'dan her node çalıştığında prompt çekmek, gereksiz ağ gecikmesi ekler ve async node'larda event loop'u bloke edebilir — uygulama başlangıcında bir kez çekip önbelleğe alın.

!!! failure "Tüm production trafiğini %100 online evaluation'a sokmak"
    [Online Evaluation](../evaluation/online-evaluation.md)'da yüksek örnekleme oranı hem maliyeti hem de extended data retention nedeniyle veri saklama maliyetini artırır — küçük bir örneklemle başlayın.

!!! failure "String eşleştirmeyle 'doğruluk' ölçmek"
    `"beklenen" in cevap` gibi basit string kontrolleri, anlamca doğru ama farklı ifade edilmiş cevapları yanlış olarak işaretler — bkz. [LLM-as-judge](../evaluation/llm-as-judge.md).

---

*Bu sayfa canlı bir referanstır — yeni öğrendiğin bir detayı PR ile ekleyebilirsin.*
