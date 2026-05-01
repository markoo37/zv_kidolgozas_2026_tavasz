# Operációkutatás – 11. tétel
## Egészértékű feladatok, B&B, hátizsák, hozzárendelési feladat

---

## 1. Egészértékű programozás (IP)

### 1.1 Alapfogalom
**Rövid definíció:**  
Az **[[egészértékű programozás]]** (IP) olyan optimalizálási modell, ahol a döntési változók egész értékeket vehetnek fel.

**Működési elv:**  
- Az LP modell kiegészül integritási feltétellel: `x in Z`.  
- Diszkrét döntések modellezésére alkalmas (igen/nem, darabszám).

**Egyszerű példa:**  
Nem lehet 2.7 darab gépet venni, csak egész számú egységet.

**Vizsgán fontos kulcsszavak:**  
**[[egészértékű programozás]]**, **integritási feltétel**, **diszkrét döntés**

---

### 1.2 Típusok
**Rövid definíció:**  
IP lehet tiszta vagy vegyes egészértékű.

**Működési elv:**  
- Tiszta IP: minden változó egész.  
- **[[MILP]]**: csak a változók egy része egész, mások folytonosak.

**Egyszerű példa:**  
Beruházási döntés bináris, termelési mennyiség folytonos -> MILP.

**Vizsgán fontos kulcsszavak:**  
**tiszta IP**, **[[MILP]]**, **egész + folytonos változók**

---

### 1.3 Nehézség
**Rövid definíció:**  
Az egészértékű feladatok általában jóval nehezebbek, mint az LP.

**Működési elv:**  
- Sok IP probléma **[[NP-nehéz]]**.  
- LP-szimplex közvetlenül csak relaxációra használható.

**Egyszerű példa:**  
Nagy bináris döntési modellek gyorsan kombinatorikusan robbannak.

**Vizsgán fontos kulcsszavak:**  
**NP-nehézség**, **LP relaxáció**, **kombinatorikus robbanás**

---

## 2. Branch and Bound (B&B)

### 2.1 Alapötlet
**Rövid definíció:**  
A **[[Branch and Bound]]** faalapú pontos keresési stratégia egészértékű feladatokra.

**Működési elv:**  
- A problémát részproblémákra bontjuk (branch).  
- Korlátokkal levágjuk a reménytelen ágakat (bound).

**Egyszerű példa:**  
Bináris változóra ágazunk: `x_i=0` és `x_i=1`.

**Vizsgán fontos kulcsszavak:**  
**[[Branch and Bound]]**, **keresési fa**, **elágazás**, **levágás**

---

### 2.2 Lépések
**Rövid definíció:**  
A B&B iteratívan old LP-relaxációkat és osztja tovább a nem egész megoldásokat.

**Működési elv:**  
- Relaxált LP megoldás.  
- Ha egész: jelölt optimum.  
- Ha törtes: új ágak extra korlátokkal.

**Egyszerű példa:**  
`x=3.4` esetén két ág: `x<=3` és `x>=4`.

**Vizsgán fontos kulcsszavak:**  
**LP relaxáció**, **egész megoldás teszt**, **branch lépés**, **korlátozás**

---

### 2.3 Korlátozás (bound)
**Rövid definíció:**  
A bound célja, hogy ne kelljen minden ágat végigvizsgálni.

**Működési elv:**  
- Minden csomóponthoz korlát tartozik.  
- Ha biztosan nem lehet jobb az aktuális legjobbnál, az ág eldobható.

**Egyszerű példa:**  
Maximalizálásnál, ha csomópont felső korlátja kisebb a jelenlegi legjobb értéknél, prune-olunk.

**Vizsgán fontos kulcsszavak:**  
**felső/alsó korlát**, **pruning**, **áglevágás**

---

### 2.4 Előnyök / hátrányok
**Rövid definíció:**  
A B&B pontos, de potenciálisan drága számítási módszer.

**Működési elv:**  
- Előny: garantált optimum (ha lefut).  
- Hátrány: nagy probléma esetén sok csomópont.

**Egyszerű példa:**  
Kis-közepes méretben jól működik, nagyban heurisztikákkal segítik.

**Vizsgán fontos kulcsszavak:**  
**pontos módszer**, **számítási igény**, **skálázási nehézség**

---

## 3. Hátizsák probléma (Knapsack)

### 3.1 Alapfeladat
**Rövid definíció:**  
A **[[hátizsák probléma]]** célja tárgyak kiválasztása kapacitáskorlát mellett maximális értékre.

**Működési elv:**  
- Minden tárgynak súlya és értéke van.  
- A kiválasztott összsúly nem lépheti túl a kapacitást.

**Egyszerű példa:**  
Adott hátizsákba úgy pakolunk, hogy a legnagyobb összértéket vigyük.

**Vizsgán fontos kulcsszavak:**  
**[[hátizsák probléma]]**, **kapacitáskorlát**, **értékmaximalizálás**

---

### 3.2 Típusok
**Rövid definíció:**  
A hátizsák feladatnak diszkrét és folytonos jellegű változatai vannak.

**Működési elv:**  
- **0-1**: tárgy vagy bekerül, vagy nem.  
- **Tört**: tárgy osztható, részben is vihető.

**Egyszerű példa:**  
Aranyrúd darabolható (tört), laptop nem (0-1).

**Vizsgán fontos kulcsszavak:**  
**0-1 hátizsák**, **tört hátizsák**, **diszkrét vs osztható**

---

### 3.3 Megoldási módszerek
**Rövid definíció:**  
A módszerválasztás a feladatváltozattól és mérettől függ.

**Működési elv:**  
- 0-1 változatra DP és B&B gyakori.  
- Tört változatra greedy optimális.

**Egyszerű példa:**  
Érték/súly arány szerinti rendezés tört hátizsáknál optimális megoldást ad.

**Vizsgán fontos kulcsszavak:**  
**dinamikus programozás**, **greedy**, **B&B**, **módszerválasztás**

---

## 4. Hozzárendelési feladat

### 4.1 Alapfogalom
**Rövid definíció:**  
A **[[hozzárendelési feladat]]** célja feladatok és erőforrások optimális párosítása minimális költséggel.

**Működési elv:**  
- Költségmátrix adja az egyes párosítások költségét.  
- Minden feladatot pontosan egy erőforráshoz rendelünk.

**Egyszerű példa:**  
Munkatársakat rendeljünk munkákhoz a legkisebb összidővel.

**Vizsgán fontos kulcsszavak:**  
**[[hozzárendelési feladat]]**, **költségmátrix**, **minimális összköltség**

---

### 4.2 Matematikai modell
**Rövid definíció:**  
A modell kétoldali egyértelmű hozzárendelést ír elő.

**Működési elv:**  
- Sor- és oszlopkorlátok biztosítják az 1-1 megfelelést.  
- Tipikusan bináris döntési változókkal írjuk fel.

**Egyszerű példa:**  
`x_ij=1`, ha `i` feladatot `j` erőforrás kapja.

**Vizsgán fontos kulcsszavak:**  
**1-1 hozzárendelés**, **bináris változó**, **korlátok**

---

## 5. Magyar módszer (Hungarian algorithm)

### 5.1 Alapötlet
**Rövid definíció:**  
A **[[magyar módszer]]** speciális polinomiális algoritmus hozzárendelési feladatra.

**Működési elv:**  
- Költségmátrixot transzformál úgy, hogy az optimum megmaradjon.  
- Nullák szerkezetén keresztül keresi az optimális párosítást.

**Egyszerű példa:**  
Sor- és oszlopminimum kivonással nullákat hozunk létre a döntéshez.

**Vizsgán fontos kulcsszavak:**  
**[[magyar módszer]]**, **mátrixtranszformáció**, **optimális hozzárendelés**

---

### 5.2 Lépések
**Rövid definíció:**  
A módszer lépései strukturált mátrixredukciót követnek.

**Működési elv:**  
- Sorminimum, majd oszlopminimum kivonás.  
- Nullák lefedése minimális vonalszámmal.  
- Ha kell, további redukció és ismétlés.

**Egyszerű példa:**  
Addig módosítjuk a mátrixot, amíg kiválasztható teljes független nullahalmaz.

**Vizsgán fontos kulcsszavak:**  
**sor/ oszlop redukció**, **nullák lefedése**, **iteratív finomítás**

---

### 5.3 Tulajdonságok
**Rövid definíció:**  
A magyar módszer garantáltan optimális megoldást ad hozzárendelési feladatra.

**Működési elv:**  
- Polinomiális futásidejű, ezért jól használható közepes-nagy méretekre is.

**Egyszerű példa:**  
N x N költségmátrixon megbízhatóbb és gyorsabb, mint általános IP-fakeresés.

**Vizsgán fontos kulcsszavak:**  
**optimális garancia**, **polinomiális idő**, **speciális algoritmus**

---

## 6. Összefüggések
**Rövid definíció:**  
Az IP általános keret, amelyben speciális feladatok eltérő hatékony módszereket kaphatnak.

**Működési elv:**  
- B&B általános pontos stratégia IP-re.  
- Hátizsák és hozzárendelés speciális szerkezetű részterületek.  
- Speciális szerkezetnél specializált algoritmus jobb lehet.

**Egyszerű példa:**  
Hozzárendelésre magyar módszer gyorsabb, mint általános B&B IP modell.

**Vizsgán fontos kulcsszavak:**  
**általános vs speciális módszer**, **modell és algoritmus illesztés**

---

## + Vizsgán érdemes még megemlíteni
- Relaxáció adja a B&B csomópont-korlátok alapját.  
- IP nehézsége miatt fontosak a jó korlátok és heurisztikák.  
- Greedy és DP különbsége hátizsák példán jól mutatható.  
- Magyar módszer különlegessége: speciális feladatra polinomiális optimum.

---

## Rövid szóbeli összefoglaló
Az egészértékű programozás lineáris modell, de a változók egész értékre korlátozottak, ezért jóval nehezebb, mint a klasszikus LP. Általános pontos megoldási stratégia a Branch and Bound, ahol LP-relaxációkat oldunk, majd elágazással és korlátokkal vágjuk le a rossz ágakat. A hátizsák feladat tipikus speciális IP, 0-1 változata NP-nehéz, tört változata viszont greedyn optimálisan megoldható. A hozzárendelési feladat szintén speciális modell, amelyre a magyar módszer hatékony, polinomiális és optimális megoldást ad. A lényeg, hogy a modell általánossága és a feladat szerkezete együtt határozza meg a legjobb algoritmust.

## Kulcsfogalmak
- [[egészértékű programozás]]
- [[MILP]]
- [[LP relaxáció]]
- [[Branch and Bound]]
- [[korlát (bound)]]
- [[pruning]]
- [[hátizsák probléma]]
- [[0-1 hátizsák]]
- [[tört hátizsák]]
- [[dinamikus programozás]]
- [[hozzárendelési feladat]]
- [[költségmátrix]]
- [[magyar módszer]]
- [[NP-nehéz]]
- [[optimális hozzárendelés]]

## Tipikus vizsgakérdések
1. **Mi a különbség LP és IP között?**  
   IP-ben a változók egész értékűek, ezért diszkrét és nehezebb feladat.

2. **Miért használunk LP-relaxációt B&B-ben?**  
   Mert korlátot ad a csomópontra, ami segíti az ágak levágását.

3. **Mikor fogad el megoldást a B&B?**  
   Ha a relaxált csomópont optimális megoldása egész értékű.

4. **Mi a hátizsák feladat célja?**  
   Kapacitáskorlát mellett maximális összérték elérése.

5. **Mi a 0-1 és tört hátizsák különbsége?**  
   0-1-ben tárgy nem osztható, törtben osztható.

6. **Milyen feladatra jó a magyar módszer?**  
   Hozzárendelési feladatra, minimális összköltségű párosításra.

7. **Miért különleges a magyar módszer?**  
   Mert speciális feladatra garantált optimális és polinomiális idejű.

## Minimum, amit tudni kell
- IP fogalma és típusai (tiszta, MILP).  
- Miért nehezebb az IP, mint az LP.  
- B&B alapötlete: branch + bound + pruning.  
- LP-relaxáció szerepe B&B-ben.  
- Hátizsák feladat alapmodellje és két fő változata.  
- 0-1 hátizsákra DP, törtre greedy alapötlet.  
- Hozzárendelési feladat definíciója költségmátrixszal.  
- Magyar módszer fő lépései és optimális/polinomiális tulajdonsága.
