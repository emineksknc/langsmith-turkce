# İleri Seviye Soruları

<span class="badge badge-ileri">🔴 İLERİ / SENIOR</span>

Bu sorular [LLM-as-judge](../evaluation/llm-as-judge.md), [Online Evaluation](../evaluation/online-evaluation.md), [Prompt Hub](../prompts/prompt-hub.md) ve [İleri/Production](../ileri-seviye/feedback-annotation.md) konularını test eder.

??? question "1. LLM-as-judge evaluator'da `response_format` ile structured output kullanmanın avantajı nedir?"
    Yargıç modelin serbest metin yerine garanti tipli bir çıktı (ör. `bool`, sabit bir şema) döndürmesini sağlar — string ayrıştırmaya (regex, "evet" kelimesi arama) güvenmekten çok daha sağlamdır ve modelin beklenmedik bir formatta cevap vermesi riskini ortadan kaldırır.

??? question "2. LLM-as-judge, insan değerlendirmesinin yerini tamamen alabilir mi?"
    Hayır — LLM-as-judge insan değerlendirmesini **ölçeklendirir**, yerine geçmez. Yargıç modelin kendisi de hata yapabilir; kritik kararlar için yargıcın skorlarını periyodik olarak birkaç insan örneğiyle karşılaştırıp güvenilirliğini doğrulamak gerekir.

??? question "3. Online evaluation'ı yapılandırmak için temel mekanizma nedir, hangi üç bileşenden oluşur?"
    **Automation Rules** (otomasyon kuralları). Üç bileşen: filtre (hangi run'lar), örnekleme oranı (yüzde kaçı) ve aksiyon (dataset'e ekleme, annotation queue'ya gönderme, webhook tetikleme veya online evaluator çalıştırma).

??? question "4. Tüm production trafiğini %100 oranında online evaluation'a sokmanın iki dezavantajı nedir?"
    Maliyet (her örneklenen run için ek bir LLM çağrısı/yargıç maliyeti oluşur) ve veri saklama maliyeti (eşleşen trace'ler otomatik olarak extended data retention'a yükseltilir, bu da fiyatlandırmayı etkiler). Küçük bir örneklemle başlamak daha maliyet-etkindir.

??? question "5. `pull_prompt`'u bir LangGraph node'unun içinde her çağrıda çağırmanın riski nedir?"
    Her çağrı senkron bir HTTP isteği yapar — bu hem gereksiz gecikme ekler hem de async node'larda olay döngüsünü (event loop) bloke edebilir. Prompt'u uygulama başlangıcında bir kez çekip önbelleğe almak önerilir.

??? question "6. Bir prompt'u `client.push_prompt(\"isim\", object=chain)` ile bir model zinciriyle (`prompt | model`) birlikte push etmenin faydası nedir?"
    Prompt'un hangi model konfigürasyonuyla kullanılacağı bilgisini de saklar — bu sayede LangSmith Playground'da prompt'u doğrudan doğru modelle test edebilirsiniz, sadece şablon metnini değil.

??? question "7. Feedback config'in (organizasyon çapında tanımlanan şema) somut faydası nedir?"
    Her ekip üyesinin aynı metrik için **aynı ölçütle** (ör. aynı 0-1 skala, aynı kategori isimleri) geri bildirim vermesini sağlar — versiyon kontrolü ve tutarlılık sunar, özellikle CI/CD pipeline'larında veya ortamlar arası evaluation kurulumlarını çoğaltırken kullanışlıdır.

??? question "8. Bir Annotation Queue'ya run'lar tipik olarak nasıl eklenir?"
    Genelde bir Automation Rule üzerinden otomatik olarak (ör. "negatif feedback alan her run'ı bu kuyruğa ekle"), ama programatik olarak `client.add_runs_to_annotation_queue(queue_id=..., run_ids=[...])` ile de elle eklenebilir.

??? question "9. Bir organizasyonda ne zaman ayrı workspace, ne zaman aynı workspace içinde ayrı proje kullanmalısınız?"
    Farklı ekipler ya da tamamen farklı erişim gereksinimleri (ör. müşteriye özel veri izolasyonu) varsa ayrı **workspace**. Aynı ekip içindeki farklı ortamlar (dev/staging/prod) için genelde aynı workspace'te farklı **proje** adları (`LANGSMITH_PROJECT`) yeterlidir.

??? question "10. Self-hosted vs Cloud kararında en belirleyici soru nedir?"
    Verinin şirket ağının dışına çıkıp çıkamayacağı (regülasyon, KVKK/GDPR gereksinimleri). Bu kısıtlama varsa self-hosted zorunlu hale gelir; yoksa karar, platform yönetecek bir ekibin olup olmadığına ve tam kontrol ihtiyacına bağlıdır.

---

Bir önceki seviyeye dönmek için: [Orta Seviye Soruları](orta-seviye-sorulari.md) · Baştan başlamak için: [Başlangıç Soruları](baslangic-sorulari.md)
