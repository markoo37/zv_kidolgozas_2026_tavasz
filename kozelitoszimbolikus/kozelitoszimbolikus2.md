# Numerikus számítások – 6. tétel
## Sajátértékek, polinomok, interpoláció

---

## 1. Sajátértékek és sajátvektorok

### 1.1 Alapfogalom
**Rövid definíció:**  
Egy `A` mátrix **[[sajátérték]]e** és **[[sajátvektor]]a** akkor teljesíti a kapcsolatot, ha `Ax = λx`, ahol `x != 0`.

**Működési elv:**  
- A mátrixhatás nem forgatja el a sajátvektort, csak skálázza.  
- A skálázási tényező a sajátérték `λ`.  
- Sok lineáris transzformáció elemzésének alapja.

**Egyszerű példa:**  
Ha egy irányban a transzformáció kétszerezi a vektor hosszát, akkor ebben az irányban `λ = 2`.

**Vizsgán fontos kulcsszavak:**  
**[[sajátérték]]**, **[[sajátvektor]]**, **`Ax=λx`**, **nemnulla vektor**

---

### 1.2 Karakterisztikus egyenlet
**Rövid definíció:**  
A sajátértékeket a **[[karakterisztikus egyenlet]]** gyökei adják: `det(A - λI) = 0`.

**Működési elv:**  
- A determináns nullává válása jelzi, hogy van nemtriviális megoldás az `(A-λI)x=0` rendszerre.  
- A kapott `λ` értékek a mátrix spektrumát adják.

**Egyszerű példa:**  
2x2-es mátrixnál másodfokú polinom adódik, ennek gyökei a sajátértékek.

**Vizsgán fontos kulcsszavak:**  
**[[karakterisztikus egyenlet]]**, **determináns**, **`det(A-λI)=0`**, **spektrum**

---

### 1.3 Numerikus meghatározás

#### Hatványmódszer (Power method)
**Rövid definíció:**  
A **[[hatványmódszer]]** iteratív eljárás a domináns (legnagyobb abszolút értékű) sajátérték becslésére.

**Működési elv:**  
- Ismételten szorozzuk a vektort a mátrixszal: `x_(k+1) ~ A x_k`.  
- Minden lépésben normalizálunk a numerikus stabilitás miatt.  
- Konvergencia feltétele, hogy legyen domináns sajátérték.

**Egyszerű példa:**  
Nagy ritka mátrixnál gyorsan becsülhető a legnagyobb sajátérték.

**Vizsgán fontos kulcsszavak:**  
**[[hatványmódszer]]**, **iteráció**, **domináns sajátérték**, **normalizálás**

#### Inverz hatványmódszer
**Rövid definíció:**  
Az **[[inverz hatványmódszer]]** a kisebb sajátértékek keresésére alkalmas.

**Működési elv:**  
- Az `A^-1` mátrix domináns sajátértéke az eredeti legkisebb sajátértékhez kapcsolódik.  
- Eltolásos (shiftelt) változattal célzottan kereshető adott tartomány közeli sajátérték.

**Egyszerű példa:**  
Stabilitásvizsgálatnál a nullához közeli sajátértékek keresése shiftelt inverz módszerrel történhet.

**Vizsgán fontos kulcsszavak:**  
**[[inverz hatványmódszer]]**, **legkisebb sajátérték**, **shift**

#### QR-algoritmus (említés)
**Rövid definíció:**  
A **[[QR-algoritmus]]** általános sajátérték-számító iteratív módszer.

**Működési elv:**  
- Ismételt QR-felbontásra és szorzásra épül.  
- Széles körben használt numerikus eljárás.

**Egyszerű példa:**  
Sűrű mátrixok teljes spektrumának meghatározására tipikus választás.

**Vizsgán fontos kulcsszavak:**  
**[[QR-algoritmus]]**, **iteratív spektrumszámítás**, **mátrixfelbontás**

---

### 1.4 Tulajdonságok
**Rövid definíció:**  
A sajátértékprobléma fontos szerkezeti tulajdonságokat ad a mátrixról.

**Működési elv:**  
- Szimmetrikus mátrixnál különböző sajátértékhez tartozó sajátvektorok ortogonálisak.  
- A sajátértékek halmaza a spektrum.  
- Sok alkalmazásban kulcsszerepű.

**Egyszerű példa:**  
PCA dimenziócsökkentésnél a kovarianciamátrix sajátértékei mutatják a fő irányok jelentőségét.

**Vizsgán fontos kulcsszavak:**  
**ortogonalitás**, **spektrum**, **szimmetrikus mátrix**, **PCA**

---

## 2. Polinomok és zérushelyek

### 2.1 Alapfogalmak
**Rövid definíció:**  
A **[[polinom]]** hatványfüggvények lineáris kombinációja.

**Működési elv:**  
- Fokszám: legnagyobb nemnulla kitevő.  
- Együtthatók határozzák meg az alakját.

**Egyszerű példa:**  
`p(x)=2x^3-5x+1` harmadfokú polinom.

**Vizsgán fontos kulcsszavak:**  
**[[polinom]]**, **fokszám**, **együttható**

---

### 2.2 Zérushely (gyök)
**Rövid definíció:**  
A polinom **[[zérushelye]]** olyan `x`, amelyre `p(x)=0`.

**Működési elv:**  
- Gyök lehet valós vagy komplex.  
- Numerikusan gyakran közelítő módszerrel keressük.

**Egyszerű példa:**  
`x^2-4=0` gyökei: `x=2` és `x=-2`.

**Vizsgán fontos kulcsszavak:**  
**[[zérushely]]**, **gyök**, **valós/komplex megoldás**

---

### 2.3 Numerikus gyökkeresés

#### Intervallumfelezés (bisection)
**Rövid definíció:**  
Az **[[intervallumfelezés]]** megbízható gyökkereső módszer előjelváltásos intervallumban.

**Működési elv:**  
- Folytonos függvény és `f(a)*f(b)<0` feltétel kell.  
- Intervallumot felezzük, mindig megtartva az előjelváltást tartalmazó részt.  
- Biztosan konvergál, de lassabb.

**Egyszerű példa:**  
`[1,2]` intervallumban, ha előjelváltás van, a gyök fokozatosan közelíthető.

**Vizsgán fontos kulcsszavak:**  
**[[intervallumfelezés]]**, **előjelváltás**, **biztos konvergencia**

#### Newton-módszer
**Rövid definíció:**  
A **[[Newton-módszer]]** deriváltat használó iteratív gyökkeresés.

**Működési elv:**  
- Érintőegyenes metszéspontjával képez új közelítést.  
- Jó kezdőértéknél nagyon gyors (kvadratikus) konvergencia.  
- Rossz kezdőértéknél divergens is lehet.

**Egyszerű példa:**  
`f(x)=x^2-2` gyökét néhány lépésben pontosan közelíti.

**Vizsgán fontos kulcsszavak:**  
**[[Newton-módszer]]**, **derivált**, **kvadratikus konvergencia**, **kezdőérték-érzékenység**

#### Szelő módszer (említés)
**Rövid definíció:**  
A **[[szelő módszer]]** derivált nélküli, két kezdőértéket használó gyökkeresés.

**Működési elv:**  
- A deriváltat két pontból közelíti.  
- Gyakran gyorsabb bisectionnél, de kevésbé robusztus.

**Egyszerű példa:**  
Ha derivált nehezen számolható, szelő módszer praktikus lehet.

**Vizsgán fontos kulcsszavak:**  
**[[szelő módszer]]**, **derivált nélkül**, **két kezdőérték**

---

## 3. Interpoláció

### 3.1 Alapprobléma
**Rövid definíció:**  
Az **[[interpoláció]]** célja olyan függvény (gyakran polinom) keresése, amely átmegy adott pontokon.

**Működési elv:**  
- `n+1` különböző `x_i` pontra létezik egyértelmű, legfeljebb `n` fokú interpolációs polinom.  
- Pontos illesztést ad a mintapontokra.

**Egyszerű példa:**  
Mért adatok köztes értékének becslése ismert pontok között.

**Vizsgán fontos kulcsszavak:**  
**[[interpoláció]]**, **illesztés**, **interpolációs polinom**, **egyértelműség**

---

### 3.2 Lagrange-interpoláció
**Rövid definíció:**  
A **[[Lagrange-interpoláció]]** explicit képletet ad az interpolációs polinomra.

**Működési elv:**  
- `L(x)=Σ y_i·l_i(x)` alak, ahol `l_i(x)` alappolinomok.  
- Minden alappolinom saját pontján 1, a többin 0.

**Egyszerű példa:**  
3 pontból másodfokú Lagrange-polinom építhető.

**Vizsgán fontos kulcsszavak:**  
**[[Lagrange-interpoláció]]**, **alappolinom**, **`L(x)=Σ y_i l_i(x)`**

---

### 3.3 Tulajdonságok
**Rövid definíció:**  
Az interpoláció pontos a mintapontokra, de magas fokon numerikus problémák jelenhetnek meg.

**Működési elv:**  
- Nagy fokszám és egyenletesen osztott pontok esetén oszcilláció léphet fel (**[[Runge-jelenség]]**).  
- Emiatt gyakran darabos közelítést (pl. spline) választunk.

**Egyszerű példa:**  
Sok ponton egyetlen magas fokú polinom helyett több alacsony fokú szakasz stabilabb.

**Vizsgán fontos kulcsszavak:**  
**pontos illesztés**, **[[Runge-jelenség]]**, **magas fok problémája**, **numerikus költség**

---

## 4. Numerikus szempontok
**Rövid definíció:**  
A numerikus módszerek használatánál a pontosság és megbízhatóság legalább olyan fontos, mint maga a képlet.

**Működési elv:**  
- Kerekítési hibák halmozódhatnak.  
- Stabil módszer kevésbé erősíti fel a hibát.  
- Konvergencia és hibabecslés alapján ítélhető meg az eredmény minősége.

**Egyszerű példa:**  
Két módszer közül a lassabb, de stabilabb adhat jobb gyakorlati eredményt.

**Vizsgán fontos kulcsszavak:**  
**kerekítési hiba**, **stabilitás**, **konvergencia**, **hibabecslés**

---

## + Vizsgán érdemes még megemlíteni
- Sajátértékek alkalmazása: pl. **PCA**, rezgésanalízis, rendszerstabilitás.  
- Newton gyors, de jó kezdőérték kell.  
- **Interpoláció vs approximáció**: ponton átmegy vs közelít.  
- Gyakorlati numerikus kompromisszumok (pontosság-idő).

---

## Rövid szóbeli összefoglaló
A sajátérték-sajátvektor probléma alapegyenlete az `Ax=λx`, a sajátértékeket karakterisztikus egyenletből vagy numerikusan, például hatványmódszerrel számoljuk. Polinomoknál a zérushelyek keresése tipikus feladat, erre használható a biztos, de lassabb intervallumfelezés és a gyorsabb, de érzékeny Newton-módszer. Interpolációnál adott pontokra pontosan illeszkedő polinomot keresünk, klasszikus módszer a Lagrange-alak. Magas foknál azonban oszcilláció, például Runge-jelenség jelentkezhet. A gyakorlati numerikus számításban mindig figyelni kell a stabilitásra, konvergenciára és hibabecslésre.

## Kulcsfogalmak
- [[sajátérték]]
- [[sajátvektor]]
- [[karakterisztikus egyenlet]]
- [[hatványmódszer]]
- [[inverz hatványmódszer]]
- [[QR-algoritmus]]
- [[polinom]]
- [[zérushely]]
- [[intervallumfelezés]]
- [[Newton-módszer]]
- [[szelő módszer]]
- [[interpoláció]]
- [[Lagrange-interpoláció]]
- [[Runge-jelenség]]
- [[konvergencia]]

## Tipikus vizsgakérdések
1. **Mit jelent az `Ax=λx` egyenlet?**  
   A mátrix egy sajátvektort csak skáláz, a skálázási tényező a sajátérték.

2. **Hogyan kapjuk a sajátértékeket elméletben?**  
   A `det(A-λI)=0` karakterisztikus egyenlet gyökeiből.

3. **Mire jó a hatványmódszer?**  
   A domináns sajátérték és sajátvektor numerikus közelítésére.

4. **Mi a bisection és Newton fő különbsége?**  
   Bisection biztosan konvergál előjelváltással, Newton gyorsabb, de érzékenyebb.

5. **Mi az interpoláció célja?**  
   Olyan függvény találása, ami pontosan átmegy adott pontokon.

6. **Mi a Lagrange-interpoláció lényege?**  
   Alappolinomok lineáris kombinációjával közvetlenül felírja az interpoláló polinomot.

7. **Mi a Runge-jelenség?**  
   Magas fokú polinom interpolációnál fellépő oszcilláció a széleken.

## Minimum, amit tudni kell
- Sajátérték/sajátvektor definíció és `Ax=λx` alak.  
- Karakterisztikus egyenlet jelentése.  
- Hatványmódszer alapötlete.  
- Polinom gyök fogalma és két gyökkereső módszer lényege.  
- Intervallumfelezés és Newton előny-hátrány.  
- Interpoláció fogalma és Lagrange alapképlete említési szinten.  
- Runge-jelenség rövid magyarázata.  
- Stabilitás és konvergencia jelentősége numerikus módszereknél.
