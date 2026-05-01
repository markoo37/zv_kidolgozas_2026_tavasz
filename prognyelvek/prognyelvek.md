# Programozási nyelvek – 22. tétel
## Programozási nyelvek csoportosítása (paradigmák)

---

## 1. Alapfogalmak

### 1.1 Programozási nyelv
**Rövid definíció:**  
A **[[programozási nyelv]]** formális nyelv, amellyel algoritmusokat és programokat írunk.

**Működési elv:**  
- Van **[[szintaxis]]**: hogyan kell helyesen leírni a kódot.  
- Van **[[szemantika]]**: mit jelent és mit csinál a kód.  
- A fordító vagy értelmező ezt hajtja végre gépi szinten.

**Egyszerű példa:**  
`if` szerkezet szintaxisa nyelvenként eltér, de szemantikailag mindenhol feltételes végrehajtást jelent.

**Vizsgán fontos kulcsszavak:**  
**[[programozási nyelv]]**, **[[szintaxis]]**, **[[szemantika]]**, **fordítás**, **végrehajtás**

---

### 1.2 Paradigma
**Rövid definíció:**  
A **[[paradigma]]** egy programozási szemlélet vagy problémamegoldási modell.

**Működési elv:**  
- Meghatározza, hogyan gondolkodunk a program felépítéséről.  
- Ugyanaz a feladat több paradigmában is megoldható.  
- A nyelvek gyakran több paradigmát is támogatnak.

**Egyszerű példa:**  
Egy lista feldolgozható ciklussal (imperatív) vagy `map/filter` függvényekkel (funkcionális).

**Vizsgán fontos kulcsszavak:**  
**[[paradigma]]**, **programozási szemlélet**, **problémamegoldási modell**, **többparadigmás nyelv**

---

## 2. Imperatív paradigma

### 2.1 Jellemzők
**Rövid definíció:**  
Az **[[imperatív programozás]]** lépésről lépésre megadja, hogyan oldjuk meg a feladatot.

**Működési elv:**  
- A program utasítások sorozata.  
- Központi szerepű az **állapotváltozás** és a változók módosítása.  
- Gyakori elemek: ciklusok, elágazások, értékadások.

**Egyszerű példa:**  
Összegzésnél `sum = 0`, majd ciklusban hozzáadjuk az elemeket.

**Vizsgán fontos kulcsszavak:**  
**[[imperatív programozás]]**, **utasítássorozat**, **állapotváltozás**, **változó**

---

### 2.2 Típusai
**Rövid definíció:**  
Az imperatív paradigma egyik fő típusa a **[[procedurális programozás]]**.

**Működési elv:**  
- A programot eljárásokra/függvényekre bontjuk.  
- Modulárisabb, mint az egyetlen nagy főprogram.  
- Újrafelhasználhatóbb kódszerkezetet ad.

**Egyszerű példa:**  
Külön `beolvas()`, `feldolgoz()`, `kiir()` eljárásokra bontjuk a feladatot.

**Vizsgán fontos kulcsszavak:**  
**[[procedurális programozás]]**, **eljárás**, **modularitás**, **imperatív altípus**

---

### 2.3 Példák
**Rövid definíció:**  
Klasszikus imperatív/procedurális nyelvek például a C és Pascal.

**Működési elv:**  
- A hangsúly a vezérlési szerkezeteken és memória közeli működésen van.  
- Jól szemléltetik az állapotváltozásra épülő gondolkodást.

**Egyszerű példa:**  
Tömb rendezése C nyelven ciklusokkal és változócserével történik.

**Vizsgán fontos kulcsszavak:**  
**C**, **Pascal**, **imperatív példa**, **eljárásalapú felépítés**

---

## 3. Objektumorientált paradigma (OOP)

### 3.1 Alapfogalmak
**Rövid definíció:**  
Az **[[objektumorientált programozás]]** (OOP) adatok és műveletek egységbe szervezésére épít.

**Működési elv:**  
- **[[osztály]]**: sablon, ami leírja az objektum szerkezetét/viselkedését.  
- **[[objektum]]**: az osztály konkrét példánya.  
- **[[metódus]]**: az objektumhoz tartozó művelet.

**Egyszerű példa:**  
`Auto` osztályból több objektum készülhet (pl. pirosAuto, feketeAuto), mindegyik saját állapottal.

**Vizsgán fontos kulcsszavak:**  
**[[objektumorientált programozás]]**, **[[osztály]]**, **[[objektum]]**, **[[metódus]]**

---

### 3.2 Fő elvek
**Rövid definíció:**  
Az OOP négy klasszikus alappillére az egységbe zárás, öröklődés, polimorfizmus és absztrakció.

**Működési elv:**  
- **[[encapsulation]]**: adat és működés egyben, belső részletek elrejtése.  
- **[[öröklődés]]**: közös tulajdonságok átvétele ősosztályból.  
- **[[polimorfizmus]]**: azonos interfész mögött eltérő megvalósítás.  
- **[[absztrakció]]**: lényeges tulajdonságokra koncentrálás.

**Egyszerű példa:**  
`Jarmu` ősosztályból `Auto` és `Motor` származhat, mindkettő saját `indul()` metódussal.

**Vizsgán fontos kulcsszavak:**  
**[[encapsulation]]**, **[[öröklődés]]**, **[[polimorfizmus]]**, **[[absztrakció]]**

---

### 3.3 Példák
**Rövid definíció:**  
Tipikus OOP nyelvek: Java, C++, C#.

**Működési elv:**  
- Mind támogatja az osztályalapú tervezést.  
- Erős eszköztárat ad nagy rendszerek strukturálásához.

**Egyszerű példa:**  
Asztali alkalmazásnál GUI-elemeket objektumokkal modellezünk (ablak, gomb, eseménykezelő).

**Vizsgán fontos kulcsszavak:**  
**Java**, **C++**, **C#**, **osztályalapú tervezés**

---

## 4. Funkcionális paradigma

### 4.1 Jellemzők
**Rövid definíció:**  
A **[[funkcionális programozás]]** középpontjában a függvények állnak, minimális állapotváltozással.

**Működési elv:**  
- Előnyben részesíti az immutable adatkezelést.  
- Törekszik **[[mellékhatás]]**-mentes függvényekre.  
- Könnyebb lehet tesztelni és párhuzamosítani.

**Egyszerű példa:**  
Lista elemeit új listává alakítjuk `map` segítségével anélkül, hogy az eredetit módosítanánk.

**Vizsgán fontos kulcsszavak:**  
**[[funkcionális programozás]]**, **függvényközpontúság**, **immutabilitás**, **[[mellékhatás]]**

---

### 4.2 Fogalmak
**Rövid definíció:**  
A funkcionális paradigma kulcsfogalmai a tiszta függvény, rekurzió és magasabb rendű függvény.

**Működési elv:**  
- **[[tiszta függvény]]**: ugyanarra a bemenetre ugyanaz a kimenet, nincs külső mellékhatás.  
- **[[rekurzió]]**: önhívásos problémafelbontás ciklus helyett.  
- **[[magasabb rendű függvény]]**: függvényt kap paraméterként vagy visszaad függvényt.

**Egyszerű példa:**  
`filter(paros, lista)` egy függvényt kap és az alapján szűr.

**Vizsgán fontos kulcsszavak:**  
**[[tiszta függvény]]**, **[[rekurzió]]**, **[[magasabb rendű függvény]]**, **immutable adatok**

---

### 4.3 Példák
**Rövid definíció:**  
Erősen funkcionális nyelv a Haskell és Lisp, míg Scala többparadigmás, funkcionális elemekkel.

**Működési elv:**  
- Haskell közel tisztán funkcionális.  
- Lisp család nagy rugalmasságot ad függvénykezelésben.  
- Scala ötvözi az OOP és funkcionális eszközöket.

**Egyszerű példa:**  
Scalában osztályokat és `map/filter/reduce` stílust egyszerre használhatunk.

**Vizsgán fontos kulcsszavak:**  
**Haskell**, **Lisp**, **Scala**, **többparadigmás megközelítés**

---

## 5. Logikai paradigma

### 5.1 Jellemzők
**Rövid definíció:**  
A **[[logikai programozás]]** deklaratív megközelítés, ahol tényekből és szabályokból következtetünk.

**Működési elv:**  
- A program leírja az összefüggéseket, nem a részletes végrehajtási lépéseket.  
- A motor lekérdezésekből logikai következtetést végez.  
- Gyakori terület: tudásreprezentáció, expert rendszerek.

**Egyszerű példa:**  
Ha tény: `szulo(anna,bela)` és szabály: „ha szülő, akkor rokon”, akkor a rendszer kikövetkezteti a rokonságot.

**Vizsgán fontos kulcsszavak:**  
**[[logikai programozás]]**, **tény**, **szabály**, **következtetés**, **deklaratív**

---

### 5.2 Példák
**Rövid definíció:**  
A logikai paradigma legismertebb nyelve a Prolog.

**Működési elv:**  
- Tények és szabályok deklarálása után lekérdezések futtathatók.  
- A rendszer backtrackinggel keres megoldást.

**Egyszerű példa:**  
Prologban családfa-kapcsolatok lekérdezése néhány tény és szabály alapján.

**Vizsgán fontos kulcsszavak:**  
**Prolog**, **backtracking**, **logikai lekérdezés**

---

## 6. Deklaratív paradigma

### 6.1 Jellemzők
**Rövid definíció:**  
A **[[deklaratív programozás]]** azt írja le, mit akarunk, nem azt, hogyan számoljuk ki lépésről lépésre.

**Működési elv:**  
- Magasabb absztrakciós szint.  
- A végrehajtási stratégia nagy részét a rendszer kezeli.  
- Rövidebb, kifejezőbb leírásokat adhat.

**Egyszerű példa:**  
SQL-ben lekérdezésnél megadjuk, milyen adat kell, az optimalizálást az adatbázis végzi.

**Vizsgán fontos kulcsszavak:**  
**[[deklaratív programozás]]**, **mit vs hogyan**, **absztrakció**, **lekérdezés**

---

### 6.2 Példák
**Rövid definíció:**  
Deklaratív jellegű nyelvek például az SQL és részben a HTML.

**Működési elv:**  
- **[[SQL]]**: adatbázis lekérdezés deklaratívan.  
- **[[HTML]]**: dokumentum szerkezetének leírása (nem algoritmus).

**Egyszerű példa:**  
`SELECT nev FROM hallgatok WHERE atlag > 4.0` megadja a kívánt eredményt, nem az iterálási lépéseket.

**Vizsgán fontos kulcsszavak:**  
**[[SQL]]**, **[[HTML]]**, **deklaratív leírás**, **magas absztrakció**

---

## 7. Egyéb csoportosítások (említés)

### 7.1 Fordítás módja szerint
**Rövid definíció:**  
A nyelvek csoportosíthatók aszerint is, hogyan jutnak futtatható állapotba.

**Működési elv:**  
- **[[fordított nyelv]]**: előre gépi/bytekód készül (compiler).  
- **[[értelmezett nyelv]]**: futás közben interpreter dolgozza fel.  
- Gyakorlatban gyakran kevert modellek vannak.

**Egyszerű példa:**  
Java forrásból bytekód készül, amit JVM futtat.

**Vizsgán fontos kulcsszavak:**  
**compiler**, **interpreter**, **fordítás**, **végrehajtási modell**

---

### 7.2 Típusosság szerint
**Rövid definíció:**  
A nyelvek típuskezelés szerint lehetnek statikusak vagy dinamikusak.

**Működési elv:**  
- **[[statikus típusosság]]**: típusellenőrzés főleg fordításkor.  
- **[[dinamikus típusosság]]**: típusellenőrzés futásidőben hangsúlyosabb.  
- Mindkettőnek vannak előnyei: biztonság vs rugalmasság.

**Egyszerű példa:**  
Statikus nyelvben sok hiba már fordításkor kiderül, dinamikusnál gyorsabb prototípus készülhet.

**Vizsgán fontos kulcsszavak:**  
**[[statikus típusosság]]**, **[[dinamikus típusosság]]**, **fordítási hiba**, **futásidejű hiba**

---

## 8. Összehasonlítás

**Rövid definíció:**  
A paradigmák közti fő különbség az állapotkezelésben és a probléma leírásának módjában van.

**Működési elv:**  
- **Imperatív vs deklaratív**: hogyan csináld vs mit szeretnél.  
- **OOP vs funkcionális**: objektum-állapot központú vs függvény/immutabilitás központú.  
- Gyakorlatban gyakran kombináljuk a megközelítéseket.

**Egyszerű példa:**  
Ugyanazt a listafeldolgozást írhatjuk for-ciklussal (imperatív) vagy `map/filter` lánccal (funkcionális/deklaratívabb).

**Vizsgán fontos kulcsszavak:**  
**imperatív vs deklaratív**, **OOP vs funkcionális**, **állapotkezelés**, **paradigmák kombinálása**

---

## + Vizsgán érdemes még megemlíteni
- **[[többparadigmás nyelv]]** fogalma (pl. Python, C++, Scala).  
- Valós projektekben ritkán használunk csak egyetlen paradigmát.  
- A választást befolyásolja: csapat, domén, teljesítmény, karbantarthatóság.  
- Minden paradigma kompromisszum: egyszerűség, rugalmasság, hibalehetőség másképp alakul.

---

## Rövid szóbeli összefoglaló
A programozási nyelveket gyakran paradigmák szerint csoportosítjuk, ami a problémamegoldási szemléletet jelenti. Az imperatív paradigma utasítások és állapotváltozás alapján működik, míg a deklaratív inkább azt írja le, mit szeretnénk elérni. Az objektumorientált megközelítés osztályokra és objektumokra épít, fő elvei az egységbe zárás, öröklődés, polimorfizmus és absztrakció. A funkcionális paradigma függvényközpontú, igyekszik mellékhatásmentes lenni, és sokszor rekurziót, magasabb rendű függvényeket használ. A logikai paradigma szabályokból és tényekből következtet. A modern nyelvek többsége többparadigmás, ezért a gyakorlatban ezeket a szemléleteket kombináljuk.

## Kulcsfogalmak
- [[programozási nyelv]]
- [[szintaxis]]
- [[szemantika]]
- [[paradigma]]
- [[imperatív programozás]]
- [[objektumorientált programozás]]
- [[encapsulation]]
- [[öröklődés]]
- [[polimorfizmus]]
- [[funkcionális programozás]]
- [[tiszta függvény]]
- [[logikai programozás]]
- [[deklaratív programozás]]
- [[statikus típusosság]]
- [[dinamikus típusosság]]

## Tipikus vizsgakérdések
1. **Mi a különbség szintaxis és szemantika között?**  
   Szintaxis a helyes forma, szemantika a jelentés és működés.

2. **Mit jelent a paradigma a programozásban?**  
   Egy problémamegoldási szemlélet, amely meghatározza a program szerkezetét.

3. **Mi az imperatív és deklaratív paradigma fő különbsége?**  
   Imperatív: hogyan hajtsuk végre; deklaratív: mit szeretnénk elérni.

4. **Melyek az OOP fő alapelvei?**  
   Encapsulation, öröklődés, polimorfizmus, absztrakció.

5. **Mit nevezünk tiszta függvénynek?**  
   Olyan függvényt, amely ugyanarra a bemenetre ugyanazt adja, mellékhatás nélkül.

6. **Miben más a statikus és dinamikus típusosság?**  
   Statikusnál sok ellenőrzés fordításkor, dinamikusnál főleg futásidőben történik.

7. **Miért fontosak a többparadigmás nyelvek?**  
   Mert feladattól függően különböző paradigmák előnyeit tudjuk kombinálni.

## Minimum, amit tudni kell
- Programozási nyelv, szintaxis, szemantika fogalma.  
- Paradigma jelentése és szerepe.  
- Imperatív paradigma lényege (utasítás + állapotváltozás).  
- OOP alapfogalmak és a 4 fő elv.  
- Funkcionális paradigma alapjai (tiszta függvény, rekurzió, mellékhatásmentesség).  
- Logikai és deklaratív szemlélet rövid lényege.  
- Fordított vs értelmezett és statikus vs dinamikus típusosság alapkülönbsége.  
- Többparadigmás nyelvek gyakorlati jelentősége.
