
# 1. tokenizer_benchmark.py

``` bash
python3 tokenizer_benchmark.py \
  --tr "Yapay zeka mühendisliği, büyük dil modellerinin üretim ortamlarında ölçeklenebilir ve güvenli bir şekilde çalıştırılmasını sağlar." \
  --en "AI engineering ensures that large language models run scalably and securely in production environments." \
  --model gpt-4o
```

----

## AI Engineering Karşılaştırma Aracı --- Model: gpt-4o  

| Metrik | Türkçe (TR) | İngilizce (EN) | Fark / Oran |
| :--- | :--- | :--- | :--- |
| **Karakter Sayısı** | 130 | 103 | 1.26x |
| **Token Sayısı** | 31 | 16 | 1.94x daha fazla TR |
| **Tokenizasyon Süresi (ms)** | 311.0070 ms | 0.0207 ms | - |
| **Tahmini Girdi Maliyeti ($)** | $0.0000775 | $0.0000400 | - |

### 🔍 Türkçe Metnin İlk 15 Token Dağılımı

- ['Y', 'apay', ' z', 'eka', ' müh', 'endis', 'liği', ',', ' büyük', ' dil', ' modeller', 'inin', ' üret', 'im', ' ortam']

----
