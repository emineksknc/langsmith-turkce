# Otomatik İzleme (@traceable)

<span class="badge badge-orta">🟡 ORTA SEVİYE</span>

[İlk Trace](../baslangic/ilk-trace.md)'te `@traceable`'ın temelini gördük. Bu sayfa, gerçek projelerde ihtiyaç duyacağın ince ayarları kapsıyor.

## Fonksiyon adını ve run tipini özelleştirme

```python
from langsmith import traceable

@traceable(name="Belge Getirme", run_type="retriever")
def belge_getir(soru: str) -> list[str]:
    return ["belge 1", "belge 2"]
```

`run_type` parametresi, LangSmith UI'ında run'ın nasıl gösterileceğini belirler: `"llm"`, `"retriever"`, `"tool"`, `"chain"` gibi tipler farklı ikonlar/görselleştirmelerle gösterilir.

## Girdi/çıktıyı özelleştirme

Bazen fonksiyona giren ham parametreleri değil, **anlamlı bir özet** göstermek istersiniz:

```python
@traceable(
    process_inputs=lambda inputs: {"soru_uzunlugu": len(inputs["soru"])},
)
def cevap_uret(soru: str) -> str:
    return "..."
```

## Metadata ekleme (dekoratör içinden)

```python
@traceable(metadata={"model_versiyonu": "v2", "ortam": "staging"})
def cevap_uret(soru: str) -> str:
    return "..."
```

Çalışma zamanında değişen metadata için (bkz. [Metadata & Tag'ler](metadata-taglar.md)) `langsmith_extra` parametresi kullanılır:

```python
cevap_uret("soru", langsmith_extra={"metadata": {"kullanici_id": "u123"}})
```

## Async fonksiyonlar

`@traceable`, hem senkron hem asenkron fonksiyonlarda aynı şekilde çalışır:

```python
@traceable
async def cevap_uret_async(soru: str) -> str:
    sonuc = await llm.ainvoke(soru)
    return sonuc.content
```

## Bir fonksiyonu koşullu izlemek

Geliştirme ortamında izlemeyi kapatmak için kod değiştirmeye gerek yok — `LANGSMITH_TRACING=false` yeterlidir. Ama tek bir fonksiyonu programatik olarak devre dışı bırakmak isterseniz:

```python
import os
from langsmith import traceable

@traceable
def cevap_uret(soru: str) -> str:
    ...

# Ortam değişkenine göre otomatik açılır/kapanır — ek kod gerekmez
```

!!! tip "Trace edilmeyen kod bloğu"
    Bir `@traceable` fonksiyonunun **içinde**, izlenmesini istemediğiniz bir bölüm varsa (ör. hassas bir hesaplama), o kısmı ayrı, `@traceable` **olmayan** bir yardımcı fonksiyona taşıyın — LangSmith sadece işaretlediğiniz fonksiyonları izler, otomatik olarak her şeyi kaydetmez.

---

Sıradaki adım: [Metadata & Tag'ler](metadata-taglar.md).
