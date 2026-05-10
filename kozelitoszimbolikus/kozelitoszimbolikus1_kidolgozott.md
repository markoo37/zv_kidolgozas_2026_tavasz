# Numerikus számítások – Lineáris egyenletrendszerek és mátrixfelbontások
### Kidolgozott vizsgaanyag számos példákkal

---

## Tartalom
- [[#1. Az Ax = b feladat – mire megyünk ki?]]
- [[#2. Gauss-elimináció – a klasszikus alap]]
- [[#3. Gauss–Jordan – ha egylépéses megoldás kell]]
- [[#4. Pivotálás – miért baj a kis pivot?]]
- [[#5. LU-felbontás – ha ugyanazt a mátrixot sokszor használjuk]]
- [[#6. Cholesky-felbontás – az SPD mátrix gyorssávja]]
- [[#7. QR-felbontás – Gram–Schmidt és legkisebb négyzetek]]
- [[#8. Numerikus szempontok – kerekítési hiba és kondíciószám]]
- [[#Kulcsfogalmak]]
- [[#Tipikus vizsgakérdések]]
- [[#Rövid összefoglaló]]

---

## 1. Az Ax = b feladat – mire megyünk ki?

**Mi ez?**
Majdnem minden mérnöki/tudományos feladat visszavezethető arra: adott egy $A$ mátrix és egy $b$ vektor, keressük az $x$ vektort, amelyre $Ax = b$.

**Érzésre:**
Képzeld el, hogy van 3 ismeretlened és 3 egyenleted. Ezeket felírhatjuk egy "dobozba" (mátrix), és a feladat: mekkora az $x$?

**Konkrét felírás:**
```
2x + y - z  =  8       [2   1  -1] [x]   [8 ]
-3x - y + 2z = -11  →  [-3 -1   2] [y] = [-11]
-2x + y + 2z = -3       [-2  1   2] [z]   [-3 ]

          A                  x        b
```

Ez a rendszer lesz a **vörös fonalunk** az egész fejezeten át – minden módszerrel megoldjuk ugyanezt!

> **Az exact megoldás:** x = 2, y = 3, z = −1 — ezt kell minden módszernek visszaadnia.

---

## 2. Gauss-elimináció – a klasszikus alap

### Mi a lényege?
**Érzésre:** Olyan, mint amikor lépésről lépésre kiküszöbölöd az ismeretleneket. Előbb megismered $z$-t, abból $y$-t, abból $x$-et.

**Technikai lényeg:** Elemi sorátalakításokkal felső háromszög alakra hozjuk a kiterjesztett mátrixot $[A|b]$, majd **visszahelyettesítéssel** kapjuk a megoldást.

**Mire használjuk a valóságban?**
```
Mérnöki egyenletrendszerek, végeselem-módszer, hálózatelemzés.
Ez a legelterjedtebb direkt megoldó. Kis-közepes méretű (pár száz egyenlet) rendszereknél alapmódszer.
```

---

### Teljes lépésenként kidolgozott példa

**Kiindulás – kiterjesztett mátrix:**
```
[A|b] =  [ 2   1  -1 |  8 ]
         [-3  -1   2 | -11]
         [-2   1   2 |  -3]
```

---

#### 1. lépés: Az 1. oszlop nullázása (pivot = a₁₁ = 2)

**R2 ← R2 − (−3/2)·R1**, azaz R2 ← R2 + (3/2)·R1:
```
m₂₁ = (-3)/2 = -3/2

R2 új:
  x: -3 + (3/2)·2 = -3 + 3 = 0       ✓
  y: -1 + (3/2)·1 = -1 + 3/2 = 1/2
  z:  2 + (3/2)·(-1) = 2 - 3/2 = 1/2
  b: -11 + (3/2)·8 = -11 + 12 = 1
```

**R3 ← R3 − (−1)·R1**, azaz R3 ← R3 + R1:
```
m₃₁ = (-2)/2 = -1

R3 új:
  x: -2 + 1·2  = 0        ✓
  y:  1 + 1·1  = 2
  z:  2 + 1·(-1) = 1
  b: -3 + 1·8  = 5
```

**Mátrix az 1. lépés után:**
```
[ 2    1    -1  |  8 ]
[ 0   1/2  1/2  |  1 ]
[ 0    2    1   |  5 ]
```

---

#### 2. lépés: A 2. oszlop nullázása (pivot = a₂₂ = 1/2)

**R3 ← R3 − 4·R2** (mert m₃₂ = 2/(1/2) = 4):
```
m₃₂ = 2 / (1/2) = 4

R3 új:
  y: 2 - 4·(1/2) = 2 - 2 = 0       ✓
  z: 1 - 4·(1/2) = 1 - 2 = -1
  b: 5 - 4·1     = 5 - 4 = 1
```

**Felső háromszög alak (kész!):**
```
[ 2    1    -1  |  8 ]
[ 0   1/2  1/2  |  1 ]
[ 0    0   -1   |  1 ]
```

---

#### 3. lépés: Visszahelyettesítés

```
3. sorból:  -z = 1             →  z = -1

2. sorból:  (1/2)y + (1/2)·(-1) = 1
            (1/2)y - 1/2 = 1
            (1/2)y = 3/2       →  y = 3

1. sorból:  2x + 1·3 + (-1)·(-1) = 8
            2x + 3 + 1 = 8
            2x = 4             →  x = 2
```

**Megoldás: x = 2, y = 3, z = −1** ✓

**Ellenőrzés:**
```
2·2 + 3 - (-1)   = 4 + 3 + 1  = 8   ✓
-3·2 - 3 + 2·(-1) = -6 - 3 - 2 = -11  ✓
-2·2 + 3 + 2·(-1) = -4 + 3 - 2 = -3   ✓
```

---

## 3. Gauss–Jordan – ha egylépéses megoldás kell

### Mi a lényege?
**Érzésre:** A Gauss továbblép – nemcsak lefelé nulláz, hanem **felfelé is**. A végén az $A$ helyén az egységmátrix áll, a $b$ helyén meg közvetlenül az $x$.

**Technikai lényeg:** $[A|b] \;\longrightarrow\; [I|x]$

**Mire használjuk a valóságban?**
```
Mátrix inverzének kiszámítása ([A|I] → [I|A⁻¹]).
Kisebb rendszereknél, ahol explicit megoldás kell.
Numerikusan kicsit drágább, mint sima Gauss + visszahelyettesítés.
```

---

### Teljes lépésenként kidolgozott példa

**Kiindulás:** Folytatjuk a Gauss után kapott felső háromszög alakból:
```
[ 2    1    -1  |  8 ]
[ 0   1/2  1/2  |  1 ]
[ 0    0   -1   |  1 ]
```

---

#### 1. lépés: Főátlói elemeket 1-esekre hozzuk

```
R1 ← R1 / 2 :   [ 1   1/2  -1/2 |  4 ]
R2 ← R2 · 2 :   [ 0    1    1   |  2 ]
R3 ← R3 ·(-1):   [ 0    0    1   | -1 ]
```

**Mátrix:**
```
[ 1   1/2  -1/2 |  4 ]
[ 0    1    1   |  2 ]
[ 0    0    1   | -1 ]
```

---

#### 2. lépés: A 3. oszlop nullázása felfelé (pivot = R3)

**R2 ← R2 − 1·R3:**
```
R2 új: [ 0, 1, 1-1, 2-(-1) ] = [ 0, 1, 0, 3 ]
```

**R1 ← R1 − (−1/2)·R3**, azaz R1 ← R1 + (1/2)·R3:
```
R1 új: [ 1, 1/2, -1/2 + 1/2, 4 + (-1/2) ] = [ 1, 1/2, 0, 7/2 ]
```

**Mátrix:**
```
[ 1   1/2   0  |  7/2 ]
[ 0    1    0  |   3  ]
[ 0    0    1  |  -1  ]
```

---

#### 3. lépés: A 2. oszlop nullázása felfelé (pivot = R2)

**R1 ← R1 − (1/2)·R2:**
```
R1 új: [ 1, 1/2 - 1/2, 0, 7/2 - 3/2 ] = [ 1, 0, 0, 2 ]
```

**Végeredmény:**
```
[ 1   0   0  |  2 ]    →   x = 2
[ 0   1   0  |  3 ]    →   y = 3
[ 0   0   1  | -1 ]    →   z = -1
```

**Megoldás közvetlenül olvasható: x = 2, y = 3, z = −1** ✓

---

## 4. Pivotálás – miért baj a kis pivot?

### Mi a lényege?
**Érzésre:** Ha egy pivot (a szorzó "alapja") nagyon kicsi, akkor a szorzó nagyon nagy lesz, és a kerekítési hiba felerősödik. A pivotálás = megkeresi a **legnagyobb abszolút értékű** elemet az adott oszlopban, és **sorokat cserél**, hogy az kerüljön pivotnak.

**Részleges pivotálás:** csak az aktuális oszlopon belül keres (ez a gyakorlati standard).
**Teljes pivotálás:** sor- és oszlopcserét is megenged (ritkábban használt).

**Mire használjuk a valóságban?**
```
Minden komoly numerikus könyvtár (LAPACK, NumPy stb.) automatikusan pivot-ál.
Nélküle a Gauss-elimináció katasztrofálisan pontatlan lehet rosszul kondícionált rendszereknél.
```

---

### Példa: instabilitás pivotálás nélkül vs. pivotálással

**Rendszer** (ε = 0.0001, gépi pontosság: 4 tizedesjegy):
```
0.0001·x + y = 1      →  [0.0001   1  | 1]
    x + y = 2          →  [  1      1  | 2]
```

**Pontos megoldás:**
```
(2. sor) − (1. sor): (1 − 0.0001)x = 1  →  x = 1/0.9999 ≈ 1.0001
y = 1 − 0.0001·x ≈ 0.9999
```

---

#### Pivotálás NÉLKÜL (4 tizedesjegy):

```
Szorzó: m = 1 / 0.0001 = 10 000

R2 ← R2 − 10000·R1:
  y: 1 − 10000·1     = −9999
  b: 2 − 10000·1     = −9998

→  −9999·y = −9998
→  y = 9998/9999 = 0.99990...

4 tizedesjeggyel kerekítve: y ≈ 1.000   ← KEREKÍTÉSI HIBA!

Visszahelyettesítve:
0.0001·x = 1 − y = 1 − 1.000 = 0.000
x = 0                          ← TELJESEN HIBÁS EREDMÉNY!
```

> **A hiba oka:** A szorzó (10000) annyira felerősítette a kerekítési hibát, hogy az tönkretette a megoldást.

---

#### Pivotálással (sorcsere, majd ugyanaz a 4 tizedesjegy):

```
Sorcsere: R1 ↔ R2
  [  1      1  | 2]
  [0.0001   1  | 1]

Szorzó: m = 0.0001 / 1 = 0.0001    ← ez már kicsi, rendben!

R2 ← R2 − 0.0001·R1:
  y: 1 − 0.0001·1 = 0.9999
  b: 1 − 0.0001·2 = 0.9998

→  0.9999·y = 0.9998
→  y = 0.9999...  ≈ 0.9999   ✓ (kis hiba)

x = 2 − y = 2 − 0.9999 = 1.0001   ✓ (helyes!)
```

> **Tanulság:** A pivot mindig a lehető legnagyobb abszolút értékű elem legyen az oszlopban. Ez minimalizálja a szorzókat, és így a kerekítési hiba nem erősödik fel.

---

## 5. LU-felbontás – ha ugyanazt a mátrixot sokszor használjuk

### Mi a lényege?
**Érzésre:** A Gauss-elimináció végzi a kemény munkát ($A$-t feldolgozza), és ezt az elvégzett munkát eltároljuk egy $L$ és $U$ mátrixban. Ha más $b$-re is meg kell oldani $Ax = b$-t, **nem kell mindent újra csinálni** — csak az olcsó előre- és visszahelyettesítést.

**Technikai lényeg:**
$$A = L \cdot U$$
- $L$ (lower triangular): alsó háromszögmátrix, főátlójában 1-esekkel
- $U$ (upper triangular): felső háromszögmátrix (= Gauss vége)

**Megoldás két lépésben:**
1. $Ly = b$ → előrehelyettesítés (felülről lefelé)
2. $Ux = y$ → visszahelyettesítés (alulról felfelé)

**Mire használjuk a valóságban?**
```
Paraméterszenzitivitás-vizsgálatnál (sok különböző b, ugyanaz az A).
Mátrix inverzének kiszámítása (megoldjuk Ax_i = e_i-t minden egységvektorra).
Mérnöki szimulációkban, ahol az együtthatómátrix nem változik, de a jobb oldal igen.
```

---

### Teljes lépésenként kidolgozott példa

**Ugyanaz az A mátrix:**
```
A = [ 2   1  -1]
    [-3  -1   2]
    [-2   1   2]
```

#### Az L és U leolvasása a Gauss-eliminációból

A Gauss-elimináció szorzói **pontosan az L alsó háromszög elemei** lesznek (előjellel együtt):

```
m₂₁ = (-3)/2 = -3/2    →  L[2,1] = -3/2
m₃₁ = (-2)/2 = -1      →  L[3,1] = -1
m₃₂ = 2/(1/2) = 4      →  L[3,2] = 4
```

A felső háromszög alak = U:
```
U = [ 2    1    -1  ]
    [ 0   1/2  1/2  ]
    [ 0    0   -1   ]
```

Az L mátrix (főátlón 1-esek, alatta a szorzók):
```
L = [ 1      0    0 ]
    [-3/2    1    0 ]
    [ -1     4    1 ]
```

#### Ellenőrzés: L·U = A?
```
L·U sor 1: [1·2 + 0 + 0,  1·1 + 0 + 0,  1·(-1) + 0 + 0]  =  [2, 1, -1]  ✓
L·U sor 2: [-3/2·2 + 1·0,  -3/2·1 + 1·(1/2),  -3/2·(-1) + 1·(1/2)]
          = [-3,  -3/2+1/2,  3/2+1/2]  =  [-3, -1, 2]  ✓
L·U sor 3: [-1·2 + 4·0 + 0,  -1·1 + 4·(1/2) + 0,  -1·(-1) + 4·(1/2) + (-1)]
          = [-2,  -1+2,  1+2-1]  =  [-2, 1, 2]  ✓
```

---

#### Megoldás b = [8, −11, −3]ᵀ esetén

**1. lépés: Ly = b (előrehelyettesítés)**
```
[ 1      0    0 ] [y₁]   [ 8 ]
[-3/2    1    0 ] [y₂] = [-11]
[ -1     4    1 ] [y₃]   [-3 ]

Sor 1: y₁ = 8
Sor 2: -3/2 · 8 + y₂ = -11  →  -12 + y₂ = -11  →  y₂ = 1
Sor 3: -1·8 + 4·1 + y₃ = -3  →  -8 + 4 + y₃ = -3  →  y₃ = 1

y = [8, 1, 1]ᵀ
```

**2. lépés: Ux = y (visszahelyettesítés)**
```
[ 2    1    -1  ] [x]   [8]
[ 0   1/2  1/2  ] [y] = [1]
[ 0    0   -1   ] [z]   [1]

Sor 3: -z = 1               →  z = -1
Sor 2: (1/2)y + (1/2)·(-1) = 1  →  (1/2)y = 3/2  →  y = 3
Sor 1: 2x + 3 - (-1) = 8   →  2x = 4  →  x = 2
```

**Megoldás: x = 2, y = 3, z = −1** ✓

> **Ha most egy másik b', pl. [1, 0, 2]ᵀ kellene:** az L és U mátrixokat nem kell újraépíteni, csak az előre- és visszahelyettesítést futtatjuk le újra — ez sokkal gyorsabb!

---

## 6. Cholesky-felbontás – az SPD mátrix gyorssávja

### Mi a lényege?
**Érzésre:** Ha a mátrix szimmetrikus és pozitív definit (SPD), akkor egy speciális, négyzetes LU-felbontás jön ki: $A = L \cdot L^T$. Ez körülbelül feleannyi művelet, mint az általános LU.

**Feltételek:**
- $A = A^T$ (szimmetria)
- $x^T A x > 0$ minden $x \neq 0$-ra (pozitív definitság)
- Ellenőrzés: minden vezető aldetermináns (főminor) pozitív

**Mire használjuk a valóságban?**
```
Legkisebb négyzetek normálegyenletei: Aᵀ·A szimmetrikus, pozitív definit.
Finiteelem-módszer merevségi mátrixa.
Statisztika, kovariancia-mátrix inverze.
```

---

### Teljes lépésenként kidolgozott példa

**SPD mátrix:**
```
A = [4  2  2]
    [2  3  2]
    [2  2  3]
```

**Ellenőrzés (vezető aldeterminánsok):**
```
det([4]) = 4 > 0  ✓
det([[4,2],[2,3]]) = 12 - 4 = 8 > 0  ✓
det(A) = 4·(9-4) - 2·(6-4) + 2·(4-6) = 20 - 4 - 4 = 12 > 0  ✓
```
→ Az A valóban SPD.

---

#### L kiszámítása – a Cholesky-algoritmus

$$A = L \cdot L^T, \quad L = \begin{bmatrix} l_{11} & 0 & 0 \\ l_{21} & l_{22} & 0 \\ l_{31} & l_{32} & l_{33} \end{bmatrix}$$

**Képletek:**
```
l₁₁ = √(a₁₁)
lᵢ₁ = aᵢ₁ / l₁₁          (i > 1, 1. oszlop)
lⱼⱼ = √(aⱼⱼ - Σₖ<ⱼ lⱼₖ²)  (főátló)
lᵢⱼ = (aᵢⱼ - Σₖ<ⱼ lᵢₖ·lⱼₖ) / lⱼⱼ  (i > j)
```

**Lépésről lépésre:**
```
l₁₁ = √a₁₁ = √4 = 2

l₂₁ = a₂₁ / l₁₁ = 2/2 = 1
l₃₁ = a₃₁ / l₁₁ = 2/2 = 1

l₂₂ = √(a₂₂ - l₂₁²) = √(3 - 1²) = √2 ≈ 1.4142

l₃₂ = (a₃₂ - l₃₁·l₂₁) / l₂₂ = (2 - 1·1) / √2 = 1/√2 ≈ 0.7071

l₃₃ = √(a₃₃ - l₃₁² - l₃₂²) = √(3 - 1 - 1/2) = √(3/2) ≈ 1.2247
```

**Eredmény:**
```
L = [ 2       0        0     ]
    [ 1      √2        0     ]
    [ 1      1/√2    √(3/2)  ]

  = [ 2.0000   0.0000   0.0000 ]
    [ 1.0000   1.4142   0.0000 ]
    [ 1.0000   0.7071   1.2247 ]
```

**Ellenőrzés: L·Lᵀ = A?**
```
(1,1): 2² + 0 + 0 = 4              ✓
(2,1): 1·2 + 0 + 0 = 2             ✓
(2,2): 1² + (√2)² + 0 = 1+2 = 3   ✓
(3,1): 1·2 = 2                     ✓
(3,2): 1·1 + (1/√2)·√2 = 1+1 = 2  ✓
(3,3): 1 + 1/2 + 3/2 = 3           ✓
```

---

## 7. QR-felbontás – Gram–Schmidt és legkisebb négyzetek

### Mi a lényege?
**Érzésre:** Az $A$ mátrix oszlopait ortogonalizáljuk (derékszögűvé tesszük, majd normáljuk). Így kaptunk egy $Q$ (ortogonális) és egy $R$ (felső háromszög) mátrixot. A QR módszer numerikusan stabil, mert $Q$ nem "növeli meg" a hibákat.

**Technikai lényeg:**
$$A = Q \cdot R, \quad Q^T Q = I, \quad R \text{ felső háromszög}$$

**Mire használjuk a valóságban?**
```
Túlhatározott rendszerek: több egyenlet, mint ismeretlen (mérési adatillesztés).
Legkisebb négyzetek módszere: min ||Ax - b||² megoldása.
Numerikusan stabilabb, mint a normálegyenletek (AᵀAx = Aᵀb).
```

---

### Teljes lépésenként kidolgozott példa – egyenes illesztése

**Feladat:** Illesszünk $y = a + bx$ egyenest a következő pontokra:
```
(x₁, y₁) = (1, 1)
(x₂, y₂) = (2, 3)
(x₃, y₃) = (3, 2)
```

**Felírjuk az Ax = b rendszert** (túlhatározott: 3 egyenlet, 2 ismeretlen):
```
[1  1] [a]   [1]
[1  2] [b] = [3]
[1  3]        [2]

A (3×2),  b = [1, 3, 2]ᵀ
```

---

#### Gram–Schmidt ortogonalizáció

**A oszlopvektorai:**
```
a₁ = [1, 1, 1]ᵀ     (konstans tag)
a₂ = [1, 2, 3]ᵀ     (lineáris tag)
```

**1. bázisvektor:**
```
u₁ = a₁ = [1, 1, 1]ᵀ
||u₁|| = √(1+1+1) = √3

q₁ = u₁/||u₁|| = [1/√3, 1/√3, 1/√3]ᵀ
```

**2. bázisvektor (vetítés és merőlegesítés):**
```
Vetítés: a₂ · q₁ = (1·1 + 2·1 + 3·1)/√3 = 6/√3 = 2√3

u₂ = a₂ - (a₂·q₁)·q₁ = [1,2,3] - 2√3 · [1/√3, 1/√3, 1/√3]
   = [1,2,3] - 2·[1,1,1]
   = [-1, 0, 1]ᵀ

||u₂|| = √(1+0+1) = √2

q₂ = u₂/||u₂|| = [-1/√2, 0, 1/√2]ᵀ
```

---

#### Q és R mátrix felírása

```
Q = [q₁ | q₂] = [ 1/√3   -1/√2 ]
                 [ 1/√3    0    ]
                 [ 1/√3    1/√2 ]

R = [r₁₁  r₁₂] = [||u₁||    a₂·q₁ ] = [√3    2√3]
    [ 0   r₂₂]   [  0      ||u₂||  ]   [ 0     √2]
```

---

#### Megoldás: Rx = Qᵀb

**Számítsuk ki Qᵀb:**
```
Qᵀb sor 1: (1/√3)·1 + (1/√3)·3 + (1/√3)·2 = 6/√3 = 2√3  ≈ 3.464
Qᵀb sor 2: (-1/√2)·1 + 0·3 + (1/√2)·2    = 1/√2          ≈ 0.707
```

**Rendszer: Rx = Qᵀb**
```
[√3    2√3] [a]   [2√3   ]
[ 0     √2] [b] = [1/√2  ]
```

**Visszahelyettesítés:**
```
Sor 2: √2 · b = 1/√2   →   b = 1/(√2·√2) = 1/2

Sor 1: √3 · a + 2√3 · (1/2) = 2√3
       √3 · a + √3 = 2√3
       √3 · a = √3       →   a = 1
```

**Illesztett egyenes: y = 1 + 0.5x** ✓

**Ellenőrzés:**
```
x=1: ŷ = 1.5,  hiba = 1 - 1.5 = -0.5
x=2: ŷ = 2.0,  hiba = 3 - 2.0 =  1.0
x=3: ŷ = 2.5,  hiba = 2 - 2.5 = -0.5

Négyzetösszeg = 0.25 + 1.00 + 0.25 = 1.50  (ez a lehető legkisebb!)
```

---

## 8. Numerikus szempontok – kerekítési hiba és kondíciószám

### 8.1 Kerekítési hiba

**Érzésre:** A számítógép véges sok biten tárolja a számokat. Minden lebegőpontos műveletnél keletkezik egy kis hiba. Ha sok ilyen műveletet hajtunk végre, a hibák összeadódhatnak — vagy felerősödhetnek.

**Konkrét példa:**
```
Pontos szám:      1/3 = 0.333333333...
4 tizedesjegyen:  0.3333

Ha 10 000-szer hozzáadjuk:
  Pontos:  10000/3 = 3333.333...
  Gépi:    10000 × 0.3333 = 3333.0   → hiba: 0.333... (0.01%)

Ha rossz sorrendben adunk össze nagy és kis számokat:
  1 000 000 + 0.000001 = 1 000 000 (a kis szám "elvész"!)
```

**Mit tehetünk?**
- Pivot-álás (nagy pivot = kisebb szorzó = kisebb hibaterjedés)
- Stabilis algoritmus választása (QR jobb, mint normálegyenlet)
- Helyes számtani sorrend

---

### 8.2 [[kondíciószám]] – a mátrix "érzékenységmutató"

**Érzésre:** A kondíciószám megmutatja, hogy ha kicsit megváltoztatjuk a jobb oldalt ($b$), mennyire változik a megoldás ($x$). Nagy kondíciószám → rossz kondíciójú mátrix → kis bemeneti hiba is nagy megoldáshibát adhat.

**Definíció:**
$$\kappa(A) = \|A\| \cdot \|A^{-1}\|$$

A 2-es normával: $\kappa_2(A) = \sigma_{\max} / \sigma_{\min}$ (szinguláris értékek hányadosa)

**Hibakorlát:**
$$\frac{\|\delta x\|}{\|x\|} \leq \kappa(A) \cdot \frac{\|\delta b\|}{\|b\|}$$

Azaz: a relatív megoldáshiba legfeljebb $\kappa(A)$-szor akkora, mint a relatív bemeneti hiba.

---

**Konkrét szemléletes példa:**

```
Jól kondícionált mátrix:
A₁ = [2  1]   →  κ(A₁) ≈ 6.85
     [1  1]

Ha b-t 1%-kal zavarjuk meg: x is legfeljebb ~7%-kal változik.  OK!
```

```
Rosszul kondícionált (közel szinguláris) mátrix:
A₂ = [  1      1  ]   →  κ(A₂) >> 1 (akár 10⁶ is!)
     [  1   1.0001 ]

Ha b-t 0.001%-kal zavarjuk meg: x akár 1000%-kal is változhat!  KATASZTRÓFA!
```

**Intuitív képként:** A mátrix oszlopai "majdnem párhuzamosak" → sok megoldás van "majdnem jó" → kis zaj teljesen más irányba löki a megoldást.

**Mit tehetünk rossz kondíció esetén?**
- Prekondícionálás (átskálázás)
- Regularizáció (pl. Tikhonov)
- Ellenőrizni, hogy a feladat jól van-e feltéve

---

**Kerekítési hiba + kondíciószám kapcsolata:**
```
Ha κ(A) ≈ 10ᵏ, akkor kb. k tizedesjegynyi pontosságot veszítünk.

Pl. 64-bites double precision: ~15-16 jegy pontosság
    κ(A) = 10⁶  →  kb. 9-10 jegy marad  (még jó)
    κ(A) = 10¹⁵ →  alig 1 jegy marad   (katasztrófa)
```

---

## Kulcsfogalmak

- [[lineáris egyenletrendszer]] – $Ax = b$ alak
- [[mátrix]] – számok téglalap táblázata
- [[Gauss-elimináció]] – felső háromszög alak + visszahelyettesítés
- [[Gauss–Jordan]] – redukált lépcsős alak, $[A|b] \to [I|x]$
- [[pivotálás]] – numerikus stabilitást javító sorcsere
- [[LU-felbontás]] – $A = L \cdot U$, kétlépéses megoldás
- [[Cholesky-felbontás]] – $A = L \cdot L^T$, csak SPD mátrixra
- [[QR-felbontás]] – $A = Q \cdot R$, ortogonális + felső háromszög
- [[Gram–Schmidt ortogonalizáció]] – QR előállításának módszere
- [[legkisebb négyzetek módszere]] – túlhatározott rendszer optimális megoldása
- [[kondíciószám]] – $\kappa(A)$, bemeneti hibák felerősödésének mértéke
- [[numerikus stabilitás]] – az algoritmus hibaterjedési tulajdonsága
- [[előrehelyettesítés]] – $Ly = b$ megoldása (felülről lefelé)
- [[visszahelyettesítés]] – $Ux = y$ megoldása (alulról felfelé)
- [[szimmetrikus pozitív definit mátrix]] – Cholesky feltétele
- [[kerekítési hiba]] – lebegőpontos aritmetika pontatlanságai

---

## Tipikus vizsgakérdések

1. **Mit jelent az $Ax = b$ alak? Írja fel az összetevőket!**
   - $A$: $n \times n$ együtthatómátrix, $x$: ismeretlen vektor, $b$: jobb oldali (konstans) vektor. Cél: $x$ meghatározása.

2. **Mi a Gauss-elimináció lépései?**
   - Elemi sorátalakításokkal felső háromszög alakot állítunk elő, majd visszahelyettesítéssel megkapjuk $x$-et.

3. **Mi a különbség a Gauss-elimináció és a Gauss–Jordan módszer között?**
   - Gauss: felső háromszög + visszahelyettesítés. Gauss–Jordan: teljes RREF, $[I|x]$ alak, nem kell külön visszahelyettesítés.

4. **Miért szükséges a pivotálás?**
   - Kis pivot esetén a szorzó nagy lesz, és a kerekítési hiba felerősödik. Pivotálással a legnagyobb abszolút értékű elemet választjuk pivotnak, csökkentve a hibaterjedést.

5. **Mikor előnyös az LU-felbontás a sima Gauss-elimináció helyett?**
   - Ha ugyanazzal az $A$ mátrixszal több különböző $b$ vektorra kell megoldást számolni. Az LU egyszer elvégzi a "nehéz" részt, utána csak az olcsó előre-/visszahelyettesítés kell.

6. **Milyen feltétellel alkalmazható a Cholesky-felbontás? Miért előnyös?**
   - Szimmetria ($A = A^T$) és pozitív definitság ($x^TAx > 0$). Előny: kb. feleannyi művelet, mint LU, és mindig numerikusan stabil.

7. **Mire használjuk a QR-felbontást a legkisebb négyzetek feladatánál?**
   - Túlhatározott ($m > n$) rendszernél nincs pontos megoldás. QR-ral stabilan megoldható $\min \|Ax - b\|^2$, numerikusan megbízhatóbb, mint a $A^TAx = A^Tb$ normálegyenlet.

8. **Mit jelent a kondíciószám, és hogyan befolyásolja a megoldás pontosságát?**
   - $\kappa(A) = \|A\| \cdot \|A^{-1}\|$: megmutatja, mennyire erősíti fel a feladat a bemeneti hibákat. Ha $\kappa(A) = 10^k$, kb. $k$ tizedesjegynyi pontosságot veszítünk.

9. **Adjon példát, ahol pivotálás nélkül hibás az eredmény!**
   - Ld. 4. fejezet: $\varepsilon x + y = 1$, $x + y = 2$ kis $\varepsilon$ esetén 4-jegyű aritmetikával $x = 0$ jön ki pivot nélkül, pivotálással $x \approx 1$ (helyes).

10. **Mi a Gram–Schmidt eljárás szerepe a QR-felbontásban?**
    - Az $A$ mátrix oszlopvektorait ortogonorizálja és normálja → megkapjuk $Q$-t. Az $R$ az ortogonalizálás során kapott vetítési koefficiensekből áll.

---

## Rövid összefoglaló

**A nagy kép:**
```
Megoldandó: Ax = b

Módszer választás:
  ├─ Általános, egyszer kell → Gauss-elimináció
  ├─ Sok b, ugyanaz az A    → LU-felbontás
  ├─ A szimmetrikus, SPD    → Cholesky (gyorsabb!)
  ├─ Túlhatározott (m > n)  → QR + legkisebb négyzetek
  └─ Kell az explicit megoldás → Gauss–Jordan
```

**A pivotálás mindig kell** ha numerikus pontosság fontos (azaz mindig).

**A kondíciószám jelzi a bajt:** Ha $\kappa(A)$ nagy, sem a legjobb módszer sem segít igazán — a feladat rosszul kondícionált. Először a feladatot kell megvizsgálni.

**A módszerek kapcsolata:**
- Gauss-elimináció = LU-felbontás implicit elvégzése
- Gauss–Jordan = Gauss kiterjesztése (felfelé is nulláz)
- Cholesky = LU speciális esete ($L = U^T$) SPD mátrixra
- QR = ortogonalizáláson alapul, legjobban kezeli a numerikus hibákat

**Praktikus ökölszabályok:**
```
κ(A) < 100      → nyugodtan bármelyik módszer
κ(A) ~ 10⁶     → figyelni kell, pivotálás kötelező
κ(A) > 10¹²    → a megoldás 64-bites double-on értelmetlen lehet
```
