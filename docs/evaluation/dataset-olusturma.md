# Dataset Oluşturma

<span class="badge badge-orta">🟡 ORTA SEVİYE</span>

Bir **dataset**, sabit bir soru/girdi kümesidir — üzerinde tekrar tekrar değerlendirme çalıştırarak "değişikliğim kaliteyi etkiledi mi?" sorusunu tutarlı şekilde cevaplarsınız.

## Elle, liste halinde oluşturma

```python
from langsmith import Client

client = Client()

dataset = client.create_dataset(
    dataset_name="musteri-sorulari-v1",
    description="Sık sorulan müşteri destek soruları ve beklenen cevaplar",
)

examples = [
    {
        "inputs": {"soru": "İade süresi kaç gün?"},
        "outputs": {"beklenen": "14 gün"},
        "metadata": {"kategori": "iade"},
    },
    {
        "inputs": {"soru": "Kargo ücreti ne kadar?"},
        "outputs": {"beklenen": "500 TL üzeri ücretsiz"},
        "metadata": {"kategori": "kargo"},
    },
]

client.create_examples(dataset_id=dataset.id, examples=examples)
```

`create_examples` (çoğul), birden fazla örneği **tek istekte** ekler — çok sayıda örnek eklerken tercih edilmelidir. Tek bir örnek eklemek için `create_example` (tekil) kullanılır.

## Gerçek trace'lerden dataset oluşturma

[Dashboard & Alerts](../tracing/dashboard-alerts.md)'te bahsedilen "production'dan örnekleme" pratiğini burada uygularsınız:

```python
# Production'da hata veren veya düşük skorlu run'ları bul
runlar = client.list_runs(
    project_name="musteri-botu-prod",
    is_root=True,
    error=False,
)

dataset = client.create_dataset("production-ornekleri", description="Gerçek kullanıcı sorularından derlenmiş")

examples = [{"inputs": run.inputs, "outputs": run.outputs} for run in runlar]
client.create_examples(dataset_id=dataset.id, examples=examples)
```

Bu, dataset'inizin zamanla gerçek kullanıcı davranışına daha çok benzemesini sağlar — bkz. [Observability vs Evaluation](../kavramlar/observability-vs-evaluation.md)'daki "pratik döngü".

## CSV'den yükleme

Elinizde zaten bir soru-cevap tablosu (CSV) varsa, UI üzerinden **Datasets → New Dataset → Upload CSV** ile de yükleyebilirsiniz — sütun adlarını girdi/çıktı alanlarıyla eşleştirmeniz yeterlidir.

## Dataset türleri

| Tür | Ne zaman kullanılır |
|---|---|
| **KV (key-value)** | Genel amaçlı, esnek girdi/çıktı yapıları — varsayılan |
| **LLM** | Tek bir prompt/completion çifti değerlendirilecekse |
| **Chat** | Çok turlu konuşma geçmişi değerlendirilecekse |

---

Sıradaki adım: [evaluate() ile Toplu Değerlendirme](evaluate-fonksiyonu.md).
