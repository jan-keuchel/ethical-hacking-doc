# SQLMap Cheatsheet

## Table of Contents

* [Getting Started](#getting-started)
* [Database Statements](#database-statements)
* [Table Statements](#table-statements)
* [Examples](#examples)
---

## Getting Started

```bash
sqlmap --help                               # Shows the help menu
sqlmap --wizard                             # Starts interactive mode and asks for input to use for the command
```

## Flags

* `-u` : URL of the database to test.
* `--dbs` : Extract all database names.
* `--tables` : Extract all tablels in a database.
* `-T <table> --dump` : Enumerate records of the table.
* `-p` : Single password

