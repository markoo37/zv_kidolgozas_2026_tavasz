# Algoritmusok és adatszerkezetek I. – 2. alrész
## Elemi adatszerkezetek, BST, hash, gráfok és fák reprezentációja

---

## 1. Elemi adatszerkezetek

### 1.1 Alapfogalmak
**Rövid definíció:**  
Az **[[absztrakt adattípus]] (ADT)** azt mondja meg, milyen műveleteket tud egy adatszerkezet, nem azt, hogyan van konkrétan megvalósítva.

**Működési elv:**  
- Különválasztjuk az interfészt és az implementációt.  
- Ugyanazt az ADT-t többféle belső megoldással is meg lehet írni.  
- Mindig figyelni kell az **időkomplexitásra** és **tárkomplexitásra**.

**Egyszerű példa:**  
A verem ADT lehet tömbbel és listával is implementálva, de kívülről ugyanazokat a műveleteket látjuk (`push`, `pop`).

**Vizsgán fontos kulcsszavak:**  
**[[absztrakt adattípus]]**, **interfész**, **implementáció**, **időkomplexitás**, **tárkomplexitás**

---

### 1.2 Lineáris adatszerkezetek

#### Tömb (array)
**Rövid definíció:**  
A **[[tömb]]** azonos típusú elemek folytonos memóriaterületen tárolt sorozata.

**Működési elv:**  
- Index alapján közvetlen elérés: O(1).  
- Jó cache-lokalitás a memóriafolytonosság miatt.  
- Középre beszúrás/törlés drága, mert elemeket kell tolni.

**Egyszerű példa:**  
Ha sok véletlen indexű olvasás kell (pl. `a[i]` gyakran), tömb nagyon hatékony.

**Vizsgán fontos kulcsszavak:**  
**[[tömb]]**, **indexelés O(1)**, **memóriafolytonosság**, **cache-locality**

#### Láncolt lista (linked list)
**Rövid definíció:**  
A **[[láncolt lista]]** csomópontokból áll, ahol a csomópontok pointerekkel kapcsolódnak.

**Működési elv:**  
- Dinamikusan növelhető/csökkenthető méret.  
- Egyszeresen vagy kétszeresen láncolt lehet.  
- Ismert pozíciónál beszúrás/törlés O(1), de keresés tipikusan O(n).

**Egyszerű példa:**  
Ha sok törlés-beszúrás történik a lista elején vagy ismert pozíción, listával egyszerűbb és gyorsabb lehet.

**Vizsgán fontos kulcsszavak:**  
**[[láncolt lista]]**, **csomópont**, **pointer**, **dinamikus méret**, **O(1) beszúrás/törlés**

---

### 1.3 Verem (stack)
**Rövid definíció:**  
A **[[verem]]** LIFO elvű adatszerkezet: az utoljára betett elem jön ki először.

**Működési elv:**  
- Alapműveletek: `push`, `pop`, `top/peek`.  
- Megvalósítható tömbbel vagy listával.  
- Sok algoritmusnál implicit vagy explicit verem működik.

**Egyszerű példa:**  
Rekurzív függvényhívások a hívási veremben tárolódnak, visszatérés fordított sorrendben történik.

**Vizsgán fontos kulcsszavak:**  
**[[verem]]**, **LIFO**, **push**, **pop**, **hívási verem**

---

### 1.4 Sor (queue)
**Rövid definíció:**  
A **[[sor]]** FIFO elvű adatszerkezet: ami előbb bekerül, előbb is jön ki.

**Működési elv:**  
- Alapműveletek: `enqueue`, `dequeue`, `front`.  
- Implementálható láncolt listával vagy **körkörös tömbbel**.  
- Fontos változat a **[[prioritási sor]]**, ahol nem érkezési sorrend dönt.

**Egyszerű példa:**  
Nyomtatási feladatok klasszikus sorban várnak feldolgozásra.

**Vizsgán fontos kulcsszavak:**  
**[[sor]]**, **FIFO**, **enqueue**, **dequeue**, **[[prioritási sor]]**

---

## 2. Bináris keresőfák (BST)

### 2.1 Alapfogalmak
**Rövid definíció:**  
A **[[bináris keresőfa]] (BST)** olyan bináris fa, ahol minden csúcsnál bal oldalon kisebb, jobb oldalon nagyobb kulcsok vannak.

**Működési elv:**  
- Fa: hierarchikus adatszerkezet gyökérrel és részfákkal.  
- Bináris fa: legfeljebb két gyerek/csúcs.  
- BST-rend miatt keresés irányítottan történik (balra vagy jobbra lépünk).

**Egyszerű példa:**  
Ha a gyökér 20, és a keresett kulcs 12, balra megyünk; ha 27, jobbra.

**Vizsgán fontos kulcsszavak:**  
**[[bináris keresőfa]]**, **gyökér**, **bal részfa**, **jobb részfa**, **rendezési tulajdonság**

---

### 2.2 Műveletek
**Rövid definíció:**  
BST-ben a fő műveletek: keresés, beszúrás, törlés.

**Működési elv:**  
- **Keresés**: kulcs alapján lefelé haladunk.  
- **Beszúrás**: a megfelelő üres helyre tesszük az új csúcsot.  
- **Törlés**:  
  - 0 gyerek: simán törölhető,  
  - 1 gyerek: a gyereket felhúzzuk,  
  - 2 gyerek: in-order utóddal vagy előddel helyettesítünk.

**Egyszerű példa:**  
Kétgyerekes csúcs törlésekor gyakran a jobb részfa legkisebb elemét tesszük a helyére.

**Vizsgán fontos kulcsszavak:**  
**BST keresés**, **BST beszúrás**, **BST törlés**, **in-order utód**, **0/1/2 gyerekes eset**

---

### 2.3 Bejárások
**Rövid definíció:**  
A bejárás megadja, milyen sorrendben látogatjuk a fa csúcsait.

**Működési elv:**  
- **[[inorder]]**: bal - gyökér - jobb (BST-nél rendezett sorrend).  
- **[[preorder]]**: gyökér - bal - jobb.  
- **[[postorder]]**: bal - jobb - gyökér.

**Egyszerű példa:**  
BST elemeit növekvő sorrendben kiírni: inorder bejárás.

**Vizsgán fontos kulcsszavak:**  
**[[inorder]]**, **[[preorder]]**, **[[postorder]]**, **fa bejárás**

---

### 2.4 Tulajdonságok
**Rövid definíció:**  
A BST teljesítményét alapvetően a fa **magassága** határozza meg.

**Működési elv:**  
- Kiegyensúlyozottabb fa -> kisebb magasság -> gyorsabb műveletek.  
- Erősen ferde fa esetén lánccá romolhat.  
- Emiatt lehet átlagban O(log n), de legrosszabb esetben O(n).

**Egyszerű példa:**  
Rendezett adatsor beszúrása sima BST-be gyakran ferde fát eredményez.

**Vizsgán fontos kulcsszavak:**  
**fa magasság**, **kiegyensúlyozatlanság**, **átlagos O(log n)**, **legrosszabb O(n)**

---

### 2.5 Kiegyensúlyozott fák (csak említés)
**Rövid definíció:**  
A kiegyensúlyozott keresőfák célja a magasság kordában tartása.

**Működési elv:**  
- **[[AVL-fa]]**: szigorúbb egyensúlyfeltételek, rotációk.  
- **[[piros-fekete fa]]**: lazább egyensúly, színezési szabályok.  
- Mindkettő garantál közel logaritmikus műveleti időt.

**Egyszerű példa:**  
Nagy, dinamikusan változó kulcshalmaznál ezek megbízhatóbbak, mint a sima BST.

**Vizsgán fontos kulcsszavak:**  
**[[AVL-fa]]**, **[[piros-fekete fa]]**, **rotáció**, **kiegyensúlyozás**

---

## 3. Hasító táblázatok (Hash table)

### 3.1 Alapfogalmak
**Rövid definíció:**  
A **[[hash tábla]]** kulcsokat egy hash függvénnyel tömbindexre képez.

**Működési elv:**  
- **[[hash függvény]]**: kulcs -> index.  
- Cél az egyenletes eloszlás, hogy kevés ütközés legyen.  
- Keresés/beszúrás átlagban nagyon gyors lehet.

**Egyszerű példa:**  
Felhasználónév -> hash -> index, ahol a felhasználó rekordja tárolódik.

**Vizsgán fontos kulcsszavak:**  
**[[hash tábla]]**, **[[hash függvény]]**, **kulcs-index leképezés**, **egyenletes eloszlás**

---

### 3.2 Ütközéskezelés
**Rövid definíció:**  
Ütközés akkor van, ha több kulcs ugyanarra az indexre kerül.

**Működési elv:**  
- **[[chaining]]**: indexenként lista/kollekció tárolja az elemeket.  
- **Nyílt címzés**: új helyet keresünk a táblában:  
  - lineáris próba,  
  - kvadratikus próba,  
  - dupla hash.

**Egyszerű példa:**  
Ha egy index foglalt, lineáris próbánál a következő szabad helyet keressük.

**Vizsgán fontos kulcsszavak:**  
**ütközéskezelés**, **[[chaining]]**, **nyílt címzés**, **lineáris próba**, **dupla hash**

---

### 3.3 Műveletek
**Rövid definíció:**  
A hash táblán három alapművelet van: beszúrás, keresés, törlés.

**Működési elv:**  
- Hash index számítása után az ütközéskezelési szabály szerint lépünk.  
- Törlés nyílt címzésnél óvatosabb, mert a próbaláncot nem törhetjük meg rosszul.

**Egyszerű példa:**  
Egy szó gyakoriságát számláló program hash táblában tárolja a szó -> darabszám párokat.

**Vizsgán fontos kulcsszavak:**  
**beszúrás**, **keresés**, **törlés**, **próbalánc**, **hash index**

---

### 3.4 Tulajdonságok
**Rövid definíció:**  
A hash tábla teljesítményét főleg a **terhelési tényező** befolyásolja.

**Működési elv:**  
- Átlagos idő sokszor O(1), legrosszabb eset O(n).  
- **[[load factor]]** = elemek száma / tábla mérete.  
- Ha túl nagy, ütközés nő -> **[[rehashing]]** szükséges.

**Egyszerű példa:**  
Ha a tábla megtelik, nagyobb táblába helyezzük át az elemeket újrahasheléssel.

**Vizsgán fontos kulcsszavak:**  
**O(1) átlagos idő**, **O(n) legrosszabb eset**, **[[load factor]]**, **[[rehashing]]**

---

## 4. Fák és gráfok számítógépes reprezentációja

### 4.1 Fa reprezentációk
**Rövid definíció:**  
A fa többféleképpen tárolható, a választás a fa típusától és műveletektől függ.

**Működési elv:**  
- **Tömbös reprezentáció**: teljes/közel teljes fáknál jó (pl. **[[kupac]]**).  
- **Láncolt reprezentáció**: csomópont + pointerek, rugalmas.  
- **Gyereklista**: általános fákhoz praktikus.

**Egyszerű példa:**  
Bináris kupacnál tömbben a gyerekindexek egyszerűen számolhatók (`2i+1`, `2i+2`).

**Vizsgán fontos kulcsszavak:**  
**fa reprezentáció**, **tömbös tárolás**, **láncolt tárolás**, **gyereklista**, **[[kupac]]**

---

### 4.2 Gráf reprezentációk

#### Szomszédsági mátrix
**Rövid definíció:**  
A **[[szomszédsági mátrix]]** egy n x n tábla, ahol az `i,j` elem jelzi az él létezését/súlyát.

**Működési elv:**  
- Él lekérdezése O(1).  
- Memóriaigény O(n²), ezért ritka gráfnál pazarló lehet.

**Egyszerű példa:**  
Sűrű gráfban, ahol sok él van, a mátrix kényelmes és gyors éltesztet ad.

**Vizsgán fontos kulcsszavak:**  
**[[szomszédsági mátrix]]**, **O(1) éllekérdezés**, **O(n²) memória**

#### Szomszédsági lista
**Rövid definíció:**  
A **[[szomszédsági lista]]** minden csúcshoz a kimenő szomszédok listáját tárolja.

**Működési elv:**  
- Memória tipikusan O(V+E).  
- Ritka gráfoknál sokkal hatékonyabb tárolás.  
- Bejárásoknál (BFS/DFS) természetes reprezentáció.

**Egyszerű példa:**  
Közösségi hálónál, ahol csúcsonként kevés kapcsolat van, lista jobb választás.

**Vizsgán fontos kulcsszavak:**  
**[[szomszédsági lista]]**, **O(V+E)**, **ritka gráf**, **élbejárás**

---

### 4.3 Összehasonlítás
**Rövid definíció:**  
A mátrix és lista között memória-sebesség kompromisszum van.

**Működési elv:**  
- **Sűrű gráf**: mátrix gyakran előnyös.  
- **Ritka gráf**: lista általában jobb.  
- A választás függ a műveletektől: sok élteszt vagy sok bejárás.

**Egyszerű példa:**  
Ha gyakran kérdezzük „van-e él i és j között?”, mátrix praktikusabb.

**Vizsgán fontos kulcsszavak:**  
**sűrű gráf**, **ritka gráf**, **trade-off**, **memória vs sebesség**

---

### 4.4 Speciális reprezentációk (csak említés)
**Rövid definíció:**  
Vannak ritkábban használt, speciális feladathoz illeszkedő tárolások is.

**Működési elv:**  
- **[[él lista]]**: élek egyszerű felsorolása, algoritmusfüggően hasznos.  
- **[[incidenciamátrix]]**: csúcs-él kapcsolatokat mátrixban tárolja.

**Egyszerű példa:**  
Kruskal algoritmusnál él-lista reprezentáció kényelmes lehet élrendezéshez.

**Vizsgán fontos kulcsszavak:**  
**[[él lista]]**, **[[incidenciamátrix]]**, **speciális reprezentáció**

---

## + Vizsgán érdemes még megemlíteni
- A **pointer** alapvető a láncolt struktúrákban.  
- Dinamikus memóriahasználatnál fontos a felszabadítás és hibakezelés.  
- **Cache/locality**: tömb általában cache-barátabb, lista rugalmasabb.  
- Gyakorlati példák: adatbázis indexelés, útvonaltervezés, keresőrendszerek.

---

## Rövid szóbeli összefoglaló
Az adatszerkezet-választás alapvetően meghatározza az algoritmus teljesítményét. ADT szinten a műveleteket nézzük, implementáció szinten pedig az idő- és tárigényt. A tömb gyors indexelést ad, a láncolt lista rugalmas beszúrást-törlést. A verem LIFO, a sor FIFO elvű. A bináris keresőfa keresést, beszúrást, törlést támogat, de hatékonysága a fa magasságától függ, ezért fontosak a kiegyensúlyozott fák. A hash tábla átlagban O(1) műveletet ad jó hash függvénnyel és megfelelő terhelési tényezővel. Fák és gráfok tárolásánál a reprezentációt a feladat alapján választjuk: mátrix sűrű gráfra, lista ritkára előnyös.

## Kulcsfogalmak
- [[absztrakt adattípus]]
- [[tömb]]
- [[láncolt lista]]
- [[verem]]
- [[sor]]
- [[bináris keresőfa]]
- [[inorder]]
- [[AVL-fa]]
- [[hash tábla]]
- [[hash függvény]]
- [[load factor]]
- [[rehashing]]
- [[szomszédsági mátrix]]
- [[szomszédsági lista]]
- [[incidenciamátrix]]

## Tipikus vizsgakérdések
1. **Mi a különbség ADT és implementáció között?**  
   ADT a műveleteket írja le, implementáció a konkrét belső megvalósítást.

2. **Mikor jobb a tömb, és mikor a láncolt lista?**  
   Tömb gyors indexeléshez, lista sok dinamikus beszúrás/törléshez jobb.

3. **Miért romolhat le a BST teljesítménye O(n)-re?**  
   Ha a fa kiegyensúlyozatlan és láncszerűvé válik.

4. **Hogyan kezeljük a hash ütközéseket?**  
   Chaininggel vagy nyílt címzéssel (lineáris, kvadratikus, dupla hash).

5. **Mit jelent a load factor, és miért fontos?**  
   Telítettséget mér; nagy értéknél több ütközés várható, rehash kellhet.

6. **Mikor válasszunk szomszédsági mátrixot?**  
   Sűrű gráfnál és gyakori éllekérdezésnél.

7. **Mikor jobb a szomszédsági lista?**  
   Ritka gráfnál és bejárás-központú feladatoknál.

## Minimum, amit tudni kell
- ADT és implementáció fogalmi különbsége.  
- Tömb és láncolt lista fő előnye-hátránya.  
- Verem (LIFO) és sor (FIFO) alapműveletei.  
- BST szabály: bal < gyökér < jobb, és az alapműveletek menete.  
- BST-nél a magasság határozza meg a futási időt.  
- Hash tábla átlagos O(1) ideje és ütközéskezelési módjai.  
- Load factor és rehashing jelentése.  
- Gráf reprezentációk közti választás: mátrix vs lista.
