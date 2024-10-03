# Oracle Pluggable Databases

This README provides an overview of Oracle Pluggable Databases (PDBs) and explains the operations demonstrated in the provided images.

## What are Pluggable Databases?

Pluggable Databases are a feature of Oracle Database 12c and later versions. They allow a single container database (CDB) to host multiple portable databases called PDBs. This architecture offers improved resource utilization, easier management, and increased database consolidation.

## Environment Details

- Oracle Database Version: 21c Enterprise Edition Release 21.0.0.0.0 - Production
- SQL*Plus Version: 21.0.0.0.0
- Operating System: Microsoft Windows x86 64-bit

## Demonstrated Operations

### 1. Viewing Existing PDBs

The command `show pdbs;` lists all existing pluggable databases:

```sql
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 ORCLPDB                        READ WRITE NO
```

### 2. Creating a New PDB

A new PDB named `plsql_class2024db` is created:

```sql
SQL> CREATE PLUGGABLE DATABASE plsql_class2024db
  2  ADMIN USER ph_plsqlauca IDENTIFIED BY password
  3  FILE_NAME_CONVERT = 
  4  ('C:\oracle21c\oradata\ORCL\pdbseed','C:\oracle21c\oradata\ORCL\orclpdb\ph_plsqlauca');

Pluggable database created.
```

### 3. Creating Another PDB

Another PDB named `ph_to_delete_pdb` is created:

```sql
SQL> CREATE PLUGGABLE DATABASE ph_to_delete_pdb
  2  ADMIN USER ph_delplsqlauca IDENTIFIED BY password
  3  FILE_NAME_CONVERT = 
  4  ('C:\oracle21c\oradata\ORCL\pdbseed','C:\oracle21c\oradata\ORCL\orclpdb\ph_delplsqlauca');

Pluggable database created.
```

### 4. Viewing Updated PDB List

After creating the new PDBs, the updated list shows:

```sql
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 ORCLPDB                        READ WRITE NO
         4 PLSQL_CLASS2024DB              MOUNTED
         5 PH_TO_DELETE_PDB               MOUNTED
```

### 5. Dropping a PDB

The `ph_to_delete_pdb` is dropped:

```sql
SQL> DROP PLUGGABLE DATABASE ph_to_delete_pdb INCLUDING DATAFILES;

Pluggable database dropped.
```

### 6. Final PDB List

After dropping the PDB, the final list shows:

```sql
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 ORCLPDB                        READ WRITE NO
         4 PLSQL_CLASS2024DB              MOUNTED
```

## Oracle Enterprise Manager Database Express

The images also show the Oracle Enterprise Manager Database Express interface, which is a web-based tool for managing Oracle databases. It provides:

1. A login screen for accessing the management interface.
2. A dashboard showing database status, performance metrics, and resource utilization.

## Key Points

- PDBs allow for better resource management and easier database administration.
- The `CREATE PLUGGABLE DATABASE` command is used to create new PDBs.
- The `DROP PLUGGABLE DATABASE` command removes a PDB.
- The `show pdbs;` command lists all available PDBs in the container database.
- Oracle Enterprise Manager Database Express provides a graphical interface for managing databases and PDBs.

## Note

When working with PDBs, always ensure you have the necessary permissions and understand the implications of your actions, especially when creating or dropping databases.
