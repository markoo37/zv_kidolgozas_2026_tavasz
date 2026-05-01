# Numerikus számítások – 7. tétel
## Iterációs módszerek, gyökkeresés, gradiens módszerek, integrálás

---

## 1. Iterációs módszerek lineáris egyenletrendszerekre

### 1.1 Alapfogalom
**Rövid definíció:**  
Iterációs módszereknél a `Ax=b` rendszer megoldását ismételt közelítéssel számítjuk.

**Működési elv:**  
- Kezdővektorból indulunk: `x^(0)`.  
- Iteráció: `x^(k+1)=f(x^(k))`.  
- Cél, hogy a sorozat a pontos megoldáshoz konvergáljon.

**Egyszerű példa:**  
Nagy ritka mátrixoknál iterációs módszer gyakran praktikusabb, mint direkt felbontás.

**Vizsgán fontos kulcsszavak:**  
**iterációs módszer**, **`Ax=b`**, **kezdőérték**, **konvergencia**

---

### 1.2 Jacobi-módszer
**Rövid definíció:**  
A **[[Jacobi-módszer]]** klasszikus iteratív eljárás lineáris rendszerekre.

**Működési elv:**  
- Mátrixfelbontás: `A = D + L + U`.  
- Iteráció: `x^(k+1)=D^-1(b-(L+U)x^(k))`.  
- Minden komponens az előző iteráció értékeit használja -> jól párhuzamosítható.

**Egyszerű példa:**  
Többmagos környezetben egyszerre frissíthetők a komponensek, de általában lassabban konvergál, mint Gauss–Seidel.

**Vizsgán fontos kulcsszavak:**  
**[[Jacobi-módszer]]**, **`A=D+L+U`**, **párhuzamosíthatóság**, **lassabb konvergencia**

---

### 1.3 Gauss–Seidel módszer
**Rövid definíció:**  
A **[[Gauss–Seidel]]** módszer az újonnan kiszámolt komponenseket azonnal felhasználja.

**Működési elv:**  
- Iteráción belül balról jobbra haladva frissítünk.  
- Ez gyakran gyorsabb konvergenciát ad, mint Jacobi.  
- Sorrendfüggő és kevésbé párhuzamosítható.

**Egyszerű példa:**  
Ugyanarra a rendszerre kevesebb iterációval elérheti a kívánt pontosságot, mint Jacobi.

**Vizsgán fontos kulcsszavak:**  
**[[Gauss–Seidel]]**, **azonnali frissítés**, **gyorsabb konvergencia**, **sorrendfüggés**

---

### 1.4 Konvergencia
**Rövid definíció:**  
Konvergencia azt jelenti, hogy az iterációk hibája tart a nullához.

**Működési elv:**  
- Elégséges feltétel lehet a diagonális dominancia.  
- Spektrális sugár (iterációs mátrix) alapján is vizsgálható.  
- Gyakorlatban hibakritériummal állítjuk le az iterációt.

**Egyszerű példa:**  
Ha a mátrix erősen diagonálisan domináns, Jacobi/Gauss–Seidel tipikusan stabilan konvergál.

**Vizsgán fontos kulcsszavak:**  
**konvergencia**, **diagonális dominancia**, **spektrális sugár**, **hibakritérium**

---

## 2. Nemlineáris egyenletek gyökkeresése

### 2.1 Érintő módszer (Newton-módszer)
**Rövid definíció:**  
A **[[Newton-módszer]]** deriváltat használó gyors gyökkereső iteráció.

**Működési elv:**  
- Képlet: `x_(k+1)=x_k-f(x_k)/f'(x_k)`.  
- Jó kezdőértéknél kvadratikus konvergencia.  
- Derivált kell, és érzékeny lehet a kezdeti becslésre.

**Egyszerű példa:**  
`x^2-2=0` gyöke gyorsan közelíthető néhány Newton-lépéssel.

**Vizsgán fontos kulcsszavak:**  
**[[Newton-módszer]]**, **érintőmódszer**, **kvadratikus konvergencia**, **kezdőérték**

---

### 2.2 Szelő módszer
**Rövid definíció:**  
A **[[szelő módszer]]** derivált nélküli közelítés két pontból vett szelővel.

**Működési elv:**  
- Két kezdőértékből indul.  
- A deriváltat különbségi hányadossal helyettesíti.  
- Gyakran gyorsabb bisectionnél, de nem mindig konvergál.

**Egyszerű példa:**  
Olyan függvénynél hasznos, ahol derivált számítása drága vagy nehéz.

**Vizsgán fontos kulcsszavak:**  
**[[szelő módszer]]**, **derivált nélküli**, **két kezdőpont**, **nem garantált konvergencia**

---

### 2.3 Húrmódszer (regula falsi)
**Rövid definíció:**  
A **[[regula falsi]]** (húrmódszer) intervallum alapú gyökkeresés előjelváltással.

**Működési elv:**  
- A gyököt tartalmazó intervallumot megőrzi.  
- Stabilabb, mint a szelő módszer, de lassabban haladhat.

**Egyszerű példa:**  
Biztonságosabb választás, ha fontos az intervallumos kontroll.

**Vizsgán fontos kulcsszavak:**  
**[[regula falsi]]**, **intervallumos módszer**, **előjelváltás**, **stabilitás**

---

## 3. Gradiens alapú módszerek

### 3.1 Alapfogalom
**Rövid definíció:**  
A gradiens módszerek célja egy függvény minimumának megtalálása.

**Működési elv:**  
- A **[[gradiens]]** a legnagyobb növekedés irányát mutatja.  
- Minimumkeresésnél ennek ellentett irányába lépünk.

**Egyszerű példa:**  
Hegyről lefelé haladunk a legmeredekebb lejtő irányába.

**Vizsgán fontos kulcsszavak:**  
**gradiens**, **minimumkeresés**, **optimalizálás**

---

### 3.2 Gradiens módszer
**Rövid definíció:**  
A **[[gradiens módszer]]** iteratív optimalizáló eljárás.

**Működési elv:**  
- Iteráció: `x_(k+1)=x_k-α∇f(x_k)`.  
- `α` lépésköz kulcsfontosságú: túl nagy -> instabil, túl kicsi -> lassú.  
- Konvergencia függ a függvény és lépésköz tulajdonságaitól.

**Egyszerű példa:**  
Lineáris regresszió paramétereit gradiens módszerrel tanítjuk.

**Vizsgán fontos kulcsszavak:**  
**[[gradiens módszer]]**, **lépésköz**, **`x_(k+1)=x_k-α∇f`**, **konvergencia**

---

### 3.3 Alkalmazások
**Rövid definíció:**  
A gradiens alapú eljárások széles körben használt numerikus optimalizálók.

**Működési elv:**  
- Legkisebb négyzetes illesztésben és gépi tanulásban alapmódszer.  
- Magas dimenzióban is működőképes.

**Egyszerű példa:**  
Neurális hálózat tanításában a veszteségfüggvény minimumát keressük.

**Vizsgán fontos kulcsszavak:**  
**legkisebb négyzetek**, **gépi tanulás**, **veszteségminimum**

---

## 4. Numerikus integrálás

### 4.1 Alapfogalom
**Rövid definíció:**  
A **[[numerikus integrálás]]** határozott integrál közelítő számítása.

**Működési elv:**  
- Akkor használjuk, ha nincs zárt alakú primitív vagy csak numerikus adat áll rendelkezésre.  
- A területet egyszerű geometriai elemekkel közelítjük.

**Egyszerű példa:**  
Mérési pontokból ismert függvény területét trapézszabállyal becsüljük.

**Vizsgán fontos kulcsszavak:**  
**[[numerikus integrálás]]**, **határozott integrál közelítés**, **kvadratúra**

---

### 4.2 Téglalap módszer
**Rövid definíció:**  
A **[[téglalap módszer]]** a függvény alatti területet téglalapokkal közelíti.

**Működési elv:**  
- Bal- vagy jobb oldali mintavétel használható.  
- Egyszerű, de viszonylag pontatlan.

**Egyszerű példa:**  
Durva kezdeti becsléshez gyorsan alkalmazható.

**Vizsgán fontos kulcsszavak:**  
**[[téglalap módszer]]**, **bal/jobb közelítés**, **egyszerű kvadratúra**

---

### 4.3 Trapéz módszer
**Rövid definíció:**  
A **[[trapéz módszer]]** lineáris interpolációval közelíti a függvényt részintervallumonként.

**Működési elv:**  
- A görbe alatti területet trapézok összegével becsüljük.  
- Általában pontosabb a téglalapmódszernél.

**Egyszerű példa:**  
Sima függvényen kis lépésközzel jó pontosságot ad.

**Vizsgán fontos kulcsszavak:**  
**[[trapéz módszer]]**, **lineáris közelítés**, **jobb pontosság**

---

### 4.4 Simpson módszer
**Rövid definíció:**  
A **[[Simpson-módszer]]** parabolikus közelítést használ.

**Működési elv:**  
- Két részintervallumonként másodfokú közelítés történik.  
- Gyakran lényegesen pontosabb trapézszabálynál.  
- Páros számú részintervallum szükséges.

**Egyszerű példa:**  
Ugyanazzal a lépésközzel Simpson kisebb hibát adhat sima függvényeken.

**Vizsgán fontos kulcsszavak:**  
**[[Simpson-módszer]]**, **parabolikus közelítés**, **nagy pontosság**, **páros intervallum**

---

## 5. Numerikus szempontok
**Rövid definíció:**  
A numerikus módszer minőségét konvergencia, stabilitás és hibabecslés együtt jellemzi.

**Működési elv:**  
- Lépésköz csökkentése általában javít, de nő a számítási költség.  
- Hibabecslés segít a módszer vagy paraméter választásban.  
- Stabil algoritmus kevésbé érzékeny numerikus zajra.

**Egyszerű példa:**  
Integrálásnál túl nagy lépésköz pontatlan, túl kicsi viszont drága lehet.

**Vizsgán fontos kulcsszavak:**  
**konvergencia**, **stabilitás**, **hibabecslés**, **lépésköz**

---

## + Vizsgán érdemes még megemlíteni
- **Jacobi vs Gauss–Seidel**: párhuzamosíthatóság vs gyorsabb konvergencia.  
- Newton gyors, de kezdőértékre érzékeny.  
- Gradiens módszer jellemzően lokális minimumhoz tart.  
- Integrálási pontosság tipikusan: téglalap < trapéz < Simpson.

---

## Rövid szóbeli összefoglaló
Iterációs módszereknél lineáris rendszert közelítő sorozattal oldunk meg, tipikus eljárás a Jacobi és a Gauss–Seidel módszer. Jacobi jobban párhuzamosítható, Gauss–Seidel gyakran gyorsabban konvergál. Nemlineáris gyökkeresésnél Newton-módszer nagyon gyors lehet, de érzékeny kezdőértékre; szelő és regula falsi alternatívák. Gradiens alapú módszerekkel optimumot keresünk a gradiens ellentett irányába lépve, ez gépi tanulásban is alap. Numerikus integrálásnál téglalap, trapéz és Simpson módszerrel közelítjük a határozott integrált, eltérő pontossággal. A gyakorlatban mindig figyelni kell konvergenciára, stabilitásra és lépésközre.

## Kulcsfogalmak
- [[iterációs módszer]]
- [[Jacobi-módszer]]
- [[Gauss–Seidel]]
- [[diagonális dominancia]]
- [[Newton-módszer]]
- [[szelő módszer]]
- [[regula falsi]]
- [[gradiens]]
- [[gradiens módszer]]
- [[lépésköz]]
- [[numerikus integrálás]]
- [[téglalap módszer]]
- [[trapéz módszer]]
- [[Simpson-módszer]]
- [[hibabecslés]]

## Tipikus vizsgakérdések
1. **Mi a Jacobi és Gauss–Seidel fő különbsége?**  
   Jacobi az előző iterációt használja minden komponensre, Gauss–Seidel azonnal felhasználja az új értékeket.

2. **Mikor konvergálnak jól az iterációs módszerek?**  
   Például diagonálisan domináns mátrix esetén gyakran jól konvergálnak.

3. **Mi Newton-módszer előnye és hátránya?**  
   Gyors konvergencia, de derivált kell és érzékeny a kezdőértékre.

4. **Miért hasznos a szelő módszer?**  
   Nem igényel deriváltat, mégis gyakran gyors.

5. **Mi a gradiens módszer alapképlete?**  
   `x_(k+1)=x_k-α∇f(x_k)`.

6. **Mire kell figyelni a lépésköznél gradiens módszernél?**  
   Túl nagy esetén instabil, túl kicsi esetén lassú konvergencia.

7. **Melyik integrálási módszer pontosabb általában?**  
   Sima függvényeken Simpson gyakran pontosabb, mint trapéz, az pedig a téglalapnál jobb.

## Minimum, amit tudni kell
- Iterációs megoldás alapötlete `x^(k+1)=f(x^(k))`.  
- Jacobi és Gauss–Seidel működési különbsége.  
- Konvergencia szerepe és diagonális dominancia említése.  
- Newton-módszer képlete és tulajdonságai.  
- Szelő és regula falsi rövid lényege.  
- Gradiens módszer képlete és lépésköz szerepe.  
- Téglalap, trapéz, Simpson integrálás alapelve.  
- Hibabecslés és stabilitás fontossága numerikus számításban.
