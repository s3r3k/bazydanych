> [!WARNING]
> DOKOŃCZYĆ NIE SPRAWDZAŁEM

## Zadanie 1.1

### 1.1
```
CREATE TABLE Kreatura AS SELECT * FROM wikingowie.Kreatura;
CREATE TABLE Uczestnicy AS SELECT * FROM wikingowie.Uczestnicy;
CREATE TABLE Etapy_Wyprawy AS SELECT * FROM wikingowie.Etapy_Wyprawy;
CREATE TABLE Sektor AS SELECT * FROM wikingowie.Sektor;
CREATE TABLE Wyprawa AS SELECT * FROM wikingowie.Wyprawa;
```

### 1.2
```
SELECT k.nazwa
FROM Kreatura k
LEFT JOIN Uczestnicy u ON k.idKreatury = u.idKreatury
WHERE u.idKreatury IS NULL;
```

### 1.3
```
SELECT w.nazwa AS nazwa_wyprawy, SUM(e.ilosc) AS suma_ekwipunku
FROM Wyprawa w
JOIN Uczestnicy u ON w.idWyprawy = u.idWyprawy
JOIN Ekwipunek e ON u.idKreatury = e.idKreatury
GROUP BY w.nazwa;
```
## Zadanie 2
### 2.1
```
SELECT w.nazwa AS nazwa_wyprawy, COUNT(u.idKreatury) AS liczba_uczestnikow,
GROUP_CONCAT(k.nazwa SEPARATOR ', ') AS uczestnicy
FROM Wyprawa w
JOIN Uczestnicy u ON w.idWyprawy = u.idWyprawy
JOIN Kreatura k ON u.idKreatury = k.idKreatury
GROUP BY w.nazwa;
```

### 2.2
```
SELECT w.nazwa AS nazwa_wyprawy, e.nazwa AS nazwa_etapu, s.nazwa AS nazwa_sektora, k.nazwa AS kierownik
FROM Etapy_Wyprawy e
JOIN Sektor s ON e.idSektora = s.idSektora
JOIN Wyprawa w ON e.idWyprawy = w.idWyprawy
JOIN Kreatura k ON w.idKierownika = k.idKreatury
ORDER BY w.data_poczatku, e.kolejnosc;
```

## Zadanie 3
### 3.1
```
SELECT s.nazwa AS nazwa_sektora, IFNULL(COUNT(e.idSektora), 0) AS liczba_odwiedzin
FROM Sektor s
LEFT JOIN Etapy_Wyprawy e ON s.idSektora = e.idSektora
GROUP BY s.nazwa;
```

### 3.2
```
SELECT k.nazwa, CASE WHEN COUNT(u.idWyprawy) > 0 THEN 'brał udział w wyprawie' 
ELSE 'nie brał udziału w wyprawie' 
END AS status
FROM Kreatura k
LEFT JOIN Uczestnicy u ON k.idKreatury = u.idKreatury
GROUP BY k.nazwa;
```

## Zadanie 4
### 4.1
```
SELECT w.nazwa AS nazwa_wyprawy, SUM(LENGTH(d.opis)) AS liczba_znakow
FROM Wyprawa w
JOIN Dziennik d ON w.idWyprawy = d.idWyprawy
GROUP BY w.nazwa
HAVING SUM(LENGTH(d.opis)) < 400;
```
### 4.2
```
SELECT w.nazwa AS nazwa_wyprawy, SUM(e.waga * e.ilosc) / COUNT(DISTINCT u.idKreatury) AS srednia_waga
FROM Wyprawa w
JOIN Uczestnicy u ON w.idWyprawy = u.idWyprawy
JOIN Ekwipunek e ON u.idKreatury = e.idKreatury
GROUP BY w.nazwa;
```
