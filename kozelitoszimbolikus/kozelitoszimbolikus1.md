# Numerikus számítások – 5. tétel
## Lineáris egyenletrendszerek és mátrixfelbontások

---

## 1. Alapfogalmak

### 1.1 Lineáris egyenletrendszer
**Rövid definíció:**  
A **[[lineáris egyenletrendszer]]** általános alakja `Ax = b`, ahol az ismeretlenek lineárisan szerepelnek.

**Működési elv:**  
- `A`: együttható mátrix.  
- `x`: ismeretlen vektor.  
- `b`: konstans (jobb oldali) vektor.  
- A cél az `x` vektor meghatározása.

**Egyszerű példa:**  
Kétismeretlenes rendszer: `2x + y = 5`, `x - y = 1` mátrix alakban felírható.

**Vizsgán fontos kulcsszavak:**  
**[[lineáris egyenletrendszer]]**, **`Ax=b`**, **együttható mátrix**, **ismeretlen vektor**

---

### 1.2 Mátrix fogalma
**Rövid definíció:**  
A **[[mátrix]]** számok téglalap alakú táblázata, amely lineáris műveletek tömör leírására szolgál.

**Működési elv:**  
- Mérete `m x n`.  
- Fontos speciális esetek: négyzetes, egység-, zérus-, alsó/felső háromszögmátrix.  
- A felbontási módszerek ezekre a szerkezetekre építenek.

**Egyszerű példa:**  
Az egységmátrix szorzásnál „semleges elem”: `I·x = x`.

**Vizsgán fontos kulcsszavak:**  
**[[mátrix]]**, **m x n méret**, **egységmátrix**, **háromszögmátrix**

---

### 1.3 Kapcsolat
**Rövid definíció:**  
Az egyenletrendszert mátrixos alakban kezelve a megoldhatóság jól vizsgálható.

**Működési elv:**  
- A rendszer lehet egyértelműen megoldható, alulhatározott (végtelen sok megoldás) vagy ellentmondásos (nincs megoldás).  
- A rang és a soralak vizsgálata segít eldönteni az esetet.

**Egyszerű példa:**  
Két azonos egyenlet végtelen sok megoldást adhat, két ellentmondó egyenlet pedig egyet sem.

**Vizsgán fontos kulcsszavak:**  
**megoldhatóság**, **egyértelmű megoldás**, **végtelen sok**, **nincs megoldás**, **rang**

---

## 2. Eliminációs módszerek

### 2.1 Gauss-elimináció
**Rövid definíció:**  
A **[[Gauss-elimináció]]** célja, hogy a rendszert felső háromszög alakra hozza.

**Működési elv:**  
- Elemi sorátalakításokkal nullázzuk az alsó háromszög részt.  
- A kapott háromszög-rendszert **visszahelyettesítéssel** oldjuk meg.  
- Alapvető direkt numerikus módszer.

**Egyszerű példa:**  
3x3-as rendszernél előbb az alsó bal elemeket nullázzuk, majd hátulról számoljuk az ismeretleneket.

**Vizsgán fontos kulcsszavak:**  
**[[Gauss-elimináció]]**, **elemi sorátalakítás**, **felső háromszög alak**, **visszahelyettesítés**

---

### 2.2 Gauss–Jordan elimináció
**Rövid definíció:**  
A **[[Gauss–Jordan]]** módszer továbbmegy, és redukált lépcsős alakot állít elő.

**Működési elv:**  
- Nemcsak lefelé, hanem felfelé is nullázunk.  
- Bal oldalon végül egységmátrix jelenik meg.  
- A jobb oldalon közvetlenül a megoldás olvasható ki.

**Egyszerű példa:**  
Kiterjesztett mátrixon dolgozva `[A|b] -> [I|x]` alakot kapunk.

**Vizsgán fontos kulcsszavak:**  
**[[Gauss–Jordan]]**, **redukált lépcsős alak**, **egységmátrix**, **közvetlen kiolvasás**

---

### 2.3 Pivotálás
**Rövid definíció:**  
A **[[pivotálás]]** a numerikus stabilitást javító sor/oszlopcsere stratégia.

**Működési elv:**  
- Részleges pivotálás: oszlopon belül választunk nagy abszolút értékű pivotot.  
- Teljes pivotálás: sor- és oszlopcserét is megenged.  
- Csökkenti a kerekítési hibák hatását.

**Egyszerű példa:**  
Nagyon kicsi főátlóbeli elem helyett nagyobbat választunk, hogy elkerüljük a pontatlanság felerősödését.

**Vizsgán fontos kulcsszavak:**  
**[[pivotálás]]**, **numerikus stabilitás**, **részleges pivot**, **teljes pivot**

---

## 3. Trianguláris felbontások

### 3.1 LU-felbontás
**Rövid definíció:**  
Az **[[LU-felbontás]]** a mátrixot alsó és felső háromszögmátrix szorzatára bontja: `A = L·U`.

**Működési elv:**  
- Előbb `Ly = b` rendszert oldunk (előrehelyettesítés).  
- Utána `Ux = y` rendszert oldunk (visszahelyettesítés).  
- Különösen hatékony, ha ugyanazzal `A` mátrixszal több különböző `b`-re kell megoldás.

**Egyszerű példa:**  
Paramétervizsgálatnál ugyanaz az együtthatómátrix, csak a jobb oldal változik -> LU gyorsít.

**Vizsgán fontos kulcsszavak:**  
**[[LU-felbontás]]**, **`A=L·U`**, **előrehelyettesítés**, **visszahelyettesítés**, **többszöri megoldás**

---

### 3.2 Cholesky-felbontás
**Rövid definíció:**  
A **[[Cholesky-felbontás]]** speciális felbontás: `A = L·L^T`.

**Működési elv:**  
- Csak szimmetrikus, pozitív definit mátrixra alkalmazható.  
- Kevesebb műveletet igényelhet, mint általános LU.

**Egyszerű példa:**  
Legkisebb négyzetekből származó normálegyenleteknél gyakran SPD mátrix adódik, ott Cholesky hatékony.

**Vizsgán fontos kulcsszavak:**  
**[[Cholesky-felbontás]]**, **szimmetrikus**, **pozitív definit**, **`A=L·L^T`**

---

### 3.3 QR-felbontás
**Rövid definíció:**  
A **[[QR-felbontás]]** szerint `A = Q·R`, ahol `Q` ortogonális, `R` felső háromszögmátrix.

**Működési elv:**  
- Ortogonalitás miatt numerikusan stabil eljárás.  
- Túlhatározott rendszerek és **[[legkisebb négyzetek módszere]]** esetén különösen fontos.

**Egyszerű példa:**  
Mérési adatokra illesztett egyenes paraméterei QR alapú megoldással stabilan számolhatók.

**Vizsgán fontos kulcsszavak:**  
**[[QR-felbontás]]**, **ortogonális mátrix**, **túlhatározott rendszer**, **legkisebb négyzetek**

---

## 4. Numerikus szempontok
**Rövid definíció:**  
Numerikus számításnál nem csak a módszer elmélete, hanem a pontosság és stabilitás is kritikus.

**Működési elv:**  
- Lebegőpontos műveletek kerekítési hibát hoznak.  
- A módszer stabilitása befolyásolja a hiba növekedését.  
- A **[[kondíciószám]]** jelzi, mennyire érzékeny a feladat a bemeneti hibákra.

**Egyszerű példa:**  
Rossz kondíciójú mátrixnál kis bemeneti zaj is nagy megoldáshibát okozhat.

**Vizsgán fontos kulcsszavak:**  
**kerekítési hiba**, **numerikus stabilitás**, **[[kondíciószám]]**, **hibaterjedés**

---

## + Vizsgán érdemes még megemlíteni
- Háromszögmátrix rendszerek gyorsan oldhatók előre-/visszahelyettesítéssel.  
- LU lényegében a Gauss-elimináció strukturált újrafelhasználása.  
- Cholesky SPD esetben gyors és hatékony.  
- QR robusztusabb lehet illesztési feladatoknál.  
- Gyakorlati területek: mérnöki szimuláció, adatillesztés, optimalizálás.

---

## Rövid szóbeli összefoglaló
A lineáris egyenletrendszerek numerikus megoldása általában `Ax=b` alakban történik. Alapmódszer a Gauss-elimináció, ahol háromszög alakra hozunk, majd visszahelyettesítünk, ennek kiterjesztése a Gauss–Jordan eljárás. A pivotálás numerikus stabilitás miatt fontos. Mátrixfelbontásoknál az LU-felbontás többszöri megoldásnál előnyös, a Cholesky speciális, szimmetrikus pozitív definit esetben gyorsabb, a QR pedig túlhatározott rendszereknél és legkisebb négyzeteknél robusztus. A gyakorlatban mindig figyelni kell kerekítési hibára, stabilitásra és kondíciószámra, mert ezek határozzák meg a valódi pontosságot.

## Kulcsfogalmak
- [[lineáris egyenletrendszer]]
- [[mátrix]]
- [[Gauss-elimináció]]
- [[Gauss–Jordan]]
- [[pivotálás]]
- [[háromszögmátrix]]
- [[LU-felbontás]]
- [[Cholesky-felbontás]]
- [[QR-felbontás]]
- [[ortogonális mátrix]]
- [[előrehelyettesítés]]
- [[visszahelyettesítés]]
- [[kondíciószám]]
- [[numerikus stabilitás]]
- [[legkisebb négyzetek módszere]]

## Tipikus vizsgakérdések
1. **Mit jelent az `Ax=b` alak?**  
   A együttható mátrix, x ismeretlen vektor, b konstans vektor.

2. **Mi a Gauss-elimináció lényege?**  
   Felső háromszög alak előállítása elemi sorátalakításokkal, majd visszahelyettesítés.

3. **Miért kell pivotálás?**  
   Numerikus stabilitást javít, csökkenti a kerekítési hibák felerősödését.

4. **Mikor előnyös az LU-felbontás?**  
   Ha ugyanazzal az A mátrixszal több jobb oldali vektorra kell megoldás.

5. **Milyen feltétellel használható a Cholesky-felbontás?**  
   Ha a mátrix szimmetrikus és pozitív definit.

6. **Mire jó a QR-felbontás?**  
   Túlhatározott rendszerek és legkisebb négyzetes feladatok stabil megoldására.

7. **Mit jelez a kondíciószám?**  
   A feladat bemeneti hibákra való érzékenységét.

## Minimum, amit tudni kell
- `Ax=b` jelentése és mátrixos felírás alapja.  
- Gauss-elimináció és visszahelyettesítés menete.  
- Pivotálás célja (stabilitás).  
- LU-felbontás alapképlete és megoldási lépései.  
- Cholesky alkalmazási feltétele.  
- QR-felbontás alapötlete és alkalmazási területe.  
- Kerekítési hiba és stabilitás fogalma.  
- Kondíciószám említése, mint érzékenységi mutató.
