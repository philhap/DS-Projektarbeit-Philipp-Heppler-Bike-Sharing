In dieser Arbeit wird eine Machine-Learning-basierte Nachfrageprognose für ein Bike-Sharing
System entwickelt, um Einblicke in die Nutzungsmuster und die Faktoren zu gewinnen, die die 
Nachfrage beeinflussen. Ziel ist es, präzise Modelle zu erstellen, die zukünftige Nachfrage mit 
Berücksichtigung saisonaler Schwankungen und langfristiger Trends vorhersagen können. 
Des Weiteren wird folgende Hypothese untersucht: Die Nachfrage lässt sich auch 
ausschließlich auf Basis von Wetterdaten präzise vorhersagen.  

Der verwendete Datensatz umfasst tägliche Angaben zur Bike-Sharing-Nutzung über zwei 
Jahre. Er besteht aus 15 Features, einem Target und 731 Instanzen. Wichtige Variablen 
umfassen: 
• Wetterbedingungen (Luftfeuchtigkeit, Temperatur, Windgeschwindigkeit) 
• Zeitliche Merkmale (Wochentag, Monat, Feiertag) 
• Zielvariable: Gesamtzahl der täglichen Fahrrad-Registrierungen 
Für den Hypothesentest wird ein weiterer Datensatz ohne zeitliche Merkmale erstellt. Er 
enthält ausschließlich meteorologische Daten.  

Es sind drei von vier Datentypen enthalten: nominale, diskrete und kontinuierliche Daten. Die 
kontinuierlichen Daten sind normalisiert und es sind keine fehlenden Daten im Datensatz 
vorhanden. Die Daten des Targets sind nominal – Es liegt ein Regressionsproblem vor. Den 
Kategorien der Features „weathersit“ und „season“ sind Nummern zugewiesen.  

Anhand der durchschnittlichen monatlichen und täglichen Nachfrage lässt sich eine klare 
saisonale Schwankung und das Abzeichnen eines positiven Trends erkennen. Zwischen 
Temperatur und Nachfrage lässt sich ein linearer Zusammenhang erkennen. Mit steigender 
Temperatur steigt die Nachfrage. Die Temperatur weist jedoch keinen 2-jährigen positiven 
Trend, sondern nur typische saisonale Schwankungen auf. Diese Erkenntnis lässt auf einen 
übergeordneten Trend schließen, was schon jetzt auf eine Widerlegung der aufgestellten 
Hypothese hinweist.   

Um das Datum als fortlaufende Zeitkomponente (Tage) in die Korrelationsermittlung einfließen 
zu lassen, wurde das Feature ‚date‘ mit dem Feature ‚date_numeric‘ ersetzt. Die Ermittlung 
der Korrelation ergibt eine Multikollinearität zwischen den unabhängigen Variablen „temp“ und 
„atemp“. Auch ‚date_numeric‘ und ‚year‘ korreliert sehr stark. Das Attribut ‚registered‘ weist mit 
einem Korrelationskoeffizient von 0.95 eine auffällig starke Beziehung zu dem Target 
‚distribution‘ auf. Da ‚registered‘ und ‚casual‘ die Gesamtnachfrage ‚distribution‘ ergibt, sind 
diese beiden Merkmale Teil des Targets und somit keine unabhängigen Variablen. 
Die unten abgebildete Matrix zeigt die Korrelationskoeffizienten. Sie zeigt die paarweisen 
Korrelationen zwischen allen Kombinationen aus zwei Variablen auf. Hier lässt sich die 
Multikollinearität und die Zusammenhänge zwischen den unabhängigen- und dem 
Zielvariablen ablesen. Sowohl saisonale Merkmale wie z.B. ‚date_numeric‘ als auch 
meteorologische Merkmale wie ‚atemp‘ korrelieren mit dem Zielwert ‚distribution‘.   

Nach der Korrelationsermittlung wurden einige Features aufgrund starker Multikollinearität und 
fehlender Unabhängigkeit angepasst. 
 
Zum besseren Verständnis wurden vor der Korrelationsermittlung den Kategorien der Features 
‚season‘ und ‚weathersit‘ wieder Namen zugewiesen und als Dummy-Variablen umgewandelt, 
um ihre Effekte in das Modell einzubringen. Unverständliche Variablennamen wie 
beispielsweise ‚cnt‘ (distribution) wurden umbenannt. Besonders wichtig war es, die Variable 
‚date_numeric‘ hinzuzufügen, um eine fortlaufende Zeitkomponente (Tage) für den Trend zu 
bieten. Redundante Merkmale wie ‚temp‘ (Temparatur) wurden entfernt, da sie starke 
Korrelationen mit ‚atemp‘ (gefühlter Temperatur) zeigten. Da ‘date_numeric‘ und ‚year‘ im 
Wesentlichen die gleichen Informationen über den Zeitverlauf enthalten, wurde die Variable 
‚year‘ entfernt. ‚date_numeric‘ fängt den fortlaufenden Zeittrend präziser ein und mit den 
Attributen ‚month‘ und ‚season‘ sind schon weitere saisonale Einteilungen des Zeitverlaufs 
enthalten. 
Die Variablen ‚registered‘ und ‚casual‘ sind nicht unabhängig und wurden aus dem Datensatz 
entfernt. Die ID Variable ‚instant‘ wurde ebenfalls entfernt.    

Modelle: 
(1) Random Forest 
(2) XGBoost 
(3) Lineare Regression 

Für die Modellauswertung wurden R² und MSE verwendet, um die Anpassungsfähigkeit und 
die Vorhersagegenauigkeit zu bewerten. 
 
In diesem Kapitel werden die wichtigsten Ergebnisse der drei Modelle – Lineare Regression, 
Random Forest und XGBoost – präsentiert und bewertet. Die Evaluation wurde basierend auf 
den Metriken R²-Score und MSE (Mean Squared Error) durchgeführt, die die Genauigkeit und 
die durchschnittliche quadratische Abweichung der Vorhersagen anzeigen. Zusätzlich zur 
numerischen Auswertung wurden für jedes Modell visuelle Darstellungen erstellt, um die 
Leistungsunterschiede und die Feature-Bedeutung besser zu veranschaulichen. 
 
Die lineare Regression dient als einfaches Basis-Modell zur Vorhersage der Nachfrage. Ihre 
Hauptstärke liegt in der schnellen Berechnung und der einfachen Interpretierbarkeit (siehe 
Punkt 3.1). Mit der linearen Regression wurde zunächst die generelle Beziehung zwischen 
den Features und der Nachfrage untersucht. Das Modell erzielte folgende Ergebnisse: 
• R²-Score: 0.8064985918589448 
• Mean Squared Error (MSE): 648059 
Die Ergebnisse zeigen, dass die lineare Regression eine grundlegende Vorstellung über die 
Nachfrage geben kann, jedoch Einschränkungen bei der Modellierung nichtlinearer 
Zusammenhänge aufweist. Der einfache, lineare Ansatz schränkt das Modell in Bezug auf die 
Erfassung saisonaler Schwankungen und komplexer Interaktionen zwischen Features wie 
temp und humidity ein, was zu einer begrenzten Modellleistung führt. Die lineare Regression 
diente daher als Ausgangspunkt und als Vergleichsbasis für die komplexeren Modelle 

Der Random Forest-Algorithmus wurde als nächstes trainiert, um nichtlineare 
Zusammenhänge zwischen den Features und der Nachfrage zu erfassen (siehe Punkt 3.1). 
Durch die Hyperparameter-Optimierung mittels Random Search wurden optimale 
Einstellungen gefunden, die die Leistung des Modells erheblich verbesserten (siehe Punkt 
3.2). Die finalen Ergebnisse für Random Forest sind: 
• Bester R²-Score: 0.8838688620496358 
• MSE-Wert nach Optimierung: 380030 
Die Visualisierungen der Ergebnisse verdeutlichten, dass Random Forest die Nachfrage unter 
Einbezug saisonaler Schwankungen und zeitlicher Besonderheiten, besser modellieren 
konnte als die lineare Regression. Bei der Featurs-Importance war date_numeric mit 39,3 % 
das wichtigste Merkmal, gefolgt von atemp (21,7 %) und season_Winter (8,7 %). Diese Werte 
verdeutlichen den Einfluss von zeitlichen und klimatischen Faktoren auf die Nachfrage. Andere 
saisonale Variablen, wie season_Summer, und Wetterbedingungen (weathersit_Partly 
Cloudy) trugen ebenfalls zur Modellleistung bei, wenn auch in geringerem Umfang. Darüber 
hinaus wurde eine Heatmap der Hyperparameter erstellt, um die Einflüsse der Parameter wie 
min_samples_split und max_depth auf die Modellleistung zu analysieren. Der finale 
Hyperparameter-Tuning-Prozess ergab die besten Werte für diese Parameter und damit auch 
eine höhere Stabilität und Robustheit (siehe Punkt 3.2) der Vorhersagen im Vergleich zur 
linearen Regression. 

XGBoost erzielte nach der Optimierung die besten Ergebnisse und erwies sich als das 
leistungsstärkste Modell in dieser Untersuchung. Aufgrund seines Boosting-Ansatzes konnte 
XGBoost komplexe Muster in den Daten optimal erkennen und saisonale sowie langfristige 
Trends effektiv integrieren [2]. Das Modell wurde ebenfalls mit Random Search optimiert, um 
die besten Hyperparameter für die Vorhersage zu finden. Die finalen Evaluationsergebnisse 
für XGBoost sind: 
• Bester R²-Score: 0.894794054013556 
• Mean Squared Error (MSE): 354361 
XGBoost konnte dank seiner Struktur den saisonalen Einfluss und die zeitlichen 
Schwankungen noch detaillierter erfassen. Die Feature-Importanz-Analyse zeigte, dass 
Variablen wie season_winter, date_numeric, und atemp die wichtigsten Features waren. Diese 
Werte verdeutlichen den Einfluss von zeitlichen und klimatischen Faktoren auf die Nachfrage. 
Dies deckt sich mit der Erwartung, dass meteorologische und zeitliche Faktoren wesentliche 
Einflussgrößen für die Nachfrage im Modell darstellen. 

Der Vergleich der Modelle zeigt, dass XGBoost und Random Forest aufgrund ihrer Fähigkeit, 
auch nichtlineare Muster zu modellieren (siehe Punkt 3.1), die höchste Genauigkeit erreicht. 
Die Feature-Importance-Analyse veranschaulichte, dass zeitliche und wetterabhängige 
Variablen entscheidend sind, was durch die hohe Gewichtung in den Modellen unterstützt wird.  
Zusammenfassend lässt sich feststellen, dass XGBoost die beste Prognosegenauigkeit und 
Modellleistung für die Vorhersage der Nachfrage erzielt, gefolgt vom Random Forest und 
schließlich der linearen Regression als Grundmodell. Die Dokumentation der Ergebnisse 
durch Metriken und Visualisierungen lieferte wertvolle Einblicke in die Einflüsse der gewählten 
Features und die Optimierungsschritte, die für die Modellverbesserung erforderlich waren. Die 
Balkendiagramme (Abbildung 6) unten visualisieren den Leistungsvergleich der Modelle. Die 
detaillierten Werte sind in der Tabelle 2 dokumentiert. 

In einem zusätzlichen Schritt wurde die Hypothese aufgestellt, dass sich die Nachfrage 
ausschließlich auf Basis von Wetterdaten präzise vorhersagen lässt. Um diese Annahme zu 
überprüfen, wurde der Datensatz auf wetterbezogene Variablen wie atemp, hum, windspeed 
und weathersit reduziert. Die Modelle Lineare Regression, Random Forest und XGBoost 
wurden erneut trainiert und evaluiert, um die Prognosegenauigkeit unter diesen 
eingeschränkten Bedingungen zu testen. 
Wie schon unter Punkt 2.2.1 erwartet, zeigen die Ergebnisse jedoch, dass die Nachfrage allein 
auf Grundlage der Wetterdaten nicht präzise vorhergesagt werden kann. Die Leistungswerte 
der Modelle waren allesamt deutlich niedriger als bei der Nutzung aller verfügbaren Features 
im Datensatz. Während der R²-Score des Random-Forest-Modells mit 0.5753 noch am 
höchsten ausfiel, lag er für XGBoost bei 0.5468 und für die lineare Regression sogar nur bei 
0.4575. Diese Werte verdeutlichen, dass die Vorhersage auf Basis der Wetterdaten nicht viel 
besser ist als ein Zufallsmodell. 
Besonders auffällig ist, dass der Random Forest in diesem Fall eine leicht bessere Leistung 
erbringt als XGBoost und die lineare Regression..Die Hypothese konnte somit widerlegt 
werden: Es ist erforderlich, neben den Wetterdaten auch andere Faktoren wie zeitliche und 
saisonale Merkmale einzubeziehen, um die Nachfrage präzise zu prognostizieren. Der Trend 
der steigenden Nachfrage spiegelt sich nicht in den Wetterdaten wider.  

Das Projekt hat gezeigt, dass die Nachfragevorhersage mittels Machine Learning effektiv 
durchgeführt werden kann. Zukünftig könnten zusätzliche Wettermerkmale und weitere 
externe Datenquellen die Modellgenauigkeit verbessern. Ein Ausbau der Vorhersage auf 
mehrere Jahre und die Nutzung optimierter Zeitreihen-Methoden bieten Potenzial für eine 
noch präzisere Nachfrageprognose. 
Die Beobachtungen führen zu folgenden Schlussfolgerungen: 
• komplexe Modelle wie Random Forest und XGBoost in der Lage sind, die Nachfrage 
unter Berücksichtigung von wetter- und zeitbasierten Einflussfaktoren besser 
vorherzusagen als eine einfache lineare Regression 
• Die Analyse der Feature-Wichtigkeit verdeutlichte zudem, dass zeitbezogene 
Variablen, wie etwa date_numeric, und saisonale Merkmale maßgeblich zur 
Modellgenauigkeit beitragen 
• Die Widerlegung der Hypothese betont die Bedeutung eines umfassenden 
Datensatzes, der auch langfristige Trends und saisonale Muster enthält, um die 
tatsächliche Nachfrage akkurat abzubilden. 

A Codebase 
Alle Programmierungen wurden in Python 3 durchgeführt. Die verwendeten Modelle stammen alle 
aus der Bibliothek scikit-learn, mit Ausnahme des XGBoost-Algorithmus. Um XGBoost verwenden zu 
können, muss die Python-Bibliothek xgboost installiert sein. Nach der Installation kann XGBoost über 
die scikit-learn-Schnittstelle genutzt werden, die eine vereinfachte Alternative zur komplexeren 
nativen Schnittstelle bietet. 
Der Code für das hier vorgestellte Projekt ist auf GitHub verfügbar: 
https://github.com/philhap/DS-Projektarbeit-Philipp-Heppler-Bike-Sharing 
Der Datensatz kann unter Bike Sharing – UCI Machine Learning Repository heruntergeladen 
werden. 

Literaturverzeichnis 
[1] 
Breiman, L. (2001). Random forests. Machine Learning, 45(1), 5-32. 
[2] Chen, T., & Guestrin, C. (2016). XGBoost: A scalable tree boosting system. In 
Proceedings of the 22nd ACM SIGKDD international conference on knowledge 
discovery and data mining. 
[3] Weisberg, S. (2005). Applied linear regression (Vol. 528). John Wiley & Sons. 
[4] Kuhn, M., & Johnson, K. (2013). Applied predictive modeling. Springer. 
[5] James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). An introduction to statistical 
learning with applications in R. Springer. 
[6] Bergstra, J., & Bengio, Y. (2012). Random Search for Hyper-Parameter Optimization. 
Journal of Machine Learning Research, 13, 281-305. 
[7] Géron, A. (2019). Hands-On Machine Learning with Scikit-Learn, Keras, and 
TensorFlow. O'Reilly Media. 
