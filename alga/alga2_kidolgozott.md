# Algoritmusok és adatszerkezetek I. – 2. alrész
## Elemi adatszerkezetek, BST, hash, gráfok és fák reprezentációja
### Teljes kidolgozás – szóbeli záróvizsga szintű

---

## 1. Elemi adatszerkezetek

### 1.1 Absztrakt adattípus (ADT)

## Definíció

Az **[[absztrakt adattípus]] (ADT)** egy matematikai modell, amely meghatározza, milyen **műveletek** végezhetők el az adatokon, és azok milyen szemantikával rendelkeznek – de **nem** mondja meg, hogyan valósítják meg ezeket belülre. Az ADT elválasztja az **interfészt** (mit tud csinálni?) az **implementációtól** (hogyan csinálja?).

## Hogyan működik

**Intuíció:** Gondolj egy autóra. Tudod, hogy a gázpedállal gyorsítasz, a fékkel lassítasz – ez az interfész, azaz az ADT. De nem kell tudnod, hogy benzinmotor vagy elektromos hajtja, hogyan működnek a fékek belülről – ez az implementáció. Ugyanígy egy verem ADT-nek van push, pop és peek művelete, de mindegy, hogy tömbbel vagy láncolt listával van megvalósítva.

**Miért fontos az elválasztás?**
- A kód könnyebben cserélhető, ha az interfész stabil marad.
- Különböző implementációk különböző kompromisszumokat kínálnak: sebesség, memóriahasználat, egyszerűség.
- Absztrakt szinten gondolkodva az algoritmus az implementációtól **független** – csak a műveletek időkomplexitása számít.

**Példa:** A sor (queue) ADT megvalósítható tömbös körkörös pufferrel vagy láncolt listával. Kívülről mindkettő ugyanúgy néz ki: enqueue, dequeue, front, isEmpty. De a belső működés más.

⚠️ **Vizsgán kiemelendő:** ADT szinten csak a **műveleteket** és azok **időkomplexitását** nézzük. Implementáció szinten nézhetjük a belső megvalósítást és a tényleges konstans tényezőket.

## Tipikus vizsgakérdések

- Mi a különbség az ADT és az implementáció között?
- Miért hasznos az absztrakció az adatszerkezeteknél?

---

### 1.2 Tömb (Array)

## Definíció

A **[[tömb]]** azonos típusú elemek rögzített méretű, **folytonos memóriaterületen** tárolt sorozata. Az elemek 0-tól (vagy 1-től) indexeltek, és az index alapján **O(1)** időben elérhetők.

## Hogyan működik

A tömb elemeit a memóriában **egymás mellé** tároljuk. Ha az első elem memóriacíme `base` és minden elem `s` byte-ot foglal, akkor az i-edik elem valódi memóriacíme:

```
cím(a[i]) = base + i × s
```

Ez a számítás konstans idejű, ezért az indexelés O(1) – ezért nevezik **közvetlen elérési** (random access) adatszerkezetnek.

## Előnyök

- **Véletlenszerű elérés O(1):** a[i] bármely i-re konstans idő.
- **Cache-barátság:** A szomszédos elemek a memóriában is szomszédosak → kevés cache-kihagyás (cache miss), ami valós rendszerekben nagy teljesítményelőnyt jelent.
- **Egyszerűség és alacsony overhead:** Nincs pointer-fej az elemek mellett.

## Hátrányok

- **Rögzített méret:** A klasszikus tömb mérete fordítási időben rögzített. Dinamikus tömbök (pl. Java ArrayList, C++ vector) ezt orvosolják **amortizált** átméretezéssel.
- **Közepébe szúrás / törlés drága (O(n)):** Az elemeket el kell tolni, ami n-arányos másolást jelent.

## Komplexitás

| Művelet | Idő |
|---------|-----|
| Elérés a[i] | **O(1)** |
| Keresés (rendezetlen) | O(n) |
| Keresés (rendezett, bináris keresés) | O(log n) |
| Végére szúrás (dinamikus tömb, amortizált) | O(1) |
| Közepébe szúrás | O(n) |
| Közepéből törlés | O(n) |

## Mikor érdemes / NEM érdemes

- **Érdemes:** Sok véletlen indexű olvasás; fix méretű adat; cache-érzékeny alkalmazások; rendezett adatnál bináris keresés.
- **NEM érdemes:** Ha sok dinamikus szúrás/törlés történik a közepén → láncolt lista.

---

### 1.3 Láncolt lista (Linked List)

## Definíció

A **[[láncolt lista]]** csomópontokból (node) áll, ahol minden csomópont tartalmaz egy **adatot** (értéket) és egy (vagy két) **pointert**, amely a következő (és előző) csomópontra mutat. A csomópontok nincsenek feltétlenül egymás mellett a memóriában.

## Típusok

- **Egyszeresen láncolt (singly linked):** Minden csomópont csak a következőre mutat. Bejárás csak előre lehetséges.
- **Kétszeresen láncolt (doubly linked):** Minden csomópont az előzőre és a következőre is mutat. Könnyebb visszafele bejárás és törlés.
- **Körkörös lista:** Az utolsó csomópont visszamutat az elsőre.

## Hogyan működik

Nincs folytonos memóriaterület. Minden csomópont bárhol lehet a heap-ben, csak a pointerek tartják össze a láncot. A fejcsomópont (head) a lista elejére mutat. Végig kell menni az egész listán, hogy megtaláljunk egy elemet – nincs közvetlen indexelés.

## Előnyök

- **Dinamikus méret:** Könnyen bővíthető / csökkenthető, nem kell előre foglalni helyet.
- **Ismert pozíciónál O(1) szúrás/törlés:** Ha rendelkezünk a megelőző csomópontra mutató pointerrel, a szúrás és törlés konstans idejű – csak pointert kell átirányítani.
- **Nincs előre lekötött memória:** Csak annyi helyet foglal, amennyi ténylegesen szükséges.

## Hátrányok

- **Keresés O(n):** Nincs közvetlen indexelés, a listát végig kell járni.
- **Pointer-overhead:** Minden csomópont extra memóriát igényel a pointer(ek)hez.
- **Cache-barátság gyenge:** A csomópontok szétszórtan lehetnek a memóriában → sok cache-kihagyás.

## Komplexitás

| Művelet | Idő |
|---------|-----|
| Keresés | O(n) |
| Elejébe szúrás | **O(1)** |
| Végéhez szúrás (tail pointer ismert) | **O(1)** |
| Közepébe szúrás (pozíció ismert) | **O(1)** |
| Törlés (pozíció ismert) | **O(1)** |
| Elérés index szerint | O(n) |

⚠️ **Vizsgán kiemelendő:** A láncolt lista és a tömb közötti döntés a leggyakoribb trade-off kérdés. Tömb: gyors indexelés O(1), drága közepébe szúrás/törlés O(n). Láncolt lista: olcsó szúrás/törlés ismert pozíciónál O(1), lassú keresés/indexelés O(n). Nincs egyértelműen jobb – a feladattól függ.

---

### 1.3 Verem (Stack)

## Definíció

A **[[verem]]** **LIFO** (Last In, First Out – utoljára be, először ki) elvű adatszerkezet: az utoljára betett elem jön ki először, mint egy tányérpakli, amiből mindig a legfelső tányért vesszük le.

## Alapműveletek

- **push(x):** Beteszi x-et a verem tetejére.
- **pop():** Kiveszi és visszaadja a verem tetején lévő elemet. (Ha üres: hiba/kivétel.)
- **peek() / top():** Visszaadja (de nem veszi ki) a verem tetején lévő elemet.
- **isEmpty():** True, ha a verem üres.

## Implementáció

**Tömbbel:** Van egy `top` egész változó, amely a verem tetejének indexét jelzi.
- push(x): `top++; a[top] = x;`
- pop(): `return a[top--];`
- Minden művelet: **O(1)**. Hátrány: rögzített maximális méret.

**Láncolt listával:** Mindig a lista elejére szúrunk / onnan törlünk.
- push(x): Új csomópontot szúrunk a fejre.
- pop(): A fejcsomópontot eltávolítjuk.
- Minden művelet: **O(1)**. Dinamikus méret.

## Alkalmazások

- **Rekurzió megvalósítása:** A hívási verem (call stack) verem-alapú – minden függvényhívás egy keret (frame) a veremen.
- **Zárójelezés ellenőrzése:** Nyitó zárójelet veremre tesszük, zárójelénél az illő nyitóját vesszük le és ellenőrizzük.
- **DFS iteratív megvalósítása:** A rekurzió helyett explicit veremmel.
- **Visszalépéses keresés (backtracking):** Állapotok veremre kerülnek.
- **Infix → Postfix konverzió (Shunting-yard algoritmus).**
- **Visszavonás (undo) funkció** szövegszerkesztőkben.

## Komplexitás

| Művelet | Idő |
|---------|-----|
| push | **O(1)** |
| pop | **O(1)** |
| peek / top | **O(1)** |
| Tár | O(n) |

---

### 1.4 Sor (Queue)

## Definíció

A **[[sor]]** **FIFO** (First In, First Out – először be, először ki) elvű adatszerkezet: ami először kerül be, az jön ki először – mint egy bolti sor, ahol a legkorábban álló kapja meg a kiszolgálást.

## Alapműveletek

- **enqueue(x):** Beteszi x-et a sor **végére**.
- **dequeue():** Kiveszi és visszaadja a sor **elejéről** az elemet.
- **front() / peek():** Visszaadja (nem veszi ki) a sor elején lévő elemet.
- **isEmpty():** True, ha a sor üres.

## Implementáció

**Körkörös tömbbel:** Két mutató: `head` (elejére) és `tail` (végére). A modulo operátor kezeli a körkörösséget: `tail = (tail + 1) % m`. Minden művelet **O(1)**. Előny: cache-barát. Hátrány: rögzített maximális méret.

**Láncolt listával:** Elejéről törlünk (`head`), végéhez szúrunk (`tail`). Minden művelet **O(1)**. Dinamikus méret.

## Prioritási sor (Priority Queue)

Nem érkezési sorrend, hanem **prioritás** dönt: mindig a legkisebb (vagy legnagyobb) prioritású elem kerül ki. Általában **bináris kupacként** implementálják.

- **insert(x, priority):** O(log n)
- **extractMin() / extractMax():** O(log n)
- **peekMin() / peekMax():** O(1)

Alkalmazások: Dijkstra algoritmus, Prim algoritmus, eseményvezérelt szimuláció, A* keresés.

## Alkalmazások

- **BFS:** A sor biztosítja a réteges bejárást – a sorba először tett csúcsok kerülnek ki először.
- **Nyomtatási sor, ütemezési feladatok:** Operációs rendszerekben a folyamatok ütemezése.
- **Feladatsorok (task queues):** Webes szervereken kérésfeldolgozás sorban.

## Komplexitás

| Művelet | Idő |
|---------|-----|
| enqueue | **O(1)** |
| dequeue | **O(1)** |
| front / peek | **O(1)** |
| Tár | O(n) |

---

## 2. Bináris keresőfák (BST)

### 2.1 Alapfogalmak

## Definíció

A **[[bináris keresőfa]] (BST)** egy bináris fa, amely kielégíti a **BST-rendezési tulajdonságot**: minden x csúcsnál a **bal részfában** csak x-nél **kisebb** kulcsú csúcsok vannak, a **jobb részfában** csak x-nél **nagyobb** kulcsú csúcsok.

## Fa terminológia

- **Gyökér (root):** A fa legfelső csúcsa – nincs szülője.
- **Levél (leaf):** Csúcs, amelynek nincs gyereke.
- **Belső csúcs:** Csúcs legalább egy gyerekkel.
- **Magasság (height):** A leghosszabb gyökér–levél út élszáma. Jelölés: h.
- **Mélység (depth):** Egy csúcs gyökértől való távolsága élben.
- **Részfa (subtree):** Egy csúcs és összes leszármazottjának halmaza.

**Bináris fa:** Minden csúcsnak legfeljebb 2 gyereke van (bal és jobb gyerek, amelyik hiányzik, az NIL).

## BST-rendezési tulajdonság (formálisan)

Ha x egy BST-beli csúcs:
- Minden y csúcsra x bal részfájában: **y.key < x.key**
- Minden z csúcsra x jobb részfájában: **z.key > x.key**

Ez a tulajdonság **rekurzívan** érvényes minden részfára is.

## Miért hasznos?

A BST-rendezési tulajdonság lehetővé teszi, hogy a keresés, beszúrás, törlés mindegyike **O(h)** időben fusson, ahol h a fa magassága. Ha a fa kiegyensúlyozott, h ≈ log n, tehát a műveletek **O(log n)**-esek. Ez gyorsabb, mint egy rendezetlen tömb O(n) keresése és flexibilisebb, mint egy rendezett tömb (ahol a szúrás drága).

**Intuíció:** Amikor keresünk, mindig tudjuk, melyik irányba kell menni (bal vagy jobb), így feleannyira csökkentjük a keresési teret minden lépésben – mint a bináris keresés tömbön.

---

### 2.2 Műveletek

#### Keresés (Search)

## Definíció

Adott k keresett kulcs. A keresés a gyökértől indul, és minden csúcsnál eldönti, hogy balra vagy jobbra kell-e lépni.

## Lépések

1. x = gyökér.
2. Ha x = NIL: a kulcs **nincs** a fában.
3. Ha k = x.key: **megtaláltuk**.
4. Ha k < x.key: x = x.left (balra lépés).
5. Ha k > x.key: x = x.right (jobbra lépés).
6. Vissza a 2. lépésre.

## Pszedokód

```
Search(x, k):
  if x == NIL or k == x.key: return x
  if k < x.key: return Search(x.left, k)
  else: return Search(x.right, k)
```

**Komplexitás:** O(h), ahol h a fa magassága.

---

#### Minimum és maximum keresés

- **Minimum:** A fa bal szélén menjünk le, amíg nincs bal gyerek → ez a legkisebb elem. **O(h)**.
- **Maximum:** A fa jobb szélén menjük le, amíg nincs jobb gyerek → ez a legnagyobb elem. **O(h)**.

---

#### Utód (Successor) és előd (Predecessor) keresés

- **In-order utód (successor):** Az x csúcs következő eleme az in-order bejárásban.
  - Ha x-nek van jobb részfája: a jobb részfa minimuma.
  - Ha nincs jobb részfája: menjünk fel a fán, amíg olyan csúcsot érünk el, amelynek mi a bal részfájában vagyunk.
- **O(h)** idő.

---

#### Beszúrás (Insert)

## Lépések

1. Hajts végre egy sikertelen keresést k-ra (menj le a fán, amíg NIL-t nem érsz).
2. Jegyezd meg az utolsó valódi csomópontot (szülő) és azt, hogy balról vagy jobbról értük el a NIL-t.
3. Hozz létre egy új csomópontot k kulccsal.
4. Kapcsold az új csomópontot a szülő bal vagy jobb gyerekeként (aszerint, honnan értük el a NIL-t).

**Komplexitás:** O(h).

**Megjegyzés:** A BST-ben nincs automatikus kiegyensúlyozás – a fa magassága függhet a szúrások sorrendjétől.

---

#### Törlés (Delete)

Ez a legbonyolultabb BST-művelet. Három eset van:

**1. eset – A csúcsnak nincs gyereke (levél):**
Egyszerűen töröljük: a szülőcsomópontban a ráutó pointert NIL-re állítjuk.

**2. eset – A csúcsnak pontosan 1 gyereke van:**
A törlendő csúcsot kivesszük, és az egyetlen gyerekét "**felhúzzuk**" a helyére: a szülő a törlendő csúcsra mutató pointerét az egyetlen gyerekre irányítjuk át.

**3. eset – A csúcsnak 2 gyereke van:**
Ez a bonyolult eset. A megoldás:
1. Keresd meg a törlendő csúcs **in-order utódját** (jobb részfa minimuma). Ez az elem az in-order sorban közvetlenül utána következik, és mindig levél vagy 1 gyerekes csomópont (mert ha lenne bal gyereke, az megelőzné).
2. Másold az in-order utód **kulcsát** a törlendő csúcsba (logikailag csere).
3. **Töröld az in-order utódot** (ami már 1-es vagy 0-ás eset, tehát egyszerű).

## Pszedokód (3. eset)

```
Delete(T, z):
  if z.left == NIL:       // 0 vagy 1 gyerek (jobbra)
    Transplant(T, z, z.right)
  elif z.right == NIL:    // 1 gyerek (balra)
    Transplant(T, z, z.left)
  else:                   // 2 gyerek
    y = Minimum(z.right)  // in-order utód
    if y.parent != z:
      Transplant(T, y, y.right)
      y.right = z.right
      y.right.parent = y
    Transplant(T, z, y)
    y.left = z.left
    y.left.parent = y
```

**Komplexitás:** O(h).

⚠️ **Vizsgán kiemelendő:** A kétgyerekes csúcs törlésénél az **in-order utód** (jobb részfa minimuma) módszert kell tudni elmagyarázni! Ez a leggyakoribb vizsgakérdés a BST-törlésre vonatkozóan.

---

### 2.3 Bejárások

## Definíció

A bejárás megadja, milyen **sorrendben** látogatjuk meg a fa csúcsait. Mindhárom bejárás **O(n)** idejű és **O(h)** veremteret (rekurzív stack) használ.

## [[Inorder]] bejárás (bal – gyökér – jobb)

**BST-nél az inorder bejárás az elemeket növekvő sorrendben adja ki.** Ez a BST egyik legalapvetőbb tulajdonsága.

```
inorder(x):
  if x ≠ NIL:
    inorder(x.left)
    print(x.key)
    inorder(x.right)
```

Alkalmazás: BST elemeit rendezett sorrendben kiírni; "kiegyenesíteni" a fát rendezett listává.

## [[Preorder]] bejárás (gyökér – bal – jobb)

A gyökeret először, aztán rekurzívan a bal, majd a jobb részfát.

```
preorder(x):
  if x ≠ NIL:
    print(x.key)
    preorder(x.left)
    preorder(x.right)
```

Alkalmazás: Fa másolása (szülő előbb kerül az újba, mint a gyerekei), fa soros mentése (serialization).

## [[Postorder]] bejárás (bal – jobb – gyökér)

Először a részfák, majd a gyökér.

```
postorder(x):
  if x ≠ NIL:
    postorder(x.left)
    postorder(x.right)
    print(x.key)
```

Alkalmazás: Fa törlése (előbb töröljük a gyerekeket, utána a szülőt); kifejezésfák kiértékelése (előbb az operandusok, utána a művelet).

⚠️ **Vizsgán kiemelendő:** BST-nél az inorder bejárás automatikusan rendezett sorrendet ad – ez az egyik legalapvetőbb és legfontosabb tulajdonság!

---

### 2.4 BST teljesítménye

## A magasság hatása

Minden BST-művelet (keresés, szúrás, törlés) **O(h)** idejű, ahol h a fa magassága. Ezért a teljesítmény teljes mértékben a fa magasságától függ:

- **Tökéletesen kiegyensúlyozott bináris fa:** h = log₂(n) → minden művelet **O(log n)**.
- **Erősen ferde fa (degenerált eset):** Ha az elemeket rendezett sorrendben szúrjuk be egy sima BST-be (pl. 1, 2, 3, 4, 5...), a fa egyoldalas lánccá romlik, h = n−1 → minden művelet **O(n)** (mint egy láncolt lista).

**Átlagos eset:** Véletlenszerű sorrendű szúrásoknál a várható magasság ≈ 1.39·log n – azaz átlagban O(log n).

**Összefoglalás:**

| Eset | Magasság | Műveletek ideje |
|------|---------|----------------|
| Kiegyensúlyozott | O(log n) | **O(log n)** |
| Véletlenszerű | O(log n) átlagosan | O(log n) várhatóan |
| Legrosszabb (rendezett input) | O(n) | **O(n)** |

## Megoldás: Kiegyensúlyozott keresőfák

---

### 2.5 Kiegyensúlyozott fák – AVL-fa és piros-fekete fa

## Miért kell?

A sima BST degenerálódhat rendezett bemenet esetén. A **kiegyensúlyozott keresőfák** célja: mindig logaritmikus magasságot garantálni, akármilyen sorrendben szúrjuk be az elemeket.

## [[AVL-fa]]

**Definíció:** Az AVL-fa olyan BST, amelyben minden csúcsnál a bal és jobb részfa magasságának különbsége legfeljebb 1 – ezt **egyensúlyfeltételnek** nevezzük.

**Egyensúlyfaktor:** balance(x) = height(x.right) − height(x.left). AVL-fában minden csúcsnál balance ∈ {−1, 0, +1}.

**Rotációk:** Ha egy szúrás vagy törlés megsérti az egyensúlyfeltételt, **forgatásokkal** (rotációkkal) helyreállítjuk:
- **Jobb rotáció (right rotation):** Bal gyereket felhúzzuk.
- **Bal rotáció (left rotation):** Jobb gyereket felhúzzuk.
- **Bal-jobb (double rotation):** Bal gyereken bal rotáció, majd a csúcson jobb rotáció.
- **Jobb-bal (double rotation):** Jobb gyereken jobb rotáció, majd a csúcson bal rotáció.

**Garantált magasság:** h ≤ 1.44·log(n+2) ≈ O(log n).

**Minden műveleti idő garantáltan O(log n).**

## [[Piros-fekete fa]] (Red-Black Tree)

**Definíció:** A piros-fekete fa olyan BST, ahol minden csúcs piros vagy fekete, és a következő négy szabály teljesül:
1. Minden csúcs piros vagy fekete.
2. A gyökér fekete.
3. Minden NIL-levél (sentinel) fekete.
4. Ha egy csúcs piros, mindkét gyereke fekete (nincs két egymást követő piros csúcs).
5. Minden csúcsból az összes leszármazott NIL-levélhez vezető út egyenlő számú fekete csúcsot tartalmaz (**fekete magasság**).

**Garantált magasság:** h ≤ 2·log(n+1) ≈ O(log n).

**Minden műveleti idő garantáltan O(log n).**

**Gyakorlati fontosság:** A Java `TreeMap`/`TreeSet` és a C++ `std::map`/`std::set` piros-fekete fával implementált. A Linux kernel is piros-fekete fát használ belső adatszerkezetként.

## AVL vs. Piros-fekete fa

| | AVL-fa | Piros-fekete fa |
|---|---|---|
| Egyensúlyfeltétel | Szigorúbb | Lazább |
| Magasság | Kisebb (≤ 1.44 log n) | Kisebb (≤ 2 log n) |
| Keresés | Gyorsabb | Kicsit lassabb |
| Szúrás/Törlés | Több rotáció | Kevesebb rotáció |
| Ideális eset | Sok keresés, kevés szúrás | Sok szúrás/törlés |

⚠️ **Vizsgán kiemelendő:** Mindkettő O(log n) garantált minden műveletre. AVL-fa: szigorúbb egyensúly, gyorsabb keresés. Piros-fekete fa: lazább egyensúly, gyorsabb szúrás/törlés. Ha csak O(log n) garanciát kell mondani, mindkettő egyenértékű.

---

## 3. Hasító táblázatok (Hash Table)

### 3.1 Alapfogalmak

## Definíció

A **[[hash tábla]]** (hasítótábla) kulcs-érték párokat tárol, és a kulcsokat egy **[[hash függvény]]** segítségével tömb-indexre képezi. A cél: átlagosan **O(1)** idejű keresés, beszúrás és törlés.

## Hogyan működik

1. Van egy `T[0..m−1]` tömb (a "hash tábla"), ahol m a tábla mérete.
2. A `h(k)` hash függvény minden k kulcshoz egy 0..m−1 indexet rendel.
3. A k kulcsú elem a `T[h(k)]` pozícióba kerül (vagy az ahhoz tartozó struktúrába).

**Jó hash függvény három tulajdonsága:**
- **Determinisztikus:** Ugyanarra a kulcsra mindig ugyanazt az indexet adja.
- **Egyenletes eloszlás:** Az elemeket egyenletesen szórja szét a táblában → kevés ütközés.
- **Gyorsan számítható:** Maga a hash-számítás ne legyen szűk keresztmetszet.

**Egyszerű példa – maradékos hash:**
`h(k) = k mod m`, ahol m prímszám (a prímszám jobban szétszórja az értékeket, mint 2-hatvány).

**Karakterlánc hash példa (Horner-séma):**
`h("abc") = (a·p² + b·p + c) mod m` – ahol p egy alapszám (pl. 31).

**Ütközés (collision):** Két különböző kulcs ugyanarra az indexre esik: `h(k1) = h(k2)`, de `k1 ≠ k2`. Ez **elkerülhetetlen**, ha a kulcstartomány nagyobb, mint m.

---

### 3.2 Ütközéskezelés

#### Láncolás (Chaining)

## Definíció

Minden tábla-slotban egy **láncolt lista** (vagy más gyűjtemény) tárolja az összes olyan elemet, amelynek hash értéke arra az indexre esik. Ha ütközés van, az új elemet a listához fűzzük.

## Hogyan működik

- **Keresés:** Számítjuk `h(k)`-t, majd a `T[h(k)]` slotban lévő listán végigmegyünk és összehasonlítjuk a kulcsokat.
- **Szúrás:** Számítjuk `h(k)`-t, az elemet a lista elejéhez fűzzük (O(1)).
- **Törlés:** Megkeressük az elemet a listában, majd töröljük.

## Átlagos keresési idő

Ha a terhelési tényező α = n/m (elemek száma / tábla mérete):
- Sikeres keresés: Θ(1 + α/2) ≈ Θ(1 + α)
- Sikertelen keresés: Θ(1 + α)

Ha α = O(1) (azaz m ≥ c·n), akkor az összes műveleti idő átlagosan **O(1)**.

## Előnyök / Hátrányok

- **Előnyök:** Egyszerű, a tábla soha nem telik meg, törlés egyszerű.
- **Hátrányok:** Extra memória a listákhoz; cache-barátság gyenge (a listaelemek szétszórtan vannak).

---

#### Nyílt címzés (Open Addressing)

## Definíció

Nyílt címzésnél **nincs külső lista** – ha ütközés van, a következő szabad helyet keressük a **táblán belül** meghatározott módszerrel. Minden elem a táblában tárolódik.

## Próbasorozat

A próbasorozat: `h(k, 0), h(k, 1), h(k, 2), ...` – egymás utáni próbált indexek, amelyeken keressük a szabad helyet (szúrásnál) vagy az elemet (kereséskor).

## Lineáris próba (Linear Probing)

`h(k, i) = (h'(k) + i) mod m`

Az ütközésnél a következő szabad helyet keressük egyenként előre haladva.

**Probléma: Elsőrendű klaszteresedés (primary clustering).** Az elfoglalt helyek klaszterekbe gyűlnek, ami lassítja a keresést, mert minden új ütköző elem a klaszter végére kerül, tovább növelve azt.

## Kvadratikus próba (Quadratic Probing)

`h(k, i) = (h'(k) + c₁·i + c₂·i²) mod m`

Csökkenti az elsőrendű klaszteresedést, de **másodlagos klaszteresedés** (secondary clustering) előfordulhat: két azonos hash-értékű kulcs ugyanazt a próbasorozatot járja be.

## Dupla hash (Double Hashing)

`h(k, i) = (h₁(k) + i·h₂(k)) mod m`

Két különböző hash függvényt használ. A próbasorozat lépésközét `h₂(k)` adja, amely kulcsonként más.
- Elkerüli mind az elsőrendű, mind a másodlagos klaszteresedést.
- A leghatékonyabb nyílt-címzéses módszer, de bonyolultabb.
- Fontos: `h₂(k)` soha ne legyen 0, és m-hez relatív prím legyen.

## Törlés nyílt címzésnél

Nyílt címzésnél **nem lehet egyszerűen törölni** egy elemet! Ha törlünk egy elemet, a próbalánc megszakadna: egy keresés, amelynek keresési útja átment ezen az elemen, korai NIL-t találna, és azt hinné, hogy a keresett elem nincs ott – holott van, csak odébb.

**Megoldás:** "Törölt" jelölőt (**tombstone**) helyezünk az elemek helyére. Szúrásnál egy tombstone-ra is írhatunk, keresésnél átlépjük a tombstone-okat.

**Hátrány:** A tombstone-ok felhalmozódásával a tábla "szennyezetté" válik, ami lassítja a keresést → időnként **rehashing** szükséges.

⚠️ **Vizsgán kiemelendő:** Nyílt címzésnél a load factor SOHA nem lehet ≥ 1 (a tábla megtelhet!). Chainingnél α > 1 is lehetséges. Lineáris próbánál a klaszteresedés a fő probléma. Dupla hash elkerüli a klaszteresedést, de bonyolultabb.

---

### 3.3 Teljesítmény és terhelési tényező

## [[Load factor]] (Terhelési tényező)

`α = n / m`, ahol n az elemek száma, m a tábla mérete.

- **α közel 0:** Tábla alig teli, kevés ütközés, de sok memória pazarlik.
- **α = 0.7:** Általánosan jó kompromisszum – jó teljesítmény, mérsékelt memóriahasználat.
- **α → 1 (nyílt címzésnél):** Nagyon sok ütközés, az átlagos próbák száma drasztikusan nő.
- **α > 1 (csak chainingnél lehetséges):** A listák átlagos hossza α.

**Chainingnél:** Az átlagos keresési idő Θ(1 + α). Ha α = O(1), O(1) átlagos idő.

**Lineáris próbánál:** Az átlagos próbák száma sikertelen keresésnél ≈ 1/(1−α)². Ha α = 0.9, ez ≈ 50 próba!

## [[Rehashing]] (Újrahashelés)

Ha α túl nagy lesz (pl. α > 0.75 határértéknél), egy **nagyobb táblát** hozunk létre (általában kétszeres méret), és az **összes elemet újra hash-eljük** az új táblába (mert az új m-hez tartozó `h(k)` értékek változnak).

- Egyszeri rehashing: O(n) idő.
- Amortizáltan: az elemenkénti átlagos cóst O(1) – mint a dinamikus tömb bővítése.

---

### 3.4 Összefoglalás

## Komplexitás

| Művelet | Átlagos | Legrosszabb |
|---------|---------|-------------|
| Keresés | **O(1)** | O(n) |
| Szúrás | **O(1)** | O(n) |
| Törlés | **O(1)** | O(n) |

A legrosszabb eset akkor áll elő, ha minden elem ugyanarra az indexre hash-elődik (pl. rossz hash függvény vagy speciálisan összeállított input). Ezért fontos a jó hash függvény és a megfelelő load factor tartása.

## Mikor érdemes / NEM érdemes

- **Érdemes:** Gyors lookup, insert, delete; a kulcsok jól hash-elhetők; a load factor kordában tartható.
- **NEM érdemes:** Rendezett bejárás szükséges (BST jobb, O(log n) és rendezett); a kulcstartomány ismert és kicsi (counting sort / tömb jobb); ha a legrosszabb eset garantáltan O(log n) kell (BST jobb, hash O(n) legrosszabb).

---

## 4. Fák és gráfok számítógépes reprezentációja

### 4.1 Fa reprezentációk

#### Tömbös reprezentáció

## Definíció

A fa csúcsait egy tömbben tároljuk **level-order** (szintenkénti, balról jobbra) sorrendben. A gyöker az 1-es (vagy 0-ás) indexen van.

## Indexszámítás (0-indexelésnél)

Az i-edik csomópont:
- **Bal gyerek:** 2i + 1
- **Jobb gyerek:** 2i + 2
- **Szülő:** ⌊(i − 1) / 2⌋

## Mikor alkalmazható

**Teljes vagy közel teljes bináris fáknál** kiváló – klasszikus alkalmazás a **[[kupac]] (bináris heap)**.

## Előnyök

- Nincs pointer overhead.
- Nagyon cache-barát – a csomópontok egymás mellett vannak a memóriában.
- Az indexszámítás aritmetikai, konstans idejű.

## Hátrányok

- Nem teljes fáknál sok üres slot keletkezik, ami memóriahasználatot pazarolja.
- Nem flexibilis – a fa struktúrája nehézkes módosítani.

---

#### Láncolt reprezentáció

## Hogyan működik

Minden csomópont egy rekord (struct), amely tartalmaz:
- kulcs/adat mezőt
- pointert a bal gyerekre (`left`)
- pointert a jobb gyerekre (`right`)
- (opcionálisan) pointert a szülőre (`parent`)

A fa gyökerét a `root` pointer azonosítja.

## Előnyök

- Rugalmas – bármely formájú fa tárolható.
- Nincs üres hely pazarlás – pontosan annyi memória, amennyi kell.
- Egyszerű a fa struktúrájának módosítása (rotációk, stb.).

## Hátrányok

- Pointer overhead (minden csomópont extra memória a pointerekhez).
- Cache-barátság rosszabb – a csomópontok szétszórtan lehetnek.

---

#### Gyereklista reprezentáció (általános fáknál)

Ha a csúcsoknak **tetszőleges számú** gyereke lehet, minden csomóponthoz tároljuk a gyerekek listáját (láncolt lista vagy dinamikus tömb). Fa erdők esetén is használható.

---

### 4.2 Gráf reprezentációk

#### [[Szomszédsági mátrix]] (Adjacency Matrix)

## Definíció

Az n × n méretű mátrix, ahol `M[i][j]` értéke:
- 1 (vagy az él súlya), ha van él i-ből j-be,
- 0 (vagy ∞), ha nincs él.

Irányítatlan gráfban a mátrix szimmetrikus: M[i][j] = M[j][i].

## Hogyan működik és kompromisszumok

- **Él lekérdezése ("van-e él i és j között?"):** **O(1)** – egyszerű tömb-index.
- **Szomszédok listázása (i összes szomszédja):** O(V) – az i-edik sort végig kell nézni, még ha kevés szomszéd is van.
- **Tárméret:** **O(V²)** – még ritka gráfnál is V² memóriát foglal.

## Mikor érdemes / NEM érdemes

- **Érdemes:** Sűrű gráfnál (E ≈ V²), ahol a memória így sem pazarlódik jelentősen. Gyors éllekérdezés kell. Floyd–Warshall algoritmusnál természetes representáció.
- **NEM érdemes:** Ritka gráfnál (V² memória jobbára üres cellák lesznek). BFS/DFS esetén O(V²) szomszédlistázás.

---

#### [[Szomszédsági lista]] (Adjacency List)

## Definíció

Minden csúcshoz tároljuk a tőle kimenő élek célcsúcsainak listáját. Megvalósítható:
- Tömb listák tömbjeként: `adj[v]` = v szomszédainak listája (láncolt lista vagy dinamikus tömb).
- Súlyozott gráfban: `adj[v]` = (szomszéd, súly) párok listája.

## Hogyan működik és kompromisszumok

- **Él lekérdezése:** O(deg(u)) – végig kell menni u szomszádjain.
- **Szomszédok listázása:** **O(deg(v))** – csak a tényleges szomszédokat kell végignézni.
- **Tárméret:** **O(V + E)** – ritka gráfon sokkal hatékonyabb.

## Mikor érdemes / NEM érdemes

- **Érdemes:** Ritka gráfnál (E << V²). BFS, DFS, Dijkstra, Prim – mind lista alapján fut hatékonyan. A legtöbb valós gráf (közösségi hálók, úthálózatok) ritka.
- **NEM érdemes:** Gyors éllekérdezés kell ("van-e él?") → mátrix jobb.

---

#### [[Él lista]] (Edge List)

## Definíció

Az összes él felsorolása `(u, v, w)` hármasok listájaként.

- **Tárméret:** O(E)
- **Él lekérdezés:** O(E) – végig kell menni a listán
- **Élek sorbarendezése:** Közvetlen, egyszerű

## Mikor érdemes használni

- **Kruskal algoritmusnál** ideális: az élt súly szerint rendezzük, majd egyenként vesszük.
- Ritkán használt általános célra, mert sem gyors éllekérdezést, sem gyors szomszédlistázást nem ad.

---

#### [[Incidenciamátrix]] (Incidence Matrix)

## Definíció

V × E méretű mátrix. Sor = csúcs, oszlop = él. `M[v][e]` = 1, ha v incidens e-vel (azaz e egyik végpontja v).

## Mikor érdemes használni

- Hálózati folyam, párosítás (matching) feladatoknál.
- Ritka alkalmazás a standard algoritmusoknál – főleg elméleti célokra.

---

### 4.3 Összehasonlítás – mikor mit válasszunk?

| Szempont | Szomszédsági mátrix | Szomszédsági lista |
|----------|--------------------|--------------------|
| Tárméret | **O(V²)** | **O(V + E)** |
| Él lekérdezés (u,v) | **O(1)** | O(deg(u)) |
| Szomszédok bejárása | O(V) | **O(deg(v))** |
| Ritka gráf | Pazarló | Hatékony |
| Sűrű gráf | Hatékony | Nincs nagy előny |
| BFS / DFS futási idő | O(V²) | **O(V + E)** |
| Floyd–Warshall | Természetes | Kevésbé kényelmes |
| Kruskal | Nem ideális | Nem ideális (él lista jobb) |

⚠️ **Vizsgán kiemelendő:** Gráfalgoritmusok futási ideje **függ a reprezentációtól**! Mindig pontosítsd: "Szomszédsági listával O(V+E), mátrixszal O(V²)." BFS és DFS elemzésekor ezt mindig meg kell jegyezni.

---

### 4.4 Speciális reprezentációk

**[[Él lista]]:** Élek egyszerű felsorolása. Kruskal algoritmusnál természetes.

**[[Incidenciamátrix]]:** Csúcs-él kapcsolatokat mátrixban tárolja. Hálózatelméleti feladatoknál hasznos.

---

## + Vizsgán érdemes még megemlíteni

- **Pointer** alapvető a láncolt adatszerkezetekben – minden dinamikus struktúra alapja.
- **Dinamikus memóriahasználatnál** fontos a felszabadítás (C/C++-ban: memóriaszivárgás), valamint a hibakezelés (NULL-pointer dereferencia).
- **Cache/locality:** A tömb cache-barát (egymás melletti elemek → kevés cache-kihagyás). A láncolt lista cache-barátság szempontjából gyenge. Ez a különbség a valós teljesítményre is hatással van.
- **Gyakorlati példák:** Adatbázis-indexelés (B-fa, B+-fa), keresőrendszerek (hash tábla kulcs → dokumentum), útvonaltervezés (gráf reprezentáció), DNS (hash tábla domain → IP).

---

## Rövid szóbeli összefoglaló (záróvizsga szintű megfogalmazás)

Az adatszerkezet-választás alapvetően meghatározza az algoritmus teljesítményét. ADT szinten a műveleteket és azok komplexitását nézzük, implementáció szinten a belső megvalósítást. A **tömb** gyors véletlen indexelést O(1) biztosít, de közepébe szúrás/törlés O(n), mert az elemeket el kell tolni. A **láncolt lista** dinamikusan méretezhető, ismert pozíciónál szúrás/törlés O(1), de keresés O(n) és cache-barátság gyenge. A **verem** LIFO elvű, push/pop O(1), rekurzió és DFS alapja. A **sor** FIFO elvű, enqueue/dequeue O(1), BFS alapja; a prioritási sor kupac alapú, O(log n) kivétellel.

A **bináris keresőfa** a rendezési tulajdonsága miatt irányítottan kereshet, minden művelet O(h) idejű. Ha a fa kiegyensúlyozatlan, h = O(n) degenerált esetben; kiegyensúlyozott fák (AVL, piros-fekete) O(log n)-t garantálnak. Az inorder bejárás BST-ben növekvő sorrendet ad.

A **hash tábla** hash függvénnyel O(1) átlagos keresést, szúrást, törlést biztosít. Ütközéskezelés: chaining (lista per slot) vagy nyílt címzés (lineáris próba, kvadratikus, dupla hash). A load factor és a rehashing kulcsfontosságú a teljesítmény fenntartásában.

Fák és gráfok reprezentációjánál: tömbös tárolás kupachoz és teljes bináris fákhoz, láncolt csomópontok általános BST-hez és egyéb fákhoz. Gráfoknál szomszédsági mátrix O(1) éllekérdezéssel sűrű gráfra, szomszédsági lista O(V+E) tárolással és hatékony bejárással ritka gráfra optimális.

---

## Kulcsfogalmak

- [[absztrakt adattípus]]
- [[tömb]]
- [[láncolt lista]]
- [[verem]]
- [[sor]]
- [[prioritási sor]]
- [[bináris keresőfa]]
- [[inorder]]
- [[preorder]]
- [[postorder]]
- [[AVL-fa]]
- [[piros-fekete fa]]
- [[hash tábla]]
- [[hash függvény]]
- [[load factor]]
- [[rehashing]]
- [[chaining]]
- [[szomszédsági mátrix]]
- [[szomszédsági lista]]
- [[él lista]]
- [[incidenciamátrix]]
- [[kupac]]

---

## Tipikus vizsgakérdések és mintaválaszok

1. **Mi a különbség ADT és implementáció között?**
   Az ADT a műveleteket és azok szemantikáját írja le (mit tud csinálni), az implementáció pedig a konkrét belső megvalósítást (hogyan csinálja). Például a sor ADT (FIFO, enqueue/dequeue) megvalósítható tömbös körpufferrel vagy láncolt listával is.

2. **Mikor jobb a tömb, és mikor a láncolt lista?**
   Tömb gyors véletlenszerű indexeléshez (O(1)), láncolt lista sok dinamikus szúráshoz/törléshez ismert pozíciónál (O(1)). Tömb cache-barátabb, lista dinamikus méretű. Ha sok a keresés-indexelés, tömb; ha sok a szúrás-törlés a lista elejére/közepébe, láncolt lista.

3. **Miért romolhat le a BST teljesítménye O(n)-re?**
   Ha a fa kiegyensúlyozatlanná válik, például rendezett sorrendű elemek szúrásakor, a fa lánccá degenerálódik és a magasság n-1 lesz. Így minden művelet O(n)-es, mint egy egyszerű listán.

4. **Hogyan kezeljük a hash ütközéseket?**
   Kétféle módszerrel: **chaining** (láncolás) esetén minden slotban egy lista tárolja az összes ütköző elemet; **nyílt címzés** esetén a próbasorozat alapján keresünk szabad slotot a táblán belül (lineáris próba, kvadratikus próba, dupla hash).

5. **Mit jelent a load factor, és miért fontos?**
   A load factor α = n/m az elemek száma és a tábla mérete hányadosa. Nagy α esetén sok ütközés várható, ami lassítja a keresést. Ha α meghalad egy küszöbértéket (pl. 0.75), rehashing szükséges: kétszeres méretű új táblát hozunk létre és az összes elemet újra behelyezzük.

6. **Mikor válasszunk szomszédsági mátrixot?**
   Sűrű gráfnál (sok él), ha az O(V²) tárméret nem gond, és ha sokszor kell gyors éllekérdezés ("van-e él i és j között?" → O(1)). Például Floyd–Warshall algoritmusnál természetes.

7. **Mikor jobb a szomszédsági lista?**
   Ritka gráfnál, ahol E << V², mert az O(V+E) tárméret jóval kisebb az O(V²)-nél. BFS/DFS esetén a szomszédok bejárása O(deg(v)), nem O(V), ami teljes bejárásnál O(V+E) futást ad.

8. **Mi az in-order utód, és miért kell a BST-törléshez?**
   Az in-order utód az a csomópont, amely az in-order bejárásban közvetlenül a törlendő után következik – ez a jobb részfa minimuma. Kétgyerekes csúcs törlésénél az in-order utód kulcsát másoljuk a törlendő helyére, majd az utódot töröljük (ami már egyszerűbb eset).

9. **Mi a különbség a verem és a sor között?**
   Verem LIFO (Last In, First Out): az utoljára betett elem jön ki először – push, pop O(1). Sor FIFO (First In, First Out): az először betett elem jön ki először – enqueue, dequeue O(1). Verem alapja a DFS és a rekurzió; sor alapja a BFS.

10. **Mikor érdemes AVL-fát, mikor piros-fekete fát használni?**
    AVL-fa szigorúbb egyensúlyt tart, kisebb magasságot garantál → gyorsabb keresés. Piros-fekete fa kevesebb rotációt igényel szúrásnál/törlésnél → gyorsabb módosítás. Ha a keresés dominál: AVL. Ha sok szúrás/törlés van: piros-fekete fa. Mindkettő O(log n) garantált.
