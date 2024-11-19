```
                   ~.                       
            Ya...___|__..ab.     .   .  
             Y88b  \88b  \88b   (     )  
              Y88b  :88b  :88b   `.oo'   
              :888  |888  |888  ( (`-'          LAB 5                Bjorn wśród fal tonie,
     .---.    d88P  ;88P  ;88P   `.`.           19.11.2024           okręt zniknął jak cień snu,
    / .-._)  d8P-"""|"""'-Y8P      `.`.         Jakub Serowski       wiatr niesie skargę...
   ( (`._) .-.  .-. |.-.  .-.  .-.   ) )         
    \ `---( O )( O )( O )( O )( O )-' /  
     `.    `-'  `-'  `-'  `-'  `-'  .' CJ 
       `---------------------------'
```

## Zadanie 1

### 1.1
```
CREATE TABLE kreatura AS SELECT * FROM wikingowie.kreatura;
CREATE TABLE zasob AS SELECT * FROM wikingowie.zasob;
CREATE TABLE ekwipunek AS SELECT FROM wikingowie.ekwipunek;
```

### 1.2
```
SELECT * FROM zasob;
```

### 1.3
```
SELECT * FROM zasob WHERE typ = 'jedzenie';
```

### 1.4
```
SELECT idZasobu, ilosc FROM ekwipunek WHERE idKreatury IN (1, 2, 5);
```

> [!TIP]
> Jesli nie dziala IN (bo stara wersja) to
```
SELECT idZasobu, ilosc FROM ekwipunek WHERE idKreatury = 1 OR idKreatury = 2 OR idKreatury = 5;
```


## Zadanie 2

### 2.1
```
SELECT * FROM kreatura WHERE rodzaj != 'wiedźma' AND ciezar >= 50;
```

### 2.2
```
SELECT * FROM zasob WHERE waga BETWEEN 2 AND 5;
```

### 3.3
```
SELECT * FROM kreatura WHERE nazwa LIKE '%or%' AND ciezar BETWEEN 30 AND 70;
```


## Zadanie 3

> [!TIP]
> Do poniższych możemy też użyć TOP albo ROW_NUMBER()

```
### 3.1
SELECT * from zasob WHERE MONTH(dataPozyskania) IN (7,8);
```

### 3.2
```
SELECT * FROM zasob WHERE rodzaj IS NOT NULL ORDER BY waga;
```

### 3.3
```
SELECT * FROM kreatura ORDER BY dataUrodzenia LIMIT 5;
```


## Zadanie 4

### 4.1
```
SELECT DISTINCT rodzaj FROM zasob;
```

### 4.2

> [!IMPORTANT]
> Z uzyciem CONCAT (łączenie dwóch lub więcej ciągów w jeden ciąg)

```
SELECT CONCAT(nazwa, ' - ', rodzaj) AS nazwa_rodzaj FROM kreatura WHERE rodzaj LIKE 'wi%';
```

### 4.3
```
SELECT nazwa, rodzaj, ilosc * waga AS calkowita_waga FROM zasob WHERE YEAR(dataPozyskania) BETWEEN 2000 AND 2007;
```

## Zadanie 5

### 5.1
```
SELECT nazwa,
      waga * ilosc * 0.7 as masa_netto,
      waga * ilosc * 0.3 as waga_odpadow
FROM zasob WHERE typ = 'jedzenie';
```

### 5.2
```
SELECT * FROM zasob WHERE rodzaj IS NULL;
```

### 5.3
```
SELECT DISTINCT rodzaj FROM zasob
WHERE nazwa LIKE 'Ba%' OR nazwa LIKE '%os'
ORDER BY rodzaj;
```
