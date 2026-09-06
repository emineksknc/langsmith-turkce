# Sözlük — Terimler

Bu sayfada rehber boyunca geçen terimler, orijinal İngilizce karşılıklarıyla birlikte kısaca açıklanıyor.

## Temel Kavramlar

**Run (çalıştırma)**
: Tek bir işlemin kaydı — bir LLM çağrısı, araç çalıştırması veya `@traceable` fonksiyon çağrısı.

**Trace (iz)**
: Bir isteğin kök run'ından başlayan tüm run ağacı. Bkz. [Run, Trace, Thread, Trajectory](kavramlar/temel-terimler.md).

**Thread (iş parçacığı / konuşma dizisi)**
: Birden fazla trace'i tek bir konuşma altında gruplayan kimlik — LangGraph'taki `thread_id` ile aynı fikir.

**Trajectory (izlence)**
: Bir ajanın bir görevi tamamlarken izlediği adım dizisi (hangi araçları hangi sırayla çağırdığı).

**Observability (izlenebilirlik)**
: "Üretimde şu an ne oluyor?" sorusuna cevap veren, sürekli trace toplama yeteneği.

**Evaluation (değerlendirme)**
: "Bu değişiklik kaliteyi bozdu mu?" sorusuna cevap veren, dataset üzerinde otomatik skorlama yeteneği.

## Tracing

**@traceable**
: Herhangi bir Python fonksiyonunu izlenebilir hale getiren dekoratör.

**wrap_openai**
: OpenAI istemcisini sararak tüm model çağrılarını otomatik izleyen fonksiyon.

**run_type**
: Bir run'ın UI'da nasıl gösterileceğini belirten tip (`llm`, `retriever`, `tool`, `chain`).

**Metadata**
: Bir run'a eklenen yapılandırılmış anahtar-değer bilgisi (kullanıcı ID, model versiyonu gibi).

**Tag**
: Bir run'a eklenen basit, aranabilir string etiket (`production`, `staging` gibi).

**Masking (maskeleme)**
: Hassas verinin (kişisel bilgi, API anahtarı) trace'lere kaydedilmeden önce gizlenmesi.

**Anonymizer**
: Regex tabanlı, belirli veri kalıplarını (e-posta, telefon) otomatik maskeleyen fonksiyon.

## Evaluation

**Dataset**
: Üzerinde tekrar tekrar değerlendirme çalıştırılan, sabit bir girdi (ve genelde beklenen çıktı) kümesi.

**Example (örnek)**
: Bir dataset'in tek bir satırı — girdi, (opsiyonel) beklenen çıktı ve metadata içerir.

**Target fonksiyon**
: `evaluate()`'e verilen, dataset girdisini alıp uygulamanın çıktısını döndüren fonksiyon.

**Evaluator**
: Girdi/çıktıyı alıp bir skor döndüren fonksiyon.

**Experiment (deney)**
: Bir dataset üzerinde `evaluate()` ile yapılan tek bir değerlendirme çalıştırması; `experiment_prefix` ile adlandırılır.

**LLM-as-judge (yargıç olarak LLM)**
: Bir LLM'in, başka bir uygulamanın çıktısının kalitesini otomatik olarak puanlaması yöntemi.

**Offline evaluation**
: Sabit bir dataset üzerinde, deploy öncesi yapılan değerlendirme.

**Online evaluation**
: Gerçek production trafiği üzerinde, otomasyon kurallarıyla sürekli çalışan değerlendirme.

**Automation Rule (otomasyon kuralı)**
: Filtre + örnekleme oranı + aksiyondan oluşan, trace verisi üzerinde otomatik işlem tetikleyen LangSmith kuralı.

## Prompts

**Prompt Hub**
: Promptların versiyonlanmış, paylaşılabilir nesneler olarak yönetildiği LangSmith özelliği (eski adıyla "repo").

**push_prompt / pull_prompt**
: Bir prompt'u Hub'a göndermek / Hub'dan çekmek için kullanılan `Client` metodları.

**Commit**
: Bir prompt'un belirli bir versiyonu — hash ile referans verilir (`:latest` varsayılan).

## İnsan Geri Bildirimi

**Feedback**
: Bir run hakkında insan ya da model tarafından verilen skor/yorum.

**Feedback config**
: Organizasyon çapında tanımlanan, bir feedback anahtarının şemasını (sürekli, kategorik, serbest metin) belirleyen yapı.

**Annotation Queue**
: İncelenmesi gereken run'ların toplandığı, ekip tarafından gözden geçirilen kuyruk.

## Organizasyon & Erişim

**Organization**
: Faturalandırma ve üyelik seviyesindeki en üst birim.

**Workspace**
: Bir organizasyon içinde izole edilmiş, kendi proje/dataset/API key'lerine sahip çalışma alanı.

**RBAC (Role-Based Access Control — rol bazlı erişim kontrolü)**
: Kullanıcıların yetkilerinin roller üzerinden tanımlandığı erişim modeli.

**Service account**
: Bir kullanıcıya değil, bir otomasyona (CI/CD gibi) bağlı, sabit yetkili API key türü.

---

Bir terimi bulamadıysan, [GitHub reposundan](https://github.com/emineksknc/langsmith-turkce) bir issue/PR açabilirsin.
