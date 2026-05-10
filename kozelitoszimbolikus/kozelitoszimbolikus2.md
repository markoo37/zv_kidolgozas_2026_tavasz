# Numerikus számítások – 6. tétel

## Sajátértékek, polinomok, interpoláció

---

**Mit jelent ez egyszerűen?**  
Ebben a tételben azt nézzük, hogyan „kibontjuk” egy lineáris transzformáció legfontosabb irányait ([[sajátérték]] / [[sajátvektor]]), hogyan keresünk megoldást egyenletekhez ([[zérushely]]-keresés), és hogyan illesztünk görbét mérési pontokra ([[interpoláció]]) — mindezt úgy, hogy a számítógép csak közelítő számolást tud.

**Mire használjuk a valóságban?**  
Rezgésanalízis, stabilitásvizsgálat, adatelemzés (pl. PCA), hálózati rangok, mérnöki egyenletek megoldása, robotika/pályatervezés, grafika — mindenhol előjönnek ugyanazok az eszközök: spektrum, gyökkeresés, interpoláció.

**Mit jegyezz meg vizsgára?**  
- `Ax = λx` geometriai jelentése + miért kell `x ≠ 0`  
- `det(A - λI) = 0` és a nemtriviális megoldás kapcsolata  
- Hatványmódszer: domináns sajátérték, normalizálás  
- Inverz + shift: kicsi / célzott sajátérték  
- Bisection: biztos, lassú; Newton: gyors, „veszélyes”  
- Lagrange: `l_i` alappolinomok + `L(x)=Σ y_i l_i(x)`  
- Runge: magas fok → szél oszcilláció  
- Numerikus „minőség”: [[kerekítési hiba]], [[stabilitás]], [[konvergencia]], [[hibabecslés]]

---

## 1. [[sajátérték]]ek és [[sajátvektor]]ok

### Mi az `Ax = λx`?

Legyen `A` egy négyzetes mátrix, `x` egy nemnulla vektor, `λ` egy skalár (szám). Ha

$$
A x = \lambda x,
$$

akkor `λ` a mátrix **[[sajátérték]]e**, `x` pedig hozzá tartozó **[[sajátvektor]]a**.

**Intuíció:** Az `A` lineáris leképezés a sajátvektor **irányát** nem forgatja el: csak **nyújtja vagy zsugorítja** (és esetleg megfordítja az irányt, ha `λ < 0`). A `λ` éppen azt mondja meg, **hányszorosára** változik a vektor hossza ebben az irányban (előjellel együtt).

### Miért kell, hogy `x ≠ 0`?

Ha `x = 0`, akkor `Ax = 0` és `λx = 0` **minden** `λ`-ra igaz lenne — tehát a „sajátérték” fogalma értelmetlenné válna. A definíció ezért kifejezetten **nemnulla** `x`-et követel.

### Mi az a [[spektrum]]?

A mátrix **spektruma** a sajátértékek halmaza (ismétlődéssel, ha kell). Jele gyakran: `\sigma(A)`.

---

### TELJES példa (2×2): számolás végig

Legyen

$$
A=\begin{pmatrix}2&1\\1&2\end{pmatrix}.
$$

**1) Karakterisztikus egyenlet**

$$
A-\lambda I=\begin{pmatrix}2-\lambda&1\\1&2-\lambda\end{pmatrix}.
$$

```text
det(A - λI) = (2-λ)(2-λ) - 1·1
            = λ² - 4λ + 4 - 1
            = λ² - 4λ + 3
            = (λ - 1)(λ - 3)
```

Tehát a sajátértékek: **λ₁ = 3**, **λ₂ = 1**.

**2) Sajátvektor `λ = 3`-hoz**

```text
(A - 3I)x = 0  →  (-1)x₁ + 1·x₂ = 0
                 1·x₁ + (-1)x₂ = 0
Mindkettő: x₁ = x₂.
```

Választás: `x = (1, 1)^T` (vagy bármilyen nemnulla skalárszorosa).

Ellenőrzés:

```text
Ax = (2·1+1·1, 1·1+2·1)^T = (3, 3)^T = 3·(1, 1)^T  ✓
```

**3) Sajátvektor `λ = 1`-hez**

```text
(A - I)x = 0  →  x₁ + x₂ = 0  →  x₂ = -x₁.
```

Választás: `x = (1, -1)^T`.

Ellenőrzés:

```text
Ax = (2-1, 1-2)^T = (1, -1)^T = 1·(1, -1)^T  ✓
```

**Mit jegyezz meg vizsgára?**  
2×2-nél a karakterisztikus polinom másodfokú; a gyökök a sajátértékek. A sajátvektorok homogén lineáris rendszer nemtriviális megoldásai — ezért nem egyértelmű a hossz, csak az irány (skalár szorzás erejéig).

**Mire használjuk a valóságban?**  
[[sajátérték]]-számítás kell pl. **rezgés módusaihoz**, **stabilitáshoz**, **főkomponens-elemzéshez (PCA)**, **PageRank-jellegű** lineáris modellekhez.

---

## 2. [[karakterisztikus egyenlet]]

### Miért `det(A - λI) = 0`?

A sajátérték definíciója: létezik `x ≠ 0`, hogy

$$
(A-\lambda I)x = 0.
$$

Ez pontosan azt jelenti, hogy `(A - λI)` **szinguláris** (nem invertálható), különben az egyetlen megoldás a nullvektor lenne. Szingularitás ekvivalens a

$$
\det(A-\lambda I)=0
$$

feltétellel.

### Mit jelent a nemtriviális megoldás?

Az `(A-λI)x=0` rendszernek mindig megvan a **triviális** megoldás `x=0`. A sajátvektor definíciója **nemtriviális** megoldást kér: `x ≠ 0`. Ilyen akkor létezik, ha a mátrix rangja „csökken” — determináns = 0.

### Miért lesz ebből polinom?

`\det(A-\lambda I)` kifejtése `\lambda` hatványainak kombinációja; `n×n` mátrixnál legfeljebb `n`-edfokú polinomot kapsz — ezt hívják **karakterisztikus polinomnak**. A gyökei a sajátértékek (algebrai multiplicitással).

---

### Példa (2×2) — ugyanaz a mátrix, de „QR-feladatos” részletezés

`A` ugyanaz, mint fent. Már láttuk:

```text
det(A - λI) = λ² - 4λ + 3 = 0
Megoldás: λ = (4 ± √(16-12))/2 = (4 ± 2)/2 → λ ∈ {3, 1}
```

**Mit jegyezz meg vizsgára?**  
A „determináns = 0” nem „varázslat”: geometriailag azt mondja, van kitérő irány, amit `(A-λI)` „elnyom”.

---

## 3. Numerikus sajátérték-meghatározás

---

### 3.1 [[hatványmódszer]]

**Mit jelent ez egyszerűen?**  
Veszünk egy kezdővektort, és ismételten ráeresztjük a mátrixot: `x, Ax, A²x, …`. Ha van **erősen domináns** sajátirány, a vektor „beáll” abba az irányba.

**Mire jó?**  
Nagy mátrixnál is olcsón becsüli a **legnagyobb abszolút értékű** sajátértékhez tartozó sajátvektort (domináns módusz).

**Mikor működik jól?**  
Ha a domináns sajátérték **szigorúan nagyobb** abszolút értékben a többinél, és a kezdővektor nem merőleges véletlenül a domináns sajátaltérre.

**Mi a domináns sajátérték?**  
Az a sajátérték, amelyre `|λ|` maximalis a spektrumban (egyszerű esetben egyértelmű).

**Miért kell normalizálni?**  
Mert `A^k x` normája exponenciálisan nő/csökkenhet; a számítógépen túlcsordulás/underflow lenne. Normalizálással csak az **irányt** követjük stabilan.

**Sajátérték-becslés** (ha `q` már közel egységvektor): Rayleigh-hányados

$$
\lambda \approx q^\top A q \quad (\text{valós esetben, ha } \|q\|_2=1).
$$

---

### TELJES számos példa — legalább 4 iteráció

`A` ugyanaz: `\begin{pmatrix}2&1\\1&2\end{pmatrix}`, sajátértékek `3` és `1` — domináns: **3**.  
Kezdő: `x^{(0)} = (1, 0)^T`.  
Lépés: `y = Ax`, majd `x_{\text{új}} = y / \|y\|_2`, és `\lambda \approx x^\top A x` a normalizált `x`-re.

```text
k=0:  x = (1, 000, 0, 000)^T

k=1:  y = Ax = (2, 1)^T
      ||y|| = √5 ≈ 2,23607
      x ≈ (0,89443, 0,44721)^T
      λ ≈ x^T A x = 2,80000

k=2:  y = Ax ≈ (2,23607, 1,78885)^T
      ||y|| ≈ 2,86356
      x ≈ (0,78087, 0,62470)^T
      λ ≈ 2,97561

k=3:  y = Ax ≈ (2,18644, 2,03027)^T
      ||y|| ≈ 2,98375
      x ≈ (0,73294, 0,68043)^T
      λ ≈ x^T A x ≈ 2,9979

k=4:  y = Ax ≈ (2,14632, 2,09380)^T
      ||y|| ≈ 2,99778
      x ≈ (0,71596, 0,69843)^T
      λ ≈ x^T A x ≈ 2,9999
```

Láthatóan `\lambda` **a 3 felé** tart; a vektor iránya közelít a `(1,1)` irányhoz.

**Mit jegyezz meg vizsgára?**  
Hatványmódszer = iterált szorzás + normalizálás; domináns sajátérték/vektor.

**Mire használjuk a valóságban?**  
PageRank-szerű vektorok, domináns rezgésmód, nagy ritka mátrixok „első” sajátiránya.

---

### 3.2 [[inverz hatványmódszer]]

**Mit jelent ez egyszerűen?**  
Nem `A`-t, hanem `A^{-1}`-et (vagy lineáris rendszert megoldva `Ax=b` lépésekben) iterálunk ugyanígy.

**Mire jó?**  
Ha `A` invertálható, `A^{-1}` sajátértékei `1/λ` alakúak (ahol `λ` az `A` sajátértéke). A **legnagyobb** `|1/λ|` általában a **legkisebb** `|λ|`-hoz tartozik — így megkapjuk a **legkisebb** (abszolút értékben tipikusan „legkisebb magnitudójú”) sajátérték irányát.

**Shift (eltolás):**  
`(A - σI)^{-1}` esetén a „domináns” irány a `λ ≈ σ` sajátértékhez szokott közelíteni — ez **célzott** sajátérték-keresés.

---

### Egyszerű példa — 2 iteráció (számszerűen)

`A` ugyanaz. `A^{-1} = \frac{1}{3}\begin{pmatrix}2&-1\\-1&2\end{pmatrix}`.

Kezdő: `x^{(0)}=(1,0)^T`.

```text
k=0:  x = (1, 000, 0, 000)^T

k=1:  y = A^{-1}x = (2/3, -1/3)^T
      ||y|| ≈ 0,74536
      x ≈ (0,89443, -0,44721)^T

k=2:  y = A^{-1}x ≈ (0,74536, -0,59629)^T
      ||y|| ≈ 0,95347
      x ≈ (0,7818, -0,6254)^T
```

Ez az irány a **λ = 1** sajátvektor `(1,-1)` felé tart (az inverz domináns sajátértéke itt `1`, nem `1/3`, mert `|1|>|1/3|`).

**Miért kapcsolódik `A^{-1}` domináns sajátértéke a legkisebb `λ`-hoz?**  
Mert ha `Ax=λx`, akkor `A^{-1}x = (1/λ)x`. A legnagyobb `|1/λ|` a legkisebb `|λ|`-nél van (ha egyértelmű a minimum abszolút értékben).

**Mit jegyezz meg vizsgára?**  
Inverz hatvány + shift = „közelítünk egy adott `\sigma` környékén lévő sajátértékhez”.

---

### 3.3 [[QR-algoritmus]]

**Mit jelent ez egyszerűen?**  
Ismételjük: `A = QR` (ortogonális `Q`, felsőháromszög `R`), majd **fordított sorrendben szorzunk**: `A_1 = RQ`. Ez „hátrább tolja” a mátrixot egy olyan alak felé, ahol a sajátértékek könnyen leolvashatók (pl. kvázi-háromszög alak).

**Miért QR?**  
A `QR` felbontás numerikusan stabil út arra, hogy ortogonális transzformációkkal „tisztítsuk” a mátrixot; az iteráció során a szerkezet fokozatosan diagonalizálódik/kvázi-diagonalizálódik.

**Mire használják?**  
Teljes spektrum (közelítőleg) közepes/nagy sűrű mátrixoknál; gyakorlatban finomításokkal (shift, Hessenberg-preprocessing).

---

### Mini példa — egy QR-lépés elvi menete (2×2)

Legyen `A=\begin{pmatrix}2&1\\1&2\end{pmatrix}`. Egy lehetséges `QR` (Gram–Schmidt jelleggel):

```text
a₁ = (2, 1)^T,  r₁₁ = ||a₁|| = √5
q₁ = a₁/r₁₁ = (2/√5, 1/√5)^T

r₁₂ = q₁ᵀa₂,  a₂ = (1, 2)^T  →  r₁₂ = 4/√5
u₂ = a₂ - r₁₂ q₁ = (-3/5, 6/5)^T
r₂₂ = ||u₂|| = 3√5/5
q₂ = u₂/r₂₂ = (-1/√5, 2/√5)^T

Q = [q₁ | q₂],  R felsőháromszög (r₁₁, r₁₂, 0, r₂₂)
```

Ezután a QR-lépés: **`A_1 = RQ`** (nem `QR`!), és ezt ismételjük. Vizsgán elég annyit mondani: **„QR felbontás, majd fordított szorzás, iterálva a spektrum előjön.”**

**Mit jegyezz meg vizsgára?**  
QR-algoritmus = iteratív ortogonális transzformációs spektrumszámítás; nem kell kézzel 10 lépést számolni, elég az alapötlet.

---

## 4. [[polinom]]ok és [[zérushely]]ek

**Mit jelent ez egyszerűen?**  
A polinom olyan függvény, mint `p(x)=a_n x^n+...+a_0`: véges sok összeadás és hatvány.

**Fokszám:** a legnagyobb olyan `k`, amelyre `a_k ≠ 0` (pl. `3x^2+1` foka 2).

**[[zérushely]] / gyök:** olyan `r`, ahol `p(r)=0`.

**Miért fontos numerikusan?**  
Magas foknál nincs „képlet mindig”; ráadásul a gyökök **érzékenyek** lehetnek az együtthatók kis zavarára — ezért stabil algoritmus kell.

**Példa — pontos gyök:** `p(x)=x^2-5x+6=(x-2)(x-3)` gyökei `2` és `3`.

**Példa — numerikus módszer kell:** `p(x)=x^5-x-1` (általános ötödfokú képlet helyett iteráció).

**Mire használjuk a valóságban?**  
Egyenletek, karakterisztikus polinom gyökei, vezérléselmélet, optimalizálás nulla gradiensnél, fizikai modellek.

---

## 5. Numerikus gyökkeresés

---

### 5.1 [[intervallumfelezés]]

**Mikor használható?**  
`f` folytonos `[a,b]`-n, és `f(a)` és `f(b)` **ellentétes előjelű** ⇒ van gyök (Bolzano-tétel).

**Miért kell előjelváltás?**  
Mert ez garantálja a gyök létezését a zárt intervallumon (legalább egy).

**Miért biztos, de lassú?**  
Mindig felezi a bizonytalanságot, de csak lineárisan jó általában (minden lépés ~1 bitnyi pontosság `log2` skálán).

---

### TELJES példa — `f(x)=x^3-x-2`, `[1,2]`, legalább 5 lépés

```text
f(1) = 1 - 1 - 2 = -2  < 0
f(2) = 8 - 2 - 4 = +4  > 0   →  van gyök [1, 2]-ben

1) [a,b]=[1, 2],   m=1,5,   f(1,5)=3,375-1,5-2=-0,125 < 0  →  új: [1,5, 2]
2) [1,5, 2],       m=1,75,  f(1,75)≈+1,609 > 0            →  új: [1,5, 1,75]
3) [1,5, 1,75],    m=1,625, f(1,625)≈+0,666 > 0           →  új: [1,5, 1,625]
4) [1,5, 1,625],   m=1,5625,f(1,5625)≈+0,252 > 0          →  új: [1,5, 1,5625]
5) [1,5, 1,5625],  m=1,53125,f(1,53125)≈+0,0568 > 0       →  új: [1,5, 1,53125]
```

**Mit jegyezz meg vizsgára?**  
Előjelváltás + folytonosság + felezés = garantált konvergencia.

---

### 5.2 [[Newton-módszer]]

**Alapötlet:** a függvényt lokálisan az érintő egyenessel közelítjük, a gyököt az érintő zérushelyével becsüljük.

**Iteráció:**

$$
x_{n+1}=x_n-\frac{f(x_n)}{f'(x_n)}.
$$

**Miért gyors?**  
Jó kezdés mellett gyakran **kvadratikusan** közelít a gyök felé: a hiba nagysága lépésenként négyzetre csökkenő tendenciát mutat (egyszerű gyöknél, „lágy” feltételek mellett).

**Mikor veszélyes?**  
- `f'(x)≈0` a közelben → osztás katasztrófa  
- rossz kezdőpont → divergencia / másik gyök  
- nem sima függvény / nem megfelelő feltételek

---

### TELJES példa — `f(x)=x^2-2`, `x0=1`, legalább 4 iteráció (`√2` közelítése)

Itt `f'(x)=2x`.

```text
x0 = 1,000000
x1 = 1 - (-1)/2 = 1,500000
x2 = 1,5 - 0,25/3 = 1,4166667
x3 = 1,4166667 - (0,0069444)/(2,8333333) ≈ 1,4142157
x4 = 1,4142157 - (0,0000060)/(2,8284314) ≈ 1,4142136
```

Összehasonlításképp `√2 ≈ 1,414213562…` — 4 lépés után már sok tizedesjegy stimmel.

**Rövid ellenpélda — miért „elromolhat”**

1) **Rossz kezdőpont:** pl. olyan `x0`, ahol az érintő nem visz a gyök felé (pl. ciklikus viselkedés, vagy másik minimum környéke).  
2) **`f'(x0)=0`:** `f(x)=x^2-1`, `x0=0` → `f'(0)=0`, a Newton-lépés **nem értelmezett** (osztás nullával).

---

### 5.3 [[szelő módszer]]

**Miben hasonlít Newtonra?**  
Szintén lineáris közelítést használ, de az érintő helyett **szelő egyenes** megy két ponton át.

**Miért nem kell derivált?**  
Mert a meredekséget közelíti:

$$
f'(x_n)\approx \frac{f(x_n)-f(x_{n-1})}{x_n-x_{n-1}}.
$$

**Miért kevésbé biztos, mint bisection?**  
Nem garantált mindig az előjelváltásos „biztos zárás”; előfordulhat osztás kis nevezővel, rossz ugrások.

**Rövid számos példa — 3 iteráció**  
`f(x)=x^2-2`, kezdőpontok: `x0=1`, `x1=2`.

```text
x2 = x1 - f(x1)·(x1-x0)/(f(x1)-f(x0))
   = 2 - 2·(1)/(2-(-1)) = 2 - 2/3 = 4/3 ≈ 1,333333

x3 = 4/3 - f(4/3)·(4/3 - 2)/(f(4/3) - f(2))
   = 4/3 - (-2/9)·(-2/3)/(-2/9 - 2)
   = 4/3 + 1/15 = 7/5 = 1,400000

x4 = 7/5 - f(7/5)·(7/5 - 4/3)/(f(7/5) - f(4/3))
   = 1,4 - (-0,04)·(1/15)/(-0,04 + 2/9)
   ≈ 1,414634
```

(Ez csak illusztráció: a szelő módszer lépései gyorsak, de a konvergencia feltételei kevésbé „szép” szavakban, mint bisectionnél.)

---

## 6. [[interpoláció]]

**Mit jelent ez egyszerűen?**  
Adott pontokon **pontosan átmenő** függvényt keresünk.

**Interpoláció vs approximáció:**  
- **Interpoláció:** átmegy a pontokon (általában nulla hiba a mintapontokban).  
- **Approximáció / illesztés:** lehet kis hiba mindenhol, cél lehet zajszűrés (pl. legkisebb négyzet).

**Miért `n+1` pontra legfeljebb `n` fok?**  
`n+1` együtthatót akarsz meghatározni egy polinomban (`a_n,...,a_0`), és `n+1` lineáris egyenletet kapsz a pontokra illesztve — tipikusan **egyértelmű** megoldás van, ha az `x_i` különböző, és a fok **legfeljebb** `n`.

**Példa — 2 pontból egyenes:** `(0,0)` és `(1,1)` → `p(x)=x`.  
**Példa — 3 pontból másodfok:** `(0,1),(1,2),(2,5)` → `p(x)=x^2+1` (ellenőrizd: `p(0)=1`, `p(1)=2`, `p(2)=5`).

**Mire használjuk a valóságban?**  
Mérések köztes értéke, grafika, pálya simítás, integrálás előkészítése.

---

## 7. [[Lagrange-interpoláció]]

**Alappolinomok:** minden `i`-re `l_i(x_j)=1`, ha `j=i`, különben `0`.

**Polinom:**

$$
L(x)=\sum_{i=0}^{n} y_i\, \ell_i(x).
$$

---

### TELJES példa — pontok: `(0,1)`, `(1,3)`, `(2,2)`

```text
ℓ0(x) = (x-1)(x-2) / ((0-1)(0-2)) = (x-1)(x-2)/2
ℓ1(x) = (x-0)(x-2) / ((1-0)(1-2)) = x(x-2)/(-1) = x(2-x)
ℓ2(x) = (x-0)(x-1) / ((2-0)(2-1)) = x(x-1)/2
```

Összeállítás:

```text
L(x) = 1·ℓ0 + 3·ℓ1 + 2·ℓ2
     = (x²-3x+2)/2 + 3(2x-x²) + x(x-1)
     = -1,5x² + 3,5x + 1
```

Ellenőrzés:

```text
L(0)=1,  L(1)=3,  L(2)=2  ✓
```

`x=1,5`:

```text
L(1,5) = -1,5·(2,25) + 3,5·(1,5) + 1
       = -3,375 + 5,25 + 1
       = 2,875
```

**Mit jegyezz meg vizsgára?**  
Lagrange szépen tanítja a „bázisfüggvények” gondolatát; nagy `n`-nél numerikusan drága/instabil lehet — ezért gyakorlatban más alak (pl. Newton-forma, spline).

---

## 8. [[Runge-jelenség]]

**Miért gond a magas fok?**  
Sok, egyenletesen felvett ponton a **egyetlen** magas fokú interpolációs polinom a **széleken** extrém oszcillációt mutathat — jól illeszkedik ugyan a pontokra, de közben „vad” lehet közöttük.

**Miért oszcillál?**  
A polinom „túl sok rugalmasságot” kap: a pontonkénti kényszereket úgy elégíti ki, hogy nagy meredekségek keletkezhetnek a peremek közelében.

**Miért jobb sokszor spline / darabos?**  
Mert alacsony fokú darabokkal lokálisan simítunk: kevesebb globális „berúgás”.

**Szemléletesen sok egyenletes pontnál:**  
Mintha egy gumiszálat kényszerítenél sok szögre: a széleken „rángatózni” fog, még ha minden szögön át is megy.

### „Vizsgán így mondanám”

> Ha sok pontot egyetlen magas fokú polinommal interpolálunk egyenletes rácsban, a peremen nagy kilengések jelentkezhetnek — ez a Runge-jelenség. Emiatt gyakran spline-ot vagy alacsony fokú szakaszokat használunk.

**Mire használjuk / mit tanít?**  
„Pontos illeszkedés” nem egyenlő „jó közelítés a pontok között”.

---

## 9. Numerikus szempontok

### [[kerekítési hiba]]

A valós számok véges ábrázolása miatt minden lépés „kicsit elcsúszik”; a hiba **halmozódhat**.

### [[stabilitás]]

Egy módszer stabil, ha a kis bemeneti/zaj hiba **nem növekszik végzetesen** az algoritmus során.

### [[konvergencia]]

Az iteráció „jó irányba megy-e”: pl. `\|x_{k}-x^*\| \to 0` (lokálisan vagy globálisan, feltételek mellett).

### [[hibabecslés]]

Becsüljük, mennyi a maradék hiba (intervallum hossza bisectionnél, derivált alapú becslés Newtonnál, stb.).

### Miért nem elég a képlet?

Mert a képlet **feltételeket** feltételez (simaság, jó kezdőpont, nemnulla derivált, jól kondicionált feladat). Gyakorlatban a **feladat kondicionáltsága** + **algoritmus stabilitása** dönti el, hogy az eredmény hihető-e.

**Példák a szöveges összehasonlításokhoz:**

- **Gyors, de instabil:** bizonyos naiv eliminációk / rosszul skálázott problémák; kis perturbáció → nagy változás.  
- **Lassabb, de megbízhatóbb:** bisection jó előjelváltással; stabil QR a sajátértékekhez (finomításokkal).  
- **Newton vs bisection:** Newton gyors lehet, de kevésbé „garanciás”; bisection lassabb, de robosztus előjelváltás mellett.

---

## 10. Valós alkalmazások (témakörönként)

### Sajátértékek — **Mire használjuk a valóságban?**

- **PCA / adatelemzés:** kovarianciamátrix [[sajátérték]]ei = fő irányok „fontossága”  
- **Rezgésanalízis:** sajátfrekvenciák és módusok  
- **Rendszerstabilitás:** dinamika mátrixának spektruma  
- **PageRank-jelleg:** nagy lineáris rendszerek domináns invariáns iránya

### Gyökkeresés — **Mire használjuk a valóságban?**

- Mérnöki egyenletek (hő, áramlás, szerkezet)  
- **Optimalizálás:** stacionárius pontok (`f'=0`)  
- Fizikai modellek egyensúlyi állapotai

### Interpoláció — **Mire használjuk a valóságban?**

- Mérési adatok köztes értéke  
- Grafika (görbék, animációk)  
- Pályatervezés  
- Numerikus integrálás előkészítése (függvény-diszkretizálás)

---

## Rövid szóbeli összefoglaló

A sajátérték-probléma lényege, hogy az `A` mátrix bizonyos irányokban csak skáláz: `Ax=λx`, ahol a nemnulla `x` a [[sajátvektor]], `λ` a [[sajátérték]]. Elméletben a `\det(A-λI)=0` karakterisztikus egyenlet gyökei adják a spektrumot; nagy mátrixnál numerikus módszerek kellenek. A [[hatványmódszer]] a domináns sajátirányt keresi iterált szorzással és normalizálással, az [[inverz hatványmódszer]] pedig a kisebb sajátértékek irányához közelít, shifttel célozható. A [[QR-algoritmus]] ortogonális QR-lépésekkel finomítja a mátrixot, hogy a teljes spektrum kiolvasható legyen. Polinomoknál a [[zérushely]] gyakran csak közelítőleg számolható: a [[intervallumfelezés]] biztos, de lassú, a [[Newton-módszer]] gyors lehet jó feltételek mellett, a [[szelő módszer]] derivált nélkül közelít, de kevésbé garanciális. Az [[interpoláció]] pontokra illeszkedő függvényt ad; a [[Lagrange-interpoláció]] alappolinomok összegével épít polinomot. Magas foknál figyelni kell a [[Runge-jelenség]]re. Végül numerikusan mindig számít a [[kerekítési hiba]], a [[stabilitás]], a [[konvergencia]] és a [[hibabecslés]]: a jó eredményhez nem elég a képlet, kell a módszer választása és a feltételek ismerete is.

---

## Kulcsfogalmak

- [[sajátérték]]
- [[sajátvektor]]
- [[spektrum]]
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
- [[stabilitás]]
- [[kerekítési hiba]]
- [[hibabecslés]]

---

## Tipikus vizsgakérdések

1. **Mit jelent geometriailag az `Ax=λx`?**  
   Az `A` a sajátvektor irányát megtartja, csak `λ`-szorosára változtatja (előjellel együtt).

2. **Miért követeljük, hogy `x≠0`?**  
   Mert `x=0` minden `λ`-ra „megoldás” lenne, a fogalom értelmetlenné válna.

3. **Honnan jön a `det(A-λI)=0`?**  
   Mert nemtriviális megoldás csak szinguláris `(A-λI)` esetén létezik, ami ekvivalens a determináns nullával.

4. **Mi a spektrum?**  
   A sajátértékek halmaza (ismétlődéssel számolva, ha kell).

5. **Mit becsül a hatványmódszer, és miért normalizálunk?**  
   A domináns sajátérték/vektor irányát; a normalizálás numerikus stabilitás és túlcsordulás elkerülése miatt kell.

6. **Miért segít az inverz hatványmódszer kisebb sajátértékhez?**  
   Mert `A^{-1}` sajátértékei `1/λ` alakúak; a legnagyobb `|1/λ|` tipikusan a legkisebb `|λ|`-hez tartozik.

7. **Mi a shift szerepe?**  
   `(A-σI)^{-1}` domináns iránya közelíthet a `λ≈σ` sajátértékhez.

8. **QR-algoritmus lényege egy mondatban?**  
   `A=QR`, majd `RQ` új iteráció — ortogonális transzformációkkal közelítjük a spektrum kiolvasható alakját.

9. **Bisection mikor garantált?**  
   Folytonos `f`-re és `f(a)f(b)<0`-ra zárt intervallumban.

10. **Newton előnye és fő veszélye?**  
    Gyakran nagyon gyors lokálisan; veszélyes lehet kis derivált vagy rossz kezdőpont.

11. **Interpoláció vs approximáció?**  
    Interpoláció: pontokon pontos; approximáció: lehet zajcsökkentés kis hibával mindenhol.

12. **Mi a Runge-jelenség?**  
    Magas fokú egyenletes interpolációnál perem oszcilláció, rossz közelítés a pontok között.

13. **Mit jelent az, hogy egy módszer stabil?**  
    Kis perturbáció nem növekszik végzetesen az algoritmus lépéseiben.

---

## Minimum, amit tudni kell (túlélőlista)

- `Ax=λx` + `x≠0` + geometriai skálázás  
- `\det(A-λI)=0` és a nemtriviális megoldás kapcsolata  
- Spektrum fogalma  
- Hatványmódszer: domináns sajátérték, normalizálás, Rayleigh-becslés ötlete  
- Inverz hatványmódszer + shift rövid értelmezése  
- QR-algoritmus: `QR` majd `RQ`, iteráció, spektrum  
- Polinom, fok, gyök; mikor kell numerikus módszer  
- Bisection feltétele és lépése  
- Newton képlete + mikor romlik el  
- Szelő: derivált nélkül, kevésbé garanciális  
- Interpoláció alap + `n+1` pont → legfeljebb `n` fok  
- Lagrange alappolinomok + `L(x)=Σ y_i l_i(x)`  
- Runge: magas fok egyenletes rács → perem oszcilláció  
- Kerekítés, stabilitás, konvergencia, hibabecslés: miért számít

---

## Tételvázlat (bemásolandó váz)

```text
# Numerikus számítások – 6. tétel
## Sajátértékek, polinomok, interpoláció

1) Sajátérték/sajátvektor: Ax=λx, geometria, spektrum, 2×2 teljes példa + ellenőrzés
2) Karakterisztikus egyenlet: det(A-λI)=0, nemtriviális megoldás, polinom
3) Numerikus spektrum:
   - hatványmódszer (domináns, normalizálás, iteráció)
   - inverz hatványmódszer (1/λ, shift)
   - QR-algoritmus (QR majd RQ, miért stabil/általános)
4) Polinom, fok, zérushely; mikor numerikus
5) Gyökkeresés: bisection (előjelváltás), Newton (érintő), szelő (derivált nélkül)
6) Interpoláció vs approximáció; n+1 pont → legfeljebb n fok
7) Lagrange: l_i alappolinomok, L(x)=Σ y_i l_i(x), számos példa
8) Runge-jelenség: magas fok, perem oszcilláció, spline/darabos
9) Numerikus minőség: kerekítés, stabilitás, konvergencia, hibabecslés
10) Alkalmazások: PCA/rezgés/stabilitás/PageRank; gyökök mérnökien; interpoláció mérés/grafika/pálya

Záró: szóbeli összefoglaló + kulcsfogalmak + kérdések + minimumlista
```
