# Oracle Pluggable Database Assignment II

**Student ID:** 27164  
**First Name:** GASANA LANCE JONATHAN  

## Overview
This project demonstrates the creation, management, and deletion of Oracle Pluggable Databases (PDBs). The tasks include:
- Creating a persistent PDB with an admin user.
- Creating and then completely removing a temporary PDB.
- Configuring and accessing Oracle Enterprise Manager (EM) Express.
- Documenting the process and challenges in a public GitHub repository.


## Task 1: Create a New Pluggable Database
**PDB Name:** `la_pdb_27164`  
**Admin User:** `lance_plsqlauca_27164`  

The PDB was created from the `PDB$SEED` using the `CREATE PLUGGABLE DATABASE` command with explicit `FILE_NAME_CONVERT` paths. After creation, the PDB was opened and verified. The admin user was confirmed to exist inside the PDB.

**Screenshots:**
- [task1_creation.png](screenshots/task1_creation.png) – The `CREATE PLUGGABLE DATABASE` command execution.
- [task1_open_state.png](screenshots/task1_open_state.png) – Query showing the PDB open mode (`READ WRITE`).
- [task1_user.png](screenshots/task1_user.png) – Query confirming the admin user exists inside the PDB.

## Task 2: Create and Delete a Temporary PDB
**Temporary PDB Name:** `la_to_delete_pdb_27164`  

A temporary PDB was created using the same method. Its existence was verified, then it was closed and dropped completely using the `INCLUDING DATAFILES` clause. Final verification confirmed it no longer exists.

**Screenshots:**
- [task2_creation.png](screenshots/task2_creation.png) – Creation of the temporary PDB.
- [task2_view.png](screenshots/task2_view.png) – Verification that the temporary PDB exists.
- [task2_deletion.png](screenshots/task2_deletion.png) – The `DROP` command.
- [task2_deleted.png](screenshots/task2_deleted.png) – Final check showing the temporary PDB is gone.

## Task 3: Oracle Enterprise Manager (EM) Express
EM Express was configured and accessed via a web browser. After setting `DBMS_XDB_CONFIG.SETGLOBALPORTENABLED(TRUE)`, the dashboard became accessible. The screenshot shows the main dashboard with the PDB name and the logged-in user (`SYS`) visible.

**Screenshot:**
- [task3_oem.png](screenshots/task3_oem.png) – OEM dashboard displaying the environment and PDB details.

## Challenges Faced
1. **FILE_NAME_CONVERT Path Errors**  
   Initially, the `CREATE PLUGGABLE DATABASE` command failed due to incorrect file paths. The solution was to verify the actual datafile locations using `SELECT name FROM v$datafile` and update the paths with double backslashes for Windows.

2. **PDB Not Open After Creation**  
   After creation, the PDB remained in `MOUNTED` state. This was resolved by explicitly running `ALTER PLUGGABLE DATABASE OPEN`.

3. **EM Express Authentication Loop**  
   Accessing `https://localhost:5500/em` resulted in a persistent browser pop‑up that would not accept credentials. The issue was fixed by executing `EXEC DBMS_XDB_CONFIG.SETGLOBALPORTENABLED(TRUE);` in SQL*Plus, which allowed the EM Express login page to load properly.

4. **Invalid Container Name in EM Express**  
   When logging into EM Express for the PDB, the container name was initially rejected. The correct container name (uppercase) was obtained by querying `v$pdbs`, and leaving the field blank as a fallback allowed access to the CDB, from which the PDB could be navigated.


---
**Repository Link:** [https://github.com/Lance-7-1-2/oracle_pdb_ass_II_27164_lance](https://github.com/Lance-7-1-2/oracle_pdb_ass_II_27164_lance)  
**PDB Name Created:** la_pdb_27164  
**Issues Encountered:** Yes
