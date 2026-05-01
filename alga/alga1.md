# Algoritmusok és adatszerkezetek I. – 1. tétel
## Részproblémára bontó algoritmusok, rendezések, gráfalgoritmusok

---

## 1. Részproblémára bontó algoritmusok

### 1.1 Mohó algoritmusok (Greedy)
**Rövid definíció:**  
A **[[mohó algoritmus]]** mindig az adott lépésben legjobbnak tűnő választást teszi.

**Működési elv:**  
- Lokális optimumot választunk minden lépésben.  
- Ez akkor ad globális optimumot, ha teljesül a **mohó választási tulajdonság** és az **optimális részstruktúra**.  
- Gyors és egyszerű, de nem minden problémára jó.

**Egyszerű példa:**  
**Intervallumütemezésnél** mindig azt az intervallumot vesszük fel, ami leghamarabb befejeződik. Ezzel maximális számú, nem átfedő intervallum választható.

**Vizsgán fontos kulcsszavak:**  
**[[mohó algoritmus]]**, **lokális optimum**, **globális optimum**, **optimális részstruktúra**, **mohó választás**

**Mikor alkalmazható / mikor nem:**  
- Akkor jó, ha bizonyítható a mohó stratégia helyessége.  
- Nem jó például több olyan optimalizálási feladatnál, ahol egy korai döntés később rossz irányba visz.

---

### 1.2 Oszd meg és uralkodj (Divide and Conquer)
**Rövid definíció:**  
Az **[[oszd meg és uralkodj]]** módszer a problémát kisebb részekre bontja, azokat külön megoldja, majd az eredményeket összevonja.

**Működési elv:**  
- **Divide**: felosztás kisebb részproblémákra.  
- **Conquer**: részproblémák megoldása általában rekurzívan.  
- **Combine**: részmegoldások egyesítése.  
- Futási időt gyakran rekurziós egyenlettel írjuk fel, és becsüljük a **[[Mester-tétel]]** segítségével.

**Egyszerű példa:**  
**[[merge sort]]**: a tömböt felezzük, rendezzük a feleket, majd lineáris időben összefésüljük.

**Vizsgán fontos kulcsszavak:**  
**[[oszd meg és uralkodj]]**, **rekurzió**, **rekurziós egyenlet**, **[[Mester-tétel]]**, **combine lépés**

**Előnyök, hátrányok:**  
- Előny: jól skálázható, tiszta szerkezet.  
- Hátrány: rekurziós többletköltség, néha extra memóriaigény.

---

### 1.3 Dinamikus programozás (DP)
**Rövid definíció:**  
A **[[dinamikus programozás]]** ugyanazokat a részproblémákat nem számolja újra, hanem eltárolja az eredményeket.

**Működési elv:**  
- Kell az **átfedő részprobléma** és az **optimális részstruktúra**.  
- **Memoization**: felülről lefelé (rekurzív, cache-elt).  
- **Tabuláció**: alulról felfelé (iteratív táblázat).  
- A kulcs az állapottér jó definiálása.

**Egyszerű példa:**  
Fibonacci számoknál naiv rekurzió exponenciális, DP-vel lineáris időre csökkenthető.

**Vizsgán fontos kulcsszavak:**  
**[[dinamikus programozás]]**, **átfedő részproblémák**, **memoization**, **tabuláció**, **állapottér**

**Idő- és tárigény:**  
Gyakran időben nagy javulást ad, cserébe több memória kell a tároláshoz.

---

## 2. Rendező algoritmusok

### 2.1 Alapfogalmak
**Rövid definíció:**  
A rendezés célja, hogy az elemeket adott sorrendbe állítsuk (pl. növekvő kulcs szerint).

**Működési elv:**  
- **[[stabil rendezés]]**: azonos kulcsú elemek relatív sorrendje megmarad.  
- **[[in-place]]**: kis extra memóriával dolgozik.  
- Összehasonlításos rendezéseknél az általános alsó korlát: **Ω(n log n)**.

**Egyszerű példa:**  
Ha hallgatók listáját jegy szerint rendezzük, stabil rendezésnél az azonos jegyűek eredeti sorrendje megmarad.

**Vizsgán fontos kulcsszavak:**  
**rendezés**, **[[stabil rendezés]]**, **[[in-place]]**, **összehasonlításos rendezés**, **Ω(n log n)**

---

### 2.2 Egyszerű rendezések
**Rövid definíció:**  
Az egyszerű rendezések könnyen implementálhatók, de nagy adathalmazra általában lassúak.

**Működési elv:**  
- **[[bubble sort]]**: szomszédos elemek cseréje, amíg rendezett nem lesz.  
- **[[selection sort]]**: mindig kiválasztja a minimumot, előre teszi.  
- **[[insertion sort]]**: az új elemet a már rendezett rész megfelelő helyére szúrja be.  
- Általában O(n²) átlagos/rossz eset.

**Egyszerű példa:**  
Kicsi vagy majdnem rendezett tömbnél az insertion sort gyakorlatban jól működhet.

**Vizsgán fontos kulcsszavak:**  
**[[bubble sort]]**, **[[selection sort]]**, **[[insertion sort]]**, **O(n²)**, **best/average/worst case**

---

### 2.3 Hatékony rendezések
**Rövid definíció:**  
Nagy bemenetre ezek a klasszikus, hatékony rendezőalgoritmusok.

**Működési elv:**  
- **[[merge sort]]**: oszd meg és uralkodj, stabil, O(n log n), de extra memória kell.  
- **[[quicksort]]**: pivot köré particionál, átlagban O(n log n), rossz esetben O(n²).  
- **[[heapsort]]**: kupacra épül, garantált O(n log n), in-place jellegű.

**Egyszerű példa:**  
Ha fontos a stabilitás, merge sort jó választás; ha kis memória és garantált felső korlát kell, heapsort előnyös lehet.

**Vizsgán fontos kulcsszavak:**  
**[[merge sort]]**, **[[quicksort]]**, **[[heapsort]]**, **pivot**, **O(n log n)**

---

### 2.4 Nem összehasonlításos rendezések
**Rövid definíció:**  
Ezek a rendezések nem közvetlen elempár-összehasonlításra épülnek.

**Működési elv:**  
- **[[counting sort]]**: kulcsok előfordulását számolja, kis kulcstartomány kell.  
- **[[radix sort]]**: számjegyenként rendez stabil részrendezéssel.  
- **[[bucket sort]]**: elemeket vödrökbe szór, majd külön rendez.  
- Bizonyos feltételek mellett lineáris közeli idő is elérhető.

**Egyszerű példa:**  
Vizsgapontok 0–100 tartományban: counting sort nagyon gyors lehet.

**Vizsgán fontos kulcsszavak:**  
**[[counting sort]]**, **[[radix sort]]**, **[[bucket sort]]**, **kulcstartomány**, **nem összehasonlításos**

---

## 3. Gráfalgoritmusok

### 3.1 Alapfogalmak
**Rövid definíció:**  
A **[[gráf]]** csúcsok és élek halmaza, kapcsolatok modellezésére használjuk.

**Működési elv:**  
- **[[csúcs]]**: objektum, **[[él]]**: kapcsolat két csúcs között.  
- Lehet **irányított** vagy **irányítatlan**, illetve **súlyozott**.  
- Reprezentáció: **[[szomszédsági lista]]** (ritka gráfhoz jó), **[[szomszédsági mátrix]]** (sűrű gráfhoz jó).

**Egyszerű példa:**  
Úthálózat: városok csúcsok, utak élek, távolság az élsúly.

**Vizsgán fontos kulcsszavak:**  
**[[gráf]]**, **[[csúcs]]**, **[[él]]**, **irányított gráf**, **[[szomszédsági lista]]**, **[[szomszédsági mátrix]]**

---

### 3.2 Bejárások

#### Szélességi keresés (BFS)
**Rövid definíció:**  
A **[[BFS]]** rétegesen járja be a gráfot egy kezdőcsúcsból.

**Működési elv:**  
- **[[sor]]** adatszerkezetet használ.  
- Előbb az 1 élre lévő szomszédokat nézi, majd a 2 élre lévőket, stb.  
- Egységsúlyú gráfban legrövidebb útra is alkalmas.

**Egyszerű példa:**  
Szociális hálóban a „hány lépésre van” kérdés BFS-sel számolható.

**Vizsgán fontos kulcsszavak:**  
**[[BFS]]**, **réteges bejárás**, **[[sor]]**, **legrövidebb út**, **O(V+E)**

#### Mélységi keresés (DFS)
**Rövid definíció:**  
A **[[DFS]]** egy ágon megy végig mélyre, majd visszalép.

**Működési elv:**  
- Rekurzióval vagy explicit **[[verem]]** használatával működik.  
- Bejárási fát épít.  
- Alkalmazások: komponenskeresés, ciklusdetektálás, topologikus rendezés alapja.

**Egyszerű példa:**  
Irányított gráfban cikluskeresésnél DFS-ben figyelhetjük a visszaéleket.

**Vizsgán fontos kulcsszavak:**  
**[[DFS]]**, **rekurzió**, **[[verem]]**, **cikluskeresés**, **O(V+E)**

---

### 3.3 Minimális feszítőfa (MST)
**Rövid definíció:**  
Az **[[MST]]** egy olyan feszítőfa, ami minden csúcsot elér, és az összsúlya minimális.

**Működési elv:**  
- **[[Kruskal]]**: éleket súly szerint rendezi, és a legkisebb nem ciklust okozó éleket választja (**[[Union-Find]]** segít).  
- **[[Prim]]**: egy kezdőcsúcsból növeli a fát, mindig a legkisebb kifelé menő élt választja (**[[prioritási sor]]**).  
- Mindkettő mohó stratégia.

**Egyszerű példa:**  
Hálózatépítésnél (kábelezés) minimális összköltségű kapcsolatrendszert ad.

**Vizsgán fontos kulcsszavak:**  
**[[MST]]**, **[[Kruskal]]**, **[[Prim]]**, **[[Union-Find]]**, **mohó stratégia**

---

### 3.4 Legrövidebb utak
**Rövid definíció:**  
A feladat egy vagy több forrásból minimális útvonalhossz meghatározása.

**Működési elv:**  
- Algoritmusválasztás az élsúlyok tulajdonságától függ (van-e negatív él, egy forrás vagy minden csúcspár).  

**Egyszerű példa:**  
GPS jellegű útvonaltervezésnél forráscsúcsból a célcsúcsba vezető legkisebb költségű út kell.

**Vizsgán fontos kulcsszavak:**  
**legrövidebb út**, **súlyozott gráf**, **egyforrású**, **minden csúcspár**

#### Dijkstra algoritmus
**Rövid definíció:**  
A **[[Dijkstra]]** algoritmus egy forrásból számol legrövidebb utakat **nemnegatív** súlyok mellett.

**Működési elv:**  
- Mindig a jelenleg legkisebb távolságú feldolgozatlan csúcsot választja.  
- **[[prioritási sor]]**-ral hatékony.  
- Relaxálja a kimenő éleket.

**Egyszerű példa:**  
Ha minden úthossz pozitív, Dijkstra gyors és megbízható választás.

**Vizsgán fontos kulcsszavak:**  
**[[Dijkstra]]**, **nemnegatív súly**, **relaxáció**, **[[prioritási sor]]**

#### Bellman-Ford algoritmus
**Rövid definíció:**  
A **[[Bellman-Ford]]** kezeli a negatív éleket is, és jelzi a negatív kört.

**Működési elv:**  
- Az összes élt ismételten relaxálja (|V|-1 körben).  
- Egy további körben ellenőrzi, maradt-e javítható távolság -> negatív ciklus.

**Egyszerű példa:**  
Pénzügyi arbitrage-jellegű modellekben negatív költségű élek is lehetnek, itt Bellman-Ford kell.

**Vizsgán fontos kulcsszavak:**  
**[[Bellman-Ford]]**, **negatív él**, **negatív ciklus**, **relaxáció**

#### Floyd–Warshall (opcionális)
**Rövid definíció:**  
A **[[Floyd–Warshall]]** minden csúcspár legrövidebb útját számolja.

**Működési elv:**  
- Dinamikus programozás: fokozatosan engedjük meg a köztes csúcsokat.  
- Tipikusan O(V³), ezért kisebb-közepes gráfokra alkalmas.

**Egyszerű példa:**  
Ha minden várospár távolsága kell egyszerre, ez kényelmes módszer.

**Vizsgán fontos kulcsszavak:**  
**[[Floyd–Warshall]]**, **minden csúcspár**, **[[dinamikus programozás]]**, **O(V³)**

---

## + Vizsgán érdemes még megemlíteni
- Időkomplexitás jelölések: **O**, **Ω**, **Θ**.  
- Algoritmusválasztás szempontjai: bemenetméret, adateloszlás, stabilitásigény, memória.  
- Elméleti és gyakorlati teljesítmény eltérhet (cache, konstans tényezők).  
- Gyakorlati alkalmazások: útvonaltervezés, ütemezés, hálózattervezés, adatfeldolgozás.

---

## Rövid szóbeli összefoglaló
A részproblémára bontó módszerek közül a mohó algoritmus mindig lokálisan legjobbat választ, de csak bizonyos feltételek mellett optimális. Az oszd meg és uralkodj felosztja a problémát, rekurzívan megoldja, majd összevonja az eredményeket, tipikus példa a merge sort. A dinamikus programozás átfedő részproblémáknál hatékony, mert eltárolja a részeredményeket. Rendezéseknél fontos fogalom a stabilitás és az in-place működés; nagy bemenetre jellemzően O(n log n) körüli algoritmusokat használunk. Gráfoknál alap a BFS és DFS, minimális feszítőfához Kruskal és Prim, legrövidebb útra Dijkstra vagy negatív élek esetén Bellman-Ford. A lényeg, hogy mindig a feladat tulajdonságai alapján választunk algoritmust.

## Kulcsfogalmak
- [[mohó algoritmus]]
- [[oszd meg és uralkodj]]
- [[dinamikus programozás]]
- [[memoization]]
- [[tabuláció]]
- [[merge sort]]
- [[quicksort]]
- [[stabil rendezés]]
- [[in-place]]
- [[gráf]]
- [[BFS]]
- [[DFS]]
- [[MST]]
- [[Dijkstra]]
- [[Bellman-Ford]]

## Tipikus vizsgakérdések
1. **Mikor jó a mohó algoritmus?**  
   Akkor, ha bizonyítható a mohó választási tulajdonság és optimális részstruktúra.

2. **Mi a különbség memoization és tabuláció között?**  
   Memoization felülről lefelé rekurzív cache-elés, tabuláció alulról felfelé iteratív táblázat.

3. **Miért fontos az Ω(n log n) alsó korlát?**  
   Megmutatja, hogy összehasonlításos rendezéssel általánosan ennél gyorsabb nem lehet.

4. **Mikor használunk BFS-t és mikor DFS-t?**  
   BFS rövid útra egységsúlyú gráfban, DFS szerkezeti vizsgálatokra (pl. ciklus, komponensek).

5. **Mi a különbség Kruskal és Prim között?**  
   Kruskal élalapú válogatással épít, Prim csúcsból kiindulva növeszti a fát.

6. **Mikor nem használható Dijkstra?**  
   Negatív élsúly esetén nem helyes, ilyenkor Bellman-Ford kell.

7. **Mit tud a Floyd–Warshall?**  
   Minden csúcspárra ad legrövidebb utat DP-alapon, O(V³) időben.

## Minimum, amit tudni kell
- A **mohó**, **oszd meg és uralkodj**, **DP** közti alapelvi különbség.  
- Rendezéseknél a **stabilitás** és **in-place** jelentése.  
- Egyszerű rendezések tipikusan O(n²), hatékonyak jellemzően O(n log n).  
- BFS és DFS működése, adatszerkezete (sor/verem), O(V+E) idő.  
- MST fogalma, Kruskal és Prim lényegi ötlete.  
- Dijkstra csak nemnegatív súlyokra jó.  
- Bellman-Ford kezeli a negatív éleket és detektál negatív ciklust.  
- Algoritmusválasztás mindig feladat- és bemenetfüggő.
