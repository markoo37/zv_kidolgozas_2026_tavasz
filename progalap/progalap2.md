# Programozás alapjai – 18. tétel
## Adattípusok C nyelven

---

## 1. Alapfogalmak
**Rövid definíció:**  
Az **[[adattípus]]** meghatározza, milyen értékek tárolhatók és milyen műveletek végezhetők rajtuk.

**Működési elv:**  
- A típus befolyásolja a memóriaigényt és az értelmezést.  
- Segít a hibák megelőzésében és az egyértelmű programlogikában.

**Egyszerű példa:**  
`int` egész számra jó, `double` lebegőpontos számra.

**Vizsgán fontos kulcsszavak:**  
**[[adattípus]]**, **értékkészlet**, **műveletek**, **memóriafoglalás**

---

## 2. Egyszerű adattípusok

### 2.1 Egész típusok
**Rövid definíció:**  
Az egész típusok diszkrét, egész értékek tárolására szolgálnak.

**Működési elv:**  
- Fő típusok: `char`, `short`, `int`, `long`.  
- Lehetnek `signed` vagy `unsigned`.  
- Ábrázolás jellemzően kettes komplemens; méret platformfüggő lehet.

**Egyszerű példa:**  
`unsigned int` negatív számot nem tárol, de nagyobb pozitív tartományt ad.

**Vizsgán fontos kulcsszavak:**  
**int típuscsalád**, **signed/unsigned**, **kettes komplemens**, **értéktartomány**

---

### 2.2 Valós típusok
**Rövid definíció:**  
A valós típusok (`float`, `double`) lebegőpontos számokat tárolnak.

**Működési elv:**  
- IEEE 754 jellegű ábrázolás (előjel, mantissza, kitevő).  
- Véges pontosság miatt kerekítési hiba előfordul.

**Egyszerű példa:**  
`0.1 + 0.2` eredménye nem feltétlen pontosan `0.3`.

**Vizsgán fontos kulcsszavak:**  
**float**, **double**, **IEEE 754**, **mantissza/kitevő**, **pontatlanság**

---

### 2.3 Logikai típus
**Rövid definíció:**  
C99-től a `bool` logikai érték kezelésére használható.

**Működési elv:**  
- `0` hamis, nem nulla igaz.  
- Logikai operátorokkal (`&&`, `||`, `!`) kombinálható.

**Egyszerű példa:**  
`bool jo = (x > 10);`

**Vizsgán fontos kulcsszavak:**  
**bool**, **igaz/hamis**, **logikai operátorok**

---

### 2.4 Karakter típus
**Rövid definíció:**  
A `char` típus karakterek tárolására szolgál, de valójában kis egész szám.

**Működési elv:**  
- Karakterkód (pl. ASCII) numerikus értékként tárolódik.  
- A C-string null-terminált karaktertömb.

**Egyszerű példa:**  
`'A'` karakterhez számkód tartozik, string: `"alma"`.

**Vizsgán fontos kulcsszavak:**  
**char**, **ASCII**, **karakterkód**, **null-terminált string**

---

## 3. Kifejezések és operátorok
**Rövid definíció:**  
A kifejezések operátorok és operandusok kombinációi, amelyek értéket adnak.

**Működési elv:**  
- Operátortípusok: aritmetikai, relációs, logikai, értékadó.  
- Precedencia és asszociativitás meghatározza a kiértékelés sorrendjét.  
- Típuskonverzió lehet implicit vagy explicit (cast).

**Egyszerű példa:**  
`(double)a / b` explicit casttal valós osztást kényszerít.

**Vizsgán fontos kulcsszavak:**  
**operátorok**, **precedencia**, **asszociativitás**, **implicit/explicit konverzió**, **cast**

---

## 4. Összetett adattípusok

### 4.1 Tömb (array)
**Rövid definíció:**  
A **[[tömb]]** azonos típusú elemek fix méretű, folytonos memóriájú tárolója.

**Működési elv:**  
- Indexeléssel érhető el (`a[i]`).  
- Gyors, közvetlen hozzáférést ad.

**Egyszerű példa:**  
`int a[10];` tíz egész szám tárolására.

**Vizsgán fontos kulcsszavak:**  
**[[tömb]]**, **indexelés**, **fix méret**, **folytonos memória**

---

### 4.2 Pointer
**Rövid definíció:**  
A **[[pointer]]** memória címet tároló változó.

**Működési elv:**  
- `&` címkérés, `*` dereferálás.  
- Pointeraritmetika a mutatott típus méretével lépked.  
- Tömb és pointer C-ben szorosan kapcsolódik.

**Egyszerű példa:**  
`int x=5; int *p=&x;` majd `*p` értéke `5`.

**Vizsgán fontos kulcsszavak:**  
**[[pointer]]**, **cím**, **dereferálás**, **pointeraritmetika**, **tömb-pointer kapcsolat**

---

### 4.3 Rekord (struct)
**Rövid definíció:**  
A **[[struct]]** különböző típusú mezőket fog össze egy logikai egységgé.

**Működési elv:**  
- Összetett adatrekordok modellezésére használjuk.  
- Hozzáférés: `.` operátorral, pointer esetén `->`.

**Egyszerű példa:**  
`struct Hallgato { int id; char nev[50]; };`

**Vizsgán fontos kulcsszavak:**  
**[[struct]]**, **mezők**, **adatmodellezés**, **`.`**, **`->`**

---

### 4.4 Unió (union)
**Rövid definíció:**  
A **[[union]]** mezői közös memóriaterületet használnak.

**Működési elv:**  
- Egyszerre jellemzően egy mező tekinthető érvényesnek.  
- Memóriatakarékos lehet, de óvatos kezelést igényel.

**Egyszerű példa:**  
Kommunikációs protokoll adategység többféle értelmezése ugyanazon bájtokra.

**Vizsgán fontos kulcsszavak:**  
**[[union]]**, **közös memória**, **egyszerre egy aktív mező**, **struct vs union**

---

## 5. Típusképzés és típusdefiníció
**Rövid definíció:**  
A `typedef` olvashatóbb, új néven hivatkozható típusdefiníciót ad.

**Működési elv:**  
- Nem új típuslogikát, hanem alias nevet készít.  
- Segíti az összetett deklarációk egyszerűsítését.

**Egyszerű példa:**  
`typedef struct Hallgato Hallgato;`

**Vizsgán fontos kulcsszavak:**  
**typedef**, **típusalias**, **olvasahatóság**

---

## 6. Memóriakezelés
**Rövid definíció:**  
C-ben a memória kezelése részben automatikus, részben programozói feladat.

**Működési elv:**  
- **Stack**: automatikus lokális változók.  
- **Heap**: dinamikus foglalás (`malloc`) és felszabadítás (`free`).  
- Hibás kezelés memóriahibákhoz vezethet.

**Egyszerű példa:**  
Dinamikus tömb: `int *a = malloc(n * sizeof(int)); ... free(a);`

**Vizsgán fontos kulcsszavak:**  
**stack**, **heap**, **dinamikus memória**, **malloc**, **free**

---

## + Vizsgán érdemes még megemlíteni
- **[[overflow]]** veszélye egész típusoknál.  
- Lebegőpontos pontatlanság gyakori összehasonlítási hiba forrása.  
- Pointerhibák: null pointer, dangling pointer.  
- **[[undefined behavior]]** C-ben kritikus fogalom.  
- Struct és tömb eltérő célú: rekord vs homogén elemsor.

---

## Rövid szóbeli összefoglaló
C nyelvben az adattípus meghatározza az értékkészletet, a memóriaigényt és a végezhető műveleteket. Az egyszerű típusok közé tartoznak az egész, valós, logikai és karakter típusok, amelyeknél fontos a tartomány és pontosság. Kifejezésekben az operátorok precedenciája, asszociativitása és a típuskonverziók meghatározzák az eredményt. Az összetett típusok közül a tömb homogén, fix méretű tároló, a pointer címeket kezel, a struct heterogén adatrekordot ad, a union pedig közös memóriát használ. A typedef javítja az olvashatóságot. Memóriakezelésnél meg kell különböztetni stack és heap területet, dinamikus foglalásnál pedig a malloc/free helyes használata kulcsfontosságú.

## Kulcsfogalmak
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

## Tipikus vizsgakérdések
1. **Mi az adattípus szerepe C-ben?**  
   Meghatározza az értéktartományt, a memóriafoglalást és a műveleteket.

2. **Mi a különbség signed és unsigned típus között?**  
   Signed tartalmaz negatív értékeket is, unsigned csak nemnegatívakat.

3. **Miért pontatlan a lebegőpontos számolás?**  
   Mert véges bitszámon közelítő ábrázolás történik.

4. **Mi a különbség tömb és pointer között?**  
   Tömb fix, folytonos elemhalmaz; pointer memória címet tárol.

5. **Miben különbözik struct és union?**  
   Struct minden mezőnek külön helyet ad, union mezői közös memóriát használnak.

6. **Mire jó a typedef?**  
   Típusalias készítésére, olvashatóbb deklarációkhoz.

7. **Mi a stack és heap közti fő különbség?**  
   Stack automatikus élettartamú, heap dinamikus és explicit kezelést igényel.

## Minimum, amit tudni kell
- Adattípus fogalma és szerepe C-ben.  
- Egész és lebegőpontos típusok alap különbsége.  
- bool és char rövid jelentése.  
- Operátorok fő csoportjai és precedencia fontossága.  
- Tömb és pointer alapkapcsolata.  
- Struct és union eltérő memóriahasználata.  
- typedef célja.  
- Stack/heap és malloc/free alapok, pointerhibák veszélye.
