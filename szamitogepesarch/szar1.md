# Számítógép architektúra – 27. tétel

## 1. Neumann-elvű gép

### 1.1 Alapfogalom

**Rövid definíció:**  
A **[[Neumann-architektúra]]** olyan számítógép-modell, ahol **a program utasításai és az adatok közös memóriában** vannak; a **[[CPU]]** ugyanabból a tárból olvassa az utasításokat és az adatokat.

**Működési elv:**  
- **Tárolt program elve:** a végrehajtandó műveletek **memóriában tárolt utasítások** formájában vannak jelen, nem „beégetett” külön hardverprogramként.  
- A végrehajtás **ciklikus**: utasítás **beolvasása → értelmezése → végrehajtása** (és gyakran eredmény **visszaírása**).  
- Egyszerű, általános célú séma; a gyakorlati gépek ennél bonyolultabbak, de az **alapgondolkodás** ettől indul.

**Egyszerű példa:**  
Egy összeadó program **utasításai** és a **összeadandó számok** ugyanabban a **[[RAM]]**-ban lehetnek — a processzor **nem két külön „tárból”** dolgozik.

**Vizsgán fontos kulcsszavak:**  
**[[Neumann-architektúra]]**, **tárolt program elve**, **közös memória**, **utasítás-végrehajtási ciklus**

### 1.2 Fő egységek

**Rövid definíció:**  
A Neumann-elvű gép **fő egységei** együtt végzik a feldolgozást és a külvilág felé az adatáramlást.

**Működési elv:**  
- **[[CPU]]**: utasítások **végrehajtása** és **vezérlése**.  
- **[[memória]]** (főtár): program és adatok **tárolása**, amit a CPU címek alapján elér.  
- **Bemenet (input)**: adat a külvilágból (billentyűzet, egér, szenzor…).  
- **Kimenet (output)**: eredmény kiadása (monitor, nyomtató…).  
- **Összeköttetés**: **[[busz]]** / kapcsolófelületek a CPU, memória és perifériák között.

**Egyszerű példa:**  
Szám beírása billentyűzetről (**bemenet**), a **[[CPU]]** feldolgozza a **[[memória]]**ban lévő program szerint, az eredmény megjelenik a képernyőn (**kimenet**).

**Vizsgán fontos kulcsszavak:**  
**[[CPU]]**, **[[memória]]**, **input**, **output**, **busz**, **Neumann-modell**

## 2. CPU felépítése

### 2.1 Részegységek

**Rövid definíció:**  
A **[[CPU]]** olyan integrált egység, amely **specializált részekből** áll, és ezek együtt hajtják végre a gépi utasításokat.

**Működési elv:**  
- **[[CU]]** (vezérlőegység, *Control Unit*): **ütemez**, **dekódoláshoz vezérlőjeleket** készít, **irányítja** az **[[adatút]]** működését.  
- **[[ALU]]** (*Arithmetic Logic Unit*): **arithmetikai és logikai** műveletek (pl. összeadás, AND, összehasonlítás).  
- **[[regiszter]]ek**: a CPU-n **belüli**, rendkívül **gyors**, kis kapacitású tárolók — itt „forog” az aktuális utasítás, operandus, cím.

**Egyszerű példa:**  
Összeadásnál a **[[CU]]** megmondja, **honnan** jöjjön a két szám és **hova** menjen az eredmény; a számok **[[regiszter]]**ből a **[[ALU]]**-ba kerülnek, ott **összeadódnak**.

**Vizsgán fontos kulcsszavak:**  
**[[CU]]**, **[[ALU]]**, **[[regiszter]]**, **vezérlés**, **végrehajtás**

### 2.2 Regiszterek

**Rövid definíció:**  
A **[[regiszter]]ek** a **[[CPU]]** leggyorsabb tárolói; az **aktuális végrehajtáshoz** szükséges utasításrészletek, operandusok és címek ide kerülnek.

**Működési elv:**  
- **[[PC]]** (*Program Counter*): a **következő** végrehajtandó utasítás **memóriacíme**.  
- **[[IR]]** (*Instruction Register*): az **éppen feldolgozott** utasítás **gépi alakja**.  
- **Általános célú regiszterek**: operandusok, köztes és végeredmények — a konkrét szám architektúrától függ, hány van és hogyan hívják őket.

**Egyszerű példa:**  
Ha a **[[PC]]** éppen a 200-as címet mutatja, a következő **fetch** ott olvassa az utasítást; betöltés után ez az utasítás látható az **[[IR]]**-ben, miközben a **[[PC]]** már a soron következő címre léphet.

**Vizsgán fontos kulcsszavak:**  
**[[PC]]**, **[[IR]]**, **általános célú regiszterek**, **gyors belső tárolás**

## 3. Adatút

### 3.1 Fogalom

**Rövid definíció:**  
Az **[[adatút]]** (*datapath*) a **[[CPU]]**-n **belüli** az a **hardveres útvonal**, amin az **operandusok mozognak** és ahol az **[[ALU]]** (és kapcsolódó egységek) **feldolgozza** őket.

**Működési elv:**  
- Összeköti a **[[regiszter]]eket**, multiplexer(ek)et, **[[ALU]]**-t, gyakran ide kapcsolódó ideiglenes tárolókat.  
- A **[[CU]]** **vezérlőjelekkel** dönti el: **melyik regiszter** kapcsolódjon be, **milyen ALU-művelet** fusson, **hova** íródjon az eredmény.  
- Az **adatút** a „**mit számolunk**”; a **[[CU]]** a „**mikor és hogyan**”.

**Egyszerű példa:**  
Mint egy **gyár futószalag-szakasza** csak az **adagoknak**: két szám **beesik** az **[[ALU]]** „gépébe”, összeadódnak, a **végeredmény** egy **[[regiszter]]**be **visszakerül** — a **sínrendszer + kapcsolók**, amin ez történik, az **[[adatút]]**.

**Vizsgán fontos kulcsszavak:**  
**[[adatút]]**, **adatáramlás**, **[[ALU]]**, **vezérlőjelek**, **[[CU]]**

### 3.2 Buszrendszer

**Rövid definíció:**  
A **buszrendszer** **közös kommunikációs csatornákat** jelent a **[[CPU]]**, **[[memória]]** és **perifériák** között (és a lapkán belül is lehet több szint).

**Működési elv:**  
- **[[adatbusz]]**: a **tényleges adat** (pl. beolvasott utasítás, memóriaszó) továbbítása.  
- **[[címbusz]]**: **melyik** memóriacímre/perifériára hivatkozunk.  
- **[[vezérlőbusz]]**: **vezérlőjelek** (olvasás/írás, időzítés, megszakítás-kérések jellegű információk).

**Egyszerű példa:**  
Memóriaolvasásnál a **[[címbusz]]**on kimegy pl. a **200**, a **[[vezérlőbusz]]** jelzi: „**olvasás**”, a **[[adatbusz]]**on visszaérkezik a **memóriaszó** (pl. egy gépi utasítás).

**Vizsgán fontos kulcsszavak:**  
**[[adatbusz]]**, **[[címbusz]]**, **[[vezérlőbusz]]**, **memória-hozzáférés**

## 4. Utasítás-végrehajtás ciklusa

### 4.1 Fetch

**Rövid definíció:**  
A **fetch** (*lekérés*) lépésben a **[[CPU]]** **beolvassa** a **[[PC]]** által mutatott helyről a **következő utasítást** a **[[memória]]**ból.

**Működési elv:**  
- A **[[PC]]** **címet** ad a **[[memória]]**-hoz.  
- Az beolvasott gépi szó az **[[IR]]**-be (vagy egy előtár-regiszterbe) kerül.  
- A **[[PC]]** tipikusan **lép** a következő utasításra (kivéve, ha később ugrás módosítja).

**Egyszerű példa:**  
Ha **[[PC]] = 1000**, a fetch a **1000-es címen** lévő utasítást hozza be — olyan, mintha a könyvben a **könyvjelző** szerinti **következő sort** felolvasnánk.

**Vizsgán fontos kulcsszavak:**  
**fetch**, **[[PC]]**, **[[IR]]**, **utasításbeolvasás**

### 4.2 Decode

**Rövid definíció:**  
A **decode** (*dekódolás*) során a **[[CPU]]** **értelmezi** az utasítást: **milyen művelet** és **milyen operandusok** tartoznak hozzá.

**Működési elv:**  
- A **műveletkód** (**opcode**) alapján kiválasztódik a végrehajtandó művelet típusa.  
- A **[[CU]]** **vezérlőjeleket** állít elő az **[[adatút]]** számára.  
- Eldőlnek az operandusforrások (**[[regiszter]]**, azonnali érték, memóriacím — architektúrától függően).

**Egyszerű példa:**  
Ha az utasítás „**ADD R1, R2**” jellegű, dekódolásra kiderül: **összeadás**, források **R1 és R2**, nem memóriabetöltés — mint amikor a **receptből** kiolvasod: „**keverd össze**” vs „**süsd**”.

**Vizsgán fontos kulcsszavak:**  
**decode**, **opcode**, **[[CU]]**, **utasításértelmezés**

### 4.3 Execute

**Rövid definíció:**  
Az **execute** (*végrehajtás*) fázisban történik a **tényleges művelet**: számolás, memóriahozzáférés, ugrás, stb.

**Működési elv:**  
- **[[ALU]]** vagy más végrehajtó egység **elvégzi** a műveletet.  
- Lehet **arithmetikai/logikai**, **memóriaolvasás/írás**, **vezérlésátadás** (ugrás, hívás).  
- Ekkor keletkezik **eredmény** és/vagy **állapotváltozás** (pl. **[[PC]]** új értéke ugrásnál).

**Egyszerű példa:**  
**ADD**: az **[[ALU]]** kiszámolja az összeget; **JMP**: nem kell ALU-összeadás, viszont a **[[PC]]** **új címet** kap — a „**végrehajtás**” itt **címátállítás**.

**Vizsgán fontos kulcsszavak:**  
**execute**, **[[ALU]]**, **memória-művelet**, **vezérlésátadás**, **[[PC]]**

### 4.4 Write-back

**Rövid definíció:**  
A **write-back** (*visszaírás*) lépésben az eredmény **visszakerül** oda, ahol a következő utasítások **elérik**: tipikusan **[[regiszter]]**be vagy **[[memória]]**ba.

**Működési elv:**  
- A végrehajtás **eredménye** **elmentésre** kerül a célhelyre.  
- Ez teszi **újra felhasználhatóvá** a számot a program számára.  
- Nem minden utasításnál van külön, kiemelhető write-back fázis (architektúra- és utasítástípus-függő).

**Egyszerű példa:**  
Összeadás után az eredmény **visszaíródik R3-ba** — a következő utasítás már **R3-ból olvashat**, mint kész értékből.

**Vizsgán fontos kulcsszavak:**  
**write-back**, **visszaírás**, **regiszter**, **memóriaírás**

## 5. Párhuzamosság

### 5.1 Utasításszintű párhuzamosság (ILP)

**Rövid definíció:**  
Az **[[ILP]]** (*instruction-level parallelism*) azt jelenti, hogy **egyetlen végrehajtó egységen (magon) belül** igyekszünk **egy időben több utasításhoz** is hozzájárulni.

**Működési elv:**  
- Gyakori eszköz: **[[pipelining]]** — az utasítás **fázisai átfedésben** futnak.  
- Léteznek **összetettebb** technikák is (pl. szupereszkálás, out-of-order — elég említésszinten), de vizsgán a **pipeline-ötlet** a központi.  
- **Korlátok**: **adatfüggőség** (az egyik eredményére vár a másik), **vezérlési függőség** (elágazás), erőforrás-ütközés — ezek **lelassíthatják** az ideális párhuzamosságot.

**Egyszerű példa:**  
Miközben az egyik utasítás **execute** fázisban van, a következő már **fetch/decode** alatt lehet — mint amikor **mosogatás** közben már **töltöd** a gépet: **egy ember**, de **több lépés egyszerre** halad.

**Vizsgán fontos kulcsszavak:**  
**[[ILP]]**, **utasításszintű párhuzamosság**, **[[pipelining]]**, **függőség**

### 5.2 Processzorszintű párhuzamosság

**Rövid definíció:**  
**Processzorszintű párhuzamosságnál** **több végrehajtó egység** (**többmagos** **[[CPU]]**, vagy több processzor) dolgozik **valóban párhuzamosan**.

**Működési elv:**  
- A szoftver **szálakra/folyamatokra** bontható; ezek **külön magokon** futhatnak.  
- **Skálázódás** nem automatikus: a programnak **párhuzamosíthatónak** kell lennie, különben **egy mag** lesz terhelve.  
- Nőhet az **áteresztőképesség** több **független** feladatnál.

**Egyszerű példa:**  
**[[ILP]]** = **egy szakács**, több edényben főz egyszerre; **többmag** = **több szakács** ugyanazon a konyhán — több **komplett** fogás készülhet egyszerre, ha van **elég külön feladat**.

**Vizsgán fontos kulcsszavak:**  
**többmagos processzor**, **multiprocesszor**, **szál**, **párhuzamos végrehajtás**

### 5.3 Pipelining

**Rövid definíció:**  
A **[[pipelining]]** (*csővezeték*) az utasítás-végrehajtás **fázisainak átfedése**: különböző utasítások **különböző fázisban** vannak **uganabban az időben**.

**Működési elv:**  
- Tipikus fázisok: **fetch → decode → execute → write-back** (lehet tovább bontva).  
- **Áteresztőképesség** (*throughput*): ideálisan **minden órajelciklusban** „**készül el**” egy utasítás a pipeline végén (betelt állapot után).  
- **Egyetlen** utasítás **teljes ideje** nem feltétlenül csökken; a **nyereség** a **sok utasítás** együttes üteme.  
- **Hazard** („ütközés”): pl. függőség miatt **üres ciklus** / buborék.

**Egyszerű példa:**  
**Autógyár futószalagja:** miközben az egyik autót **fényezik**, a másikat **szerelik**, a harmadikat **összerakják** — **uganannyi idő alatt több autó** készül el, mint ha egy autót **végigvinél** minden állomáson **szekvenciálisan**, mielőtt a következőnek kezdenél.

**Vizsgán fontos kulcsszavak:**  
**[[pipelining]]**, **csővezeték**, **átfedés**, **throughput**, **hazard**

## 6. Korszerű tervezési elvek

**Rövid definíció:**  
A **korszerű processzorok** tervezése a **magas teljesítmény** és az **elfogadható energiafogyasztás / hő** egyensúlyára épül, **memória-késleltetés** elleni védekezéssel.

**Működési elv:**  
- **Párhuzamosság**: **[[pipelining]]**, több végrehajtó egység, **többmag**.  
- **[[memóriahierarchia]]**: **[[cache memória]]** (L1/L2/L3) a **lassú [[RAM]]** előtt — a **gyakori adat közelebb** van a **[[CPU]]**-hoz.  
- **Energia**: dinamikus frekvencia/feszültség-szabályozás, **takarékos magok** mobil eszközökben.  
- **Összetett végrehajtás** (említés): modern **[[x86]]** belül gyakran **mikro-utasításokra** bont; kifelé **CISC**, belül **RISC-szerű** végrehajtás.

**Egyszerű példa:**  
A **[[cache]]** olyan, mint a **íróasztal fiókja**: ami **gyakran kell**, ott van **kéznél**; ami ritkán, a **pincében** (**[[RAM]]**) — kevesebb „**le-fel szaladgálás**”, gyorsabb munka.

**Vizsgán fontos kulcsszavak:**  
**teljesítmény**, **energiahatékonyság**, **[[cache memória]]**, **[[memóriahierarchia]]**, **párhuzamosság**

## 7. RISC és CISC

### 7.1 RISC

**Rövid definíció:**  
A **[[RISC]]** (*Reduced Instruction Set Computer*) olyan tervezési irány, amely **egyszerű, gyorsan dekódolható és végrehajtható** utasításokra épít.

**Működési elv:**  
- **Kevés, egyszerű** utasítástípus; gyakran **fix utasításhossz**.  
- A **komplexebb** feladatot a **fordító** bontja **több egyszerű** utasításra.  
- Jól illeszkedik a **[[pipelining]]**-hez, mert az utasítások **egyenletesek** és **kis lépések**.

**Egyszerű példa:**  
Mint **építőkocka-készlet** **kis**, **egyféle** elemekből: sok **kis lépésből** épül fel bármi, de **minden lépés** **gyorsan** megvan.

**Vizsgán fontos kulcsszavak:**  
**[[RISC]]**, **egyszerű utasításkészlet**, **fix utasításhossz**, **pipeline-barát**

### 7.2 CISC

**Rövid definíció:**  
A **[[CISC]]** (*Complex Instruction Set Computer*) **gazdagabb utasításkészletet** ad: egy utasítás **több részműveletet** is elvégezhet.

**Működési elv:**  
- **Komplex** utasítások, **változó** utasításhossz gyakori.  
- Programszinten **kevesebb utasítás** is eléghet ugyanarra a feladatra.  
- A **hardveres dekódolás** **bonyolultabb** lehet; a végrehajtás időzítése **utasításonként** változhat.

**Egyszerű példa:**  
Mint egy **távirányító** sok **egygombos** funkcióval: egy nyomásra **sok minden** történhet — **kényelmes**, de a **belső logika** **összetettebb**.

**Vizsgán fontos kulcsszavak:**  
**[[CISC]]**, **komplex utasítás**, **változó utasításhossz**, **gazdag utasításkészlet**

### 7.3 Összehasonlítás (táblázat!)

**Rövid definíció:**  
**[[RISC]]** és **[[CISC]]** **két klasszikus filozófia**: az egyik az **egyszerű, gyors lépéseket**, a másik a **gazdag, tömör utasításokat** helyezi előtérbe.

**Működési elv:**  
- **[[RISC]]**: komplexitás gyakran **szoftver (fordító)** felé tolódik; **hardver** egyszerűbb végrehajtást céloz.  
- **[[CISC]]**: komplexitás **hardver + utasításkészlet** felé tolódik; **kevesebb** gépi utasítás lehet a forráskód egy részére.  
- **Ma:** sok **[[x86]]** processzor **kifelé CISC**, **belül** **mikro-op** / **RISC-szerű** magokkal hajt végre.

**Egyszerű példa:**  
Ugyanaz a **ciklus** **[[RISC]]**-en lehet **hosszabb utasításlista**, de **minden sor** „**egyszerű**”; **[[CISC]]**-en lehet **kevesebb sor**, de egy-egy sor **„sűrűbb”**.

**Vizsgán fontos kulcsszavak:**  
**[[RISC]] vs [[CISC]]**, **kompromisszum**, **mikro-utasítás**, **fordító vs hardver**

| Szempont | **[[RISC]]** | **[[CISC]]** |
|----------|----------------|----------------|
| Utasítások típusa | Főleg **egyszerű**, kevés alapművelet | **Gazdag**, **komplex** utasítások is |
| Utasításhossz | Gyakran **fix** | Gyakran **változó** |
| Tipikus cél | **Pipeline**, gyors **órajel**-hez illeszkedő lépések | **Tömör kód**, **visszafelé kompatibilitás** (főleg **[[x86]]**) |
| Komplexitás eltolása | Gyakran **fordító** felé | Gyakran **dekódoló / mikroarchitektúra** felé |
| Vizsgapélda | **[[ARM]]** | **[[x86]]** / Intel, AMD |

### 7.4 Példák

**Rövid definíció:**  
Tipikus **[[RISC]]**-példa: **[[ARM]]**; tipikus **[[CISC]]**-gyökér: **[[x86]]** család (PC-k, szerverek).

**Működési elv:**  
- **[[ARM]]**: mobil, beágyazott, ma már **szerver** / laptop (**Apple Silicon**) környezetben is erős.  
- **[[x86]]**: hagyományos **asztali Windows/Linux** világ, **hosszú** utasítás-kompatibilitás.

**Egyszerű példa:**  
**Telefon/tablet** processzor: gyakran **[[ARM]]**; **klasszikus asztali gép**: gyakran **[[x86]]**-64.

**Vizsgán fontos kulcsszavak:**  
**[[ARM]]**, **[[x86]]**, **mobil vs asztali**, **ISA**

## 8. Összefüggések

**Rövid definíció:**  
A tétel elemei **egy lánc**: **Neumann-modell** → **[[CPU]]-felépítés** → **[[adatút]] + busz** → **utasításciklus** → **párhuzamosság** → **korszerű** **cache/többmag** → **[[RISC]]/[[CISC]]** megközelítés.

**Működési elv:**  
- A **tárolt program** és a **közös memória** megadja, **mit** és **honnan** hajt végre a gép.  
- A **[[CPU]]** **[[CU]]** + **[[ALU]]** + **[[regiszter]]** + **[[adatút]]** révén **valósítja meg** a gépi utasításokat.  
- **[[pipelining]]** és **többmag** **növeli** a gyakorlati sebességet; **[[cache]]** **csökkenti** a memória-várakozást.  
- **[[RISC]]/[[CISC]]** az **utasításkészlet** szintjének **különböző kompromisszuma** — a **modern CPU** gyakran **vegyes** technikákat használ.

**Egyszerű példa:**  
Egy **laptop CPU**: **Neumann-elvű** gépen fut a program, **fetch–decode–execute** megy, közben **pipeline** és **2–16 mag**, **L1/L2/L3 cache**, és lehet **[[x86]]** utasításkészlet **belső** **mikro-op** végrehajtással.

**Vizsgán fontos kulcsszavak:**  
**architektúra-összefüggés**, **modell vs megvalósítás**, **teljesítmény**

## + Vizsgán érdemes még megemlíteni

- **[[Neumann-szűk keresztmetszet]]**: a **közös** memória/busz **egyszerre keveset** tud átvinni — korlátozhatja a **[[CPU]]** „éhségét”.  
- **[[cache memória]]**: a **legfontosabb** gyakorlati gyorsítás a **[[RAM]]** lassúsága ellen.  
- **[[pipelining]]** fő nyeresége: **áteresztőképesség**, nem feltétlenül **egyetlen** utasítás **ideje**.  
- **Többmag** önmagában nem **varázs**: kell **párhuzamosítható** munka.  
- **[[x86]]** ma gyakran **hibrid**: **CISC ISA**, **RISC-szerű belső** végrehajtás.

## Rövid szóbeli összefoglaló

A **[[Neumann-architektúra]]** lényege a **tárolt program** és a **közös memória**: utasítás és adat **ugyanott** lehet. A **[[CPU]]** **[[CU]]**-val irányít, **[[ALU]]**-val számol, **[[regiszter]]ekben** tartja az aktuális adatokat; az **[[adatút]]** a belső **adat- és műveleti pálya**, a **buszrendszer** pedig **[[CPU]]–[[memória]]–periféria** kapcsolat. Az utasítás **fetch, decode, execute, write-back** lépésekben fut. **[[ILP]]** és **[[pipelining]]** **egy magon** átfedést ad; **többmag** **valódi párhuzamosság** több szálon. **[[RISC]]** **egyszerű** utasítások (**[[ARM]]**), **[[CISC]]** **gazdag** utasítások (**[[x86]]**); a modern gépek **cache-t**, **hierarchiát** és gyakran **hibrid** végrehajtást használnak.

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
- [[címbusz]]
- [[vezérlőbusz]]
- [[memória]]
- [[RAM]]
- [[pipelining]]
- [[ILP]]
- [[cache memória]]
- [[memóriahierarchia]]
- [[RISC]]
- [[CISC]]
- [[ARM]]
- [[x86]]

## Tipikus vizsgakérdések

1. **Mi a tárolt program elve?**  
   Az utasítások **memóriában** vannak, a **[[CPU]]** onnan olvassa és hajtja végre őket, **ugyanúgy** kezelhető „adatként”, mint a számok (Neumann-elv).

2. **Melyek a Neumann-gép fő egységei?**  
   **[[CPU]]**, **[[memória]]**, **bemenet**, **kimenet** (és összeköttetés / **busz**).

3. **Melyek a [[CPU]] fő részegységei?**  
   **[[CU]]**, **[[ALU]]**, **[[regiszter]]ek**.

4. **Mit tart a [[PC]] és az [[IR]]?**  
   **[[PC]]**: következő utasítás **címe**; **[[IR]]**: az **aktuális** utasítás **gépi kódja**.

5. **Mi a fetch–decode–execute–write-back ciklus?**  
   Beolvasás, értelmezés, végrehajtás, eredmény **visszaírása** (ahol kell).

6. **Mi az [[adatút]]?**  
   A **[[CPU]]** belső **hardveres útvonala** az adatmozgásnak és **[[ALU]]**-műveleteknek, **[[CU]]** vezérli.

7. **Mi a különbség adat-, cím- és vezérlőbusz között?**  
   **Adat**, **cím**, **vezérlőjelek** külön szerepkörben.

8. **[[ILP]] vs processzorszintű párhuzamosság?**  
   **[[ILP]]**: egy mag **belül** több utasítás átfedése; **processzorszintű**: **több mag** / processzor **párhuzamosan**.

9. **Miért gyorsít a [[pipelining]]?**  
   Mert a fázisok **átfedésben** futnak → nő az **áteresztőképesség** (sok utasítás üteme).

10. **[[RISC]] és [[CISC]] fő különbsége?**  
    **Egyszerű, pipeline-barát** utasítások vs **gazdag, komplex** utasításkészlet; példa: **[[ARM]]** vs **[[x86]]**.

11. **Miért fontos a [[cache]]?**  
    Csökkenti a **[[RAM]]**-ra várakozást, **közelebb** tartja a gyakori adatot a **[[CPU]]**-hoz.

## Minimum, amit tudni kell

- **[[Neumann-architektúra]]**: közös **memória** programnak és adatnak; **tárolt program**.  
- **[[CPU]]**: **[[CU]]**, **[[ALU]]**, **[[regiszter]]**; **[[PC]]**, **[[IR]]** szerepe.  
- **[[adatút]]** + **busz**: **adat / cím / vezérlés**.  
- **Fetch–decode–execute–write-back**.  
- **[[ILP]]**, **[[pipelining]]**, **többmag** — mi a különbség.  
- **[[cache memória]]**, **[[memóriahierarchia]]** lényege.  
- **[[RISC]]** vs **[[CISC]]** táblázatban; **[[ARM]]**, **[[x86]]** példa.
