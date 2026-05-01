# Rendszerfejlesztés I. – 24. tétel
## Projektmenedzsment, költségbecslés, szoftvermérés

---

## 1. Projektmenedzsment

### 1.1 Fogalom
**Rövid definíció:**  
A **[[projekt]]** egyedi, időben korlátozott tevékenység, amelynek célja konkrét eredmény létrehozása. A **[[projektmenedzsment]]** ennek tervezése és irányítása.

**Működési elv:**  
- A projektnek van kezdete és vége.  
- Erőforrásokkal, határidővel és költségkerettel dolgozik.  
- A menedzsment feladata az összehangolás és döntéstámogatás.

**Egyszerű példa:**  
Egy vállalati belső ügykezelő rendszer bevezetése tipikus projekt: fix cél, határidő, csapat és költségkeret.

**Vizsgán fontos kulcsszavak:**  
**[[projekt]]**, **[[projektmenedzsment]]**, **időkorlát**, **eredményorientáltság**, **erőforrás**

---

### 1.2 Projektmenedzsment céljai
**Rövid definíció:**  
A projektmenedzsment fő célja, hogy a projekt időre, költségkereten belül és megfelelő minőségben készüljön el.

**Működési elv:**  
- Ütemezés és prioritások kezelése.  
- Költségek nyomon követése és kontrollja.  
- Minőségbiztosítási pontok beépítése.

**Egyszerű példa:**  
Ha csúszik a fejlesztés, a projektvezető erőforrást csoportosít át, hogy a kritikus határidő tartható maradjon.

**Vizsgán fontos kulcsszavak:**  
**határidő**, **költségkeret**, **minőségbiztosítás**, **projektkontroll**

---

### 1.3 Projekt háromszög
**Rövid definíció:**  
A **[[projekt háromszög]]** azt mutatja, hogy az idő, költség és minőség egymással összefüggő korlátok.

**Működési elv:**  
- Ha rövidül a határidő, gyakran nő a költség vagy csökken a minőség.  
- Ha csökkentjük a költséget, nőhet az idő vagy romolhat a minőség.  
- Projektvezetői döntés, melyik dimenzió mennyire rugalmas.

**Egyszerű példa:**  
Gyorsabb szállítás igénye esetén több fejlesztőt vesznek fel, ami növeli a költséget.

**Vizsgán fontos kulcsszavak:**  
**[[projekt háromszög]]**, **idő**, **költség**, **minőség**, **trade-off**

---

### 1.4 Projekt fázisok
**Rövid definíció:**  
A projekt fázisokra bontása segít az átlátható irányításban.

**Működési elv:**  
- **Tervezés**: célok, feladatok, becslések.  
- **Végrehajtás**: fejlesztés és napi működtetés.  
- **Ellenőrzés**: státusz, eltérések, korrekciók.  
- **Lezárás**: átadás, értékelés, tanulságok.

**Egyszerű példa:**  
Lezáráskor készül egy „lessons learned” dokumentum, amit a következő projektben felhasználnak.

**Vizsgán fontos kulcsszavak:**  
**projektfázisok**, **tervezés**, **végrehajtás**, **ellenőrzés**, **lezárás**

---

## 2. Projekttervezés

### 2.1 Feladatok bontása
**Rövid definíció:**  
A **[[WBS]]** (Work Breakdown Structure) a projekt feladatainak hierarchikus bontása.

**Működési elv:**  
- A nagy célokat kisebb, kezelhető munkacsomagokra bontjuk.  
- Segíti a felelősségek és becslések pontosítását.  
- Jó alapot ad ütemezéshez és költségtervezéshez.

**Egyszerű példa:**  
„Webshop” -> „felhasználókezelés”, „katalógus”, „fizetés”, majd ezek további részfeladatokra bonthatók.

**Vizsgán fontos kulcsszavak:**  
**[[WBS]]**, **munkacsomag**, **feladatbontás**, **felelősség**

---

### 2.2 Ütemezés
**Rövid definíció:**  
Az ütemezés azt határozza meg, mikor melyik feladat készül el és milyen függőségek vannak.

**Működési elv:**  
- **[[Gantt-diagram]]**: idővonalas vizuális feladatábra.  
- **[[CPM]]** (kritikus út): meghatározza a projekt minimális időtartamát adó feladatláncot.  
- Kritikus út feladatai nem csúszhatnak büntetlenül.

**Egyszerű példa:**  
Ha a kritikus úton lévő „tesztelés” csúszik 3 napot, a teljes projekt is 3 napot csúszik.

**Vizsgán fontos kulcsszavak:**  
**ütemezés**, **[[Gantt-diagram]]**, **[[CPM]]**, **kritikus út**, **függőség**

---

### 2.3 Erőforrások
**Rövid definíció:**  
Erőforrástervezésnél meghatározzuk, milyen emberekre és eszközökre van szükség.

**Működési elv:**  
- Szerepkörök kiosztása (fejlesztő, tesztelő, PM).  
- Szükséges technikai eszközök biztosítása.  
- Kapacitás és túlterhelés folyamatos figyelése.

**Egyszerű példa:**  
Ha egyszerre több kritikus modul indul, extra tesztelő bevonása szükséges lehet.

**Vizsgán fontos kulcsszavak:**  
**erőforrástervezés**, **kapacitás**, **szerepkör**, **eszközigény**

---

## 3. Költségbecslés

### 3.1 Fogalom
**Rövid definíció:**  
A **[[költségbecslés]]** a projekt várható pénzügyi ráfordításának előrejelzése.

**Működési elv:**  
- A becslés nem egyszeri szám, hanem folyamatosan pontosodik.  
- Tartalmazhat személyi, eszköz- és üzemeltetési költséget.  
- Döntéstámogató szerepe van a projektindításnál.

**Egyszerű példa:**  
Első becslés induláskor 20 millió Ft, majd részletes tervezés után 24 millióra pontosodik.

**Vizsgán fontos kulcsszavak:**  
**[[költségbecslés]]**, **ráfordítás**, **budget**, **becslési bizonytalanság**

---

### 3.2 Módszerek

#### Szakértői becslés
**Rövid definíció:**  
Tapasztalt szakemberek korábbi tudására épülő becslés.

**Működési elv:**  
- Gyors, ha van releváns tapasztalat.  
- Szubjektív torzítás lehetséges.  
- Gyakran más módszerekkel kombinálják.

**Egyszerű példa:**  
Senior fejlesztő korábbi hasonló projekt alapján 3 hónapra becsüli a backend fejlesztést.

**Vizsgán fontos kulcsszavak:**  
**szakértői becslés**, **tapasztalat**, **szubjektivitás**

---

#### Analóg becslés
**Rövid definíció:**  
Korábbi hasonló projektek adatai alapján készített becslés.

**Működési elv:**  
- Referenciaprojektet keresünk.  
- Méret- és komplexitáskülönbséggel korrigálunk.  
- Gyors, de jó történeti adat kell hozzá.

**Egyszerű példa:**  
Egy korábbi mobilapp 6 hónap volt, az új funkciógazdagabb változatot 8 hónapra becsülik.

**Vizsgán fontos kulcsszavak:**  
**analóg becslés**, **referenciaprojekt**, **korrekció**

---

#### Algoritmikus modellek
**Rövid definíció:**  
Matematikai modellek, amelyek bemeneti paraméterekből (pl. méret) számolnak idő- és költségbecslést.

**Működési elv:**  
- Példa: **[[COCOMO]]**.  
- Bemenet lehet **[[LOC]]** vagy más méretmérő.  
- Kimenet: fejlesztési erőfeszítés, idő, költség.

**Egyszerű példa:**  
Nagyvállalati projektben COCOMO-t használnak induló becslésre, majd sprintenként finomítják.

**Vizsgán fontos kulcsszavak:**  
**[[COCOMO]]**, **algoritmikus becslés**, **[[LOC]]**, **idő-költség becslés**

---

### 3.3 Költségtípusok
**Rövid definíció:**  
A költségek nem csak fejlesztésből állnak, hanem fenntartásból is.

**Működési elv:**  
- **Fejlesztési költség**: tervezés, implementáció, tesztelés, bevezetés.  
- **Fenntartási költség**: hibajavítás, támogatás, továbbfejlesztés.  
- Hosszú távon a fenntartás sokszor domináns.

**Egyszerű példa:**  
Egy rendszer első évben drága fejlesztés, de 3-5 év alatt a karbantartási költség nagyobb lehet.

**Vizsgán fontos kulcsszavak:**  
**fejlesztési költség**, **fenntartási költség**, **TCO**, **életciklus-költség**

---

## 4. Szoftvermérés

### 4.1 Fogalom
**Rövid definíció:**  
A **[[szoftvermérés]]** a szoftver tulajdonságainak számszerűsítése, hogy objektív döntéseket tudjunk hozni.

**Működési elv:**  
- Mérünk méretet, minőséget, teljesítményt.  
- A mérések segítik a becslést, nyomon követést és javítást.  
- Fontos az egységes mérési szabály.

**Egyszerű példa:**  
Ha sprintenként mérjük a hibaarányt, látszik, javul-e a minőség.

**Vizsgán fontos kulcsszavak:**  
**[[szoftvermérés]]**, **metrika**, **objektív értékelés**, **nyomon követés**

---

### 4.2 Méretmérés

#### LOC (Lines of Code)
**Rövid definíció:**  
A **[[LOC]]** a forráskód sorainak száma.

**Működési elv:**  
- Egyszerűen mérhető.  
- Erősen nyelv- és stílusfüggő.  
- Nem mindig tükrözi a valódi funkcionális értéket.

**Egyszerű példa:**  
Ugyanaz a funkció Pythonban kevesebb, C++-ban több LOC lehet.

**Vizsgán fontos kulcsszavak:**  
**[[LOC]]**, **méretmérés**, **nyelvfüggőség**

---

#### Funkciópont (Function Point)
**Rövid definíció:**  
A **[[funkciópont]]** a rendszer nyújtott funkcionalitását méri, nem a kód mennyiségét.

**Működési elv:**  
- Bemenetek, kimenetek, lekérdezések, interfészek alapján értékel.  
- Nyelvfüggetlenebb és üzleti szempontból beszédesebb.  
- Becsléshez gyakran hasznosabb, mint a LOC.

**Egyszerű példa:**  
Két különböző technológiájú rendszer azonos funkciópontra jöhet ki, bár a LOC eltér.

**Vizsgán fontos kulcsszavak:**  
**[[funkciópont]]**, **funkcionalitás**, **nyelvfüggetlen mérés**

---

### 4.3 Minőségmérés
**Rövid definíció:**  
A minőségmérés a szoftver hibamentességét és hosszú távú használhatóságát értékeli.

**Működési elv:**  
- Metrikák: hibasűrűség, kiesési idő, javítási idő.  
- Vizsgálható megbízhatóság és karbantarthatóság is.  
- Minőségtrendek alapján folyamat javítható.

**Egyszerű példa:**  
Ha egy modulban tartósan magas a hibaszám, refaktorálás vagy extra teszt szükséges.

**Vizsgán fontos kulcsszavak:**  
**hibaszám**, **megbízhatóság**, **karbantarthatóság**, **hibasűrűség**

---

### 4.4 Teljesítménymérés
**Rövid definíció:**  
A teljesítménymérés azt mutatja meg, mennyire gyorsan és erőforrás-hatékonyan fut a szoftver.

**Működési elv:**  
- Kulcsmutatók: válaszidő, áteresztőképesség, memóriahasználat.  
- Terheléses tesztekkel mérhető valós környezetközeli helyzetekben.  
- Kritikus rendszereknél folyamatos monitorozás szükséges.

**Egyszerű példa:**  
Webalkalmazásnál 1000 egyidejű felhasználó mellett mérjük az átlagos válaszidőt.

**Vizsgán fontos kulcsszavak:**  
**teljesítménymérés**, **válaszidő**, **áteresztőképesség**, **memóriahasználat**

---

## 5. Kockázatkezelés
**Rövid definíció:**  
A **[[kockázatkezelés]]** a lehetséges problémák előzetes azonosítása és kezelése.

**Működési elv:**  
- Kockázatok listázása (technikai, erőforrás, üzleti).  
- Valószínűség és hatás becslése.  
- Stratégiák: elkerülés, csökkentés, áthárítás, elfogadás.

**Egyszerű példa:**  
Kulcsfejlesztő kiesésének kockázatát tudásmegosztással és dokumentálással csökkentjük.

**Vizsgán fontos kulcsszavak:**  
**[[kockázatkezelés]]**, **kockázati mátrix**, **valószínűség**, **hatás**, **mitigáció**

---

## 6. Összefüggések
**Rövid definíció:**  
A projektmenedzsment, becslés és mérés egymásra épülő rendszer.

**Működési elv:**  
- A mérések adatot adnak a becsléshez.  
- A becslések táplálják a tervezést és ütemezést.  
- A projektmenedzsment mindezt folyamatosan koordinálja.

**Egyszerű példa:**  
Ha a mért hibaszám nő, a menedzsment módosítja az ütemezést és több tesztelési erőforrást ad.

**Vizsgán fontos kulcsszavak:**  
**mérés-becslés-tervezés lánc**, **visszacsatolás**, **irányítás**

---

## + Vizsgán érdemes még megemlíteni
- **[[COCOMO]]** modell: méretből becsült erőfeszítés és idő.  
- **[[LOC]] vs [[funkciópont]]**: kódmennyiség vs funkcionalitás.  
- **[[projekt háromszög]]** trade-off mindig jelen van.  
- A kockázatkezelés hiánya gyakran költség- és időtúllépéshez vezet.

---

## Rövid szóbeli összefoglaló
A projektmenedzsment célja, hogy a szoftverprojekt időre, költségkereten belül és megfelelő minőségben valósuljon meg. A projektet fázisokra bontjuk, a tervezésben WBS-sel strukturálunk, ütemezéshez például Gantt-diagramot és kritikus út elemzést használunk. A költségbecslés történhet szakértői, analóg vagy algoritmikus módon, például COCOMO-val. A szoftvermérés adatot ad a döntésekhez: méretmérésre LOC vagy funkciópont, minőségre hibametrikák, teljesítményre válaszidő és memóriahasználat használható. A kockázatkezelés végigkíséri a projektet, mert a problémákat jobb előre kezelni, mint utólag javítani. A lényeg, hogy mérés, becslés és menedzsment egymásra épül.

## Kulcsfogalmak
- [[projekt]]
- [[projektmenedzsment]]
- [[projekt háromszög]]
- [[WBS]]
- [[Gantt-diagram]]
- [[CPM]]
- [[költségbecslés]]
- [[COCOMO]]
- [[LOC]]
- [[funkciópont]]
- [[szoftvermérés]]
- [[kockázatkezelés]]
- [[kockázati mátrix]]
- [[minőségbiztosítás]]
- [[rehashing]]

## Tipikus vizsgakérdések
1. **Mi a projektmenedzsment fő célja?**  
   A projekt idő-, költség- és minőségi céljainak együttes teljesítése.

2. **Mit jelent a projekt háromszög?**  
   Az idő, költség és minőség egymást befolyásoló korlátok.

3. **Mi a WBS szerepe a tervezésben?**  
   A projektet kezelhető feladatokra bontja, ami alap az ütemezéshez és becsléshez.

4. **Milyen költségbecslési módszereket ismersz?**  
   Szakértői, analóg és algoritmikus becslés (pl. COCOMO).

5. **Mi a különbség LOC és funkciópont között?**  
   LOC kódsort mér és nyelvfüggő, funkciópont funkcionalitást mér és nyelvfüggetlenebb.

6. **Miért fontos a szoftvermérés?**  
   Objektív adatot ad a becsléshez, nyomon követéshez és folyamatjavításhoz.

7. **Hogyan történik a kockázatkezelés?**  
   Kockázatok azonosítása, valószínűség-hatás értékelése, majd kezelési stratégia választása.

## Minimum, amit tudni kell
- A projektmenedzsment célhármasa: idő, költség, minőség.  
- A projekt fő fázisai: tervezés, végrehajtás, ellenőrzés, lezárás.  
- WBS és ütemezés (Gantt, kritikus út) alapötlete.  
- Költségbecslés fő típusai és COCOMO említése.  
- LOC és funkciópont különbsége.  
- Minőség- és teljesítménymérés alapmetrikái.  
- Kockázatkezelés lépései.  
- A mérés -> becslés -> tervezés összefüggése.
