
## Funkcje agregujące

Wykonują obliczenia na wielu rekordach i zwracają jedną wartość dla zbioru całego zbioru danych lub dla każdej grupy danych.

|Funkcja		|Zastosowanie|
|---|---|
|COUNT()|Zlicza wiersze lub niepuste wartości w konkretnej kolumnie|
|SUM()|Oblicza sumę wartości liczbowych|
|AVG()|Oblicza średnią arytmetyczną|
|MIN()|Znajduje najmniejszą wartość|
|MAX()|Znajduje największą wartość|

### Funkcja COUNT()
* `COUNT(*)` - liczy wszystkie rekordy.
	* Przykład: ilu jest klientów.
* `COUNT(kolumna)` - liczy tylko rekordy, w których wskazana kolumna nie ma wartości NULL.
	* Przykład: ilu klientów ma podany adres e-mail.
* `COUNT(DISTINCT)` - liczy unikalne wartości.
	* Przykład: z ilu różnych miast pochodzą klienci.

## Grupowanie

`GROUP BY` grupuje wiersze, które mają takie same wartości w określonej kolumnie lub kolumnach. Następnie można zastosować funkcje agregujące do każdej grupy.

Dla tabeli `CUSTOMER`: `CUSTOMER_ID`, `NAME`, `CITY`
```SQL
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

W tej składni porządkuje zestaw wyników w grupy na podstawie wartości w kolumnie department.

### Grupowanie a filtrowanie
`WHERE` i `HAVING` służą do filtrowania danych, ale działają na różnych etapach przetwarzania zapytania.

|Cecha|WHERE|HAVING|
|---|---|---|
|Co filtruje?|Rekordy|Grupy rekordów|
|Zastosowanie|Filtrowanie danych przed grupowaniem|Filtrowanie danych po grupowaniu|
|Funkcje agregujące|Nie można używać|Można używać|
|Kolejność wykonania|Przed `GROUP BY`|Po `GROUP BY`|
|Przykład|`WHERE price > 1000`|`HAVING SUM(price) > 1000`|

```SQL
SELECT CITY, COUNT(*) AS LICZBA_KLIENTOW
FROM CUSTOMER
WHERE CITY IS NOT NULL	-- pomija klientów, dla których nie podano miasta
GROUP BY CITY			-- grupuje klientów według miasta
HAVING COUNT(*) > 5;	-- tylko te miasta, w których jest więcej niż 5 klientów
```

## Łączenie tabel

Klauzula `JOIN` służy do łączenia wierszy z dwóch lub więcej tabel na podstawie powiązanych kolumn.

### Rodzaje JOIN
* **INNER JOIN** - zwraca tylko te wiersze, które mają odpowiadające sobie rekordy w obu tabelach.
* **LEFT JOIN** - zwraca wszystkie wiersze z lewej tabeli oraz dopasowane wiersze z prawej tabeli.
* **RIGHT JOIN** - zwraca wszystkie wiersze z prawej tabeli oraz dopasowane wiersze z lewej tabeli.
* **CROSS JOIN** - zwraca iloczyn kartezjański tabel. Każdy wiersz tabeli1 jest łączony z każdym wierszem tabeli2.
* **SELF JOIN** - polega na połączeniu tabeli z samą sobą. Wykorzystuje się aliasy, żeby odróżnić dwa wystąpienia tej samej tabeli.
* **NATURAL JOIN** - łączy tabele automatycznie na podstawie kolumn o identycznych nazwach. Nie wymagania podawania warunku `ON`.

Dla tabeli:
* `CUSTOMER`: `CUSTOMER_ID`, `NAME`, `CITY`.
* `ORDERS`: `ORDER_ID`, `CUSTOMER_ID`, `TOTAL_PRICE`.

```SQL
-- Wszyscy klienci, również ci bez zamówień
SELECT CUSTOMER.NAME, ORDERS.ORDER_ID
FROM CUSTOMER
LEFT JOIN ORDERS
ON CUSTOMER.CUSTOMER_ID = ORDERS.CUSTOMER_ID;
```

## Kolejność składni zapytania

1. SELECT
2. FROM
3. JOIN
4. WHERE
5. GROUP BY
6. HAVING
7. ORDER BY
8. LIMIT
