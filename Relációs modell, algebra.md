---
title: Relációs modell, algebra
publish: true
---

# Relációs modell, algebra

- logikai adat modell
- elméleti háttér az SQL-nek
- fizikailag független
	- módosítható, a logikai réteg megváltoztatásának szükségessége nélkül
- logikailag független
	- módosítható az alkalmazások felé nem destruktív módon
	- az adatbázis létrehozása utáni új követelményeknek megfelelés érdekében

| Kifejezés | Leírás |
| --- | --- |
| Reláció, Tábla | Egy entitásokból álló halmaz, ahol minden entitás (sor, vagy tuple) közös struktúrával rendelkezik. |
| Attribútum | Egy reláció névvel és típussal rendelkező oszlopa, ami egy a reláció összes elemében jelen lévő adathoz tartozik. |
| Tuple, Sor, Bejegyzés | Egy adathoz tartozó bejegyzés, ami rendelkezik a séma által meghatározott tulajdonságokkal. |
| Tartomány | Egy vagy több attribútum számára megengedett értékek halmaza. (1-100, szöveg, I/H, stb.) |
| Kulcs | Egy attribútum vagy attribútumok halmaza, amely egyedileg azonosít egy sort egy relációban. |
| Relációs adatbázis séma | Egy vagy több reláció séma, egy minden relációhoz |
| Relációs adatbázis példány | Egy vagy több reláció példány, egy minden relációhoz |

## Relációs algebra

### Alapműveletek

| Művelet | Szimbólum (Szimbólum neve) | Leírás | SQL Parancs | RA Formula |
| --- | --- | --- | --- | --- |
| Kiválasztás | σ (szigma) | Predikátumot kielégítő sorokat választ ki | `WHERE` | $\sigma_{\text{condition}}(R)$ |
| Projekció | π (pi) | Kiválaszt meghatározott oszlopokat a táblából, eredménye halmaz -> nincs duplikátum | `SELECT` | $\pi_{\text{attribute-list}}(R)$ |
| Descartes-szorzat | x (kereszt) | Két reláció sorait összefűzi, új relációt létrehozva | `CROSS JOIN` | $R \times S$ |
| Unió | ∪ (unió jel) | Két kompatibilis táblát egyesít | `UNION` | $R \cup S$ |
| Különbség | - (mínusz) | Két relációból visszaadja a csak az elsőben megtalálható sorokat | `EXCEPT` vagy `MINUS` | $R - S$ |

Relációs algebrában a halmaz eredményekben nem léteznek duplikátumok, azonban gyakorlatban, adatbázis rendszerekben a relációkat multihalmazoknak tekintjük.
Működés alapján ez a duplikátumokat alapértelmezés szerint eliminálhatja (`UNION`, `INTERSECT`, `EXCEPT`) ami viselkedés felülírható az `ALL` kulcsszóval, illetve megtarthatja (`SELECT`, `JOIN`). Kiválasztás eliminációval: `SELECT DISTINCT`

## Származtatott műveletek

| Művelet | Szimbólum (Szimbólum neve) | Leírás | SQL Parancs | RA Formula |
| --- | --- | --- | --- | --- |
| Természetes csatlakozás | - | Két táblázat sorait kombinálja egy közös oszlop alapján, hibára hajlamosít, implicit | `NATURAL JOIN` | $R \bowtie S$ |
| Theta csatlakozás | - | Két táblázat sorait kombinálja egy adott feltétel alapján | - | $R \bowtie_{\text{condition}} S$ |
| Equi csatlakozás | - | Egy speciális eset a természetes csatlakozásra, ahol az összes közös attribútum egyenlő | `EQUI JOIN` vagy `INNER JOIN` | $R \bowtie_{\text{condition}} S$ |
| Félig csatlakozás | - | Egy aszimmetrikus csatlakozás, ahol csak az első táblázat sorai jelennek meg | `SEMI JOIN` | $R \ltimes S$ or $R \rtimes S$ |
| Külső csatlakozás | - | Két táblázat sorait kombinálja úgy, hogy a hiányzó értékek `NULL`-ként jelennek meg | `OUTER JOIN` (`LEFT`, `RIGHT`, `FULL`) | $R \blacktriangleleft S$ vagy $R \blacktriangleright S$ vagy $R \bowtie S$ |
| Átnevezés | - | Átnevezi a reláció sémáját (reláció neve, attribútum nevek) | `AS` | $\rho_{\text{new-name(old-name)}}(R)$ |
| Hozzárendelés | - | Egy ideiglenes reláció változóhoz rendeli a relációs algebra kifejezés eredményét | `INTO` | $R := \text{expression}$ |
| Aggregáció | - | Aggregált számításokat végez egy oszlop értékein, mint például összeg, átlag, szám, min, max, stb. | `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` | $G_{\text{aggregation-function}}(R)$ |

## Relációs Algebra korlátai

- nem tud tranzitív klózt számolni (a -> b, b->c => a->c)
- hierarchiák, gráfok, geográfia, útvonal tervezés

PK és FK nem részei a relációs algebrának.
