# Programozás I–II – 21. tétel
## Fordítás, futtatás, absztrakció, generikusok, virtuális függvények

---

## 1. Programok fordítása és futtatása

### 1.1 Fordítás folyamata (C++)
**Rövid definíció:**  
C++-ban a forráskódból több lépésben készül natív futtatható program.

**Működési elv:**  
- Folyamat: forráskód -> előfeldolgozás -> fordítás -> objektumkód -> linkelés -> bináris.  
- **Preprocessing**: makrók és include-ok feloldása.  
- **Fordítás**: gépközeli objektumkód generálása.  
- **Linkelés**: külön modulok és könyvtárak összekapcsolása.

**Egyszerű példa:**  
Két `.cpp` fájlt külön fordítunk, majd a linker egyetlen futtatható fájllá fűzi.

**Vizsgán fontos kulcsszavak:**  
**fordítási lánc**, **preprocessing**, **objektumkód**, **linkelés**, **natív bináris**

---

### 1.2 Fordítás Java-ban
**Rövid definíció:**  
Java-ban a forráskód először bytecode-dá fordul, amit a JVM futtat.

**Működési elv:**  
- `.java` -> `javac` -> `.class` bytecode.  
- A **[[JVM]]** platformfüggő implementáció, ami platformfüggetlen bytecode-ot futtat.  
- Gyakori JIT optimalizáció futás közben.

**Egyszerű példa:**  
Ugyanaz a `.class` fájl futtatható Windowson és Linuxon is, ha van JVM.

**Vizsgán fontos kulcsszavak:**  
**[[JVM]]**, **bytecode**, **javac**, **platformfüggetlenség**, **JIT**

---

### 1.3 C++ vs Java
**Rövid definíció:**  
A fő különbség: C++ közvetlenül natív kódot ad, Java virtuális gépen futó bytecode-ot.

**Működési elv:**  
- **C++**: platform-specifikus bináris, közvetlen hardverközeli teljesítmény.  
- **Java**: „write once, run anywhere” szemlélet JVM-en keresztül.  
- Kompromisszum: kontroll és nyers sebesség vs hordozhatóság.

**Egyszerű példa:**  
C++ programot gyakran újra kell fordítani más platformra, Java programot elég JVM-en futtatni.

**Vizsgán fontos kulcsszavak:**  
**C++ natív**, **Java bytecode**, **platformfüggő vs platformfüggetlen**, **virtuális gép**

---

## 2. Parancssori használat

### 2.1 C++
**Rövid definíció:**  
C++ fejlesztésnél gyakori a parancssori fordítás és futtatás.

**Működési elv:**  
- Fordítás: `g++ file.cpp -o program`  
- Futtatás: `./program` (Windowson tipikusan `program.exe`)  
- Több fájl is fordítható egy parancsban vagy build rendszerrel.

**Egyszerű példa:**  
`g++ main.cpp utils.cpp -o app` majd futtatás `./app`.

**Vizsgán fontos kulcsszavak:**  
**g++**, **parancssori fordítás**, **futtatható állomány**, **build**

---

### 2.2 Java
**Rövid definíció:**  
Java-ban külön fordítási és futtatási parancsot használunk.

**Működési elv:**  
- Fordítás: `javac File.java`  
- Futtatás: `java File` (osztálynév, `.class` kiterjesztés nélkül)  
- A `main` metódus belépési pont.

**Egyszerű példa:**  
`javac Main.java` után `java Main` indítja a programot.

**Vizsgán fontos kulcsszavak:**  
**javac**, **java parancs**, **main metódus**, **bytecode futtatás**

---

### 2.3 Parancssori paraméterek
**Rövid definíció:**  
A parancssori paraméterek külső bemenetet adnak a programnak induláskor.

**Működési elv:**  
- C++: `int main(int argc, char* argv[])`  
- Java: `public static void main(String[] args)`  
- Az argumentumok sztringként érkeznek, parse-olni kell őket.

**Egyszerű példa:**  
`program input.txt` esetén az első argumentum a fájlnév.

**Vizsgán fontos kulcsszavak:**  
**argc/argv**, **String[] args**, **parancssori argumentum**, **bemenet**

---

## 3. Fordítási opciók és projektek

### 3.1 Fordítási opciók
**Rövid definíció:**  
A fordítási opciók befolyásolják a teljesítményt, hibakereshetőséget és kódminőséget.

**Működési elv:**  
- Optimalizálás: `-O2`, `-O3` (gyorsabb kód).  
- Figyelmeztetések: `-Wall` (rejtett hibák kiszűrése).  
- Debug információ: `-g` (debugger támogatás).

**Egyszerű példa:**  
Fejlesztéskor `-g -Wall`, release buildnél inkább `-O2` tipikus.

**Vizsgán fontos kulcsszavak:**  
**-O2/-O3**, **-Wall**, **-g**, **debug vs release build**

---

### 3.2 Nagyobb projektek fordítása
**Rövid definíció:**  
Nagy projektnél a fordítás automatizált build rendszerrel történik.

**Működési elv:**  
- Több forrásfájl és könyvtár kezelése szükséges.  
- Build eszközök: `make`, `cmake`, Java oldalon pl. Maven/Gradle.  
- Függőségkezelés és inkrementális újrafordítás időt spórol.

**Egyszerű példa:**  
Csak a módosított fájl fordul újra, nem az egész projekt.

**Vizsgán fontos kulcsszavak:**  
**build rendszer**, **makefile**, **cmake**, **függőségkezelés**, **inkrementális build**

---

## 4. Absztrakt osztályok

### 4.1 Fogalom
**Rövid definíció:**  
Az **[[absztrakt osztály]]** olyan osztály, amely nem példányosítható közvetlenül.

**Működési elv:**  
- Tartalmazhat absztrakt (megvalósítás nélküli) metódust.  
- A leszármazott osztályok kötelesek megadni a konkrét implementációt.  
- Tartalmazhat közös, kész metódusokat is.

**Egyszerű példa:**  
`Shape` absztrakt osztályban `draw()` absztrakt, `Circle` és `Rectangle` valósítja meg.

**Vizsgán fontos kulcsszavak:**  
**[[absztrakt osztály]]**, **nem példányosítható**, **absztrakt metódus**, **ősosztály**

---

### 4.2 Szerep
**Rövid definíció:**  
Az absztrakt osztály egységes alapot ad rokonságban lévő típusoknak.

**Működési elv:**  
- Közös állapotot és részben közös működést ad.  
- A konkrét különbségeket a leszármazottak valósítják meg.  
- Segíti a polimorf használatot.

**Egyszerű példa:**  
Minden alakzatra van `terulet()`, de számítás típustól függően eltér.

**Vizsgán fontos kulcsszavak:**  
**közös ős**, **egységes API**, **leszármazotti implementáció**, **polimorf használat**

---

## 5. Interfészek

### 5.1 Java
**Rövid definíció:**  
A Java **[[interfész]]** szerződést ad: milyen metódusokat kell biztosítani.

**Működési elv:**  
- Osztály több interfészt is implementálhat.  
- Többszörös viselkedés modellezhető osztályszintű többszörös öröklődés nélkül.  
- Gyakori architektúraeszköz laza csatoláshoz.

**Egyszerű példa:**  
`Printable` interfészt több, egymástól független osztály is megvalósíthat.

**Vizsgán fontos kulcsszavak:**  
**[[interfész]]**, **szerződés**, **implementálás**, **többszörös viselkedés**

---

### 5.2 C++ megfelelője
**Rövid definíció:**  
C++-ban az interfész szerepét gyakran tisztán virtuális osztály tölti be.

**Működési elv:**  
- Pure virtual metódusok (`= 0`) definiálják a kötelező API-t.  
- Az ilyen osztály absztrakt, közvetlenül nem példányosítható.

**Egyszerű példa:**  
`class IShape { virtual void draw() = 0; };`

**Vizsgán fontos kulcsszavak:**  
**pure virtual**, **interfész-szerű osztály**, **=0**, **absztrakt API**

---

## 6. Generikus osztályok

### 6.1 Fogalom
**Rövid definíció:**  
A **[[generikus programozás]]** típusparaméterezéssel újrafelhasználható kódot ad.

**Működési elv:**  
- Ugyanaz a logika több adattípussal használható.  
- Csökkenti a duplikációt és növeli a típusbiztonságot.

**Egyszerű példa:**  
`Lista<T>` ugyanúgy kezel `Integer` és `String` elemeket.

**Vizsgán fontos kulcsszavak:**  
**[[generikus programozás]]**, **típusparaméter**, **újrafelhasználás**, **típusbiztonság**

---

### 6.2 Java
**Rövid definíció:**  
Java generics fordítási idejű típusbiztonságot ad gyűjteményeknél és API-knál.

**Működési elv:**  
- Példa: `List<T>`, `Map<K,V>`.  
- Fordító ellenőrzi a helyes típushasználatot.  
- Runtime-ban type erasure modell működik.

**Egyszerű példa:**  
`List<String>`-be nem tehető `Integer`, fordítási hibát ad.

**Vizsgán fontos kulcsszavak:**  
**Java generics**, **List<T>**, **típusbiztonság**, **type erasure**

---

### 6.3 C++
**Rövid definíció:**  
C++-ban a generikus programozás fő eszköze a **[[template]]**.

**Működési elv:**  
- A fordító konkrét típusokra példányosítja a sablont.  
- Erős teljesítmény és rugalmasság érhető el.  
- Bonyolultabb hibaüzenetek előfordulhatnak.

**Egyszerű példa:**  
`template<typename T> T max(T a, T b)` több típusra használható.

**Vizsgán fontos kulcsszavak:**  
**[[template]]**, **példányosítás**, **fordítási idejű generikusság**, **C++ sablon**

---

## 7. Virtuális függvények

### 7.1 Fogalom
**Rövid definíció:**  
A virtuális függvény a futásidejű polimorfizmus alapja.

**Működési elv:**  
- Bázisosztály interfészt ad, leszármazott felüldefiniál.  
- Híváskor a tényleges objektumtípus szerinti implementáció fut.

**Egyszerű példa:**  
`Shape* s` mögött lehet `Circle` vagy `Square`, a `draw()` ennek megfelelően választódik.

**Vizsgán fontos kulcsszavak:**  
**virtuális függvény**, **futásidejű polimorfizmus**, **felüldefiniálás**

---

### 7.2 Megvalósítás
**Rövid definíció:**  
C++ és Java eltérően jelöli/kezeli a virtuális metódusokat.

**Működési elv:**  
- C++-ban explicit `virtual` kell a dinamikus kötéshez.  
- Java-ban az instance metódusok alapvetően virtuálisak (kivételekkel, pl. `final`).

**Egyszerű példa:**  
C++-ban `virtual void f();`, Java-ban `void f(){}` már virtuálisan felülírható.

**Vizsgán fontos kulcsszavak:**  
**C++ virtual**, **Java alapértelmezett virtualitás**, **dinamikus kötés**

---

### 7.3 Virtuális táblázat (vtable)
**Rövid definíció:**  
A **[[vtable]]** C++ belső mechanizmus a virtuális hívások feloldására.

**Működési elv:**  
- Az objektum típusa alapján a megfelelő függvénycím kerül kiválasztásra.  
- Ez teszi lehetővé a dinamikus polimorf viselkedést.

**Egyszerű példa:**  
Ugyanazon bázis pointerrel más objektumtípus más függvénycímre mutat.

**Vizsgán fontos kulcsszavak:**  
**[[vtable]]**, **függvénycím**, **dinamikus dispatch**, **runtime feloldás**

---

## 8. Szerep és használat
**Rövid definíció:**  
Az absztrakciós eszközök célja rugalmas, bővíthető és újrafelhasználható programtervezés.

**Működési elv:**  
- Absztrakt osztályok és interfészek egységes API-t adnak.  
- Generikusok csökkentik a kódduplikációt.  
- Virtuális függvények biztosítják a dinamikus viselkedést.

**Egyszerű példa:**  
Plugin rendszerben közös interfész alapján különböző modulok cserélhetően használhatók.

**Vizsgán fontos kulcsszavak:**  
**API absztrakció**, **bővíthetőség**, **generikusság**, **dinamikus viselkedés**

---

## 9. Összefüggések
**Rövid definíció:**  
A témakörök együtt alkotják az OOP rugalmas tervezési eszköztárát.

**Működési elv:**  
- Absztrakt osztály és öröklődés: közös alap + konkrét leszármazott.  
- Interfész: szerződésalapú tervezés.  
- Generikus: típusfüggetlen újrafelhasználhatóság.  
- Virtuális függvény: futásidejű kötés és polimorf viselkedés.

**Egyszerű példa:**  
Generikus tároló interfészt adunk meg, és több konkrét implementációt virtuális metódussal cserélünk.

**Vizsgán fontos kulcsszavak:**  
**absztrakciós eszköztár**, **szerződésalapú tervezés**, **dinamikus kötés**, **újrafelhasználhatóság**

---

## + Vizsgán érdemes még megemlíteni
- A **[[JVM]]** szerepe a hordozhatóságban és futtatásban.  
- **Template vs generics**: C++ fordítási példányosítás vs Java type erasure jelleg.  
- **virtual vs non-virtual**: dinamikus vs statikus kötés.  
- Build rendszerek (make, cmake) jelentősége nagy projektnél.  
- Gyakorlati példák: plugin-rendszer, rajzolófelület, adatstruktúra-könyvtár.

---

## Rövid szóbeli összefoglaló
A fordítás és futtatás C++ és Java esetén eltérő modell szerint történik. C++-ban a forráskód natív binárissá fordul preprocessing, fordítás és linkelés után, Java-ban pedig bytecode készül, amit a JVM futtat. Parancssorban mindkét nyelvnél külön fordítási és futtatási lépések vannak, és paraméterek átadhatók a main függvénynek. Nagy projektnél fontosak a build rendszerek és a fordítási opciók. OOP tervezésben az absztrakt osztályok és interfészek közös szerződést adnak, a generikusok típusparaméteres újrafelhasználhatóságot biztosítanak, a virtuális függvények pedig futásidejű polimorfizmust valósítanak meg. A lényeg, hogy ezek együtt adnak rugalmas, bővíthető és karbantartható rendszert.

## Kulcsfogalmak
- [[fordítás]]
- [[linkelés]]
- [[JVM]]
- [[bytecode]]
- [[build rendszer]]
- [[absztrakt osztály]]
- [[interfész]]
- [[generikus programozás]]
- [[template]]
- [[virtuális függvény]]
- [[dinamikus kötés]]
- [[vtable]]
- [[overriding]]
- [[típusbiztonság]]
- [[parancssori argumentum]]

## Tipikus vizsgakérdések
1. **Melyek a C++ fordítás fő lépései?**  
   Előfeldolgozás, fordítás objektumkóddá, majd linkelés futtatható binárissá.

2. **Mi a JVM szerepe Java-ban?**  
   A bytecode futtatása és platformfüggetlenség biztosítása.

3. **Mi a fő különbség C++ és Java futtatási modellje között?**  
   C++ natív bináris, Java JVM-en futó bytecode.

4. **Mire jó az absztrakt osztály?**  
   Közös alapot ad, de közvetlenül nem példányosítható.

5. **Mi az interfész lényege?**  
   Szerződés: meghatározza a kötelező metódusokat implementáció nélkül.

6. **Mi a különbség Java generics és C++ template között?**  
   Java főleg type erasure modell, C++ fordításkor konkrét példányosítást végez.

7. **Mitől lesz egy metódushívás dinamikus?**  
   Virtuális kötés esetén futáskor a tényleges objektumtípus alapján dől el.

## Minimum, amit tudni kell
- C++ fordítási lánc röviden: preprocess -> compile -> link.  
- Java modell: `.java` -> `.class` -> JVM futtatás.  
- Parancssori fordítás/futtatás alapparancsai C++ és Java esetén.  
- Absztrakt osztály és interfész közti alap különbség.  
- Generikus osztály célja: típusparaméteres újrafelhasználás.  
- C++ template és Java generics rövid eltérése.  
- Virtuális függvény szerepe futásidejű polimorfizmusnál.  
- Dinamikus kötés és vtable fogalma (C++ említési szinten).
