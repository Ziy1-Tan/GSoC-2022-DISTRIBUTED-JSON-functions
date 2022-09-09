# GSoC 2022 Final Report

## Introduction

- **Organization:** [MariaDB Corporation](https://github.com/mariadb-corporation?type=source)
- **Project:** [Implement DISTRIBUTED JSON Functions](https://summerofcode.withgoogle.com/programs/2022/projects/VIJfR79a)
- **Product:** [Pull Request](https://github.com/mariadb-corporation/mariadb-columnstore-engine/pull/2425) (reviewed, code 8600+ lines, tests 2000+ lines)

## Works in GSoC

**ColumnStore (MCS)** is a large-scale **columnar storage engine** based on a parallel distributed data architecture. I am mainly responsible for **adding support for the `JSON_*` functions** into the existing functions.

```sql
MariaDB [(none)]> USE test;
Database changed
MariaDB [test]> CREATE TABLE json_test(j LONGTEXT) ENGINE=ColumnStore;
Query OK, 0 rows affected (0.231 sec)

MariaDB [test]> INSERT INTO json_test VALUES(2022),('"hello GSoC2022"');
Query OK, 2 rows affected (0.176 sec)
Records: 2  Duplicates: 0  Warnings: 0

MariaDB [test]> SELECT j AS json, JSON_TYPE(j) AS type FROM json_test;
+------------------+---------+
| json             | type    |
+------------------+---------+
| 2022             | INTEGER |
| "hello GSoC2022" | STRING  |
+------------------+---------+
2 rows in set (0.050 sec)
```

> [Full List](https://mariadb.com/kb/en/json-functions/) of JSON functions **(34 functions)**

- **Boolean Adaptation:** Adapted for JSON and MariaDB Boolean incompatibility issues to make it **fully compatible**;
- **RAII Encapsulation:** Use Exception, RAII and other features to encapsulate code, the encapsulated code has stronger **exception-safe** and **resource-safe**;
- **Constant Cache:** Cache constants such as json path during function execution, which **greatly improves** the execution efficiency of functions;
- **SQL Test:** use the `Mysql-test-run` test framework to write test cases, and the final test coverage rate reaches **90%**;
- **Additional Patches:** 3 during GSoC development were **merged**:
  1. [Refactor: remove redundant assignments of JSON_MERGE_PATCH](https://github.com/MariaDB/server/pull/2209);
  2. [MDEV-28947 JSON_TYPE result is turncated, charset max length should be considered](https://github.com/MariaDB/server/pull/2172);
  3. [MDEV-29264: JSON function overflow error based on LONGTEXT field](https://github.com/MariaDB/server/pull/2226).
- **Result:**
  - Deeper understanding of the parsing and execution process of JSON and SQL functions
  - More familiar with the compilation and debugging of C/C++ code
  - Better understanding of test case design;
## Reference

- **[JIRA](https://jira.mariadb.org/browse/MCOL-785)**
- **[Design](https://docs.google.com/document/d/1Kt41H61QCfTgBMgFB6i77URc7jNppWL9Ph_5_-LEBOU/edit?usp=sharing)**
