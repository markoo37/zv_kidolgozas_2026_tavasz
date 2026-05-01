# Számítógép architektúra – 27. tétel
## Neumann-architektúra, CPU, párhuzamosság, RISC vs CISC

---

## 1. Neumann-elvű gép

### 1.1 Alapfogalom
**Rövid definíció:**  
A **[[Neumann-architektúra]]** alapelve, hogy a program és az adatok közös memóriában vannak tárolva.

**Működési elv:**  
- A CPU ugyanabból a memóriából olvassa az utasításokat és adatokat.  
- Az utasítás-végrehajtás ciklikus (beolvasás, értelmezés, végrehajtás).  
- Egyszerű, általános célú modell, a mai gépek alapja.

**Egyszerű példa:**  
Egy összeadó program utasításai és az összeadandó számok ugyanabban a RAM-ban lehetnek.

**Vizsgán fontos kulcsszavak:**  
**[[Neumann-architektúra]]**, **tárolt program elve**, **közös memória**, **utasításciklus**

---

### 1.2 Fő egységek
**Rövid definíció:**  
A Neumann-gép fő egységei együtt biztosítják az adatfeldolgozást és a külvilággal való kapcsolatot.

**Működési elv:**  
- **[[CPU]]**: végrehajtás és vezérlés.  
- **Memória**: programok és adatok tárolása.  
- **Input**: adatbevitel (pl. billentyűzet, szenzor).  
- **Output**: eredmény megjelenítése/kiadása (pl. monitor, nyomtató).

**Egyszerű példa:**  
Felhasználó beír egy számot billentyűzetről (input), CPU feldolgozza, kijelzi monitoron (output).

**Vizsgán fontos kulcsszavak:**  
**[[CPU]]**, **memória**, **input**, **output**, **rendszerelemek**

---

## 2. CPU felépítése

### 2.1 Részegységek
**Rövid definíció:**  
A CPU több specializált részegységből áll, amelyek együtt hajtják végre az utasításokat.

**Működési elv:**  
- **[[CU]]** (vezérlő egység): vezérlőjeleket ad, koordinálja a működést.  
- **[[ALU]]**: aritmetikai és logikai műveletek végrehajtása.  
- **[[regiszter]]ek**: nagyon gyors, kis méretű belső tárolók.

**Egyszerű példa:**  
Összeadásnál a CU irányít, a számok regiszterből jönnek, a műveletet az ALU végzi.

**Vizsgán fontos kulcsszavak:**  
**[[CU]]**, **[[ALU]]**, **[[regiszter]]**, **vezérlés**, **végrehajtás**

---

### 2.2 Regiszterek
**Rövid definíció:**  
A regiszterek a CPU leggyorsabb tárolói, az aktuális végrehajtáshoz szükséges adatokat tartják.

**Működési elv:**  
- **[[PC]]**: a következő utasítás címét tartalmazza.  
- **[[IR]]**: az éppen végrehajtott utasítás kódja.  
- Általános célú regiszterek: operandusok és köztes eredmények tárolása.

**Egyszerű példa:**  
Egy ciklusban a PC lépteti az utasításokat, az IR-ben mindig az aktuális művelet van.

**Vizsgán fontos kulcsszavak:**  
**[[PC]]**, **[[IR]]**, **általános célú regiszterek**, **gyors tárolás**

---

## 3. Adatút (Datapath)

### 3.1 Fogalom
**Rövid definíció:**  
Az **[[adatút]]** a CPU-n belüli adatmozgás és adatfeldolgozás hardveres útvonala.

**Működési elv:**  
- Összeköti a regisztereket, ALU-t és buszokat.  
- Meghatározza, honnan hova jutnak az operandusok és eredmények.  
- A vezérlőegység vezérlőjelekkel irányítja.

**Egyszerű példa:**  
Két regiszter tartalma az ALU-ba kerül, ott összeadódik, majd eredmény visszaíródik egy regiszterbe.

**Vizsgán fontos kulcsszavak:**  
**[[adatút]]**, **adatáramlás**, **ALU**, **regiszterkapcsolat**, **vezérlőjelek**

---

### 3.2 Buszrendszer
**Rövid definíció:**  
A buszok közös kommunikációs csatornák a CPU, memória és perifériák között.

**Működési elv:**  
- **[[adatbusz]]**: adatokat továbbít.  
- **[[címbusz]]**: megadja a memória/periféria címet.  
- **[[vezérlőbusz]]**: vezérlőjeleket visz (olvasás, írás, megszakítás).

**Egyszerű példa:**  
Memóriaolvasásnál címbuszon kimegy a cím, vezérlőbusz jelzi az olvasást, adatbuszon érkezik vissza az adat.

**Vizsgán fontos kulcsszavak:**  
**[[adatbusz]]**, **[[címbusz]]**, **[[vezérlőbusz]]**, **kommunikáció**

---

## 4. Utasítás-végrehajtás ciklusa

### 4.1 Fetch
**Rövid definíció:**  
A **fetch** lépésben a CPU beolvassa a következő utasítást a memóriából.

**Működési elv:**  
- PC megadja az utasítás címét.  
- Utasítás bekerül az IR-be.  
- PC általában a következő címre lép.

**Egyszerű példa:**  
Ha a PC értéke 100, a CPU a 100-as memóriacímen lévő utasítást tölti be.

**Vizsgán fontos kulcsszavak:**  
**fetch**, **[[PC]]**, **utasításbeolvasás**, **[[IR]]**

---

### 4.2 Decode
**Rövid definíció:**  
A **decode** során a CPU értelmezi, milyen műveletet kell végrehajtani.

**Működési elv:**  
- Az opcode alapján eldől a művelet típusa.  
- A vezérlőegység előkészíti a szükséges vezérlőjeleket.  
- Meghatározódik az operandusok forrása.

**Egyszerű példa:**  
Az `ADD R1, R2` utasításnál dekódoláskor kiderül, hogy két regisztert kell összeadni.

**Vizsgán fontos kulcsszavak:**  
**decode**, **opcode**, **vezérlőjelek**, **utasításértelmezés**

---

### 4.3 Execute
**Rövid definíció:**  
Az **execute** a tényleges műveletvégrehajtás fázisa.

**Működési elv:**  
- ALU vagy más végrehajtó egység végzi a műveletet.  
- Lehet aritmetikai, logikai, memória vagy vezérlési utasítás.  
- Ekkor keletkezik az eredmény vagy állapotváltozás.

**Egyszerű példa:**  
`ADD` esetén az ALU kiszámolja az összeget, `JMP` esetén a PC új címet kap.

**Vizsgán fontos kulcsszavak:**  
**execute**, **ALU művelet**, **vezérlési utasítás**, **állapotváltozás**

---

### 4.4 Write-back
**Rövid definíció:**  
A **write-back** lépésben az eredmény visszakerül regiszterbe vagy memóriába.

**Működési elv:**  
- A végrehajtás eredménye elmentésre kerül.  
- Ez teszi használhatóvá a következő utasítások számára.  
- Nem minden utasításnál van klasszikus write-back.

**Egyszerű példa:**  
Összeadás eredménye visszaírásra kerül az R1 regiszterbe.

**Vizsgán fontos kulcsszavak:**  
**write-back**, **visszaírás**, **eredménytárolás**

---

## 5. Párhuzamosság

### 5.1 Utasításszintű párhuzamosság (ILP)
**Rövid definíció:**  
Az **[[ILP]]** célja, hogy egy CPU-n belül több utasítás feldolgozása átfedjen.

**Működési elv:**  
- Az utasítás külön fázisai párhuzamosíthatók.  
- Fontos eszköz a **[[pipelining]]**.  
- Függőségek és elágazások korlátozhatják.

**Egyszerű példa:**  
Miközben az egyik utasítás dekódolódik, a következő már beolvasható.

**Vizsgán fontos kulcsszavak:**  
**[[ILP]]**, **utasításszintű párhuzamosság**, **[[pipelining]]**, **függőség**

---

### 5.2 Processzorszintű párhuzamosság
**Rövid definíció:**  
Processzorszintű párhuzamosságnál több mag vagy több CPU dolgozik egyszerre.

**Működési elv:**  
- A feladatokat szálakra vagy folyamatokra bontjuk.  
- Ezek külön magokon futhatnak.  
- Javulhat a teljesítmény és az áteresztőképesség.

**Egyszerű példa:**  
Böngésző külön szálon futtatja a felületet, a hálózati műveletet és a JavaScript-végrehajtást.

**Vizsgán fontos kulcsszavak:**  
**többmagos processzor**, **multiprocesszor**, **szál**, **párhuzamos végrehajtás**

---

### 5.3 Pipelining
**Rövid definíció:**  
A **[[pipelining]]** az utasítás-végrehajtási fázisok csővezetékes átfedése.

**Működési elv:**  
- A fetch/decode/execute/write-back fázisok külön „állomásként” működnek.  
- Ideális esetben minden ciklusban készül egy utasítás eredménye.  
- Veszélyek (hazardok) csökkenthetik a nyereséget.

**Egyszerű példa:**  
Olyan, mint egy futószalag: miközben az egyik darab festés alatt van, a másik már szerelés alatt.

**Vizsgán fontos kulcsszavak:**  
**[[pipelining]]**, **csővezeték**, **átfedés**, **hazard**, **throughput**

---

## 6. Korszerű számítógépek tervezési elvei

**Rövid definíció:**  
A modern architektúrák célja nagy teljesítmény elérése elfogadható energiafogyasztás mellett.

**Működési elv:**  
- Teljesítménynövelés: párhuzamosság, optimalizált végrehajtás.  
- Energiahatékonyság: frekvenciafeszültség-kezelés, hatékony magok.  
- **[[cache memória]]** és **[[memóriahierarchia]]** csökkenti a lassú főmemória-hozzáféréseket.

**Egyszerű példa:**  
Gyakran használt adat L1 cache-ben gyorsan elérhető, nem kell minden alkalommal RAM-ból olvasni.

**Vizsgán fontos kulcsszavak:**  
**teljesítmény**, **energiahatékonyság**, **[[cache memória]]**, **[[memóriahierarchia]]**, **párhuzamosság**

---

## 7. RISC és CISC architektúrák

### 7.1 RISC (Reduced Instruction Set Computer)
**Rövid definíció:**  
A **[[RISC]]** filozófia egyszerű, gyorsan végrehajtható utasításkészletet használ.

**Működési elv:**  
- Egyszerűbb, gyakran fix hosszúságú utasítások.  
- Több műveletet a fordító bont elemi lépésekre.  
- Jól illik pipelined végrehajtáshoz.

**Egyszerű példa:**  
ARM architektúrán sok mobilprocesszor energiahatékonyan működik RISC-szerű elvekkel.

**Vizsgán fontos kulcsszavak:**  
**[[RISC]]**, **egyszerű utasításkészlet**, **fix utasításhossz**, **pipeline-hatékonyság**

---

### 7.2 CISC (Complex Instruction Set Computer)
**Rövid definíció:**  
A **[[CISC]]** komplexebb utasításkészletet kínál, ahol egy utasítás több műveletet is végezhet.

**Működési elv:**  
- Gazdag utasításkészlet, változó utasításhossz is lehet.  
- Programszinten kevesebb utasítás szükséges ugyanarra a feladatra.  
- Hardveres dekódolás összetettebb.

**Egyszerű példa:**  
x86 processzorok sokféle komplex utasítást támogatnak visszafelé kompatibilitással.

**Vizsgán fontos kulcsszavak:**  
**[[CISC]]**, **komplex utasítás**, **változó utasításhossz**, **összetett dekódolás**

---

### 7.3 Összehasonlítás
**Rövid definíció:**  
A RISC és CISC eltérő tervezési filozófia, eltérő kompromisszumokkal.

**Működési elv:**  
- **RISC**: egyszerűbb utasítások, jellemzően több utasítás/program.  
- **CISC**: összetettebb utasítások, jellemzően kevesebb utasítás/program.  
- Modern processzorok gyakran hibrid módon közelítenek egymáshoz.

**Egyszerű példa:**  
Mai x86 CPU belül mikro-utasításokra bonthat komplex utasítást, ami RISC-szerű végrehajtást jelent.

**Vizsgán fontos kulcsszavak:**  
**RISC vs CISC**, **tervezési kompromisszum**, **hardverkomplexitás**, **mikro-utasítás**

---

### 7.4 Példák
**Rövid definíció:**  
A gyakorlatban az ARM és x86 jó szemléltető példa a két hagyományra.

**Működési elv:**  
- **[[ARM]]**: RISC-gyökerű, mobilban és beágyazott rendszerekben erős.  
- **[[x86]]**: CISC-gyökerű, PC-kben és szerverekben elterjedt.

**Egyszerű példa:**  
Okostelefonban általában ARM, asztali PC-ben jellemzően x86 architektúra dolgozik.

**Vizsgán fontos kulcsszavak:**  
**[[ARM]]**, **[[x86]]**, **mobil vs asztali architektúra**

---

## 8. Összefüggések
**Rövid definíció:**  
Az architektúra témakörei egymásra épülnek: alapmodell, CPU-működés, teljesítménynövelés, tervezési irányok.

**Működési elv:**  
- Neumann-modell adja az alap gondolkodási keretet.  
- CPU és adatút valósítja meg az utasítás-végrehajtást.  
- Párhuzamosság és cache növeli a gyakorlati teljesítményt.  
- RISC/CISC különböző megközelítései a végrehajtás szervezésének.

**Egyszerű példa:**  
Egy modern laptop CPU egyszerre használ pipeline-t, többmagos működést, cache-hierarchiát és hibrid utasítás-végrehajtást.

**Vizsgán fontos kulcsszavak:**  
**összefüggő architektúra-kép**, **teljesítményoptimalizálás**, **modell és megvalósítás**

---

## + Vizsgán érdemes még megemlíteni
- **[[Neumann-szűk keresztmetszet]]**: közös memóriaútvonal korlátozhatja a sebességet.  
- A **[[cache memória]]** kulcsszerepe a késleltetés csökkentésében.  
- A **[[pipelining]]** fő előnye a nagyobb áteresztőképesség.  
- Többmagos rendszerek a párhuzamos végrehajtás alapjai.  
- Modern CPU-k gyakran hibrid, vegyes (RISC/CISC-szerű) technikákat használnak.

---

## Rövid szóbeli összefoglaló
A Neumann-architektúra alapelve, hogy a program és adat közös memóriában van, és a CPU ciklikusan hajtja végre az utasításokat. A CPU fő részei a vezérlőegység, az ALU és a regiszterek, az adatmozgást pedig az adatút és a buszrendszer valósítja meg. Az utasítás-végrehajtási ciklus fetch, decode, execute és write-back lépésekből áll. A teljesítmény növelésének fő eszközei az utasításszintű párhuzamosság, a pipelining és a többmagos feldolgozás, valamint a cache-hierarchia. A RISC és CISC eltérő tervezési filozófiát képvisel: RISC egyszerűbb utasításokra, CISC összetettebb utasításokra épít, de a modern processzorok sokszor a kettőt kombinálják.

## Kulcsfogalmak
- [[Neumann-architektúra]]
- [[Neumann-szűk keresztmetszet]]
- [[CPU]]
- [[CU]]
- [[ALU]]
- [[regiszter]]
- [[PC]]
- [[IR]]
- [[adatút]]
- [[adatbusz]]
- [[pipelining]]
- [[ILP]]
- [[cache memória]]
- [[RISC]]
- [[CISC]]

## Tipikus vizsgakérdések
1. **Mi a tárolt program elve?**  
   Az utasítások és adatok közös memóriában vannak, a CPU onnan olvassa őket.

2. **Melyek a CPU fő részegységei?**  
   Vezérlőegység (CU), ALU és regiszterek.

3. **Mi a fetch-decode-execute ciklus lényege?**  
   Az utasítás beolvasása, értelmezése, végrehajtása, majd az eredmény visszaírása.

4. **Mi a különbség az adatbusz, címbusz és vezérlőbusz között?**  
   Adatbusz adatot visz, címbusz címet visz, vezérlőbusz vezérlőjeleket visz.

5. **Miért gyorsít a pipelining?**  
   Mert az utasításfázisok átfedésben futnak, így nő az áteresztőképesség.

6. **RISC és CISC között mi a fő különbség?**  
   RISC egyszerűbb utasításkészletre, CISC komplexebb utasításokra épít.

7. **Miért fontos a cache?**  
   Mert csökkenti a főmemória lassúságának hatását, így javítja a teljesítményt.

## Minimum, amit tudni kell
- A Neumann-architektúra alapelve (közös memória programnak és adatnak).  
- A CPU fő részei: CU, ALU, regiszterek.  
- A fetch-decode-execute-write-back ciklus lépései.  
- Busztípusok szerepe: adat-, cím- és vezérlőbusz.  
- Pipelining és ILP alapötlete.  
- Többmagos feldolgozás jelentősége.  
- Cache és memóriahierarchia szerepe a teljesítményben.  
- RISC és CISC közti fő különbség és tipikus példák (ARM, x86).
