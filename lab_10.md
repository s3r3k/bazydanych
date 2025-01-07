
> [!IMPORTANT]
> W trakcie.
### 1.
``` MySQL
SELECT imie, nazwisko, YEAR(data_urodzenia) AS rok_urodzenia FROM pracownik;
```

### 2.
``` MySQL
SELECT imie, nazwisko, YEAR(CURDATE()) - YEAR(data_urodzenia) AS wiek 
FROM pracownik;
```

### 3.
``` MySQL
SELECT d.nazwa AS dzial, COUNT(p.id_pracownika) AS liczba_pracownikow
FROM dzial d
LEFT JOIN pracownik p ON d.id_dzialu = p.dzial
GROUP BY d.id_dzialu;
```


### 4.
``` MySQL
SELECT k.nazwa_kategorii, COUNT(t.id_towaru) AS liczba_produktow
FROM kategoria k
LEFT JOIN towar t ON k.id_kategorii = t.kategoria
GROUP BY k.id_kategorii;
```

### 5.
``` MySQL
SELECT k.nazwa_kategorii, GROUP_CONCAT(t.nazwa_towaru SEPARATOR ', ') AS produkty
FROM kategoria k
LEFT JOIN towar t ON k.id_kategorii = t.kategoria
GROUP BY k.id_kategorii;
```

### 6.
``` MySQL
SELECT ROUND(AVG(pensja), 2) AS srednie_zarobki FROM pracownik;
```

### 7.
``` MySQL
SELECT ROUND(AVG(pensja), 2) AS srednie_zarobki
FROM pracownik
WHERE YEAR(CURDATE()) - YEAR(data_zatrudnienia) >= 5
```

### 8.1
``` MySQL
SELECT t.nazwa_towaru, COUNT(zp.id_zamowienia) AS liczba
FROM zamowienie_pozycja zp
JOIN towar t ON zp.towar = t.id_towaru
JOIN zamowienie z ON zp.id_zamowienia = z.id_zamowienia
WHERE z.status = 'zrealizowane'
GROUP BY t.id_towaru
ORDER BY liczba DESC
LIMIT 10;
```

### 8.2
``` MySQL
SELECT t.nazwa_towaru, SUM(zp.ilosc) AS laczna_ilosc
FROM zamowienie_pozycja zp
JOIN towar t ON zp.towar = t.id_towaru
JOIN zamowienie z ON zp.id_zamowienia = z.id_zamowienia
WHERE z.status = 'zrealizowane'
GROUP BY t.id_towaru
ORDER BY laczna_ilosc DESC
LIMIT 10;
```

### 9.
``` MySQL
SELECT z.id_zamowienia, SUM(zp.ilosc * zp.cena_jednostkowa) AS wartosc
FROM zamowienie z
JOIN zamowienie_pozycja zp ON z.id_zamowienia = zp.id_zamowienia
WHERE z.data_zamowienia BETWEEN '2017-01-01' AND '2017-03-31'
GROUP BY z.id_zamowienia;
```

### 10.
``` MySQL
SELECT p.imie, p.nazwisko, SUM(z.wartosc) AS suma_zamowien
FROM pracownik p
JOIN zamowienie z ON p.id_pracownika = z.pracownik
GROUP BY p.id_pracownika
ORDER BY suma_zamowien DESC;
```

### 11.
``` MySQL
SELECT d.nazwa AS dzial, 
       MIN(p.pensja) AS minimalna_pensja,
       MAX(p.pensja) AS maksymalna_pensja,
       ROUND(AVG(p.pensja), 2) AS srednia_pensja
FROM dzial d
LEFT JOIN pracownik p ON d.id_dzialu = p.dzial
GROUP BY d.id_dzialu;
```

### 12.
``` MySQL
SELECT k.pelna_nazwa, SUM(zp.ilosc * zp.cena_jednostkowa) AS wartosc_zamowienia
FROM klient k
JOIN zamowienie z ON k.id_klienta = z.klient
JOIN zamowienie_pozycja zp ON z.id_zamowienia = zp.id_zamowienia
GROUP BY z.id_zamowienia
ORDER BY wartosc_zamowienia DESC
LIMIT 10;
```

### 13.
``` MySQL
SELECT YEAR(z.data_zamowienia) AS rok, SUM(zp.ilosc * zp.cena_jednostkowa) AS przychod
FROM zamowienie z
JOIN zamowienie_pozycja zp ON z.id_zamowienia = zp.id_zamowienia
GROUP BY YEAR(z.data_zamowienia)
ORDER BY przychod DESC;
```

### 14.
``` MySQL
SELECT SUM(zp.ilosc * zp.cena_jednostkowa) AS suma_anulowanych
FROM zamowienie z
JOIN zamowienie_pozycja zp ON z.id_zamowienia = zp.id_zamowienia
WHERE z.status = 'anulowane';
```

### 15.
``` MySQL
SELECT k.miasto, COUNT(z.id_zamowienia) AS liczba_zamowien, 
       SUM(zp.ilosc * zp.cena_jednostkowa) AS suma_zamowien
FROM klient k
JOIN zamowienie z ON k.id_klienta = z.klient
JOIN zamowienie_pozycja zp ON z.id_zamowienia = zp.id_zamowienia
GROUP BY k.miasto;
```

