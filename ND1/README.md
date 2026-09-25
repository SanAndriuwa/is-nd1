# IS namų darbas Nr. 1 – ranka rašytų skaitmenų klasifikavimas

Šiame projekte atkuriamas ir išplečiamas IS laboratorinio darbo Nr. 4 skaitmenų atpažinimo pavyzdys. Lyginami du radialinių bazinių funkcijų tinklai (RBF) su 13 ir 8 centrais bei 35–20–10 daugiasluoksnis perceptronas (MLP). Papildomam eksperimentui tie patys modeliai tikrinami su triukšmu papildytais testavimo vaizdais.

## Sprendžiamas uždavinys

Tai yra dešimties klasių klasifikavimo uždavinys. Kiekvienas 8×8 pilkumo pustonių skaitmens vaizdas sumažinamas iki 7×5, t. y. 35 požymių. Modelis turi priskirti vaizdą vienai iš klasių nuo 0 iki 9.

Naudojami metodai:

- RBF tinklas su tolimiausių taškų centrų parinkimu ir mažiausių kvadratų išėjimo sluoksniu;
- MLP su 20 `tanh` paslėptų neuronų ir `softmax` išėjimu;
- papildomas atsparumo eksperimentas, į testavimo požymius pridedant Gauso triukšmą.

## Šaltiniai

- Ankstesnis laboratorinis darbas: [serackis/IS-Lab4](https://github.com/serackis/IS-Lab4).
- Duomenys: `scikit-learn` pateikiamas [Optical Recognition of Handwritten Digits](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_digits.html) rinkinys, kilęs iš UCI duomenų saugyklos.

## Paleidimas

Rekomenduojama Python 3.11 arba naujesnė versija.

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python src/run_experiment.py --output-dir results
```

Programa automatiškai sukuria:

- `results/results.json` – rezultatus ir programinės aplinkos versijas;
- `results/results.csv` – glaustą rezultatų lentelę;
- `results/accuracy_comparison.png` – pradinio ir triukšmingo testo palyginimą;
- `results/confusion_matrix.png` – geriausio modelio klaidų matricą.

## Atkartojamumas

Naudojama fiksuota duomenų dalijimo sėkla `42`, MLP sėkla `4`, o triukšmo sėkla `123`. Duomenys dalijami į 70 % mokymo ir 30 % testavimo dalis išlaikant klasių proporcijas.

Trumpa ataskaita pateikta faile [`report/ataskaita.md`](report/ataskaita.md). Joje rezultatų lentelę reikia atnaujinti pagal konkrečiame kompiuteryje sugeneruotą `results/results.csv`.

## Patikrinto paleidimo rezultatai

2026-09-24 eksperimentas sėkmingai paleistas Windows 11 aplinkoje su Python 3.12.14. Gautas testavimo tikslumas: RBF-13 – 87,59 %, RBF-8 – 74,26 %, MLP – 92,59 %. Triukšmingame teste atitinkamai gauta 50,74 %, 42,59 % ir 74,63 %. Sugeneruoti CSV, JSON ir PNG įrodymai saugomi `results/` kataloge.

![Pradinio ir triukšmingo testo palyginimas](results/accuracy_comparison.png)

![Geriausio modelio klaidų matrica](results/confusion_matrix.png)
