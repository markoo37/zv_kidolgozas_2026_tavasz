# Számítógép architektúra – 28. tétel
## Perifériák: háttértárak, RAID, nyomtatók, hálózati eszközök

---

## 1. Háttértárak

### 1.1 Feladat
**Rövid definíció:**  
A **[[háttértár]]** feladata az adatok tartós, nem felejtő tárolása.

**Működési elv:**  
- Kikapcsolás után is megőrzi az adatokat.  
- Programok, dokumentumok, mentések itt tárolódnak hosszú távon.  
- A fő különbségek: sebesség, kapacitás, ár, megbízhatóság.

**Egyszerű példa:**  
Az operációs rendszer és a felhasználói fájlok HDD-n vagy SSD-n helyezkednek el.

**Vizsgán fontos kulcsszavak:**  
**[[háttértár]]**, **tartós tárolás**, **nem felejtő memória**, **kapacitás**

---

## 2. Háttértár típusok

### 2.1 Mágneses háttértárak (HDD)
**Rövid definíció:**  
A **[[HDD]]** forgó mágneslemezes háttértár.

**Működési elv:**  
- Mechanikus fej olvas/ír a forgó lemezen.  
- Nagy kapacitás kedvező áron.  
- Hátránya a magasabb késleltetés és kisebb mechanikai ellenállás.

**Egyszerű példa:**  
Nagy mennyiségű médiafájl tárolására gyakran HDD-t választanak költséghatékonyság miatt.

**Vizsgán fontos kulcsszavak:**  
**[[HDD]]**, **mágneses tárolás**, **forgó lemez**, **kapacitás/ár arány**

---

### 2.2 Flash memória (SSD)
**Rövid definíció:**  
Az **[[SSD]]** félvezető alapú háttértár, mozgó alkatrész nélkül.

**Működési elv:**  
- Flash cellákban tárol adatot.  
- Gyorsabb random hozzáférés és kisebb késleltetés, mint HDD-nél.  
- Ár/GB általában magasabb.

**Egyszerű példa:**  
Rendszermeghajtónak SSD-t használva gyorsabban indul az operációs rendszer.

**Vizsgán fontos kulcsszavak:**  
**[[SSD]]**, **flash memória**, **alacsony késleltetés**, **gyors elérés**

---

### 2.3 Optikai háttértárak
**Rövid definíció:**  
Az optikai háttértárak lézeres elven működő adathordozók (CD, DVD, Blu-ray).

**Működési elv:**  
- A lemezen lévő mintázatot lézer olvassa ki.  
- Jó lehet hosszabb távú, ritkán módosított adatokra.  
- Sebességük és kapacitásuk ma sokszor korlátozó tényező.

**Egyszerű példa:**  
Archivált fényképek vagy telepítőlemezek tárolása Blu-ray hordozón.

**Vizsgán fontos kulcsszavak:**  
**optikai háttértár**, **CD/DVD/Blu-ray**, **lézeres olvasás**, **archiválás**

---

### 2.4 Szalagos háttértárak
**Rövid definíció:**  
A szalagos tárolás nagy kapacitású, főleg mentési és archiválási célra használt technológia.

**Működési elv:**  
- Szekvenciális elérés: az adatokhoz sorrendben jutunk hozzá.  
- Nagyon jó költség/kapacitás arány hosszú távú tárolásra.  
- Random elérésre nem ideális.

**Egyszerű példa:**  
Nagyvállalati napi mentések szalagos könyvtárba kerülnek.

**Vizsgán fontos kulcsszavak:**  
**szalagos háttértár**, **szekvenciális elérés**, **backup**, **archiválás**

---

## 3. Összehasonlítás

**Rövid definíció:**  
A háttértár típusok különböző kompromisszumokat adnak sebesség, ár és célfelhasználás szerint.

**Működési elv:**  
- **HDD**: olcsóbb nagy kapacitás, de lassabb.  
- **SSD**: gyors és alacsony késleltetés, de drágább/GB.  
- **Optikai**: jó archiválásra, de lassabb és kevésbé rugalmas.  
- **Szalag**: backupra kiváló, de nem random hozzáférésű.

**Egyszerű példa:**  
Sok rendszer kombinálja: OS SSD-n, nagy adattárolás HDD-n, mentés szalagon.

**Vizsgán fontos kulcsszavak:**  
**sebesség-kapacitás-ár kompromisszum**, **random vs szekvenciális elérés**, **rétegezett tárolás**

---

## 4. RAID (Redundant Array of Independent Disks)

### 4.1 Cél
**Rövid definíció:**  
A **[[RAID]]** több lemez összekapcsolása teljesítmény- és/vagy megbízhatósági célból.

**Működési elv:**  
- Adatelosztás (striping), tükrözés (mirroring), paritás kombinálható.  
- Néhány szint gyorsít, mások hibatűrést adnak, vagy mindkettőt.  
- Fontos: RAID nem egyenlő mentéssel.

**Egyszerű példa:**  
Szerverben RAID 1-et használva egy lemezhiba esetén is működhet a rendszer.

**Vizsgán fontos kulcsszavak:**  
**[[RAID]]**, **redundancia**, **hibatűrés**, **teljesítmény**, **nem backup**

---

### 4.2 Alap szintek

#### RAID 0
**Rövid definíció:**  
A **RAID 0** adatelosztást használ redundancia nélkül.

**Működési elv:**  
- Az adat blokkokra bontva több lemezre kerül.  
- Nő az írás/olvasás sebessége.  
- Egy lemezhiba az egész tömb adatvesztését okozhatja.

**Egyszerű példa:**  
Videószerkesztés ideiglenes munkaterületre használható, ahol a sebesség a fő szempont.

**Vizsgán fontos kulcsszavak:**  
**RAID 0**, **striping**, **gyorsaság**, **nincs hibatűrés**

---

#### RAID 1
**Rövid definíció:**  
A **RAID 1** tükrözést alkalmaz: ugyanaz az adat több lemezen is megvan.

**Működési elv:**  
- Minden írás minden tükörlemezre megtörténik.  
- Jó hibatűrés egy lemez kiesése esetén.  
- Hasznos kapacitás csökken, mert a tükör helyet foglal.

**Egyszerű példa:**  
Kisvállalati szerveren RAID 1 gyakori az üzembiztonság növelésére.

**Vizsgán fontos kulcsszavak:**  
**RAID 1**, **mirroring**, **hibatűrés**, **kapacitásvesztés**

---

#### RAID 5
**Rövid definíció:**  
A **RAID 5** elosztott paritást használ, így teljesítmény és adatbiztonság között kompromisszumot ad.

**Működési elv:**  
- Legalább 3 lemez szükséges.  
- Egy lemezhiba túlélhető paritás segítségével.  
- Írási műveletek paritásszámítás miatt lassulhatnak.

**Egyszerű példa:**  
Fájlszervereknél gyakori választás, ha kell kapacitás és hibatűrés is.

**Vizsgán fontos kulcsszavak:**  
**RAID 5**, **paritás**, **kompromisszum**, **egy lemezhiba tolerálás**

---

#### RAID 10 (említés)
**Rövid definíció:**  
A **RAID 10** a RAID 1 és RAID 0 kombinációja (tükrözött stripe).

**Működési elv:**  
- Jó teljesítmény és jó hibatűrés együtt.  
- Több lemez kell, ezért drágább megoldás.

**Egyszerű példa:**  
Nagy terhelésű adatbázis-szervernél gyakori választás.

**Vizsgán fontos kulcsszavak:**  
**RAID 10**, **mirror + stripe**, **nagy teljesítmény**, **nagyobb költség**

---

## 5. Nyomtatók

### 5.1 Tintasugaras (inkjet)
**Rövid definíció:**  
A **[[tintasugaras nyomtató]]** folyékony tintacseppeket juttat a papírra.

**Működési elv:**  
- Finom cseppképzés miatt jó képminőséget adhat.  
- Kis mennyiségű, vegyes nyomtatásra gyakori.  
- Nagy volumenben lassabb és oldalanként drágább lehet.

**Egyszerű példa:**  
Otthoni fotónyomtatásra tintasugaras eszköz jó választás.

**Vizsgán fontos kulcsszavak:**  
**[[tintasugaras nyomtató]]**, **folyékony tinta**, **jó képminőség**, **kisebb sebesség**

---

### 5.2 Lézernyomtató
**Rövid definíció:**  
A **[[lézernyomtató]]** tonerport és elektrofotográfiai elvet használ.

**Működési elv:**  
- Lézerrel „rajzolja” a képet a dobra, toner tapad rá, majd papírra kerül és fixálódik.  
- Gyors, nagy mennyiségű szöveges nyomtatásra kiváló.  
- Irodai környezetben gyakori.

**Egyszerű példa:**  
Egy irodában napi több száz oldal nyomtatására lézernyomtató hatékonyabb.

**Vizsgán fontos kulcsszavak:**  
**[[lézernyomtató]]**, **toner**, **nagy sebesség**, **irodai felhasználás**

---

## 6. Telekommunikációs berendezések

### 6.1 Modem
**Rövid definíció:**  
A **[[modem]]** digitális és analóg jelek közti átalakítást végez.

**Működési elv:**  
- Moduláció/demoduláció folyamatával továbbítható adat hagyományos vonalon is.  
- Több technológiában is alap komponens lehet.

**Egyszerű példa:**  
Régi telefonvonalas internetkapcsolat modem nélkül nem működött.

**Vizsgán fontos kulcsszavak:**  
**[[modem]]**, **moduláció**, **demoduláció**, **digitális-analóg átalakítás**

---

### 6.2 ADSL
**Rövid definíció:**  
Az **[[ADSL]]** szélessávú adatátviteli technológia réz telefonvonalon.

**Működési elv:**  
- Aszimmetrikus: letöltés jellemzően gyorsabb, mint feltöltés.  
- A hang és adat külön frekvenciasávban halad.

**Egyszerű példa:**  
Otthoni internetszolgáltatásnál régebben gyakori volt az ADSL modemes kapcsolat.

**Vizsgán fontos kulcsszavak:**  
**[[ADSL]]**, **telefonvonal**, **aszimmetrikus sávszélesség**, **szélessáv**

---

### 6.3 KábelTV-s internet
**Rövid definíció:**  
A kábeltelevíziós hálózaton nyújtott internet koaxiális infrastruktúrát használ.

**Működési elv:**  
- Nagyobb sávszélességet tud adni, mint sok régebbi telefonvonalas megoldás.  
- Megosztott közeg, ezért terhelésfüggő teljesítmény előfordulhat.

**Egyszerű példa:**  
Lakótelepi szolgáltatásoknál elterjedt a koaxiális kábelre épülő internet.

**Vizsgán fontos kulcsszavak:**  
**kábelnet**, **koaxiális kábel**, **sávszélesség**, **megosztott közeg**

---

## 7. Összefüggések
**Rövid definíció:**  
A perifériák és háttértárak együtt biztosítják a rendszer adatkezelését és külső kapcsolatait.

**Működési elv:**  
- Háttértárak az adatok tartós megőrzését adják.  
- RAID javíthatja a rendelkezésre állást és/vagy teljesítményt.  
- Nyomtatók és hálózati eszközök az I/O és kommunikáció részei.

**Egyszerű példa:**  
Egy céges szerver SSD + RAID tömböt használ, a felhasználók hálózaton érik el, és központi nyomtatóra küldenek dokumentumot.

**Vizsgán fontos kulcsszavak:**  
**I/O eszköz**, **adatmegőrzés**, **rendelkezésre állás**, **kommunikáció**

---

## + Vizsgán érdemes még megemlíteni
- **[[SSD]] vs [[HDD]]**: késleltetés, mechanika, ár/kapacitás különbség.  
- **[[RAID]] célja**: redundancia/teljesítmény, de **nem helyettesíti a backupot**.  
- Nyomtatóknál használati profil alapján választunk (fotó vs nagy irodai mennyiség).  
- Hálózati hozzáférések fejlődése: telefonvonal -> kábel -> modern optikai rendszerek.

---

## Rövid szóbeli összefoglaló
A perifériák közül a háttértárak a tartós adatmegőrzésért felelnek. A HDD mágneses, olcsó és nagy kapacitású, de lassabb, míg az SSD gyorsabb és kisebb késleltetésű, viszont drágább. Optikai és szalagos tárolás főleg archiválásra jellemző. A RAID több lemezből álló rendszer, amely teljesítményt és/vagy hibatűrést adhat: RAID 0 gyors, de nem biztonságos, RAID 1 tükröz, RAID 5 paritással jó kompromisszum, RAID 10 kombinált megoldás. A nyomtatóknál a tintasugaras jó minőségű, a lézernyomtató gyors és nagy mennyiségre ideális. Hálózati oldalon modem, ADSL és kábelnet különböző adatátviteli technológiákat képviselnek. Fontos, hogy a megfelelő periféria kiválasztása mindig feladattól és költségkerettől függ.

## Kulcsfogalmak
- [[háttértár]]
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
- [[kábelnet]]

## Tipikus vizsgakérdések
1. **Mi a háttértárak fő feladata?**  
   Az adatok tartós, nem felejtő tárolása.

2. **Mi a legfontosabb különbség HDD és SSD között?**  
   HDD mechanikus és lassabb, SSD félvezetős és gyorsabb, de drágább/GB.

3. **Mi a RAID célja?**  
   Teljesítmény növelése és/vagy hibatűrés javítása több lemez használatával.

4. **Miért nem backup a RAID?**  
   Mert hardverhibát kezelhet, de nem véd például törlés, zsarolóvírus vagy logikai hiba ellen.

5. **Miben különbözik RAID 0 és RAID 1?**  
   RAID 0 gyors, de nincs redundancia; RAID 1 tükrözéssel hibatűrőbb.

6. **Mikor célszerű tintasugaras és mikor lézernyomtató?**  
   Tintasugaras: jobb fotó/otthoni vegyes használat; lézer: nagy mennyiségű irodai nyomtatás.

7. **Mit jelent az ADSL aszimmetrikussága?**  
   A letöltési sebesség jellemzően nagyobb, mint a feltöltési.

## Minimum, amit tudni kell
- A háttértár fogalma és fő típusai (HDD, SSD, optikai, szalag).  
- HDD és SSD alap különbsége sebességben, mechanikában, árban.  
- RAID fogalma és fő célja (teljesítmény +/vagy redundancia).  
- RAID 0, 1, 5 alapötlete.  
- A tétel kulcsmondata: RAID nem helyettesíti a biztonsági mentést.  
- Tintasugaras és lézernyomtató fő felhasználási különbsége.  
- Modem alapfunkciója (digitális-analóg átalakítás).  
- ADSL és kábelnet rövid jellemzése.
