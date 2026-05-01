
# Programozás I–II – 19. tétel
## Objektumorientált paradigma (Java, C++)

---

## 1. Objektumorientált paradigma (OOP)

### 1.1 Alapfogalom
**Rövid definíció:**  
Az **[[objektumorientált programozás]]** (OOP) olyan paradigma, ahol a program együttműködő objektumokból épül fel.

**Működési elv:**  
- Az adat és a hozzá tartozó művelet egy egységben jelenik meg.  
- Az objektumok metódushívásokkal kommunikálnak.  
- Jól modellez valós vagy logikai rendszereket.

**Egyszerű példa:**  
Egy `BankSzamla` objektum saját egyenleget tárol, és `befizet()` / `kivesz()` metódusokkal kezelhető.

**Vizsgán fontos kulcsszavak:**  
**[[objektumorientált programozás]]**, **objektumok együttműködése**, **adat + művelet**, **modellalkotás**

---

## 2. Absztrakt adattípus (ADT)

### 2.1 Fogalom
**Rövid definíció:**  
Az **[[absztrakt adattípus]]** (ADT) azt írja le, milyen műveletek érhetők el egy adaton, nem pedig a belső megvalósítást.

**Működési elv:**  
- Interfész-szintű gondolkodás: mit tud az objektum.  
- Implementáció elrejtése növeli a cserélhetőséget.  
- OOP-ben osztályokkal és interfészekkel jól megvalósítható.

**Egyszerű példa:**  
`Stack` ADT esetén kívülről `push/pop/top` látszik, de lehet tömbös vagy listás implementáció.

**Vizsgán fontos kulcsszavak:**  
**[[absztrakt adattípus]]**, **interfész**, **implementáció elrejtése**, **modularitás**

---

## 3. Osztály és objektum

### 3.1 Osztály
**Rövid definíció:**  
Az **[[osztály]]** egy sablon, amely leírja az objektum adatait és viselkedését.

**Működési elv:**  
- Tartalmaz mezőket (állapot) és metódusokat (műveletek).  
- Példányosításkor jönnek létre konkrét objektumok.  
- Az osztály a típus szerepét is betölti.

**Egyszerű példa:**  
`Auto` osztály mezői: `szin`, `sebesseg`; metódusai: `gyorsit()`, `fekez()`.

**Vizsgán fontos kulcsszavak:**  
**[[osztály]]**, **mező**, **metódus**, **sablon**

---

### 3.2 Objektum
**Rövid definíció:**  
Az **[[objektum]]** egy osztály konkrét példánya.

**Működési elv:**  
- Saját állapota van (mezők aktuális értékei).  
- A viselkedését metódusok adják.  
- Több objektum ugyanabból az osztályból eltérő állapotú lehet.

**Egyszerű példa:**  
Két `Auto` objektum ugyanabból az osztályból jön létre, de az egyik piros, a másik kék.

**Vizsgán fontos kulcsszavak:**  
**[[objektum]]**, **példány**, **állapot**, **viselkedés**

---

## 4. OOP alapelvek

### 4.1 Egységbe zárás (Encapsulation)
**Rövid definíció:**  
Az **[[encapsulation]]** adatot és a rajta végzett műveleteket egy egységbe zár.

**Működési elv:**  
- Az osztály határozza meg, mi látható kívülről.  
- Hozzáférési szintek (pl. `private`, `public`) védik az adatot.  
- Segít megakadályozni az inkonzisztens állapotot.

**Egyszerű példa:**  
Az egyenleg mező `private`, módosítás csak `befizet()` metóduson keresztül.

**Vizsgán fontos kulcsszavak:**  
**[[encapsulation]]**, **hozzáférés-szabályozás**, **adatvédelem**, **public/private**

---

### 4.2 Információ elrejtés
**Rövid definíció:**  
Az információelrejtés azt jelenti, hogy a belső megvalósítás részleteit elválasztjuk a külső használattól.

**Működési elv:**  
- Kívülről csak a publikus API látszik.  
- Belső szerkezet változtatható a használók törése nélkül.  
- Jobb karbantarthatóságot ad.

**Egyszerű példa:**  
Egy osztály belül listát cserélhet hash mapre, ha az interfésze változatlan, a klienskód marad.

**Vizsgán fontos kulcsszavak:**  
**információelrejtés**, **publikus interfész**, **belső implementáció**, **karbantarthatóság**

---

### 4.3 Öröklődés (Inheritance)
**Rövid definíció:**  
Az **[[öröklődés]]** lehetővé teszi, hogy egy osztály egy másik osztály tulajdonságait és metódusait átvegye.

**Működési elv:**  
- Van ősosztály (base) és származtatott osztály (derived).  
- A leszármazott bővítheti vagy felüldefiniálhatja a viselkedést.  
- Támogatja a kód újrafelhasználását.

**Egyszerű példa:**  
`Jarmu` osztályból `Auto` és `Bicikli` származhat.

**Vizsgán fontos kulcsszavak:**  
**[[öröklődés]]**, **base/derived**, **kód-újrafelhasználás**, **felüldefiniálás**

---

### 4.4 Újrafelhasználás
**Rövid definíció:**  
Az újrafelhasználás célja, hogy meglévő, kipróbált kódot ismét használjunk.

**Működési elv:**  
- Történhet öröklődéssel vagy **[[kompozíció]]val**.  
- Gyakran a kompozíció rugalmasabb és biztonságosabb.  
- Csökkenti a duplikációt.

**Egyszerű példa:**  
`Auto` nem örökli a `Motor` osztályt, hanem tartalmaz egy `Motor` objektumot (kompozíció).

**Vizsgán fontos kulcsszavak:**  
**újrafelhasználás**, **[[kompozíció]]**, **öröklődés**, **kódduplikáció csökkentés**

---

### 4.5 Polimorfizmus
**Rövid definíció:**  
A **[[polimorfizmus]]** azt jelenti, hogy azonos interfész mögött eltérő viselkedés valósulhat meg.

**Működési elv:**  
- A hívó fél az interfészt ismeri, nem a konkrét típust.  
- A konkrét objektum dönti el a végrehajtandó metódust.  
- Növeli a bővíthetőséget.

**Egyszerű példa:**  
`rajzol(Shape s)` hívásnál `Circle` és `Rectangle` másképp rajzolódik.

**Vizsgán fontos kulcsszavak:**  
**[[polimorfizmus]]**, **közös interfész**, **dinamikus viselkedés**, **bővíthetőség**

---

## 5. Polimorfizmus típusai

### 5.1 Fordítási idejű (statikus)
**Rövid definíció:**  
A statikus polimorfizmusnál a megfelelő hívás fordítási időben dől el.

**Működési elv:**  
- **[[overloading]]**: azonos név, eltérő paraméterlista.  
- C++-ban operátor-túlterhelés is ide tartozik.  
- Nem igényel futásidejű típusfeloldást.

**Egyszerű példa:**  
`print(int)` és `print(string)` közül a fordító választ.

**Vizsgán fontos kulcsszavak:**  
**statikus polimorfizmus**, **[[overloading]]**, **fordítási idő**

---

### 5.2 Futási idejű (dinamikus)
**Rövid definíció:**  
A dinamikus polimorfizmusnál a konkrét metódus futás közben dől el.

**Működési elv:**  
- **[[overriding]]**: leszármazott újradefiniálja az ős metódust.  
- Virtuális dispatch választja ki a tényleges implementációt.  
- Erős alap az általánosítható API-knak.

**Egyszerű példa:**  
`Shape* s` mutathat `Circle`-re, `s->draw()` a `Circle::draw()`-t hívja.

**Vizsgán fontos kulcsszavak:**  
**dinamikus polimorfizmus**, **[[overriding]]**, **virtuális függvény**, **runtime dispatch**

---

## 6. Polimorfizmus feloldása

### 6.1 Statikus kötés (early binding)
**Rövid definíció:**  
A **[[statikus kötés]]** esetén a hívott függvény címe fordításkor meghatározódik.

**Működési elv:**  
- Tipikusan overloadingnál történik.  
- Gyorsabb lehet, mert nincs futásidejű feloldás.

**Egyszerű példa:**  
Nem virtuális metódushívás C++-ban rendszerint statikusan kötött.

**Vizsgán fontos kulcsszavak:**  
**[[statikus kötés]]**, **early binding**, **fordításkori feloldás**

---

### 6.2 Dinamikus kötés (late binding)
**Rövid definíció:**  
A **[[dinamikus kötés]]** futásidőben dönti el, melyik metódus fusson.

**Működési elv:**  
- Virtuális metódusoknál alkalmazzuk.  
- C++-ban tipikusan **vtable** mechanizmus segíti.  
- Rugalmasabb, de kis futásidejű többletköltség lehet.

**Egyszerű példa:**  
Bázisosztály referencia mögött más-más leszármazott metódus hívódik.

**Vizsgán fontos kulcsszavak:**  
**[[dinamikus kötés]]**, **late binding**, **vtable**, **virtuális dispatch**

---

## 7. Megvalósítás Java és C++ nyelvekben

### 7.1 Java
**Rövid definíció:**  
A Java erősen objektumorientált, biztonságra és egyszerűbb memóriakezelésre optimalizált.

**Működési elv:**  
- Osztályalapú OOP, interfészekkel többes viselkedés modellezhető.  
- Nincs osztályszintű többszörös öröklődés.  
- Automatikus memóriafelszabadítás **[[garbage collector]]**-ral.

**Egyszerű példa:**  
Egy objektumot elengedve (nincs rá referencia), később a GC felszabadítja.

**Vizsgán fontos kulcsszavak:**  
**Java OOP**, **interfész**, **nincs többszörös öröklődés**, **[[garbage collector]]**

---

### 7.2 C++
**Rövid definíció:**  
A C++ rugalmas, nagy kontrollt adó nyelv, de összetettebb felelősséggel.

**Működési elv:**  
- Támogatja a többszörös öröklődést.  
- Manuális és modern erőforráskezelési minták együtt használhatók.  
- Dinamikus polimorfizmushoz `virtual` kulcsszó szükséges.

**Egyszerű példa:**  
Objektumot `new`-val hozunk létre, és megfelelően felszabadítjuk vagy okos mutatóval kezeljük.

**Vizsgán fontos kulcsszavak:**  
**C++ OOP**, **többszörös öröklődés**, **virtual**, **manuális erőforráskezelés**

---

## 8. Összehasonlítás
**Rövid definíció:**  
Java és C++ eltérő kompromisszumot ad: biztonság/egyszerűség vs kontroll/rugalmasság.

**Működési elv:**  
- **Java**: egyszerűbb memóriahasználat, szabályozottabb modell.  
- **C++**: közelebb van a hardverhez, finomabb teljesítménykontroll.  
- A választás feladattól és környezettől függ.

**Egyszerű példa:**  
Nagyvállalati backendhez Java gyakori, valós idejű motorhoz C++ lehet jobb.

**Vizsgán fontos kulcsszavak:**  
**Java vs C++**, **biztonság vs kontroll**, **komplexitás**, **alkalmazási terület**

---

## + Vizsgán érdemes még megemlíteni
- Az **[[absztrakció]]** segít a lényegkiemelésben és általánosításban.  
- Java interfészekkel többféle viselkedés kombinálható.  
- **[[kompozíció]] vs [[öröklődés]]**: gyakran „kompozíció előnyben”.  
- Tipikus példa: `Shape -> Circle` polimorf feldolgozás.  
- OOP előnyök: modularitás, bővíthetőség, karbantarthatóság.

---

## Rövid szóbeli összefoglaló
Az objektumorientált paradigma lényege, hogy az adatot és a rajta végzett műveleteket objektumokba szervezzük. Az osztály egy sablon, az objektum ennek konkrét példánya saját állapottal és viselkedéssel. Az OOP fő elvei az egységbe zárás, információelrejtés, öröklődés, absztrakció és polimorfizmus. Polimorfizmus lehet statikus, például overloading, illetve dinamikus, amikor futás közben dől el a hívott metódus. Java és C++ mindkettő OOP nyelv, de Java egyszerűbb és biztonságosabb memóriakezelést ad, míg C++ nagyobb rugalmasságot és alacsonyabb szintű kontrollt biztosít. Vizsgán fontos hangsúlyozni, hogy jó tervezésnél az interfész stabil, a megvalósítás cserélhető.

## Kulcsfogalmak
- [[objektumorientált programozás]]
- [[absztrakt adattípus]]
- [[osztály]]
- [[objektum]]
- [[encapsulation]]
- [[információelrejtés]]
- [[öröklődés]]
- [[kompozíció]]
- [[polimorfizmus]]
- [[overloading]]
- [[overriding]]
- [[statikus kötés]]
- [[dinamikus kötés]]
- [[garbage collector]]
- [[vtable]]

## Tipikus vizsgakérdések
1. **Mi a különbség osztály és objektum között?**  
   Az osztály sablon, az objektum ennek konkrét példánya.

2. **Mi az encapsulation lényege?**  
   Az adat és művelet egysége, hozzáférések szabályozásával.

3. **Miben különbözik overloading és overriding?**  
   Overloading: azonos név eltérő paraméterrel (fordításkor), overriding: ős metódus felülírása (futáskor).

4. **Mit jelent a dinamikus kötés?**  
   Futásidőben dől el, melyik metódusimplementáció hívódik.

5. **Miért hasznos a polimorfizmus?**  
   Egységes interfésszel különböző típusok kezelhetők.

6. **Mi a fő különbség Java és C++ OOP között?**  
   Java egyszerűbb memóriakezelésű és kötöttebb, C++ rugalmasabb és komplexebb.

7. **Kompozíció vagy öröklődés: mikor melyik?**  
   Sok esetben kompozíció előnyösebb a lazább csatolás miatt.

## Minimum, amit tudni kell
- OOP alapfogalma: objektumok együttműködése.  
- ADT szerepe: interfész és implementáció szétválasztása.  
- Osztály és objektum közti különbség.  
- Encapsulation, öröklődés, polimorfizmus, absztrakció rövid lényege.  
- Statikus és dinamikus polimorfizmus különbsége.  
- Statikus és dinamikus kötés alapja.  
- Java és C++ fő OOP eltérései.  
- Miért fontos a jó interfésztervezés és az információelrejtés.
