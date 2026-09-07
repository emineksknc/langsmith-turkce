# Kurulum & API Key

<span class="badge badge-baslangic">🟢 BAŞLANGIÇ</span>

## Paket kurulumu

```bash
pip install -U langsmith
```

LangChain/LangGraph kullanıyorsanız ek bir paket gerekmez — `langchain`/`langgraph` zaten `langsmith` SDK'sına bağımlıdır.

## Hesap ve API key oluşturma

1. [smith.langchain.com](https://smith.langchain.com) üzerinden ücretsiz bir hesap oluşturun.
2. Settings → API Keys kısmından yeni bir API key üretin (`ls_...` ile başlar).

## Ortam değişkenleri

```bash title=".env"
LANGSMITH_TRACING=true
LANGSMITH_API_KEY=ls_...
LANGSMITH_PROJECT=ilk-projem
```

!!! note "Eski isimler hâlâ çalışıyor"
    Daha önce `LANGCHAIN_TRACING_V2=true` ve `LANGCHAIN_API_KEY` kullanılıyordu — bunlar hâlâ desteklenir (LangChain/LangGraph dokümantasyonunda sık görürsünüz), ama yeni projelerde `LANGSMITH_*` öneki tercih edilmelidir.

`LANGSMITH_PROJECT`, trace'lerinizin hangi proje altında gruplanacağını belirler — belirtilmezse `"default"` kullanılır. Farklı ortamlar (dev/staging/prod) için farklı proje adları kullanmanız önerilir (bkz. [Metadata & Tag'ler](../tracing/metadata-taglar.md)).

## Kurulumu doğrulama

```python
from langsmith import Client

client = Client()
print("LangSmith bağlantısı hazır ✔")
```

Hata almadıysanız hazırsınız — sıradaki adım: [Yerel Geliştirme Ortamının Kurulması](yerel-kurulum.md) ile bilgisayarında baştan sona çalışan bir ortam kur.
