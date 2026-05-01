# Rendszerfejlesztés I. – 23. tétel
## Szoftverfejlesztési folyamat és modellek

---

## 1. Szoftverfejlesztési folyamat

### 1.1 Fogalom
**Rövid definíció:**  
A **[[szoftverfejlesztési folyamat]]** olyan tevékenységek rendezett sorozata, amelynek célja egy működő, fenntartható szoftver létrehozása.

**Működési elv:**  
- Nem csak kódolásból áll, hanem tervezésből, tesztelésből és karbantartásból is.  
- A folyamat segít abban, hogy a fejlesztés tervezhető és ellenőrizhető legyen.  
- Cél a minőség, határidő és költség egyensúlya.

**Egyszerű példa:**  
Egy webshop fejlesztésénél először igényeket gyűjtünk, majd tervezünk, fejlesztünk, tesztelünk, és csak ezután adunk át.

**Vizsgán fontos kulcsszavak:**  
**[[szoftverfejlesztési folyamat]]**, **életciklus**, **minőség**, **határidő**, **költség**

---

### 1.2 Fő lépések

#### Követelményanalízis
**Rövid definíció:**  
A követelményanalízisben rögzítjük, mit kell tudnia a rendszernek.

**Működési elv:**  
- Felhasználói igények felmérése interjúval, workshopokkal, kérdőívvel.  
- **[[funkcionális követelmény]]**: mit csináljon a rendszer.  
- **[[nem funkcionális követelmény]]**: hogyan csinálja (pl. teljesítmény, biztonság).

**Egyszerű példa:**  
Funkcionális követelmény: „lehessen rendelést leadni”. Nem funkcionális: „2 másodpercen belül töltődjön be az oldal”.

**Vizsgán fontos kulcsszavak:**  
**követelményanalízis**, **[[funkcionális követelmény]]**, **[[nem funkcionális követelmény]]**, **igényfelmérés**

---

#### Tervezés (design)
**Rövid definíció:**  
A tervezés során meghatározzuk a rendszer felépítését és belső szerkezetét.

**Működési elv:**  
- Architektúra kiválasztása (pl. réteges, mikroszolgáltatás).  
- Komponensek, interfészek, adatmodellek meghatározása.  
- Cél a bővíthető és karbantartható megoldás.

**Egyszerű példa:**  
Egy webalkalmazásnál külön frontend, backend és adatbázis réteg készül.

**Vizsgán fontos kulcsszavak:**  
**[[tervezés]]**, **[[architektúra]]**, **komponens**, **interfész**, **adatmodell**

---

#### Implementáció
**Rövid definíció:**  
Az implementáció a tervek alapján történő kódolás és modulfejlesztés.

**Működési elv:**  
- Fejlesztők modulonként dolgoznak.  
- Verziókezeléssel (pl. **[[Git]]**) koordinálják a változásokat.  
- Kódellenőrzés és szabványok segítik az egységes minőséget.

**Egyszerű példa:**  
Külön fejlesztő készíti a bejelentkezést, másik a rendeléskezelést, majd ezek integrálódnak.

**Vizsgán fontos kulcsszavak:**  
**implementáció**, **modul**, **[[Git]]**, **kódreview**, **kódolási szabvány**

---

#### Tesztelés
**Rövid definíció:**  
A tesztelés célja a hibák korai felismerése és a követelmények teljesülésének ellenőrzése.

**Működési elv:**  
- **[[egységteszt]]**: kis komponensek külön vizsgálata.  
- **[[integrációs teszt]]**: modulok együttműködése.  
- **[[rendszerteszt]]**: teljes rendszer viselkedése.  
- Ideális esetben folyamatos automatizált tesztfutás történik.

**Egyszerű példa:**  
Egy rendelés funkció lehet egységszinten jó, de integrációban hibázhat, ha az adatbázis-kapcsolat rossz.

**Vizsgán fontos kulcsszavak:**  
**tesztelés**, **[[egységteszt]]**, **[[integrációs teszt]]**, **[[rendszerteszt]]**, **hibafelderítés**

---

#### Üzembe helyezés (deployment)
**Rövid definíció:**  
Az üzembe helyezés során a fejlesztett rendszer éles környezetbe kerül.

**Működési elv:**  
- Telepítés, konfiguráció, adatátvitel (ha kell).  
- Gyakran fokozatos bevezetés történik a kockázat csökkentésére.  
- Fontos a visszaállítási terv hibás release esetére.

**Egyszerű példa:**  
Új verziót először csak a felhasználók 10%-a kap meg, így kisebb a kockázat.

**Vizsgán fontos kulcsszavak:**  
**[[deployment]]**, **éles környezet**, **release**, **rollback**, **bevezetés**

---

#### Karbantartás
**Rövid definíció:**  
A karbantartás az átadás utáni hibajavítást, módosítást és továbbfejlesztést jelenti.

**Működési elv:**  
- Hibák javítása és biztonsági frissítések.  
- Új igények kezelése, rendszer finomhangolása.  
- Hosszú távon ez gyakran a teljes költség nagy részét adja.

**Egyszerű példa:**  
Törvényi változás miatt módosítani kell a számlázási logikát a már működő rendszerben.

**Vizsgán fontos kulcsszavak:**  
**karbantartás**, **hibajavítás**, **továbbfejlesztés**, **frissítés**, **életciklus**

---

## 2. Folyamatmodellek

### 2.1 Vízesés modell (Waterfall)
**Rövid definíció:**  
A **[[vízesés modell]]** lineáris fejlesztési modell, ahol a fázisok egymás után következnek.

**Működési elv:**  
- Előbb specifikáció, utána tervezés, kódolás, tesztelés, átadás.  
- Kevés visszalépési lehetőség van.  
- Jól dokumentált, de változó igényeknél nehézkes.

**Egyszerű példa:**  
Stabil, jól szabályozott környezetben (pl. fix követelményű állami rendszer) működhet jól.

**Vizsgán fontos kulcsszavak:**  
**[[vízesés modell]]**, **lineáris**, **fázisok**, **rugalmatlanság**

---

### 2.2 Iteratív modell
**Rövid definíció:**  
Az **[[iteratív modell]]** ismétlődő ciklusokban fejleszt, minden körben finomítva a terméket.

**Működési elv:**  
- Kis lépésekben haladunk.  
- Minden iteráció után visszajelzés alapján javítunk.  
- Kockázatot és félreértést hamarabb felfed.

**Egyszerű példa:**  
Első iterációban alap keresés készül el, következőben szűrés és rendezés kerül hozzá.

**Vizsgán fontos kulcsszavak:**  
**[[iteratív fejlesztés]]**, **visszacsatolás**, **ciklus**, **folyamatos javítás**

---

### 2.3 Inkrementális modell
**Rövid definíció:**  
Az **[[inkrementális modell]]** a rendszert részenként, működő bővítményekben adja át.

**Működési elv:**  
- A teljes rendszer kisebb funkcionális egységekre bontódik.  
- Minden inkrementum önmagában használható értéket ad.  
- Korai üzleti haszon érhető el.

**Egyszerű példa:**  
Először csak regisztráció + belépés készül el, később jön a rendelés és fizetés modul.

**Vizsgán fontos kulcsszavak:**  
**[[inkrementális modell]]**, **részrendszer**, **korai átadás**, **fokozatos bővítés**

---

### 2.4 Spirál modell
**Rövid definíció:**  
A **[[spirál modell]]** kockázatvezérelt megközelítés, amely iterációkat és kockázatelemzést kombinál.

**Működési elv:**  
- Iterációnként tervezés, kockázatelemzés, fejlesztés, értékelés történik.  
- Nagy, bizonytalan projekteknél különösen hasznos.  
- Erős projektmenedzsmentet igényel.

**Egyszerű példa:**  
Új technológiát használó rendszernél először prototípus készül, hogy a technikai kockázatot csökkentsük.

**Vizsgán fontos kulcsszavak:**  
**[[spirál modell]]**, **kockázatelemzés**, **iteráció**, **prototípus**

---

### 2.5 Agile módszerek (említés)
**Rövid definíció:**  
Az **[[Agile]]** család rugalmas, gyors visszacsatolású fejlesztési szemlélet.

**Működési elv:**  
- Rövid iterációk (**[[sprint]]**), gyakori szállítás.  
- Szoros együttműködés az ügyféllel.  
- Változó követelményekhez jól alkalmazkodik.

**Egyszerű példa:**  
Kéthetes sprint végén demó készül, és az ügyfél visszajelzése alapján változik a következő sprint tartalma.

**Vizsgán fontos kulcsszavak:**  
**[[Agile]]**, **[[sprint]]**, **backlog**, **folyamatos visszajelzés**, **adaptivitás**

---

## 3. Modellek összehasonlítása

**Rövid definíció:**  
A modellek különbsége főleg a rugalmasságban, kockázatkezelésben és visszacsatolás gyakoriságában van.

**Működési elv:**  
- **Vízesés**: egyszerű, jól tervezhető, de merev.  
- **Iteratív**: fokozatos javítás, jobb alkalmazkodás.  
- **Inkrementális**: korán ad működő részeredményt.  
- **Spirál**: kockázatkezelésre erős, de összetettebb.

**Egyszerű példa:**  
Gyorsan változó startup-terméknél általában iteratív/agile jobb, mint a tiszta vízesés.

**Vizsgán fontos kulcsszavak:**  
**modellválasztás**, **rugalmasság**, **visszacsatolás**, **kockázatkezelés**, **korai eredmény**

---

## 4. Folyamat elemei

**Rövid definíció:**  
A folyamat sikeréhez nem csak lépések, hanem szerepkörök, eszközök és szabályok is kellenek.

**Működési elv:**  
- **Szereplők**: fejlesztő, tesztelő, üzleti oldal, ügyfél, projektvezető.  
- **Eszközök**: IDE, verziókezelés, ticketing, CI/CD.  
- **Dokumentáció**: követelmények, tervek, döntések nyoma.  
- **Minőségbiztosítás**: tesztelés, review, szabványok.

**Egyszerű példa:**  
Ha nincs egységes hibajegykezelés, ugyanazt a hibát többen párhuzamosan javíthatják feleslegesen.

**Vizsgán fontos kulcsszavak:**  
**szerepkörök**, **eszköztámogatás**, **dokumentáció**, **minőségbiztosítás**, **CI/CD**

---

## 5. Gyakorlati szempontok
**Rövid definíció:**  
A valós projektben a modell mellett a csapatkommunikáció és a projektkörnyezet dönt a sikerességről.

**Működési elv:**  
- Követelmények gyakran változnak, ezt kezelni kell.  
- A kommunikációs hibák sokszor drágábbak, mint a technikai hibák.  
- A projekt mérete, kockázata és doménje alapján kell modellt választani.

**Egyszerű példa:**  
Kis belső eszköznél gyors iterációk jók, nagy szabályozott rendszernél több dokumentáció és formálisabb folyamat kell.

**Vizsgán fontos kulcsszavak:**  
**követelményváltozás**, **kommunikáció**, **projektkomplexitás**, **modellválasztás**

---

## + Vizsgán érdemes még megemlíteni
- **[[Agile]] vs [[vízesés modell]]**: rugalmasság és visszacsatolás különbsége.  
- Az iteráció előnye: korai hibaészlelés és jobb illeszkedés az igényekhez.  
- Kockázatkezelés szerepe különösen nagy, bizonytalan projekteknél.  
- Valós projektekben gyakori a hibrid, kombinált megoldás.

---

## Rövid szóbeli összefoglaló
A szoftverfejlesztési folyamat célja, hogy tervezhetően és jó minőségben készüljön el egy működő rendszer. Ennek fő lépései a követelményanalízis, tervezés, implementáció, tesztelés, üzembe helyezés és karbantartás. A választott folyamatmodell meghatározza, mennyire rugalmas a fejlesztés. A vízesés modell lineáris és egyszerű, de kevésbé alkalmazkodik a változásokhoz. Az iteratív és inkrementális megközelítés gyorsabb visszacsatolást ad, a spirál modell pedig erős kockázatkezelést biztosít. A gyakorlatban sokszor ezek kombinációját használják, és a sikerhez kulcsfontosságú a jó kommunikáció, dokumentáció és minőségbiztosítás.

## Kulcsfogalmak
- [[szoftverfejlesztési folyamat]]
- [[funkcionális követelmény]]
- [[nem funkcionális követelmény]]
- [[tervezés]]
- [[implementáció]]
- [[egységteszt]]
- [[integrációs teszt]]
- [[rendszerteszt]]
- [[deployment]]
- [[vízesés modell]]
- [[iteratív fejlesztés]]
- [[inkrementális modell]]
- [[spirál modell]]
- [[Agile]]
- [[sprint]]

## Tipikus vizsgakérdések
1. **Melyek a szoftverfejlesztési folyamat fő lépései?**  
   Követelményanalízis, tervezés, implementáció, tesztelés, üzembe helyezés, karbantartás.

2. **Mi a különbség funkcionális és nem funkcionális követelmény között?**  
   Funkcionális: mit csináljon a rendszer; nem funkcionális: milyen minőségi feltételekkel működjön.

3. **Mikor előnyös a vízesés modell?**  
   Stabil, jól definiált követelményeknél, kevés változás esetén.

4. **Miért hasznos az iteratív/inkrementális megközelítés?**  
   Korai működő eredményt ad és gyorsabb visszajelzést tesz lehetővé.

5. **Mitől különleges a spirál modell?**  
   Kockázatvezérelt, minden iterációban hangsúlyos a kockázatelemzés.

6. **Mi az Agile lényege?**  
   Rövid ciklusokban fejleszt, és folyamatosan alkalmazkodik a változó igényekhez.

7. **Miért fontos a tesztelés több szinten?**  
   Mert más hibákat talál az egység-, integrációs és rendszerteszt.

## Minimum, amit tudni kell
- A fejlesztési életciklus fő lépéseit és célját.  
- Funkcionális és nem funkcionális követelmény közti különbséget.  
- Vízesés modell fő jellemzőit (lineáris, kevés visszacsatolás).  
- Iteratív és inkrementális modellek előnyét (rugalmasság, korai eredmény).  
- Spirál modell lényegét (kockázatkezelés).  
- Agile alapgondolatát (rövid iterációk, folyamatos visszajelzés).  
- A tesztelés szintjeit és szerepét.  
- Hogy valós projektekben gyakori a modellek kombinálása.
