# İlk Trace

<span class="badge badge-baslangic">🟢 BAŞLANGIÇ</span>

## LangChain/LangGraph kullanıyorsanız: sıfır kod değişikliği

[Kurulum](kurulum.md)'daki ortam değişkenleri ayarlandıysa, LangChain veya LangGraph ile yazdığınız her şey **otomatik olarak** izlenir — çünkü bu kütüphaneler LangSmith'in Runnable/callback altyapısını zaten kullanır.

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini")
llm.invoke("Merhaba, kimsin?")
# Hiçbir ek kod yok — bu çağrı otomatik olarak LangSmith'e trace olarak gönderilir
```

[smith.langchain.com](https://smith.langchain.com) üzerinden projenize gidip trace'in göründüğünü doğrulayın.

## LangChain kullanmıyorsanız: @traceable dekoratörü

Herhangi bir Python fonksiyonunu, LangChain'e bağımlı olmadan izlenebilir hale getirmek için:

```python
from langsmith import traceable

@traceable
def cevap_uret(soru: str) -> str:
    # herhangi bir LLM çağrısı, iş mantığı vb.
    return f"'{soru}' sorusuna cevap"

cevap_uret("Türkiye'nin başkenti neresi?")
```

## OpenAI istemcisini otomatik sarmalamak

LangChain kullanmadan doğrudan OpenAI SDK'sı kullanıyorsanız, `wrap_openai` ile tüm çağrıları otomatik izletebilirsiniz:

```python
from openai import OpenAI
from langsmith.wrappers import wrap_openai

client = wrap_openai(OpenAI())

client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "Merhaba"}],
)
# Bu çağrı da otomatik trace olur
```

## İç içe fonksiyonlar — otomatik parent-child ilişkisi

`@traceable` ile işaretlenen bir fonksiyon başka bir `@traceable` fonksiyonu çağırırsa, LangSmith bunları otomatik olarak **iç içe** (parent-child) gösterir:

```python
@traceable
def belge_getir(soru: str) -> list[str]:
    return ["ilgili belge 1", "ilgili belge 2"]

@traceable
def rag_pipeline(soru: str) -> str:
    belgeler = belge_getir(soru)  # otomatik child trace
    return f"{len(belgeler)} belge bulundu, cevap üretiliyor..."

rag_pipeline("İade politikası nedir?")
```

Trace ağacında `rag_pipeline` üst düğüm, `belge_getir` onun altında bir alt düğüm olarak görünür — karmaşık pipeline'larda "hangi adım ne kadar sürdü, ne döndürdü" sorusunu tek bakışta cevaplar.

---

Sıradaki adım: [Run, Trace, Thread, Trajectory](../kavramlar/temel-terimler.md) ile temel kavramları netleştirelim.
