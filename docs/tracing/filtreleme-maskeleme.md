# Filtreleme & Hassas Veri Maskeleme

<span class="badge badge-orta">🟡 ORTA SEVİYE</span>

Trace hacmi büyüdükçe iki farklı ihtiyaç ortaya çıkar: **belirli trace'leri bulmak** (filtreleme) ve **hassas veriyi hiç göndermemek** (maskeleme).

## Trace filtreleme — SDK ile sorgulama

```python
from langsmith import Client

client = Client()

# Belirli bir projede, hata veren run'ları listele
hatali_runlar = client.list_runs(
    project_name="musteri-botu-prod",
    error=True,
)

# Belirli bir metadata değerine göre filtrele
kullanici_runlari = client.list_runs(
    project_name="musteri-botu-prod",
    filter='has(metadata, \'{"kullanici_id": "u123"}\')',
)

# Yalnızca kök run'ları (tam trace'leri) getir
tum_traceler = client.list_runs(
    project_name="musteri-botu-prod",
    is_root=True,
)
```

`filter` parametresi, LangSmith'in kendi sorgu dilini kullanır — UI'daki arama çubuğuna yazdığınız ifadelerle birebir aynıdır; UI'da bir filtre kurup "sorguyu kopyala" ile SDK'da kullanacağınız ifadeyi alabilirsiniz.

## UI'da hızlı filtreleme

Dashboard'da en sık kullanılan filtreler:

- `is:error` — hata veren run'lar
- `latency>5` — 5 saniyeden uzun süren run'lar
- `tag:production` — belirli bir tag'e sahip run'lar

## Hassas veri maskeleme

### Tamamen gizleme

```bash
LANGSMITH_HIDE_INPUTS=true
LANGSMITH_HIDE_OUTPUTS=true
```

Bu, **tüm** trace'lerin girdi/çıktısını LangSmith'e hiç göndermez — sadece metadata (süre, hata durumu, token sayısı) kalır. Sıfır-tutma (zero-retention) politikası olan müşteriler için uygundur.

### Seçici maskeleme — Client seviyesinde

```python
from langsmith import Client
from langsmith.wrappers import wrap_openai
import openai

langsmith_client = Client(
    hide_inputs=lambda inputs: {},
    hide_outputs=lambda outputs: {},
)

openai_client = wrap_openai(openai.Client())
openai_client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "Hassas bilgi içeren mesaj"}],
    langsmith_extra={"client": langsmith_client},
)
```

Bu yaklaşımla, hangi çağrıların maskeleneceğini **programatik olarak** seçebilirsiniz — ör. sadece belirli bir müşteri segmentinin verisini gizlemek gibi.

### Kural bazlı maskeleme — anonymizer

Regex tabanlı, belirli kalıpları (e-posta, telefon, kredi kartı gibi) otomatik maskelemek için:

```python
from langsmith import Client

client = Client(
    anonymizer=lambda data: {
        **data,
        "email": "***@***.com" if "email" in data else data,
    }
)
```

!!! warning "Hangi yöntemi seçmeliyim?"
    - **Tüm hassas veriyi hiç göndermeyeceksen** → `LANGSMITH_HIDE_INPUTS/OUTPUTS`
    - **Belirli alanları maskeleyip geri kalanını görmek istiyorsan** → `anonymizer`
    - **Belirli çağrıları koşullu olarak gizlemek istiyorsan** → `hide_inputs`/`hide_outputs` fonksiyonları

## Neyi maskelemeli, neyi maskelememelisin?

| ❌ Maskelenmeli | ✅ Güvenle bırakılabilir |
|---|---|
| T.C. kimlik no, pasaport no | Trace metadata (proje adı, ortam) |
| E-posta, telefon, adres | Model versiyonu |
| API key, access token, şifre | Latency, token kullanımı |
| Kullanıcıya özel finansal/sağlık bilgisi | Hata mesajı tipi (içeriği değil) |

!!! danger "Trace edebilmek ≠ her şeyi trace etmek"
    Maskeleme, sadece "LangSmith'e ne gönderiyorum" sorusuyla sınırlı değildir — uygulamanızın **tüm loglama/tracing katmanının** (kendi log dosyalarınız, üçüncü parti APM araçları dahil) bu prensiple tasarlanması gerekir. LangSmith'te maskelediğiniz bir veriyi başka bir logda maskelemeden bırakmak, sorunu çözmez, sadece taşır.

---

Sıradaki adım: [Dashboard & Alerts](dashboard-alerts.md).
