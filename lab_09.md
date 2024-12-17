## Zadanie 1.1
### 1.1.1
```
SELECT nazwisko FROM pracownik ORDER BY nazwisko ASC;
```

### 1.1.2
```
SELECT imie, nazwisko, pensja FROM pracownik WHERE YEAR(data_urodzenia) > 1979;
```
### 1.1.3
```
SELECT * FROM pracownik WHERE pensja BETWEEN 3500 AND 5000;
```

### 1.1.4
```
SELECT towar FROM stan_magazynowy WHERE ilosc > 10;
```

### 1.1.5
```
SELECT * FROM towar 
WHERE nazwa_towaru LIKE '%A'
OR nazwa_towaru LIKE '%B'
OR nazwa_towaru LIKE '%C';
```

### 1.1.6
```
SELECT * FROM klient WHERE czy_firma = 0;
```

### 1.1.7
```
SELECT * FROM zamowienie ORDER BY data_zamowienia DESC
LIMIT 10;
```

### 1.1.8 
```
SELECT * FROM pracownik ORDER BY pensja ASC
LIMIT 5;
```

### 1.1.9
```
SELECT * FROM towar
WHERE nazwa_towaru NOT LIKE '%a'
ORDER BY cena_zakupu DESC
LIMIT 10;
```

### 1.1.10
```
--Chyba dobrze?
SELECT t.* FROM towar t
JOIN stan_magazynowy sm ON t.id_towaru = sm.towar
WHERE sm.jm = 'szt'
ORDER BY t.nazwa_towaru ASC,
t.cena_zakupu DESC;
```

### 1.1.11
```
CREATE TABLE towary_powyzej_100 AS
SELECT * FROM towar WHERE cena_zakupu >= 100;
```

### 1.1.12
> [!TIP]
> Można użyć TIMESTAMPDIFF
```
CREATE TABLE pracownik_50_plus LIKE pracownik;

INSERT INTO pracownik_50_plus SELECT * FROM pracownik
WHERE TIMESTAMPDIFF(YEAR, data_urodzenia, CURDATE()) >= 50;

-- Albo bez
INSERT INTO pracownik_50_plus
SELECT * FROM pracownik
WHERE YEAR(CURDATE()) - YEAR(data_urodzenia) >= 50;
```

## Zadanie 1.2
### 1.2.1
```
SELECT p.imie, p.nazwisko, p.nazwa
FROM pracownik p
JOIN dzial d ON p.dzial = d.id_dzialu;
```

### 1.2.2
```
SELECT t.nazwa_towaru, k.nazwa_kategorii, sm.ilosc
FROM towar t
JOIN kategoria k ON t.kategoria = k.id_kategorii
JOIN stan_magazynowy sm ON t.id_towaru = sm.towary
ORDER BY sm.ilosc DESC
```



 
