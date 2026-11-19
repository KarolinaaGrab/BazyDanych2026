## CREATE TABLE AS SELECT

Pozwala utworzyć nową tabelę na podstawie wyników zapytania SELECT. Nowa tabela zostaje wypełniona danymi zwróconymi przez zapytanie.

```sql
CREATE TABLE nowa_tabela AS
SELECT *
FROM stara_tabela;
```

## SELECT

Służy do pobierania danych z tabeli.

```sql
SELECT kolumna1, kolumna2
FROM tabela;
```

- `SELECT *` – pobiera wszystkie kolumny.
- Można podać konkretne kolumny, aby wyświetlić tylko wybrane dane.

## WHERE

Służy do filtrowania wierszy - wybierania rekordów spełniających określony **warunek**.

```sql
SELECT *
FROM tabela
WHERE warunek;
```

## Łączenie warunków

- `AND` – wszystkie warunki muszą być spełnione.
- `OR` – przynajmniej jeden warunek musi być spełniony.

```sql
WHERE warunek1 AND warunek2;
WHERE warunek1 OR warunek2;
```

### Operatory porównania

| Operator | Znaczenie |
|---|---|
| `=` | równe |
| `<>` lub `!=` | różne |
| `>` | większe |
| `<` | mniejsze |
| `>=` | większe lub równe |
| `<=` | mniejsze lub równe |

## BETWEEN

Wybiera wartości z określonego przedziału. Wartości graniczne również są uwzględniane.
Można stosować do typów danych liczbowych, dat lub typów tekstowych.

```sql
SELECT kolumna1
FROM tabela
WHERE kolumna BETWEEN wartosc1 AND wartosc2;
```

`NOT BETWEEN` – wybiera wartości spoza określonego przedziału (wartości graniczne również wykluczane).

## IN

Sprawdza czy wartość znajduje się na podanej liście.
Operator IN zastępuje wiele warunków połączonych przez `OR`.

```sql
WHERE kolumna IN (wartosc1, wartosc2, wartosc3);
```

`NOT IN` – wyklucza podane wartości.

## LIKE

Służy do wyszukiwania tekstów pasujących do wzorca.

| Wzorzec | Znaczenie |
|---|---|
| `'A%'` | zaczyna się od A |
| `'%A'` | kończy się na A |
| `'%abc%'` | zawiera abc |
| `'a_c'` | a, jeden dowolny znak, c |

Symbole wieloznaczne:
- `%` – zastępuje dowolną liczbę znaków (także zero).
- `_` – zastępuje dokładnie jeden dowolny znak.

## NULL

NULL oznacza brak wartości. Nie należy używać `= NULL` ani `<> NULL`.

```sql
WHERE kolumna IS NULL;

WHERE kolumna IS NOT NULL;
```

## DISTINCT

Instrukcje `SELECT DISTINCT` stosuje się, gdy chcemy mieć unikalne wartości.

```sql
SELECT DISTINCT kolumna
FROM tabela;
```

## ORDER BY

Sortuje wyniki według wybranej kolumny.

```sql
ORDER BY kolumna [ASC|DESC];
```

Gdzie:
- `ASC` – sortowanie rosnące (domyślne) (od najmniejszej do największej wartości, od A do Z).
- `DESC` – sortowanie malejące (od największej do najmniejszej wartości, od Z do A).

Można sortować według kilku kolumn:

```sql
ORDER BY kolumna1 ASC, kolumna2 DESC;
```

Najpierw sortuje po kolumnie 1 rosnąco, następnie po kolumnie 2 malejąco. Jeżeli wartości w kolumnie 1 są takie same, sortuje je według kolumny 2.

## LIMIT

Ogranicza liczbę zwracanych rekordów.

```sql
SELECT *
FROM tabela
LIMIT 10;
```

## AS - alias

Pozwala nadać kolumnie lub tabeli tymczasową nazwę (na czas wykonywania danego zapytania).

```sql
SELECT kolumna AS nowa_nazwa_kolumny
FROM tabela;
```

## CONCAT()

Funkcja CONCAT `CONCAT()` służy do łączenia dwóch lub więcej ciągów znaków w jeden.

```sql
SELECT CONCAT(kolumna1, ' ', kolumna2)
FROM tabela;
```

## Funkcje na typie daty

- `YEAR()` – wyciąga rok
- `MONTH()` – wyciąga miesiąc
- `DAY()` – wyciąga dzień

```sql
SELECT YEAR(kolumna_daty)
FROM tabela;
```

## Kolejność składni zapytania (poznane dotychczas elementy)

```sql
SELECT kolumny
FROM tabela
WHERE warunki
ORDER BY kolumna
LIMIT liczba;
```
