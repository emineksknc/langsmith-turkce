# Prompt Hub

<span class="badge badge-ileri">🔴 İLERİ / SENIOR</span>

**Prompt Hub**, promptlarınızı kodun dışında, versiyonlanmış, paylaşılabilir nesneler olarak yönetmenizi sağlayan LangSmith özelliğidir. (Eski adıyla "repo" — dokümantasyonda hâlâ bu terime rastlayabilirsiniz.)

## Neden promptu kodun içine gömmemeli?

Prompt kod içinde bir string olduğunda, her küçük değişiklik bir deploy gerektirir ve prompt'un geçmiş versiyonlarını takip etmek zorlaşır. Prompt Hub ile prompt'u **ayrı bir varlık** olarak versiyonlarsınız — deploy etmeden güncelleyebilir, önceki versiyona anında dönebilirsiniz.

## Prompt push etme (oluşturma/güncelleme)

```python
from langsmith import Client
from langchain_core.prompts import ChatPromptTemplate

client = Client()

prompt = ChatPromptTemplate.from_template(
    "Sen bir müşteri destek asistanısın. Kullanıcı sorusu: {soru}"
)

url = client.push_prompt("musteri-destek-sistem-promptu", object=prompt)
print(url)  # UI'daki prompt sayfasının linki
```

Aynı isimle tekrar `push_prompt` çağırırsanız, prompt **güncellenir** (yeni bir commit oluşturur) — isim yoksa yeni oluşturulur.

## Model konfigürasyonuyla birlikte push etme

Prompt'u, hangi modelle kullanılacağı bilgisiyle birlikte de saklayabilirsiniz:

```python
from langchain_openai import ChatOpenAI

model = ChatOpenAI(model="gpt-4o-mini")
chain = prompt | model

client.push_prompt("musteri-destek-sistem-promptu-model-dahil", object=chain)
```

Bu, LangSmith Playground'da prompt'u doğrudan doğru modelle test edebilmenizi sağlar.

## Prompt pull etme (kullanma)

```python
prompt = client.pull_prompt("musteri-destek-sistem-promptu")
mesaj = prompt.invoke({"soru": "İade süresi kaç gün?"})
```

Belirli bir versiyona (commit) sabitlemek için:

```python
prompt = client.pull_prompt("musteri-destek-sistem-promptu:a1b2c3d")
```

Commit hash belirtilmezse varsayılan olarak `:latest` (en güncel versiyon) çekilir.

## LangGraph içinde kullanım

```python
def chatbot(state: State):
    prompt = client.pull_prompt("musteri-destek-sistem-promptu")
    yanit = llm.invoke(prompt.invoke({"soru": state["messages"][-1].content}).to_messages())
    return {"messages": [yanit]}
```

!!! warning "pull_prompt senkron bir ağ çağrısıdır"
    `pull_prompt`, her çağrıldığında LangSmith API'sine bir HTTP isteği atar. Bunu bir [LangGraph node'unun](https://emineksknc.github.io/langgraph-turkce/baslangic/temel-kavramlar/) içinde her çağrıda tekrar tekrar yapmak yerine, **uygulama başlangıcında bir kez** çekip önbelleğe almanız önerilir — özellikle async node'larda senkron bir ağ çağrısı olay döngüsünü (event loop) bloke edebilir.

## Public vs Private prompt'lar

`push_prompt`'a `is_public=True` vererek prompt'u herkese açık hale getirebilirsiniz — LangChain topluluğunun paylaştığı hazır promptlara (`hwchase17/react` gibi) da `pull_prompt` ile erişebilirsiniz.

---

Sıradaki bölüm: [İleri / Production — Human Feedback & Annotation Queue](../ileri-seviye/feedback-annotation.md).
