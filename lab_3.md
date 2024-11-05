CREATE TABLE przetwory (
  id_przetworu INT PRIMARY KEY,
  rok_produkcji YEAR DEFAULT 2022,
  id_wykonawcy INT,
  zawartosc VARCHAR(255),
  dodatek VARCHAR(255) DEFAULT 'papryczka chilli',
  id_konsumenta INT,
  FOREIGN KEY (id_konsumenta) REFERENCES postac(id_postasci),
  FOREIGN KEY (id_wykonawcy) REFERENCES postac(id_postasci)
);

INSERT INTO przetwory (id_przetworu, rok_produkcji, id_wykonawcy, zawartosc, dodatek, id_konsumenta)
VALUES (1, 2023, 1, 'bigos', 'papryczka_chilli', 2);

INSERT INTO postac (id_postasci, nazwa, rodzaj, date_ur, wiek)
VALUES
      (4, 'Ragnar', 'Wiking', '1972-03-05', '21'),
      (5, 'Thor', 'Wiking', '1952-02-02', '21'),
      (6, 'Flokki', 'Wiking', '1920-05-01', '21'),
      (7, 'Rob', 'Wiking', '1950-08-05', '21'),
      (8, 'Larry', 'Wiking', '192-09-09', '21');
      

CREATE TABLE statek (
  nazwa_statku VARCHAR(100) PRIMARY KEY,
  rodzaj_statku ENUM('drakkar', 'barka', 'katamaran'),
  data_wodowania DATE,
  max_ladownosc INT UNSIGNED
);

INSERT INTO statek (nazwa_statku, rodzaj_statku, data_wodowania, max_ladownosc)
VALUES
      ('Santa Maria', 'drakkar', '2023-05-06', 5000),      
      ('Titanic', 'katamaran', '2023-06-03', 5000);

ALTER TABLE postac
ADD COLUMN funcja VARCHAR(50);

UPDATE postac
SET funcja = 'kapitan'
WHERE nazwa = 'Bjorn';

ALTER TABLE postac
ADD COLUMN nazwa_statku VARCHAR(100),
ADD FOREIGN KEY (nazwa_statku) REFERENCES statek(nazwa_statku);

UPDATE postac SET nazwa_statku = 'Missouri' WHERE nazwa = 'Bjorn';
UPDATE postac SET nazwa_statku = 'Victory' WHERE nazwa = 'Drozd';
UPDATE postac SET nazwa_statku = 'Wilhlem Gustloff' WHERE nazwa = 'Ragnar';
UPDATE postac SET nazwa_statku = 'Orzel' WHERE nazwa = 'Thor';
UPDATE postac SET nazwa_statku = 'Fram' WHERE nazwa = 'Flokki';
UPDATE postac SET nazwa_statku = 'Myflower' WHERE nazwa = 'Rob';
UPDATE postac SET nazwa_statku = 'PapaBarka' WHERE nazwa = 'Larry';

DELETE FROM izba WHERE nazwa_izby = 'Spizarnia';

DROP TABLE izba;
