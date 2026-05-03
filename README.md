# Layihənin qısa izahatı
## 📝 Layihə Haqqında

Açıq mənbəli OpenAI Whisper-Small modelinin "tahmaz/azerbaijani-asr-zenfira_1k" dataseti üzərində  
Azərbaycan dili üçün fine-tuning layihəsi.  

Fine-tuning nəticəsində baza modelinin WER-i **55.28%** səviyyəsindən **22.05%**-ə endirildi —  
yəni **təxminən 2.5 dəfə yaxşılaşma** əldə olundu.




##  Model və Parametrlər

###  Dataset və Dil

| Parametr            | Dəyər                                      |
|---------------------|---------------------------------------------|
| Baza model          | `openai/whisper-small`                      |
| Dataset             | `tahmaz/azerbaijani-asr-zenfira_1k`        |
| Dil                 | Azərbaycan (`az`)                           |
| Train nümunə sayı   | 459                                         |
| Test nümunə sayı    | 57                                          |

---

###  Training Hiperparametrləri

Aşağıdakı konfiqurasiya istifadə olunub:

```python
output_dir                  = "./whisper-small-az"
per_device_train_batch_size = 8
per_device_eval_batch_size  = 8
gradient_accumulation_steps = 2
weight_decay                = 0.01
learning_rate               = 3e-5
warmup_steps                = 50
num_train_epochs            = N_EPOCHS

eval_strategy               = "epoch"
save_strategy               = "epoch"
load_best_model_at_end      = True
greater_is_better           = False
metric_for_best_model       = "wer"

predict_with_generate       = True
generation_max_length       = 225

logging_steps               = 5
logging_dir                 = "./logs"
report_to                   = ["tensorboard"]

save_total_limit            = 2
fp16                        = torch.cuda.is_available()
dataloader_num_workers      = 0

push_to_hub                 = False

# ## 📊 WER / CER Nəticələri

### Training Curve

| Epoch | Training Loss | Validation Loss | WER (%)    |
|-------|----------------|------------------|-------------|
| 1     | 2.043803       | 0.808082         | 79.577465   |
| 2     | 0.912347       | 0.378674         | 27.112676   |
| 3     | 0.177027       | 0.221595         | 22.887324   |

##  •Fine-tuning nəticəsinin müqayisəsi

| Model                  | WER   | CER   | dWER  | dCER  |
|------------------------|-------|-------|-------|-------|
| Baza (whisper-small)   | 55.28 | 17.72 |   -   |   -   |
| Fine-tuned (whisper-az)| 23.46 |  4.81 | 31.81 | 12.91 |

#Transkripsiya Müqayisələri
# En cox komek etdiyi 3 netice
| № | Dəyişmə (%) | Orijinal                          | Model çıxışı                   | Düz çıxış                       |
|---|-------------|-----------------------------------|--------------------------------|---------------------------------|
| 1 | 100.0       | Ərazisi səksən altı min kvadrat kilometrdir. | Erazisi 86.000 km.             | Ərazisi səksən altı min kvadrat kilometrdir. |
| 2 | 100.0       | Vətənpərvərlik tərbiyəsi güclüdür. | və tən pərvəri lik tərbiyəsi güçlüdə. | Vətənpərvərlik tərbiyyəsi güçlüdür. |
| 3 | 100.0       | Üçüncü əsrə qədər.                | üçüncə istirəq edər.           | Üçüncü əsrə qədər.             |



# En az komek etdiyi 3 netice
| № | Dəyişmə (%) | Orijinal             | Model çıxışı          | Düz çıxış                |
|---|-------------|----------------------|------------------------|--------------------------|
| 1 | -50.0       | Məscidlər çoxdur.    | Məscidlər çoxdur.     | Məskidlər çoxdur.        |
| 2 | -50.0       | Birinci Axsitan.     | Birinci Axtan          | Berinci Axtan.           |
| 3 | -33.3       | Ailə dəyərləri vacibdir. | Ailə dəyərləri vacibdir. | Ailə dəhərləri vacibdir. |

##  Kodu işə salmaq üçün addımlar (Setup + Run)

### 1️Python versiyası
- **Python ≥ 3.10** tələb olunur.

---

### 	Kodu işə salmaq üçün addımlar (setup + run)
1) git clone <repo>
2) cd <repo>
3) python -m venv venv && source venv/bin/activate
4) pip install -r requirements.txt

TRAIN etmək üçün:
   training/whisper_train.ipynb aç və run et

TEST etmək üçün:
   evaluation/whisper_eval.ipynb aç və run et
 Nəticələr:
   results/results.pdf
























