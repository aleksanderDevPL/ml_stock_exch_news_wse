# 📈 AI Stock Price Change News Predictor

![NLP](https://img.shields.io/badge/NLP-yellow)
![Finance](https://img.shields.io/badge/Finance-green)
![R](https://img.shields.io/badge/R-blue)  
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-blue)  
![Text Classification](https://img.shields.io/badge/Text%20Classification-orange)  


## 🧠 O projekcie
**AI Stock Price Change News Predictor** to model uczenia maszynowego analizujący komunikaty bieżące i okresowe spółek giełdowych. Celem modelu jest przewidywanie wpływu treści komunikatów na zmiany cen akcji w dniu publikacji.

Model został wytrenowany na podstawie tysięcy historycznych publicznych komunikatów giełdowych oraz historycznych cen akcji spółek notowanych na Giełdzie Papierów Wartościowych w Warszawie (Warsaw Stock Exchange). 

Model wykorzystuje **inżynierię cech (Feature Engineering)** oraz **analizę tekstu (NLP)** do wyodrębnienia istotnych informacji wpływających na rynek.

---

## ⚙️ Jak działa model?
1. Pobiera treść komunikatu giełdowego.
2. Przetwarza tekst za pomocą NLP (tokenizacja, embeddingi, analiza sentymentu).
3. Przewiduje czy komunikat może wywrzeć istotny wpływ na zmianę ceny akcji w danym dniu. Poprzez istotny wpływ rozumie się zmianę kursu akcji danej spółki różniącą się o 0,75% vs. zmiana ceny tzw. szerokiego rynku (indeksu WIG).

---

## 🛠 Technologie
- 📊 **Uczenie maszynowe:** caret, randomForest, e1071
- 🔍 **Analiza tekstu (NLP):** quanteda, lsa, tokenizacja, TF-IDF, bigramy
- 📈 **Dane źródłowe:** Analiza klasyfikacji tekstu (modelowanie etykiet)
- 🛠 **Feature Engineering:** Redukcja wymiarowości (irlba – SVD), podobieństwo kosinusowe, długość tekstu


---

## 📌 Przykład użycia

```R
libraries <- c("caret", "quanteda", "e1071", "ggplot2", "irlba", "randomForest", "dplyr", "readxl", "doSNOW", "lsa")
lapply(libraries, require, character.only = TRUE)

load_data <- function(path) {
  dataset <- read_excel(path) %>% select(2, 4) %>% rename(Text = 2, Label = 4)
  dataset$Label <- as.factor(dataset$Label)
  dataset$TextLength <- nchar(dataset$Text)
  dataset
}

split_data <- function(dataset, split_ratio = 0.7, seed = 32911) {
  set.seed(seed)
  indexes <- createDataPartition(dataset$Label, p = split_ratio, list = FALSE)
  list(train = dataset[indexes,], test = dataset[-indexes,])
}

process_text <- function(text_data, stopwords) {
  tokens <- tokens(text_data, what = "word", remove_numbers = TRUE, remove_punct = TRUE, remove_symbols = TRUE, remove_hyphens = TRUE)
  tokens <- tokens_tolower(tokens)
  tokens_select(tokens, stopwords, selection = "remove")
}

calculate_tfidf <- function(tokens) {
  dfm_data <- dfm(tokens, tolower = FALSE)
  tf <- function(row) row / sum(row)
  idf <- function(col) log10(length(col) / length(which(col > 0)))
  
  tf_matrix <- apply(as.matrix(dfm_data), 1, tf)
  idf_vector <- apply(as.matrix(dfm_data), 2, idf)
  t(apply(tf_matrix, 2, function(x) x * idf_vector))
}

create_cv_control <- function() {
  set.seed(49701)
  trainControl(method = "repeatedcv", number = 10, repeats = 3)
}

train_model <- function(data, method, cv_control) {
  cl <- makeCluster(detectCores() - 1, type = "SOCK")
  registerDoSNOW(cl)
  model <- train(Label ~ ., data = data, method = method, trControl = cv_control, tuneLength = 7)
  stopCluster(cl)
  model
}

---

## 📊 Wyniki modelu
✅ **Dokładność predykcji:** 82.5% na danych testowych  
✅ **F1-score:** 0.78  
✅ **Przetestowany na tysiącach komunikatów**  


---

## 📜 Dostęp do kodu
Kod źródłowy tego projektu nie jest publicznie dostępny.  
Jeśli jesteś zainteresowany współpracą lub testowaniem modelu, skontaktuj się ze mną:  

📧 Email: [aleksander.herc@wp.pl](mailto:aleksander.herc@wp.pl) 

