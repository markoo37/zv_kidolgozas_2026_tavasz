# Programozás I–II – 20. tétel
## Objektumok életciklusa, statikus elemek, overloading, kivételkezelés

---

## 1. Objektumok életciklusa

### 1.1 Lépések
**Rövid definíció:**  
Az objektum életciklusa az objektum megszületésétől a megszűnéséig tartó folyamat.

**Működési elv:**  
- **Létrehozás**: memóriafoglalás és példányosítás.  
- **Inicializálás**: kezdőállapot beállítása (tipikusan konstruktorral).  
- **Használat**: metódushívások, állapotváltozások.  
- **Megszüntetés**: erőforrások felszabadítása.

**Egyszerű példa:**  
`new Auto()` létrehoz egy objektumot, használjuk, majd nyelvtől függően GC vagy destruktor gondoskodik a lezárásról.

**Vizsgán fontos kulcsszavak:**  
**objektuméletciklus**, **creation**, **initialization**, **destruction**, **erőforráskezelés**

---

## 2. Létrehozás és inicializálás

### 2.1 Konstruktor
**Rövid definíció:**  
A **[[konstruktor]]** speciális metódus, ami az objektum kezdeti állapotát állítja be.

**Működési elv:**  
- Objektum létrejöttekor automatikusan lefut.  
- Lehet paraméter nélküli vagy paraméteres.  
- Segít érvényes kezdőállapotot biztosítani.

**Egyszerű példa:**  
`Pont(int x, int y)` konstruktor beállítja a koordinátákat.

**Vizsgán fontos kulcsszavak:**  
**[[konstruktor]]**, **inicializálás**, **paraméteres konstruktor**, **objektumállapot**

---

### 2.2 Inicializálás
**Rövid definíció:**  
Az inicializálás az adattagok kezdeti értékeinek meghatározása.

**Működési elv:**  
- Történhet alapértelmezett értékekkel vagy konstruktorparaméterből.  
- Jó inicializálás csökkenti a futásidejű hibákat.  
- Komplex objektumnál függő mezők sorrendje is fontos.

**Egyszerű példa:**  
`szamlalo = 0` alapérték vagy `Szamla(kezdoEgyenleg)` konstruktorból beállítva.

**Vizsgán fontos kulcsszavak:**  
**inicializálás**, **kezdőérték**, **konstruktorlogika**, **érvényes állapot**

---

## 3. Másolás

### 3.1 C++
**Rövid definíció:**  
C++-ban másoláskor másoló konstruktor és értékadási logika határozza meg, hogyan másolódik objektumállapot.

**Működési elv:**  
- Alapértelmezés szerint tagonkénti másolás történik.  
- Erőforrásos objektumnál külön kell kezelni a másolást.  
- Különbség: **[[sekély másolás]]** vs **[[mély másolás]]**.

**Egyszerű példa:**  
Ha egy objektum nyers mutatót tárol, sekély másolás dupla felszabadításhoz vezethet.

**Vizsgán fontos kulcsszavak:**  
**copy constructor**, **érték szerinti másolás**, **[[sekély másolás]]**, **[[mély másolás]]**

---

### 3.2 Java
**Rövid definíció:**  
Java-ban változók objektumreferenciát tárolnak, így alapból referencia másolás történik.

**Működési elv:**  
- `A b = a;` esetén ugyanarra az objektumra mutat két referencia.  
- Valódi másolathoz külön logika kell (pl. másoló konstruktor, factory, clone-szerű megoldás).  
- A `clone()` létezik, de gyakorlatban körültekintést igényel.

**Egyszerű példa:**  
Egy listát referencia szerint másolva két név ugyanazt az objektumot módosítja.

**Vizsgán fontos kulcsszavak:**  
**referencia másolás**, **objektumreferencia**, **clone()**, **másolási stratégia**

---

## 4. Objektum megszüntetése

### 4.1 C++
**Rövid definíció:**  
C++-ban az objektum élettartam végén **[[destruktor]]** fut, amely erőforrás-felszabadításra szolgál.

**Működési elv:**  
- Stack objektumnál automatikusan hívódik.  
- Heap objektumnál törlés (`delete`) szükséges, ha nyers mutatót használunk.  
- RAII mintával biztonságosabb erőforráskezelés érhető el.

**Egyszerű példa:**  
Fájlkezelő osztály destruktora automatikusan lezárja a fájlt.

**Vizsgán fontos kulcsszavak:**  
**[[destruktor]]**, **delete**, **RAII**, **erőforrás-felszabadítás**

---

### 4.2 Java
**Rövid definíció:**  
Java automatikus memóriakezelést használ **[[garbage collector]]**-ral.

**Működési elv:**  
- A GC felszabadítja az elérhetetlenné vált objektumokat.  
- Programozónak nem kell explicit `delete`.  
- A `finalize()` elavult, nem megbízható erőforráskezelési eszköz.

**Egyszerű példa:**  
Ha egy objektumra már nincs referencia, a GC később felszabadítja.

**Vizsgán fontos kulcsszavak:**  
**[[garbage collector]]**, **automatikus memória**, **elérhetetlenség**, **finalize elavult**

---

## 5. Objektumok típusa memória szerint

### 5.1 Lokális objektumok
**Rövid definíció:**  
Lokális objektumok tipikusan függvényblokkhoz kötött élettartamúak.

**Működési elv:**  
- Stack területen jönnek létre (C++ esetén).  
- Blokkból kilépéskor automatikusan megszűnnek.  
- Gyors létrehozás és felszabadítás.

**Egyszerű példa:**  
Függvényen belül létrehozott `Pont p;` kilépéskor megszűnik.

**Vizsgán fontos kulcsszavak:**  
**lokális objektum**, **stack**, **automatikus élettartam**

---

### 5.2 Dinamikus objektumok
**Rövid definíció:**  
A dinamikus objektumok heapen jönnek létre, élettartamuk rugalmasabb.

**Működési elv:**  
- C++: `new`/`delete` vagy okos mutatók.  
- Java: `new` + GC kezeli a felszabadítást.  
- Nagyobb rugalmasság, de körültekintő erőforráskezelés kell.

**Egyszerű példa:**  
Futás közben változó elemszámú objektumlista tipikusan heapen tárolódik.

**Vizsgán fontos kulcsszavak:**  
**heap**, **dinamikus allokáció**, **new/delete**, **new + GC**

---

### 5.3 Statikus objektumok
**Rövid definíció:**  
A statikus objektumok a program futásának nagy részében vagy egészében léteznek.

**Működési elv:**  
- Egyszer inicializálódnak.  
- Élettartamuk hosszú, jellemzően programvégéig tart.  
- Alkalmasak közös erőforrások vagy singleton jellegű állapot tárolására.

**Egyszerű példa:**  
Globális konfigurációs objektum statikus tárolási idővel.

**Vizsgán fontos kulcsszavak:**  
**statikus objektum**, **hosszú élettartam**, **egyszeri inicializálás**

---

## 6. Statikus adattagok és metódusok

### 6.1 Statikus adattag
**Rövid definíció:**  
A **statikus adattag** nem példányhoz, hanem az osztályhoz tartozik.

**Működési elv:**  
- Egyetlen közös példány létezik belőle osztályonként.  
- Minden objektum ugyanazt az értéket látja.  
- Jó számlálókra, közös konfigurációra.

**Egyszerű példa:**  
`Student.count` mutatja, hány példány jött létre összesen.

**Vizsgán fontos kulcsszavak:**  
**statikus adattag**, **osztályszintű állapot**, **közös adat**

---

### 6.2 Statikus metódus
**Rövid definíció:**  
A **statikus metódus** osztályon keresztül hívható, példány nélkül.

**Működési elv:**  
- Nincs `this` kontextusa.  
- Közvetlenül statikus mezőket ér el.  
- Segédfüggvényként gyakori.

**Egyszerű példa:**  
`Math.max(a,b)` tipikus statikus metódushasználat.

**Vizsgán fontos kulcsszavak:**  
**statikus metódus**, **objektum nélküli hívás**, **this hiánya**, **utility függvény**

---

### 6.3 Szerepük
**Rövid definíció:**  
A statikus elemek közös osztályszintű viselkedést és állapotot biztosítanak.

**Működési elv:**  
- Központi számlálók, gyármetódusok, konstansok kezelése.  
- Túlhasználva rejtett csatolást és tesztelési nehézséget okozhatnak.

**Egyszerű példa:**  
`Logger.log()` statikus metódus globálisan elérhető naplózáshoz.

**Vizsgán fontos kulcsszavak:**  
**közös állapot**, **segédfüggvény**, **globális elérés**, **tervezési kompromisszum**

---

## 7. Overloading (túlterhelés)

### 7.1 Függvény túlterhelés
**Rövid definíció:**  
Az **[[overloading]]** azonos nevű, de eltérő paraméterezésű függvények használata.

**Működési elv:**  
- A fordító paraméterlista alapján választ.  
- Javítja az API olvashatóságát.  
- Statikus polimorfizmus esete.

**Egyszerű példa:**  
`print(int)`, `print(double)`, `print(string)` ugyanazzal a névvel.

**Vizsgán fontos kulcsszavak:**  
**[[overloading]]**, **paraméterlista**, **fordítási idejű feloldás**

---

### 7.2 Operátor túlterhelés (C++)
**Rövid definíció:**  
C++-ban operátorok viselkedése típushoz igazítható operátor-túlterheléssel.

**Működési elv:**  
- Saját osztályokhoz definiálható pl. `+`, `<<`, `==`.  
- Kifejezőbb kódot adhat, de túlhasználva félreérthető.

**Egyszerű példa:**  
`Complex a+b` összeadást természetesen lehet írni operátor-túlterheléssel.

**Vizsgán fontos kulcsszavak:**  
**operátor túlterhelés**, **C++**, **kifejező kód**, **olvashatóság**

---

### 7.3 Java vs C++
**Rövid definíció:**  
Java és C++ eltérően kezeli az operátor-túlterhelést.

**Működési elv:**  
- Java-ban gyakorlatilag nincs általános operátor-overloading (kivételként String `+` összeillesztés).  
- C++ teljes körűen támogatja.

**Egyszerű példa:**  
Java-ban saját `add()` metódus kell komplex számra, C++-ban lehet `operator+`.

**Vizsgán fontos kulcsszavak:**  
**Java vs C++**, **operátor overloading korlátai**, **String + kivétel**

---

## 8. Kivételkezelés (Exception handling)

### 8.1 Fogalom
**Rövid definíció:**  
A **[[kivételkezelés]]** strukturált mechanizmus futásidejű hibák kezelésére.

**Működési elv:**  
- A hibát kivételobjektum jelzi.  
- A vezérlés a megfelelő kezelő blokkhoz kerül.  
- Elválasztja az üzleti logikát a hibakezeléstől.

**Egyszerű példa:**  
Fájlmegnyitás sikertelensége kivételt dob, amit magasabb szinten kezelünk.

**Vizsgán fontos kulcsszavak:**  
**[[kivételkezelés]]**, **futásidejű hiba**, **hiba propagáció**, **robusztusság**

---

### 8.2 Alap elemek
**Rövid definíció:**  
A kivételkezelés alap építőelemei a `try`, `catch`, `throw`, és Java-ban a `finally`.

**Működési elv:**  
- `try`: kockázatos kód.  
- `throw`: kivétel dobása.  
- `catch`: kivétel típusa szerinti kezelés.  
- `finally`: takarítási lépés, ami általában mindig lefut.

**Egyszerű példa:**  
Adatbázis-kapcsolatot `finally` blokkban lezárunk akkor is, ha hiba történt.

**Vizsgán fontos kulcsszavak:**  
**try**, **catch**, **throw**, **finally**, **takarítás**

---

### 8.3 Java
**Rövid definíció:**  
Java kivételeknél különbséget tesz checked és unchecked típusok között.

**Működési elv:**  
- **Checked exception**: fordító kikényszeríti a kezelést vagy továbbdobást.  
- **Unchecked exception**: futásidejű hibák, nem kötelező deklarálni.  
- Tudatos API-tervezésnél fontos a megfelelő kivételtípus.

**Egyszerű példa:**  
`IOException` checked, ezért kezelni kell vagy `throws`-sal jelezni.

**Vizsgán fontos kulcsszavak:**  
**checked exception**, **unchecked exception**, **throws**, **fordítási kényszer**

---

### 8.4 C++
**Rövid definíció:**  
C++ is támogat `try-catch` kivételkezelést, de nincs Java-s checked kivételrendszer.

**Működési elv:**  
- Kivételek típus alapján foghatók.  
- Erőforrás-biztos kódnál kulcs a **[[RAII]]**, mert kivételnél is lefut a destruktor.  
- Modern C++-ban fontos a kivételbiztos tervezés.

**Egyszerű példa:**  
Ha kivétel dobódik, egy lokális fájlkezelő objektum destruktora automatikusan lezárja a fájlt.

**Vizsgán fontos kulcsszavak:**  
**C++ exception**, **try-catch**, **nincs checked**, **[[RAII]]**, **kivételbiztosság**

---

## 9. Összefüggések
**Rövid definíció:**  
Az életciklus, memória, túlterhelés és kivételkezelés együtt adják az objektumorientált program stabil működését.

**Működési elv:**  
- Életciklus dönti el, mikor foglalunk/felszabadítunk erőforrást.  
- Statikus elemek osztályszintű közös állapotot adnak.  
- Overloading a kód kifejező erejét növeli.  
- Kivételkezelés robusztusságot ad hibás helyzetekben.

**Egyszerű példa:**  
Egy erőforrás-igényes osztály konstruktora nyit, destruktora zár, és hibát kivétellel jelez.

**Vizsgán fontos kulcsszavak:**  
**életciklus és memória**, **statikus állapot**, **overloading szerepe**, **robusztus hibakezelés**

---

## + Vizsgán érdemes még megemlíteni
- **[[sekély másolás]] vs [[mély másolás]]** gyakori hibaforrás.  
- **Stack vs heap** élettartam- és teljesítménykülönbségek.  
- **GC** előnye: egyszerűbb kezelés; hátránya: kevésbé kiszámítható időzítés.  
- Java és C++ memóriakezelése eltérő programozói felelősséget ad.  
- Kivételkezelés előnye: tisztább, biztonságosabb hibakezelési útvonal.

---

## Rövid szóbeli összefoglaló
Objektumok életciklusa létrehozással indul, inicializálással folytatódik, használat után pedig megszűnéssel zárul. C++-ban ezt konstruktorok és destruktorok, Java-ban konstruktor és garbage collector támogatja. Másolásnál fontos különbség, hogy C++-ban külön figyelni kell sekély és mély másolásra, Java-ban pedig alapból referencia másolás történik. A memória szempontjából megkülönböztetünk stack, heap és statikus élettartamot. Statikus adattagok és metódusok osztályszintű közös elemek. Az overloading fordítási időben feloldott túlterhelés, C++-ban operátorokra is alkalmazható. A kivételkezelés try-catch mechanizmussal robusztusabbá teszi a programot; Java-ban checked/unchecked kivételek, C++-ban pedig RAII szemlélet különösen fontos.

## Kulcsfogalmak
- [[objektuméletciklus]]
- [[konstruktor]]
- [[destruktor]]
- [[sekély másolás]]
- [[mély másolás]]
- [[stack]]
- [[heap]]
- [[statikus objektum]]
- [[statikus adattag]]
- [[statikus metódus]]
- [[overloading]]
- [[operátor túlterhelés]]
- [[kivételkezelés]]
- [[garbage collector]]
- [[RAII]]

## Tipikus vizsgakérdések
1. **Mik az objektum életciklus fő lépései?**  
   Létrehozás, inicializálás, használat, megszüntetés.

2. **Mi a különbség C++ és Java memóriafelszabadításában?**  
   C++-ban explicit/RAII alapú felszabadítás is van, Java-ban GC kezeli automatikusan.

3. **Mi a sekély és mély másolás közti különbség?**  
   Sekély másolás referenciát másol, mély másolás külön erőforrást és tartalmat másol.

4. **Mit jelent a statikus adattag?**  
   Osztályszintű közös adat, minden példány osztozik rajta.

5. **Mi az overloading lényege?**  
   Azonos név eltérő paraméterlistával, fordítási időben feloldva.

6. **Java-ban mi a checked exception?**  
   Olyan kivétel, amit a fordító kötelezően kezeltet vagy továbbdobat.

7. **Miért fontos a RAII C++-ban?**  
   Mert kivétel esetén is garantálja az erőforrások felszabadítását.

## Minimum, amit tudni kell
- Objektuméletciklus négy fő lépése.  
- Konstruktor szerepe és inicializálás jelentősége.  
- C++ másolásnál shallow/deep különbség lényege.  
- Stack, heap, statikus élettartam közti alapkülönbség.  
- Statikus adattag és statikus metódus fogalma.  
- Overloading fogalma és fordítási idejű feloldása.  
- Kivételkezelés alap elemei: try, catch, throw, finally.  
- Java vs C++ fő különbsége memória- és kivételkezelésben.
