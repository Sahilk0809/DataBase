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

## Table
<img src="https://github.com/user-attachments/assets/4b72d39d-e8e7-4499-b936-1a385e5fcc6c">

## Table in App Inspection
<img src="https://github.com/user-attachments/assets/bfd66ba1-863f-46cf-8996-51b7a941a0c0">

## Database Helper class
```bash
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';

class DatabaseHelper {
  static DatabaseHelper databaseHelper = DatabaseHelper._();

  DatabaseHelper._();

  static const String databaseName = 'notes.db';
  static const String tableName = 'notes';

  Database? _database;

  Future<Database?> get database async => _database ?? await initDatabase();

  Future<Database?> initDatabase() async {
    final path = await getDatabasesPath();
    final dbPath = join(path, databaseName);
    return await openDatabase(
      dbPath,
      version: 1,
      onCreate: (db, version) {
        String sql = '''
      CREATE TABLE $tableName (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      amount INTEGER NOT NULL,
      description TEXT NOT NULL,
      category TEXT
      )
      ''';
        db.execute(sql);
      },
    );
  }

  Future<int> insertData() async {
    final db = await database;
    String sql = '''
    INSERT INTO $tableName (amount, description)
    VALUES (3000, 'Bike Service');
    ''';
    final result = await db!.rawInsert(sql);
    return result;
  }

  Future<int> deleteData(int id) async {
    final db = await database;
    String sql = '''
    DELETE FROM $tableName WHERE id = $id
    ''';
    final result = await db!.rawDelete(sql);
    return result;
  }
}
```

## Controller
```bash
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'package:sqlite_practice/helper/database_helper.dart';

class BudgetController extends GetxController{

  @override
  void onInit(){
    super.onInit();
    initDb();
  }

  Future initDb() async{
    await DatabaseHelper .databaseHelper.database;
  }

  Future insertRecord() async{
    await DatabaseHelper.databaseHelper.insertData();
  }
  Future deleteRecord(int id) async{
    await DatabaseHelper.databaseHelper.deleteData(id);
  }
}
```
