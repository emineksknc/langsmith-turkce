# Metadata & Tag'ler

<span class="badge badge-orta">🟡 ORTA SEVİYE</span>

Trace hacmi arttıkça, "hangi trace'ler production'a mı ait, hangi kullanıcıya ait, hangi model versiyonuyla üretildi" gibi sorular sormanız gerekir. Bunun için **metadata** (anahtar-değer bilgisi) ve **tag** (basit etiketler) kullanılır.

## Proje ile ortam ayrımı

En temel ayrım, farklı ortamlar için farklı proje adları kullanmaktır:

```python
import os

os.environ["LANGSMITH_PROJECT"] = "musteri-botu-staging"
# production'da: "musteri-botu-prod"
```

## Metadata ekleme

```python
from langsmith import traceable

@traceable(metadata={"model": "gpt-4o-mini", "versiyon": "v2"})
def cevap_uret(soru: str) -> str:
    return "..."
```

Çalışma zamanında değişen bilgi (ör. kullanıcı kimliği) için `langsmith_extra`:

```python
cevap_uret(
    "soru",
    langsmith_extra={"metadata": {"kullanici_id": "u123", "oturum_id": "s456"}},
)
```

## LangChain/LangGraph'ta metadata

LangChain Runnable'ları ve LangGraph graf çağrıları için metadata, `config` üzerinden geçirilir:

```python
llm.invoke("soru", config={"metadata": {"kullanici_id": "u123"}, "tags": ["prod"]})
```

LangGraph'ta bu, [Config & Context Injection](https://emineksknc.github.io/langgraph-turkce/orta-seviye/context-config/)'de gördüğünüz `config["configurable"]` mekanizmasıyla aynı `config` nesnesidir — LangGraph'ta zaten kullanıcı kimliği geçirmek için config kullanıyorsanız, aynı config'e `metadata`/`tags` eklemeniz yeterlidir.

## Tag'ler — basit, aranabilir etiketler

Metadata anahtar-değer çiftleriyken, **tag** basit string etiketlerdir — hızlı filtreleme için idealdir:

```python
@traceable(tags=["production", "musteri-destek"])
def cevap_uret(soru: str) -> str:
    return "..."
```

## Metadata vs Tag — ne zaman hangisi?

| | Metadata | Tag |
|---|---|---|
| Yapı | Anahtar-değer (dict) | Düz string listesi |
| Kullanım | Yapılandırılmış bilgi (kullanıcı ID, model versiyonu, maliyet) | Hızlı kategorileme (prod, staging, deneysel) |
| Filtreleme | `metadata.kullanici_id = "u123"` gibi spesifik sorgular | `tag:production` gibi basit içerme sorguları |

---

Sıradaki adım: [Filtreleme & Hassas Veri Maskeleme](filtreleme-maskeleme.md) — bu metadata/tag'leri nasıl sorgulayacağını gör.
