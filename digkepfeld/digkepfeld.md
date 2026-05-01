# Digitális képfeldolgozás – 16. tétel
## Szűrés képtérben és frekvenciatérben

---

## 1. Alapfogalmak

**Rövid definíció:**  
A digitális kép pixelekből álló mátrix, ahol minden pixelhez egy intenzitás- vagy színérték tartozik. A szűrés célja, hogy a képből hasznos információt emeljünk ki, vagy zavaró hatásokat csökkentsünk.

**Működési elv:**  
- **[[digitális kép]]**: diszkrét mintavételezett vizuális jel.  
- **[[pixel]]**: a kép legkisebb eleme.  
- **[[intenzitás]]**: szürkeárnyalatos képnél egy számérték (pl. 0–255).  
- Színes képnél több csatorna van (pl. **[[RGB]]**).  
- A **[[zaj]]** olyan véletlen hiba, ami rontja a képet (szenzor, átvitel, tömörítés miatt).  
- Szűrés fő céljai: **zajcsökkentés**, **simítás**, **kiemelés**, **éldetektálás előkészítése**.

**Egyszerű példa:**  
Egy telefonos fotón a sötét részek szemcsések. Egy simító szűrővel csökkenthető a szemcse, de túl erős szűrésnél a részletek is elmosódnak.

**Vizsgán fontos kulcsszavak:**  
**[[digitális kép]]**, **[[pixel]]**, **[[intenzitás]]**, **[[RGB]]**, **[[zaj]]**, **zajcsökkentés**, **simítás**, **kiemelés**

---

## 2. Szűrés képtérben (spatial domain)

### 2.1 Alapelvek
**Rövid definíció:**  
A képtérbeli szűrésnél közvetlenül a pixelek értékét módosítjuk a környezetük alapján.

**Működési elv:**  
- A központi pixel új értékét a szomszédos pixelekből számítjuk.  
- Ehhez **[[kernel]]** vagy **[[maszk]]** kell (pl. 3x3-as súlytábla).  
- A leggyakoribb művelet a **[[konvolúció]]**.  
- **Lineáris** szűrés: összeadás-szorzás alapú (pl. átlagoló, Gauss).  
- **Nemlineáris** szűrés: nem írható le egyszerű lineáris kombinációval (pl. medián).

**Egyszerű példa:**  
Egy 3x3-as átlagoló maszk minden súlya 1/9, így a középső pixel az ablak átlagát kapja.

**Vizsgán fontos kulcsszavak:**  
**[[képtérbeli szűrés]]**, **[[kernel]]**, **[[maszk]]**, **[[konvolúció]]**, **lineáris szűrés**, **nemlineáris szűrés**

---

### 2.2 Átlagoló szűrő (mean filter)
**Rövid definíció:**  
Lineáris simító szűrő, amely a környezet átlagával helyettesíti a pixelt.

**Működési elv:**  
- Egyenlő súlyú kernel (pl. 3x3).  
- Jól csökkenti a kisebb amplitúdójú véletlen zajt.  
- Mellékhatás: az élek és finom részletek is gyengülnek.

**Egyszerű példa:**  
Szemcsés háttér esetén tisztább lesz a homogén terület, de a felirat kontúrja kevésbé éles.

**Vizsgán fontos kulcsszavak:**  
**[[átlagoló szűrő]]**, **lineáris szűrés**, **simítás**, **élmosás**

---

### 2.3 Gauss-simítás (Gaussian blur)
**Rövid definíció:**  
Lineáris simító szűrés, ahol a súlyok Gauss-eloszlást követnek.

**Működési elv:**  
- A középső pixel nagyobb súlyt kap, a távolabbiak kisebbet.  
- Ez természetesebb elmosást ad, mint az egyszerű átlagolás.  
- A simítás erősségét a **[[szórás]]** (σ) adja: nagyobb σ -> erősebb elmosás.

**Egyszerű példa:**  
Éldetektálás előtt Gauss-simítást alkalmazunk, hogy a zaj ne okozzon hamis éleket.

**Vizsgán fontos kulcsszavak:**  
**[[Gauss-szűrő]]**, **[[szórás]]**, **súlyozott átlag**, **zajcsökkentés**, **előszűrés**

---

### 2.4 Medián szűrő (median filter)
**Rövid definíció:**  
Nemlineáris szűrő, amely az ablak pixeleinek mediánját veszi.

**Működési elv:**  
- A szomszédság értékeit rendezzük, és a középső (medián) értéket választjuk.  
- Különösen jó **[[impulzuszaj]]** (salt-and-pepper) ellen.  
- Jobban megőrzi az éleket, mint az átlagoló szűrő.

**Egyszerű példa:**  
Ha egy fekete-fehér zajpont jelenik meg egy sima felületen, a medián szűrő gyakran eltünteti anélkül, hogy az éleket jelentősen elmossa.

**Vizsgán fontos kulcsszavak:**  
**[[medián szűrő]]**, **nemlineáris szűrés**, **[[impulzuszaj]]**, **élmegőrzés**

---

### 2.5 Min-max szűrés
**Rövid definíció:**  
Olyan nemlineáris szűrők, amelyek az ablak minimumát vagy maximumát adják vissza.

**Működési elv:**  
- **Minimum szűrő**: sötétíti a képet, eltávolíthat világos zajpontokat.  
- **Maximum szűrő**: világosít, eltávolíthat sötét zajpontokat.  
- Kapcsolódnak a **[[morfológiai műveletek]]** alapjaihoz (erózió, dilatáció szemlélet).

**Egyszerű példa:**  
Fehér pöttyök eltávolítására minimum szűrőt alkalmazunk, mert a lokális minimum csökkenti a kiugró világos értékeket.

**Vizsgán fontos kulcsszavak:**  
**[[minimum szűrő]]**, **[[maximum szűrő]]**, **[[morfológiai műveletek]]**, **struktúramódosítás**

---

## 3. Konvolúció

### 3.1 Fogalom
**Rövid definíció:**  
A konvolúció lineáris művelet, ahol egy kernel végigcsúszik a képen, és minden helyen súlyozott összeget számol.

**Működési elv:**  
- Kiválasztjuk a lokális ablakot.  
- Pixelenként összeszorozzuk a kernel értékeivel.  
- Összegezzük -> ez lesz az új pixelérték.  
- Sok klasszikus szűrő így írható le.

**Egyszerű példa:**  
Egy élkiemelő kernel pozitív és negatív súlyokkal nagy választ ad ott, ahol intenzitásugrás van.

**Vizsgán fontos kulcsszavak:**  
**[[konvolúció]]**, **kernelcsúsztatás**, **súlyozott összeg**, **lineáris operátor**

---

### 3.2 Tulajdonságok
**Rövid definíció:**  
A konvolúció fontos matematikai tulajdonságai miatt jól kezelhető és kombinálható.

**Működési elv:**  
- **Kommutativitás**: a kernel és jel felcserélhető.  
- **Asszociativitás**: több szűrő egymás után kombinálható.  
- **Linearitás**: az összegre és skálázásra külön-külön alkalmazható.

**Egyszerű példa:**  
Két egymást követő lineáris simító szűrés összevonható egyetlen ekvivalens kernellé.

**Vizsgán fontos kulcsszavak:**  
**kommutativitás**, **asszociativitás**, **linearitás**, **szűrők kombinálása**

---

## 4. Szűrés frekvenciatérben (frequency domain)

### 4.1 Alapelvek
**Rövid definíció:**  
A képet frekvenciaösszetevőkre bontjuk, és ezek amplitúdóját módosítjuk.

**Működési elv:**  
- **[[Fourier-transzformáció]]**: kép -> frekvenciatér.  
- Alacsony frekvencia: lassan változó területek (háttér, sima régiók).  
- Magas frekvencia: gyors változások (élek, textúra, finom részletek).  
- Szűrés után inverz transzformációval visszamegyünk képtérbe.

**Egyszerű példa:**  
Ha a magas frekvenciákat gyengítjük, a kép simább lesz; ha erősítjük, élesebbnek tűnik.

**Vizsgán fontos kulcsszavak:**  
**[[frekvenciatér]]**, **[[Fourier-transzformáció]]**, **alacsony frekvencia**, **magas frekvencia**, **inverz transzformáció**

---

### 4.2 Konvolúciós tétel
**Rövid definíció:**  
A képtérbeli konvolúció megfelel a frekvenciatérbeli szorzásnak.

**Működési elv:**  
- Képtér: konvolúció számításigényes lehet nagy kernelnél.  
- Frekvenciatér: transzformálás után elemenkénti szorzás történik.  
- Ezt gyorsítja az **[[FFT]]**.

**Egyszerű példa:**  
Nagy méretű elmosó kernel esetén gyakran gyorsabb FFT-vel számolni, mint képtérben közvetlenül konvolválni.

**Vizsgán fontos kulcsszavak:**  
**[[konvolúciós tétel]]**, **[[FFT]]**, **képtérbeli konvolúció**, **frekvenciatérbeli szorzás**

---

## 5. Frekvencia alapú szűrés

### 5.1 Aluláteresztő szűrés (low-pass)
**Rövid definíció:**  
Az alacsony frekvenciákat megtartja, a magasakat csökkenti.

**Működési elv:**  
- Zajcsökkentésre és simításra használjuk.  
- Mellékhatás: részletvesztés, élek lágyulása.

**Egyszerű példa:**  
Erősen zajos képen aluláteresztéssel csökken a szemcsézettség, de a finom textúra is gyengül.

**Vizsgán fontos kulcsszavak:**  
**[[aluláteresztő szűrés]]**, **low-pass**, **zajcsökkentés**, **elmosás**

---

### 5.2 Felüláteresztő szűrés (high-pass)
**Rövid definíció:**  
A magas frekvenciákat tartja meg, az alacsonyakat csökkenti.

**Működési elv:**  
- Élek, részletek, kontúrok kiemelésére jó.  
- Könnyen felerősítheti a zajt is, ezért gyakran óvatosan kell használni.

**Egyszerű példa:**  
Egy enyhén elmosott képen a high-pass szűrés javíthatja az élek láthatóságát.

**Vizsgán fontos kulcsszavak:**  
**[[felüláteresztő szűrés]]**, **high-pass**, **élkiemelés**, **részleterősítés**

---

### 5.3 Frekvenciamaszkok
**Rövid definíció:**  
A frekvenciatérben szűrőfüggvényekkel (maszkokkal) szabályozzuk, mely frekvenciák maradjanak meg.

**Működési elv:**  
- **Ideális szűrő**: éles levágás, de csengési jelenséget okozhat.  
- **Gauss szűrő**: sima átmenet, kevesebb műtermék.  
- **Butterworth szűrő**: átmenet meredeksége renddel szabályozható.  
- Maszkolás után inverz Fourier-transzformáció következik.

**Egyszerű példa:**  
Ha nem akarunk erős csengést, ideális helyett Gauss vagy alacsony rendű Butterworth szűrőt választunk.

**Vizsgán fontos kulcsszavak:**  
**[[frekvenciamaszk]]**, **ideális szűrő**, **[[Gauss-szűrő]]**, **[[Butterworth-szűrő]]**, **csengés**

---

## 6. Képtér vs frekvenciatér

### 6.1 Összehasonlítás
**Rövid definíció:**  
Mindkét megközelítés ugyanazt a célt szolgálja, de más szemléletet és számítási előnyt ad.

**Működési elv:**  
- **Képtér**: intuitív, lokális, kis kernelnél egyszerű és gyors.  
- **Frekvenciatér**: globális szemlélet, nagy kernelnél FFT miatt hatékony lehet.  
- A választás feladatfüggő: zajtípus, részletigény, számítási költség.

**Egyszerű példa:**  
3x3-as előszűréshez képtér célszerű, de nagyon nagy elmosó kernelhez frekvenciatér gyakran jobb.

**Vizsgán fontos kulcsszavak:**  
**[[képtér]]**, **[[frekvenciatér]]**, **lokális művelet**, **globális művelet**, **hatékonyság**

---

## + Vizsgán érdemes még megemlíteni
- **[[FFT]]** (Fast Fourier Transform): gyors Fourier-számítás.
- Zajtípusok: **[[Gauss-zaj]]**, **[[impulzuszaj]]**.
- **Élmegőrzés vs simítás** kompromisszum.
- Gyakorlati alkalmazások: orvosi képalkotás, ipari ellenőrzés, AI előfeldolgozás.

---

## Rövid szóbeli összefoglaló
A digitális képszűrés célja, hogy a képet javítsuk: csökkentsük a zajt, és kiemeljük a fontos részleteket. Képtérben közvetlenül a pixelekkel dolgozunk, általában kernel segítségével, tipikus művelet a konvolúció. Itt az átlagoló és Gauss-szűrő simít, míg a medián különösen jó impulzuszaj ellen, és jobban megőrzi az éleket. Frekvenciatérben Fourier-transzformációval szétválasztjuk az alacsony és magas frekvenciákat: az aluláteresztő szűrés simít, a felüláteresztő éleket emel ki. A konvolúciós tétel miatt nagy szűrőknél FFT-vel gyakran hatékonyabb a frekvenciatérbeli megoldás. Vizsgán fontos hangsúlyozni, hogy mindig kompromisszum van a zajcsökkentés és a részletmegőrzés között.

## Kulcsfogalmak
- [[digitális kép]]
- [[pixel]]
- [[intenzitás]]
- [[zaj]]
- [[konvolúció]]
- [[kernel]]
- [[átlagoló szűrő]]
- [[Gauss-szűrő]]
- [[medián szűrő]]
- [[impulzuszaj]]
- [[Fourier-transzformáció]]
- [[FFT]]
- [[aluláteresztő szűrés]]
- [[felüláteresztő szűrés]]
- [[Butterworth-szűrő]]

## Tipikus vizsgakérdések
1. **Mi a különbség a képtérbeli és frekvenciatérbeli szűrés között?**  
   Képtérben pixeleket módosítunk lokálisan, frekvenciatérben frekvenciaösszetevőket szabályozunk globálisan.

2. **Miért használunk Gauss-szűrőt átlagoló helyett?**  
   Természetesebb simítást ad, mert a közeli pixeleket jobban súlyozza.

3. **Mikor előnyös a mediánszűrő?**  
   Impulzuszajnál, mert jól eltávolítja a kiugró zajpontokat és közben jobban tartja az éleket.

4. **Mit mond ki a konvolúciós tétel?**  
   A képtérbeli konvolúció a frekvenciatérben szorzásnak felel meg.

5. **Mire jó az aluláteresztő szűrés?**  
   Zajcsökkentésre és simításra, de csökkenti a részleteket.

6. **Mire jó a felüláteresztő szűrés?**  
   Élek és finom részletek kiemelésére, viszont zajt is erősíthet.

7. **Miért fontos az FFT?**  
   Jelentősen gyorsítja a Fourier-alapú szűrések számítását.

## Minimum, amit tudni kell
- A szűrés célja: **zajcsökkentés** és/vagy **részletkiemelés**.  
- Képtérben a fő művelet a **[[konvolúció]]** kernel segítségével.  
- Az átlagoló és a Gauss szűrő simít, de részletet veszítünk.  
- A **[[medián szűrő]]** nemlineáris, és jó **[[impulzuszaj]]** ellen.  
- Frekvenciatérben a kép Fourier-transzformáltját szűrjük.  
- **Aluláteresztő**: simít; **felüláteresztő**: élt emel ki.  
- A konvolúciós tétel összeköti a képtér- és frekvenciatérbeli megközelítést.  
- A gyakorlatban mindig kompromisszum van a simítás és élmegőrzés között.
