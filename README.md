# AG_News_Classification
Projenin kodlarına [buraya tıklayarak](https://colab.research.google.com/drive/1HBkst5ELRJN93jEJ9AQ8s7L4WODyXshB) ulaşabilirsiniz.
Proje: AG News Sınıflandırma

Hedef: AG News veri seti kullanarak haber metinlerini 4 ana kategoriye (World, Sports, Business, Science/Technology) sınıflandırmak.
# Kütüphaneler
```
!pip install transformers torch datasets
# Hugging Face’in transformers kütüphanesi
```
```
from transformers import DistilBertTokenizer, DistilBertForSequenceClassification, Trainer, TrainingArguments
from datasets import load_dataset
import torch
```
# Veri Setini Yükleme ve İnceleme
```
# AG News veri setini yükle
dataset = load_dataset("ag_news", split='train[:1000]')  # İlk 1000 örneği al

# Veri setinin örneklerini inceleyin
for example in dataset:
    print(f"Label: {example['label']}, Text: {example['text']}")
    break  # İlk örneği görüntüle, fazla veri dökümünü önler
```
# Veriyi Tokenizasyon
```
# Tokenizer Yükleme
tokenizer = DistilBertTokenizer.from_pretrained('distilbert-base-uncased') #Bu satır, DistilBERT modelinin önceden eğitilmiş tokenizer'ını yükler. Tokenizer, metinleri modelin anlayacağı forma dönüştürür.

# Tokenizasyon işlemi
def tokenize_function(example):
    return tokenizer(example['text'], padding='max_length', truncation=True, max_length=128)

# Tokenizasyon
tokenized_datasets = dataset.map(tokenize_function, batched=True)

# Sütunları yeniden adlandırma ve formatlama
tokenized_datasets = tokenized_datasets.rename_column("label", "labels")
tokenized_datasets.set_format("torch", columns=["input_ids", "attention_mask", "labels"])

# Eğitim ve test veri setlerine bölme
train_test_split = tokenized_datasets.train_test_split(test_size=0.2)
train_dataset = train_test_split['train']
eval_dataset = train_test_split['test']
```
# Model Seçimi ve Eğitim
```
# Modeli Yükleme
model = DistilBertForSequenceClassification.from_pretrained('distilbert-base-uncased', num_labels=4)

# Eğitim argümanları
training_args = TrainingArguments(
    output_dir='./results',
    num_train_epochs=3,
    per_device_train_batch_size=8,
    per_device_eval_batch_size=8,
    warmup_steps=500,
    weight_decay=0.01,
    logging_dir='./logs',
    logging_steps=10,
)

# Trainer Nesnesini Oluşturma
trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=train_dataset,
    eval_dataset=eval_dataset
)

# Modeli Eğitme
trainer.train()
```
# Modeli Değerlendirme
```
# Modeli değerlendirme
eval_results = trainer.evaluate()
print(eval_results)
```
# Tahmin Yapma
```
def predict(text):
    inputs = tokenizer(text, return_tensors="pt", truncation=True, padding=True, max_length=128)
    outputs = model(**inputs)
    predictions = torch.argmax(outputs.logits, dim=-1)
    return predictions.item()

# Örnek tahmin yapma
sample_text = "Microsoft announces new AI technologies"
predicted_label = predict(sample_text)
print(f"Predicted label: {predicted_label}")
```
```
# Tahmin yapma fonksiyonu
def predict(text):
    inputs = tokenizer(text, return_tensors="pt", truncation=True, padding=True, max_length=128)
    outputs = model(**inputs)
    predictions = torch.argmax(outputs.logits, dim=-1)
    return predictions.item()

# Test için örnek metinler
sample_texts = [
    "Microsoft announces new AI technologies",
    "The latest sports news and scores",
    "Stock market crashes amid economic uncertainty",
    "New discoveries in quantum physics"
]

# Etiketler
labels = ["World", "Sports", "Business", "Science"]

# Tahminleri yapma ve yazdırma
print("\nSample Predictions:")
for text in sample_texts:
    predicted_label = predict(text)
    predicted_label_name = labels[predicted_label]
    print(f"Text: {text}")
    print(f"Predicted Label: {predicted_label_name}\n")
```
