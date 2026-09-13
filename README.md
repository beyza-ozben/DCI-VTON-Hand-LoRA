# Enhancing Hand Region Visual Quality in DCI-VTON Based Virtual Try-On Systems Using LoRA

> **DCI-VTON Tabanlı Sanal Giyim Sistemlerinde El Bölgesi Görsel Kalitesinin LoRA ile Artırılması**

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19183626.svg)](https://doi.org/10.5281/zenodo.19183626)
[![Status: Preprint](https://img.shields.io/badge/Status-Preprint-blue.svg)](https://zenodo.org/records/19183626)
[![Indexed in OpenAIRE](https://img.shields.io/badge/Indexed%20in-OpenAIRE-blue.svg)](https://explore.openaire.eu)
[![Conference](https://img.shields.io/badge/Conference-TOK%202025-orange.svg)](https://zenodo.org/communities/tok2025)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Paper](https://img.shields.io/badge/Paper-PDF-red.svg)](docs/Revize-DCI-VTON.pdf)

Bu depo; **26. Otomatik Kontrol Ulusal Konferansı (TOK)** kapsamında sunumu gerçekleştirilen ve resmi bildiri kitabı öncesinde Zenodo üzerinde **ön baskı (preprint)** olarak yayımlanan çalışmanın tam metnini, deneysel bulgularını ve sunum materyallerini açık erişime sunmak amacıyla hazırlanmıştır.

---

## 👥 Authors & Supervision

### Authors
* **Beyza Nur Özben** ([@beyza-ozben](https://github.com/beyza-ozben)) – *Department of Computer Engineering, Ondokuz Mayıs University*
* **Elif Altunsu** ([@ElifAltunsu](https://github.com/ElifAltunsu)) – *Department of Computer Engineering, Ondokuz Mayıs University*

### Supervisor / Advisor
* **Dr. Öğr. Üyesi Oğuz Emre Kural** ([@ekural](https://github.com/ekural)) – *Department of Computer Engineering, Ondokuz Mayıs University*

---

## 📖 Özetçe (Abstract)

Sanal Deneme (Virtual Try-On, VTON) sistemlerinde difüzyon tabanlı görüntü tamamlama (inpainting) yaklaşımları, kıyafet transferinde yüksek kaliteli çıktılar üretmektedir . Ancak DCI-VTON gibi gelişmiş modellerde dahi üretilen kıyafet mankenle başarılı biçimde hizalanırken, el ve parmak gibi ince anatomik detaylarda yapısal deformasyonlar ve yapaylıklar meydana gelmektedir .

Bu çalışmada:
- Tüm difüzyon mimarisini baştan eğitmek yerine, Parametre Verimli İnce Ayar (**PEFT**) metotlarından **LoRA (Low-Rank Adaptation)** kullanılmıştır .
- LoRA katmanları, U-Net yapısındaki dikkat mekanizmalarına (Self-Attention ve Cross-Attention) entegre edilmiştir .
- Düşük veri hacmi ve kısıtlı donanım imkanları altında dahi yüksek adım sayısı kullanılarak el bölgelerindeki görsel kalitede, parmak formlarında ve doğal görünümde belirgin iyileşmeler elde edilmiştir .

---

## 🧠 Yöntem ve Entegrasyon

```text
[Hedef Kıyafet] ──> [Warping Network] ─┐
                                       ├──> [Bükülmüş Girdi + Gürültü] ──> [U-Net Difüzyon Modeli] ──> [Nihai Çıktı]
[Kişi Görseli]  ──────────────────────┘                                         │
                                                                       ┌────────┴────────┐
                                                                       │ LoRA Entegrasyonu│
                                                                       │ (Attention Layers)
                                                                       └─────────────────┘
```

1. **Temel Model:** DCI-VTON (Diffusion-based Conditional Inpainting for Virtual Try-On) 
2. **LoRA Uyarlaması:** Modelin dikkat katmanlarındaki ağırlık matrisleri dondurulmuş, düşük dereceli ($r$) matris çarpanları üzerinden güncelleme sağlanmıştır . Böylece milyonlarca parametre yerine çok daha az parametre eğitilerek donanım ve zaman maliyeti düşürülmüştür .
3. **Pipeline Entegrasyonu:** DCI-VTON doğrudan Stable Diffusion boru hattını temel almadığından, kohya_ss eğitim çatısı ve DCI-VTON arasındaki veri akışını sağlayan özel bir boru hattı kurgulanmıştır .

---

## 🔬 Deneysel Çalışmalar & Donanım

* **Veri Kümesi:** VITON-HD veri kümesinden ellerin belirgin olduğu 385 görsel filtrelenerek ikili (binary) maskeleri hazırlanmıştır .
* **Eğitim Çatısı:** `kohya_ss` 
* **Donanım:** NVIDIA GeForce RTX 2080 Ti GPU (11 GB VRAM), 32 GB RAM 
* **Eğitim Parametreleri:**
  * **Eğitim Adım Sayısı:** 6000 adım (~62 epoch) 
  * **Ağırlık Formatı:** `.safetensors` 
* **Bulgular:** Donanım kısıtları nedeniyle veri hacmi sınırlandırıldığında bile adım sayısının artırılması (1500, 4500 ve 6000 adımlık deneyler) el bölgesindeki bozulmaların giderilmesinde ve parmak detaylarının belirginleştirilmesinde doğrudan etkili olmuştur .

---

## 📝 Atıf (Citation)

Bu ön baskıyı (preprint) araştırmalarınızda veya projelerinizde kaynak göstermek isterseniz aşağıdaki BibTeX formatını kullanabilirsiniz:

```bibtex
@misc{ozben2026dcivtonlora,
  author       = {Özben, Beyza Nur and Altunsu, Elif and Kural, Oğuz Emre},
  title        = {DCI-VTON Tabanlı Sanal Giyim Sistemlerinde El Bölgesi Görsel Kalitesinin LoRA ile Artırılması},
  howpublished = {26. Otomatik Kontrol Ulusal Konferansı (TOK) Preprint, Zenodo},
  year         = {2026},
  doi          = {10.5281/zenodo.19183626},
  url          = {[https://doi.org/10.5281/zenodo.19183626](https://doi.org/10.5281/zenodo.19183626)}
}
```

---

## 📄 Lisans

Bu çalışmanın doküman ve metin içerikleri [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) lisansı altındadır.
