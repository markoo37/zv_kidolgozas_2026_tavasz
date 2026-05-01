# Operációs rendszerek – 12. tétel
## Processzusok, szálak, ütemezés, kontextusváltás

---

## 1. Processzus fogalma

### 1.1 Definíció
**Rövid definíció:**  
A **[[processzus]]** végrehajtás alatt álló program példány, saját erőforrásokkal és címtérrel.

**Működési elv:**  
- Nemcsak kód, hanem futási környezet is: memória, regiszterállapot, nyitott fájlok.  
- Az operációs rendszer kezeli az életciklusát.

**Egyszerű példa:**  
Két megnyitott böngészőablak mögött külön processzusok futhatnak.

**Vizsgán fontos kulcsszavak:**  
**[[processzus]]**, **futó program**, **címtér**, **erőforrás**

---

### 1.2 Processzus vs program
**Rövid definíció:**  
A program passzív kódfájl, a processzus ennek aktív futó példánya.

**Működési elv:**  
- Ugyanaz a program több processzusként is futhat egyszerre.  
- Processzusnak saját állapota van, programnak nincs futásállapota.

**Egyszerű példa:**  
Egy `.exe` programfájlból több külön futó példány indítható.

**Vizsgán fontos kulcsszavak:**  
**program vs processzus**, **passzív vs aktív**, **példányos futás**

---

## 2. Szálak (thread)

### 2.1 Alapfogalom
**Rövid definíció:**  
A **[[szál]]** (thread) egy processzuson belüli végrehajtási egység.

**Működési elv:**  
- Több szál ugyanazon processzuson belül futhat párhuzamosan/konkurensen.  
- Kisebb overhead, mint külön processzusoknál.

**Egyszerű példa:**  
Egy alkalmazásban külön szál kezeli a felületet és külön a háttérszámítást.

**Vizsgán fontos kulcsszavak:**  
**[[szál]]**, **könnyűsúlyú végrehajtás**, **többszálúság**

---

### 2.2 Tulajdonságok
**Rövid definíció:**  
A szálak közös címtéren osztoznak, de saját futási kontextusuk is van.

**Működési elv:**  
- Közös: kód, globális adatok, heap.  
- Egyedi: verem, regiszterkészlet.  
- Emiatt létrehozásuk és váltásuk általában gyorsabb.

**Egyszerű példa:**  
Két szál ugyanazt a listát módosíthatja, ezért szinkronizáció kell.

**Vizsgán fontos kulcsszavak:**  
**közös memória**, **külön verem**, **gyors szálkezelés**

---

### 2.3 Processzus vs szál
**Rövid definíció:**  
Processzusok között erősebb izoláció, szálak között szorosabb erőforrás-megosztás van.

**Működési elv:**  
- Processzusok közti kommunikáció nehezebb (IPC).  
- Szálak közti adatcsere egyszerűbb, de versenyhelyzet veszélyesebb.

**Egyszerű példa:**  
Szálak közös változója lock nélkül inkonzisztens lehet.

**Vizsgán fontos kulcsszavak:**  
**izoláció**, **erőforrás-megosztás**, **IPC vs közös memória**

---

## 3. Processzus életciklus

### 3.1 Állapotok
**Rövid definíció:**  
A processzus életciklusát tipikus állapotmodell írja le.

**Működési elv:**  
- `new`: létrehozás alatt.  
- `ready`: futásra kész, CPU-ra vár.  
- `running`: CPU-n fut.  
- `waiting`: eseményre/I-O-ra vár.  
- `terminated`: befejezett.

**Egyszerű példa:**  
I/O kérés után futó processzus waiting állapotba kerül.

**Vizsgán fontos kulcsszavak:**  
**processzusállapotok**, **ready/running/waiting**, **életciklus**

---

### 3.2 Állapotátmenetek
**Rövid definíció:**  
Állapotváltást az ütemező döntései és külső események okoznak.

**Működési elv:**  
- CPU kiosztás: ready -> running.  
- I/O kérés: running -> waiting.  
- I/O vége: waiting -> ready.

**Egyszerű példa:**  
Időszelet lejárta után running folyamat visszakerülhet ready sorba.

**Vizsgán fontos kulcsszavak:**  
**állapotátmenet**, **scheduler**, **I/O esemény**

---

## 4. Processzus létrehozása és befejezése

### 4.1 Létrehozás
**Rövid definíció:**  
Létrehozáskor az OS új processzus-környezetet állít fel.

**Működési elv:**  
- Rendszerhívás indítja (pl. `fork` szemlélet).  
- Memória és egyéb erőforrások kiosztása.  
- PCB bejegyzés létrehozása.

**Egyszerű példa:**  
Shell új parancs indításakor gyerekfolyamatot hoz létre.

**Vizsgán fontos kulcsszavak:**  
**rendszerhívás**, **erőforrás-foglalás**, **PCB létrehozás**

---

### 4.2 Befejezés
**Rövid definíció:**  
A processzus befejezése lehet normál vagy rendkívüli.

**Működési elv:**  
- Normál kilépés, hiba miatti leállás vagy külső megszakítás.  
- OS felszabadítja az erőforrásokat.

**Egyszerű példa:**  
Szabályos `exit` után lezáródnak a nyitott erőforrások.

**Vizsgán fontos kulcsszavak:**  
**processzus leállás**, **normál/hhiba**, **erőforrás-felszabadítás**

---

## 5. Processzus leírása (PCB)

### 5.1 Process Control Block
**Rövid definíció:**  
A **[[PCB]]** (Process Control Block) az OS által tárolt processzus-metaadat.

**Működési elv:**  
- Tartalmaz PID-t, állapotot, programszámlálót, regisztereket, memóriaadatokat, fájlleírókat.  
- Kontextusváltásnál ebből ment/állít vissza az OS.

**Egyszerű példa:**  
CPU váltáskor az aktuális processzus regiszterei a PCB-be mentődnek.

**Vizsgán fontos kulcsszavak:**  
**[[PCB]]**, **PID**, **programszámláló**, **regisztermentés**

---

## 6. Ütemezés (Scheduling)

### 6.1 Cél
**Rövid definíció:**  
Az **[[ütemezés]]** feladata eldönteni, melyik kész folyamat kapjon CPU-t.

**Működési elv:**  
- Célok: CPU-kihasználás, válaszidő, throughput, méltányosság.  
- A célok rendszerfajtától függően eltérően fontosak.

**Egyszerű példa:**  
Interaktív rendszerben gyors válaszidő fontosabb, mint batch-ben.

**Vizsgán fontos kulcsszavak:**  
**[[ütemezés]]**, **CPU-kihasználás**, **válaszidő**, **throughput**

---

### 6.2 Rendszertípusok

#### Kötegelt (batch)
**Rövid definíció:**  
Batch rendszerben feladatok kötegekben futnak, közvetlen felhasználói interakció nélkül.

**Működési elv:**  
- A teljes áteresztőképesség és erőforrás-hatékonyság a fő cél.

**Egyszerű példa:**  
Éjszakai tömeges riportgenerálás.

**Vizsgán fontos kulcsszavak:**  
**batch rendszer**, **throughput**, **nem interaktív**

#### Interaktív
**Rövid definíció:**  
Interaktív rendszerben a felhasználói reakcióidő kritikus.

**Működési elv:**  
- Rövid időszeletek és gyors context switch kell a jó élményhez.

**Egyszerű példa:**  
Asztali operációs rendszer alkalmazáskezelése.

**Vizsgán fontos kulcsszavak:**  
**interaktív rendszer**, **alacsony válaszidő**, **felhasználói élmény**

#### Valós idejű (real-time)
**Rövid definíció:**  
Valós idejű rendszerben feladatok határidőre történő végrehajtása kötelező.

**Működési elv:**  
- Determinisztikus időzítési viselkedés szükséges.  
- Késés funkcionális hibát okozhat.

**Egyszerű példa:**  
Ipari vezérlő, ahol szenzorolvasásnak fix időn belül meg kell történnie.

**Vizsgán fontos kulcsszavak:**  
**valós idejű rendszer**, **határidő**, **determinisztikus működés**

---

## 7. Ütemezési algoritmusok

### 7.1 FCFS (First Come First Served)
**Rövid definíció:**  
Az **[[FCFS]]** a beérkezési sorrend alapján ütemez.

**Működési elv:**  
- Egyszerű FIFO elv.  
- Hosszú feladatok mögött torlódás alakulhat ki.

**Egyszerű példa:**  
Rövid feladat sokat várhat egy hosszú előtt álló processzus miatt.

**Vizsgán fontos kulcsszavak:**  
**[[FCFS]]**, **FIFO**, **convoy effect**

---

### 7.2 SJF (Shortest Job First)
**Rövid definíció:**  
Az **[[SJF]]** a legrövidebb becsült futásidejű feladatot választja.

**Működési elv:**  
- Átlagos várakozási idő szempontjából kedvező.  
- A futási idő előzetes becslése szükséges.

**Egyszerű példa:**  
Sok rövid feladatot gyorsan kiszolgál, ha jól becsülhető a hosszuk.

**Vizsgán fontos kulcsszavak:**  
**[[SJF]]**, **rövid feladat előny**, **várakozási idő optimalizálás**

---

### 7.3 Round Robin
**Rövid definíció:**  
A **[[Round Robin]]** időosztásos, körkörös CPU-kiosztást alkalmaz.

**Működési elv:**  
- Minden futásra kész folyamat időszeletet kap.  
- Időszelet végén preempció történik.

**Egyszerű példa:**  
Interaktív rendszerekben sok folyamat kap gyors, rövid CPU-időt.

**Vizsgán fontos kulcsszavak:**  
**[[Round Robin]]**, **time slice**, **preempció**

---

### 7.4 Prioritásos ütemezés
**Rövid definíció:**  
Prioritásos ütemezésnél magasabb prioritású folyamatok előnyt élveznek.

**Működési elv:**  
- Rugalmas, de alacsony prioritású folyamat éhezhet.  
- Aging technikával csökkenthető az éhezés.

**Egyszerű példa:**  
Rendszerfolyamatok magasabb prioritást kapnak felhasználói háttérfeladatnál.

**Vizsgán fontos kulcsszavak:**  
**prioritásos ütemezés**, **starvation**, **aging**

---

## 8. Kontextusváltás (Context switch)

### 8.1 Fogalom
**Rövid definíció:**  
A **[[kontextusváltás]]** egyik futó processzus/szál állapotából a másikba történő CPU-váltás.

**Működési elv:**  
- Az OS menti az aktuális kontextust és betölti a következőt.

**Egyszerű példa:**  
Időszelet lejártakor a scheduler új folyamatot indít a CPU-n.

**Vizsgán fontos kulcsszavak:**  
**[[kontextusváltás]]**, **CPU-váltás**, **scheduler**

---

### 8.2 Lépések
**Rövid definíció:**  
A váltás két fő része: mentés és visszaállítás.

**Működési elv:**  
- Futó folyamat regiszterei/PC mentése PCB-be.  
- Következő folyamat adatai betöltése PCB-ből.

**Egyszerű példa:**  
Minden váltásnál futási kontextus snapshot cserélődik.

**Vizsgán fontos kulcsszavak:**  
**állapotmentés**, **állapotbetöltés**, **PCB használat**

---

### 8.3 Költség
**Rövid definíció:**  
A kontextusváltás hasznos, de közvetlen számítási munkát nem végez, ezért overhead.

**Működési elv:**  
- Túl gyakori váltás csökkenti a hatékonyságot.  
- Időszelet mérete kompromisszum: reakcióidő vs overhead.

**Egyszerű példa:**  
Nagyon kicsi quantum mellett sok idő mehet el váltásokra.

**Vizsgán fontos kulcsszavak:**  
**context switch overhead**, **időszelet kompromisszum**, **hatékonyság**

---

## 9. Összefüggések
**Rövid definíció:**  
A processzuskezelés elemei szorosan összekapcsolódnak az OS-ben.

**Működési elv:**  
- Ütemező választása váltást indít.  
- PCB tartja fenn a folyamatállapotot.  
- Szálak javíthatják párhuzamos végrehajtás hatékonyságát.

**Egyszerű példa:**  
Interaktív app sok szállal és RR ütemezéssel gördülékenyebb működést adhat.

**Vizsgán fontos kulcsszavak:**  
**scheduler-kontekstusváltás kapcsolat**, **PCB szerep**, **szálhatékonyság**

---

## + Vizsgán érdemes még megemlíteni
- **Preemptív vs nem preemptív** ütemezés különbsége.  
- **Starvation** és **aging** kapcsolata.  
- Kontextusváltás ára és teljesítményhatása.  
- Példák: desktop OS, szerver, real-time rendszerek.

---

## Rövid szóbeli összefoglaló
A processzus a futó program aktív példánya, saját címtérrel és erőforrásokkal, míg a szál egy processzuson belüli könnyűsúlyú végrehajtási egység. A processzusok életciklusát az OS kezeli állapotok között, és ezt a PCB-ben tárolt adatok támogatják. Ütemezéskor a rendszer célja a CPU jó kihasználása, a válaszidő javítása és az áteresztőképesség növelése. Különböző algoritmusok léteznek, például FCFS, SJF, Round Robin és prioritásos ütemezés, mindegyiknek van előnye és hátránya. Az ütemező döntése kontextusváltást okoz, ami szükséges, de költséges művelet. Gyakorlatban mindig kompromisszum van reakcióidő, méltányosság és overhead között.

## Kulcsfogalmak
- [[processzus]]
- [[szál]]
- [[processzus életciklus]]
- [[PCB]]
- [[ütemezés]]
- [[FCFS]]
- [[SJF]]
- [[Round Robin]]
- [[prioritásos ütemezés]]
- [[preemptív ütemezés]]
- [[starvation]]
- [[aging]]
- [[kontextusváltás]]
- [[CPU-kihasználás]]
- [[válaszidő]]

## Tipikus vizsgakérdések
1. **Mi a különbség program és processzus között?**  
   Program passzív kód, processzus futó aktív példány.

2. **Mi a különbség processzus és szál között?**  
   Processzus izoláltabb, szálak közös memóriát osztanak egy processzuson belül.

3. **Mit tárol a PCB?**  
   Azonosító, állapot, regiszterek, PC, memória- és erőforrásinformációk.

4. **Mi a Round Robin lényege?**  
   Időszelet alapú körkörös ütemezés, jó interaktív rendszerekhez.

5. **Mikor lehet gond a prioritásos ütemezésnél?**  
   Éhezés (starvation) előfordulhat alacsony prioritásnál.

6. **Mi a kontextusváltás fő lépése?**  
   Futó folyamat állapotmentése és következő folyamat állapotbetöltése.

7. **Miért költséges a context switch?**  
   Mert CPU-időt visz el hasznos számítás nélkül.

## Minimum, amit tudni kell
- Processzus és szál definíciója, különbsége.  
- Processzusállapotok és alap átmenetek.  
- PCB szerepe.  
- Ütemezés céljai.  
- FCFS, SJF, Round Robin alapötlete.  
- Prioritásos ütemezés és starvation fogalma.  
- Kontextusváltás jelentése és költsége.  
- Preemptív és nem preemptív szemlélet rövid különbsége.
