# Programozás alapjai (C) – záróvizsga / szóbeli szintű kidolgozás

*Forrás: [[progalap1]] + [[progalap2]] vázlat kibontva. Az Obsidian [[linkek]] változatlanok maradtak.*

---

# Rész I. Algoritmusok és vezérlési szerkezetek C nyelven

## 1. Alapfogalmak: [[algoritmus]], vezérlési szerkezet, [[strukturált programozás]]

### Definition
Az **[[algoritmus]]** véges, egyértelmű lépéssorozat egy feladat megoldására: minden lépés pontosan meg van határozva, és véges időn belül befejeződik. A **vezérlési szerkezet** azt mondja meg, **milyen sorrendben** hajtódnak végre ezek a lépések (egymás után, feltételtől függően, vagy ismétlődve).

### How it works
A **[[strukturált programozás]]** három alapvető vezérlési mintára épül: **szekvencia** (egymás után), **szelekció** (elágazás), **iteráció** (ciklus). Ezek kombinációjával bármely ésszerű algoritmus felírható anélkül, hogy „ugráló” `goto` szerkezetre lenne szükség — ez javítja az átláthatóságot és a hibakeresést.

### Syntax
Nincs külön „algoritmus kulcsszó” C-ben; az algoritmus a `main` és a **[[függvény]]**ek utasításaiból áll.

### Step-by-step execution
A futás elején a vezérlés a `main` első utasításánál van. Utasításról utasításra halad (szekvencia), amíg elágazás vagy ciklus meg nem változtatja a következő végrehajtandó lépést. **[[függvény]]** híváskor a vezérlés a hívott függvényhez ugrik, ott szekvenciálisan fut, majd **[[return]]** után visszatér a hívóhoz.

### Example
```c
/* Beolvasás -> feltétel -> ismétlés: tipikus algoritmus-váz */
#include <stdio.h>
int main(void) {
    int n;
    scanf("%d", &n);           /* 1. lépés: bemenet */
    if (n < 0)                 /* 2. lépés: döntés */
        n = -n;
    int i = 0;
    while (i < n) {            /* 3. lépés: ismétlés */
        printf("%d\n", i);
        i++;
    }
    return 0;
}
```
Először beolvassuk `n`-et, majd ha negatív, normalizáljuk. Ezután a ciklus `0`-tól `n-1`-ig kiírja az indexeket.

### Common mistakes
- Összekeverni az **algoritmust** (logika) a **konkrét C kóddal** (szintaxis): vizsgán mindkettőt elvárják, de külön is tudni kell megfogalmazni.
- **Végtelen lépéssor** (nem véges algoritmus) — pl. ciklusban soha nem változik a feltétel.

### When to use
Minden program megírásakor: először gondold át az algoritmust (papíron vagy pszeudókódban), utána írd le C-ben.

### Comparison (if relevant)
**Strukturált** megközelítés vs. **nem strukturált** (`goto`-halmaz): az egyetemi C-kurzusok a strukturált hármast várják el szóban.

**⚠️ Exam tip:** Tudj példát mondani **szekvenciára, elágazásra és ciklusra** egyetlen feladaton belül (pl. összegzés pozitív számokra).

---

## 2. [[szekvenciális vezérlés]]

### Definition
A **[[szekvenciális vezérlés]]** azt jelenti, hogy az utasítások **egymás után**, a forráskódban leírt sorrendben hajtódnak végre, egyik a másik után.

### How it works
Ez a C **alapértelmezett** viselkedése: nincs elágazás vagy ciklus, ami megváltoztatná a sorrendet. A **[[utasításblokk]]** (`{ ... }`) belsejében is felülről lefelé halad a végrehajtás.

### Syntax
```c
x = 5;
y = x + 2;
printf("%d\n", y);
```
Mindhárom sor egymás után fut.

### Step-by-step execution
1. `x` kap értéket a **[[stack]]**en (lokális változó esetén) vagy globális tárban.  
2. `y` kiértékelése: beolvasás `x` aktuális értékéből, összeadás, értékadás `y`-nak.  
3. `printf` hívás: a formátumstring és `y` értéke a hívási konvenció szerint kerül átadásra, majd kiírás.

### Example
```c
int a = 10;
a = a * 2;
a = a + 1;   /* most a == 21 */
```
Sorrend számít: ha felcserélnénk a két értékadást, más lenne az eredmény.

### Common mistakes
- Azt hinni, hogy a fordító „optimalizálásként” átrendezhet bármit: **szekvenciapontok** (`;`, teljes kifejezések) között a látható mellékhatások sorrendje kötelezően megmarad a C szabályai szerint — de ezt vizsgán elég annyiban tudni, hogy **a sorrend fontos**.

### When to use
Minden olyan résznél, ahol nincs döntés vagy ismétlés: inicializálás, egyszeri számítás, egymásra épülő lépések.

### Comparison (if relevant)
**Szekvencia** vs. **elágazás**: elágazásnál a vezérlés **csak az egyik ágat** futtatja; szekvenciánál **minden** lépés lefut.

**⚠️ Common mistake:** `if (x = 5)` helyett `if (x == 5)` — az értékadás **szekvenciában** lefut és mellékhatásként módosítja `x`-et; vizsgán gyakran kérdezik.

---

## 3. Elágazásos vezérlés

### 3.1 `if`

#### Definition
Az **`if`** **feltételes utasítás**: a mögötte lévő blokk (vagy egyetlen utasítás) **csak akkor** fut le, ha a feltétel **igaz** (nem nulla).

#### How it works
C-ben a feltétel **skalár kifejezés**: **0** = hamis, **bármilyen nem nulla** = igaz. A feltételt kiértékeljük; ha igaz, belépünk az ágba.

#### Syntax
```c
if (feltétel)
    utasítás;           /* egy utasítás */

if (feltétel) {         /* blokk */
    utasítás1;
    utasítás2;
}
```

#### Step-by-step execution
1. Kiértékelődik a `feltétel` (pl. `x > 0`).  
2. Ha eredmény **0**, a blokk kihagyása, a vezérlés az `if` után folytatódik.  
3. Ha **nem 0**, végrehajtódik a blokk, majd az `if` után.

#### Example
```c
if (x > 0)
    printf("pozitiv\n");
```
Ha `x == 3`, kiírás történik; ha `x == -1`, a `printf` nem fut.

#### Common mistakes
- Feltétel nélküli `if` — szintaktikai hiba.  
- Több utasítás `if` nélküli blokk nélkül: csak az **első** sor tartozik az `if`-hez.

#### When to use
Egyetlen, egyszeri döntés: „csak akkor csináljuk, ha…”.

#### Comparison (if relevant)
**`if`** vs. **`if-else`**: az `if`-nek nincs „különben” ága.

**⚠️ Exam tip:** Magyarázd el: **„mi számít hamisnak C-ben a feltételben?”** — a nulla skalárérték.

---

### 3.2 `if`–`else`

#### Definition
Az **`if-else`** **kétirányú döntés**: az egyik blokk fut **igaz** feltételnél, a másik **hamis** feltételnél.

#### How it works
Kizárólagos választás a két ág között (az `else` mindig a **legközelebbi** felvezetés nélküli `if`-hez tartozik — **dangling else** probléma).

#### Syntax
```c
if (feltétel)
    igaz_ag;
else
    hamis_ag;
```

#### Step-by-step execution
1. Feltétel kiértékelése.  
2. Igaz → `igaz_ag`, majd a szerkezet után.  
3. Hamis → `hamis_ag`, majd a szerkezet után.

#### Example
```c
if (x % 2 == 0)
    printf("paros\n");
else
    printf("paratlan\n");
```

#### Common mistakes
- **`else if`** helyett egymásba fésült `if`–`else` zárójelezés elrontása.  
- `else` után feltétel — helyette **`else if (új_feltétel)`** kell.

#### When to use
Két egymást kizáró eset: igen/nem, páros/páratlan.

#### Comparison (if relevant)
**`if-else`** vs. **`switch`**: utóbbi tipikusan **egy változó diszkrét értékei** szerint választ; az `if-else` **tetszőleges logikai** feltételeket enged.

**⚠️ Common mistake:** `if (a == b == c)` — C-ben ez **nem** „három szám egyenlő”; a `==` balról jobbra asszociál, és 0/1 értékeket ad.

---

### 3.3 `else if` lánc

#### Definition
Az **`else if` lánc** **több, sorban vizsgált feltétel**: az **első igaz** ág fut le, a többi ágat a rendszer **kihagyja**.

#### How it works
Gyakorlatilag egymásba ágyazott `if-else` szerkezet: `if ... else if ... else if ... else`.

#### Syntax
```c
if (pont >= 90)
    jegy = 5;
else if (pont >= 80)
    jegy = 4;
else if (pont >= 65)
    jegy = 3;
else
    jegy = 2;
```

#### Step-by-step execution
1. Első feltétel: ha igaz → `jegy = 5`, **vége** (többi ág nem fut).  
2. Ha hamis, jön a második feltétel, stb.  
3. `else` opcionális „minden más” ág.

#### Example
Jegybesorolás, hőmérséklet-tartományok, menü logika több logikai feltétellel.

#### Common mistakes
- **Rossz sorrend**: pl. `pont >= 65` előbb, mint `pont >= 90` — a szélesebb tartomány „elkapja” az eseteket.  
- **Hiányzó `else`**: nem hiba, de lehet **nem kezelt** eset.

#### When to use
Több **kizáró** tartomány vagy eset, ahol nem egyetlen változó konstans értékei döntenek (akkor lehet `switch` is).

#### Comparison (if relevant)
**`else if` lánc** vs. **`switch`**: a lánc **bármilyen** boolean kifejezést enged; a `switch` egy kifejezés **konstans** `case` címkéihez hasonlít (C-ben a `case` címkék konstansok).

**⚠️ Exam tip:** „Miért fontos a feltételek **sorrendje**?” — mert csak az első igaz ág fut.

---

### 3.4 `switch`

#### Definition
A **`switch`** **többirányú elágazás**, amely egy **egész típusú kifejezés** értékét hasonlítja a **`case` címkékhez** (konstans értékek).

#### How it works
A vezérlés a megfelelő **`case`**-hez ugrik. **Ha nincs `break`**, **beleesés** (**fall-through**) történik a következő `case`-be — ez néha szándékos, gyakran hiba.

#### Syntax
```c
switch (kifejezés) {
    case konstans1:
        utasítások;
        break;
    case konstans2:
        utasítások;
        break;
    default:
        utasítások;
        break;
}
```

#### Step-by-step execution
1. Kiértékelődik a zárójelben lévő kifejezés (pl. `int` vagy `char` numerikus érték).  
2. Összehasonlítás a `case` értékekkel.  
3. Egyezés → ugrás oda; **`break`** → kilépés a `switch`-ből.  
4. Ha egyik sem egyezik → **`default`** (ha van).

#### Example
```c
switch (menuPont) {
    case 1:
        printf("Inditas\n");
        break;
    case 2:
        printf("Beallitasok\n");
        break;
    default:
        printf("Ismeretlen\n");
        break;
}
```

#### Common mistakes
- **`break` elhagyása** → több ág lefut egymás után.  
- **`case` nem konstans** — fordítási hiba.  
- **`switch` lebegőpontos kifejezéssel** — C-ben nem megengedett / nem praktikus (típusok korlátai).

#### When to use
Sok **diszkrét, előre ismert** érték (menü, nap kódja, parancs kód). Olvashatóbb lehet, mint hosszú `else if` lánc.

#### Comparison (if relevant)
**`switch`** vs. **`if` lánc**: `switch` egy helyen mutatja az összes ágat; **`if`** rugalmasabb összetett feltételekkel.

**⚠️ Exam tip:** Tudj **fall-through**-ról beszélni: mikor szándékos (több `case` ugyanarra a kódra), mikor hiba.

---

## 4. Iterációs vezérlés (ciklusok)

### 4.1 `while`

#### Definition
A **`while` ciklus** **elöltesztelő**: először a **feltételt** nézzük; ha igaz, lefut a **ciklusmag**, majd újra a feltétel, stb.

#### How it works
Ha a feltétel **elsőre hamis**, a mag **nulla alkalommal** fut.

#### Syntax
```c
while (feltétel) {
    ciklusmag;
}
```

#### Step-by-step execution
1. Feltétel kiértékelése.  
2. Ha 0 → kilépés a ciklusból.  
3. Ha nem 0 → mag végrehajtása → vissza az 1. lépésre.

#### Example
```c
while (x > 0) {
    printf("%d ", x);
    x--;
}
```

#### Common mistakes
- **Végtelen ciklus**: a mag nem változtatja a feltételhez tartozó állapotot.  
- **Off-by-one**: rossz feltétel (`while (i <= n)` vs `i < n`).

#### When to use
**Ismeretlen** ismétlésszám: addig megyünk, **amíg** valami igaz (pl. beolvasás EOF-ig).

#### Comparison (if relevant)
**`while`** vs. **`for`**: a `while` jó, ha nincs természetes „számláló” struktúra; a **`for`** akkor kényelmes, ha **inicializálás + teszt + léptetés** egy helyen van.

**⚠️ Common mistake:** `while (i = n)` — értékadás, nem összehasonlítás; a feltétel „igaz”, ha `n` nem 0.

---

### 4.2 `do`–`while`

#### Definition
A **`do-while` ciklus** **hátultesztelő**: először a **mag** fut **legalább egyszer**, utána jön a feltétel.

#### How it works
A mag után értékeljük a feltételt; ha igaz, újabb iteráció.

#### Syntax
```c
do {
    ciklusmag;
} while (feltétel);  /* pontosvessző kötelező! */
```

#### Step-by-step execution
1. Mag végrehajtása.  
2. Feltétel: ha igaz → 1.; ha hamis → kilépés.

#### Example
```c
int valasz;
do {
    printf("Valassz (1-3): ");
    scanf("%d", &valasz);
} while (valasz < 1 || valasz > 3);
```

#### Common mistakes
- **`while` után hiányzó `;`** — szintaktikai hiba.  
- Olyan esetben használni, ahol **nulla iteráció** kellene — akkor **`while`** vagy **`for`** kell.

#### When to use
**Legalább egy** interakció: menü, validált beolvasás.

#### Comparison (if relevant)
**`while`** vs. **`do-while`**: előbbi **0 vagy több**, utóbbi **1 vagy több** futás.

**⚠️ Exam tip:** Egy mondatban: **„elöltesztelő vs. hátultesztelő”**.

---

### 4.3 `for`

#### Definition
A **`for` ciklus** tipikusan **számlálós**: egy helyen összefoglalja az **inicializálást**, a **folytatási feltételt** és a **léptetést**.

#### How it works
A fejléc három része: `for (init; feltétel; léptetés)`. Minden iteráció előtt: **első iteráció előtt** egyszer `init`; minden **kör elején** `feltétel` (hamis → kilépés); a mag után **`léptetés`**.

#### Syntax
```c
for (int i = 0; i < n; i++) {
    osszeg += a[i];
}
```
(C99+ `for`-ban deklarált `i` hatóköre blokk-specifikus lehet — fordító / standard szerint.)

#### Step-by-step execution
1. `i = 0` egyszer.  
2. `i < n`? Ha hamis → vége.  
3. Mag: `osszeg += a[i]`.  
4. `i++` → vissza 2.

#### Example
Tömb bejárása, sorozatszámítás, `n` darab ismétlés.

#### Common mistakes
- **`for (;;)`** végtelen ciklus — szándékos lehet, de veszélyes.  
- **`<= n` vs `< n`** — egy elemmel több vagy kevesebb iteráció.

#### When to use
**Ismert** vagy **indexelt** ismétlés: tömbök, fix `N` lépés.

#### Comparison (if relevant)
**`for`** vs. **`while`**: funkcionálisan átírhatók egymásba; a `for` **strukturáltabb** számláláshoz.

**⚠️ Exam tip:** Rajzold fel táblázatban **`i` értékét** iterációnként — vizsgán gyakori kérdés.

---

## 5. Vezérlés módosítása: `break`, `continue`, `return`

### Definition
- **`break`**: azonnali kilépés a legbelső **`switch`** vagy **ciklus** szerkezetből.  
- **`continue`**: a ciklus **hátralévő részét** kihagyja, **következő iteráció** jön (feltétel / léptetés a `for`-nál).  
- **`return`**: kilépés a **[[függvény]]**ből; opcionálisan visszaad értéket a hívónak.

### How it works
Ezek **nem** strukturált elágazást csinálnak új típusként, hanem a normál folyamatot **megszakítják** vagy **átugranak** egy részt.

### Syntax
```c
while (1) {
    if (feltetel_break)
        break;
    if (feltetel_continue)
        continue;
    /* tovabbi kod */
}

int foo(void) {
    return 42;
}
```

### Step-by-step execution (pl. `for` + `continue`)
1. Fejléc feltétel.  
2. Ha `continue` a magban → **léptetés** fut (`for`-nál), majd új feltétel.  
3. `break` → ciklus azonnal véget ér.

### Example
Keresés tömbben: megtaláltuk az elemet → `break`.

### Common mistakes
- **`break` nem ugrik ki több egymásba ágyazott ciklusból** egyszerre — csak egy szint.  
- **`continue` `switch`-ben** — nem a `switch`-re vonatkozik így (a `continue` a **körülötte lévő ciklusra**).

### When to use
- **`break`**: korai kilépés keresésnél, hibánál.  
- **`continue`**: „ezt az elemet hagyjuk ki”, de a ciklus menjen tovább.  
- **`return`**: függvény eredménye + azonnali visszatérés.

### Comparison (if relevant)
**`break`** vs. **`return`**: a `break` **ciklust/switch-et** hagy el; a `return` a **függvényt**.

**⚠️ Common mistake:** `break` használata **`if`-ben**, ami **nem** ciklus része — csak szintaktikai hiba vagy rossz hely (pl. `if` belsejében lévő `switch`-ben OK).

**⚠️ Exam tip:** „Mit csinál a `continue` a **`while`** és a **`for`** ciklusban?” — `while`-nál közvetlenül a feltételhez ugrik; `for`-nál előbb a **léptető kifejezés** fut.

---

## 6. [[függvény]]ek és eljárásvezérlés

### 6.1 Alapfogalmak: deklaráció, definíció, hívás

#### Definition
A **[[függvény]]** **újrafelhasználható** kódegység névvel, **paraméterlistával** és opcionális **visszatérési típussal**. A **prototípus** (**deklaráció**) megadja az **aláírást**; a **definíció** tartalmazza a törzset.

#### How it works
Híváskor a hívó helyén **aktuális paraméterek** kiértékelődnek; létrejön egy **aktivációs rekord** (gyakran **[[stack]]**en): lokális változók, visszatérési cím. A vezérlés a függvény elejére ugrik, fut a törzs, **`return`** után vissza.

#### Syntax
```c
/* prototípus */
int max(int a, int b);

/* definíció */
int max(int a, int b) {
    return (a > b) ? a : b;
}

/* hívás */
int m = max(3, 7);
```

#### Step-by-step execution (memória szemlélet)
1. `max(3, 7)` hívás: `a` és `b` **paraméterváltozók** kapják a **másolatot** (érték szerinti átadás).  
2. A függvény törzse a **stack frame**-ben fut.  
3. `return 7` → érték visszakerül (regiszterben / stacken, hívási konvenció szerint), a frame felszabadul, a hívó folytatja.

#### Example
Lásd fent: két `int` közül a nagyobb.

#### Common mistakes
- Prototípus és definíció **nem egyezik** — linker vagy fordító hiba.  
- **`void` függvényből érték visszaadása** — hiba.  
- **Hiányzó prototípus** régi C-ben veszélyes (implicit deklaráció) — ma is kerülendő.

#### When to use
Modularizálás, ismétlődő logika, tesztelhető egységek.

#### Comparison (if relevant)
**[[függvény]]** vs. **makró**: a makró **szöveghelyettesítés**, nincs valódi hívás / típusellenőrzés ugyanúgy; vizsgán a **függvény** az alap.

**⚠️ Exam tip:** „Mi van a **stack**en függvényhíváskor?” — visszatérési cím, paraméterek, lokális változók (implementációfüggő részletek, de az elv ez).

---

### 6.2 Paraméterátadás: **érték szerint**, **pointer** a cím szerinti hatáshoz

#### Definition
C-ben az alapértelmezett **[[érték szerinti átadás]]** (**call by value**): a függvény **másolatot** kap. A hívó változóját **kívülről módosítani** csak **[[pointer]]** átadásával lehet (vagy globális / statikus adat — kerülendő tananyagban példának).

#### How it works
**Pointer paraméter**: a **cím** másolódik (ami szintén érték — a cím értéke), de ugyanarra a **memóriacellára** mutat; **dereferálással** (`*p`) módosítható a hívó adata.

#### Syntax
```c
void novel(int *p) {
    if (p != NULL)
        (*p)++;   /* zárójel fontos: *p++ más lenne! */
}
```

#### Step-by-step execution
```c
int x = 5;
novel(&x);
```
1. `novel` kap egy `int*`-ot, amely **`x` címét** tartalmazza.  
2. `(*p)++` növeli az **`x` memóriacellájában** lévő értéket.  
3. `x` most 6 a hívóban is.

#### Example
Két érték csere `swap` (pointer kell):
```c
void swap(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}
```

#### Common mistakes
- **`void f(int x) { x++; }`** — a hívó **`x`-je nem változik**.  
- **`*p++` vs `(*p)++`** — operátor precedencia; vizsgán klasszikus csapda.

#### When to use
- Kis adat (`int`, `double`): érték szerint egyszerű.  
- Nagy struktúra, tömb, vagy **visszaadás több értékre**: pointer / struktúra.

#### Comparison (if relevant)
**Érték szerint** vs. **cím szerinti hatás (pointerrel)**: előbbi **biztonságosabb** mellékhatás szempontjából; utóbbi **szükséges** módosításhoz és tömböknél.

**⚠️ Exam tip:** „Miért kell **`&x`** a `scanf("%d", &x)`-nél?” — mert a `scanf`-nek **cím** kell, hogy **oda** írjon.

---

### 6.3 [[rekurzió]]

#### Definition
A **[[rekurzió]]** olyan technika, amikor a **függvény önmagát hívja** egy **kisebb / egyszerűbb** részproblémára redukálva az eredeti feladatot.

#### How it works
Minden hívás **új stack frame**-et kap. Kell **báziseset** (megállás), különben **stack overflow**. A rekurzív lépés közelebb visz a bázishoz.

#### Syntax
```c
unsigned long fact(unsigned n) {
    if (n <= 1)          /* báziseset */
        return 1;
    return n * fact(n - 1);  /* rekurzív lépés */
}
```

#### Step-by-step execution
`fact(3)`:
1. `3 * fact(2)` — frame `n=3` várakozik.  
2. `2 * fact(1)` — frame `n=2`.  
3. `fact(1)` → `1` (bázis).  
4. Visszaszámítás: `2*1=2`, majd `3*2=6`.  
A **verem** mélysége ~ a rekurzió mélysége.

#### Example
Faktoriális, Fibonacci (naiv rekurzió lassú — de szemléltet), bináris keresés rekurzívan.

#### Common mistakes
- **Hiányzó báziseset** → végtelen rekurzió / stack overflow.  
- **Túl mély rekurzió** nagy `n`-re.

#### When to use
Fa bejárás, oszd meg és uralkodj, matematikai definíció természetes rekurzív (pl. `gcd`).

#### Comparison (if relevant)
**Rekurzió** vs. **iteráció**: rekurzió **olvashatóbb** lehet; iteráció **költséghatékonyabb** verem szempontból.

**⚠️ Exam tip:** Sorold fel: **báziseset + rekurzív hívás + konvergencia** a bázis felé.

---

# Rész II. Adattípusok, kifejezések, összetett típusok, memória

## 1. [[adattípus]] alapfogalom

### Definition
Az **[[adattípus]]** meghatározza, **milyen értékek** lehetségesek (**értékkészlet**), **mennyi memória** tipikusan kell, és **milyen műveletek** értelmezettek.

### How it works
A fordító típusinformáció alatt **ellenőrzi** az értékadásokat, **kiosztja** a változók méretét, és **értelmezi** a biteket (pl. előjeles egész vs. lebegőpont).

### Syntax
```c
int x;
double y;
char c;
```

### Step-by-step execution
Változó definíciókor (lokálisan) **stacken** foglalódik (implementáció szerint) **nem inicializált** értékkel (automatikus tárolási időtartam — **[[undefined behavior]]** olvasni, ha nem inicializált).

### Example
```c
unsigned int u = 4000000000u;  /* nagy pozitív, ha befér */
```

### Common mistakes
- **Típus és scanf formátum** nem egyezik — **[[undefined behavior]]**.

### When to use
Minden változónál meg kell választani a **legszűkebb megfelelő** típust (olvashatóság + tartomány).

### Comparison (if relevant)
**Erős** vs. **gyenge** típusosság: C **gyengébb** — sok **implicit konverzió**.

**⚠️ Exam tip:** „Miért fontos a **típus**?” — tartomány, pontosság, értelmezés, hibák elkerülése.

---

## 2. Egyszerű adattípusok

### 2.1 Egész típusok (`char`, `short`, `int`, `long`, `signed` / `unsigned`)

#### Definition
Az **egész típusok** **diszkrét** egész értékeket tárolnak. **`signed`** esetén negatív is lehet (tipikusan **kettes komplemens**); **`unsigned`** csak nemnegatív, de **nagyobb felső határ** ugyanakkora bitméret mellett.

#### How it works
A **konkrét méretek** **implementációfüggők** (`sizeof`), de van **minimum követelmény** (pl. `int` legalább 16 bit — gyakorlatban 32). Az **[[overflow]]** előjelest egésznél **C-ben gyakran UB** (signed overflow) — vizsgán fontos említés.

#### Syntax
```c
signed int a = -5;
unsigned int b = 10U;
short s;
long L = 42L;
```

#### Step-by-step execution
`unsigned` műveletek modulo \(2^n\) szerint viselkednek (szabályosan definiált wrap); **`signed` overflow** sok esetben **[[undefined behavior]]**.

#### Example
```c
unsigned char uc = 255;
uc++;  /* 0, wrap */
```

#### Common mistakes
- **`unsigned` és `signed` összehasonlítás** egy kifejezésben → a **`signed` gyakran `unsigned`-dá konvertálódik**, meglepő eredmény.  
- **`scanf("%u", &signed_int)`** keverése.

#### When to use
- **`unsigned`**: bitműveletek, méret/index nemnegatív, bitmask.  
- **`signed`**: általános számolás.

#### Comparison (if relevant)
**`int` vs `long`**: nagyobb tartomány; fájlban / hálózaton **fix méret**hez `<stdint.h>` (`int32_t` stb.) — ha a tananyag említi.

**⚠️ Exam tip:** „Mi a **kettes komplemens** lényege egy mondatban?” — negatív számok ábrázolása úgy, hogy az összeadás ugyanúgy működjön.

---

### 2.2 Valós típusok (`float`, `double`)

#### Definition
A **`float`** és **`double`** **lebegőpontos** típusok (tipikusan **IEEE 754** szerinti **előjel + mantissza + kitevő**).

#### How it works
**Véges bitszám** → sok valós szám **közelítés**; összehasonlítás **`==`** gyakran **hibás**.

#### Syntax
```c
float x = 1.5f;
double y = 1.5;
```

#### Step-by-step execution
`0.1 + 0.2` kiértékelése bináris lebegőpontban nem ad pontosan `0.3`-at — kerekítési hiba.

#### Example
```c
double a = 0.1, b = 0.2;
/* Kerüljük: if (a + b == 0.3) */
if (fabs((a + b) - 0.3) < 1e-9) { /* közelítő egyenlőség */ }
```

#### Common mistakes
- **`float` pontosság** elegendőtlen pénzügyi számításra.  
- **`=` vs `==`** lebegőpontnál is.

#### When to use
Mérnöki, tudományos, grafikus számítások; ha kell **nagy pontosság**, **`double`**.

#### Comparison (if relevant)
**`float`** vs **`double`**: sebesség vs pontosság / méret.

**⚠️ Common mistake:** `if (x == y)` lebegőpontnál.

---

### 2.3 Logikai típus (`bool`, C99+ `<stdbool.h>`)

#### Definition
A **`bool`** (**`_Bool`**) logikai érték: **`true` / `false`**. Régebbi C-ben is volt logika: **0 hamis, nem 0 igaz**.

#### How it works
Logikai operátorok: **`&&`**, **`||`**, **`!`**. **Rövidzárlat**: `&&` / `||` esetén a jobb oldalt **nem** mindig értékeljük ki.

#### Syntax
```c
#include <stdbool.h>
bool jo = (x > 10);
```

#### Step-by-step execution
`if (p != NULL && *p == 0)` — ha `p` null, a `*p` **nem** értékelődik ki (biztonságos).

#### Example
Lásd fent.

#### Common mistakes
- **`if (a & b)`** bitenkénti ÉS **nem** logikai — más eredmény.

#### When to use
Olvasható flag-ek; de sok C kód `int`-et használ 0/1 értékekkel.

#### Comparison (if relevant)
**`&&` vs `&`**: logikai vs bitművelet.

**⚠️ Exam tip:** **Rövidzárlat** magyarázata példával.

---

### 2.4 Karakter típus (`char`, karakterlánc)

#### Definition
A **`char`** **egy bájt** (implementáció szerint signed vagy unsigned lehet `char` maga!) — **karakterkód** (pl. **ASCII**) tárolására; **numerikusan is** viselkedhet.

#### How it works
**C string**: **`char` tömb**, **`'\0'`** (**null terminator**) jelzi a végét.

#### Syntax
```c
char c = 'A';        /* karakter literál */
const char *s = "alma";  /* string literál: statikus, olvasható memória */
char buf[10] = "pi";     /* 'p','i','\0', ... */
```

#### Step-by-step execution
`'A'` tipikusan **65** (ASCII). A `"alma"` memóriában: `'a','l','m','a','\0'`.

#### Example
```c
printf("%c %d\n", c, c);  /* A és kódja */
```

#### Common mistakes
- **`'A'` vs `"A"`**: előbbi `char`, utóbbi `char*` pointer stringre.  
- **Buffer overflow**: `char t[3]; strcpy(t, "hosszu");` — veszélyes függvények.

#### When to use
Szöveg, bemenet/kimenet, protokoll bájtok.

#### Comparison (if relevant)
**Karakter** vs **string**: egy elem vs. nullával terminált sorozat.

**⚠️ Exam tip:** Miért **`'\0'`**? — hogy a függvények (pl. `strlen`, `printf("%s")`) tudják, hol a vég.

---

## 3. Kifejezések, **operátorok**, **precedencia**, **típuskonverzió**

### Definition
A **kifejezés** **operátorok** és **operandusok** kombinációja, amely **értékké** redukálódik (és lehet mellékhatás).

### How it works
A **precedencia** megmondja, melyik operátor „erősebb” (pl. `*` az `+` előtt). Az **asszociativitás** megmondja, azonos precedenciánál **balra** vagy **jobbra** köt. **Implicit konverzió**: „kisebb” típus nagyobba emelkedik kifejezésben; **explicit**: **cast** `(double)a`.

### Syntax
```c
int a = 5, b = 2;
double r = (double)a / b;   /* 2.5, nem 2 */
```

### Step-by-step execution
`a / b` egészként **2** lenne; cast után `a` `double`, osztás **lebegőpontos**.

### Example
```c
if (a & 1)  /* páratlan bit */
```

### Common mistakes
- **`a / b` egész osztás** elveszi a tizedest.  
- **Precedencia**: `*p++` vs `(*p)++`.

### When to use
Minden számításnál tudatosan: melyik operandus milyen típusú legyen.

### Comparison (if relevant)
**Implicit** vs **explicit** konverzió: utóbbi olvashatóbb szándék.

**⚠️ Exam tip:** „Miért **`(double)a / b`** és nem **`(double)(a/b)`**?”

---

## 4. Összetett adattípusok

### 4.1 [[tömb]]

#### Definition
A **[[tömb]]** **azonos típusú** elemek **fix méretű**, **folytonos memóriabeli** sorozata.

#### How it works
Indexelés **0-tól** `n-1`-ig. A név sok kontextusban **„első elem címévé”** alakul (**tömb–pointer dekay**).

#### Syntax
```c
int a[10];
a[0] = 3;
```

#### Step-by-step execution
`a[i]` címének képlete szemléletesen: **`base + i * sizeof(elem)`**. Ezért **O(1)** indexelés.

#### Example
```c
for (int i = 0; i < 10; i++)
    a[i] = i * i;
```

#### Common mistakes
- **Túlindexelés** — **[[undefined behavior]]**.  
- **`int a[n];`** — C99 **VLA** (fordítófüggő); vizsgán óvatosan.

#### When to use
Fix méretű sorozat, mátrix (`int m[3][4]`).

#### Comparison (if relevant)
**Tömb** vs **dinamikus tömb (`malloc`)**: előbbi stack/static, méret fordítási / VLA esetén korlátos; heap rugalmasabb.

**⚠️ Exam tip:** „Mi a különbség **`sizeof(a)`** a **deklaráció helyén** vs függvényparaméter `int a[]` esetén?” — paraméterként **pointerméret** lesz.

---

### 4.2 [[pointer]]

#### Definition
A **[[pointer]]** olyan változó, amely **memóriacímet** tárol, és típushoz kötött: **`T*`** azt jelenti, „`T` típusú objektumra mutat”.

#### How it works
**`&`**: cím képzése. **`*`**: dereferálás — „ami a címen van”. **Pointerarithmetika**: `p+1` a következő **`sizeof(T)`** bájttal odébb mutat.

#### Syntax
```c
int x = 5;
int *p = &x;
*p = 7;     /* x is 7 */
```

#### Step-by-step execution (memória)
- `x` stacken foglal (pl. cím 0x1000, érték 5).  
- `p` külön cella (pl. 0x2000), értéke **0x1000**.  
- `*p = 7` írás a **0x1000** címre.

#### Example
Tömb bejárás pointerrel:
```c
int a[3] = {1,2,3};
int *p = a;  /* &a[0] */
printf("%d\n", *(p+1)); /* 2 */
```

#### Common mistakes
- **Null pointer dereferálása** — UB / crash.  
- **Függő pointer** (**dangling**): `free` után használat.  
- **`int* p, q;`** — csak `p` pointer, `q` `int` — zavaró; jobb külön sor.

#### When to use
Tömb átadás függvénynek, **helyben módosítás**, dinamikus memória, adatszerkezetek.

#### Comparison (if relevant)
**Tömb név** vs **pointer**: sok kifejezésben ekvivalens (`a[i]` ↔ `*(a+i)`).

**⚠️ Exam tip:** Rajzold le **`p`**, **`*p`**, **`&x`** szerepét.

---

### 4.3 [[struct]]

#### Definition
A **[[struct]]** **különböző típusú mezőket** egy **logikai rekordba** fűz; minden mezőnek **saját** memóriaterülete van (általában **egymás után**, **padding** miatt lehet „lyuk”).

#### How it works
Hozzáférés: **`.`** értékre; **`->`** ha **`struct*`** pointer van (`p->mezo` ≡ `(*p).mezo`).

#### Syntax
```c
struct Hallgato {
    int id;
    char nev[50];
};

struct Hallgato h;
h.id = 123;
```

#### Step-by-step execution
A `struct` objektum egy **összefüggő** memóriablokk; másolás **érték szerint** másolhatja az egész rekordot (nagy lehet).

#### Example
```c
void kiir(const struct Hallgato *hp) {
    printf("%d %s\n", hp->id, hp->nev);
}
```

#### Common mistakes
- **Önhivatkozás** csak **pointerrel** (`struct Node* next;`), nem beágyazott érték.  
- **Kezdetlen mező** olvasása.

#### When to use
Entitások modellezése: hallgató, dátum, gráf csomópont.

#### Comparison (if relevant)
**[[struct]] vs [[union]]**: struct **minden mezőt** eltárol; union **közös helyet** oszt meg.

**⚠️ Exam tip:** **`->` vs `.`** mikor?

---

### 4.4 [[union]]

#### Definition
A **[[union]]** olyan szerkezet, ahol a **mezők ugyanazon a memóriaterületen** osztoznak; egyszerre tipikusan **csak egy** értelmezés „aktív”.

#### How it works
Méret ≈ a **legnagyobb mező** mérete (plusz padding). **Type punning** óvatosan — **[[undefined behavior]]** kockázat, ha nem megfelelően (tananyag szerint: egyszerű példák, bitmezű protokoll).

#### Syntax
```c
union Adat {
    int i;
    float f;
};
union Adat u;
u.i = 42;
```

#### Step-by-step execution
`u.i` írás után `u.f` olvasása **értelmetlen** lehet (különböző típusú ábrázolás).

#### Example
Protokoll mező, ahol ugyanaz a bájtsor **`int`**-ként vagy **más** értelmezésben jön — csak szabályos mintákban.

#### Common mistakes
- Aktív mező **nyomon követésének** elmulasztása.  
- **Unióban nem triviális** objektumok (C11 `_Alignas`, stb.) — haladó.

#### When to use
Memóriatakarékosság, alacsony szintű adatnézetek (óvatosan).

#### Comparison (if relevant)
Lásd struct fejezet.

**⚠️ Common mistake:** „**union** több mezőt **egyszerre** tárol” — **nem**; **ugyanaz a bájttartomány**, több nézőpont.

---

## 5. `typedef` és típusalias

### Definition
A **`typedef`** **új nevet** ad egy meglévő típusnak (**alias**), nem hoz létre **új szemantikai** típust.

#### How it works
Olvashatóság, rövidítés **[[struct]]** típusoknál.

#### Syntax
```c
typedef struct Hallgato {
    int id;
    char nev[50];
} Hallgato;

Hallgato h;  /* struct kulcsszo nelkul */
```

#### Step-by-step execution
Fordítási időbeli név-feloldás; futási különbség nincs.

#### Example
```c
typedef int* IntPtr;  /* figyelem: typedef int* A, B; mindketto pointer */
```

#### Common mistakes
- **`const` és typedef** sorrendje zavaró lehet.

#### When to use
API-k, ismétlődő összetett típusok.

#### Comparison (if relevant)
**`typedef`** vs **`#define`**: typedef **típusbiztosabb**, nem szövegcserélő makró.

**⚠️ Exam tip:** „**typedef** létrehoz új típust?” — **nem**, csak álnevet.

---

## 6. Memóriakezelés: **[[stack]]**, **heap**, **`malloc`**, **`free`**

### Definition
A **[[stack]]** általában **automatikus** változóknak és **függvényhívások** keretének ad helyet; **[[heap]]** a **dinamikus** foglalás tere (`malloc` / `calloc` / `realloc`).

### How it works
- **Stack**: belépéskor allokál, kilépéskor **felszabadul** (scope vége). Gyors, de **korlátos** méret.  
- **Heap**: **`malloc(n)`** ad `n` bájtot (inicializálatlan); **`free(ptr)`** visszaadja. **Programozó felelőssége**.

### Syntax
```c
#include <stdlib.h>
int *a = (int*)malloc(n * sizeof *a);
if (!a) { /* hiba */ }
/* hasznalat */
free(a);
a = NULL; /* jo gyakorlat */
```

### Step-by-step execution
1. `malloc` **heapen** keres blokkot, visszaad **címet** vagy `NULL`.  
2. A pointer **stacken** vagy máshol élhet; a **tartalom** heapen.  
3. `free` felszabadítja; utána **használat tilos** (dangling).

### Example
Dinamikus tömb, amelynek mérete futásidejű.

### Common mistakes
- **Memory leak**: `malloc` után nincs `free`.  
- **Double free** / **use after free** — UB, biztonsági rés.  
- **`malloc` méret**: `n * sizeof(int)` helyett **`n * sizeof *p`** biztonságosabb típusváltásnál.

### When to use
Futásidejű méret, nagy adat, adatszerkezetek élettartama nem illeszkedik a scope-hoz.

#### Comparison (if relevant)
**Automatikus tömb** vs **malloc tömb**: élettartam és méret rugalmasság.

**⚠️ Exam tip:** „Mi történik a **stack**kel függvény visszatérésekor?” — lokális változók **érvényüket vesztik**; **ne adj vissza** lokális címre mutató pointert!

---

# Záró összefoglalók (szóbeli „felvezetés”)

## Rövid szóbeli összefoglaló (vezérlés + típusok)
A C program alapból **szekvenciálisan** fut. **Elágazások** (`if`, `if-else`, `else if`, `switch`) **döntési pontokat** adnak; **ciklusok** (`while`, `do-while`, `for`) **ismétlést**. A **`break`**, **`continue`**, **`return`** módosítja a normál menetet. **[[függvény]]**ek modulárisak; C-ben a paraméter **érték szerint** megy át, **[[pointer]]**rel érhető el **helyben módosítás**. A **[[rekurzió]]** veret használ; kell **báziseset**. Adatoldalon a **[[adattípus]]** meghatározza **tartományt** és **értelmezést**; a **[[tömb]]** folytonos, a **[[pointer]]** címekkel dolgozik; a **[[struct]]** rekord, a **[[union]]** közös memória. **[[stack]]** és **heap** szétválasztása, **`malloc`/`free`** felelőssége vizsgaközpontú.

## Kulcsfogalmak (megőrizve a hivatkozásokat)
- [[algoritmus]]
- [[strukturált programozás]]
- [[szekvenciális vezérlés]]
- [[if]]
- [[switch]]
- [[while]]
- [[do-while]]
- [[for]]
- [[break]]
- [[continue]]
- [[return]]
- [[függvény]]
- [[prototípus]]
- [[érték szerinti átadás]]
- [[rekurzió]]
- [[adattípus]]
- [[int]]
- [[unsigned]]
- [[float]]
- [[double]]
- [[bool]]
- [[char]]
- [[operátor precedencia]]
- [[típuskonverzió]]
- [[tömb]]
- [[pointer]]
- [[struct]]
- [[union]]
- [[typedef]]
- [[undefined behavior]]

## Tipikus vizsgakérdések (kibővített lista)
1. **Melyek a strukturált vezérlés fő típusai?** — Szekvencia, elágazás, iteráció.  
2. **While vs do-while?** — Elöltesztelő (0+ iteráció) vs hátultesztelő (1+).  
3. **Mikor switch if helyett?** — Sok diszkrét konstans ág, olvashatóság.  
4. **A for három része?** — Inicializálás, feltétel, léptetés.  
5. **Break vs continue?** — Kilépés a ciklusból/switch-ből vs következő iteráció.  
6. **C paraméterátadás?** — Érték szerint; pointerrel cím szerinti *hatás*.  
7. **Rekurzió elemei?** — Bázis + konvergáló rekurzív hívás.  
8. **Signed vs unsigned?** — Negatív ábrázolás vs nagyobb pozitív tartomány; keverés veszélye.  
9. **Miért pontatlan a lebegőpont?** — Véges mantissza.  
10. **Tömb vs pointer?** — Tömb fix méretű objektum (de sok helyen decay); pointer cím változó.  
11. **Struct vs union?** — Külön mezőméretek vs közös tárterület.  
12. **Stack vs heap?** — Automatikus scope vs explicit dinamikus élettartam.  
13. **Mi az UB és egy példa?** — Nem specifikált viselkedés; pl. túlindexelés, null derefer, signed overflow.

## Minimum, amit „biztosan” tudni kell
- Vezérlési szerkezetek **működése** és **tipikus hibák** (`=`, túlindexelés, `break` hiány).  
- **`for`/`while` átírás** és **iterációszám** számolás.  
- **[[függvény]]** hívás **memória** szemlélete (frame).  
- **[[pointer]]**: `&`, `*`, paraméter **`scanf`**.  
- **[[tömb]]–pointer** kapcsolat: `a[i]` ≡ `*(a+i)`.  
- **[[struct]]** `.` vs **`->`**.  
- **Dinamikus memória**: pár **`malloc`–`free`**, **ne** használd a felszabadított pointert.  
- **[[undefined behavior]]** és **vizsgán** miért kerüljük.

---

*A vázlat eredeti fájljai: `progalap1.md`, `progalap2.md`.*
