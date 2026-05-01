# Számítógép-hálózatok – 25. tétel
## Internet alapelvek, rétegzés, architektúrák

---

## 1. Internet tervezési alapelvei

### 1.1 End-to-end elv
**Rövid definíció:**  
Az **[[end-to-end elv]]** szerint a komplex funkciók nagy része a végpontokban van, a hálózati mag pedig egyszerűbb marad.

**Működési elv:**  
- A hálózat főleg továbbít, nem „okoskodik” túl sokat.  
- Hibakezelés, megbízhatóság, alkalmazási logika jellemzően végponti feladat.  
- Ez segíti az internet skálázhatóságát.

**Egyszerű példa:**  
TCP szintjén a végpontok kezelik az újraküldést és sorrendezést, nem maga az alaphálózat.

**Vizsgán fontos kulcsszavak:**  
**[[end-to-end elv]]**, **végponti intelligencia**, **egyszerű hálózati mag**, **skálázhatóság**

---

### 1.2 Best-effort szolgáltatás
**Rövid definíció:**  
A **[[best-effort]]** hálózat megpróbálja kézbesíteni a csomagot, de nem garantál mindent.

**Működési elv:**  
- Nincs garantált kézbesítés és késleltetés.  
- Nincs garantált sorrend sem.  
- Egyszerűbb és általánosabb hálózati működést tesz lehetővé.

**Egyszerű példa:**  
IP szinten csomag elveszhet, ezért a TCP a végpontoknál pótolja az elveszett adatot.

**Vizsgán fontos kulcsszavak:**  
**[[best-effort]]**, **nincs garancia**, **csomagvesztés**, **végponti megbízhatóság**

---

### 1.3 Decentralizáció
**Rövid definíció:**  
Az internet decentralizált: nincs egyetlen központi vezérlőpont.

**Működési elv:**  
- Független hálózatok együttműködnek szabványos protokollokon keresztül.  
- Jobb skálázhatóság és hibatűrés érhető el.  
- Egy pont kiesése nem állítja le az egész rendszert.

**Egyszerű példa:**  
Egy szolgáltató hibája mellett más szolgáltatók hálózata tovább működik.

**Vizsgán fontos kulcsszavak:**  
**decentralizáció**, **autonóm rendszerek**, **robusztusság**, **skálázható internet**

---

## 2. Architekturális következmények

**Rövid definíció:**  
Az alapelvek közvetlenül meghatározzák az internet architektúráját.

**Működési elv:**  
- Egyszerű hálózati mag, intelligensebb végpontok.  
- Moduláris protokollrétegek és elosztott működés.  
- Könnyebb növekedés és jobb hibatűrés nagy méretben.

**Egyszerű példa:**  
Új alkalmazásprotokoll bevezethető anélkül, hogy az egész internetmagot át kellene tervezni.

**Vizsgán fontos kulcsszavak:**  
**hálózati architektúra**, **végponti komplexitás**, **hibatűrés**, **globális skálázás**

---

## 3. Rétegzés (Layering)

### 3.1 Fogalom
**Rövid definíció:**  
A **[[rétegzés]]** a hálózati feladatokat egymásra épülő szintekre bontja.

**Működési elv:**  
- Minden réteg jól körülhatárolt funkciót végez.  
- Egy réteg szolgáltatást nyújt a felette lévőnek.  
- A rétegek közti interfészek szabványosak.

**Egyszerű példa:**  
Az alkalmazás HTTP-t használ, ami TCP-re épül, ami IP-re épül.

**Vizsgán fontos kulcsszavak:**  
**[[rétegzés]]**, **szolgáltatási interfész**, **modularitás**, **protokollstack**

---

### 3.2 Előnyök
**Rövid definíció:**  
A rétegzett felépítés csökkenti a rendszer komplexitását.

**Működési elv:**  
- Könnyebb fejlesztés, tesztelés és hibaelhárítás.  
- Rétegek részben cserélhetők, ha interfész kompatibilis marad.  
- Jobb skálázhatóság és technológiai evolúció.

**Egyszerű példa:**  
A fizikai hálózat cserélhető Wi-Fi-ről Ethernetre, miközben a felsőbb protokollok változatlanok maradnak.

**Vizsgán fontos kulcsszavak:**  
**modularitás**, **cserélhetőség**, **rétegszétválasztás**, **karbantarthatóság**

---

## 4. OSI modell

### 4.1 Rétegek
**Rövid definíció:**  
Az **[[OSI modell]]** egy 7 rétegű referencia modell a hálózati kommunikáció leírására.

**Működési elv:**  
- Rétegek: fizikai, adatkapcsolati, hálózati, szállítási, viszony (session), megjelenítési (presentation), alkalmazási.  
- Oktatási és tervezési szemléleti keretként nagyon hasznos.  
- A valós internetprotokollok nem mindig követik szigorúan.

**Egyszerű példa:**  
Hálózati hibánál vizsgálhatjuk, mely OSI-rétegen lehet a probléma (pl. fizikai kábel, IP routing, alkalmazás).

**Vizsgán fontos kulcsszavak:**  
**[[OSI modell]]**, **7 réteg**, **referenciamodell**, **rétegszintű hibakeresés**

---

## 5. TCP/IP modell

### 5.1 Rétegek
**Rövid definíció:**  
A **[[TCP/IP modell]]** a gyakorlatban használt internetes protokollarchitektúra.

**Működési elv:**  
- Rétegek: hálózati interfész, internet, szállítási, alkalmazási.  
- Az internet alap protokolljai erre épülnek (IP, TCP, UDP, HTTP stb.).  
- Egyszerűbb, mint az OSI elméleti modell.

**Egyszerű példa:**  
Webböngészésnél HTTP alkalmazási szint, TCP szállítási, IP internet réteg.

**Vizsgán fontos kulcsszavak:**  
**[[TCP/IP modell]]**, **internet réteg**, **szállítási réteg**, **alkalmazási protokollok**

---

### 5.2 OSI vs TCP/IP
**Rövid definíció:**  
OSI inkább elméleti referencia, TCP/IP inkább működő gyakorlati architektúra.

**Működési elv:**  
- OSI 7 rétegű, TCP/IP tipikusan 4 rétegű szemlélet.  
- OSI oktatási és tervezési keret, TCP/IP valós internetes implementációs alap.  
- Réteghatárok részben eltérnek.

**Egyszerű példa:**  
Session/presentation OSI-rétegek funkciói TCP/IP-ben jellemzően az alkalmazási rétegbe olvadnak.

**Vizsgán fontos kulcsszavak:**  
**OSI vs TCP/IP**, **elmélet vs gyakorlat**, **rétegszám-különbség**, **protokollstack**

---

## 6. Hálózati síkok (planes)

### 6.1 Adatsík (data plane)
**Rövid definíció:**  
Az **[[adatsík]]** a csomagok tényleges továbbítását végzi.

**Működési elv:**  
- Router/switch eszközök gyors forwarding döntéseket hoznak.  
- Cél az alacsony késleltetés és nagy áteresztőképesség.

**Egyszerű példa:**  
Bejövő csomag célcíme alapján a router kimeneti interfészt választ.

**Vizsgán fontos kulcsszavak:**  
**[[adatsík]]**, **forwarding**, **csomagtovábbítás**, **gyors útvonal**

---

### 6.2 Vezérlési sík (control plane)
**Rövid definíció:**  
A **[[vezérlési sík]]** a hálózat működési logikáját és útvonalait határozza meg.

**Működési elv:**  
- Routing protokollok útvonalinformációt cserélnek.  
- A vezérlési döntésekből kerülnek bejegyzések az adatsík tábláiba.

**Egyszerű példa:**  
OSPF/BGP frissítés után a router új útvonalat kezd használni.

**Vizsgán fontos kulcsszavak:**  
**[[vezérlési sík]]**, **routing**, **útvonalválasztás**, **vezérlőlogika**

---

### 6.3 Menedzsment sík (management plane)
**Rövid definíció:**  
A **[[menedzsment sík]]** a hálózat felügyeletét és üzemeltetését támogatja.

**Működési elv:**  
- Monitoring, naplózás, riasztás, konfigurációkezelés.  
- Üzemeltetési eszközök és automatizálás kapcsolódik ide.

**Egyszerű példa:**  
SNMP/telemetria alapján a rendszer riaszt, ha egy link túlterhelt.

**Vizsgán fontos kulcsszavak:**  
**[[menedzsment sík]]**, **monitoring**, **konfiguráció**, **üzemeltetés**

---

## 7. Modern paradigmák

### 7.1 SDN (Software Defined Networking)
**Rövid definíció:**  
Az **[[SDN]]** a vezérlési sík és adatsík logikai szétválasztására épít.

**Működési elv:**  
- Központibb vezérlőlogika, programozható hálózati viselkedés.  
- Gyorsabb konfigurálhatóság és automatizálás.

**Egyszerű példa:**  
Egy vezérlő egyszerre több switch forwarding szabályait frissíti.

**Vizsgán fontos kulcsszavak:**  
**[[SDN]]**, **control-data plane szétválasztás**, **programozható hálózat**, **centralizált vezérlés**

---

### 7.2 NFV (Network Function Virtualization)
**Rövid definíció:**  
Az **[[NFV]]** hálózati funkciókat dedikált hardver helyett virtualizált szoftverként futtat.

**Működési elv:**  
- Funkciók (pl. tűzfal, load balancer) virtuális gépen vagy konténerben futnak.  
- Rugalmasabb skálázás és gyorsabb bevezetés.

**Egyszerű példa:**  
Új virtuális tűzfal példány indítható percek alatt fizikai appliance helyett.

**Vizsgán fontos kulcsszavak:**  
**[[NFV]]**, **virtualizált hálózati funkció**, **hardverfüggetlenség**, **rugalmas skálázás**

---

## 8. Összefüggések
**Rövid definíció:**  
Az internet alapelvei, rétegzése és modern hálózati paradigmái egymásra épülnek.

**Működési elv:**  
- Tervezési alapelvek adják az architektúra logikáját.  
- Rétegzés kezelhetővé teszi a komplexitást.  
- SDN/NFV a mai üzemeltetési és automatizálási igényekre válasz.

**Egyszerű példa:**  
Egy felhős környezetben SDN vezérli a forgalmat, NFV adja a virtuális hálózati funkciókat.

**Vizsgán fontos kulcsszavak:**  
**architektúra-folytonosság**, **rétegzett tervezés**, **modernizáció**, **automatizálás**

---

## + Vizsgán érdemes még megemlíteni
- **[[end-to-end elv]]** és „intelligens hálózat” kompromisszumai.  
- **[[best-effort]]** korlátait felsőbb rétegek kezelik.  
- **OSI vs TCP/IP** különbség említése mindig fontos.  
- **[[SDN]]** előnye: rugalmasság és gyors vezérelhetőség.  
- A skálázhatóság az internet legfontosabb rendszer-szintű célja.

---

## Rövid szóbeli összefoglaló
Az internet tervezésének alapja az end-to-end elv, a best-effort szolgáltatás és a decentralizált működés. Ezek miatt a hálózati mag egyszerű, a végpontok viszont összetettebbek. A komplexitás kezelésére rétegzett modell szolgál, elméletben az OSI, gyakorlatban pedig a TCP/IP architektúra terjedt el. A hálózati működés három síkra bontható: adatsík a csomagtovábbításra, vezérlési sík az útvonal-döntésekre, menedzsment sík az üzemeltetésre. Modern hálózatokban SDN és NFV segíti a programozhatóságot és a rugalmas skálázást. A fő üzenet, hogy az egyszerű alapelvek teszik lehetővé a globálisan skálázható internetet.

## Kulcsfogalmak
- [[end-to-end elv]]
- [[best-effort]]
- [[decentralizáció]]
- [[rétegzés]]
- [[OSI modell]]
- [[TCP/IP modell]]
- [[adatsík]]
- [[vezérlési sík]]
- [[menedzsment sík]]
- [[routing]]
- [[SDN]]
- [[NFV]]
- [[protokollstack]]
- [[skálázhatóság]]
- [[hibatűrés]]

## Tipikus vizsgakérdések
1. **Mit jelent az end-to-end elv?**  
   A komplex funkciók többsége a végpontokban van, a hálózatmag egyszerű marad.

2. **Mit jelent a best-effort szolgáltatás?**  
   Nincs garantált kézbesítés, sorrend vagy késleltetés az alap IP-szinten.

3. **Miért fontos a rétegzés a hálózatokban?**  
   Modularitást, cserélhetőséget és kezelhető komplexitást ad.

4. **Mi a különbség OSI és TCP/IP között?**  
   OSI inkább elméleti 7 rétegű modell, TCP/IP gyakorlati, kevesebb réteggel.

5. **Miben különbözik adatsík és vezérlési sík?**  
   Adatsík továbbít, vezérlési sík útvonalat és szabályokat számol.

6. **Mi az SDN lényege?**  
   A vezérlési sík logikai elkülönítése és programozható hálózati irányítás.

7. **Mire jó az NFV?**  
   Hálózati funkciók virtualizálása dedikált hardver helyett.

## Minimum, amit tudni kell
- End-to-end elv, best-effort, decentralizáció rövid lényege.  
- Miért lett egyszerű hálózati mag és komplex végponti működés.  
- Rétegzés fogalma és fő előnyei.  
- OSI és TCP/IP modell alapkülönbsége.  
- Adatsík, vezérlési sík, menedzsment sík szerepe.  
- SDN alapötlete (control/data plane szétválasztás).  
- NFV alapötlete (funkciók virtualizálása).  
- Skálázhatóság és hibatűrés szerepe internetes rendszerekben.
