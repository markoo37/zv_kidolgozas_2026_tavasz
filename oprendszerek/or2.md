# Operációs rendszerek – 13. tétel
## Processzusok kommunikációja és szinkronizáció

---

## 1. Processzusok kommunikációja

### 1.1 IPC (Inter-Process Communication)
**Rövid definíció:**  
Az **[[IPC]]** (Inter-Process Communication) processzusok közötti adatcsere és együttműködés mechanizmusa.

**Működési elv:**  
- Szükséges, ha folyamatok közösen oldanak meg feladatot vagy erőforrást osztanak meg.  
- Biztonságos és rendezett adatcserét kell biztosítania.

**Egyszerű példa:**  
Egy folyamat adatot termel, másik feldolgozza és kiírja.

**Vizsgán fontos kulcsszavak:**  
**[[IPC]]**, **adatcsere**, **együttműködő processzusok**

---

### 1.2 Módszerek
**Rövid definíció:**  
Az IPC két alapmodellje a megosztott memória és az üzenetküldés.

**Működési elv:**  
- Megosztott memória: gyors, de szinkronizációt igényel.  
- Üzenetküldés: strukturáltabb, de lehet nagyobb overhead.

**Egyszerű példa:**  
Producer-consumer rendszer pipe-on vagy közös pufferen keresztül.

**Vizsgán fontos kulcsszavak:**  
**megosztott memória**, **send/receive**, **IPC modellek**

---

## 2. Versenyhelyzet (Race condition)

### 2.1 Fogalom
**Rövid definíció:**  
**[[Versenyhelyzet]]** akkor lép fel, ha több szál/processzus ugyanazt az adatot nem koordináltan módosítja.

**Működési elv:**  
- A végeredmény a futási sorrendtől függ, így nem determinisztikus lehet.

**Egyszerű példa:**  
Két szál egyszerre növel egy számlálót lock nélkül -> elvesző növelés.

**Vizsgán fontos kulcsszavak:**  
**[[versenyhelyzet]]**, **nem determinisztikus eredmény**, **adatütközés**

---

### 2.2 Következmény
**Rövid definíció:**  
A versenyhelyzet adatinkonzisztenciát és rejtett hibákat okoz.

**Működési elv:**  
- Nehezen reprodukálható hibák jelenhetnek meg.  
- Rendszerhelyességet veszélyezteti.

**Egyszerű példa:**  
Banki egyenleg frissítés közben hibás végösszeg alakul ki.

**Vizsgán fontos kulcsszavak:**  
**inkonzisztens állapot**, **konkurens hiba**, **helyességi probléma**

---

## 3. Kritikus szekció

### 3.1 Fogalom
**Rövid definíció:**  
A **[[kritikus szekció]]** olyan kódrész, ahol közösen használt erőforráshoz férünk hozzá.

**Működési elv:**  
- Egy időben csak szabályozottan engedhető be végrehajtási szál/processzus.

**Egyszerű példa:**  
Közös puffer írása/olvasása kritikus szekció.

**Vizsgán fontos kulcsszavak:**  
**[[kritikus szekció]]**, **megosztott erőforrás**, **védett kódrész**

---

### 3.2 Követelmények
**Rövid definíció:**  
A helyes kritikus szekció-megoldásnak klasszikus feltételei vannak.

**Működési elv:**  
- **Mutual exclusion**: egyszerre csak egy belépő.  
- **Progress**: ne akadjon meg feleslegesen.  
- **Bounded waiting**: ne éhezzen végtelen ideig egy folyamat.

**Egyszerű példa:**  
Ha egy szál vár, de sorra kerül garantáltan, bounded waiting teljesül.

**Vizsgán fontos kulcsszavak:**  
**mutual exclusion**, **progress**, **bounded waiting**

---

## 4. Kölcsönös kizárás megvalósítása (busy waiting)

### 4.1 Megszakítások tiltása
**Rövid definíció:**  
Megszakítások tiltása egyszerű védelem, de általánosan rossz skálázhatóságú.

**Működési elv:**  
- Rövid kritikus szakaszokban használható kernel-szinten.  
- Felhasználói szinten nem praktikus.

**Egyszerű példa:**  
Uniprocesszoros rendszeren átmenetileg megakadályozható a megszakítás.

**Vizsgán fontos kulcsszavak:**  
**megszakítás tiltás**, **busy waiting**, **nem skálázható**

---

### 4.2 Zároló változók
**Rövid definíció:**  
Egyszerű lock változó önmagában nem biztonságos, ha nem atomi a kezelés.

**Működési elv:**  
- Ellenőrzés és beállítás között versenyhelyzet lehet.

**Egyszerű példa:**  
Két szál egyszerre látja szabadnak a lockot, mindkettő belép.

**Vizsgán fontos kulcsszavak:**  
**lock változó**, **nem atomi művelet**, **versenyhelyzet**

---

### 4.3 Szigorú váltogatás
**Rövid definíció:**  
A szigorú váltogatás korrekt lehet, de gyakorlatban rossz hatékonyságú.

**Működési elv:**  
- Mereven felváltva enged belépést, függetlenül a valós igénytől.

**Egyszerű példa:**  
Egyik folyamat nem akar belépni, mégis a másiknak várnia kell.

**Vizsgán fontos kulcsszavak:**  
**szigorú váltogatás**, **hatékonysági probléma**

---

### 4.4 Peterson algoritmus
**Rövid definíció:**  
A **[[Peterson-algoritmus]]** két folyamatra ad helyes szoftveres kölcsönös kizárást.

**Működési elv:**  
- `flag` és `turn` változókat használ.  
- Biztosítja mutual exclusiont és progress-t (ideális feltételek mellett).

**Egyszerű példa:**  
Két szál versenyét oktatási célra jól szemlélteti.

**Vizsgán fontos kulcsszavak:**  
**[[Peterson-algoritmus]]**, **flag**, **turn**, **kétfolyamatos megoldás**

---

### 4.5 TSL utasítás (Test-and-Set Lock)
**Rövid definíció:**  
A **[[TSL]]** hardveresen atomi lock-művelet.

**Működési elv:**  
- Atomi teszt+beállítás miatt versenyhelyzet elkerülhető lock megszerzéskor.  
- Busy waiting alapú **spinlock** megoldásokhoz használják.

**Egyszerű példa:**  
Rövid kritikus szekcióknál spinlock működhet hatékonyan többmagos CPU-n.

**Vizsgán fontos kulcsszavak:**  
**[[TSL]]**, **atomi utasítás**, **spinlock**, **hardvertámogatás**

---

## 5. Altatás és ébresztés (blocking)

### 5.1 Probléma
**Rövid definíció:**  
Busy waiting CPU-időt pazarol, mert aktívan várakozik.

**Működési elv:**  
- Várakozó szál folyamatosan pöröghet hasznos munka nélkül.

**Egyszerű példa:**  
Lockra váró szál 100%-os CPU-terhelést okozhat.

**Vizsgán fontos kulcsszavak:**  
**busy waiting**, **CPU-pazarlás**, **aktív várakozás**

---

### 5.2 Megoldás
**Rövid definíció:**  
A blocking modellben a váró folyamat elaltatható, és eseményre ébreszthető.

**Működési elv:**  
- Nem foglal aktívan CPU-t várakozás alatt.  
- Esemény vagy jelzés aktiválja újra.

**Egyszerű példa:**  
Üres puffer esetén fogyasztó blokkol, termelő jelzésre ébred.

**Vizsgán fontos kulcsszavak:**  
**blocking**, **altatás/ébresztés**, **eseményalapú várakozás**

---

## 6. Klasszikus szinkronizációs problémák

### 6.1 Termelő–fogyasztó
**Rövid definíció:**  
A **[[termelő-fogyasztó]]** probléma közös puffer szinkronizált használatát modellezi.

**Működési elv:**  
- Termelő csak nem teli pufferbe írhat.  
- Fogyasztó csak nem üres pufferből olvashat.

**Egyszerű példa:**  
Üzenetsor kezelése producer és consumer szálakkal.

**Vizsgán fontos kulcsszavak:**  
**[[termelő-fogyasztó]]**, **közös puffer**, **túlcsordulás/kiürülés**

---

### 6.2 Írók–olvasók
**Rövid definíció:**  
Az **[[írók-olvasók]]** probléma olvasási párhuzamosság és írási kizárás egyensúlyát kezeli.

**Működési elv:**  
- Több olvasó futhat egyszerre.  
- Író csak kizárólagosan léphet be.

**Egyszerű példa:**  
Adatbázis-olvasásnál sok olvasó, ritka író művelet.

**Vizsgán fontos kulcsszavak:**  
**[[írók-olvasók]]**, **olvasói párhuzamosság**, **írói kizárás**

---

### 6.3 Sorompó (barrier)
**Rövid definíció:**  
A **[[barrier]]** pontnál a résztvevők megvárják egymást.

**Működési elv:**  
- Továbblépés csak akkor, ha minden résztvevő elérte a sorompót.

**Egyszerű példa:**  
Párhuzamos ciklus fázisai között szinkronpont.

**Vizsgán fontos kulcsszavak:**  
**[[barrier]]**, **globális szinkronizáció**, **fázisvárakozás**

---

## 7. Szinkronizációs eszközök

### 7.1 Szemafor
**Rövid definíció:**  
A **[[szemafor]]** számláló alapú szinkronizációs primitív.

**Működési elv:**  
- `wait(P)`: csökkent és szükség esetén blokkol.  
- `signal(V)`: növel és felébreszthet várakozót.  
- Bináris vagy számláló változat.

**Egyszerű példa:**  
Szabad pufferhelyek száma számláló szemaforral kezelhető.

**Vizsgán fontos kulcsszavak:**  
**[[szemafor]]**, **wait(P)**, **signal(V)**, **számláló**

---

### 7.2 Mutex
**Rövid definíció:**  
A **[[mutex]]** kizárólagos hozzáférést biztosító lock.

**Működési elv:**  
- Egyszerre egy szál birtokolhatja.  
- Kritikus szekció védelmére használjuk.

**Egyszerű példa:**  
Közös lista módosítása mutex-zárral védve.

**Vizsgán fontos kulcsszavak:**  
**[[mutex]]**, **kölcsönös kizárás**, **lock/unlock**

---

### 7.3 Monitor
**Rövid definíció:**  
A **[[monitor]]** magas szintű szinkronizációs absztrakció.

**Működési elv:**  
- A monitor belső metódusai implicit kizárást adnak.  
- Feltételváltozók segítik a várakozás-jelzés logikát.

**Egyszerű példa:**  
Pufferkezelés monitorral áttekinthetőbb, mint nyers lockokkal.

**Vizsgán fontos kulcsszavak:**  
**[[monitor]]**, **implicit mutual exclusion**, **feltételváltozó**

---

### 7.4 Üzenetküldés
**Rövid definíció:**  
Üzenetküldésnél explicit adatcsere történik `send/receive` primitívekkel.

**Működési elv:**  
- Szinkron (blokkoló) vagy aszinkron (nem blokkoló) lehet.  
- Elosztott rendszerekben alapmechanizmus.

**Egyszerű példa:**  
Mikroszervizek üzenetsoron kommunikálnak.

**Vizsgán fontos kulcsszavak:**  
**üzenetküldés**, **send/receive**, **szinkron vs aszinkron**

---

## 8. Konkurens és kooperatív processzusok

### 8.1 Konkurens
**Rövid definíció:**  
Konkurens folyamatok időben átfedő végrehajtása erőforrás-versenyt okozhat.

**Működési elv:**  
- Szinkronizáció hiányában versenyhelyzetek alakulnak ki.

**Egyszerű példa:**  
Két szál ugyanazt a naplófájlt írja egyszerre.

**Vizsgán fontos kulcsszavak:**  
**konkurencia**, **erőforrásverseny**, **versenyhelyzet**

---

### 8.2 Kooperatív
**Rövid definíció:**  
Kooperatív folyamatok közös cél érdekében kommunikálnak és koordinálnak.

**Működési elv:**  
- IPC és szinkronizáció nélkül nem biztosítható helyes együttműködés.

**Egyszerű példa:**  
Pipeline feldolgozás több folyamatlánccal.

**Vizsgán fontos kulcsszavak:**  
**kooperatív folyamat**, **koordináció**, **IPC szükségesség**

---

## 9. Összefüggések
**Rövid definíció:**  
Az IPC és szinkronizáció együtt biztosítja a konkurens programok helyes működését.

**Működési elv:**  
- Kritikus szekciók védelme nélkül adatkorrupt állapot jöhet létre.  
- IPC adatcserét, szinkronizáció sorrendhelyességet biztosít.

**Egyszerű példa:**  
Producer-consumer csak puffer + szemafor kombinációval működik helyesen.

**Vizsgán fontos kulcsszavak:**  
**kritikus szekció védelem**, **szinkronizáció**, **IPC összhang**

---

## + Vizsgán érdemes még megemlíteni
- **[[deadlock]]** fogalma és veszélye említési szinten.  
- **starvation** és fairness kérdése.  
- Busy waiting vs blocking teljesítménykülönbség.  
- Szemafor és mutex eltérő szerepe.  
- Gyakorlati minta: producer-consumer, olvasó-író.

---

## Rövid szóbeli összefoglaló
Processzusok együttműködéséhez IPC kell, ami lehet megosztott memória vagy üzenetküldés. Konkurens végrehajtásnál versenyhelyzet alakulhat ki, ha több szál/processzus ugyanazt az adatot nem védetten módosítja. Ezért kritikus szekciókat kell védeni kölcsönös kizárással, és teljesíteni kell a helyességi követelményeket. Busy waiting alapú megoldások egyszerűek, de CPU-pazarlók, ezért gyakori a blocking alapú altatás-ébresztés. Klasszikus problémák a termelő-fogyasztó, írók-olvasók és barrier. Fő eszközök a szemafor, mutex, monitor és üzenetküldés. A cél mindig a helyes és hatékony párhuzamos működés.

## Kulcsfogalmak
- [[IPC]]
- [[megosztott memória]]
- [[üzenetküldés]]
- [[versenyhelyzet]]
- [[kritikus szekció]]
- [[mutual exclusion]]
- [[Peterson-algoritmus]]
- [[TSL]]
- [[busy waiting]]
- [[blocking]]
- [[szemafor]]
- [[mutex]]
- [[monitor]]
- [[termelő-fogyasztó]]
- [[deadlock]]

## Tipikus vizsgakérdések
1. **Miért van szükség IPC-re?**  
   Mert processzusoknak adatot kell cserélniük és együttműködniük.

2. **Mi a race condition lényege?**  
   A végeredmény a konkurens végrehajtási sorrendtől függ.

3. **Mi a kritikus szekció három fő követelménye?**  
   Mutual exclusion, progress, bounded waiting.

4. **Miért problémás a busy waiting?**  
   Mert CPU-időt pazarol aktív várakozással.

5. **Mit tud a Peterson-algoritmus?**  
   Két folyamatra helyes kölcsönös kizárást ad szoftveresen.

6. **Mi a különbség szemafor és mutex között?**  
   Mutex tipikusan kizárásra, szemafor általánosabb számlálásra/szinkronizációra való.

7. **Mikor használunk monitor absztrakciót?**  
   Ha magasabb szintű, biztonságosabb szinkronizációs szerkezetet akarunk.

## Minimum, amit tudni kell
- IPC fogalma és két fő módszere.  
- Race condition és következménye.  
- Kritikus szekció és helyességi követelmények.  
- Busy waiting és blocking különbsége.  
- Peterson és TSL említési szintű lényege.  
- Termelő-fogyasztó probléma alapötlete.  
- Szemafor, mutex, monitor szerepe.  
- Deadlock/starvation fogalmak említése.
