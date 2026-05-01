# Mesterséges Intelligencia I. – 9. tétel
## Valószínűségi modellek és gépi tanulás

---

## 1. Teljes együttes eloszlás

### 1.1 Fogalom
**Rövid definíció:**  
A **[[teljes együttes eloszlás]]** több valószínűségi változó együttes viselkedését írja le: `P(X1, X2, ..., Xn)`.

**Működési elv:**  
- Minden lehetséges értékkombinációhoz valószínűséget rendel.  
- Elvileg teljes információt tartalmaz a rendszerről.

**Egyszerű példa:**  
Időjárás (napos/esős) és forgalom (kicsi/nagy) közös eloszlása 4 kombinációt fed le.

**Vizsgán fontos kulcsszavak:**  
**[[teljes együttes eloszlás]]**, **`P(X1,...,Xn)`**, **közös valószínűség**

---

### 1.2 Probléma
**Rövid definíció:**  
A teljes együttes eloszlás gyakorlati gondja a méretrobbanás.

**Működési elv:**  
- A szükséges paraméterszám a változók számával exponenciálisan nő.  
- Nagy rendszereknél közvetlen tárolása és tanulása nehézkes.

**Egyszerű példa:**  
10 bináris változóhoz már `2^10 = 1024` kombináció tartozik.

**Vizsgán fontos kulcsszavak:**  
**paraméterrobbanás**, **exponenciális növekedés**, **skalázhatósági probléma**

---

## 2. Tömör reprezentáció

### 2.1 Alapötlet
**Rövid definíció:**  
A tömör reprezentáció célja a valószínűségi modell egyszerűsítése függetlenségi feltételek segítségével.

**Működési elv:**  
- Nem minden változó függ minden másiktól.  
- Ha ezt kihasználjuk, sokkal kevesebb paraméter kell.

**Egyszerű példa:**  
Ha egy tünet csak egy betegségváltozótól függ, nem kell minden más tényezőtől függően táblázni.

**Vizsgán fontos kulcsszavak:**  
**tömör modell**, **függetlenség**, **paramétercsökkentés**

---

### 2.2 Feltételes függetlenség
**Rövid definíció:**  
A **[[feltételes függetlenség]]** azt jelenti, hogy egy változó adott feltétel mellett független más változóktól.

**Működési elv:**  
- Jelentősen egyszerűsíti a valószínűségi felbontást.  
- Bayes-hálók alapelve.

**Egyszerű példa:**  
Eső és öntöző együtt befolyásolja a füves talaj nedvességét; bizonyos feltétel mellett más változók hatása elhanyagolható.

**Vizsgán fontos kulcsszavak:**  
**[[feltételes függetlenség]]**, **modell egyszerűsítés**, **faktorozás**

---

## 3. Bayes-hálók

### 3.1 Fogalom
**Rövid definíció:**  
A **[[Bayes-háló]]** irányított körmentes gráf (DAG), amely valószínűségi függőségeket ábrázol.

**Működési elv:**  
- Csúcsok: valószínűségi változók.  
- Élek: közvetlen függőségi kapcsolat.

**Egyszerű példa:**  
`Betegség -> Tünet` él azt jelzi, hogy a tünet eloszlása függ a betegségtől.

**Vizsgán fontos kulcsszavak:**  
**[[Bayes-háló]]**, **DAG**, **változók és függőségek**

---

### 3.2 Jellemzők
**Rövid definíció:**  
Bayes-hálóban minden csúcshoz lokális feltételes eloszlás tartozik.

**Működési elv:**  
- A globális eloszlás a lokális tényezők szorzataként írható fel.  
- Ez teszi kezelhetővé a nagy modelleket.

**Egyszerű példa:**  
`P(A,B,C)=P(A)P(B|A)P(C|A,B)` faktorozott alak.

**Vizsgán fontos kulcsszavak:**  
**lokális feltételes eloszlás**, **faktorizáció**, **valószínűségi gráfmodell**

---

### 3.3 Előnyök
**Rövid definíció:**  
A Bayes-háló előnye a tömörség és az értelmezhetőség.

**Működési elv:**  
- Kevesebb paraméter, mint teljes együttes eloszlásban.  
- Következtetés és valószínűségszámítás hatékonyabb lehet.

**Egyszerű példa:**  
Orvosi döntéstámogatásban valószínűségi diagnózist ad tünetek alapján.

**Vizsgán fontos kulcsszavak:**  
**tömör reprezentáció**, **hatékony következtetés**, **magyarázhatóság**

---

## 4. Gépi tanulás alapjai

### 4.1 Felügyelt tanulás
**Rövid definíció:**  
A **[[felügyelt tanulás]]** címkézett példákból tanul bemenet-kimenet leképezést.

**Működési elv:**  
- Tanító adathalmaz: `(x, y)` párok.  
- Cél olyan modell, ami új bemenetre jó előrejelzést ad.

**Egyszerű példa:**  
E-mailről eldönteni, spam-e, korábbi címkézett levelekből tanulva.

**Vizsgán fontos kulcsszavak:**  
**[[felügyelt tanulás]]**, **címkézett adat**, **predikció**

---

### 4.2 Feladatok
**Rövid definíció:**  
A felügyelt tanulás két alapfeladata az osztályozás és a regresszió.

**Működési elv:**  
- **Osztályozás**: diszkrét címkét jósol.  
- **Regresszió**: folytonos értéket jósol.

**Egyszerű példa:**  
Lakásár-becslés regresszió, hiteljóváhagyás osztályozás.

**Vizsgán fontos kulcsszavak:**  
**osztályozás**, **regresszió**, **tanulási feladat**

---

## 5. Tanulási módszerek

### 5.1 Döntési fák
**Rövid definíció:**  
A **[[döntési fa]]** szabályalapú modell, amely kérdéseken át jut döntéshez.

**Működési elv:**  
- Belső csomópontok feltételek, levelek osztályok/értékek.  
- Jól értelmezhető, vizuálisan követhető.

**Egyszerű példa:**  
„Kor > 30?” -> „jövedelem > X?” -> hiteldöntés.

**Vizsgán fontos kulcsszavak:**  
**[[döntési fa]]**, **magyarázhatóság**, **szabályalapú döntés**

---

### 5.2 Naiv Bayes
**Rövid definíció:**  
A **[[Naiv Bayes]]** Bayes-tételen alapuló, feltételes függetlenséget feltételező osztályozó.

**Működési elv:**  
- Gyors tanítás és előrejelzés.  
- Meglepően jól működik sok szöveges feladaton.

**Egyszerű példa:**  
Spam szűrés kulcsszavak valószínűsége alapján.

**Vizsgán fontos kulcsszavak:**  
**[[Naiv Bayes]]**, **Bayes-tétel**, **feltételes függetlenség**, **gyors osztályozó**

---

### 5.3 k-legközelebbi szomszéd (k-NN)
**Rövid definíció:**  
A **[[k-NN]]** példaalapú módszer: az új pontot a közeli tanítópéldák alapján sorolja be.

**Működési elv:**  
- Távolságmértéket használ.  
- `k` szomszéd osztályai alapján többségi döntés.

**Egyszerű példa:**  
Új virág mintát a legközelebbi ismert virágok címkéje alapján osztályoz.

**Vizsgán fontos kulcsszavak:**  
**[[k-NN]]**, **távolságalapú tanulás**, **többségi szavazás**

---

### 5.4 Mesterséges neuronhálók
**Rövid definíció:**  
A **[[neuronháló]]** egymásra épülő neuronszintekkel tanul nemlineáris mintákat.

**Működési elv:**  
- Bemenetek súlyozása és aktivációs függvények.  
- Tanuláskor a súlyok optimalizálása történik (pl. gradiens módszer).

**Egyszerű példa:**  
Képfelismerésnél mély háló tanulja meg a vizuális mintázatokat.

**Vizsgán fontos kulcsszavak:**  
**[[neuronháló]]**, **súlyok**, **aktiváció**, **tanítás**

---

### 5.5 Modellillesztés
**Rövid definíció:**  
A modellillesztés a paraméterek adatokhoz igazítása hibafüggvény minimalizálásával.

**Működési elv:**  
- Célfüggvény: veszteség minimalizálása tanító adaton.  
- Fontos az általánosítás, nem csak a tanítóhalmaz pontos illesztése.

**Egyszerű példa:**  
Lineáris modell paramétereit úgy választjuk, hogy a becslési hiba kicsi legyen.

**Vizsgán fontos kulcsszavak:**  
**modellillesztés**, **paramétertanulás**, **hiba minimalizálás**, **általánosítás**

---

## 6. Összehasonlítás

**Rövid definíció:**  
A modellek eltérő kompromisszumot adnak pontosság, sebesség és értelmezhetőség között.

**Működési elv:**  
- Döntési fa: jól magyarázható.  
- Naiv Bayes: gyors és egyszerű.  
- k-NN: tanulás helyett tárol és keres.  
- Neuronháló: nagy kifejezőerő, de komplexebb.

**Egyszerű példa:**  
Magyarázhatóság-igényes üzleti döntéshez fa, képfeldolgozáshoz háló lehet jobb.

**Vizsgán fontos kulcsszavak:**  
**modellkompromisszum**, **magyarázhatóság**, **pontosság**, **költség**

---

## 7. Összefüggések
**Rövid definíció:**  
A valószínűségi modellezés és a gépi tanulás ugyanarra a célra ad különböző megközelítéseket: bizonytalanság kezelése és predikció.

**Működési elv:**  
- Bayes-háló: explicit valószínűségi struktúra.  
- ML modellek: adatvezérelt függvénytanulás.  
- Gyakorlatban gyakran kombinálják őket.

**Egyszerű példa:**  
Diagnosztikában Bayes-szemlélet + tanuló osztályozó együtt használható.

**Vizsgán fontos kulcsszavak:**  
**valószínűségi modell**, **adatvezérelt tanulás**, **kombinált megközelítés**

---

## + Vizsgán érdemes még megemlíteni
- **[[túlillesztés]]** és ennek megelőzése (validáció, regularizáció említés).  
- Tanító, validáló és teszt adathalmaz szerepe.  
- Valószínűségi és determinisztikus döntési szemlélet különbsége.  
- Gyakorlati példák: spam szűrés, diagnózis, ajánlórendszer.

---

## Rövid szóbeli összefoglaló
A valószínűségi modellezésben a teljes együttes eloszlás elvileg mindent leír, de nagy rendszereknél túl sok paramétert igényel. Ezért függetlenségeket használunk, például Bayes-hálókban, ahol egy DAG és lokális feltételes eloszlások adják a modellt. A gépi tanulásban felügyelt módon címkézett adatokból tanulunk, jellemző feladat az osztályozás és regresszió. Fontos módszerek a döntési fa, Naiv Bayes, k-NN és neuronháló, mindegyik más kompromisszumot ad. A jó modell nem csak a tanító adatra illeszkedik, hanem új adaton is jól teljesít, ezért lényeges az overfitting kezelése és a helyes kiértékelés.

## Kulcsfogalmak
- [[teljes együttes eloszlás]]
- [[feltételes függetlenség]]
- [[Bayes-háló]]
- [[DAG]]
- [[felügyelt tanulás]]
- [[osztályozás]]
- [[regresszió]]
- [[döntési fa]]
- [[Naiv Bayes]]
- [[k-NN]]
- [[neuronháló]]
- [[modellillesztés]]
- [[túlillesztés]]
- [[tanító adat]]
- [[teszt adat]]

## Tipikus vizsgakérdések
1. **Mi a teljes együttes eloszlás fő problémája?**  
   Exponenciálisan sok paramétert igényel sok változó esetén.

2. **Miért fontos a feltételes függetlenség?**  
   Mert drasztikusan csökkenti a modell komplexitását.

3. **Mit ábrázol egy Bayes-háló?**  
   Változókat és köztük irányított függőségeket DAG formában.

4. **Mi a felügyelt tanulás lényege?**  
   Címkézett példákból bemenet-kimenet kapcsolat tanulása.

5. **Miben különbözik osztályozás és regresszió?**  
   Osztályozás diszkrét címkét, regresszió folytonos értéket becsül.

6. **Mi a Naiv Bayes fő feltételezése?**  
   A jellemzők feltételes függetlensége adott osztály mellett.

7. **Mi az overfitting?**  
   Amikor a modell tanító adatra túl jól illeszkedik, de új adaton rosszul teljesít.

## Minimum, amit tudni kell
- Teljes együttes eloszlás fogalma és méretproblémája.  
- Feltételes függetlenség szerepe tömörítésben.  
- Bayes-háló alap elemei (DAG, lokális valószínűségek).  
- Felügyelt tanulás definíciója.  
- Osztályozás és regresszió különbsége.  
- Döntési fa, Naiv Bayes, k-NN, neuronháló rövid jellemzése.  
- Modellillesztés és hiba minimalizálás alapötlete.  
- Overfitting és train/test adatszétválasztás fontossága.
