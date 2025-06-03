# 🛠 SQL Cheat Sheet

## 📌 Allgemeine Syntax

```sql
SELECT spalte1, spalte2
FROM tabelle
WHERE bedingung
ORDER BY spalte DESC
LIMIT anzahl OFFSET start;
```

## 🎯 JOIN-Operationen

| JOIN-Typ   | Beschreibung                              | Beispiel                                      |
| ---------- | ----------------------------------------- | --------------------------------------------- |
| INNER JOIN | Nur Übereinstimmungen beider Tabellen     | `SELECT * FROM A INNER JOIN B ON A.id = B.id` |
| LEFT JOIN  | Alle Datensätze von A, plus Matches aus B | `SELECT * FROM A LEFT JOIN B ON A.id = B.id`  |
| RIGHT JOIN | Alle Datensätze von B, plus Matches aus A | `SELECT * FROM A RIGHT JOIN B ON A.id = B.id` |
| FULL JOIN  | Alle Datensätze von A und B               | `SELECT * FROM A FULL JOIN B ON A.id = B.id`  |

### Beispiel INNER JOIN

```sql
SELECT customers.name, orders.order_date
FROM customers
INNER JOIN orders ON customers.id = orders.customer_id;
```

## 🗃 Subqueries und IN SELECT

```sql
SELECT product_name
FROM products
WHERE category_id IN (
    SELECT id FROM categories WHERE category_name = 'Electronics'
);
```

## 🔍 COUNT()-Funktion

* Gesamtzahl der Datensätze:

```sql
SELECT COUNT(*) FROM students;
```

* Anzahl Datensätze mit nicht-null Werten in einer Spalte:

```sql
SELECT COUNT(score) FROM students;
```

* Anzahl einzigartiger Werte:

```sql
SELECT COUNT(DISTINCT score) FROM students;
```

## 🔢 Aggregatfunktionen

```sql
SELECT AVG(preis), SUM(preis), MAX(preis), MIN(preis)
FROM produkte
GROUP BY kategorie
HAVING AVG(preis) > 100;
```

## 🚧 Operatoren

| Vergleichsoperatoren | Bedeutung                     |
| -------------------- | ----------------------------- |
| `=`                  | gleich                        |
| `!=`, `<>`           | nicht gleich                  |
| `>`                  | größer als                    |
| `<`                  | kleiner als                   |
| `>=`, `<=`           | größer/gleich, kleiner/gleich |

* Logische Operatoren: `AND`, `OR`, `NOT`

## 📆 Datum & Zeit Funktionen

```sql
SELECT NOW(); -- Aktuelle Zeit
SELECT DATE_ADD(NOW(), INTERVAL 1 DAY); -- morgen
SELECT DATE_FORMAT(NOW(), '%Y-%m-%d'); -- Datum formatieren
```

## 🔑 Transaktionen

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT; -- oder ROLLBACK
```

## ⚡ Fortgeschrittene Funktionen

* **Common Table Expression (CTE)**:

```sql
WITH top_customers AS (
    SELECT customer_id, SUM(amount) AS total
    FROM orders
    GROUP BY customer_id
)
SELECT * FROM top_customers WHERE total > 1000;
```

* **Fensterfunktionen**:

```sql
SELECT product_name,
       RANK() OVER (ORDER BY price DESC) as price_rank
FROM products;
```

## 🔐 Verschlüsselung & Komprimierung (MySQL)

```sql
SELECT AES_ENCRYPT('Text', 'key');
SELECT AES_DECRYPT(column, 'key');
```

## 🔧 Sonstige nützliche Funktionen

* String-Funktionen:

  ```sql
  SELECT CONCAT(vorname, ' ', nachname) FROM personen;
  ```

* Mathematische Funktionen:

  ```sql
  SELECT ROUND(preis, 2) FROM produkte;
  ```

## 📝 Beispielabfragen

* Einfache SELECT-Abfrage:

```sql
SELECT * FROM customers;
```

* SELECT mit WHERE und ORDER:

```sql
SELECT name FROM customers
WHERE country = 'Germany'
ORDER BY name;
```

* SELECT mit GROUP BY:

```sql
SELECT category, COUNT(*) FROM products
GROUP BY category;
```

## 📚 Quellen

* ANSI SQL Standard
* PostgreSQL, MySQL, MSSQL Dokumentationen
* Praktische Nutzungserfahrung
