# CI/CD & Maliyet Takibi

<span class="badge badge-ileri">🔴 İLERİ / SENIOR</span>

## CI/CD'ye entegre değerlendirme

[evaluate()](../evaluation/evaluate-fonksiyonu.md), normal bir Python fonksiyonu olduğu için `pytest` içinde doğrudan kullanılabilir — her pull request'te kaliteyi otomatik doğrulamak için:

```python
import pytest
from langsmith import Client

def test_musteri_botu_kalite_regresyonu():
    client = Client()
    sonuclar = client.evaluate(
        hedef_fonksiyon,
        data="musteri-sorulari-v1",
        evaluators=[dogruluk_yargici],
        experiment_prefix="ci-test",
    )
    ortalama_skor = sonuclar.to_pandas()["feedback.dogruluk_yargici"].mean()
    assert ortalama_skor >= 0.85, f"Kalite eşiğinin altında: {ortalama_skor}"
```

Bu testi GitHub Actions'a eklemek, [LangGraph rehberindeki proje yapısı](https://emineksknc.github.io/langgraph-turkce/ileri-seviye/proje-yapisi/)nda önerilen `tests/` klasörüne doğal olarak oturur:

```yaml title=".github/workflows/kalite-testi.yml"
name: Kalite Regresyon Testi
on: [pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.11"
      - run: pip install -r requirements.txt
      - run: pytest tests/test_kalite.py
        env:
          LANGSMITH_API_KEY: ${{ secrets.LANGSMITH_API_KEY }}
          LANGSMITH_TRACING: true
```

!!! warning "Her PR'da gerçek LLM çağrısı = maliyet"
    Bu testler gerçek LLM çağrıları içerir — [LangGraph rehberindeki test katmanları](https://emineksknc.github.io/langgraph-turkce/orta-seviye/testing/)nda "Katman 4" olarak adlandırılan, en pahalı test katmanıdır. Her PR'da değil, `main` branch'e merge öncesi ya da günlük olarak çalıştırmak daha maliyet-etkin olabilir.

## Maliyet takibi

Her LLM run'ı, model fiyatlandırmasına göre otomatik olarak maliyet hesaplar — [Dashboard](../tracing/dashboard-alerts.md)'da model/proje bazında kırılım görebilirsiniz.

### Programatik maliyet sorgulama

```python
from langsmith import Client

client = Client()

runlar = client.list_runs(project_name="musteri-botu-prod", run_type="llm")
toplam_maliyet = sum(run.total_cost or 0 for run in runlar)
print(f"Toplam maliyet: ${toplam_maliyet:.4f}")
```

### Maliyet metadata'sı ile kırılım

[Metadata & Tag'ler](../tracing/metadata-taglar.md)'de gösterilen yaklaşımla, maliyeti kullanıcı/özellik bazında kırmak için metadata ekleyin:

```python
llm.invoke("soru", config={"metadata": {"ozellik": "iade-akisi", "musteri_plani": "premium"}})
```

Sonra dashboard'da `metadata.ozellik = "iade-akisi"` filtresiyle sadece o özelliğin maliyetini görebilirsiniz.

### Model routing kararlarını maliyetle doğrulama

Küçük/büyük model routing yapıyorsanız (ör. basit sorular için `gpt-4o-mini`, karmaşık sorular için `gpt-4o`), bu iki grubun maliyet ve kalite farkını [evaluate()](../evaluation/evaluate-fonksiyonu.md) ile karşılaştırarak routing eşiğinizin doğru yerde olduğunu periyodik olarak doğrulayın.

---

Sıradaki adım: [Organizations, Erişim & Self-hosted Kararı](organizasyon-erisim.md).
