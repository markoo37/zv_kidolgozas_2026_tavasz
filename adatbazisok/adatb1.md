# Adatbázisok – 14. tétel
## Adatbázis-tervezés, relációs modell, normalizálás

---

## 1. Alapfogalmak

### 1.1 Adatbázis
**Rövid definíció:**  
Az **[[adatbázis]]** strukturált, tartósan tárolt adathalmaz, amelyet hatékonyan lehet kezelni.

**Működési elv:**  
- Cél a redundancia csökkentése és a konzisztencia fenntartása.  
- Több felhasználó és alkalmazás is elérheti szabályozott módon.  
- A DBMS gondoskodik az adatok integritásáról.

**Egyszerű példa:**  
Egy egyetemi rendszerben hallgatók, kurzusok és jegyek adatai közös adatbázisban vannak.

**Vizsgán fontos kulcsszavak:**  
**[[adatbázis]]**, **redundancia**, **konzisztencia**, **DBMS**

---

### 1.2 Relációs adatmodell
**Rövid definíció:**  
A **[[relációs adatmodell]]** adatait táblák (relációk) formájában szervezi.

**Működési elv:**  
- **Reláció/tábla**: az adatok logikai tárolója.  
- **Sor (tuple)**: egy rekord.  
- **Oszlop (attribútum)**: egy tulajdonság.  
- **Domain**: attribútum lehetséges értékkészlete.  
- **Relációs séma**: a tábla szerkezetének leírása.

**Egyszerű példa:**  
`Hallgato(neptun, nev, szak)` séma szerint minden hallgató egy sor.

**Vizsgán fontos kulcsszavak:**  
**[[relációs adatmodell]]**, **tábla**, **tuple**, **attribútum**, **domain**, **séma**

---

## 2. Egyed-kapcsolat modell (ER modell)

### 2.1 Egyed (entity)
**Rövid definíció:**  
Az **[[egyed]]** a valós világ egy megkülönböztethető objektuma.

**Működési elv:**  
- Hasonló egyedek együtt **egyedhalmazt** alkotnak.  
- Az egyedekből később relációs táblák készülnek.

**Egyszerű példa:**  
`Hallgató` egyedhalmaz: minden hallgató egy külön egyed.

**Vizsgán fontos kulcsszavak:**  
**[[egyed]]**, **egyedhalmaz**, **valós világ modellje**

---

### 2.2 Attribútumok
**Rövid definíció:**  
Az attribútum az egyed tulajdonságát írja le.

**Működési elv:**  
- Lehet egyszerű vagy összetett.  
- Lehet egyértékű vagy többértékű.  
- Kulcsattribútum egyedileg azonosítja az egyedet.

**Egyszerű példa:**  
`név` összetett lehet (vezetéknév + keresztnév), `telefonszám` többértékű lehet.

**Vizsgán fontos kulcsszavak:**  
**attribútum**, **kulcsattribútum**, **egyszerű/összetett**, **egyértékű/többértékű**

---

### 2.3 Kapcsolatok (relationship)
**Rövid definíció:**  
A **[[kapcsolat]]** egyedhalmazok közti összefüggést jelenti.

**Működési elv:**  
- Kardinalitás szerint lehet 1:1, 1:N vagy N:M.  
- A kapcsolat típusa meghatározza a relációs leképezést.

**Egyszerű példa:**  
Hallgató és kurzus között jellemzően N:M kapcsolat van (sok hallgató sok kurzust felvehet).

**Vizsgán fontos kulcsszavak:**  
**[[kapcsolat]]**, **kardinalitás**, **1:1**, **1:N**, **N:M**

---

### 2.4 ER diagram
**Rövid definíció:**  
Az **[[ER diagram]]** az egyedek, attribútumok és kapcsolatok grafikus ábrázolása.

**Működési elv:**  
- Segít tervezési szinten átlátni az adatstruktúrát.  
- A relációs séma előkészítő lépése.

**Egyszerű példa:**  
„Hallgató - felvesz - Kurzus” kapcsolat diagramon jól láthatóan modellezhető.

**Vizsgán fontos kulcsszavak:**  
**[[ER diagram]]**, **tervezési modell**, **grafikus reprezentáció**

---

## 3. ER → relációs modell leképezés

### 3.1 Egyed → tábla
**Rövid definíció:**  
Az ER modell egyedeit relációs táblákra képezzük.

**Működési elv:**  
- Egyed -> tábla.  
- Attribútumok -> oszlopok.  
- Kulcsattribútum -> **[[elsődleges kulcs]]**.

**Egyszerű példa:**  
`Kurzus(kod, nev, kredit)`, ahol `kod` az elsődleges kulcs.

**Vizsgán fontos kulcsszavak:**  
**ER-reláció leképezés**, **egyedből tábla**, **elsődleges kulcs**

---

### 3.2 Kapcsolatok leképezése
**Rövid definíció:**  
A kapcsolatok relációs leképezése a kardinalitástól függ.

**Működési elv:**  
- 1:1: egyik oldalba idegen kulcs kerül.  
- 1:N: az N oldali táblába kerül idegen kulcs.  
- N:M: külön **kapcsolótábla** szükséges két idegen kulccsal.

**Egyszerű példa:**  
`Felvesz(hallgato_id, kurzus_id, datum)` tipikus N:M kapcsolótábla.

**Vizsgán fontos kulcsszavak:**  
**kardinalitás leképezés**, **[[idegen kulcs]]**, **kapcsolótábla**

---

### 3.3 Többértékű attribútum
**Rövid definíció:**  
A többértékű attribútumot relációs modellben külön táblára bontjuk.

**Működési elv:**  
- A fő egyed kulcsa idegen kulcsként megjelenik az új táblában.  
- Így megszűnik az ismétlődő csoport.

**Egyszerű példa:**  
`HallgatoTelefon(hallgato_id, telefonszam)` tábla több telefonszám kezelésére.

**Vizsgán fontos kulcsszavak:**  
**többértékű attribútum**, **külön tábla**, **1:N felbontás**

---

## 4. Kulcsok fajtái

**Rövid definíció:**  
A kulcsok biztosítják az egyedi azonosítást és a táblák közötti kapcsolatot.

**Működési elv:**  
- **[[elsődleges kulcs]]**: egyedi sorazonosító.  
- **[[idegen kulcs]]**: másik tábla kulcsára hivatkozik.  
- **[[szuperkulcs]]**: egyediséget biztosító attribútumhalmaz.  
- **[[kandidáns kulcs]]**: minimális szuperkulcs.  
- **Összetett kulcs**: több attribútumból áll.

**Egyszerű példa:**  
Kapcsolótáblában gyakori az összetett elsődleges kulcs: `(hallgato_id, kurzus_id)`.

**Vizsgán fontos kulcsszavak:**  
**kulcsfajták**, **PK**, **FK**, **szuperkulcs**, **kandidáns kulcs**, **összetett kulcs**

---

## 5. Funkcionális függőség

### 5.1 Fogalom
**Rövid definíció:**  
A **[[funkcionális függőség]]** `X -> Y` azt jelenti, hogy X értéke egyértelműen meghatározza Y-t.

**Működési elv:**  
- Alap a normalizálási döntéseknél.  
- Segít felismerni redundanciát és anomáliákat.

**Egyszerű példa:**  
`Neptun -> HallgatoNev`, mert egy Neptun-kódhoz egy hallgatónév tartozik.

**Vizsgán fontos kulcsszavak:**  
**[[funkcionális függőség]]**, **determináns**, **X -> Y**

---

### 5.2 Típusok
**Rövid definíció:**  
A függőségek típusa meghatározza, milyen normalizálási lépés szükséges.

**Működési elv:**  
- Triviális függőség: Y része X-nek.  
- Teljes függőség: teljes kulcstól függ.  
- Részleges: csak kulcsrészlettől függ (2NF sérül).  
- Tranzitív: nem kulcs -> nem kulcs függés (3NF sérülhet).

**Egyszerű példa:**  
Összetett kulcsnál, ha egy attribútum csak a kulcs egyik részétől függ, részleges függőség van.

**Vizsgán fontos kulcsszavak:**  
**részleges függőség**, **tranzitív függőség**, **teljes függőség**, **normalizálási jelzők**

---

## 6. Normalizálás

### 6.1 Cél
**Rövid definíció:**  
A **[[normalizálás]]** a relációk átalakítása redundancia és anomáliák csökkentésére.

**Működési elv:**  
- Cél a jó szerkezetű, konzisztens séma.  
- Kezeli a beszúrási, törlési és módosítási anomáliákat.

**Egyszerű példa:**  
Ha tárgy és oktató adatai egy táblában ismétlődnek, bontással csökkenthető a duplikáció.

**Vizsgán fontos kulcsszavak:**  
**[[normalizálás]]**, **redundancia csökkentés**, **anomália**, **sémabontás**

---

### 6.2 Normálformák

#### 1NF (első normálforma)
**Rövid definíció:**  
Az **[[1NF]]** megköveteli, hogy minden mező atomi legyen.

**Működési elv:**  
- Egy cellában egy érték szerepel.  
- Nincs ismétlődő csoport vagy lista egy mezőben.

**Egyszerű példa:**  
`telefonok` lista helyett külön sorok/tábla.

**Vizsgán fontos kulcsszavak:**  
**[[1NF]]**, **atomi érték**, **ismétlődő csoport tilalma**

---

#### 2NF
**Rövid definíció:**  
A **[[2NF]]** az 1NF-en túl kizárja a részleges függőséget.

**Működési elv:**  
- Összetett kulcs esetén minden nem kulcs attribútumnak a teljes kulcstól kell függenie.

**Egyszerű példa:**  
Ha `(hallgato_id, kurzus_id)` kulcs mellett `hallgato_nev` csak `hallgato_id`-tól függ, bontani kell.

**Vizsgán fontos kulcsszavak:**  
**[[2NF]]**, **részleges függőség megszüntetése**, **teljes kulcsfüggés**

---

#### 3NF
**Rövid definíció:**  
A **[[3NF]]** a 2NF-en túl kizárja a tranzitív függéseket nem kulcs attribútumok között.

**Működési elv:**  
- Nem kulcs attribútum ne függjön másik nem kulcs attribútumtól.  
- Csökken a módosítási anomália.

**Egyszerű példa:**  
Ha `irszam -> varos`, akkor város ne a hallgató táblában legyen ismételve.

**Vizsgán fontos kulcsszavak:**  
**[[3NF]]**, **tranzitív függőség megszüntetése**, **tisztább séma**

---

#### BCNF (említés)
**Rövid definíció:**  
A **[[BCNF]]** szigorúbb forma: minden determinánsnak kulcsnak kell lennie.

**Működési elv:**  
- További redundancia csökkentés speciális esetekben is.

**Egyszerű példa:**  
Bizonyos 3NF táblák BCNF-re bontás után még stabilabb szerkezetet adnak.

**Vizsgán fontos kulcsszavak:**  
**[[BCNF]]**, **determináns kulcs**, **szigorú normalizálás**

---

## 7. Gyakorlati szempontok
**Rövid definíció:**  
Gyakorlatban a normalizáltság és teljesítmény között kompromisszumot kell találni.

**Működési elv:**  
- Túlzott normalizálás sok JOIN-t igényelhet.  
- Bizonyos esetekben kontrollált **[[denormalizálás]]** javíthat teljesítményt.  
- Tervezési folyamat: igényfelmérés -> ER -> relációs séma -> normalizálás -> finomhangolás.

**Egyszerű példa:**  
Riport táblákban néha denormalizált struktúrát használunk gyors lekérdezéshez.

**Vizsgán fontos kulcsszavak:**  
**normalizálás vs teljesítmény**, **[[denormalizálás]]**, **tervezési folyamat**, **JOIN költség**

---

## + Vizsgán érdemes még megemlíteni
- Az **[[ER modell]]** tervezési szerepe a logikai modell előtt.  
- A kulcsok biztosítják az adatintegritást és kapcsolatokat.  
- Normalizálás gyakorlati példával könnyen kérdezhető.  
- Redundancia közvetlenül anomáliákhoz vezethet.

---

## Rövid szóbeli összefoglaló
Az adatbázis-tervezés célja, hogy az adatokat konzisztensen, redundancia nélkül tudjuk tárolni. A relációs modellben táblákkal, sorokkal és oszlopokkal dolgozunk, kulcsokkal biztosítjuk az egyedi azonosítást és a kapcsolatok épségét. Tervezésnél először ER modell készül, ezt képezzük át relációs sémára kardinalitási szabályok alapján. A normalizálás a funkcionális függőségekre épít, és csökkenti a beszúrási, törlési, módosítási anomáliákat. 1NF, 2NF, 3NF a legfontosabb vizsgaszint, BCNF említési szinten. Gyakorlatban teljesítmény miatt néha denormalizálás is előfordul, de ezt tudatosan kell kezelni.

## Kulcsfogalmak
- [[adatbázis]]
- [[relációs adatmodell]]
- [[ER modell]]
- [[egyed]]
- [[kapcsolat]]
- [[ER diagram]]
- [[elsődleges kulcs]]
- [[idegen kulcs]]
- [[funkcionális függőség]]
- [[normalizálás]]
- [[1NF]]
- [[2NF]]
- [[3NF]]
- [[BCNF]]
- [[denormalizálás]]

## Tipikus vizsgakérdések
1. **Mi a relációs adatmodell lényege?**  
   Adatok táblákban vannak, sorokkal és oszlopokkal, kulcsokkal összekapcsolva.

2. **Mi az ER modell szerepe?**  
   Fogalmi tervezési eszköz, amelyből relációs séma készíthető.

3. **Hogyan képezünk le N:M kapcsolatot relációs modellbe?**  
   Külön kapcsolótáblával, két idegen kulccsal.

4. **Mi a különbség elsődleges és idegen kulcs között?**  
   Elsődleges kulcs azonosít, idegen kulcs más tábla kulcsára hivatkozik.

5. **Mit jelent az X -> Y funkcionális függőség?**  
   X egyértelműen meghatározza Y értékét.

6. **Miért normalizálunk?**  
   Redundancia és anomáliák csökkentése érdekében.

7. **Miben különbözik 2NF és 3NF?**  
   2NF részleges függőséget zár ki, 3NF tranzitív függőséget is.

## Minimum, amit tudni kell
- Relációs modell alapfogalmai: tábla, sor, oszlop, séma.  
- ER modell fő elemei: egyed, attribútum, kapcsolat.  
- ER -> reláció leképezés alap szabályai (1:1, 1:N, N:M).  
- Kulcsfajták és szerepük (PK, FK legalább).  
- Funkcionális függőség alapjelentése.  
- Normalizálás célja és anomáliák típusa.  
- 1NF, 2NF, 3NF rövid definíciója.  
- Hogy teljesítmény miatt denormalizálás néha indokolt lehet.
