## Zadanie 1
### a

> [!NOTE]
> Tu by wypadalo uzyc LIMIT...

```
DELETE FROM postac 
WHERE id_postasci IN(
SELECT id_postasci FROM postac
WHERE nazwa != 'Bjorn'
ORDER BY wuej DESC
LIMIT 2
);
```


```SELECT * FROM postac ORDER BY wiek DESC;```

```
DELETE FROM postac WHERE nazwa = 'Thor';
DELETE FROM postac WHERE nazwa = 'Ragnar';
```

### b

```
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_1;
ALTER TABLE przetwory DROP FOREIGN KEY przetwory_ibfk_2;
```

```
ALTER TABLE postac CHANGE id_postasci id_postasci int;
```
I w koncu primary key
```
ALTER TABLE postac DROP PRIMARY KEY
```
## Zadanie 2
### a
```
ALTER TABLE postac
ADD pesel VARCHAR(11) NOT NULL PRIMARY KEY;
```
### b
```
ALTER TABLE postac
MODIFY rodzaj ENUM('kobieta', 'wiking', 'ptak', 'syrena');
```
### c
```
INSERT INTO postac (nazwa)
VALUES ('Gertruda Nieszczera');
```

## Zadanie 3
### a
```
UPDATE postac
SET nazwa_statku = (SELECT nazwa_statku FROM postac WHERE nazwa = 'Bjorn')
WHERE nazwa LIKE '%a%';
```
### b
```
UPDATE postac
SET max_ladownosc = max_ladownosc = 0.7
WHERE YEAR(data_wodowania) BETWEEN 1901 AND 2000;
```
### c
```
ALTER TABLE postac
ADD CONSTRAINT sprawdz_wiek CHECK (wiek <= 1000);
```

## Zadanie 4

### a
```
INSERT INTO postac (nazwa)
VALUES ('Loko')
```

### b
```
CREATE TABLE marynarz LIKE postac;
INSERT INTO marynarz select *
FROM postac WHERE STATEK IS NOT NULL;
```

ALBO

```
CREATE TABLE marynarz AS
SELECT * FROM WHERE STATEK IS NOT NULL;
```

### c
```
INSERT INTO marynarz 
SELECT * FROM postac
WHERE STATEK IS NOT NULL;
```

### d
```
ALTER TABLE marynarz
ADD PRIMARY KEY (id_postasci)
ADD FOREIGN KEY (nazwa_statku) REFERENCES statek(nazwa_statku);
```

## Zadanie 5
### a
```
UPDATE postac
SET nazwa_statku = NULL;
```

### b
```
DELETE FROM postac
WHERE rodzaj = 'wiking'
LIMIT 1;
```


ALBO (bo limit nie dziala?)

```
DELETE FROM postac
WHERE nazwa = 'Larry'
```

### c
```
DELETE FROM statek;
```

### d
```
DROP TABLE statek;
```
### e
```
CREATE TABLE zwierz (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nazwa VARCHAR(255),
  wiek INT
);
```
### f
```
INSERT INTO zwierz (nazwa, wiek)
SELECT nazwa, wiek FROM postac
WHERE rodzaj NOT IN ('wiking', 'kobieta', 'ptak');
```
> [!NOTE]
> Chyba ze przegapiłem zeby dodac zwierz do tabeli postac w rodzaju..
