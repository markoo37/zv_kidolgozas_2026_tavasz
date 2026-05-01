# Programozás alapjai – 17. tétel
## Algoritmusok vezérlési szerkezetei C nyelven

---

## 1. Alapfogalmak
**Rövid definíció:**  
Az **[[algoritmus]]** véges, egyértelmű lépéssor egy feladat megoldására. A vezérlési szerkezet azt határozza meg, milyen sorrendben futnak ezek a lépések.

**Működési elv:**  
- Strukturált programozásban három fő vezérlés van: szekvenciális, elágazásos, iterációs.  
- Cél az átlátható, hibamentes programlogika.

**Egyszerű példa:**  
Egy szám feldolgozása: beolvasás -> feltételvizsgálat -> ismétléses számítás.

**Vizsgán fontos kulcsszavak:**  
**[[algoritmus]]**, **vezérlési szerkezet**, **strukturált programozás**, **szekvenciális/elágazásos/iterációs**

---

## 2. Szekvenciális vezérlés
**Rövid definíció:**  
A **[[szekvenciális vezérlés]]** az utasítások egymás utáni, sorban történő végrehajtása.

**Működési elv:**  
- Ez a C program alapértelmezett működése.  
- Nincs ugrás vagy ismétlés, a kódlineárisan halad.

**Egyszerű példa:**  
`x = 5; printf("%d", x);` — előbb értékadás, aztán kiírás.

**Vizsgán fontos kulcsszavak:**  
**[[szekvenciális vezérlés]]**, **lineáris végrehajtás**, **alapértelmezett futás**

---

## 3. Elágazásos vezérlés

### 3.1 if
**Rövid definíció:**  
Az `if` egy feltételes utasítás, amely csak igaz feltétel esetén futtat blokkot.

**Működési elv:**  
- Logikai kifejezést értékel (`igaz`/`hamis`).  
- Igaz esetben belép az `if` blokkba.

**Egyszerű példa:**  
`if (x > 0) printf("pozitiv");`

**Vizsgán fontos kulcsszavak:**  
**if**, **feltételvizsgálat**, **logikai kifejezés**

### 3.2 if–else
**Rövid definíció:**  
Az `if-else` kétirányú döntést valósít meg.

**Működési elv:**  
- Igaz feltételnél az `if`, különben az `else` ág fut.

**Egyszerű példa:**  
`if (x%2==0) printf("paros"); else printf("paratlan");`

**Vizsgán fontos kulcsszavak:**  
**if-else**, **kétirányú elágazás**, **igaz/hamis ág**

### 3.3 else if lánc
**Rövid definíció:**  
Az `else if` lánc több feltétel egymás utáni ellenőrzésére szolgál.

**Működési elv:**  
- Fentről lefelé vizsgál, az első igaz ág fut le.  
- Sorrend és prioritás fontos.

**Egyszerű példa:**  
Jegybesorolás pontszám alapján több tartományra bontva.

**Vizsgán fontos kulcsszavak:**  
**else if**, **többfeltételes döntés**, **prioritási sorrend**

### 3.4 switch
**Rövid definíció:**  
A `switch` többirányú elágazás diszkrét értékekre.

**Működési elv:**  
- `case` ágakat vizsgál, `break` zárja az ágat.  
- `default` az alapértelmezett eset.

**Egyszerű példa:**  
Menüpont választás `switch(menuPont)` alapján.

**Vizsgán fontos kulcsszavak:**  
**switch**, **case**, **break**, **default**, **diszkrét érték**

---

## 4. Iterációs vezérlés

### 4.1 while
**Rövid definíció:**  
A `while` elöltesztelő ciklus: feltételvizsgálat után indul a ciklusmag.

**Működési elv:**  
- Ha feltétel hamis, egyszer sem fut le.  
- Ismétlődő feladatokra alkalmas, amíg feltétel igaz.

**Egyszerű példa:**  
`while (x > 0) { x--; }`

**Vizsgán fontos kulcsszavak:**  
**while**, **elöltesztelő ciklus**, **feltételes ismétlés**

### 4.2 do–while
**Rövid definíció:**  
A `do-while` hátultesztelő ciklus, ezért legalább egyszer végrehajtódik.

**Működési elv:**  
- Ciklusmag fut, utána történik feltételvizsgálat.

**Egyszerű példa:**  
Menü kiírása és újra-kérdezése legalább egyszer.

**Vizsgán fontos kulcsszavak:**  
**do-while**, **hátultesztelő**, **legalább egyszer lefut**

### 4.3 for
**Rövid definíció:**  
A `for` számlálós ciklus, tipikusan ismert ismétlésszám esetén.

**Működési elv:**  
- Három része: inicializálás, feltétel, léptetés.  
- Kompakt és jól olvasható ciklusforma.

**Egyszerű példa:**  
`for (int i=0; i<n; i++) osszeg += a[i];`

**Vizsgán fontos kulcsszavak:**  
**for**, **számlálós ciklus**, **inicializálás-feltétel-léptetés**

---

## 5. Vezérlés módosítása
**Rövid definíció:**  
Ezek az utasítások módosítják a normál ciklus- vagy függvényfutást.

**Működési elv:**  
- `break`: ciklus/switch azonnali megszakítása.  
- `continue`: aktuális iteráció kihagyása, következőre lépés.  
- `return`: kilépés a függvényből (opcionális visszatérési értékkel).

**Egyszerű példa:**  
Kereséskor `break`, ha megtaláltuk az elemet.

**Vizsgán fontos kulcsszavak:**  
**break**, **continue**, **return**, **vezérlés megszakítása**

---

## 6. Eljárás vezérlés (függvények)

### 6.1 Alapfogalmak
**Rövid definíció:**  
A **[[függvény]]** önálló, újrafelhasználható programrész, amely paraméterekkel hívható.

**Működési elv:**  
- Deklaráció (prototípus) írja le az aláírást.  
- Definíció tartalmazza a megvalósítást.  
- Híváskor vezérlés átadódik, majd visszatér.

**Egyszerű példa:**  
`int max(int a, int b);` prototípus alapján hívható a függvény.

**Vizsgán fontos kulcsszavak:**  
**[[függvény]]**, **prototípus**, **hívás**, **visszatérési érték**

---

### 6.2 Paraméterátadás
**Rövid definíció:**  
C nyelvben alapból érték szerinti paraméterátadás van.

**Működési elv:**  
- `call by value`: másolatot kap a függvény.  
- Ha hívó oldali változót akarunk módosítani, pointert adunk át.

**Egyszerű példa:**  
`void novel(int *p){ (*p)++; }` ténylegesen módosítja a hívó változóját.

**Vizsgán fontos kulcsszavak:**  
**érték szerinti átadás**, **pointer paraméter**, **cím szerinti hatás**

---

### 6.3 Rekurzió
**Rövid definíció:**  
A **[[rekurzió]]** olyan technika, amikor a függvény önmagát hívja.

**Működési elv:**  
- Kell báziseset (megállási feltétel).  
- Kell rekurzív lépés (probléma csökkentése).  
- A hívások veremben tárolódnak.

**Egyszerű példa:**  
Faktoriális: `n! = n * (n-1)!`, bázis: `0! = 1`.

**Vizsgán fontos kulcsszavak:**  
**[[rekurzió]]**, **báziseset**, **rekurzív lépés**, **hívási verem**

---

## + Vizsgán érdemes még megemlíteni
- `while` vs `for`: feltételes ismétlés vs számlálós forma.  
- `switch` vs `if`: diszkrét értékeknél switch gyakran áttekinthetőbb.  
- Végtelen ciklusok tipikus hibaforrásai (rossz feltétel/léptetés).  
- Rekurzió vs iteráció: olvashatóság vs veremköltség.  
- Gyakorlati minta: beolvasás-feldolgozás-kiírás ciklusokkal.

---

## Rövid szóbeli összefoglaló
A C nyelv vezérlési szerkezetei a strukturált programozás alapját adják. Alapesetben a program szekvenciálisan fut, de elágazásokkal döntési pontokat hozunk létre, ciklusokkal pedig ismétlünk. Az `if`, `if-else`, `else if` és `switch` különböző döntési helyzetekre használható. Iterációra `while`, `do-while` és `for` áll rendelkezésre, eltérő tesztelési és használati mintával. A `break`, `continue`, `return` módosítja a futás menetét. Függvényekkel a program moduláris lesz, paraméterátadásnál C-ben alapból érték szerinti átadás van, pointerrel lehet hívói adatot módosítani. Rekurzió is használható, de mindig kell báziseset.

## Kulcsfogalmak
- [[algoritmus]]
- [[strukturált programozás]]
- [[szekvenciális vezérlés]]
- [[if]]
- [[switch]]
- [[while]]
- [[do-while]]
- [[for]]
- [[break]]
- [[continue]]
- [[return]]
- [[függvény]]
- [[prototípus]]
- [[érték szerinti átadás]]
- [[rekurzió]]

## Tipikus vizsgakérdések
1. **Melyek a strukturált vezérlés fő típusai?**  
   Szekvenciális, elágazásos és iterációs.

2. **Mi a különbség while és do-while között?**  
   While elöltesztelő, do-while hátultesztelő, ezért utóbbi legalább egyszer fut.

3. **Mikor célszerű switch-et használni if helyett?**  
   Diszkrét, többágú választásnál gyakran áttekinthetőbb.

4. **Mi a for ciklus három része?**  
   Inicializálás, feltétel, léptetés.

5. **Mit csinál a break és a continue?**  
   Break megszakít, continue a következő iterációra ugrik.

6. **Hogyan működik C-ben a paraméterátadás?**  
   Alapból érték szerint, pointerrel érhető el cím szerinti hatás.

7. **Mik a rekurzió kötelező elemei?**  
   Báziseset és rekurzív lépés.

## Minimum, amit tudni kell
- Algoritmus és vezérlési szerkezet fogalma.  
- Szekvenciális vezérlés lényege.  
- if/if-else/else-if/switch alapkülönbség.  
- while, do-while, for használati mintái.  
- break, continue, return szerepe.  
- Függvény deklaráció és definíció különbsége.  
- Érték szerinti paraméterátadás C-ben.  
- Rekurzió alapötlete és báziseset fontossága.
