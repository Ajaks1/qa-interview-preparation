## 12. Базы данных

### 12.1. Основные операции SQL

#### CRUD-операции
- **SELECT** - выборка данных (пример: `SELECT * FROM users WHERE active = true`)
- **INSERT** - добавление данных (пример: `INSERT INTO products (name, price) VALUES ('Phone', 999)`)
- **UPDATE** - обновление данных (пример: `UPDATE orders SET status = 'shipped' WHERE id = 42`)
- **DELETE** - удаление данных (пример: `DELETE FROM logs WHERE created_at < '2023-01-01'`)

#### Полезные модификаторы
- **DISTINCT** - уникальные значения (пример: `SELECT DISTINCT city FROM offices`)
- **LIMIT/OFFSET** - пагинация (пример: `SELECT * FROM products LIMIT 10 OFFSET 20`)
- **ORDER BY** - сортировка (пример: `SELECT * FROM users ORDER BY registration_date DESC`)
- **GROUP BY** - группировка (пример: `SELECT department, COUNT(*) FROM employees GROUP BY department`)
- **HAVING** - фильтрация групп (пример: `SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 5000`)

#### Пример SQL-запросов:
```sql
-- Сложный JOIN с агрегацией
SELECT c.name, COUNT(o.id) as order_count 
FROM customers c
LEFT JOIN orders o ON c.id = o.customer_id
GROUP BY c.name
HAVING COUNT(o.id) > 3
ORDER BY order_count DESC;

-- Вставка с возвратом данных (RETURNING)
INSERT INTO products (name, price) 
VALUES ('Laptop', 1299)
RETURNING id, created_at;
```
---

### 12.2. JOIN-операции

| Тип JOIN       | Описание                                | Пример использования                  |
|----------------|-----------------------------------------|---------------------------------------|
| **INNER JOIN** | Только совпадающие строки               | `SELECT users.name, orders.total FROM users INNER JOIN orders ON users.id = orders.user_id` |
| **LEFT JOIN**  | Все строки левой таблицы + совпадения   | `SELECT customers.name, orders.id FROM customers LEFT JOIN orders ON customers.id = orders.customer_id WHERE orders.id IS NULL` |
| **RIGHT JOIN** | Все строки правой таблицы + совпадения  | `SELECT departments.name, employees.id FROM departments RIGHT JOIN employees ON departments.id = employees.department_id` |
| **FULL JOIN**  | Все строки обеих таблиц                 | `SELECT a.id, b.id FROM table_a FULL JOIN table_b ON a.id = b.a_id` |
| **CROSS JOIN** | Декартово произведение                  | `SELECT * FROM sizes CROSS JOIN colors` |

---

### 12.3. NoSQL базы данных

#### Основные типы
- **Документные**: MongoDB, CouchDB (пример структуры: {_id: "abc123", name: "John", orders: [...]})
- **Ключ-значение**: Redis, DynamoDB (пример: SET user:123 "{'name':'Alice'}")
- **Колоночные**: Cassandra, HBase  
- **Графовые**: Neo4j, ArangoDB  

#### Инструменты для NoSQL
- **MongoDB Compass** - GUI для MongoDB  
- **Redis Insight** - визуализация Redis  
- **Robo 3T** - легковесный клиент MongoDB  

### Пример NoSQL-запросов:
```javascript
// MongoDB запрос
db.users.find(
  { age: { $gt: 25 } },
  { name: 1, email: 1, _id: 0 }
).sort({ created_at: -1 }).limit(10);
```
---

### 12.4. Инструменты для работы с БД

| Инструмент    | Поддерживаемые СУБД           | Особенности                     |
|---------------|-------------------------------|---------------------------------|
| **DBeaver**   | PostgreSQL, MySQL, Oracle и др| Универсальный, есть CE версия   |
| **pgAdmin**   | PostgreSQL                    | Официальный инструмент          |
| **TablePlus** | MySQL, SQLite, MongoDB        | Современный интерфейс           |
| **HeidiSQL**  | MySQL, MariaDB                | Легковесный клиент              |
| **DataGrip**  | Все основные СУБД             | Продвинутые функции (JetBrains) |

---

### 12.5. Полезные SQL-запросы

#### Агрегация данных
Пример: `SELECT category, COUNT(*) as count, AVG(price) FROM products GROUP BY category HAVING COUNT(*) > 5 ORDER BY count DESC`

#### Работа с датами
Пример: `SELECT user_id, EXTRACT(MONTH FROM created_at) as month, COUNT(*) FROM orders WHERE created_at BETWEEN '2023-01-01' AND '2023-12-31' GROUP BY user_id, month`

#### Оптимизация запросов
- Использование EXPLAIN ANALYZE
- Правильное индексирование
- Ограничение выборки (LIMIT)

---

📌 _Следующий файл: [13. Тестирование безопасности](13_devops.md)_
