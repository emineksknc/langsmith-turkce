# Orta Seviye Soruları

<span class="badge badge-orta">🟡 ORTA SEVİYE</span>

Bu sorular [Tracing](../tracing/otomatik-izleme.md) ve [Dataset/evaluate() temelleri](../evaluation/dataset-olusturma.md) konularını test eder.

??? question "1. Metadata ile Tag arasındaki yapısal fark nedir, ne zaman hangisi tercih edilir?"
    Metadata anahtar-değer (dict) yapısındadır ve yapılandırılmış bilgi (kullanıcı ID, model versiyonu) taşır. Tag, düz string listesidir ve hızlı, basit kategorileme (`production`, `staging`) için kullanılır. Spesifik bir değere göre filtreleme gerekiyorsa metadata, hızlı içerme kontrolü yeterliyse tag tercih edilir.

??? question "2. LangGraph'ta bir node'a metadata eklemek için hangi mekanizma kullanılır?"
    `config` nesnesi — `config={"metadata": {...}, "tags": [...]}`. Bu, LangGraph'ta zaten [kullanıcı kimliği geçirmek için kullanılan](https://emineksknc.github.io/langgraph-turkce/orta-seviye/context-config/) `RunnableConfig` ile aynı nesnedir.

??? question "3. `LANGSMITH_HIDE_INPUTS=true` ile `Client(hide_inputs=lambda inputs: {})` arasındaki fark nedir?"
    Ortam değişkeni **tüm** trace'lerin girdisini koşulsuz gizler. `Client` üzerindeki `hide_inputs` fonksiyonu ise **programatik olarak seçici** davranmanızı sağlar — hangi çağrıların maskeleneceğine kod içinde karar verebilirsiniz.

??? question "4. Bir dataset'e tek bir örnek eklemekle 100 örnek eklemek için hangi metodları kullanmalısınız?"
    Tek örnek için `create_example` (tekil), çok sayıda örnek için `create_examples` (çoğul) — çoğul metod, örnekleri **tek bir istekte** toplu ekler, tek tek `create_example` çağırmaktan çok daha verimlidir.

??? question "5. Production trace'lerinden bir dataset oluşturmanın somut faydası nedir?"
    Dataset'in zamanla gerçek kullanıcı davranışına daha çok benzemesini sağlar — sadece hayal edilen senaryolar değil, gerçekten karşılaşılan sorular test setine girer. Bu, [Observability vs Evaluation](../kavramlar/observability-vs-evaluation.md)'daki "pratik döngü"nün temelidir.

??? question "6. `evaluate()`'e verilen target fonksiyon tam olarak ne yapar?"
    Dataset'in her bir örneğinin girdisini (`inputs`) alır ve uygulamanızın (LLM çağrısı, LangGraph app'i, vb.) o girdiye verdiği çıktıyı döndürür — `evaluate()` bu fonksiyonu dataset'teki her örnek için otomatik çağırır.

??? question "7. Bir evaluator fonksiyonu hangi üç parametreyi alabilir?"
    `inputs` (dataset girdisi), `outputs` (uygulamanın ürettiği gerçek çıktı), `reference_outputs` (dataset'teki beklenen çıktı, varsa). Bir skor (bool, float, vb.) döndürür.

??? question "8. `experiment_prefix` parametresi neden önemlidir?"
    Aynı dataset üzerinde yapılan farklı değerlendirme çalıştırmalarını (ör. `v1-deneme`, `v2-deneme`) birbirinden ayırt etmenizi sağlar — bu isimlendirme olmadan hangi sonucun hangi denemeye ait olduğunu UI'da karıştırırsınız."

??? question "9. `evaluate()` çağrısı sırasında target fonksiyonun içindeki `@traceable` alt fonksiyonları nereye kaydedilir?"
    Ana projenizin genel run listesine değil, **dataset'in Examples → Linked Traces** kısmına — bu ayrım, production trace'leri ile deneysel evaluation trace'lerinin karışmamasını sağlar.

??? question "10. Target fonksiyonunuz `async def` ise `evaluate()` yerine ne kullanmalısınız?"
    `aevaluate()` — aynı parametreleri alan asenkron karşılığıdır (`client.aevaluate(...)`, `await` ile çağrılır).

---

Bir önceki seviyeye dönmek için: [Başlangıç Soruları](baslangic-sorulari.md) · Sıradaki seviye: [İleri Seviye Soruları](ileri-seviye-sorulari.md)
