Readme spamshield · MD
# 🛡️ SpamShield — SMS Spam Classification System
 
A production-grade SMS spam detector powered by a soft-voting ensemble of machine learning classifiers, served through a sleek Flask web application with real-time analysis and confidence gauges.
 
---
 
## 📖 Overview
 
SpamShield trains on the **UCI SMS Spam Collection** (5,574 real-world SMS messages) and classifies new messages as **spam** or **ham** with high accuracy. A TF-IDF pipeline feeds a calibrated ensemble of Complement Naïve Bayes, Logistic Regression, and Linear SVM. Results are surfaced through an interactive browser UI with probability gauges, feature signal bars, and pattern flags.
 
---
 
## ✨ Features
 
- **Ensemble classifier** — soft-voting combination of ComplementNB + LogisticRegression + calibrated LinearSVC
- **~98–99% accuracy** with F1 above 97% and ROC-AUC above 0.99
- **Rich text preprocessing** — URL tokenization, digit normalization, stop-word removal
- **EDA suite** — 6-panel exploration chart + ham vs. spam word clouds
- **Interactive web UI** — real-time spam probability gauges, feature signal bars, and detected pattern flags
- **Analysis history** — browse and replay recent classifications in-session
- **Google Colab compatible** — automatic ngrok proxy URL for public access
---
 
## 🗂️ Project Structure
 
```
SpamShield_Spam_Classification_System_.ipynb
│
├── Cell 1 — Install Dependencies
├── Cell 2 — Download Dataset              (UCI SMS Spam Collection)
├── Cell 3 — Dataset Exploration & Cleaning →  eda_exploration.png, wordclouds.png
├── Cell 4 — Train/Test Split & Model Training
└── Cell 5 — Launch SpamShield Web App    (Flask server + Colab proxy)
```
 
---
 
## 🛠️ Tech Stack
 
| Component | Library / Tool |
|---|---|
| Data handling | `pandas`, `numpy` |
| ML pipeline | `scikit-learn` (TF-IDF, ComplementNB, LogisticRegression, LinearSVC, VotingClassifier) |
| Visualisation | `matplotlib`, `seaborn`, `wordcloud` |
| Web server | `Flask`, `flask-cors` |
| Colab tunneling | `pyngrok` |
| Frontend | Vanilla HTML / CSS / JS (embedded in Flask) |
 
---
 
## 🚀 Getting Started
 
### Prerequisites
 
- Python 3.8+
- Jupyter Notebook or Google Colab
### Installation
 
```bash
pip install pyngrok flask flask-cors scikit-learn pandas numpy matplotlib seaborn wordcloud
```
 
### Running the Notebook
 
1. Open `SpamShield_Spam_Classification_System_.ipynb` in Jupyter or Colab.
2. **Cell 1** — installs all dependencies.
3. **Cell 2** — downloads the UCI SMS Spam Collection; falls back to an inline mini-dataset if the download fails.
4. **Cell 3** — cleans the data and generates `eda_exploration.png` and `wordclouds.png`.
5. **Cell 4** — trains the ensemble and prints a full classification report.
6. **Cell 5** — starts the Flask server and prints a clickable URL to open the web UI.
---
 
## 🤖 ML Pipeline
 
```
Raw SMS message
      ↓
Text Cleaning:
  • Lowercase
  • URLs  →  "urltoken"
  • Numbers (4+ digits)  →  "numtoken"
  • Remove punctuation & stop-words
      ↓
TF-IDF Vectorizer  (8 000 features, unigrams + bigrams)
      ↓
Soft-Voting Ensemble:
  ├─ Complement Naïve Bayes
  ├─ Logistic Regression
  └─ Calibrated Linear SVC
      ↓
Spam probability  +  Ham probability
```
 
### Custom features engineered per message
 
| Feature | Description |
|---|---|
| `msg_len` | Total character count |
| `word_count` | Number of words |
| `url_count` | Number of URLs detected |
| `digit_count` | Count of digit characters |
| `upper_ratio` | Fraction of uppercase characters |
 
---
 
## 📊 Dataset
 
**UCI SMS Spam Collection** — 5,574 real SMS messages labelled `ham` or `spam`.
 
| Split | Size |
|---|---|
| Training | ~4,459 messages (80%) |
| Test | ~1,115 messages (20%) |
| Spam ratio | ~13.4% |
 
> If the UCI download fails, the notebook falls back to a built-in 9-message mini-dataset so you can still run all cells.
 
---
 
## 📈 Model Performance
 
| Metric | Score |
|---|---|
| Accuracy | ~98–99% |
| F1 Score | > 97% |
| ROC-AUC | > 0.99 |
 
Evaluation includes a full `classification_report`, confusion matrix display, and ROC curve plot.
 
---
 
## 🌐 Web Interface
 
After Cell 5 launches the server, the Colab proxy URL opens a browser UI with three tabs:
 
### Classifier tab
- **Text input** — paste or type any SMS (up to 1,000 characters)
- **Example buttons** — pre-loaded spam and ham samples
- **Spam / Ham gauges** — animated circular probability displays
- **Message stats** — word count, character count, URL count
- **Feature signal bars** — UPPERCASE ratio, monetary signals, urgency language, URL presence, long numbers, message length
- **Pattern flags** — colour-coded tags for detected patterns (prize keywords, urgency language, phishing signals, CTAs, etc.)
### History tab
- Scrollable list of all analyses in the current session
- Click any entry to reload the message into the classifier
### About tab
- Summary of the ML pipeline, dataset, feature engineering, and performance
---
 
## 📸 EDA Outputs
 
| File | Contents |
|---|---|
| `eda_exploration.png` | 6-panel chart: label distribution, message length KDE, word count boxplot, uppercase ratio KDE, URL count bar, digit count violin |
| `wordclouds.png` | Side-by-side word clouds for ham and spam corpora |
 
---
 
## 🔮 Possible Improvements
 
- Add deep learning alternatives (BERT, DistilBERT fine-tuning)
- Support email / social media spam beyond SMS
- Build a persistent user feedback loop to retrain on misclassified examples
- Deploy as a standalone API (FastAPI + Docker)
- Add multilingual spam detection
---
 
## 📄 License
 
This project is for educational and personal use. The UCI SMS Spam Collection dataset is publicly available at the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/SMS+Spam+Collection).
