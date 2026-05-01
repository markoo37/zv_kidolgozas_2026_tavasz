# Számítógép-hálózatok – 26. tétel
## Hálózati biztonság alapjai

---

## 1. Alapfogalmak

### 1.1 Információbiztonság célja
**Rövid definíció:**  
Az **[[információbiztonság]]** célja az adatok és rendszerek védelme a jogosulatlan hozzáférés, módosítás és kiesés ellen.

**Működési elv:**  
- Technikai és szervezeti kontrollok együtt működnek.  
- Nem csak titkosításról szól, hanem teljes kockázatkezelési szemléletről.  
- Cél a biztonság és használhatóság egyensúlya.

**Egyszerű példa:**  
Bejelentkezés + jogosultságkezelés + naplózás együtt ad védelmet egy vállalati rendszerben.

**Vizsgán fontos kulcsszavak:**  
**[[információbiztonság]]**, **adatvédelem**, **jogosultságkezelés**, **kockázatkezelés**

---

## 2. CIA-triász

### 2.1 Confidentiality (bizalmasság)
**Rövid definíció:**  
A **[[bizalmasság]]** azt jelenti, hogy csak jogosult fél férhet hozzá az adathoz.

**Működési elv:**  
- Hozzáférés-szabályozás és titkosítás védi az információt.  
- Kommunikációban és tárolásban is biztosítható.

**Egyszerű példa:**  
HTTPS titkosított csatornán küldi a jelszót, így harmadik fél nehezen olvassa el.

**Vizsgán fontos kulcsszavak:**  
**[[bizalmasság]]**, **titkosítás**, **hozzáférés-kontroll**, **jogosultság**

---

### 2.2 Integrity (sértetlenség)
**Rövid definíció:**  
A **[[sértetlenség]]** biztosítja, hogy az adat jogosulatlanul ne módosuljon.

**Működési elv:**  
- Hash, MAC, digitális aláírás jelezheti a módosítást.  
- Fontos mind adatátvitelkor, mind tároláskor.

**Egyszerű példa:**  
Letöltött fájl hash-e eltér a hivatalos értéktől -> a fájl sérült vagy manipulált.

**Vizsgán fontos kulcsszavak:**  
**[[sértetlenség]]**, **hash ellenőrzés**, **manipuláció detektálás**, **adatkonzisztencia**

---

### 2.3 Availability (rendelkezésre állás)
**Rövid definíció:**  
A **[[rendelkezésre állás]]** azt jelenti, hogy a szolgáltatás akkor is elérhető, amikor szükség van rá.

**Működési elv:**  
- Redundancia, terheléselosztás, monitoring segíti.  
- DoS/DDoS támadások ellen védekezni kell.

**Egyszerű példa:**  
Több szerveres felállásnál egy gép kiesésekor a szolgáltatás tovább él.

**Vizsgán fontos kulcsszavak:**  
**[[rendelkezésre állás]]**, **redundancia**, **DoS/DDoS**, **üzemfolytonosság**

---

## 3. Kerckhoffs-elv
**Rövid definíció:**  
A **[[Kerckhoffs-elv]]** szerint a kriptorendszer biztonsága a kulcs titkosságán múljon, ne az algoritmus titkosságán.

**Működési elv:**  
- Algoritmus lehet nyilvános és auditálható.  
- A támadó ismerheti a módszert, de kulcs nélkül ne tudja feltörni.

**Egyszerű példa:**  
Az AES algoritmus publikus, mégis biztonságos a megfelelő kulccsal.

**Vizsgán fontos kulcsszavak:**  
**[[Kerckhoffs-elv]]**, **kulcstitkosság**, **nyílt algoritmus**, **kriptográfiai biztonság**

---

## 4. Shannon-féle tökéletes titkosság
**Rövid definíció:**  
A **[[tökéletes titkosság]]** esetén a titkosított szöveg nem ad információt az eredeti üzenetről.

**Működési elv:**  
- Klasszikus példa az **[[one-time pad]]**.  
- Kulcs legalább olyan hosszú, mint az üzenet, valóban véletlen és csak egyszer használható.  
- Elméletileg erős, gyakorlatban nehezen kezelhető.

**Egyszerű példa:**  
Eldobható egyszeri kulccsal XOR-olt üzenet elméletileg feltörhetetlen kulcs nélkül.

**Vizsgán fontos kulcsszavak:**  
**[[tökéletes titkosság]]**, **[[one-time pad]]**, **egyszer használatos kulcs**, **információelméleti biztonság**

---

## 5. Kriptográfia

### 5.1 Szimmetrikus titkosítás
**Rövid definíció:**  
A **[[szimmetrikus titkosítás]]** ugyanazt a kulcsot használja titkosításhoz és visszafejtéshez.

**Működési elv:**  
- Nagyon gyors, nagy adatmennyiségre jól használható.  
- Fő kihívás a kulcs biztonságos cseréje.

**Egyszerű példa:**  
VPN adatforgalom titkosítása gyakran szimmetrikus algoritmussal történik a sebesség miatt.

**Vizsgán fontos kulcsszavak:**  
**[[szimmetrikus titkosítás]]**, **közös kulcs**, **gyorsaság**, **kulcselosztási probléma**

---

### 5.2 Aszimmetrikus titkosítás
**Rövid definíció:**  
Az **[[aszimmetrikus titkosítás]]** kulcspárt használ: nyilvános és privát kulcsot.

**Működési elv:**  
- Nyilvános kulccsal titkosíthatunk, priváttal lehet visszafejteni (vagy fordítva aláírásnál).  
- Lassabb, mint a szimmetrikus módszerek, de kulcscserére kiváló.

**Egyszerű példa:**  
HTTPS kézfogásban aszimmetrikus módszerrel indul a biztonságos kulcsegyeztetés.

**Vizsgán fontos kulcsszavak:**  
**[[aszimmetrikus titkosítás]]**, **publikus kulcs**, **privát kulcs**, **kulcscsere**

---

### 5.3 Összehasonlítás
**Rövid definíció:**  
A két titkosítási mód eltérő erősségeket ad, ezért gyakran kombinálják őket.

**Működési elv:**  
- Szimmetrikus: gyors adatcsatornához.  
- Aszimmetrikus: kulcscsere és hitelesség biztosítására.  
- Hibrid modellek adják a gyakorlati megoldást.

**Egyszerű példa:**  
TLS-ben aszimmetrikus kézfogás után szimmetrikus munkakulcs védi a forgalmat.

**Vizsgán fontos kulcsszavak:**  
**hibrid kriptográfia**, **sebesség vs kulcskezelés**, **TLS modell**

---

## 6. Digitális aláírás

### 6.1 Fogalom
**Rövid definíció:**  
A **[[digitális aláírás]]** hitelességet és sértetlenséget biztosít.

**Működési elv:**  
- Bizonyítja, hogy ki írta alá az adatot.  
- Jelzi, ha az adat az aláírás óta módosult.  
- Nem titkosítás, hanem hitelesítési mechanizmus.

**Egyszerű példa:**  
Szoftverfrissítés aláírás alapján ellenőrizhető, hogy valódi gyártótól jött-e.

**Vizsgán fontos kulcsszavak:**  
**[[digitális aláírás]]**, **hitelesség**, **sértetlenség**, **nem-letagadhatóság**

---

### 6.2 Működés
**Rövid definíció:**  
Az aláírás folyamata hash és aszimmetrikus kulcsművelet kombinációja.

**Működési elv:**  
- Üzenetről hash készül.  
- Hash privát kulccsal aláírásra kerül.  
- Ellenőrzés publikus kulccsal történik.

**Egyszerű példa:**  
Ha az ellenőrzött hash eltér az újraszámolttól, az üzenet sérült vagy hamis.

**Vizsgán fontos kulcsszavak:**  
**hash + aláírás**, **privát kulcsos aláírás**, **publikus kulcsos verifikáció**

---

## 7. Hash függvények

### 7.1 Tulajdonságok
**Rövid definíció:**  
A **[[hash függvény]]** tetszőleges hosszú bemenetből fix hosszúságú lenyomatot készít.

**Működési elv:**  
- Egyirányú működés: hash-ből nehéz visszaállítani a bemenetet.  
- Cél a jó ütközésállóság.  
- Integritás-ellenőrzés alapja.

**Egyszerű példa:**  
Két azonos fájl hash-e egyezik, módosítás után hash is megváltozik.

**Vizsgán fontos kulcsszavak:**  
**[[hash függvény]]**, **fix hosszúság**, **egyirányúság**, **ütközésállóság**

---

### 7.2 Felhasználás
**Rövid definíció:**  
A hash gyakori biztonsági építőelem jelszókezelésben és integritásvédelemben.

**Működési elv:**  
- Jelszó tárolásnál hash (+ sózás) formában tárolunk.  
- Fájlok és üzenetek sértetlensége hash összehasonlítással ellenőrizhető.

**Egyszerű példa:**  
Regisztrációkor a rendszer nem a jelszót, hanem annak sózott hash-ét menti.

**Vizsgán fontos kulcsszavak:**  
**jelszóhash**, **sózás**, **integritás ellenőrzés**, **lenyomat**

---

## 8. Védelmi paradigmák evolúciója

### 8.1 Perimeter (hagyományos modell)
**Rövid definíció:**  
A hagyományos **[[perimeter security]]** modell a hálózati határ védelmére épít.

**Működési elv:**  
- Külső-belső határvonal (tűzfal, DMZ).  
- Belső hálózatot jellemzően megbízhatónak tekinti.  
- Modern támadások ellen ez önmagában kevés lehet.

**Egyszerű példa:**  
Ha támadó bejut belülre, sokszor könnyebben mozoghat laterálisan.

**Vizsgán fontos kulcsszavak:**  
**[[perimeter security]]**, **tűzfal**, **külső-belső határ**, **hagyományos védelem**

---

### 8.2 Defense-in-depth
**Rövid definíció:**  
A **[[defense-in-depth]]** többrétegű védekezést jelent.

**Működési elv:**  
- Egymást kiegészítő kontrollok: hálózati, alkalmazás- és végpontvédelem.  
- Egy védelmi réteg áttörése után további rétegek lassítanak/megállítanak.

**Egyszerű példa:**  
Tűzfal + MFA + EDR + naplóelemzés együtt nagyobb biztonságot ad.

**Vizsgán fontos kulcsszavak:**  
**[[defense-in-depth]]**, **többrétegű védelem**, **redundáns kontrollok**

---

### 8.3 Zero Trust
**Rövid definíció:**  
A **[[Zero Trust]]** elv szerint alapból sem felhasználó, sem eszköz nem megbízható.

**Működési elv:**  
- „Never trust, always verify” szemlélet.  
- Minden hozzáférés hitelesítése, autorizációja és naplózása szükséges.  
- Kontextus-alapú, folyamatos ellenőrzés.

**Egyszerű példa:**  
Belső hálózatról érkező kérésnél is kell MFA és jogosultságellenőrzés.

**Vizsgán fontos kulcsszavak:**  
**[[Zero Trust]]**, **folyamatos ellenőrzés**, **MFA**, **least privilege**

---

## 9. Összefüggések
**Rövid definíció:**  
A biztonsági célok, kriptográfiai eszközök és védelmi modellek együtt adják a teljes védelmi stratégiát.

**Működési elv:**  
- CIA-triász kijelöli a célokat.  
- Kriptográfia technikai alapot ad a megvalósításhoz.  
- Védelmi paradigmák meghatározzák az üzemeltetési szemléletet.

**Egyszerű példa:**  
Zero Trust környezetben titkosított kommunikáció, erős azonosítás és naplózás együtt működik.

**Vizsgán fontos kulcsszavak:**  
**biztonsági stratégia**, **CIA + kriptográfia**, **védelmi modell**, **integrált védelem**

---

## + Vizsgán érdemes még megemlíteni
- **HTTPS** jó példa hibrid kriptográfiára a gyakorlatban.  
- Kulcscsere szerepe (pl. RSA/ECDHE típusú megoldások említése).  
- **Hash nem titkosítás**: más célra szolgál.  
- **[[Zero Trust]]** modern felhő és hibrid környezetben különösen fontos.  
- Biztonság és teljesítmény között gyakran kompromisszumot kell kezelni.

---

## Rövid szóbeli összefoglaló
A hálózati biztonság célja az adatok és szolgáltatások védelme, amit a CIA-triász ír le: bizalmasság, sértetlenség, rendelkezésre állás. A kriptográfia ezt gyakorlati eszközökkel valósítja meg: szimmetrikus és aszimmetrikus titkosítással, digitális aláírással és hash függvényekkel. Fontos elv, hogy a rendszer biztonsága ne az algoritmus titkosságán, hanem a kulcson múljon. A modern védelem már nem csak peremvédelem: a defense-in-depth többrétegű, a Zero Trust pedig minden hozzáférést folyamatosan ellenőriz. A gyakorlatban hibrid megoldások működnek, például HTTPS, ahol aszimmetrikus és szimmetrikus elemek együtt adnak biztonságot.

## Kulcsfogalmak
- [[információbiztonság]]
- [[CIA-triász]]
- [[bizalmasság]]
- [[sértetlenség]]
- [[rendelkezésre állás]]
- [[Kerckhoffs-elv]]
- [[tökéletes titkosság]]
- [[szimmetrikus titkosítás]]
- [[aszimmetrikus titkosítás]]
- [[digitális aláírás]]
- [[hash függvény]]
- [[defense-in-depth]]
- [[Zero Trust]]
- [[HTTPS]]
- [[kulcscsere]]

## Tipikus vizsgakérdések
1. **Mi a CIA-triász három eleme?**  
   Bizalmasság, sértetlenség, rendelkezésre állás.

2. **Mit mond ki a Kerckhoffs-elv?**  
   A biztonság a kulcs titkosságától függjön, ne az algoritmus titkosságától.

3. **Mi a különbség szimmetrikus és aszimmetrikus titkosítás között?**  
   Szimmetrikusnál közös kulcs, aszimmetrikusnál kulcspár van.

4. **Mire jó a digitális aláírás?**  
   Hitelességet és sértetlenséget biztosít.

5. **Mi a hash és titkosítás közti különbség?**  
   Hash egyirányú lenyomat, titkosítás visszafejthető megfelelő kulccsal.

6. **Mi a Zero Trust lényege?**  
   Alapértelmezett bizalmatlanság és folyamatos hozzáférés-ellenőrzés.

7. **Miért kell defense-in-depth?**  
   Mert egyetlen védelmi réteg áttörése esetén további rétegek maradnak.

## Minimum, amit tudni kell
- Információbiztonság célja és a CIA-triász elemei.  
- Kerckhoffs-elv lényege.  
- Szimmetrikus és aszimmetrikus titkosítás alap különbsége.  
- Digitális aláírás működési ötlete (hash + privát/public kulcs).  
- Hash függvény fő tulajdonságai és felhasználása.  
- Perimeter, defense-in-depth, Zero Trust rövid különbsége.  
- HTTPS mint gyakorlati kriptográfiai példa.  
- Biztonság és teljesítmény közti kompromisszum fogalma.
