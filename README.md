# 🚲 Bike Sharing Demand Forecasting

Projektarbeit im Rahmen der Data-Science-Zertifizierung (2024)  
Vorhersage der täglichen Nachfrage nach Leihfahrrädern auf Basis von Wetter- und Zeitdaten mit verschiedenen Regressionsmodellen.

---

## 📌 Projektziel

Ziel war es, ein Vorhersagemodell für die Anzahl täglicher Fahrradverleihungen zu entwickeln. Der Fokus lag auf dem Erkenntnisgewinn und der Modellierung der Zusammenhänge zwischen Nachfrage, Wetterbedingungen und zeitlichen Faktoren. Grundlage war der öffentliche "Bike Sharing Demand"-Datensatz (Kaggle).

---

## 🔍 Vorgehensweise

- Datenexploration: Datenlage/Visualisierung
- Datenvorbereitung: Feature Engineering
- Modellierung & Vergleich dreier Regressionsmodelle:
  - Random Forest
  - XGBoost
  - Lineare Regression (Baseline)
- Evaluierung: MSE, R²-Score, Visualisierung der Prognosequalität, Hypothese

---

## 🧪 Hypothese

> *„Die Nachfrage lässt sich auch ausschließlich auf Basis von Wetterdaten präzise vorhersagen.“*

Zur Überprüfung wurde der Datensatz auf wetterbezogene Variablen (wie `atemp`, `hum`, `windspeed`, `weathersit`) reduziert und erneut modelliert.  
**Ergebnis:** Die Vorhersagegenauigkeit sank deutlich, was die Hypothese widerlegte. Neben Wetterdaten sind insbesondere zeitliche und saisonale Faktoren (z. B. Uhrzeit, Wochentag) entscheidend für verlässliche Prognosen. Es zeichnet sich ein langfristiger positiver Trend der Nachfrage ab.

---

## 📊 Ergebnisse

- **XGBoost** erzielte die beste Prognosegenauigkeit, gefolgt vom **Random Forest**.
- Die **lineare Regression** diente als einfaches Vergleichsmodell mit deutlich schwächerer Leistung.
- Die **Feature-Importance-Analyse** zeigte, dass sowohl zeitliche als auch wetterbezogene Merkmale eine entscheidende Rolle spielen.
- Der Versuch, nur mit Wetterdaten zu prognostizieren, lieferte deutlich schlechtere R²-Werte (z. B. RF: 0.575, XGB: 0.547, LR: 0.458).

---

## 🛠️ Verwendete Technologien

- Python, Pandas, Matplotlib, Seaborn
- Scikit-learn, XGBoost
- Jupyter Notebooks

---

## 👤 Autor

Philipp Heppler  
Zertifizierter Data Scientist (2024) mit Fokus auf anwendungsorientierte Machine-Learning-Projekte

🔗 [Weitere Projekte ansehen – z. B. Predictive Maintenance](https://github.com/philhap/predictive-maintenance-light)
