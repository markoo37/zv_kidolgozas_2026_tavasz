# Adatbázisok – 15. tétel
## SQL: DDL, DML, relációsémák, megszorítások, lekérdezések

---

## 1. SQL alapok

### 1.1 SQL fogalma
**Rövid definíció:**  
Az **[[SQL]]** (Structured Query Language) a relációs adatbázisok szabványos kezelőnyelve.

**Működési elv:**  
- Deklaratív jellegű: azt mondjuk meg, mit szeretnénk, nem a végrehajtási lépéseket.  
- Tábla létrehozásra, módosításra, lekérdezésre és adatműveletekre használható.

**Egyszerű példa:**  
`SELECT nev FROM Hallgato WHERE atlag > 4.0;` megadja a kívánt adatot, az optimalizálást az adatbázis végzi.

**Vizsgán fontos kulcsszavak:**  
**[[SQL]]**, **deklaratív nyelv**, **relációs adatbázis**, **lekérdezés**

---

### 1.2 SQL nyelvi részek
**Rövid definíció:**  
Az SQL több alnyelvre bontható funkció szerint.

**Működési elv:**  
- **[[DDL]]**: adatstruktúra definiálása.  
- **[[DML]]**: adatok beszúrása, módosítása, törlése, lekérdezése.  
- **DCL**: jogosultságkezelés (említési szinten).

**Egyszerű példa:**  
`CREATE TABLE` DDL, `INSERT` és `UPDATE` DML művelet.

**Vizsgán fontos kulcsszavak:**  
**[[DDL]]**, **[[DML]]**, **DCL**, **SQL alnyelvek**

---

## 2. DDL – Adatdefiníciós nyelv

### 2.1 CREATE
**Rövid definíció:**  
A `CREATE` új adatbázis objektum létrehozására szolgál.

**Működési elv:**  
- Táblát, oszlopokat, adattípusokat és megszorításokat definiálunk.  
- A séma alapja itt készül el.

**Egyszerű példa:**  
`CREATE TABLE Hallgato(id INT PRIMARY KEY, nev VARCHAR(100));`

**Vizsgán fontos kulcsszavak:**  
**CREATE**, **tábladefiníció**, **oszlop**, **séma**

---

### 2.2 ALTER
**Rövid definíció:**  
Az `ALTER` meglévő tábla szerkezetét módosítja.

**Működési elv:**  
- Oszlop hozzáadás, törlés, típusmódosítás, megszorítás módosítás.  
- Éles rendszernél körültekintően kell használni.

**Egyszerű példa:**  
`ALTER TABLE Hallgato ADD email VARCHAR(150);`

**Vizsgán fontos kulcsszavak:**  
**ALTER**, **sémamódosítás**, **oszlop hozzáadás/törlés**

---

### 2.3 DROP
**Rövid definíció:**  
A `DROP` objektumot teljesen eltávolít az adatbázisból.

**Működési elv:**  
- Tábla és szerkezete is megszűnik.  
- Függőségek miatt hiba vagy kaszkád törlés is lehet.

**Egyszerű példa:**  
`DROP TABLE Hallgato;` törli a táblát minden adatával együtt.

**Vizsgán fontos kulcsszavak:**  
**DROP**, **objektumtörlés**, **visszafordíthatatlanság**

---

### 2.4 TRUNCATE (említés)
**Rövid definíció:**  
A `TRUNCATE` a tábla összes sorát törli, a szerkezetet megtartja.

**Működési elv:**  
- Gyors tömeges ürítésre használják.  
- Nem ugyanaz, mint a `DROP`.

**Egyszerű példa:**  
Tesztadatok gyors ürítése `TRUNCATE TABLE Teszt;`

**Vizsgán fontos kulcsszavak:**  
**TRUNCATE**, **tartalomtörlés**, **szerkezet megmarad**

---

## 3. Relációsémák definiálása

### 3.1 Tábla szerkezete
**Rövid definíció:**  
A relációséma meghatározza, milyen oszlopok és szabályok szerint tárolható adat.

**Működési elv:**  
- Oszlopnév + adattípus + megszorítás kombináció.  
- Ez biztosítja a helyes, valid adatbevitelt.

**Egyszerű példa:**  
`szul_datum DATE NOT NULL` mező kötelező dátumértéket vár.

**Vizsgán fontos kulcsszavak:**  
**relációs séma**, **oszlopszerkezet**, **adattípus**, **megszorítás**

---

### 3.2 Adattípusok
**Rövid definíció:**  
Az adattípus meghatározza a tárolható érték formátumát és tartományát.

**Működési elv:**  
- Numerikus: `INTEGER`, `FLOAT`, stb.  
- Szöveges: `CHAR`, `VARCHAR`.  
- Dátum/idő: `DATE`, `TIMESTAMP` jellegű típusok.

**Egyszerű példa:**  
Telefonszámot gyakran `VARCHAR`-ban tárolunk, nem `INTEGER`-ben.

**Vizsgán fontos kulcsszavak:**  
**adattípus**, **INTEGER**, **VARCHAR**, **DATE**, **helyes típusválasztás**

---

## 4. Megszorítások (constraints)

### 4.1 Kulcs megszorítások
**Rövid definíció:**  
A kulcs megszorítások az egyediséget és kapcsolati integritást biztosítják.

**Működési elv:**  
- `PRIMARY KEY`: egyedi azonosító, nem NULL.  
- `FOREIGN KEY`: másik tábla kulcsára hivatkozás.  
- `UNIQUE`: egyediség biztosítása nem elsődleges kulcsként.

**Egyszerű példa:**  
`email` lehet `UNIQUE`, míg `id` a `PRIMARY KEY`.

**Vizsgán fontos kulcsszavak:**  
**PRIMARY KEY**, **FOREIGN KEY**, **UNIQUE**, **integritás**

---

### 4.2 Egyéb megszorítások
**Rövid definíció:**  
Ezek a megszorítások adatminőségi szabályokat kényszerítenek ki.

**Működési elv:**  
- `NOT NULL`: kötelező mező.  
- `CHECK`: értéktartomány vagy logikai feltétel.  
- `DEFAULT`: alapértelmezett érték.

**Egyszerű példa:**  
`CHECK(kor >= 18)` csak nagykorú értéket enged.

**Vizsgán fontos kulcsszavak:**  
**NOT NULL**, **CHECK**, **DEFAULT**, **adatvalidáció**

---

### 4.3 Referenciális integritás
**Rövid definíció:**  
A **[[referenciális integritás]]** biztosítja, hogy idegen kulcs ne mutasson nem létező sorra.

**Működési elv:**  
- Idegen kulcs szabályok kötik össze a táblákat.  
- Műveleti szabályok: `CASCADE`, `SET NULL`, `RESTRICT`.

**Egyszerű példa:**  
Ha szülősort törlünk `ON DELETE CASCADE` mellett, gyereksorok is törlődnek.

**Vizsgán fontos kulcsszavak:**  
**[[referenciális integritás]]**, **ON DELETE/UPDATE**, **CASCADE**, **RESTRICT**

---

## 5. DML – Adatmanipulációs nyelv

### 5.1 INSERT
**Rövid definíció:**  
Az `INSERT` új rekordokat visz be a táblába.

**Működési elv:**  
- Megadjuk céloszlopokat és értékeket.  
- Több sor is beszúrható egy utasítással.

**Egyszerű példa:**  
`INSERT INTO Hallgato(id, nev) VALUES (1, 'Kiss Anna');`

**Vizsgán fontos kulcsszavak:**  
**INSERT**, **rekord beszúrás**, **DML**

---

### 5.2 UPDATE
**Rövid definíció:**  
Az `UPDATE` meglévő rekord(ok) módosítására szolgál.

**Működési elv:**  
- `SET` adja meg az új értéket.  
- `WHERE` nélkül minden sor módosulhat.

**Egyszerű példa:**  
`UPDATE Hallgato SET atlag = 4.5 WHERE id = 1;`

**Vizsgán fontos kulcsszavak:**  
**UPDATE**, **SET**, **WHERE**, **tömeges módosítás veszélye**

---

### 5.3 DELETE
**Rövid definíció:**  
A `DELETE` rekordok törlésére használható feltétel alapján.

**Működési elv:**  
- `WHERE` feltétel szűri a törlendő sorokat.  
- Integritási szabályok befolyásolhatják a műveletet.

**Egyszerű példa:**  
`DELETE FROM Hallgato WHERE id = 1;`

**Vizsgán fontos kulcsszavak:**  
**DELETE**, **sor törlés**, **WHERE feltétel**, **FK-hatás**

---

## 6. Lekérdezések (SELECT)

### 6.1 Alap SELECT
**Rövid definíció:**  
A `SELECT` az adatok lekérdezésének alaputasítása.

**Működési elv:**  
- `SELECT` oszlopok, `FROM` forrástábla, `WHERE` szűrés.  
- Ez az SQL leggyakrabban használt része.

**Egyszerű példa:**  
`SELECT nev FROM Hallgato WHERE szak = 'Mérnökinformatikus';`

**Vizsgán fontos kulcsszavak:**  
**SELECT**, **FROM**, **WHERE**, **alap lekérdezés**

---

### 6.2 Szűrés
**Rövid definíció:**  
Szűrésnél feltételekkel válogatjuk ki a sorokat.

**Működési elv:**  
- Összehasonlító operátorok: `=`, `<`, `>`, `<=`, `>=`.  
- Mintakeresés: `LIKE`.  
- Halmaztagság: `IN`.

**Egyszerű példa:**  
`WHERE nev LIKE 'Kis%'` minden „Kis” kezdetű névre szűr.

**Vizsgán fontos kulcsszavak:**  
**szűrés**, **LIKE**, **IN**, **feltételes lekérdezés**

---

### 6.3 Rendezés
**Rövid definíció:**  
Az `ORDER BY` rendezi a lekérdezett sorokat.

**Működési elv:**  
- Növekvő (`ASC`) vagy csökkenő (`DESC`) sorrend adható meg.  
- Több oszlop szerint is rendezhetünk.

**Egyszerű példa:**  
`ORDER BY atlag DESC, nev ASC`

**Vizsgán fontos kulcsszavak:**  
**ORDER BY**, **ASC/DESC**, **rendezés**

---

### 6.4 Csoportosítás
**Rövid definíció:**  
A `GROUP BY` csoportonkénti összesítést tesz lehetővé.

**Működési elv:**  
- Azonos kulcsértékű sorok csoportot alkotnak.  
- Aggregáló függvények: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.

**Egyszerű példa:**  
`SELECT szak, COUNT(*) FROM Hallgato GROUP BY szak;`

**Vizsgán fontos kulcsszavak:**  
**GROUP BY**, **aggregáció**, **COUNT/SUM/AVG**

---

### 6.5 Csoport szűrés
**Rövid definíció:**  
A `HAVING` csoportszintű feltételt ad meg aggregáció után.

**Működési elv:**  
- `WHERE` sorokra, `HAVING` csoportokra szűr.  
- Gyakran aggregált kifejezéssel együtt használjuk.

**Egyszerű példa:**  
`HAVING COUNT(*) > 10` csak 10-nél több elemű csoportokat ad vissza.

**Vizsgán fontos kulcsszavak:**  
**HAVING**, **csoportszűrés**, **WHERE vs HAVING**

---

### 6.6 Összekapcsolás (JOIN)
**Rövid definíció:**  
A **[[JOIN]]** több tábla adatainak összekapcsolása kulcsfeltétel alapján.

**Működési elv:**  
- `INNER JOIN`: csak egyező sorok.  
- `LEFT JOIN`: bal oldali minden sor megmarad.  
- `RIGHT JOIN`: jobb oldali minden sor megmarad.  
- `ON` adja a kapcsolati feltételt.

**Egyszerű példa:**  
Hallgató neve + felvett kurzusok lekérdezése két vagy több tábla joinjával.

**Vizsgán fontos kulcsszavak:**  
**[[JOIN]]**, **INNER/LEFT/RIGHT**, **ON feltétel**, **táblakapcsolat**

---

### 6.7 Beágyazott lekérdezések
**Rövid definíció:**  
A **[[subquery]]** egy lekérdezésen belüli lekérdezés.

**Működési elv:**  
- Megjelenhet `WHERE`, `FROM`, `SELECT` részekben is.  
- Összetett szűrésekhez és köztes eredményekhez hasznos.

**Egyszerű példa:**  
`WHERE atlag > (SELECT AVG(atlag) FROM Hallgato)`

**Vizsgán fontos kulcsszavak:**  
**[[subquery]]**, **beágyazott SELECT**, **összetett feltétel**

---

## 7. Gyakorlati szempontok
**Rövid definíció:**  
SQL-ben a helyes lekérdezés mellett a teljesítményoptimalizálás is fontos.

**Működési elv:**  
- Indexek gyorsítják a keresést, de karbantartási költségük van.  
- Nagy tábláknál különösen fontos a jó JOIN és szűrési stratégia.  
- Lekérdezési terv (execution plan) elemzéssel javítható a teljesítmény.

**Egyszerű példa:**  
Gyakran szűrt oszlopra indexet téve jelentősen csökkenhet a válaszidő.

**Vizsgán fontos kulcsszavak:**  
**index**, **lekérdezés optimalizálás**, **teljesítmény**, **execution plan**

---

## + Vizsgán érdemes még megemlíteni
- **[[DDL]] vs [[DML]]** különbség röviden és példával.  
- **[[referenciális integritás]]** szerepe adatminőségben.  
- JOIN típusok különbsége és tipikus használat.  
- Aggregációs példa `GROUP BY` + `HAVING` párossal.

---

## Rövid szóbeli összefoglaló
Az SQL a relációs adatbázisok deklaratív nyelve. DDL-lel a szerkezetet kezeljük, például CREATE, ALTER, DROP utasításokkal, DML-lel pedig az adatot, például INSERT, UPDATE, DELETE és SELECT műveletekkel. A relációséma oszlopokból, adattípusokból és megszorításokból áll, amelyek biztosítják az adatok helyességét. Kulcsfontosságú a primary key, foreign key és a referenciális integritás. Lekérdezésnél alap a SELECT-FROM-WHERE, ehhez jön rendezés, csoportosítás, HAVING, JOIN és subquery. Gyakorlatban a teljesítmény miatt indexelés és lekérdezés-optimalizálás is fontos.

## Kulcsfogalmak
- [[SQL]]
- [[DDL]]
- [[DML]]
- [[CREATE]]
- [[ALTER]]
- [[PRIMARY KEY]]
- [[FOREIGN KEY]]
- [[referenciális integritás]]
- [[SELECT]]
- [[WHERE]]
- [[GROUP BY]]
- [[HAVING]]
- [[JOIN]]
- [[subquery]]
- [[index]]

## Tipikus vizsgakérdések
1. **Mi a különbség DDL és DML között?**  
   DDL a szerkezetet kezeli, DML az adatokat manipulálja/lekérdezi.

2. **Mire használjuk a CREATE és ALTER utasítást?**  
   CREATE új objektumot hoz létre, ALTER meglévőt módosít.

3. **Miért fontos a referenciális integritás?**  
   Megakadályozza, hogy idegen kulcs érvénytelen rekordra mutasson.

4. **Mi a különbség WHERE és HAVING között?**  
   WHERE sorokra, HAVING csoportokra szűr.

5. **Mit csinál az INNER JOIN?**  
   Csak az egyező kapcsolódó sorokat adja vissza.

6. **Mikor használunk subquery-t?**  
   Ha egy lekérdezés eredményét egy másik feltételében akarjuk használni.

7. **Mire jó az index?**  
   Gyorsítja a keresést/szűrést, de karbantartási költséggel jár.

## Minimum, amit tudni kell
- SQL deklaratív nyelv, fő részei: DDL és DML.  
- CREATE, ALTER, DROP alapjelentése.  
- PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL fogalma.  
- Referenciális integritás lényege és ON DELETE opciók említése.  
- INSERT, UPDATE, DELETE alapműveletek szerepe.  
- SELECT-FROM-WHERE alapszerkezet.  
- GROUP BY, HAVING és alap aggregáló függvények.  
- JOIN és subquery alapötlete.
