# Operációkutatás – 10. tétel
## Lineáris programozás és szimplex módszer

---

## 1. Lineáris programozási (LP) alapfeladat

### 1.1 Alapfogalom
**Rövid definíció:**  
A **[[lineáris programozás]]** célja lineáris célfüggvény optimalizálása lineáris korlátozó feltételek mellett.

**Működési elv:**  
- Döntési változókra írjuk fel a célt és a korlátokat.  
- Tipikusan erőforrás-allokációs problémák modellje.

**Egyszerű példa:**  
Gyártási tervnél adott erőforrásokból maximalizáljuk a profitot.

**Vizsgán fontos kulcsszavak:**  
**[[lineáris programozás]]**, **célfüggvény**, **korlátozó feltételek**, **optimalizálás**

---

### 1.2 Általános alak
**Rövid definíció:**  
Az LP standard felírása: `max/min c^T x`, feltételekkel `Ax <= b`, `x >= 0`.

**Működési elv:**  
- `x` döntési változóvektor.  
- `c` célfüggvény együtthatói.  
- `A,b` a korlátokat adja.

**Egyszerű példa:**  
`max 3x1+2x2`, korlátokkal: nyersanyag és idő kapacitás.

**Vizsgán fontos kulcsszavak:**  
**`c^T x`**, **`Ax<=b`**, **nemnegativitás**, **döntési változó**

---

### 1.3 Geometriai értelmezés
**Rövid definíció:**  
Az LP megengedett tartománya konvex poliéder, ahol az optimum csúcspontban kereshető.

**Működési elv:**  
- A korlátok féltereket adnak, metszetük a megengedett tartomány.  
- Lineáris célfüggvény szintvonalai miatt szélsőponton adódik optimum.

**Egyszerű példa:**  
2 változós feladatnál a sokszög csúcspontjain értékeljük a célfüggvényt.

**Vizsgán fontos kulcsszavak:**  
**megengedett tartomány**, **konvex poliéder**, **csúcspont optimum**

---

## 2. Standard alak

**Rövid definíció:**  
A standard alak a szimplex számára kedvező algebrai formára hozza az LP-t.

**Működési elv:**  
- `<=` típusú korlátokhoz slack változót adunk.  
- Így egyenletek rendszerét kapjuk nemnegatív változókkal.

**Egyszerű példa:**  
`x1+x2 <= 5` átalakul: `x1+x2+s1=5`, `s1>=0`.

**Vizsgán fontos kulcsszavak:**  
**standard alak**, **slack változó**, **egyenlőtlenség-átalakítás**

---

## 3. Szimplex algoritmus

### 3.1 Alapötlet
**Rövid definíció:**  
A **[[szimplex módszer]]** csúcspontok között haladva javítja a célfüggvényt.

**Működési elv:**  
- Minden iteráció új bázismegoldást ad.  
- Addig lép, amíg nincs jobb szomszédos csúcspont.

**Egyszerű példa:**  
Kezdő megoldásból pivot lépésekkel jutunk optimális sarokpontra.

**Vizsgán fontos kulcsszavak:**  
**[[szimplex módszer]]**, **csúcsponti lépkedés**, **iteratív javítás**

---

### 3.2 Alapfogalmak
**Rövid definíció:**  
A szimplex algebrai keretét bázis- és nem bázisváltozók adják.

**Működési elv:**  
- Bázisváltozók aktuálisan nem nulla jelöltek.  
- Nem bázisváltozók tipikusan nullára állítottak.  
- A bázis meghatározza az aktuális csúcspontot.

**Egyszerű példa:**  
Két bázisváltozós táblázatban minden pivot új bázist eredményez.

**Vizsgán fontos kulcsszavak:**  
**bázisváltozó**, **nem bázisváltozó**, **bázismegoldás**

---

### 3.3 Lépések
**Rövid definíció:**  
A szimplex lépések szabályozott báziscserét valósítanak meg.

**Működési elv:**  
- Kezdő megengedett bázis.  
- Belépő változó (javítja a célt).  
- Kilépő változó (megengedettség megtartása).  
- Pivot és új iteráció.

**Egyszerű példa:**  
Negatív reduced cost alapján választunk belépőt maximalizálásnál.

**Vizsgán fontos kulcsszavak:**  
**belépő/kilépő változó**, **pivot**, **szimplex iteráció**

---

### 3.4 Leállási feltétel
**Rövid definíció:**  
Az algoritmus leáll, ha nincs olyan irány, amely javítaná a célfüggvényt.

**Működési elv:**  
- Optimalitási feltétel teljesül a táblázatban.  
- Ekkor az aktuális bázismegoldás optimális.

**Egyszerű példa:**  
Ha maximalizálásnál nincs negatív javító mutató, kész az optimum.

**Vizsgán fontos kulcsszavak:**  
**leállási feltétel**, **optimalitási kritérium**, **optimális bázis**

---

## 4. Speciális esetek

### 4.1 Degeneráció
**Rövid definíció:**  
**[[Degeneráció]]**, ha bázisváltozó nulla értéket vesz fel.

**Működési elv:**  
- A célfüggvény néha nem javul pivot után sem.  
- Lassulhat a haladás.

**Egyszerű példa:**  
Több aktív korlát metszése ugyanazon csúcsponton.

**Vizsgán fontos kulcsszavak:**  
**[[degeneráció]]**, **nulla bázisváltozó**, **lassuló iteráció**

---

### 4.2 Ciklizáció
**Rövid definíció:**  
**[[Ciklizáció]]** esetén ugyanazok a bázisok ismétlődnek.

**Működési elv:**  
- Végtelen iteráció elméleti veszélye.  
- Pivotszabályokkal (pl. Bland) megelőzhető.

**Egyszerű példa:**  
Degenerált feladatnál rossz pivotválasztás ismétlődést okozhat.

**Vizsgán fontos kulcsszavak:**  
**[[ciklizáció]]**, **ismétlődő bázis**, **Bland-szabály**

---

### 4.3 Több optimális megoldás
**Rövid definíció:**  
Több optimum akkor van, ha különböző megengedett pontok azonos célfüggvényértéket adnak.

**Működési elv:**  
- Gyakran teljes él vagy lap mentén azonos optimum érték áll fenn.

**Egyszerű példa:**  
2D-ben a célfüggvény egy megengedett él mentén állandó.

**Vizsgán fontos kulcsszavak:**  
**több optimális megoldás**, **azonos célérték**, **optimális él**

---

### 4.4 Nem korlátos feladat
**Rövid definíció:**  
Nem korlátos feladatnál a célfüggvény tetszőlegesen javítható a megengedett tartományban.

**Működési elv:**  
- Nincs felső/alsó korlát az optimalizálandó értékre.

**Egyszerű példa:**  
Maximalizálásnál létezik olyan irány, ahol korlát nélkül nő a profit.

**Vizsgán fontos kulcsszavak:**  
**nem korlátos LP**, **végtelen javulás**, **nincs optimum**

---

### 4.5 Nincs megoldás
**Rövid definíció:**  
Ha a korlátok ellentmondanak egymásnak, a megengedett tartomány üres.

**Működési elv:**  
- Nincs olyan pont, amely minden feltételt egyszerre teljesít.

**Egyszerű példa:**  
`x >= 5` és `x <= 3` egyszerre teljesíthetetlen.

**Vizsgán fontos kulcsszavak:**  
**infeasible feladat**, **üres tartomány**, **ellentmondó korlátok**

---

## 5. Kétfázisú szimplex módszer

### 5.1 Probléma
**Rövid definíció:**  
A kétfázisú módszer akkor kell, ha nem ismert kezdeti megengedett bázis.

**Működési elv:**  
- Először mesterségesen keressük a megengedett indulópontot.

**Egyszerű példa:**  
`>=` és `=` korlátok esetén gyakran nincs kézenfekvő kezdő bázis.

**Vizsgán fontos kulcsszavak:**  
**kétfázisú szimplex**, **kezdeti bázis hiánya**, **mesterséges változó**

---

### 5.2 I. fázis
**Rövid definíció:**  
Az I. fázis segédfeladatot old meg a megengedett bázis megtalálására.

**Működési elv:**  
- Mesterséges változókat vezetünk be.  
- Cél ezek nullára csökkentése.

**Egyszerű példa:**  
Ha I. fázis optimuma nem nulla, az eredeti feladat infeasible.

**Vizsgán fontos kulcsszavak:**  
**I. fázis**, **segédfeladat**, **mesterséges változók**

---

### 5.3 II. fázis
**Rövid definíció:**  
A II. fázis már az eredeti LP célfüggvényét optimalizálja.

**Működési elv:**  
- Az I. fázisban talált megengedett bázisból indul.

**Egyszerű példa:**  
A tényleges gazdasági cél (profitmaximum) csak II. fázisban jelenik meg.

**Vizsgán fontos kulcsszavak:**  
**II. fázis**, **eredeti célfüggvény**, **optimalizálás**

---

## 6. LP alaptételek

### 6.1 Alaptétel
**Rövid definíció:**  
LP alaptétel: ha létezik optimum, akkor található optimális bázismegoldás.

**Működési elv:**  
- Ez igazolja a csúcspontkereső szimplex módszer helyességét.

**Egyszerű példa:**  
Nem kell a poliéder belsejét vizsgálni, elég a szélsőpontok környezete.

**Vizsgán fontos kulcsszavak:**  
**LP alaptétel**, **optimális bázismegoldás**, **szélsőpont**

---

### 6.2 Egyéb tételek
**Rövid definíció:**  
Az LP elméleti alapja a konvexitás és a dualitási szemlélet.

**Működési elv:**  
- Konvex tartomány + lineáris célfüggvény -> kezelhető geometria.  
- Dualitás kapcsolja a primal és dual feladatot.

**Egyszerű példa:**  
Erőforrás-árnyékárak dual változókkal értelmezhetők.

**Vizsgán fontos kulcsszavak:**  
**konvexitás**, **szélsőpont tétel**, **dualitás**

---

## 7. Gyakorlati szempontok
**Rövid definíció:**  
Gyakorlatban a módszer stabilitása és implementációs részletei erősen számítanak.

**Működési elv:**  
- Pivotszabály választás befolyásolja a futást és ciklizációt.  
- Numerikus pontosság és skálázás is fontos nagy feladatoknál.

**Egyszerű példa:**  
Rossz kondíciójú adatoknál a táblázatos számolás pontatlansága nőhet.

**Vizsgán fontos kulcsszavak:**  
**numerikus stabilitás**, **pivot szabály**, **hatékonyság**

---

## + Vizsgán érdemes még megemlíteni
- Geometriai és algebrai nézőpont együtt ad teljes képet.  
- Degeneráció nem ugyanaz, mint ciklizáció, de kapcsolódhat hozzá.  
- Kétfázisú szimplex induló megoldás kereséshez kulcsfontosságú.  
- Alkalmazások: termelés, logisztika, erőforrás-allokáció.

---

## Rövid szóbeli összefoglaló
A lineáris programozás lineáris célfüggvény optimalizálása lineáris korlátok mellett. Geometriailag a megengedett tartomány konvex poliéder, és az optimum csúcspontban kereshető. A szimplex módszer csúcspontok között lépked pivot műveletekkel, mindig a célfüggvény javítására törekedve. Ha nincs induló megengedett bázis, kétfázisú szimplexet alkalmazunk mesterséges változókkal. Fontos speciális eset a degeneráció, ciklizáció, nem korlátosság és infeasibility. Elméleti alap, hogy ha optimum létezik, van optimális bázismegoldás is.

## Kulcsfogalmak
- [[lineáris programozás]]
- [[célfüggvény]]
- [[megengedett tartomány]]
- [[konvex poliéder]]
- [[standard alak]]
- [[slack változó]]
- [[szimplex módszer]]
- [[bázisváltozó]]
- [[pivot]]
- [[degeneráció]]
- [[ciklizáció]]
- [[kétfázisú szimplex]]
- [[mesterséges változó]]
- [[dualitás]]
- [[optimális bázismegoldás]]

## Tipikus vizsgakérdések
1. **Mi az LP feladat általános alakja?**  
   Lineáris célfüggvény max/min, lineáris korlátokkal és nemnegativitással.

2. **Miért csúcspontban keressük az optimumot LP-ben?**  
   Mert konvex poliéderen lineáris célfüggvény optimuma szélsőponton adódik.

3. **Mi a szimplex alapötlete?**  
   Csúcspontok között haladunk úgy, hogy a célfüggvény javuljon.

4. **Mi a belépő és kilépő változó szerepe?**  
   Ezek határozzák meg a báziscserét pivot során.

5. **Mikor kell kétfázisú szimplex?**  
   Ha nincs kézenfekvő kezdeti megengedett bázismegoldás.

6. **Mi a különbség degeneráció és ciklizáció között?**  
   Degeneráció: nulla bázisváltozó; ciklizáció: ismétlődő bázisállapotok.

7. **Mit jelent, hogy a feladat nem korlátos?**  
   A célfüggvény korlát nélkül javítható, nincs véges optimum.

## Minimum, amit tudni kell
- LP fogalma és általános felírása.  
- Megengedett tartomány és csúcspont-optimum elve.  
- Standard alak és slack változók szerepe.  
- Szimplex iteráció fő lépései.  
- Leállási feltétel lényege.  
- Speciális esetek: degeneráció, nem korlátos, nincs megoldás.  
- Kétfázisú szimplex alapötlete.  
- Alaptétel: optimum esetén van optimális bázismegoldás.
