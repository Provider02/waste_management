# Využitie metód strojového učenia v odpadovom hospodárstve

Tento repozitár bol vytvorený ako súčasť diplomovej práce na tému Využitie metód strojového učenia v odpadovom hospodárstve (2025). Obsahom tohto repozitára je kompletný pipeline pre predspracovanie, exploratívnu analýzu a predikciu denného množstva komunálneho odpadu na šiestich datasetoch z troch krajín, s využitím piatich rôznych modelov strojového učenia.


## Abstrakt práce

Efektívne odpadové hospodárstvo predstavuje jednu z kľúčových výziev súčasných mestských samospráv. V tejto práci sa zaoberáme využitím metód strojového učenia pre predikciu denného množstva vyváženého komunálneho odpadu. V rámci práce porovnávame výkonnosť viacerých modelov, medzi ktoré patria modely SARIMA, XGBoost, Random Forest, Prophet a LSTM, pričom vyhodnocujeme ich schopnosť zachytiť sezónne vzory a predpovedať budúce hodnoty v časovom rade. Súčasťou práce je taktiež podanie teoretického prehľadu existujúcich prístupov v oblasti predikcie tvorby odpadu s využitím strojového učenia


## Príprava prostredia a kódu

Kód obsiahnutý v tomto repozitári bol použitý a je vhodný na použitie prostredníctvom platformy Google Colab & Google Drive.
 
1. Prevzatie / Stiahnutie
 
   Obsah repozitára stiahnite a nahrajte na Google Drive alebo použite kód pre prevzatie:
   ```sh
   git clone https://github.com/Provider02/waste_management.git
   ```
 
2. Štruktúra projektu
 
   Upravte súbory do nasledujúcej štruktúry na Google Drive:
 
   <pre>
   DP/
   └─── 00_data/
     | boralasgamuwa_uc_2012-2018.csv
     | dehiwala_mc_2012-2018.csv
     | homagama_ps_2012-2018.csv
     | moratuwa_mc_2014-2018.csv
     | open_source_austin_daily_waste_2003_jan_2021_jul.csv
     | open_source_ballarat_daily_waste_2000_jul_2015_mar.csv
  
   └─── 01_data_processing_eda/
     | data_processing_eda_boralasgamuwa.ipynb
     | data_processing_eda_dehiwala.ipynb
     | data_processing_eda_homagama.ipynb
     | data_processing_eda_moratuwa.ipynb
     | data_processing_eda_austin.ipynb
     | data_processing_eda_ballarat.ipynb
  
   └─── 02_processed_data/
     | boralasgamuwa_processed.csv
     | dehiwala_processed.csv
     | ...
  
   └─── 03_visualizations/
     └─── EDA
       └─── Boralasgamuwa/
       └─── Dehiwala/
       └─── ...
     └─── Experiments
       └─── SARIMA/
       └─── XGBoost/
       └─── LSTM/
       └─── RF/
       └─── Prophet/
     └─── Results/

   └─── 04_experiments/
     | prediction_baseline.ipynb
     | prediction_sarima.ipynb
     | prediction_xgboost.ipynb
     | prediction_lstm.ipynb
     | prediction_rf.ipynb
     | prediction_prophet.ipynb
     | results_comparison.ipynb
  
   └─── 05_prediction_results/
     | baseline_results.csv
     | sarima_results.csv
     | xgboost_results.csv
     | lstm_results.csv
     | rf_results.csv
     | prophet_results.csv
     | all_models_comparison.csv
     | improvement_over_baseline.csv
     | wilcoxon_sginificance.csv
   </pre>
 
3. Nastavenie ciest
 
   V každom notebooku je potrebná úprava označená komentárom:
   <pre>
   !!! ACTION REQUIRED !!! - update path to your Google Drive project folder
   </pre>
   V tejto časti kódu je potrebné upraviť premennú `DRIVE_PATH` podľa usporiadania priečinkov používateľa na Google Drive.
 
4. Spustenie notebookov
 
   Notebooky je potrebné spúšťať v nasledujúcom poradí:
   
   **Krok 1 — Predspracovanie dát a EDA** (priečinok `01_data_processing_eda/`)
   
   Spustite postupne notebooky pre každý dataset. Tieto notebooky vykonajú:
   * Načítanie, filtráciu a agregáciu dát na denné hodnoty
   * Pridanie kalendárnych príznakov a sviatkov príslušnej krajiny
   * Stiahnutie a integráciu meteorologických dát prostredníctvom API Meteostat
   * Analýzu chýbajúcich hodnôt cieľového atribútu
   * Konštrukciu príznakov (lag features, kĺzavé štatistiky, cyklické kódovanie)
   * Exploratívnu analýzu dát s vizualizáciami
   * Korelačnú analýzu a autokorelačnú analýzu (ACF/PACF)
   * Export spracovaného datasetu do priečinka `02_processed_data/`
 
   **Krok 2 — Predikcie** (priečinok `04_experiments/`)
   
   Po úspešnom spracovaní všetkých datasetov spustite predikčné notebooky. Každý notebook natrénuje príslušný model na všetkých šiestich datasetoch a uloží výsledky do priečinka `05_prediction_results/`. Notebooky je možné spúšťať v ľubovoľnom poradí.
 
   **Krok 3 — Porovnanie výsledkov** (priečinok `04_experiments/`)
   
   Po dokončení všetkých predikčných notebookov spustite `results_comparison.ipynb`, ktorý načíta výsledky všetkých modelov a vytvorí porovnávacie tabuľky a vizualizácie.


   ## Použité dáta
 
Projekt využíva šesť datasetov denného množstva vyvezeného komunálneho odpadu:
 
| Dataset | Región | Obdobie | Priem. množstvo |
|---------|--------|---------|-----------------|
| Boralesgamuwa UC | Srí Lanka | 2012–2018 | ~27 ton/deň |
| Dehiwala MC | Srí Lanka | 2012–2015 | ~142 ton/deň |
| Homagama PS | Srí Lanka | 2012–2018 | ~33 ton/deň |
| Moratuwa MC | Srí Lanka | 2015–2018 | ~76 ton/deň |
| Austin TX | USA | 2003–2021 | ~1480 ton/deň |
| Ballarat | Austrália | 2001–2014 | ~69 ton/deň |
 
Štyri datasety zo Srí Lanky pochádzajú z repozitára [UCloudMl/solid-waste-prediction](https://github.com/UCloudMl/solid-waste-prediction). Datasety z Austinu a Ballaratu sú verejne dostupné open-source datasety, taktiež dostupné v spomenutom repozitári.
 
Meteorologické dáta (priemerná denná teplota, zrážky) boli získané prostredníctvom API služby [Meteostat](https://meteostat.net/) pre geografickú polohu príslušnú každému datasetu.


## Použité modely
 
V rámci práce bolo implementovaných a porovnaných päť predikčných modelov:
 
| Model | Typ | Popis |
|-------|-----|-------|
| SARIMA | Štatistický baseline | Sezónny autoregresný model s parametrami (1,0,1)(1,1,1,7) |
| Random Forest | Ensemble (bagging) | Súbor rozhodovacích stromov, 300 estimátorov |
| XGBoost | Ensemble (boosting) | Gradient boosting ansámblový model |
| LSTM | Deep learning | Dvojvrstvová rekurentná neurónová sieť s lookback 30 dní |
| Prophet | Špecializovaný | Model od Meta pre časové rady so sezónnosťou |
 
 
## Konštruované príznaky
 
Oproti referenčnému projektu boli dáta obohatené o nasledujúce príznaky:
 
* **Kalendárne:** rok, mesiac, deň v týždni, deň v roku, týždeň v roku
* **Binárne:** víkend, sviatok, deň po víkende, deň po sviatku, deň po chýabjúcom zázname
* **Meteorologické:** priemerná teplota, zrážky
* **Lag príznaky:** hodnoty z predchádzajúcich 1, 2, 3, 7, 14 a 30 dní
* **Kĺzavé štatistiky:** 7-dňový a 30-dňový priemer a štandardná odchýlka
* **Cyklické kódovanie:** sínus/kosínus transformácie mesiaca a dňa v týždni
 
 
## Rozšírenia oproti referenčnému projektu
 
Oproti pôvodnému projektu [UCloudMl/solid-waste-prediction](https://github.com/UCloudMl/solid-waste-prediction) boli realizované nasledujúce rozšírenia:
 
* Integrácia meteorologických dát prostredníctvom API Meteostat
* Iný prístup k chýabjúcim záznamom, ktoré sú dopĺňané nulovou hodnotou len pri potvrdenom prípade kumulácie odpadu
* Pridanie príznakov akumulácie odpadu (deň po víkende, deň po sviatku, deň po chýabjúcom zázname)
* Korelačná analýza príznakov a autokorelačná analýza (ACF/PACF)
* Kvartilová analýza vplyvu meteorologických podmienok na tvorbu odpadu
* Testovanie predikcie modelov na viacerých rozdeleniach dát
* Test štatistickej významnosti rozdielov medzi modelmi
 
 
## Technológie
 
* **Jazyk:** Python 3.10+
* **Prostredie:** Google Colab
* **Hlavné knižnice:** pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost, statsmodels, prophet, meteostat, holidays
 
 
## Autor
 
* [**Jakub Paranič**](https://github.com/Provider02) — Fakulta elektrotechniky a informatiky, Technická univerzita v Košiciach
 
 
## Uznanie
 
Táto práca vychádza z repozitára [**UCloudMl/solid-waste-prediction**](https://github.com/UCloudMl/solid-waste-prediction) a príslušného článku:
 
> Mudannayake, O., Rathnayake, D., Herath, J.D., Fernando, D.K., & Fernando, M. (2022). *Exploring Machine Learning and Deep Learning Approaches for Multi-Step Forecasting in Municipal Solid Waste Generation.* IEEE Access, 10, 122570–122585.
