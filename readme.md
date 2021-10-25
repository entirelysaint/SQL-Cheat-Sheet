# SQL Bazy Danych Streszczenie

> Co to jest relacyjna baza danych?

- Relacyjne bazy danych: Bazy danych, które organizują informacje w jedną lub więcej tabel.
- Tabela: zbiór danych zorganizowanych w wiersze i kolumny.
- Kolumny + Wiersze: Informacje są przechowywane w grupach specyficznych dla typu.

> Wspólna składnia SQL
> 'CREATE TABLE table_name (
> column_1 data_type,
> column_2 data_type,
> column_3 data_type
> );'

- CREATE TABLE: To jest klauzula. Klauzule wykonują określone zadania w SQL.
- table_name to nazwa tabeli, do której odnosi się klauzula / polecenie.
- ( ): Jest parametrem, który może być listą kolumn, typów danych lub wartości.

# Create

Instrukcje Create pozwalają na utworzenie nowej tabeli w bazie danych.

'CREATE TABLE family (
id INTEGER,
name TEXT,
age INTEGER
);'

### Insert

Instrukcje Insert wstawia nowy wiersz do tabeli.
'INSERT INTO family
(id, name, age)
VALUES (1, 'Dariusz Nowak', 26);'

### Select

Instrukcje Select służą do pobierania danych z bazy danych. \* to specjalny znak wieloznaczny, który pozwala wybrać każdą kolumnę bez nazywania ich wszystkich.
'SELECT \* FROM family;'
'SELECT name FROM family;'

### Alter

Instrukcja alter table dodaje nową kolumnę do tabeli.
NULL to specjalna wartość w SQL, która reprezentuje brakujące lub nieznane dane.

'ALTER TABLE family
ADD COLUMN twitter_handle TEXT;'

### Update

Instrukcja aktualizacji edytuje wiersz w tabeli.

'UPDATE family
SET twitter_handle = '@andrzej13'
WHERE id = 4;'

### Delete

Instrukcja delete from usuwa jeden lub więcej wierszy z tabeli.

'DELETE FROM family WHERE twitter_handle IS NULL;'

### Ograniczenia

Ograniczenia mogą być użyte, aby poinformować bazę danych, aby odrzuciła wstawione dane, które nie spełniają określonego ograniczenia.

'CREATE TABLE family ( id INTEGER PRIMARY KEY, name TEXT UNIQUE, date_of_birth TEXT NOT NULL, date_of_death TEXT DEFAULT 'Not Applicable' );'

- Klucz podstawowy: kolumny mogą służyć do jednoznacznej identyfikacji wiersza.
- Unikalne: kolumny mają inną wartość dla każdego wiersza. Zauważ, że możesz mieć więcej niż jedną unikatową kolumnę w tabeli, nie więcej niż jeden taki sam klucz podstawowy.

## Podsumowanie

- CREATE TABLE tworzy nową tabelę.
- INSERT INTO dodaje nowy wiersz do tabeli.
- SELECT zapytania o dane z tabeli.
- ALTER TABLE zmienia istniejącą tabelę.
- UPDATE edytuje wiersz w tabeli.
- DELETE FROM usuwa wiersze z tabeli.

# Zapytania

> Zapytania umożliwiają SQL komunikowanie się z bazą danych poprzez zadawanie pytań, a zestaw wyników zwraca dane istotne dla pytania.

## Select

**SELECT** column_names **FROM** table_name;
'SELECT name, genre FROM movies;'

## As

Umożliwia zmianę nazwy kolumny lub tabeli za pomocą aliasu.
'SELECT name AS 'Titles' FROM movies;'

## Distinct

'SELECT DISTINCT genre FROM movies;'

## Where

Umożliwia SQL ograniczanie wyników zapytań.
'SELECT \* FROM movies WHERE year > 2014;'

### LIKE

Może służyć do porównywania podobnych wartości. W przypadku użycia z where like można użyć do znalezienia określonego wzorca, podobnego do wyrażeń regularnych, jak nie jest rozróżniana wielkość liter.

**Podkreślenia**
Podkreślenia można używać w przypadku znaków wieloznacznych.
'SELECT \* FROM movies WHERE name LIKE 'Se_en';'

**Z procentem**
Znak procentu to kolejny znak wieloznaczny, który odpowiada zero lub większej liczbie brakujących liter we wzorcu.
'SELECT \* FROM movies WHERE name LIKE 'the %';'

### Is NULL

NULL jest używany jako symbol zastępczy brakujących wartości.
'SELECT name FROM movies WHERE imdb_rating IS NULL;'

### Between

Używane w klauzuli WHERE do filtrowania wyniku w określonym zakresie.

- BETWEEN dwie litery nie obejmują drugiej litery.
- BETWEEN dwie liczby zawierają drugą liczbę.
  'SELECT _ FROM movies WHERE name BETWEEN 'D' AND 'G';'
  'SELECT _ FROM movies WHERE year BETWEEN 1970 AND 1979;'

### And

Jest to sposób na łańcuchowanie i łączenie wielu warunków w klauzuli WHERE.
'SELECT \* FROM movies WHERE year < 1985 AND genre is 'horror';'

### Or

Może służyć do łączenia warunków, ale tylko jeden warunek musi być prawdziwy.
'SELECT \* FROM movies WHERE genre is 'romance' OR genre = 'comedy';'

## Order By

Przydatne do wykazu danych.
'SELECT name, year, imdb_rating FROM movies ORDER BY imdb_rating DESC;'

## Limit

Ogranicz liczbę wierszy w wyniku. Jest to dobre, gdy dany stół jest duży.
'SELECT \* FROM movies ORDER BY imdb_rating DESC LIMIT 3;'

## Case

Jest to podobne do instrukcji switch, która modyfikuje dane wyjściowe z zapytania.
'SELECT name,
CASE
WHEN genre = 'romance' or genre = 'comedy'
THEN 'Chill'
ELSE 'Intense'
END AS 'Mood'
FROM movies;'

## Podsumowanie

- SELECT to klauzula, której używamy za każdym razem, gdy chcemy uzyskać informacje z bazy danych.
- AS zmienia nazwę kolumny lub tabeli.
- DISTINCT zwracać unikalne wartości.
- WHERE to popularne polecenie, które pozwala filtrować wyniki zapytania na podstawie określonych przez Ciebie warunków.
- LIKE i BETWEEN są operatorami specjalnymi.
- AND i OR łączy wiele warunków.
- ORDER BY sortuje wynik.
- LIMIT określa maksymalną liczbę wierszy, które zwróci zapytanie.
- CASE tworzy różne wyniki.

# Funkcje agregujące

> Obliczenia wykonywane na wielu wierszach tabeli.

## Wspólne funkcje

- COUNT(): 'SELECT COUNT(star) FROM fake_apps;' | 'SELECT COUNT(star) FROM fake_apps WHERE price = 0;'
- SUM()
- MAX()/ MIN()
- AVG(): 'SELECT ROUND(AVG(price), 2) FROM fake_apps;'

## Group By

Zagregowane dane o określonych cechach.
'SELECT price, COUNT(star)
FROM fake_apps
WHERE downloads > 20000
GROUP BY price;'

## Having

Filtruj, które grupy należy uwzględnić, a które wykluczyć.
'SELECT price,
ROUND(AVG(downloads)),
COUNT(star)
FROM fake_apps
GROUP BY price
HAVING COUNT(star) > 10;'

## Podsumowanie

- COUNT(): policz liczbę rzędów.
- SUM(): sumuje wartości w kolumnie
- MAX()/MIN(): największa/najmniejsza wartość.
- AVG(): średnia wartości w kolumnie.
- GROUP BY to klauzula używana z funkcjami agregującymi do łączenia danych z co najmniej jednej kolumny.
- HAVING ograniczyć wyniki zapytania na podstawie właściwości zagregowanej.

# Wiele tabel

> SQL może obsługiwać dane i zapytania w wielu tabelach.

## Join

Używane żeby łączyć tabele.
'SELECT \*
FROM orders
JOIN subscriptions
ON orders.subscription_id = subscriptions.subscription_id;

SELECT \*
FROM orders
JOIN subscriptions
ON orders.subscription_id = subscriptions.subscription_id
WHERE subscriptions.description = 'Fashion Magazine';'

### Połączenie wewnętrzne

'SELECT COUNT(start)
FROM newspaper;

SELECT COUNT(star)
FROM online;

SELECT COUNT(star)
FROM newspaper
JOIN online
ON newspaper.id = online.id;'

### Dołącz do lewej

'SELECT \*
FROM newspaper
LEFT JOIN online
ON newspaper.id = online.id;

SELECT \*
FROM newspaper
LEFT JOIN online
ON newspaper.id = online.id
WHERE online.id IS NULL;'

## Klucz podstawowy a klucz obcy

**Podstawowy**
Klucze podstawowe mają kilka wymagań:

- Żadna z wartości nie może być NULL.
- Każda wartość musi być unikalna (tzn. nie możesz mieć dwóch klientów o tym samym identyfikatorze klienta w tabeli Klienci).
- Tabela nie może mieć więcej niż jednej kolumny klucza podstawowego.

### Połączenie krzyżowe

'WITH previous_query AS (
SELECT customer_id,
COUNT(subscription_id) AS 'subscriptions'
FROM orders
GROUP BY customer_id
)
SELECT customers.customer_name,
previous_query.subscriptions
FROM previous_query
JOIN customers
ON previous_query.customer_id = customers.customer_id;'

## Streszczenie

- JOIN połączy wiersze z różnych tabel, jeśli warunek złączenia jest spełniony.
- LEFT JOIN zwróci każdy wiersz w lewej tabeli, a jeśli warunek złączenia nie zostanie spełniony, do wypełnienia kolumn z prawej tabeli zostaną użyte wartości NULL.
- Klucz podstawowy to kolumna, która podaje unikalny identyfikator wierszy w tabeli.
- Klucz obcy to kolumna zawierająca klucz podstawowy do innej tabeli.
- CROSS JOIN pozwala nam połączyć wszystkie wiersze jednej tabeli ze wszystkimi wierszami innej tabeli.
- UNION układa jeden zestaw danych na drugim.
- WITH pozwala nam zdefiniować jedną lub więcej tabel tymczasowych, które mogą być użyte w ostatecznym zapytaniu.
