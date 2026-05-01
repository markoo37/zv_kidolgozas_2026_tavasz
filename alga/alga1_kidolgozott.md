# Algoritmusok és adatszerkezetek I. – 1. tétel
## Részproblémára bontó algoritmusok, rendezések, gráfalgoritmusok
### Teljes kidolgozás – szóbeli záróvizsga szintű

---

## 1. Részproblémára bontó algoritmusok

### 1.1 Mohó algoritmusok (Greedy)

## Definíció

A **mohó algoritmus** olyan algoritmustervezési módszer, amelynek során minden egyes lépésben az adott pillanatban **lokálisan legjobbnak tűnő döntést** hozzuk meg, anélkül hogy visszatérnénk korábbi döntésekre, vagy előrenéznénk a jövőbe. Más szóval: a mohó algoritmus mindig az aktuális lehetséges lépések közül a „legvonzóbbal" él.

## Hogyan működik

A mohó stratégia kulcsgondolata az, hogy **egyszer döntünk, és nem lépünk vissza**. Ez rendkívül gyors megközelítés, de korántsem minden problémán ad helyes megoldást.

Ahhoz, hogy a mohó stratégia **biztosan helyes** globálisan optimális megoldást adjon, két feltételnek kell egyidejűleg teljesülnie:

1. **Mohó választási tulajdonság (Greedy choice property):** Létezik olyan globálisan optimális megoldás, amely tartalmazza az aktuálisan mohón meghozott döntést. Más szóval: a mohó döntés soha nem zárja ki az optimumot – mindig „megúszhatjuk" azzal, hogy az adott lépésben a lokálisan legjobbat választjuk.

2. **Optimális részstruktúra (Optimal substructure):** Ha az eredeti probléma optimális megoldásából elhagyjuk a mohó döntést, a megmaradó részprobléma optimális megoldása szintén optimális. Vagyis az optimum „felépíthető" kisebb optimumokból.

Ha valamelyik feltétel nem teljesül, a mohó stratégia **helytelen** eredményt adhat.

## Lépések (általánosan)

1. A probléma elemeit valamilyen szempont szerint sorba rendezzük (pl. legkisebb, legkorábban befejeződő, legnagyobb ár/súly arány, stb.).
2. Az elemeket sorban vesszük, és minden elemet felveszünk, ha az **megfelel az aktuális feltételnek**.
3. Ha egy elem nem felel meg a feltételnek, kihagyjuk – **visszalépés nincs**.
4. Addig folytatjuk, amíg van elem, vagy a megoldás kész.

## Példa – Intervallumütemezés

Adott n előadás, mindegyiknek van egy kezdő- és egy befejezési időpontja. Cél: minél több előadást hallgassunk meg anélkül, hogy átfednének egymással.

**Mohó stratégia:** Minden lépésben azt az előadást választjuk, amely **leghamarabb fejeződik be**, és nem ütközik az eddig kiválasztott előadásokkal.

**Miért helyes?** Mert a korán befejeződő előadás a lehető legtöbb helyet hagyja a következő előadásoknak. Bizonyítható, hogy ez az optimális számú előadást adja.

**Lépések:**
1. Rendezzük az előadásokat befejezési idő szerint.
2. Vegyük az első előadást (legkorábban végzőt).
3. Minden következő előadást vegyük fel, ha kezdési ideje ≥ az utoljára felvett befejezési ideje.

## Komplexitás

| | |
|---|---|
| Intervallumütemezésnél | O(n log n) – a rendezés dominál |
| Mohó lépések | Általában O(n) – lineáris végigmenet |
| Tár | Tipikusan O(1)–O(n) |

## Mikor érdemes használni

- Ha **bizonyíthatóan** teljesül a mohó választási tulajdonság és az optimális részstruktúra.
- Amikor egyszerű, gyors megoldás kell, és a visszalépés szükségtelen.
- Klasszikus alkalmazások: intervallumütemezés, törtszámos hátizsák, Huffman-kódolás, MST (Kruskal, Prim), Dijkstra.

## Korlátok / Mikor NEM

- Ha a korai döntések rossz irányba vihetnek, és visszalépésre lenne szükség.
- **Klasszikus ellenpélda:** Az egész-hátizsák probléma (0/1 Knapsack) – ott a mohó stratégia nem ad optimumot, **dinamikus programozás** kell.
- Összefoglalva: mohó akkor jó, ha a helyes választás bizonyítható; egyébként DP vagy backtracking kell.

⚠️ **Vizsgán kiemelendő:** Mindig indokold meg, miért helyes a mohó stratégia! Pusztán azt mondani, hogy „mohóval megoldom", nem elégséges. Hivatkozz a mohó választási tulajdonságra és az optimális részstruktúrára.

## Tipikus vizsgakérdések

- Mik a mohó algoritmus alkalmazhatóságának szükséges feltételei?
- Mi a különbség a mohó és a dinamikus programozás megközelítés között?
- Adj példát, ahol a mohó helyes, és ahol nem helyes!
- Miért helyes a mohó stratégia az intervallumütemezésnél?

---

### 1.2 Oszd meg és uralkodj (Divide and Conquer)

## Definíció

Az **oszd meg és uralkodj** paradigma olyan algoritmustervezési módszer, amelynek során a problémát **kisebb, hasonló jellegű részproblémákra osztjuk**, ezeket rekurzívan megoldjuk, majd a részmegoldásokat **összevonjuk** a teljes megoldás előállításához.

## Hogyan működik

A módszer három jól elkülönülő fázisból áll:

1. **Divide (Felosztás):** A problémát két vagy több kisebb részproblémára osztjuk. A leggyakoribb a felezés.
2. **Conquer (Uralom):** A kisebb részproblémákat rekurzívan oldjuk meg. Ha a részprobléma elég kicsi (ún. **alapeset**), közvetlenül megoldjuk rekurzió nélkül.
3. **Combine (Összevonás):** A részproblémák megoldásait összevonjuk a teljes megoldás előállításához.

## A Mester-tétel (Master Theorem)

A Divide and Conquer algoritmusok futási ideje általában egy **rekurzív egyenlettel** írható le:

$$T(n) = a \cdot T(n/b) + f(n)$$

ahol:
- **a** = a részproblémák száma,
- **b** = a méretcsökkentés tényezője (minden részprobléma n/b méretű),
- **f(n)** = a felosztás és összevonás lépések összesített költsége.

A **[[Mester-tétel]]** három esetben ad zárt formát:

| Eset | Feltétel | Eredmény |
|------|---------|---------|
| 1. eset | f(n) = O(n^(log_b(a) − ε)) | T(n) = Θ(n^log_b(a)) |
| 2. eset | f(n) = Θ(n^log_b(a)) | T(n) = Θ(n^log_b(a) · log n) |
| 3. eset | f(n) = Ω(n^(log_b(a) + ε)) | T(n) = Θ(f(n)) |

**Merge sort alkalmazása:** T(n) = 2·T(n/2) + Θ(n). Itt a=2, b=2, f(n)=Θ(n), log₂(2)=1. Mivel f(n)=Θ(n^1), a 2. eset: **T(n) = Θ(n log n)**.

## Lépések – Merge Sort példán

1. Ha a tömb mérete ≤ 1: kész (alap eset, már rendezett).
2. Felezd a tömböt: bal[0..n/2−1] és jobb[n/2..n−1].
3. Rekurzívan rendezd a bal félrészt.
4. Rekurzívan rendezd a jobb félrészt.
5. **Összefésülés:** Két mutató az i és j, mindkettő a megfelelő rész elejére mutat.
   - Mindkét mutató érvényes: a kisebb elemet másold az eredménytömbbe, lépj azzal a mutatóval.
   - Ha valamelyik rész kiürül: a másik részt másold hozzá.

## Komplexitás

| Algoritmus | Legjobb | Átlagos | Legrosszabb | Tár |
|---|---|---|---|---|
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Bináris keresés | O(1) | O(log n) | O(log n) | O(1) |

## Mikor érdemes használni

- Rendezés nagy adathalmazon (Merge Sort).
- Keresési feladatok rendezett tömbben (bináris keresés).
- Ha a részproblémák **diszjunktak** (nem fedik át egymást) – ez különbözteti meg a DP-től.
- Számpárok közelség számítása, mátrixszorzás (Strassen), stb.

## Korlátok / Mikor NEM

- Ha a rekurzió mélysége nagy és veremtúlcsordulás fenyeget.
- Ha az összevonás drága és nem vezet hatékonyabb megoldáshoz.
- Ha a részproblémák átfednek → ott **dinamikus programozás** hatékonyabb.

⚠️ **Vizsgán kiemelendő:** Ismerd a Mester-tétel három esetét és tudj konkrét példát mondani mindegyikre! Tudj merge sort-ot rekurzív egyenlettel levezetni.

## Tipikus vizsgakérdések

- Mi a Divide and Conquer három fázisa?
- Hogyan számolod ki a merge sort futási idejét a Mester-tétellel?
- Mi a különbség a D&C és a dinamikus programozás között?

---

### 1.3 Dinamikus programozás (DP)

## Definíció

A **[[dinamikus programozás]]** olyan algoritmustervezési technika, amellyel az **átfedő részproblémákat** hatékonyan oldjuk meg azáltal, hogy a már kiszámított részeredményeket **eltároljuk** (memoizáljuk), és nem számítjuk ki újra őket. Ez drámai futási idő-javulást eredményezhet az egyszerű rekurzióhoz képest.

## Hogyan működik

DP alkalmazásához két kulcstulajdonságnak kell teljesülnie:

1. **Optimális részstruktúra:** Az optimális megoldás felépíthető részproblémák optimális megoldásaiból. (Ez megegyezik a mohó és D&C feltételével.)

2. **Átfedő részproblémák:** Ugyanazok a részproblémák ismételten fordulnak elő a rekurzió során. Ez az, ami a DP-t megkülönbözteti a D&C-től: D&C-nél a részproblémák diszjunktak, DP-nél átfednek.

**Intuitív magyarázat:** Gondolj a Fibonacci sorozatra. A fib(5) kiszámításához szükség van fib(4)-re és fib(3)-ra. A fib(4) kiszámításához szükség van fib(3)-ra és fib(2)-re. A fib(3)-at kétszer számítjuk ki! Ha eltároljuk az eredményt, ezt elkerülhetjük.

## A két megközelítés

### Memoization (felülről lefelé, top-down)

Rekurzívan számítunk, de az eredményeket egy **cache-táblában** tároljuk. Ha egy részproblémát már megoldottunk, a cache-ből olvassuk ki az eredményt rekurzív újraszámítás helyett.

- Természetes, intuitív – közel áll a rekurzív gondolkodáshoz.
- Csak azokat a részproblémákat számítja ki, amelyekre ténylegesen szükség van.

```
fib(n):
  if n in cache: return cache[n]
  if n <= 1: return n
  cache[n] = fib(n-1) + fib(n-2)
  return cache[n]
```

### Tabuláció (alulról felfelé, bottom-up)

Iteratív megközelítés: először a **legkisebb részproblémákat** oldjuk meg, majd ezekre építve haladunk a nagyobbak felé, egy táblázatot töltünk fel.

- Nincs rekurzív hívás → nincs stack overhead.
- Általában gyorsabb a konstans tényező miatt.

```
fib(n):
  dp[0] = 0, dp[1] = 1
  for i = 2 to n:
    dp[i] = dp[i-1] + dp[i-2]
  return dp[n]
```

## Az állapottér definiálása – a DP lelke

A DP **legkritikusabb lépése** az **állapot (state) pontos meghatározása**: mit jelent `dp[i]`? Mit jelent `dp[i][j]`? Ezt kell elsőként tisztázni. Ezután az **átmeneti egyenlet (recurrence relation)** és az **alapeset** leírása következik.

## Lépések (általánosan)

1. **Definiáld az állapotot:** Mit jelent `dp[i]` (vagy `dp[i][j]` stb.)?
2. **Írd fel az átmeneti egyenletet:** Hogyan függ `dp[i]` a kisebb dp-értékektől?
3. **Határozd meg az alapesetet:** Mi `dp[0]`, `dp[1]` értéke?
4. **Számítsd ki a táblát** (tabuláció) vagy rekurzívan cache-szel (memoization).
5. **Olvasd le a végeredményt** a táblából.

## Példa – Leghosszabb közös részsorozat (LCS)

Adott két X és Y sorozat. `dp[i][j]` = az `X[1..i]` és `Y[1..j]` sorozatok LCS hossza.

**Átmenet:**
- Ha `X[i] = Y[j]`: `dp[i][j] = dp[i−1][j−1] + 1`
- Egyébként: `dp[i][j] = max(dp[i−1][j], dp[i][j−1])`

**Alap eset:** `dp[0][j] = dp[i][0] = 0.`

## Komplexitás

| Probléma | Idő | Tár |
|---|---|---|
| Fibonacci (DP) | O(n) | O(n) vagy O(1) |
| LCS | O(n·m) | O(n·m) |
| Mátrixlánc-szorzás | O(n³) | O(n²) |
| Általánosan | (állapotok száma) × (átmenet ideje) | (állapotok száma) |

## Mikor érdemes használni

- Ha az egyszerű rekurzió exponenciális idejű, de átfedő részproblémák vannak.
- Optimalizálási feladatoknál: legrövidebb/leghosszabb út, maximális összeg, stb.
- Kombinatorikus megszámlálási feladatoknál.

## Korlátok / Mikor NEM

- Ha nincsenek átfedő részproblémák → D&C hatékonyabb és egyszerűbb.
- Ha az állapottér hatalmas és nem szükséges minden állapot kiszámítása.
- Ha az állapot nehezen definiálható.

⚠️ **Vizsgán kiemelendő:** A legtöbb DP feladatnál az állapot definiálása a kulcs. Mindig mondd el, mit jelent dp[i]! A különbség memoization és tabuláció között szintén gyakori vizsgakérdés.

## Tipikus vizsgakérdések

- Mi a különbség a memoization és a tabuláció között?
- Hogyan különböztethető meg a DP és az oszd meg és uralkodj?
- Mik a DP alkalmazásának szükséges feltételei?
- Miért O(2^n) a Fibonacci naiv rekurzióval, és hogyan javítja ezt a DP?

---

## 2. Rendező algoritmusok

### 2.1 Alapfogalmak

## Definíció

A **rendezés** feladata: adott n elemű tömb, állítsuk az elemeket valamilyen összehasonlítható kulcs szerint növekvő (vagy csökkenő) sorrendbe. A rendezés az egyik legalapvetőbb algoritmikus feladat, és számos más algoritmus és adatszerkezet alapját képezi.

## Kulcsfogalmak

**[[Stabil rendezés]]:** Olyan rendezőalgoritmus, amelynél az azonos kulcsú elemek relatív sorrendje a rendezés után is ugyanolyan marad, mint a bemenetben volt. Ez akkor fontos, ha több szempont szerint rendezünk egymás után: az előző rendezés eredménye "megmarad" az egyforma kulcsúaknál. Stabil: merge sort, insertion sort, counting sort, radix sort (ha stabil alaprendezést használ). Nem stabil: quicksort, heapsort, selection sort.

**[[In-place]] rendezés:** Az algoritmus az eredeti tömbön belül, minimális extra memóriával (O(1) vagy O(log n) stack) dolgozik. In-place: insertion sort, selection sort, bubble sort, quicksort, heapsort. Nem in-place: merge sort (O(n) extra tömb).

**Az összehasonlításos rendezés alsó korlátja:**

Megmutatható döntési fa modellel, hogy bármely összehasonlításos rendező algoritmus **legrosszabb esetben legalább Ω(n log n) összehasonlítást** végez.

**Intuitív indoklás:** n elem rendezésénél n! lehetséges permutáció lehetséges. A döntési fa (ahol minden belső csomópont egy összehasonlítás) legalább n! levelet kell tartalmazzon. Egy bináris fa legkevesebb levele 2^h, tehát 2^h ≥ n!, amiből h ≥ log(n!) = Ω(n log n) (Stirling-közelítéssel).

⚠️ **Vizsgán kiemelendő:** Ez az Ω(n log n) alsó korlát CSAK összehasonlításos rendezésekre érvényes. A nem összehasonlításos rendezések (counting sort, radix sort, bucket sort) megkerülhetik ezt, de csak speciális feltételek mellett.

---

### 2.2 Egyszerű rendezések

#### Buborékrendezés (Bubble Sort)

## Definíció

A **[[bubble sort]]** szomszédos elemeket hasonlít össze és cserél fel, amíg a tömb rendezett nem lesz. A nagyobb elemek fokozatosan „felbuborékoznak" a tömb végére.

## Lépések

1. Jelöld meg a teljes tömböt rendezetlennek.
2. Külső ciklus: i = n−1-től 1-ig (jelöli a rendezetlen rész határát).
3. Belső ciklus: j = 0-tól i−1-ig.
   - Ha a[j] > a[j+1]: cseréld fel a[j] és a[j+1]-t.
4. Egy menet végén a legnagyobb elem a helyére került.
5. **Optimalizálás:** Ha egy menetben egyetlen csere sem történt → a tömb rendezett, korai kilépés.

## Komplexitás

| Eset | Idő |
|---|---|
| Legjobb (már rendezett + korai kilépés) | O(n) |
| Átlagos | O(n²) |
| Legrosszabb (fordítottan rendezett) | O(n²) |
| Tár | O(1) – in-place |
| Stabil | Igen |

## Mikor érdemes / NEM érdemes

Csak nagyon kis tömbökre vagy oktatási célra érdemes. Nagy adathalmazra az O(n²) teljesen alkalmatlan.

---

#### Kiválasztásos rendezés (Selection Sort)

## Definíció

A **[[selection sort]]** minden lépésben megkeresi a rendezetlen rész minimumát, és azt felcseréli a rendezetlen rész első elemével.

## Lépések

1. i = 0-tól n−2-ig:
   a. Keresd meg a minimum elemet az a[i..n−1] tartományban.
   b. Cseréld fel a[i]-t és a[min_index]-et.
2. Kész – a tömb rendezett.

## Komplexitás

| Eset | Idő |
|---|---|
| Minden esetben | O(n²) – mindig megkeresi a minimumot |
| Tár | O(1) – in-place |
| Stabil | **Nem** – a csere felboríthatja az egyforma kulcsúak sorrendjét |

## Mikor érdemes / NEM érdemes

A selection sort egyszerű, de nem stabil és nem hatékony. Előnye: kevés cserét végez (O(n) csere összesen) – ha a csere drága, ez számíthat.

---

#### Beszúrásos rendezés (Insertion Sort)

## Definíció

A **[[insertion sort]]** a tömböt egy rendezett és egy rendezetlen részre osztja. Minden lépésben a rendezetlen rész első elemét a rendezett részbe szúrja be a megfelelő helyre, balra tolva az összes nálánál nagyobb elemet.

## Lépések

1. i = 1-től n−1-ig (az első elem önmagában rendezett).
2. Vedd ki a kulcsot: key = a[i].
3. j = i−1. Amíg j ≥ 0 és a[j] > key:
   - a[j+1] = a[j] (elem eltolása jobbra).
   - j--.
4. a[j+1] = key (szúrd be a kulcsot).

## Komplexitás

| Eset | Idő |
|---|---|
| Legjobb (már rendezett) | O(n) |
| Átlagos | O(n²) |
| Legrosszabb (fordítottan rendezett) | O(n²) |
| Tár | O(1) – in-place |
| Stabil | Igen |

## Mikor érdemes használni

- Kis n-re (n ≤ 20–30) kiváló, mert a kis konstans tényező miatt gyors.
- Majdnem rendezett tömbön O(n) közelítő teljesítményt ad.
- Sok hibrid rendezési algoritmus (pl. **Timsort** Python és Java alaprendezése) kis részeken insertion sort-ot használ.

⚠️ **Vizsgán kiemelendő:** Az insertion sort az egyetlen egyszerű rendezés, amely majdnem rendezett bemeneten valóban O(n) közelítő teljesítményt nyújt!

---

### 2.3 Hatékony rendezések

#### Összefésüléses rendezés (Merge Sort)

## Definíció

A **[[merge sort]]** az oszd meg és uralkodj paradigmán alapul: a tömböt rekurzívan felezi, mindkét felét rendezi, majd a két rendezett felet lineáris időben összefésüli.

## Lépések

1. Ha a tömb mérete ≤ 1: visszatér (alap eset).
2. Felezd a tömböt: bal[0..n/2−1] és jobb[n/2..n−1].
3. Rekurzívan rendezd a bal felét: mergeSort(bal).
4. Rekurzívan rendezd a jobb felét: mergeSort(jobb).
5. **Összefésülés:**
   - i = 0 (bal mutató), j = 0 (jobb mutató), k = 0 (eredménymutató).
   - Amíg mindkét rész nem üres: a kisebb elemet másold az eredménybe, lépj azzal.
   - A maradékot másold be.

## Pszedokód

```
mergeSort(A, l, r):
  if l >= r: return
  m = (l + r) / 2
  mergeSort(A, l, m)
  mergeSort(A, m+1, r)
  merge(A, l, m, r)      // két rendezett fél összefésülése

merge(A, l, m, r):
  Másold bal = A[l..m], jobb = A[m+1..r]
  i = 0, j = 0, k = l
  while i < len(bal) and j < len(jobb):
    if bal[i] <= jobb[j]: A[k++] = bal[i++]
    else: A[k++] = jobb[j++]
  A maradék elemeket másold be
```

## Komplexitás

| Eset | Idő | Tár |
|---|---|---|
| Minden esetben | **O(n log n)** | O(n) extra |
| Stabil | **Igen** | |

## Mikor érdemes használni

- Ha **garantált** O(n log n) kell minden esetben.
- Ha **stabilitás** kell.
- Külső rendezésnél (ha az adat nem fér a memóriába, lemezre is alkalmazható).

## Korlátok

- Extra O(n) memóriát igényel az összefésülés miatt → nem in-place.

⚠️ **Vizsgán kiemelendő:** A merge sort az egyetlen hatékony rendezés, amely garantáltan O(n log n) MINDEN esetben, ÉS stabil is!

---

#### Gyors rendezés (Quicksort)

## Definíció

A **[[quicksort]]** szintén oszd meg és uralkodj alapú: egy kiválasztott **pivot** elem köré particionálja a tömböt (kisebb elemek bal oldalra, nagyobbak jobb oldalra), majd rekurzívan rendezi a két részt.

## Lépések

1. Ha a tömb mérete ≤ 1: visszatér.
2. Válassz **pivotot** (pl. utolsó elem, első elem, véletlenszerű, medián-of-3).
3. **Particionálás:** Rendezd át az elemeket úgy, hogy:
   - Bal oldalon legyenek a pivot-nál kisebb (vagy egyenlő) elemek.
   - Jobb oldalon a pivot-nál nagyobb elemek.
   - A pivot a végső helyére kerül.
4. Rekurzívan rendezd a bal részt.
5. Rekurzívan rendezd a jobb részt.

## Lomuto particionálás (lépésről lépésre)

```
partition(A, l, r):
  pivot = A[r]          // utolsó elem a pivot
  i = l - 1
  for j = l to r-1:
    if A[j] <= pivot:
      i++
      swap(A[i], A[j])
  swap(A[i+1], A[r])   // pivot a helyére
  return i+1            // pivot indexe
```

## Komplexitás

| Eset | Idő | Tár |
|---|---|---|
| Legjobb | O(n log n) | O(log n) stack |
| Átlagos | O(n log n) | O(log n) stack |
| Legrosszabb | **O(n²)** | O(n) stack |
| Stabil | **Nem** | |

**Legrosszabb eset:** Ha a pivot mindig a legkisebb vagy legnagyobb elem (pl. rendezett tömb + első elem pivot). Megoldás: **véletlenszerű pivot-választás** vagy **medián-of-3**.

## Mikor érdemes használni

- Átlagosan gyorsabb a merge sort-nál a jobb cache-viselkedés miatt (in-place, folytonos memóriaelérés).
- Ha extra memória nem áll rendelkezésre (in-place).
- Véletlenszerű pivot-választással a legrosszabb eset elkerülhető.

## Korlátok

- Nem stabil.
- Legrosszabb eset O(n²) rossz pivot-választásnál.

⚠️ **Vizsgán kiemelendő:** Quicksort legrosszabb esete O(n²), de jó pivot-választással (pl. random pivot) a várható futási idő O(n log n). A legrosszabb eset elkerülése a kulcskérdés!

---

#### Kupacrendezés (Heapsort)

## Definíció

A **[[heapsort]]** egy maximális **kupacot** (max-heap) épít a tömbből, majd ismételten kiveszi a maximumot és a tömb végére rakja, csökkentve a kupac méretét.

## Kupac (heap) alapjai

A **bináris kupac** egy tömbbel reprezentált közel teljes bináris fa, ahol minden csúcs kulcsa ≥ gyerekeié (max-heap esetén). Az i-edik csomópont (0-indexelésnél):
- Bal gyerek: 2i+1
- Jobb gyerek: 2i+2
- Szülő: (i−1)/2

## Lépések

1. **Build-max-heap:** Építs max-kupacot az egész tömbből.
   - Az n/2−1-es indextől visszafelé hajtsd végre a max-heapify-t minden csomóponton.
   - Max-heapify(i): ha az i csomópont kisebb valamelyik gyerekénél, cseréld fel a nagyobbal, és rekurzívan folytasd lefelé.
   - Build-max-heap: **O(n)** összességében (nem O(n log n)!).
2. i = n−1-től 1-ig:
   a. Cseréld fel A[0]-t (a kupac maximuma) és A[i]-t.
   b. Csökkentsd a kupac méretét eggyel (az i. elem már a helyén).
   c. Max-heapify(0) – buborékolj le a gyökérből.

## Komplexitás

| Eset | Idő | Tár |
|---|---|---|
| Minden esetben | **O(n log n)** | O(1) – in-place |
| Stabil | **Nem** | |

## Mikor érdemes használni

- Ha garantált O(n log n) kell **ÉS** in-place működés is szükséges.
- Ahol sem extra memória, sem stabilitás nem kell.

## Korlátok

- A cache-viselkedése rosszabb, mint a quicksort-é → a gyakorlatban általában lassabb.
- Nem stabil.

⚠️ **Vizsgán kiemelendő:** A heapsort az egyetlen hatékony rendezés, amely egyszerre in-place ÉS garantáltan O(n log n). Sem stabilitása nincs, sem cache-barát, de elméletileg kompromisszummentes.

---

### 2.4 Nem összehasonlításos rendezések

#### Számlálórendezés (Counting Sort)

## Definíció

A **[[counting sort]]** nem hasonlítja össze az elemeket: az elemek előfordulásait egy segédtáblában **megszámolja**, majd ebből rekonstruálja a rendezett sorrendet. Csak egész (vagy korlátozott kulcstartományú) elemekre alkalmazható.

## Lépések

1. Legyen C[0..k] egy nullákkal feltöltött tömb (k = max kulcs értéke).
2. **Számlálás:** Minden A[i] elemre: C[A[i]]++.
3. **Kumulatív összeg:** C[j] += C[j−1] minden j-re 1-től k-ig. (Most C[j] megmondja, hány elem ≤ j.)
4. **Eredménytömb feltöltése (jobbról balra, stabilitás miatt):**
   - i = n−1-től 0-ig: B[C[A[i]]−1] = A[i]; C[A[i]]--.
5. B tartalmazza a rendezett tömböt.

## Komplexitás

| | |
|---|---|
| Idő | **O(n + k)** |
| Tár | O(n + k) |
| Stabil | Igen (ha jobbról balra töltjük) |

## Mikor érdemes használni

- Ha k = O(n) (a kulcstartomány arányos az elemszámmal).
- Vizsgapontok 0–100 között, korosztályok, DNS karakterek rendezése.

## Korlátok

- Ha k >> n: a C tömb hatalmas és jobbára üres → memória pazarlás.
- Csak egész kulcsokra alkalmazható közvetlenül.

---

#### Radix Sort

## Definíció

A **[[radix sort]]** számjegyenként rendez stabil segédrendezéssel (tipikusan counting sort-tal), a legkevésbé jelentős számjegytől a legjelentősebbig (LSD = Least Significant Digit).

## Lépések

1. Határozd meg a maximális elem számjegyeinek számát: d.
2. i = 1-től d-ig (legkevésbé jelentős számjegytől a legjelentősebbig):
   - Rendezd a tömböt az i-edik számjegy szerint **stabil rendezéssel** (pl. counting sort).
3. A tömb rendezett.

**Miért kell stabil az alaprendezés?** Mert ha a j-edik számjegy szerint rendezünk, az eddigi rendezési eredmény (i−1-es számjegyek) csak akkor marad érvényes, ha az egyforma j-edik számjegyű elemek sorrendje nem változik.

## Komplexitás

| | |
|---|---|
| Idő | **O(d · (n + k))** – ha d konstans és k=O(n): O(n) |
| Tár | O(n + k) |
| Stabil | Igen |

## Mikor érdemes használni

- Nagy n, de korlátozott számjegyű kulcsok esetén.
- DNS-szekvenciák, IP-cím rendezése, nagy egész számok rendezése.

---

#### Vödörrendezés (Bucket Sort)

## Definíció

A **[[bucket sort]]** az elemeket **egyenletesen osztja szét vödrökbe** (intervallumokba), mindegyik vödröt külön rendezi, majd összefűzi a vödröket.

## Lépések

1. Hozz létre n üres vödröt.
2. Minden A[i] elemre: tedd a megfelelő vödörbe (pl. ⌊n · A[i]⌋ sorszámú vödörbe, ha A[i] ∈ [0,1)).
3. Minden vödröt rendezd (pl. insertion sort).
4. Fűzd össze a vödrök tartalmát sorban.

## Komplexitás

| Eset | Idő |
|---|---|
| Átlagos (egyenletes eloszlás) | **O(n)** |
| Legrosszabb (minden elem egy vödörbe) | O(n²) |

## Mikor érdemes használni

- Ha az elemek egyenletesen oszlanak el egy ismert tartományban.
- Lebegőpontos számok [0,1) között.

⚠️ **Vizsgán kiemelendő:** A nem összehasonlításos rendezések mind megkerülik az Ω(n log n) korlátot, de CSAK speciális feltételek mellett. Counting sort: kis egész kulcstartomány. Radix sort: konstans számjegyek. Bucket sort: egyenletes eloszlás. Ha ezek nem teljesülnek, az összehasonlításos rendezések jobbak!

---

### Rendezések összefoglalása

| Algoritmus | Legjobb | Átlagos | Legrosszabb | Tár | Stabil | In-place |
|---|---|---|---|---|---|---|
| Bubble sort | O(n) | O(n²) | O(n²) | O(1) | Igen | Igen |
| Selection sort | O(n²) | O(n²) | O(n²) | O(1) | Nem | Igen |
| Insertion sort | **O(n)** | O(n²) | O(n²) | O(1) | Igen | Igen |
| Merge sort | O(n log n) | O(n log n) | **O(n log n)** | O(n) | **Igen** | Nem |
| Quicksort | O(n log n) | O(n log n) | O(n²) | O(log n) | Nem | **Igen** |
| Heapsort | O(n log n) | O(n log n) | **O(n log n)** | **O(1)** | Nem | **Igen** |
| Counting sort | – | **O(n+k)** | O(n+k) | O(n+k) | Igen | Nem |
| Radix sort | – | **O(d·(n+k))** | O(d·(n+k)) | O(n+k) | Igen | Nem |
| Bucket sort | – | **O(n)** | O(n²) | O(n) | Igen | Nem |

---

## 3. Gráfalgoritmusok

### 3.1 Alapfogalmak

## Definíció

A **[[gráf]]** G = (V, E) **csúcsok** (V – vertices) és **élek** (E – edges) halmazából áll. Az élek csúcspárokat kötnek össze, és kapcsolatokat, útvonalakat, függőségeket modellezhetnek.

## Alapfogalmak

- **[[Csúcs]] (vertex):** A gráf alapeleme, egy „objektum" vagy „állapot".
- **[[Él]] (edge):** Két csúcs közötti kapcsolat.
- **Irányított gráf (directed graph, digraph):** Az éleknek iránya van: (u, v) él u-ból v-be mutat, de visszafelé nem feltétlenül.
- **Irányítatlan gráf:** Az élek mindkét irányban bejárhatók.
- **Súlyozott gráf:** Minden élnek van egy w(u,v) súlya (pl. távolság, költség, kapacitás).
- **Fok (degree):** Irányítatlan gráfban a csúcsba be- vagy belőle kimenő élek száma. Irányított gráfban: be-fok (in-degree) és ki-fok (out-degree).
- **Út (path):** Csúcsok sorozata, ahol egymást követő csúcsok éllel kapcsolódnak.
- **Kör (cycle):** Olyan zárt út, amelynek kezdő- és végcsúcsa megegyezik.
- **Összefüggő gráf:** Irányítatlan gráf, amelyben minden csúcspár között van út.
- **DAG (Directed Acyclic Graph):** Irányított, körmentes gráf – topologikus rendezés alapja.

## Reprezentációk

### [[Szomszédsági mátrix]] (Adjacency Matrix)

n×n mátrix, ahol M[i][j] = 1 (vagy az él súlya), ha van él i-ből j-be; 0 (vagy ∞) egyébként.
- Él lekérdezése: **O(1)**
- Szomszédok listázása: O(n)
- Memória: **O(n²)** → sűrű gráfra jó, ritka gráfra pazarló

### [[Szomszédsági lista]] (Adjacency List)

Minden csúcshoz tároljuk a szomszédai listáját (kimenő élek szomszédait).
- Él lekérdezése: O(deg(u))
- Szomszédok listázása: **O(deg(v))**
- Memória: **O(V+E)** → ritka gráfra hatékony

⚠️ **Vizsgán kiemelendő:** Gráfalgoritmusoknál mindig kérdezd meg: irányított vagy irányítatlan? Súlyozott vagy nem? Negatív élek? Ezek határozzák meg az algoritmusválasztást!

---

### 3.2 Gráfbejárások

#### Szélességi keresés (BFS – Breadth-First Search)

## Definíció

A **[[BFS]]** egy forráscsúcsból kiindulva **rétegesen** (szintenkénti sorrendben) járja be a gráfot: először az 1 lépésre lévő csúcsokat látogatja meg, majd a 2 lépésre lévőket, és így tovább. **[[Sor]]** (queue) adatszerkezetet használ.

## Intuíció

Képzeld el, hogy egy kőt dobsz a vízbe: a hullámok körkörösek és egyenletesen terjeszkednek kifelé. Ez a BFS viselkedése – minden „réteg" egyszerre terjed szét.

## Lépések

1. Inicializálás: d[s] = 0 (forrás távolsága), d[v] = ∞ minden más v-re. π[v] = NIL.
2. Tedd s-t a sorba.
3. **Amíg a sor nem üres:**
   - u = dequeue() – vedd ki a sor elejét.
   - u minden szomszédjára v:
     - Ha d[v] = ∞ (nem látogatott): d[v] = d[u] + 1, π[v] = u (szülő), enqueue(v).
4. Visszatérve: d[v] = s-től v-ig a legrövidebb út **élszámban** mérve (egységsúlyú gráfban).

## Pszedokód

```
BFS(G, s):
  d[v] = ∞ minden v-re; d[s] = 0; π[s] = NIL
  Q = üres sor; enqueue(Q, s)
  while Q nem üres:
    u = dequeue(Q)
    for minden (u,v) élre:
      if d[v] == ∞:
        d[v] = d[u] + 1
        π[v] = u
        enqueue(Q, v)
```

## Legrövidebb út visszakövetése

Az út s-től v-ig: v, π[v], π[π[v]], ..., s – visszafelé olvasva adja az utat.

## Komplexitás

| | |
|---|---|
| Idő | **O(V + E)** – minden csúcsot és élt egyszer nézünk |
| Tár | O(V) – sor és d[] tömb |

## Mikor érdemes használni

- Legrövidebb út keresése **egységsúlyú** gráfban.
- Összefüggőség vizsgálata irányítatlan gráfban.
- Kétszínezhetőség (bipartit gráf) tesztelése.

## Korlátok

- **Súlyozott gráfban** a legrövidebb út meghatározásához nem elég → Dijkstra kell.

---

#### Mélységi keresés (DFS – Depth-First Search)

## Definíció

A **[[DFS]]** egy ágon megy mélyre, amíg el nem ér egy végpontot vagy már látogatott csúcsot, majd visszalép és más ágat próbál. **[[Verem]]** (stack) adatszerkezetet vagy rekurzív hívásokat használ.

## Intuíció

Képzeld el, hogy egy labirintusban jársz: mindig az első szabad folyosón mész tovább, jelölve, wahere jártál; zsákutcánál visszalépsz az utolsó elágazáshoz és más irányt próbálsz.

## Lépések (rekurzív változat)

```
DFS(G, u):
  szín[u] = SZÜRKE; d[u] = ++idő    // belépési idő
  for minden (u,v) élre:
    if szín[v] == FEHÉR:
      π[v] = u
      DFS(G, v)
  szín[u] = FEKETE; f[u] = ++idő    // kilépési idő
```

**Fehér:** még nem látogatott. **Szürke:** folyamatban. **Fekete:** befejezett.

## Élcsoportok DFS-ben

| Éltípus | Meghatározás |
|---|---|
| Faél | DFS-fa szülő-gyerek kapcsolata |
| Visszaél (back edge) | Csúcsból ősére mutató él → **kör jele irányított gráfban** |
| Előreutaló él (forward) | Csúcsból leszármazottjára mutató él (csak irányított gráfban) |
| Keresztél (cross) | Különböző DFS-fák közötti vagy ugyanazon fa párhuzamos ágai |

## Alkalmazások

- **Ciklusdetektálás:** Ha DFS-ben visszaélt találunk → irányított gráfban kör van.
- **Összefüggő komponensek:** Minden DFS-futtatás egy komponenst jár be irányítatlan gráfban.
- **Topologikus rendezés (DAG-ban):** A csúcsokat f[u] kilépési idő szerint csökkenő sorrendbe rakva topologikus sorrendet kapunk.
- **Erősen összefüggő komponensek:** Kosaraju / Tarjan algoritmus alapja.

## Komplexitás

| | |
|---|---|
| Idő | **O(V + E)** |
| Tár | O(V) – rekurzív stack mélysége |

⚠️ **Vizsgán kiemelendő:** BFS és DFS az összes gráfalgoritmus alapja. BFS = legrövidebb út (egységsúly) és réteges vizsgálat. DFS = szerkezeti vizsgálat: ciklus, komponensek, topologikus rend, erős összefüggőség.

---

### 3.3 Minimális feszítőfa (MST)

## Definíció

Adott egy összefüggő, irányítatlan, súlyozott gráf G = (V, E, w). A **[[MST]] (Minimum Spanning Tree)** egy olyan réssgráf, amely:
- **Fa** (összefüggő, körmentes),
- tartalmazza az **összes csúcsot** (tehát feszítőfa),
- és az élek **összsúlya minimális** az összes ilyen feszítőfa közül.

**Intuíció:** Városokat akarod összekötni kábelekkel úgy, hogy mindenki elérje mindenkit, de a teljes kábelhossz minimális legyen. Ez az MST.

**Mohó alaptétel (Vágástétel / Kék szabály):** Ha S ⊂ V egy tetszőleges csúcshalmaz (vágás), és e az S-t és V\S-t összekötő élek közül a minimális súlyú, akkor e biztosan szerepel valamely MST-ben.

---

#### Kruskal algoritmus

## Definíció

A **[[Kruskal]]** algoritmus az éleket súly szerint rendezi, és egyenként adja hozzá az MST-hez, kihagyva azokat, amelyek kört alkotnának a már kiválasztott élekkel.

## Lépések

1. Rendezd az összes élt **növekvő súly** szerint.
2. Inicializálj **[[Union-Find]]** adatszerkezetet (minden csúcs saját diszjunkt komponense).
3. Minden (u, v, w) élre súly szerint növekvő sorrendben:
   - Ha Find(u) ≠ Find(v) (u és v különböző komponensben vannak – felvétel nem okoz kört):
     - Add hozzá (u, v)-t az MST-hez.
     - Union(u, v) – olvaszd össze a két komponenst.
4. Megállunk, ha n−1 élt vettünk fel (n-1 éles feszítőfa) vagy az él-lista kifogyott.

## Union-Find (Diszjunkt halmazok)

- **Find(x):** Megkeresi x komponensének képviselőjét (gyökerét). **Path compression**-nal gyorsítható: minden csomópontot közvetlenül a gyökérre mutatunk rá.
- **Union(x, y):** Összevonja x és y komponensét. **Rank (rang) alapú unióval**: a kisebb mélységű fát fűzzük a nagyobbhoz.
- Együtt: majdnem O(α(n)) az összes művelet, ahol α az inverz Ackermann-függvény (gyakorlatilag konstans, ≤ 4 bármely mérsékelt n-re).

## Komplexitás

| | |
|---|---|
| Rendezés | O(E log E) |
| Union-Find műveletek | O(E · α(V)) ≈ O(E) |
| **Összesen** | **O(E log E) ≈ O(E log V)** |

**Ritka gráfra (E << V²) hatékony.**

---

#### Prim algoritmus

## Definíció

A **[[Prim]]** algoritmus egy kezdőcsúcsból kiindulva **növeszti az MST-t**: mindig a fa és a fa-on kívüli csúcsok között átkelő, minimális súlyú élt választja.

## Lépések

1. Inicializálás: key[s] = 0, key[v] = ∞ minden más v-re, π[v] = NIL.
2. Tedd az összes csúcsot egy **[[prioritási sor]]**ba (min-heap) key érték szerint.
3. **Amíg a prioritási sor nem üres:**
   a. u = ExtractMin() – vedd ki a legkisebb key-jű csúcsot.
   b. u felvéve az MST-be (az MST-él: (π[u], u), ha u ≠ s).
   c. u minden szomszédjára v (amely még a prioritási sorban van):
      - Ha w(u,v) < key[v]: key[v] = w(u,v), π[v] = u, frissítsd a prioritási sort (DecreaseKey).
4. Az MST élei: {(π[v], v) : v ≠ s}.

## Komplexitás

| Implementáció | Idő |
|---|---|
| Bináris heap | **O(E log V)** |
| Fibonacci heap | O(E + V log V) |
| Tömb | O(V²) – sűrű gráfra |

**Sűrű gráfra Prim hatékonyabb, ritka gráfra Kruskal általában jobb.**

## Kruskal vs. Prim összehasonlítás

| | Kruskal | Prim |
|---|---|---|
| Megközelítés | Él-alapú (globális választás) | Csúcs-alapú (lokális növesztés) |
| Adatszerkezet | Union-Find | Prioritási sor |
| Ritka gráfra | Jobb | Rosszabb |
| Sűrű gráfra | Rosszabb | Jobb |
| Közös alap | Mindkettő mohó, mindkettő a vágástételt alkalmazza |

⚠️ **Vizsgán kiemelendő:** Mindkét algoritmus mohó stratégián alapul és az MST vágástételét (mohó alaptételt) alkalmazza. Kruskal globálisan válogat az élek között, Prim csúcsból kiindulva lokálisan növeszti a fát.

---

### 3.4 Legrövidebb utak

## Alapfogalmak

A legrövidebb út problémájában adott egy G = (V, E, w) súlyozott gráf és egy forrás s ∈ V. Keressük minden v ∈ V csúcsra a legkisebb összsúlyú utat s-től v-ig.

**Relaxáció:** Minden legrövidebb út algoritmus alapja. Ha d[v] > d[u] + w(u,v), akkor frissítjük: d[v] = d[u] + w(u,v). Vagyis ha u-n keresztül rövidebb út vezet v-be, mint az eddigi legjobb ismert út, frissítünk.

**Negatív kör:** Ha negatív összsúlyú kör érhető el, a legrövidebb út értelmetlen (−∞). Dijkstra ezt nem kezeli, Bellman-Ford detektálja.

---

#### Dijkstra algoritmus

## Definíció

A **[[Dijkstra]]** algoritmus egyforrású legrövidebb utakat keres **nemnegatív súlyú** irányított (vagy irányítatlan) gráfban. A mohó stratégiát alkalmazza: mindig a jelenlegi legkisebb ismert távolságú feldolgozatlan csúcsot veszi ki.

## Intuíció

Hasonló a Prim algoritmushoz MST-nél. Mindig a „legközelebb lévő" (legkisebb d[]-jű) feldolgozatlan csúcsot kezeljük, és frissítjük a szomszédait. A mohó döntés helyességét az biztosítja, hogy nemnegatív súlyoknál az egyszer kiszámított d[u] már nem csökkenhet tovább.

## Lépések

1. d[s] = 0, d[v] = ∞ minden más v-re. π[v] = NIL.
2. Tedd az összes csúcsot egy min-prioritási sorba d[] szerint.
3. **Amíg a prioritási sor nem üres:**
   a. u = ExtractMin()
   b. u minden kimenő szomszédjára (u, v, w):
      - Ha d[u] + w < d[v]: **relaxáció**: d[v] = d[u] + w; π[v] = u; DecreaseKey(v).
4. d[v] = legrövidebb út s-től v-ig. Az út visszakövetése π[] alapján.

## Pszedokód

```
Dijkstra(G, w, s):
  d[s] = 0; d[v] = ∞ minden más v-re
  Q = min-prioritási sor az összes csúccsal
  while Q nem üres:
    u = ExtractMin(Q)
    for minden (u,v,w) kimenő élre:
      if d[u] + w < d[v]:
        d[v] = d[u] + w
        π[v] = u
        DecreaseKey(Q, v, d[v])
```

## Komplexitás

| Implementáció | Idő |
|---|---|
| Bináris heap | **O((V + E) log V)** |
| Fibonacci heap | O(E + V log V) |
| Tömb | O(V²) – sűrű gráfra |

## Mikor érdemes / NEM érdemes

- **Érdemes:** Nemnegatív súlyú gráfban legrövidebb út keresésére. GPS navigáció, hálózati routing.
- **NEM érdemes:** Ha negatív élsúlyok vannak → Bellman-Ford szükséges.

⚠️ **Vizsgán kiemelendő:** Dijkstra NEM kezeli a negatív éleket! Negatív él esetén helytelen eredményt adhat, mert a mohó döntés (egyszer kész = végleges) nem tartható fenn.

---

#### Bellman-Ford algoritmus

## Definíció

A **[[Bellman-Ford]]** algoritmus egyforrású legrövidebb utakat keres, **negatív élsúlyokat is kezelve**, és képes **negatív kör** detektálására.

## Intuíció

Ha n csúcs van, a legrövidebb egyszerű útnak legfeljebb n−1 éle lehet (különben kör lenne benne). Ezért n−1 körön át relaxáljuk az **összes élt** – így minden optimális út megtalálható. Ha az n-edik körben is javul valami, az negatív kört jelez.

## Lépések

1. d[s] = 0, d[v] = ∞ minden más v-re. π[v] = NIL.
2. **i = 1-től |V|−1-ig** (n−1 kör):
   - Minden (u, v, w) élre:
     - Ha d[u] + w < d[v]: d[v] = d[u] + w; π[v] = u.
3. **Negatív kör ellenőrzése (egy extra kör):**
   - Minden (u, v, w) élre:
     - Ha d[u] + w < d[v]: **negatív kör létezik** → jelzés.
4. Ha nincs negatív kör: d[v] = s-től v-ig a legrövidebb út.

## Pszedokód

```
Bellman-Ford(G, w, s):
  d[s] = 0; d[v] = ∞ minden más v-re
  for i = 1 to |V|-1:
    for minden (u,v,w) élre:
      if d[u] + w < d[v]:
        d[v] = d[u] + w; π[v] = u
  // Negatív kör detektálás:
  for minden (u,v,w) élre:
    if d[u] + w < d[v]: return "Negatív kör!"
  return d
```

## Komplexitás

| | |
|---|---|
| Idő | **O(V · E)** |
| Tár | O(V) |

## Mikor érdemes használni

- Ha a gráf tartalmazhat **negatív éleket**.
- Ha **negatív körök detektálása** szükséges.
- Lassabb, mint Dijkstra, de robusztusabb.

⚠️ **Vizsgán kiemelendő:** Bellman-Ford n−1 körös relaxációja garantálja, hogy minden legfeljebb n−1 élű legrövidebb utat megtalál. Az n-edik (extra) kör a negatív kör detektálásra való.

---

#### Floyd–Warshall algoritmus

## Definíció

A **[[Floyd–Warshall]]** algoritmus **minden csúcspár** (i, j) között meghatározza a legrövidebb utat, dinamikus programozáson alapulva. Negatív éleket is kezel (negatív kör nélkül).

## Intuíció

Fokozatosan bővítjük, hogy milyen közbenső csúcsokon mehet át az út. Az k-adik iteráció után d[i][j] tartalmazza a legjobb utat i-ből j-be, amely csak az első k csúcson mehet keresztül közbenső csúcsként.

## Lépések

1. Inicializálás: d[i][j] = w(i,j) ha van él, 0 ha i=j, ∞ egyébként.
2. **k = 1-től n-ig** (megengedett közbenső csúcs):
   - Minden i-re és j-re:
     - d[i][j] = min(d[i][j], d[i][k] + d[k][j])
3. d[i][j] = legrövidebb út i-ből j-be.
4. Ha d[i][i] < 0 valamely i-re: negatív kör létezik.

## Komplexitás

| | |
|---|---|
| Idő | **O(V³)** |
| Tár | O(V²) |

## Mikor érdemes használni

- Kisebb-közepes gráfoknál, ahol **minden csúcspárra** kell a legrövidebb út.
- Tranzitív lezárt (átjárhatóság) számítása.

## Korlátok

- Nagy gráfnál O(V³) teljes mértékben kezelhetetlenné válik.

⚠️ **Vizsgán kiemelendő:** Floyd–Warshall = all-pairs shortest path, O(V³), DP-alapú. A belső ciklus a közbenső csúcs bővítése. Ismerd a három egymásba ágyazott ciklust!

---

## Algoritmusok összefoglalása – legrövidebb utak

| Algoritmus | Forrás | Negatív él | Negatív kör | Idő |
|---|---|---|---|---|
| BFS | Egyforrású | Nem (csak egységsúly) | Nem | O(V+E) |
| Dijkstra | Egyforrású | **Nem** | Nem | O((V+E) log V) |
| Bellman-Ford | Egyforrású | **Igen** | **Detektálja** | O(V·E) |
| Floyd–Warshall | Minden pár | **Igen** | **Detektálja** | O(V³) |

---

## + Vizsgán érdemes még megemlíteni

### Időkomplexitás jelölések

- **O(f(n)):** Felső korlát – az algoritmus legfeljebb c·f(n) lépést tesz (elég nagy n-re).
- **Ω(f(n)):** Alsó korlát – az algoritmus legalább c·f(n) lépést tesz.
- **Θ(f(n)):** Szoros korlát – egyszerre O és Ω: az algoritmus pontosan f(n) nagyságrendű.

### Algoritmusválasztás szempontjai

- **Bemenetméret:** Kis n-re az egyszerű O(n²) algoritmusok is megfelelhetnek.
- **Adateloszlás:** Majdnem rendezett bemeneten insertion sort kiváló (O(n) közelítő).
- **Stabilitásigény:** Ha stabil kell: merge sort, counting sort, radix sort.
- **Memóriakorlát:** In-place kell → quicksort, heapsort, insertion/selection sort.
- **Garantált felső korlát:** Ha legrosszabb eset is O(n log n) kell → merge sort vagy heapsort.
- **Elméleti vs. gyakorlati teljesítmény:** Quicksort átlagban gyorsabb a jobb cache-viselkedés miatt, bár elméletileg O(n²) a worst case.

---

## Rövid szóbeli összefoglaló (záróvizsga szintű megfogalmazás)

A részproblémára bontó módszerek három fő paradigmát ölelnek fel. A **mohó algoritmus** mindig lokálisan optimális döntést hoz, és akkor ad globálisan optimális megoldást, ha teljesül a mohó választási tulajdonság és az optimális részstruktúra – klasszikus példa az intervallumütemezés. Az **oszd meg és uralkodj** három fázisban – felosztás, rekurzív megoldás, összevonás – dolgozza fel a problémát; futási idejét a Mester-tétellel becsüljük, tipikus példa a merge sort. A **dinamikus programozás** az átfedő részproblémákat nem számolja újra, hanem tárolja az eredményeket; memoization felülről lefelé, tabuláció alulról felfelé dolgozik; a kulcs az állapot helyes definiálása.

Rendezéseknél az összehasonlításos rendezések alsó korlátja Ω(n log n). Az egyszerű rendezések O(n²)-esek, kivéve az insertion sort-ot, amely közel rendezett bemeneten O(n)-en fut. A hatékony rendezések közül merge sort stabil és garantáltan O(n log n), quicksort in-place és átlagban gyors, de O(n²) legrosszabb esetben, heapsort garantált O(n log n) és in-place. A nem összehasonlításos rendezések (counting, radix, bucket) lineáris vagy ahhoz közeli időt érhetnek el speciális feltételek mellett.

Gráfoknál a BFS sorral réteges bejárást végez és egységsúlyú gráfban legrövidebb utat ad, a DFS verremmel mélységi bejárást végez és ciklusdetektálásra, topologikus rendezésre alkalmas – mindkettő O(V+E). Minimális feszítőfához Kruskal él-alapú sorbarendezéssel és Union-Find-dal, Prim csúcs-alapon prioritási sorral dolgozik; mindkettő mohó stratégián alapul. Legrövidebb útra nemnegatív élekre Dijkstra, negatív élekre Bellman-Ford, minden csúcspárra Floyd–Warshall a megoldás.

---

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
- [[Mester-tétel]]

---

## Tipikus vizsgakérdések és mintaválaszok

1. **Mikor jó a mohó algoritmus?**
   Akkor, ha bizonyítható a mohó választási tulajdonság (a lokálisan legjobb döntés globálisan is jó) és az optimális részstruktúra (az optimum részmegoldásokból épül fel). Mindkét feltétel szükséges.

2. **Mi a különbség memoization és tabuláció között?**
   A memoization felülről lefelé, rekurzívan dolgozik, és a már kiszámított értékeket egy cache-ben tárolja. A tabuláció alulról felfelé, iteratívan tölti ki a táblázatot. Memoization csak a szükséges részproblémákat számolja ki, tabuláció minden állapotot.

3. **Miért fontos az Ω(n log n) alsó korlát?**
   Megmutatja, hogy összehasonlításos rendezéssel általánosan ennél gyorsabb nem lehet. Ha valaki azt állítja, hogy O(n)-es összehasonlításos rendezést talált, az lehetetlen.

4. **Mikor használunk BFS-t és mikor DFS-t?**
   BFS-t egységsúlyú gráfban a legrövidebb út meghatározásához és réteges vizsgálathoz. DFS-t szerkezeti vizsgálatokhoz: cikluskeresés, összefüggő komponensek, topologikus rendezés, erős összefüggőség.

5. **Mi a különbség Kruskal és Prim között?**
   Kruskal globálisan válogat az élek közt (él-alapú, Union-Find), ritka gráfra jobb. Prim csúcsból kiindulva lokálisan növeszti a fát (prioritási sorral), sűrű gráfra jobb. Mindkettő mohó, mindkettő MST-t ad.

6. **Mikor nem használható Dijkstra?**
   Negatív élsúly esetén nem helyes, mert a mohó döntés (egyszer kész = végleges) megdőlhet negatív élek hatására. Ilyenkor Bellman-Ford szükséges.

7. **Mit tud a Floyd–Warshall?**
   Minden csúcspárra megadja a legrövidebb utat DP-alapon, O(V³) időben. Negatív éleket kezel, de negatív körök esetén nincs értelmes megoldás (amit detektálni is tud).

8. **Miért O(n) a build-max-heap, ha n heapify-t hívunk?**
   Mert a heapify-k nem mind O(log n) idejűek: a fa alsóbb szintjein lévő, több csomópontnál lévő csomópontoknál a heapify rövid – egy pontos összeg-becslés adja az O(n) eredményt.
