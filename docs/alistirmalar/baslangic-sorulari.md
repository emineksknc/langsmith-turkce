# Başlangıç Soruları

<span class="badge badge-baslangic">🟢 BAŞLANGIÇ</span>

Aşağıdaki sorular [Başlarken](../baslangic/kurulum.md) ve [Kavramlar](../kavramlar/temel-terimler.md) bölümlerindeki konuları pekiştirmek içindir.

??? question "1. LangChain/LangGraph kullanan bir uygulamayı LangSmith ile izlemek için minimum kaç satır kod eklemen gerekir?"
    Sıfır satır kod — sadece üç ortam değişkeni (`LANGSMITH_TRACING=true`, `LANGSMITH_API_KEY`, `LANGSMITH_PROJECT`) yeterlidir. LangChain/LangGraph, LangSmith'in izleme altyapısını zaten kullanır.

??? question "2. LangChain kullanmayan sıradan bir Python fonksiyonunu izlenebilir yapmak için ne kullanılır?"
    `@traceable` dekoratörü. `from langsmith import traceable` ile içe aktarılır ve fonksiyonun üstüne eklenir.

??? question "3. `wrap_openai` ne işe yarar, `@traceable` ile farkı nedir?"
    `wrap_openai`, doğrudan OpenAI SDK'sı kullanan kodda tüm model çağrılarını **otomatik** izler — çağrı başına dekoratör eklemeye gerek kalmaz. `@traceable` ise herhangi bir fonksiyonu (LLM çağrısı olsun olmasın) manuel olarak izlenebilir işaretler.

??? question "4. Bir Run ile bir Trace arasındaki fark nedir?"
    **Run**, tek bir işlemin kaydıdır (bir LLM çağrısı, bir araç çalıştırması). **Trace**, bir isteğin kök run'ından başlayan **tüm run ağacıdır** — yani bir trace, birden fazla run içerebilir.

??? question "5. Thread kavramı LangGraph'taki hangi kavramla birebir eşleşir?"
    `thread_id` ile. LangSmith'teki Thread, LangGraph'ta [checkpointer](https://emineksknc.github.io/langgraph-turkce/orta-seviye/checkpointer/) tarafından yönetilen aynı `thread_id`'yi kullanarak birden fazla trace'i tek bir konuşma altında gruplar.

??? question "6. Trajectory tam olarak neyi temsil eder?"
    Bir ajanın bir görevi tamamlarken izlediği **adım dizisini** — hangi araçları hangi sırayla çağırdığını, hangi ara kararları verdiğini. Sadece son cevaba değil, "oraya nasıl ulaşıldığına" bakmak istediğinizde önemlidir.

??? question "7. İç içe iki `@traceable` fonksiyonu (biri diğerini çağırıyor) LangSmith'te nasıl görünür?"
    Otomatik olarak parent-child ilişkisiyle, iç içe (nested) bir ağaç yapısında görünür — ayrı bir bağlama kodu yazmanıza gerek yoktur.

??? question "8. Observability hangi soruyu, Evaluation hangi soruyu cevaplar?"
    Observability "üretimde şu an ne oluyor?" sorusunu, Evaluation "bu değişiklik kaliteyi bozdu mu?" sorusunu cevaplar. Biri sürekli gerçek trafiği izler, diğeri sabit bir test seti üzerinde kontrollü karşılaştırma yapar.

??? question "9. Sadece Evaluation yapıp Observability'yi ihmal etmenin riski nedir?"
    Dataset'inizin kapsamadığı gerçek dünya senaryolarını göremezsiniz — dataset zamanla gerçek kullanıcı davranışından uzaklaşabilir (drift) ve bunu fark edemezsiniz.

??? question "10. `LANGCHAIN_TRACING_V2` ile `LANGSMITH_TRACING` arasındaki ilişki nedir?"
    İkisi de aynı işi yapar — `LANGCHAIN_TRACING_V2` eski isimdir, hâlâ çalışır. `LANGSMITH_TRACING` daha yeni, önerilen isimdir. Yeni projelerde `LANGSMITH_*` önekini kullanmak tercih edilmelidir.

---

Hazır mısın? Sıradaki seviye: [Orta Seviye Soruları](orta-seviye-sorulari.md)
