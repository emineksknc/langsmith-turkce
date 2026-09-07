# Yerel Geliştirme Ortamının Kurulması

<span class="badge badge-baslangic">🟢 BAŞLANGIÇ</span>

[Kurulum & API Key](kurulum.md)'de LangSmith hesabını ve API key'i hazırladık. Bu sayfada, kendi bilgisayarında **baştan sona çalışan** bir Python ortamı kurup ilk trace'i gönderiyoruz.

!!! warning "LangSmith'i bilgisayarına kurmuyorsun"
    Bu sayfada anlatılan **LangSmith Cloud**'dur — bilgisayarında bir LangSmith sunucusu çalıştırmıyorsun. Bilgisayarında sadece kendi Python uygulaman (LangChain/LangGraph kodun) çalışıyor; bu uygulama, ürettiği trace'leri internet üzerinden LangSmith'in sunucularına gönderiyor. Kendi sunucunda LangSmith çalıştırmak (self-hosted) tamamen ayrı bir konudur — bkz. [Organizations, Erişim & Self-hosted Kararı](../ileri-seviye/organizasyon-erisim.md).

## 1. Sanal ortam oluştur

```bash
mkdir ilk-langsmith-projem && cd ilk-langsmith-projem
python -m venv .venv
```

Aktive et:

=== "macOS / Linux"

    ```bash
    source .venv/bin/activate
    ```

=== "Windows"

    ```powershell
    .venv\Scripts\activate
    ```

## 2. Paketleri kur

```bash
pip install -U langsmith langchain langgraph python-dotenv
```

## 3. .env dosyasını oluştur

```bash title=".env"
LANGSMITH_TRACING=true
LANGSMITH_API_KEY=ls_...
LANGSMITH_PROJECT=ilk-langsmith-projem
```

```text title=".gitignore"
.venv/
.env
__pycache__/
```

!!! danger "API key'ini asla commit etme"
    `.env` dosyasını **kesinlikle** `.gitignore`'a ekle. API key'in yanlışlıkla GitHub'a push edilmesi, LangSmith belgeleri arasında en sık karşılaşılan güvenlik hatasıdır — bir key sızdıysa hemen [smith.langchain.com](https://smith.langchain.com) üzerinden iptal edip yenisini oluştur.

## 4. İlk trace'i gönder

```python title="main.py"
from dotenv import load_dotenv
load_dotenv()

from langsmith import traceable

@traceable
def merhaba(isim: str) -> str:
    return f"Merhaba {isim}!"

print(merhaba("Emine"))
```

```bash
python main.py
```

Şimdi [smith.langchain.com](https://smith.langchain.com) üzerinden **Projects → ilk-langsmith-projem** yoluna git — `merhaba` fonksiyonunun bir trace olarak göründüğünü görmelisin.

## 5. LangGraph ekleyerek genişlet

Aynı ortama, gerçek bir [LangGraph](https://emineksknc.github.io/langgraph-turkce/) uygulaması ekleyip aynı `.env` ile otomatik izlenmesini görebilirsin — hiçbir ek kod gerekmez:

```python title="main.py (devamı)"
from langgraph.graph import StateGraph, START, END
from typing import TypedDict

class State(TypedDict):
    mesaj: str

def selamla(state: State):
    return {"mesaj": f"LangGraph'tan merhaba, {state['mesaj']}"}

graph = StateGraph(State)
graph.add_node("selamla", selamla)
graph.add_edge(START, "selamla")
graph.add_edge("selamla", END)
app = graph.compile()

print(app.invoke({"mesaj": "Emine"}))
# Bu çağrı da otomatik olarak LangSmith'e trace gönderilir
```

## Özet adımlar

1. ✅ Sanal ortam + paketler
2. ✅ `.env` (API key + `.gitignore`)
3. ✅ İlk `@traceable` fonksiyonu
4. ✅ Trace'i LangSmith UI'da görüntüleme
5. ✅ LangGraph ile genişletme

---

Sıradaki adım: [İlk Trace](ilk-trace.md) — `@traceable`'ın ve `wrap_openai`'ın diğer kullanım şekillerini derinleştirelim.
