# Számítógép architektúra – 28. tétel

## 1. Háttértárak

### 1.1 Feladat

**Rövid definíció:**  
A **[[háttértár]]** (másodlagos tároló) feladata, hogy a programok, fájlok és rendszeradatok **tartósan**, **kikapcsolás után is** megmaradjanak — ellentétben a **[[RAM]]**-mal, ami **illékony** munkamemória.

**Működési elv:**  
- **Nem felejtő** tárolás: az információ **mágneses**, **optikai**, **flash** vagy **mágneses szalagos** rétegen „megmarad” áram nélkül is.  
- A **[[CPU]]** a futáshoz a **[[RAM]]**-ba tölti az adatot; a **[[háttértár]]** a **nagy kapacitású**, **lassabb** „raktár”.  
- A választást **sebesség**, **kapacitás**, **ár/GB**, **élettartam** és **feladat** (rendszerlemez vs archívum) határozza meg.

**Egyszerű példa:**  
A **[[SSD]]** / **[[HDD]]** meghajtón marad a **fotó** és a **dolgozat**, ha lehúzod a gépet a konnektorból; a **[[RAM]]**ban lévő **megnyitott**, nem mentett szöveg **elvész**.

**Vizsgán fontos kulcsszavak:**  
**[[háttértár]]**, **tartós tárolás**, **nem felejtő**, **[[RAM]] vs háttértár**, **kapacitás**

## 2. Háttértár típusok

### 2.1 HDD

**Rövid definíció:**  
A **[[HDD]]** (*Hard Disk Drive*) **forgó mágneses lemezekre** ír és onnan olvas **mozgó olvasó/író fejjel** — klasszikus „**winchester**” háttértár.

**Működési elv:**  
- **Mechanikus** pozicionálás: a fej a megfelelő **sávra** kerül, a lemez **forog** — ez **késleltetést** ad (keresés, rotációs várakozás).  
- **Nagy kapacitás**, jó **ár/GB**; **random** és **szekvenciális** olvasás is lehetséges, de a **random** lassabb, mint **[[SSD]]**-nél.  
- **Rezgés**, **ütődés** érzékenyebb, mint egy **flash** lemeznél.

**Egyszerű példa:**  
Olyan, mint egy **lejátszólemez + tű**: a **tűt** odébb kell tenni a megfelelő **sávhoz**, majd **várnod** kell, míg a **lemez** aláfordul — **sok adat olcsón**, de **nem „azonnal ott”** minden bájt.

**Vizsgán fontos kulcsszavak:**  
**[[HDD]]**, **mágneses lemez**, **mozgó fej**, **kapacitás/ár**, **késleltetés**

### 2.2 SSD

**Rövid definíció:**  
Az **[[SSD]]** (*Solid State Drive*) **félvezetős flash** memóriacellákban tárol adatot **mozgó alkatrész nélkül**.

**Működési elv:**  
- **Nincs** mechanikus fej — **alacsony késleltetés**, **gyors random** hozzáférés tipikusan **[[HDD]]**-hez képest.  
- **Írási** élettartam és **vezérlő**-algoritmusok számítanak (wear leveling — elég említés).  
- **Ár/GB** általában **magasabb**, mint **[[HDD]]**-nél.

**Egyszerű példa:**  
Olyan, mint a **telefon belső tárhelye**: **nincs forgó rész**, „**bárhová**” gyorsan **ugrasz** olvasni — ezért **gyorsan indul** róla a **rendszer**.

**Vizsgán fontos kulcsszavak:**  
**[[SSD]]**, **flash**, **nincs mechanika**, **alacsony késleltetés**, **drágább/GB**

### 2.3 Optikai

**Rövid definíció:**  
Az **[[optikai háttértár]]** **lézerrel** olvassa (és írja, ha írható) a lemez **pit**/**land** mintázatát — **CD**, **DVD**, **Blu-ray**.

**Működési elv:**  
- A fej **optikailag** követi a spirált; sebesség és kapacitás a **formátumtól** függ.  
- **Ritkán írt**, **hosszú távú** adathordozónak vagy **telepítőnek** volt ideális; ma a **hálózatos** terjesztés miatt kevésbé központi.

**Egyszerű példa:**  
Mint egy **zenelemez**, amit **lézerrel** „**tapintasz**” végig: **jó archív példány**, de **nem** ez a leggyorsabb **mindennapi** munkameghajtó.

**Vizsgán fontos kulcsszavak:**  
**[[optikai háttértár]]**, **CD/DVD/Blu-ray**, **lézer**, **archiválás**

### 2.4 Szalagos

**Rövid definíció:**  
A **[[szalagos háttértár]]** **mágneses szalagon**, **szekvenciálisan** tárol nagy adatmennyiséget — főleg **mentés** és **archiválás**.

**Működési elv:**  
- **Sorban** kell haladni az adaton (nincs valódi **random** ugrás egy fájlra, mint **[[HDD]]**-nél); egy fájlhoz gyakran **sok tekerés**.  
- **Nagyon jó TB/$** és **hosszú megőrzés** adatközponti környezetben; **helyreállítási idő** lehet nagy.

**Egyszerű példa:**  
Mint egy **VHS szalag**: ha a **film vége** kell, **végig kell tekerni** — **olcsó nagy tár**, de **nem** „**nyisd ki a 47. fájlt azonnal**” típusú használatra.

**Vizsgán fontos kulcsszavak:**  
**[[szalagos háttértár]]**, **szekvenciális elérés**, **backup**, **nagy kapacitás**

## 3. Összehasonlítás (TÁBLÁZAT kötelező!)

**Rövid definíció:**  
A háttértár-típusok **ugyanazt a feladatot** (tartós tárolás) **más-más kompromisszummal** oldják meg: **sebesség**, **ár**, **elérési mód**, **felhasználás**.

**Működési elv:**  
- **[[HDD]]** és **[[SSD]]** tipikusan **fájlrendszeres**, **random** hozzáféréses munka- és adatlemez.  
- **Optikai** és **szalag** inkább **médium** / **mentési réteg** szerepben maradt.  
- Gyakorlatban **kombinálják**: pl. **[[SSD]]** rendszernek, **[[HDD]]** nagy tárnak, **szalag** heti mentésnek.

**Egyszerű példa:**  
**[[SSD]]** = **kéznél lévő íróasztal**; **[[HDD]]** = **szekrény** nagy dobozokkal; **szalag** = **pince raktár** olcsón, de **keresgélni** macerás.

**Vizsgán fontos kulcsszavak:**  
**sebesség–kapacitás–ár**, **random vs szekvenciális**, **rétegezett tárolás**

### Fő típusok egy táblázatban

| Típus | Technológia | Mozgó alkatrész | Random hozzáférés | Ár/GB (tipikusan) | Jellemző felhasználás |
|--------|-------------|-----------------|-------------------|-------------------|------------------------|
| **[[HDD]]** | Mágneses forgó lemez + fej | **Igen** | Van, de **lassabb** | **Alacsony** | Nagy fájltár, archívum |
| **[[SSD]]** | **Flash** (NAND) | **Nem** | **Gyors** | **Magasabb** | OS, alkalmazások, gyors munka |
| **[[optikai háttértár]]** | Lézer + lemez | Igen (forgás) | Korlátozott / lassabb | Közepes / alacsony (lemez) | Telepítő, archív média |
| **[[szalagos háttértár]]** | Mágneses szalag | Igen (tekercs) | **Gyakorlatilag nem** | **Nagyon alacsony** / TB | **Backup**, archívum |

### [[HDD]] vs [[SSD]] — vizsgán ezt hasonlítsd össze

| Szempont | **[[HDD]]** | **[[SSD]]** |
|-----------|-------------|-------------|
| **Mechanika** | Forgó lemez, mozgó fej | **Nincs** forgó rész |
| **Késleltetés / random I/O** | Nagyobb (fejmozgatás) | **Kisebb**, „**ugrálós**” fájloknál előny |
| **Kapacitás / ár** | **Jobb** nagy tár olcsón | Drágább ugyanannyi GB-ért |
| **Zaj / ütés** | Zúghat, **érzékenyebb** | Csendesebb, **rázásra** ellenállóbb |
| **Tipikus szerep** | Adattó, média | Rendszerlemez, gyors projektlemez |

**Vizsgán visszamondható mondat:** „**[[HDD]]**: olcsó és nagy, de **mechanikus** és **lassabb randomnal**; **[[SSD]]**: **gyors** és **nincs fej**, de **drágább gigabájtonként**.”

## 4. RAID

### 4.1 Cél

**Rövid definíció:**  
A **[[RAID]]** (*Redundant Array of Independent Disks*) **több fizikai lemezt** egy **logikai egységként** kezel: cél a **teljesítmény** és/vagy a **hibatűrés** (redundancia) javítása.

**Működési elv:**  
- **Striping** (szétosztás): adat **több lemezre** kerül → **gyorsabb** lehet az átvitel.  
- **Mirroring** (tükrözés): **ugyanaz** a másolat **több lemezen** → **egy lemez** kieshet.  
- **Paritás**: **hibajavító** extra információ → kevesebb „nyers” kapacitás, de **védelem**.  
- **Fontos:** **[[RAID]] ≠ backup** — **törlés**, **ransomware**, **emberi hiba** ellen **nem** helyettesíti a **mentési stratégiát**.

**Egyszerű példa:**  
A **[[RAID]]** olyan, mint **több párhuzamos sáv** az autópályán (**gyorsabb**), vagy **második példány** a fontos iratról (**biztonság**) — de ha **mindkettőt** **összegyűrűd**, a **másolat** sem segít → kell **külön mentés**.

**Vizsgán fontos kulcsszavak:**  
**[[RAID]]**, **striping**, **mirroring**, **paritás**, **hibatűrés**, **nem backup**

### 4.2 RAID 0

**Rövid definíció:**  
A **[[RAID 0]]** **striping**: az adat **darabokra** bontva **több lemezre** folyik, **redundancia nélkül**.

**Működési elv:**  
- **Párhuzamos** írás/olvasás → **nőhet a sebesség**.  
- **Egyetlen lemez** hibája gyakran a **tömb egészét** veszélyezteti (adat **részek** elvesznek).  
- **Hasznos kapacitás** közel a lemezek **összege** (nincs **tükör**- vagy **paritás**-helyfoglalás).

**Egyszerű példa:**  
**Gyors**, de **veszélyes**, mint **két motor egy autóban**, de **egy lánc** köti őket: **egyik szétcsúszik**, **megáll minden**.

**Vizsgán fontos kulcsszavak:**  
**[[RAID 0]]**, **striping**, **gyors**, **nincs hibatűrés**, **kockázat**

**Vizsgán visszamondható mondat:** „**RAID 0** = **gyors**, de **üvegpadló**: **egy lemez**, és **nagyon fáj**.”

### 4.3 RAID 1

**Rövid definíció:**  
A **[[RAID 1]]** **mirroring** (*tükrözés*): **ugyanaz** az adat **legalább két lemezen** **azonos** másolatban van.

**Működési elv:**  
- **Minden írás** minden **tükörre** lefut → **lassabb írás** lehet, olvasás **több forrásból** optimalizálható.  
- **Egy lemez** kiesése után is van **másolat** → **magas rendelkezésre állás**.  
- **Ár / kapacitás:** két azonos lemeznél a **hasznos** kapacitás kb. **a fele** (a másik a másolat).

**Egyszerű példa:**  
**Biztonságos**, de **drága** tárhelyben: mint ha **minden fájlt** **kétszer** nyomtatnál **papírra** — **egyik** **elveszik**, **még mindig megvan** a másik.

**Vizsgán fontos kulcsszavak:**  
**[[RAID 1]]**, **mirroring**, **hibatűrés**, **kapacitásfelárat**

**Vizsgán visszamondható mondat:** „**RAID 1** = **biztonságos**, mert **van másolat**, de **fizetsz** érte: **fele annyi** a **hasznos** hely.”

### 4.4 RAID 5

**Rövid definíció:**  
A **[[RAID 5]]** **elosztott paritást** használ: **adat** és **paritás** **több lemezen** váltakozik — **egy lemez** hibája **visszaépíthető**.

**Működési elv:**  
- Legalább **3 lemez** szükséges.  
- **Paritás** minden írásnál **frissül** → **írás** terhelhetőbb, mint **[[RAID 0]]**-nál.  
- **Hasznos kapacitás** kb. **n−1** lemez (egy lemeznyi kapacitást a **paritás** foglal el).

**Egyszerű példa:**  
Mint a **Sudoku egy extra sora**: ha **egy szám** (**lemez**) „**kihullik**”, a **többi** alapján **visszakövetkezteted** — **nem** kell **dupla** teljes másolat, de **van** védelem.

**Vizsgán fontos kulcsszavak:**  
**[[RAID 5]]**, **elosztott paritás**, **egy lemezhiba**, **kompromisszum**

### 4.5 RAID 10 (röviden)

**Rövid definíció:**  
A **[[RAID 10]]** (1+0): **először tükrök** (**[[RAID 1]]** párok), ezekre **striping** (**[[RAID 0]]**) — **sebesség** és **hibatűrés** együtt, **több lemez** és **költség** árán.

**Működési elv:**  
- **Minimum 4 lemez** (tipikus elrendezés).  
- **Egy lemez** kiesése **a saját párján** belül kezelhető; **rossz kombináció** több hibánál már **végzetes** lehet.  
- **Adatbázisok**, **nagy IOPS** igényű szolgáltatások kedvelt megoldása.

**Egyszerű példa:**  
**Két párhuzamos sáv**, mindegyiken **biztonsági másolat** — **gyors** és **strapabíró**, de **sok lemez** kell.

**Vizsgán fontos kulcsszavak:**  
**[[RAID 10]]**, **mirror + stripe**, **teljesítmény + redundancia**, **≥4 lemez**

## 5. Nyomtatók

### 5.1 Tintasugaras

**Rövid definíció:**  
A **[[tintasugaras nyomtató]]** apró **folyékony tintacseppeket** juttat a papírra (piezo vagy hőbuborék elv — elég: **csepp** alapú).

**Működési elv:**  
- **Felbontás** és **színátmenet** jó lehet; **fotó** és **kevés** oldal otthonra ideális.  
- **Nagy mennyiség** / oldalankénti költség gyakran **rosszabb**, mint **[[lézernyomtató]]**-nál; **szárítás**, **fej** karbantartás lehet szempont.

**Egyszerű példa:**  
Mint a **filctoll** és a **permetező** keveréke: **szép szín**, de ha **napi 500 oldal** kell, **hamar** „**elfogy**” és **lassabb** lehet.

**Vizsgán fontos kulcsszavak:**  
**[[tintasugaras nyomtató]]**, **tinta**, **fotó**, **kis volumen**

### 5.2 Lézer

**Rövid definíció:**  
A **[[lézernyomtató]]** **toner** (száraz por) és **elektrofotográfia**: **lézer** „**rajzol**” a **fényérzékeny** dobra, a toner **odaragad**, majd **papírra** kerül és **hővel fixálódik**.

**Működési elv:**  
- **Nagy sebesség**, **éles szöveg**, **nagy volumen** gazdaságosabb lehet.  
- **Iroda** és **sok fekete-fehér** dokumentum tipikus választása.

**Egyszerű példa:**  
Mint egy **pecsétnyomó gyár**: **egyforma** oldalak **gyorsan**, **egyenletes minőségben** — **nem** feltétlenül nyeri a **fotóversenyt**, de **számlát** **üt**, mint a **gép**.

**Vizsgán fontos kulcsszavak:**  
**[[lézernyomtató]]**, **toner**, **lézer**, **irodai nagy volumen**

**Vizsgán visszamondható mondat:** „**Tintasugaras** = **tinta + cseppek**, jó **fotó**; **lézer** = **toner + lézer a dobon**, jó **sok szöveg**.”

## 6. Telekommunikáció

### 6.1 Modem

**Rövid definíció:**  
A **[[modem]]** (*modulator–demodulator*) **digitális adatot** és a **vonalon** továbbítható **analóg jelalakot** váltogatja: **moduláció** (küldés) és **demoduláció** (vétele).

**Működési elv:**  
- A **szolgáltató hálózata** és a **otthoni eszköz** között **illesztő** szerep.  
- Ma gyakran **modem + router** egy dobozban; a lényeg: **a vonal fizikájához** kell **hangolni** a jelet.

**Egyszerű példa:**  
Mint a **fordító** két nyelv között: a **számítógép** „**biteket**” beszél, a **telefonvonal** „**hangszerű**” jelet — a **[[modem]]** **lefordítja** oda-vissza.

**Vizsgán fontos kulcsszavak:**  
**[[modem]]**, **moduláció**, **demoduláció**, **illesztés**

### 6.2 ADSL

**Rövid definíció:**  
Az **[[ADSL]]** (*Asymmetric Digital Subscriber Line*) **digitális** adatátvitel **réz** **telefonvezetéken**, a **beszéd** és az **internet** gyakran **külön frekvenciasávban**.

**Működési elv:**  
- **Aszimmetrikus**: a **letöltés** sávszélessége tipikusan **nagyobb**, mint a **feltöltés** — otthoni **böngészés**-profilhoz illeszkedett.  
- **Távolság** a központtól és a **vonal minősége** erősen befolyásolja a sebességet.

**Egyszerű példa:**  
Mint egy **kétirányú út**, ahol **lefelé** **több sáv** van, **felfelé** **kevesebb**: **film** lejön **gyorsan**, **nagy fájl** feltöltése **lassabb** lehet.

**Vizsgán fontos kulcsszavak:**  
**[[ADSL]]**, **réz telefonvonal**, **aszimmetrikus**, **szélessáv**

### 6.3 KábelTV internet

**Rövid definíció:**  
A **[[kábelTV internet]]** a **koaxiális** kábelhálózaton (eredetileg **TV**-terjesztésre épült infrastruktúra) nyújt **szélessávú** internet-hozzáférést.

**Működési elv:**  
- **Megosztott** közeg: egy **node** környezetében sok előfizető **uganazon** a **sávon** osztozik → **csúcsidőben** lassulhat.  
- **Letöltési** sebesség gyakran **nagyon jó** volt a régi telefonos DSL-hez képest.

**Egyszerű példa:**  
Mint egy **nagy közös vízvezeték**: **este mindenki zuhanyzik** → **nyomás** (sebesség) **csökken**; **éjjel** viszont **bőven folyik**.

**Vizsgán fontos kulcsszavak:**  
**[[kábelTV internet]]**, **koaxiális kábel**, **megosztott közeg**, **szélessáv**

## 7. Összefüggések

**Rövid definíció:**  
A **[[háttértár]]**, a **[[RAID]]**, a **nyomtatók** és a **távközlési** eszközök együtt adják a számítógép **I/O** és **kommunikációs** világát a **[[CPU]]** / **[[RAM]]** mellett.

**Működési elv:**  
- **Tárolás**: **[[SSD]]**/**[[HDD]]** + opcionálisan **[[RAID]]** a **szerver** / **munkaállomás** megbízhatóságáért.  
- **Kimenet**: **[[lézernyomtató]]** / **[[tintasugaras nyomtató]]** a **papír-alapú** eredmény.  
- **Külső világ**: **[[modem]]**, **[[ADSL]]**, **[[kábelTV internet]]** a **távoli** erőforrások felé.

**Egyszerű példa:**  
**Céges gép**: **[[SSD]]** + **[[HDD]]**, **[[RAID 1]]** a fontos lemezeknek, **[[lézernyomtató]]** a számlának, **[[kábelTV internet]]** vagy **újabb** optikai **szolgáltatás** a levélhez.

**Vizsgán fontos kulcsszavak:**  
**I/O**, **tárolási réteg**, **[[RAID]]**, **hálózati illesztés**, **kimeneti eszköz**

## + Vizsgán érdemes még megemlíteni

- **[[RAID]]** javíthat **lemezhiba** ellen, **nem** véd **véletlen törlés** vagy **titkosított zsarolás** ellen → **rendszeres backup** külön.  
- **[[SSD]]** **TRIM**, **írási** terhelés — vizsgán elég: „**SSD** más karbantartási mintázat, mint **[[HDD]]**”.  
- **Nyomtató**: **TCO** (patron/toner + megbízhatóság), nem csak a **vásárlási ár**.  
- **Hozzáférés fejlődése**: **telefonvonal** → **[[kábelTV internet]]** / **[[ADSL]]** → **üvegszál** (FTTH) — a tételhez a **három** megadott technológia a **klasszikus** kép.

## Rövid szóbeli összefoglaló

A **[[háttértár]]** **tartósan** tárol; **[[HDD]]** **mágneses és mechanikus**, **olcsó nagy tár**, **[[SSD]]** **flash**, **gyors**, **drágább/GB**. **[[optikai háttértár]]** és **[[szalagos háttértár]]** főleg **archívum/mentés**. A **[[RAID]]** több lemezt kapcsol: **[[RAID 0]]** **gyors, veszélyes**, **[[RAID 1]]** **biztonságos, drága kapacitásban**, **[[RAID 5]]** **paritás**, **[[RAID 10]]** **gyors + tükrözött**. **[[tintasugaras nyomtató]]** **tinta**, **[[lézernyomtató]]** **toner + lézer**. **[[modem]]** **jelátalakító**, **[[ADSL]]** **réz, aszimmetrikus**, **[[kábelTV internet]]** **koax, megosztott sáv**.

## Kulcsfogalmak

- [[háttértár]]
- [[RAM]]
- [[HDD]]
- [[SSD]]
- [[optikai háttértár]]
- [[szalagos háttértár]]
- [[RAID]]
- [[RAID 0]]
- [[RAID 1]]
- [[RAID 5]]
- [[RAID 10]]
- [[tintasugaras nyomtató]]
- [[lézernyomtató]]
- [[modem]]
- [[ADSL]]
- [[kábelTV internet]]

## Tipikus vizsgakérdések

1. **Mi a [[háttértár]] feladata?** — **Tartós**, **nem felejtő** tárolás; **[[RAM]]**-mal szemben **megmarad** áram nélkül is.  
2. **[[HDD]] vs [[SSD]] három szóban?** — **Mechanikus vs flash**; **lassabb random vs gyors**; **olcsóbb/GB vs drágább**.  
3. **Mi az [[optikai háttértár]] és a [[szalagos háttértár]] fő különbsége használatban?** — Optikai: **lézeres lemez**, archív/telepítő; szalag: **szekvenciális**, **backup**.  
4. **Mi a [[RAID]] célja?** — **Teljesítmény** és/vagy **hibatűrés** több lemezzel.  
5. **Miért nem backup a [[RAID]]?** — **Logikai** hibák, **törlés**, **malware** ellen **nem** véd; csak **lemez-szintű** redundancia/teljesítmény.  
6. **[[RAID 0]] vs [[RAID 1]]?** — **0**: **striping**, **gyors**, **nincs** védelem; **1**: **tükör**, **hibatűrőbb**, **fele** hasznos kapacitás (2 lemeznél).  
7. **[[RAID 5]] lényege?** — **Elosztott paritás**, **≥3 lemez**, **egy lemez** hiba javítható, írás **terheltebb**.  
8. **Tintasugaras vs lézer?** — **Tinta** vs **toner+lézer**; **fotó/otthon** vs **irodai tömeg**.  
9. **Mit csinál a [[modem]]?** — **Moduláció/demoduláció**: digitális adat **vonalra** illesztése és vissza.  
10. **[[ADSL]] aszimmetria?** — **Letöltés** tipikusan **gyorsabb**, mint **feltöltés**.  
11. **Miért lehet lassabb csúcsban a [[kábelTV internet]]?** — **Megosztott** koaxiális **sávszélesség** a szomszédokkal.

## Minimum, amit tudni kell

- **[[háttértár]]** vs **[[RAM]]** szerepe.  
- **[[HDD]]** / **[[SSD]]** / **[[optikai háttértár]]** / **[[szalagos háttértár]]** egy mondatos jellemzés + **táblázatos** összehasonlítás képessége.  
- **[[RAID]]** célja; **[[RAID 0]]** = **gyors, veszélyes**; **[[RAID 1]]** = **biztonságos, drága kapacitásban**; **[[RAID 5]]** paritás; **[[RAID 10]]** röviden.  
- **[[RAID]] nem backup.**  
- **[[tintasugaras nyomtató]]** vs **[[lézernyomtató]]**.  
- **[[modem]]**, **[[ADSL]]**, **[[kábelTV internet]]** alapötlete egy-egy visszamondható mondatban.
