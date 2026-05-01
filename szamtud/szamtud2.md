# Számítástudomány – 4. tétel
## Eldönthetőség, komplexitás, P és NP osztályok

---

## 1. Eldönthetőség

### 1.1 Fogalom
**Rövid definíció:**  
Az **[[eldöntési probléma]]** kimenete igen/nem típusú, és **eldönthető**, ha van algoritmus, amely minden bemenetre megáll és helyes választ ad.

**Működési elv:**  
- Az eldönthetőség alapvetően „létezik-e teljes algoritmus?” kérdés.  
- Nem az a kérdés, hogy gyors-e, hanem hogy mindig befejeződik-e.

**Egyszerű példa:**  
Egy szám párosságának eldöntése eldönthető probléma.

**Vizsgán fontos kulcsszavak:**  
**[[eldönthetőség]]**, **[[eldöntési probléma]]**, **mindig megáll**, **helyes válasz**

---

### 1.2 Determinisztikus modell
**Rövid definíció:**  
A determinizmus azt jelenti, hogy minden állapot-bemenet párhoz egyetlen következő lépés tartozik.

**Működési elv:**  
- A számítás útvonala egyértelmű.  
- Elméleti modellként gyakran **[[Turing-gép]]et** használunk.

**Egyszerű példa:**  
Klasszikus algoritmusok (pl. rendezés) determinisztikus lépéssorozattal futnak.

**Vizsgán fontos kulcsszavak:**  
**determinisztikus modell**, **egyértelmű lépés**, **[[Turing-gép]]**

---

### 1.3 Nemdeterminisztikus modell
**Rövid definíció:**  
A nemdeterminisztikus modellben egy lépésnél több folytatás lehetséges.

**Működési elv:**  
- Elméletben „több ág” fut egyszerre.  
- Elfogadás történik, ha létezik legalább egy elfogadó számítási ág.

**Egyszerű példa:**  
NP problémáknál úgy gondolunk rá, mintha a gép „kitalálná” a jó tanút.

**Vizsgán fontos kulcsszavak:**  
**nemdeterminizmus**, **számítási ágak**, **létezik jó út**

---

## 2. Eldönthetetlen problémák

### 2.1 Fogalom
**Rövid definíció:**  
**[[Eldönthetetlen probléma]]** esetén nem létezik algoritmus, amely minden bemenetre biztosan megáll és helyesen dönt.

**Működési elv:**  
- Nem erőforrás-korlát, hanem elvi korlát.  
- A problémát nem lehet teljes általánosságban automatizálni.

**Egyszerű példa:**  
Általános programviselkedés sokszor nem dönthető el minden bemenetre.

**Vizsgán fontos kulcsszavak:**  
**[[eldönthetetlen probléma]]**, **elvi korlát**, **nincs teljes algoritmus**

---

### 2.2 Példák
**Rövid definíció:**  
Klasszikus eldönthetetlen feladat a **[[megállási probléma]]**.

**Működési elv:**  
- Nincs általános algoritmus, ami minden program-bemenet párra eldöntené, megáll-e a program.  
- Rice-tétel jellegű eredmények miatt sok nemtriviális programtulajdonság is eldönthetetlen.

**Egyszerű példa:**  
„Ez a tetszőleges program valaha kiírja-e az 1-et?” általánosan nem dönthető.

**Vizsgán fontos kulcsszavak:**  
**[[megállási probléma]]**, **Halting problem**, **Rice-tétel jelleg**

---

### 2.3 Következmény
**Rövid definíció:**  
Az eldönthetetlenség fő üzenete: a számíthatóságnak vannak elvi határai.

**Működési elv:**  
- Léteznek kérdések, amelyekre nincs univerzális algoritmus.  
- Ez kijelöli, meddig terjedhet automatizált problémamegoldás.

**Egyszerű példa:**  
Programellenőrzésnél sokszor csak részleges vagy közelítő analízist tudunk adni.

**Vizsgán fontos kulcsszavak:**  
**számíthatósági határ**, **algoritmikus korlát**, **részleges döntés**

---

## 3. Algoritmusok komplexitása

### 3.1 Időigény
**Rövid definíció:**  
Az időkomplexitás azt méri, hogyan nő a futási idő a bemenet méretével.

**Működési elv:**  
- Jelölés: `T(n)`.  
- Aszimptotikus vizsgálattal a nagy `n` viselkedés a fontos.

**Egyszerű példa:**  
Lineáris keresés időigénye tipikusan `O(n)`.

**Vizsgán fontos kulcsszavak:**  
**időkomplexitás**, **`T(n)`**, **bemenetméret**

---

### 3.2 Tárigény
**Rövid definíció:**  
A tárkomplexitás a memóriaigény növekedését írja le.

**Működési elv:**  
- Jelölés: `S(n)`.  
- Gyakran idő-tár kompromisszum figyelhető meg.

**Egyszerű példa:**  
Dinamikus programozás sok memóriát használhat időnyereségért.

**Vizsgán fontos kulcsszavak:**  
**tárkomplexitás**, **`S(n)`**, **memóriaigény**, **kompromisszum**

---

### 3.3 Aszimptotikus jelölések
**Rövid definíció:**  
Az aszimptotikus jelölések az algoritmus növekedési rendjét írják le.

**Működési elv:**  
- `O`: felső korlát.  
- `Ω`: alsó korlát.  
- `Θ`: szoros korlát.

**Egyszerű példa:**  
Merge sort időigénye `Θ(n log n)`.

**Vizsgán fontos kulcsszavak:**  
**O**, **Ω**, **Θ**, **növekedési rend**

---

## 4. P és NP osztályok

### 4.1 P osztály
**Rövid definíció:**  
A **[[P osztály]]** a determinisztikusan polinomiális időben megoldható döntési problémák halmaza.

**Működési elv:**  
- „Hatékonyan megoldható” problémák elméleti osztálya.  
- Determinisztikus Turing-géppel modellezett.

**Egyszerű példa:**  
Legrövidebb út klasszikus változatai P-ben vannak.

**Vizsgán fontos kulcsszavak:**  
**[[P osztály]]**, **polinomiális idő**, **determinista algoritmus**

---

### 4.2 NP osztály
**Rövid definíció:**  
Az **[[NP osztály]]** problémáinál egy adott megoldás polinomiális időben ellenőrizhető.

**Működési elv:**  
- Nemdeterminisztikus modellben polinomiális időben „megoldható”.  
- Gyakran tanú (certificate) ellenőrzési nézőpontból értelmezzük.

**Egyszerű példa:**  
Egy gráf Hamilton-kör jelöltje gyorsan ellenőrizhető, hogy valóban kör-e.

**Vizsgán fontos kulcsszavak:**  
**[[NP osztály]]**, **tanúellenőrzés**, **polinomiális verifikáció**, **nemdeterminizmus**

---

### 4.3 Kapcsolat
**Rövid definíció:**  
Biztos, hogy `P ⊆ NP`, de a `P = NP?` kérdés nyitott.

**Működési elv:**  
- Ha egyszer találnánk polinomiális algoritmust egy NP-teljes problémára, akkor `P=NP` lenne.  
- Ez a modern számítástudomány egyik legfontosabb nyitott kérdése.

**Egyszerű példa:**  
Jelenleg nincs ismert hatékony algoritmus minden NP-problémára.

**Vizsgán fontos kulcsszavak:**  
**`P ⊆ NP`**, **`P = NP?`**, **nyitott probléma**

---

## 5. Visszavezetések (reduction)

### 5.1 Fogalom
**Rövid definíció:**  
A **[[visszavezetés]]** egy probléma átalakítása egy másik problémára.

**Működési elv:**  
- Ha `A` visszavezethető `B`-re, és `B` megoldható, akkor `A` is megoldható.  
- Komplexitás-összehasonlítás kulcsa.

**Egyszerű példa:**  
Új probléma nehézségét ismert NP-teljes problémára visszavezetéssel mutatjuk.

**Vizsgán fontos kulcsszavak:**  
**[[visszavezetés]]**, **A -> B**, **nehézség-összehasonlítás**

---

### 5.2 Hatékony visszavezetés
**Rövid definíció:**  
Komplexitáselméletben a releváns visszavezetés polinomiális idejű.

**Működési elv:**  
- Az átalakítás költsége nem lehet túl nagy.  
- Így korrektül hasonlítható össze két probléma nehézsége.

**Egyszerű példa:**  
SAT-ból történő polinomiális transzformáció gyakori NP-teljességi bizonyításban.

**Vizsgán fontos kulcsszavak:**  
**polinomiális visszavezetés**, **komplexitási reláció**, **NP-bizonyítás**

---

## 6. NP-teljesség

### 6.1 NP-teljes problémák
**Rövid definíció:**  
Egy probléma **[[NP-teljes]]**, ha NP-ben van és minden NP-probléma polinomiálisan visszavezethető rá.

**Működési elv:**  
- Ezek az NP „legnehezebb” döntési problémái.  
- NP-teljességi bizonyítás tipikusan kétlépéses: `B ∈ NP` és `A <=_p B`.

**Egyszerű példa:**  
SAT az elsőként bizonyított NP-teljes probléma.

**Vizsgán fontos kulcsszavak:**  
**[[NP-teljes]]**, **`∈ NP`**, **minden NP visszavezethető**

---

### 6.2 Jelentőség
**Rövid definíció:**  
Az NP-teljes problémák kulcsszerepűek, mert rajtuk keresztül osztályozzuk a nehézséget.

**Működési elv:**  
- Egyetlen NP-teljes probléma polinomiális megoldása áttörés lenne: `P=NP`.  
- Emiatt gyakran közelítő vagy heurisztikus módszereket használunk.

**Egyszerű példa:**  
Nagy SAT példányokra tipikusan nem pontos polinomiális algoritmusokat futtatunk.

**Vizsgán fontos kulcsszavak:**  
**nehéz NP problémák**, **`P=NP` következmény**, **heurisztika**

---

### 6.3 Példák
**Rövid definíció:**  
Számos klasszikus kombinatorikus feladat NP-teljes döntési változatban.

**Működési elv:**  
- SAT, Hamilton-kör, döntési hátizsák gyakori tankönyvi példák.  
- Ezeken demonstrálható visszavezetéses bizonyítás.

**Egyszerű példa:**  
„Létezik-e Hamilton-kör?” igen/nem kérdésként NP-teljes.

**Vizsgán fontos kulcsszavak:**  
**SAT**, **Hamilton-kör**, **hátizsák (döntési)**

---

## 7. NP-nehéz problémák
**Rövid definíció:**  
Az **[[NP-nehéz]]** problémák legalább olyan nehezek, mint az NP-teljes problémák.

**Működési elv:**  
- Nem kötelező, hogy NP-ben legyenek.  
- Lehetnek optimalizálási vagy akár nem döntési problémák is.

**Egyszerű példa:**  
TSP optimalizálási változata NP-nehéz, döntési változata NP-teljes.

**Vizsgán fontos kulcsszavak:**  
**[[NP-nehéz]]**, **NP-teljeshez viszonyítás**, **nem feltétlen döntési**

---

## 8. Összefüggések
**Rövid definíció:**  
A számítástudomány itt két fő kérdést vizsgál: megoldható-e egyáltalán, és ha igen, mennyire hatékonyan.

**Működési elv:**  
- Eldönthetőség: van-e mindig megálló helyes algoritmus.  
- Komplexitás: mennyi idő/memória kell.  
- P vs NP és NP-teljesség: hatékonysági határok feltérképezése.

**Egyszerű példa:**  
Lehet egy probléma eldönthető, de gyakorlatban túl lassú nagy bemenetre.

**Vizsgán fontos kulcsszavak:**  
**eldönthetőség vs komplexitás**, **hatékonysági határ**, **osztályozás**

---

## + Vizsgán érdemes még megemlíteni
- A **[[megállási probléma]]** mutatja a számíthatóság elvi határát.  
- `P vs NP` kérdés gyakorlati hatása óriási (optimalizálás, kriptográfia).  
- Visszavezetés a nehézségbizonyítás alaptechnikája.  
- NP-teljes problémák kiemelt szerepűek algoritmus-tervezésben.

---

## Rövid szóbeli összefoglaló
Az eldönthetőség azt vizsgálja, hogy létezik-e algoritmus, ami minden bemenetre megáll és helyesen dönt. Vannak eldönthetetlen problémák is, például a megállási probléma, ami megmutatja a számíthatóság határait. Ha egy probléma eldönthető, még kérdés a hatékonyság, ezt a komplexitáselmélet írja le aszimptotikus jelölésekkel. A P osztály polinomiális időben megoldható problémákat tartalmaz, az NP osztályban pedig a megoldás polinomiális időben ellenőrizhető. Tudjuk, hogy `P ⊆ NP`, de a `P=NP?` kérdés nyitott. Az NP-teljesség visszavezetésekkel bizonyítható, és megmutatja a „legnehezebb” NP problémákat.

## Kulcsfogalmak
- [[eldönthetőség]]
- [[eldöntési probléma]]
- [[Turing-gép]]
- [[eldönthetetlen probléma]]
- [[megállási probléma]]
- [[időkomplexitás]]
- [[tárkomplexitás]]
- [[P osztály]]
- [[NP osztály]]
- [[P = NP]]
- [[visszavezetés]]
- [[polinomiális visszavezetés]]
- [[NP-teljes]]
- [[NP-nehéz]]
- [[SAT]]

## Tipikus vizsgakérdések
1. **Mi az eldönthető probléma definíciója?**  
   Olyan döntési probléma, amelyre van mindig megálló és helyes algoritmus.

2. **Mit jelent az eldönthetetlenség?**  
   Hogy nem létezik általános algoritmus, ami minden bemenetre dönt.

3. **Mi a megállási probléma lényege?**  
   Nem dönthető el általánosan, hogy egy program adott bemenetre megáll-e.

4. **Mit jelent a P osztály?**  
   Polinomiális időben determinisztikusan megoldható döntési problémák halmaza.

5. **Mit jelent az NP osztály?**  
   Olyan problémák osztálya, ahol egy megoldás polinomiális időben ellenőrizhető.

6. **Miért fontos a visszavezetés?**  
   Mert ezzel hasonlítjuk össze problémák nehézségét és bizonyítjuk az NP-teljességet.

7. **Mi az NP-teljes és NP-nehéz közti különbség?**  
   NP-teljes: NP-ben is van és NP-nehéz; NP-nehéz nem feltétlenül NP-beli.

## Minimum, amit tudni kell
- Eldöntési probléma és eldönthetőség fogalma.  
- Eldönthetetlen probléma jelentése és halting példa.  
- Idő- és tárkomplexitás alapötlete.  
- O, Ω, Θ jelölések szerepe.  
- P és NP osztály definíciója.  
- `P ⊆ NP` és a `P=NP?` nyitott kérdés.  
- Polinomiális visszavezetés lényege.  
- NP-teljes és NP-nehéz különbsége, legalább egy példával.
