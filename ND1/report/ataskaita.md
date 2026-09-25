# Intelektualiųjų sistemų namų darbas Nr. 1

## Ranka rašytų skaitmenų klasifikavimas RBF ir MLP tinklais

**Studentas:** _įrašyti vardą ir pavardę_  
**Data:** _įrašyti_  

## 1. Pasirinktas pavyzdys

Pasirinktas ranka rašytų skaitmenų klasifikavimo pavyzdys, paremtas ankstesniu IS laboratoriniu darbu Nr. 4 ir viešu `scikit-learn` skaitmenų duomenų rinkiniu. Originalaus laboratorinio darbo šaltinis: <https://github.com/serackis/IS-Lab4>. Duomenų rinkinio dokumentacija: <https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_digits.html>.

Uždavinio tikslas – pagal 35 iš vaizdo gautus požymius nustatyti, kuris skaitmuo nuo 0 iki 9 pavaizduotas. Tai daugiaklasio klasifikavimo uždavinys.

## 2. Programinė ir aparatinė aplinka

- Operacinė sistema: Windows 11;
- Python 3.12.14;
- bibliotekos: NumPy 2.5.3, scikit-learn 1.9.1 ir Matplotlib 3.11.2;
- procesorius: AMD Ryzen 7 7800X3D (8 branduoliai / 16 loginių procesorių), operatyvioji atmintis: 31,2 GiB;
- papildomas GPU nenaudotas.

## 3. Atlikti veiksmai

1. Įdiegta Python virtualioji aplinka ir projekto bibliotekos.
2. Įkeltas 1797 skaitmenų vaizdų rinkinys.
3. 8×8 vaizdai sumažinti iki 7×5, todėl kiekvieną skaitmenį aprašo 35 požymiai.
4. Duomenys padalyti į 70 % mokymo ir 30 % testavimo dalis išlaikant klasių proporcijas.
5. Išmokyti RBF-13, RBF-8 ir 35–20–10 MLP modeliai.
6. Apskaičiuotas mokymo ir testavimo tikslumas, vidutinė vieno pavyzdžio klasifikavimo trukmė ir klaidų matrica.
7. Papildomam eksperimentui į testavimo požymius pridėtas Gauso triukšmas, kurio standartinis nuokrypis 0,25.

## 4. Rezultatai

| Modelis | Mokymo tikslumas | Testo tikslumas | Triukšmingo testo tikslumas | Vidutinė išvados trukmė |
|---|---:|---:|---:|---:|
| RBF-13 | 86,32 % | 87,59 % | 50,74 % | 0,00194 ms |
| RBF-8 | 76,77 % | 74,26 % | 42,59 % | 0,00145 ms |
| MLP-35-20-10 | 94,11 % | 92,59 % | 74,63 % | 0,00022 ms |

Į ataskaitą įterpiami programos sugeneruoti paveikslai `accuracy_comparison.png` ir `confusion_matrix.png`. Jie yra aiškus sėkmingo paleidimo ir gauto rezultato įrodymas.

## 5. Rezultatų interpretacija

RBF tinklas klasifikuoja pavyzdį pagal jo panašumą į parinktus centrus. Sumažinus centrų skaičių nuo 13 iki 8, mažėja modelio sudėtingumas, tačiau gali suprastėti gebėjimas atskirti panašius skaitmenis. MLP mokosi netiesinį požymių ir klasių ryšį naudodamas vieną paslėptą sluoksnį.

Triukšmingas testas imituoja pasikeitusias pradines sąlygas: prastesnį apšvietimą, segmentavimo netikslumus arba kitokią rašyseną. Tikslumo sumažėjimas parodo, kiek kiekvienas metodas jautrus įvesties pokyčiams.

## 6. Kilusios problemos ir sprendimai

- Ankstesnis MATLAB sprendimas šiame kompiuteryje nepasileido dėl `File system inconsistency` klaidos. Sprendimas perkeltas į Python/NumPy, išlaikant laboratoriniame darbe naudotas RBF ir 35–20–10 MLP struktūras.
- Kad rezultatai būtų atkartojami, visiems atsitiktiniams veiksmams nustatytos pastovios sėklos.
- Kad papildomas bandymas nebūtų painiojamas su mokymo duomenimis, triukšmas pridedamas tik nepriklausomai testavimo daliai.

## 7. Išvada

Geriausią 92,59 % testavimo tikslumą pasiekė 35–20–10 MLP. RBF centrų skaičių sumažinus nuo 13 iki 8, testavimo tikslumas sumažėjo nuo 87,59 % iki 74,26 %, todėl šiame duomenų rinkinyje papildomi centrai buvo svarbūs klasių įvairovei aprašyti. Triukšmingame teste visų modelių rezultatai suprastėjo, tačiau MLP išlaikė didžiausią 74,63 % tikslumą. Tai rodo, kad MLP geriau apibendrino požymių pokyčius nei abu mažieji RBF modeliai.
