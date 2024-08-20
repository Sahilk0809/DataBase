# DataBase

## To create table

```bash
CREATE TABLE "" (
	"id"	INTEGER UNIQUE,
	"name"	TEXT NOT NULL,
	"role"	TEXT NOT NULL,
	"salary"	REAL NOT NULL,
	"age"	INTEGER NOT NULL,
	"address"	TEXT,
	"phone"	INTEGER NOT NULL,
	PRIMARY KEY("id" AUTOINCREMENT)
);
```

## Add employee to the table

```bash
INSERT INTO employee (name, role, salary, age, phone)
VALUES ('Sahil', 'Flutter Developer', 50000, 18, 8153824856);
```

## Add multiple employee data to the table

```bash
INSERT INTO employee (name, role, salary, age, phone)
VALUES ('Sahil', 'Flutter Developer', 50000, 18, 8153824856),
('Vishal', 'Flutter Developer', 50000, 18, 9904345620);
```

## Retrive all data from the table

```bash
SELECT * FROM employee;
```

## Retrive specific column of employee data

```bash
SELECT name, salary FROM employee;
```

## Find employees with a particular role

```bash
SELECT name, salary FROM employee WHERE role = 'Flutter Developer';
```

## Search for employees with names containing "Sa"

```bash
SELECT * FROM employee WHERE name like 'Sa%';
```

## Find employees older than 30 and earning more than Rs.40000

```bash
SELECT * FROM employee WHERE age > 30 AND salary > 40000;
```

## Change the salary of an employee with ID

```bash
UPDATE employee SET salary = 70000 WHERE id = 4;
```

## Update the address for employees in the 'Flutter Developer' role

```bash
UPDATE employee SET address = 'Dindoli, Surat' WHERE role = 'Flutter Developer';
```

## Remove an employee with ID 2

```bash
DELETE FROM employee WHERE id = 2;
```

## Delete all employees under 18 (assuming it's not a valid age)

```bash
DELETE FROM employee WHERE age < 18;
```
