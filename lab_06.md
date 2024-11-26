> [!NOTE]
> DOKOŃCZYĆ. WSZYSTKO NA BRUDNO. NIE SPRAWDZANE


```
--1.1
SELECT AVG(waga) AS srednia_waga_wikingow FROM kreatura WHERE rodzaj = 'wiking';

--1.2
SELECT rodzaj, AVG(waga) AS srednia_waga, COUNT(*) from kreatura GROUP BY rodzaj;
-- count oblicza liczbe kreatur

--1.3
SELECT rodzaj, AVG(YEAR(now())) - YEAR(dataurodzenia) AS sredni_wiek;
--Działa też z CURDATE()

--2.1
SELECT rodzaj, SUM(waga) AS suma_wag FROM zasoby GROUP BY rodzaj;

--2.2
SELECT nazwa, AVG(waga) AS srednia_waga FROM zasoby GROUP BY nazwa
HAVING COUNT(*) >=4 AND SUM(waga) > 10;

--2.3
SELECT rodzaj, COUNT(DISTINCT nazwa) AS liczba_nazw FROM zasoby
GROUP BY rodzaj HAVING MIN(ilosc) > 1;

--3.1
--Używamy aliasów zamiast kreatura.nazwa to k.nazwa do odwołania się do konkretnych tabel 
SELECT k.nazwa AS nazwa_kreatury, COUNT(e.idZasobu) AS ilosc_zasobow
FROM kratura k
JOIN ekwipunek e ON k.idKreatury = e.idKreatury
GROUP BY k.nazwa;

--3.2
--Używamy GROUP_CONCAT do łączenia nazwy zasobów w jedną kolumnę. Oddzielamy ', ' jako separator..
SELECT k.nazwa AS nazwa_kreatury, GROUP_CONCAT(z.nazwa SEPARATOR ', ') AS zasoby
FROM kreatura
JOIN ekwipunek e ON k.idKreatury = e.idKreatury
JOIN zasob z ON e.idZasobu = z.idZasobu
GROUP BY k.nazwa;

--3.3
-- LEFT JOIN łączy kreatury z ekwipunkiem i zachowuje kreatury bez ekwipunku
SELECT nazwa FROM kreatura k
LEFT JOIN ekwipunek e ON k.idKreatury = e.idKreatury
WHERE e.idKreatury IS NULL;

--4.1
SELECT k.nazwa AS wiking, z.nazwa AS zasob
FROM kreatura k
NATURAL JOIN ekwipunek e
NATURAL JOIN zasoby z
WHERE k.rodzaj = 'wiking' AND YEAR(k.dataurodzenia) BETWEEN 1670 AND 1679;

--4.2
SELECT k.nazwa, k.dataurodzenia
FROM kreatura k
JOIN ekwipunek e ON k.idKreatury = e.idKreatury
JOIN zasob z ON e.idZasobu = z.idZasobu
WHERE z.rodzaj = 'zywnosc'
ORDER BY k.dataurodzenia DESC
LIMIT 5
--OMG

--4.3
SELECT k1.nazwa AS kreatura1, k2.nazwa AS kreatura2
FROM kreatura k1
JOIN kreatura k2 ON ABS(k1.idKreatury - k2.idKreatury) = 5;
```
