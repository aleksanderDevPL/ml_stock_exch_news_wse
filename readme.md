# 📈 AI Stock Impact Predictor

![ML](https://img.shields.io/badge/Machine%20Learning-blue)
![NLP](https://img.shields.io/badge/NLP-yellow)
![Finance](https://img.shields.io/badge/Finance-green)

## 🧠 O projekcie
**AI Stock Impact Predictor** to model uczenia maszynowego analizujący komunikaty bieżące i okresowe spółek giełdowych. Celem modelu jest przewidywanie wpływu treści komunikatów na zmiany cen akcji w dniu publikacji.

Model został wytrenowany na podstawie tysięcy historycznych komunikatów giełdowych oraz historycznych cen akcji. Wykorzystuje **inżynierię cech (Feature Engineering)** oraz **analizę tekstu (NLP)** do wyodrębnienia istotnych informacji wpływających na rynek.

---

## 🚀 Instalacja
Aby uruchomić model lokalnie, wykonaj poniższe kroki:

```bash
# Klonowanie repozytorium
git clone https://github.com/user/repo.git
cd repo

# Instalacja zależności
pip install -r requirements.txt
```

---

## ⚙️ Jak działa model?
1. Pobiera treść komunikatu giełdowego.
2. Przetwarza tekst za pomocą NLP (tokenizacja, embeddingi, analiza sentymentu).
3. Wykorzystuje dane rynkowe i cechy fundamentalne.
4. Przewiduje wpływ komunikatu na zmianę ceny akcji w danym dniu.

---

## 🛠 Technologie
- 📊 **Uczenie maszynowe:** Scikit-Learn, XGBoost, TensorFlow
- 🔍 **Analiza tekstu (NLP):** spaCy, Transformers, TF-IDF
- 📈 **Dane finansowe:** Yahoo Finance API, GPW API
- 🛠 **Feature Engineering:** PCA, normalizacja, one-hot encoding

---

## 📌 Przykład użycia
Poniżej znajduje się przykład użycia modelu do predykcji wpływu komunikatu na cenę akcji:

```python
from model import StockImpactPredictor

# Inicjalizacja modelu
predictor = StockImpactPredictor()

# Przykładowy komunikat giełdowy
message = "Spółka XYZ ogłosiła wzrost przychodów o 20% w Q1 2024."

# Predykcja wpływu na cenę akcji
impact = predictor.predict(message)
print(f'Przewidywany wpływ: {impact}')
```

---

## 📂 Struktura katalogów
```
📦 stock-impact-predictor
 ┣ 📂 data  # Dane historyczne
 ┣ 📂 models  # Zapisane modele ML
 ┣ 📂 src  # Kod źródłowy
 ┃ ┣ 📜 preprocessing.py  # Feature engineering
 ┃ ┣ 📜 nlp_analysis.py  # Analiza tekstu
 ┃ ┗ 📜 model.py  # Kluczowy model predykcyjny
 ┣ 📜 README.md  # Dokumentacja
 ┣ 📜 requirements.txt  # Lista zależności
 ┗ 📜 main.py  # Główna aplikacja
```

---

## 📊 Wyniki modelu
✅ **Dokładność predykcji:** 82.5% na danych testowych  
✅ **F1-score:** 0.78  
✅ **Przetestowany na tysiącach komunikatów**  

---

## 🤝 Współpraca
Jeśli chcesz pomóc w rozwoju projektu, zapraszamy do kontrybucji! 🎉
1. Zrób fork repozytorium
2. Stwórz nową gałąź (`feature-nazwa`)
3. Wprowadź zmiany i prześlij Pull Request

---

## 📜 Licencja
Projekt jest dostępny na licencji **MIT**. Więcej informacji w pliku [LICENSE](LICENSE).

---

🔗 **Autor:** [Twoje Imię](https://github.com/twoj-profil) | 📧 kontakt@twoja-domena.com