# Számítástudomány – 3. tétel
## Reguláris és környezetfüggetlen nyelvek, automaták

---

## 1. Formális nyelvek alapjai

### 1.1 Ábécé és szavak
**Rövid definíció:**  
A formális nyelvelméletben az **[[ábécé]]** jelek halmaza, a **szó** ezek véges sorozata, a **[[nyelv]]** pedig szavak halmaza.

**Működési elv:**  
- `Σ` jelöli az ábécét.  
- `Σ*` az összes lehetséges véges szó halmaza.  
- Egy nyelv ennek egy részhalmaza.

**Egyszerű példa:**  
`Σ={a,b}` esetén `ab`, `baa` szavak; a csak páros hosszú szavak egy konkrét nyelvet adnak.

**Vizsgán fontos kulcsszavak:**  
**[[ábécé]]**, **szó**, **[[nyelv]]**, **`Σ`**, **`Σ*`**

---

## 2. Reguláris nyelvek

### 2.1 Definíció
**Rövid definíció:**  
A **[[reguláris nyelv]]** olyan nyelv, amely leírható reguláris kifejezéssel és felismerhető véges automatával.

**Működési elv:**  
- Ugyanazt az osztályt több ekvivalens formalizmus adja (regex, DFA, NFA).  
- Korlátozott kifejezőerő: nincs veremmemória.

**Egyszerű példa:**  
Az `a*b*` nyelv reguláris: tetszőleges sok `a`, majd tetszőleges sok `b`.

**Vizsgán fontos kulcsszavak:**  
**[[reguláris nyelv]]**, **reguláris kifejezés**, **véges automata**, **ekvivalencia**

---

### 2.2 Reguláris kifejezések
**Rövid definíció:**  
A **[[reguláris kifejezés]]** nyelvleíró jelölés reguláris nyelvekhez.

**Működési elv:**  
- **Konkatenáció**: egymás után írás.  
- **Unió (`|`)**: alternatíva.  
- **[[Kleene-csillag]] (`*`)**: tetszőleges ismétlés (0 vagy több).

**Egyszerű példa:**  
`(ab|ba)*` minden olyan szót leír, ami `ab` és `ba` blokkokból áll.

**Vizsgán fontos kulcsszavak:**  
**[[reguláris kifejezés]]**, **konkatenáció**, **unió**, **[[Kleene-csillag]]**

---

### 2.3 Véges automaták

#### Determinisztikus (DFA)
**Rövid definíció:**  
A **[[DFA]]** olyan véges automata, ahol minden állapotból minden bemeneti jelre legfeljebb egy átmenet van.

**Működési elv:**  
- A futás egyértelmű útvonalon halad.  
- Elfogadás, ha a szó végén elfogadó állapotba jut.

**Egyszerű példa:**  
Páros számú `a`-t tartalmazó szavak felismerésére 2 állapotos DFA építhető.

**Vizsgán fontos kulcsszavak:**  
**[[DFA]]**, **determinista átmenet**, **elfogadó állapot**

---

#### Nemdeterminisztikus (NFA)
**Rövid definíció:**  
Az **[[NFA]]** automata egy állapotból ugyanarra a jelre több lehetséges átmenetet is engedhet.

**Működési elv:**  
- Elfogad, ha létezik legalább egy elfogadó futás.  
- Kifejezőerőben ekvivalens a DFA-val.

**Egyszerű példa:**  
Regexből gyakran egyszerűbb először NFA-t építeni, majd DFA-vá alakítani.

**Vizsgán fontos kulcsszavak:**  
**[[NFA]]**, **nemdeterminisztikus átmenet**, **DFA-ekvivalencia**

---

### 2.4 Tulajdonságok
**Rövid definíció:**  
A reguláris nyelvek felismerésének kulcsjellemzője a véges memória.

**Működési elv:**  
- Csak állapottal „emlékeznek”, verem nélkül.  
- Egyszerű és hatékony felismerők készíthetők.

**Egyszerű példa:**  
Kulcsszavas mintakeresés szövegben jól modellezhető véges automatával.

**Vizsgán fontos kulcsszavak:**  
**véges memória**, **állapotgép**, **hatékony felismerés**

---

## 3. Környezetfüggetlen nyelvek (CFG)

### 3.1 Definíció
**Rövid definíció:**  
A **[[környezetfüggetlen nyelv]]** olyan nyelv, amely **[[környezetfüggetlen grammatika]]** segítségével generálható.

**Működési elv:**  
- Produkciós szabályok alakja: `A -> α`.  
- A bal oldalon mindig egy nemterminális áll.

**Egyszerű példa:**  
`S -> aSb | ε` nyelv: azonos számú `a` és `b` megfelelő rendben.

**Vizsgán fontos kulcsszavak:**  
**[[környezetfüggetlen nyelv]]**, **[[CFG]]**, **produkciós szabály**

---

### 3.2 Grammatika elemei
**Rövid definíció:**  
A grammatika formális komponensekből áll, amelyek együtt írják le a nyelvet.

**Működési elv:**  
- Nemterminálisok: köztes jelölések.  
- Terminálisok: a kész szó jelei.  
- Kezdőszimbólum: innen indul a generálás.  
- Produkciók: átírási szabályok.

**Egyszerű példa:**  
Egyszerű kifejezésnyelvben `E -> E+T | T` típusú szabályokkal írható le a szerkezet.

**Vizsgán fontos kulcsszavak:**  
**nemterminális**, **terminális**, **kezdőszimbólum**, **produkció**

---

### 3.3 Felismerés
**Rövid definíció:**  
A környezetfüggetlen nyelvek felismerő modellje a **[[veremautomata]] (PDA)**.

**Működési elv:**  
- A véges vezérlés mellé veremmemória társul.  
- A verem lehetővé teszi a beágyazott szerkezetek kezelését.

**Egyszerű példa:**  
Kiegyensúlyozott zárójelek nyelve PDA-val jól felismerhető.

**Vizsgán fontos kulcsszavak:**  
**[[veremautomata]]**, **[[PDA]]**, **veremmemória**, **CFG felismerés**

---

### 3.4 Tulajdonságok
**Rövid definíció:**  
A CFG-k erősek rekurzív, hierarchikus struktúrák leírásában.

**Működési elv:**  
- Beágyazott szerkezeteket természetesen kezelnek.  
- Fordítók szintaktikai elemzésének alapját adják.

**Egyszerű példa:**  
Programozási nyelvek zárójelezési szabályai CFG-vel írhatók le.

**Vizsgán fontos kulcsszavak:**  
**rekurzív szerkezet**, **beágyazás**, **szintaxisleírás**

---

## 4. Reguláris vs környezetfüggetlen

**Rövid definíció:**  
A két nyelvosztály között fő különbség a memória és kifejezőerő.

**Működési elv:**  
- Reguláris nyelv: egyszerűbb, véges állapot elég.  
- CFG: erősebb, veremmemória kellhet.

**Egyszerű példa:**  
`a^n b^n` nem reguláris, de környezetfüggetlen.

**Vizsgán fontos kulcsszavak:**  
**kifejezőerő**, **véges memória vs verem**, **`a^n b^n` példa**

---

## 5. Pumpáló lemma

### 5.1 Reguláris nyelvekre
**Rövid definíció:**  
A **[[pumpáló lemma]]** szükséges feltételt ad reguláris nyelvekre.

**Működési elv:**  
- Elég hosszú szó felbontható `w=xyz` alakra.  
- Az `y` rész pumpálható (`xy^iz`), és a szó nyelvben marad.

**Egyszerű példa:**  
Nem-regulárisság bizonyításakor feltesszük a lemma igazságát, majd ellentmondásra jutunk.

**Vizsgán fontos kulcsszavak:**  
**[[pumpáló lemma]]**, **`w=xyz`**, **pumpálhatóság**, **ellentmondásos bizonyítás**

---

### 5.2 Környezetfüggetlen nyelvekre
**Rövid definíció:**  
CFG-kre is van pumpáló lemma, de összetettebb felbontási feltételekkel.

**Működési elv:**  
- A bizonyítási technika hasonló, de a bontás (`uvxyz`) és feltételek bonyolultabbak.  
- Nem-CFG nyelvek bizonyítására használható.

**Egyszerű példa:**  
Bizonyos nyelveknél ezzel mutatható, hogy nem környezetfüggetlenek.

**Vizsgán fontos kulcsszavak:**  
**CFG pumpáló lemma**, **bonyolultabb feltételek**, **nem-CFG bizonyítás**

---

### 5.3 Szerep
**Rövid definíció:**  
A pumpáló lemma fő szerepe a „nem tartozik bele” típusú bizonyítás.

**Működési elv:**  
- Nem azt bizonyítja, hogy nyelv reguláris/CFG.  
- Azt segít bizonyítani, hogy egy nyelv **nem** reguláris vagy **nem** CFG.

**Egyszerű példa:**  
`{a^n b^n}` nyelvről pumpáló lemmával igazolható, hogy nem reguláris.

**Vizsgán fontos kulcsszavak:**  
**negatív bizonyítás**, **nem reguláris**, **nem CFG**

---

## 6. Zártsági tulajdonságok

### 6.1 Reguláris nyelvek
**Rövid definíció:**  
A reguláris nyelvek sok műveletre zártak.

**Működési elv:**  
- Zártak unióra, metszetre, komplementerre, konkatenációra, Kleene-csillagra.  
- Ez erős elméleti és gyakorlati tulajdonság.

**Egyszerű példa:**  
Két regex által leírt nyelv uniója is regexszel leírható.

**Vizsgán fontos kulcsszavak:**  
**zártság**, **unió**, **metszet**, **komplementer**, **Kleene-csillag**

---

### 6.2 Környezetfüggetlen nyelvek
**Rövid definíció:**  
A CFG nyelvek zártsága korlátozottabb a regulárisaknál.

**Működési elv:**  
- Zártak unióra, konkatenációra, Kleene-csillagra.  
- Általában nem zártak metszetre és komplementerre.

**Egyszerű példa:**  
Két CFG metszete lehet olyan nyelv, ami már nem környezetfüggetlen.

**Vizsgán fontos kulcsszavak:**  
**CFG zártság**, **nem zárt metszetre**, **nem zárt komplementerre**

---

## 7. Összefüggések
**Rövid definíció:**  
A nyelvosztályok és automaták között szoros megfeleltetések vannak.

**Működési elv:**  
- `reguláris ⊂ környezetfüggetlen`.  
- Reguláris ↔ DFA/NFA, CFG ↔ PDA.  
- Grammatika generál, automata felismer.

**Egyszerű példa:**  
Egy regexből NFA, majd DFA készíthető; CFG-ből veremautomata szemlélet adható.

**Vizsgán fontos kulcsszavak:**  
**osztálytartalmazás**, **automata-nyelv megfeleltetés**, **generálás vs felismerés**

---

## + Vizsgán érdemes még megemlíteni
- **[[DFA]] és [[NFA]]** ekvivalens kifejezőerő.  
- **[[PDA]]** kulcsszerepű beágyazott struktúrák felismerésében.  
- Pumpáló lemma tipikus nem-reguláris bizonyítási eszköz.  
- Gyakorlati példa: zárójelezés, egyszerű parser-feladatok.

---

## Rövid szóbeli összefoglaló
A formális nyelvek alapja az ábécé, a szó és a nyelv fogalma. Reguláris nyelvek regexszel leírhatók és véges automatával felismerhetők, ahol a DFA és NFA ekvivalens. Környezetfüggetlen nyelvek grammatikával írhatók le, és veremautomatával ismerhetők fel, ezért alkalmasak rekurzív, beágyazott szerkezetek modellezésére. A reguláris nyelvek egyszerűbbek, a CFG nyelvek erősebbek. A pumpáló lemma fontos eszköz annak bizonyítására, hogy egy nyelv nem reguláris vagy nem környezetfüggetlen. Zártsági tulajdonságokban a reguláris osztály erősebb, CFG-nél több műveletre nem áll fenn a zártság.

## Kulcsfogalmak
- [[ábécé]]
- [[nyelv]]
- [[reguláris nyelv]]
- [[reguláris kifejezés]]
- [[Kleene-csillag]]
- [[DFA]]
- [[NFA]]
- [[környezetfüggetlen nyelv]]
- [[CFG]]
- [[veremautomata]]
- [[PDA]]
- [[pumpáló lemma]]
- [[zártsági tulajdonság]]
- [[metszet]]
- [[komplementer]]

## Tipikus vizsgakérdések
1. **Mi a különbség ábécé, szó és nyelv között?**  
   Ábécé jelek halmaza, szó ezekből képzett véges sorozat, nyelv szavak halmaza.

2. **Mikor reguláris egy nyelv?**  
   Ha leírható regexszel és felismerhető véges automatával.

3. **Mi a DFA és NFA kapcsolata?**  
   Kifejezőerőben ekvivalensek.

4. **Miért erősebb a CFG osztály a regulárisnál?**  
   Mert veremmemória miatt rekurzív beágyazásokat is tud kezelni.

5. **Mire használjuk a pumpáló lemmát?**  
   Nem-reguláris vagy nem-CFG volt bizonyítására.

6. **Miben különbözik a reguláris és CFG zártság?**  
   Reguláris több műveletre zárt, CFG például metszetre általában nem.

7. **Milyen automata tartozik CFG nyelvekhez?**  
   Veremautomata (PDA).

## Minimum, amit tudni kell
- Ábécé, szó, nyelv alapfogalom.  
- Reguláris nyelv definíciója (regex + véges automata).  
- DFA és NFA rövid különbsége és ekvivalenciája.  
- CFG fő elemei (terminális, nemterminális, kezdőszimbólum, produkció).  
- PDA szerepe a környezetfüggetlen nyelveknél.  
- Reguláris vs CFG kifejezőerő fő különbsége.  
- Pumpáló lemma alapötlete és szerepe.  
- Reguláris és CFG zártsági tulajdonságainak lényegi eltérése.
