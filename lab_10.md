> [!IMPORTANT]
> W trakcie.
```
       /// //_.-'    .-/";  `        ``<._  ``.''_ `. / // /  W każdy wtorek około 15:10
      ///_.-' _..--.'_    \                    `( ) ) // //   ekscytuje mnie myśl,
      / (_..-' // (< _     ;_..__               ; `' / ///    o dokończeniu tych zadań
       / // // //  `-._,_)' // / ``--...____..-' /// / //     w domu.
```

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
``` MySQL
JOIN zamowienie z ON k.id_klienta = z.klient
JOIN zamowienie_pozycja zp ON z.id_zamowienia = zp.id_zamowienia
GROUP BY k.miasto;
```

