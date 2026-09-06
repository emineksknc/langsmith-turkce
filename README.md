# LangSmith Türkçe Rehber

Sıfırdan senior seviyeye LangSmith — Türkçe kapsamlı kaynak. [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) ile hazırlanmıştır.

## Yerelde çalıştırma

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
```

Tarayıcıda `http://127.0.0.1:8000` adresini aç.

## Yeni sayfa ekleme

1. İlgili klasöre bir `.md` dosyası ekle.
2. `mkdocs.yml` içindeki `nav:` bölümüne dosyayı ekle.
3. `mkdocs serve` çalışırken tarayıcıda otomatik görünür.

## GitHub Pages'e deploy

`main` branch'ine push ettiğinde `.github/workflows/deploy.yml` otomatik olarak siteyi derleyip `gh-pages` branch'ine yayınlar. Reponun **Settings → Pages** kısmından kaynak olarak `gh-pages` branch'ini seçmen yeterli (bir kere).

Elle deploy etmek istersen:

```bash
mkdocs gh-deploy --force
```

## Kaynak ve Lisans

Bu proje, LangSmith'i Türkçe öğrenmek isteyenler için hazırlanmış bağımsız bir
topluluk/eğitim kaynağıdır. Kavramlar kendi cümlelerimle anlatılmış, kod
örnekleri kendim tarafından yazılmıştır.

LangSmith, LangChain Inc. tarafından geliştirilen bir platformdur.

- Resmi dokümantasyon: https://docs.langchain.com/langsmith
- Kardeş proje: [LangGraph Türkçe Rehber](https://github.com/emineksknc/langgraph-turkce)

Bu proje LangChain Inc. tarafından resmi olarak yayımlanmış veya
onaylanmış bir kaynak değildir.
