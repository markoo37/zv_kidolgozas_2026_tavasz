# Mesterséges Intelligencia I. – 8. tétel
## Keresési feladatok, játékok, CSP

---

## 1. Keresési feladat

### 1.1 Feladatreprezentáció
**Rövid definíció:**  
Az MI keresési feladatot állapotok és állapotátmenetek rendszerével modellezzük.

**Működési elv:**  
- **[[állapottér]]**, kezdőállapot, célállapot, operátorok.  
- Opcionálisan költségfüggvény is tartozik hozzá.  
- Megoldás: olyan műveletsor, ami a célhoz vezet.

**Egyszerű példa:**  
Labirintusban a rácspontok állapotok, a lépések operátorok.

**Vizsgán fontos kulcsszavak:**  
**[[állapottér]]**, **kezdőállapot**, **célállapot**, **operátor**, **költségfüggvény**

---

### 1.2 Állapottér gráf
**Rövid definíció:**  
Az állapottér gráfban a csúcsok állapotok, az élek műveletek.

**Működési elv:**  
- Keresés során gráfbejárást végzünk.  
- A cél egy kezdőtől célállapotig vezető út megtalálása.

**Egyszerű példa:**  
8-kirakó feladatban minden konfiguráció egy csúcs.

**Vizsgán fontos kulcsszavak:**  
**állapottér gráf**, **csúcs/él**, **megoldási út**

---

## 2. Vak keresés (uninformed search)

### 2.1 Szélességi keresés (BFS)
**Rövid definíció:**  
A **[[BFS]]** rétegenként járja be az állapotteret.

**Működési elv:**  
- Sor (queue) alapú bejárás.  
- Egységköltségnél legrövidebb utat ad.  
- Memóriaigénye magas lehet.

**Egyszerű példa:**  
Minimális lépésszámú út keresése rácsos térképen.

**Vizsgán fontos kulcsszavak:**  
**[[BFS]]**, **réteges bejárás**, **legrövidebb út**, **nagy memória**

---

### 2.2 Mélységi keresés (DFS)
**Rövid definíció:**  
A **[[DFS]]** egy ágat mélyen bejár, mielőtt visszalép.

**Működési elv:**  
- Verem/rekurzió alapú.  
- Memóriaigénye kisebb lehet, de nem ad garantált optimális utat.

**Egyszerű példa:**  
Játékfában gyorsan találhat valamilyen megoldást, de nem feltétlen a legjobbat.

**Vizsgán fontos kulcsszavak:**  
**[[DFS]]**, **mélységi bejárás**, **verem**, **nem optimális**

---

### 2.3 Iteratív mélyítés (IDDFS)
**Rövid definíció:**  
Az **[[IDDFS]]** ismételt mélységkorlátos DFS, amely ötvözi BFS és DFS előnyeit.

**Működési elv:**  
- Növekvő mélységhatárral többször indít DFS-t.  
- Kisebb memóriaigény, mégis rétegszintű megtalálás.

**Egyszerű példa:**  
Ismeretlen megoldási mélységnél gyakran jó kompromisszum.

**Vizsgán fontos kulcsszavak:**  
**[[IDDFS]]**, **mélységkorlát**, **BFS+DFS kompromisszum**

---

## 3. Informált keresés (informed search)

### 3.1 Heurisztika
**Rövid definíció:**  
A **[[heurisztika]]** becslést ad arra, mennyire „messze” van az állapot a céltól.

**Működési elv:**  
- `h(n)` irányítja a keresés fókuszát.  
- Jó heurisztika sok felesleges állapotot kivág.

**Egyszerű példa:**  
Labirintusban Manhattan-távolság becsülheti a célig hátralévő utat.

**Vizsgán fontos kulcsszavak:**  
**[[heurisztika]]**, **`h(n)`**, **becslés**, **keresés gyorsítása**

---

### 3.2 Mohó keresés (Greedy best-first)
**Rövid definíció:**  
A mohó keresés mindig a legígéretesebbnek becsült csúcsot választja `h(n)` alapján.

**Működési elv:**  
- Csak a becslést nézi, az eddigi költséget nem.  
- Gyors lehet, de nem garantáltan optimális.

**Egyszerű példa:**  
Elsőre jó irányba megy, de könnyen zsákutcába kerülhet.

**Vizsgán fontos kulcsszavak:**  
**mohó keresés**, **Greedy best-first**, **gyors de nem optimális**

---

### 3.3 A* algoritmus
**Rövid definíció:**  
Az **[[A*]]** keresés az eddigi költséget és a heurisztikus becslést kombinálja: `f(n)=g(n)+h(n)`.

**Működési elv:**  
- `g(n)`: kezdőtől mért költség.  
- `h(n)`: célig becsült költség.  
- Megengedett (admissible) heurisztikával optimális.

**Egyszerű példa:**  
Útvonaltervezésnél A* gyakran optimális és gyors is.

**Vizsgán fontos kulcsszavak:**  
**[[A*]]**, **`f=g+h`**, **admissible heurisztika**, **optimális keresés**

---

## 4. Kétszemélyes zéró összegű játékok

### 4.1 Alapfogalom
**Rövid definíció:**  
Zéró összegű játékban az egyik játékos nyeresége a másik vesztesége.

**Működési elv:**  
- MAX saját hasznát maximalizálja, MIN ezt minimalizálja.  
- A döntési folyamat játékfával modellezhető.

**Egyszerű példa:**  
Sakkszerű lépésváltós játékok közelítése.

**Vizsgán fontos kulcsszavak:**  
**zéró összegű játék**, **MAX/MIN**, **játékfa**

---

### 4.2 Minimax algoritmus
**Rövid definíció:**  
A **[[Minimax]] algoritmus optimális ellenféljáték feltételezése mellett választ lépést.

**Működési elv:**  
- Leveleknél értékelés, majd visszaterjesztés a gyökér felé.  
- MAX a legnagyobbat, MIN a legkisebbet választja.

**Egyszerű példa:**  
Kis mélységű játékfán teljesen bejárható és optimális döntést ad.

**Vizsgán fontos kulcsszavak:**  
**[[Minimax]]**, **visszaterjesztés**, **optimális ellenfél**

---

### 4.3 Alfa-béta metszés
**Rövid definíció:**  
Az **[[alfa-béta metszés]]** a Minimax gyorsító technikája.

**Működési elv:**  
- `α`: eddigi legjobb MAX alsó korlát.  
- `β`: eddigi legjobb MIN felső korlát.  
- Ha `α >= β`, az ág tovább már nem befolyásolja a döntést, levágható.

**Egyszerű példa:**  
Jó lépéssorrend mellett lényegesen kevesebb csúcsot kell kiértékelni.

**Vizsgán fontos kulcsszavak:**  
**[[alfa-béta metszés]]**, **α**, **β**, **pruning**, **Minimax gyorsítás**

---

## 5. Korlátozás kielégítési feladat (CSP)

### 5.1 Alapfogalmak
**Rövid definíció:**  
A **[[CSP]]** feladat változókból, tartományokból és megszorításokból áll.

**Működési elv:**  
- Minden változóhoz értéket keresünk a saját domainből úgy, hogy minden megszorítás teljesüljön.

**Egyszerű példa:**  
Sudoku: cellák változók, számok domain, sor/oszlop/blokk szabályok megszorítások.

**Vizsgán fontos kulcsszavak:**  
**[[CSP]]**, **változó**, **domain**, **constraint**

---

### 5.2 Megoldás
**Rövid definíció:**  
CSP megoldás teljes és konzisztens értékadás.

**Működési elv:**  
- Teljes: minden változó kap értéket.  
- Konzisztens: nincs megszorítássértés.

**Egyszerű példa:**  
Naptártervezésben minden esemény kap időpontot ütközés nélkül.

**Vizsgán fontos kulcsszavak:**  
**teljes értékadás**, **konzisztencia**, **megoldásfeltétel**

---

### 5.3 Megoldási módszerek
**Rövid definíció:**  
A CSP tipikus megoldása visszalépéses keresés és megszorításalapú szűkítés kombinációja.

**Működési elv:**  
- **[[backtracking]]**: próbálkozás és visszalépés konfliktusnál.  
- **[[forward checking]]**: előre kiszűri lehetetlen értékeket.  
- Propagáció tovább erősítheti a szűkítést.

**Egyszerű példa:**  
Színezési feladatnál már részleges értékadásnál kizárhatók tiltott színek.

**Vizsgán fontos kulcsszavak:**  
**[[backtracking]]**, **[[forward checking]]**, **megszorítás propagáció**

---

### 5.4 Heurisztikák CSP-ben
**Rövid definíció:**  
Heurisztikák csökkentik a keresési teret CSP-knél.

**Működési elv:**  
- **[[MRV]]**: legkevesebb maradék értékű változó választása.  
- Legkorlátozóbb változó előre vétele.  
- Értéksorrend is optimalizálható.

**Egyszerű példa:**  
Sudokunál először azt a cellát töltjük, ahol a legkevesebb jelölt maradt.

**Vizsgán fontos kulcsszavak:**  
**[[MRV]]**, **változóválasztási heurisztika**, **értékválasztási stratégia**

---

## 6. Összefüggések
**Rövid definíció:**  
Az MI problémamegoldás közös kerete a keresés, amit heurisztikákkal gyorsítunk.

**Működési elv:**  
- Vak keresés általános, de költséges lehet.  
- Informált keresés gyorsabb, ha jó a heurisztika.  
- Gyakori kompromisszum: optimális megoldás vs számítási idő.

**Egyszerű példa:**  
A* optimális lehet, de memóriaigényesebb, mint egyszerűbb heurisztikus keresések.

**Vizsgán fontos kulcsszavak:**  
**keresési keret**, **heurisztika szerepe**, **optimalitás-gyorsaság trade-off**

---

## + Vizsgán érdemes még megemlíteni
- **[[BFS]] vs [[DFS]]**: optimálisság vs memóriaigény.  
- **[[A*]]** csak megengedett heurisztikával garantáltan optimális.  
- Minimax nagy játékfán drága, ezért kell alfa-béta metszés.  
- CSP gyakorlati példa: Sudoku, órarendkészítés.

---

## Rövid szóbeli összefoglaló
A mesterséges intelligenciában sok feladat keresési problémaként modellezhető állapottérrel, operátorokkal és célállapottal. Vak keresésnél a BFS és DFS alapmódszerek, míg informált keresésnél heurisztikákat használunk, például A* algoritmust, ahol `f=g+h`. Játékoknál kétszemélyes zéró összegű modellben a minimax ad döntési alapot, amit alfa-béta metszéssel gyorsítunk. CSP feladatoknál változók, domainek és megszorítások alapján keresünk konzisztens teljes értékadást, tipikus módszer a backtracking forward checkinggel és heurisztikákkal. A fő üzenet, hogy a jó reprezentáció és a jó heurisztika drasztikusan csökkenti a keresési költséget.

## Kulcsfogalmak
- [[állapottér]]
- [[BFS]]
- [[DFS]]
- [[IDDFS]]
- [[heurisztika]]
- [[A*]]
- [[Greedy best-first]]
- [[zéró összegű játék]]
- [[Minimax]]
- [[alfa-béta metszés]]
- [[CSP]]
- [[domain]]
- [[backtracking]]
- [[forward checking]]
- [[MRV]]

## Tipikus vizsgakérdések
1. **Mit tartalmaz egy keresési feladatreprezentáció?**  
   Állapottér, kezdőállapot, célállapot, operátorok, esetleg költségfüggvény.

2. **Mi a fő különbség BFS és DFS között?**  
   BFS réteges és egységköltségnél optimális, DFS memóriaigénye kisebb, de nem optimális.

3. **Mi a heurisztika szerepe?**  
   Becsli a célig vezető költséget és irányítja a keresést.

4. **Mikor optimális az A*?**  
   Ha a heurisztika megengedett (nem becsül túl).

5. **Mit csinál a minimax?**  
   MAX nyereségét maximalizálja MIN optimális ellenjátékát feltételezve.

6. **Miért hasznos az alfa-béta metszés?**  
   Ugyanazt a minimax eredményt adja, kevesebb csúcs vizsgálatával.

7. **Mi a CSP lényege?**  
   Változók értékadása úgy, hogy minden megszorítás teljesüljön.

## Minimum, amit tudni kell
- Keresési feladat alapkomponensei (állapot, operátor, cél).  
- BFS, DFS és IDDFS rövid összehasonlítása.  
- Heurisztika fogalma és A* alapképlete.  
- Minimax alapötlete játékfában.  
- Alfa-béta metszés célja.  
- CSP elemei: változó, domain, megszorítás.  
- Backtracking és forward checking szerepe.  
- Optimalitás és gyorsaság közti kompromisszum az MI keresésben.
