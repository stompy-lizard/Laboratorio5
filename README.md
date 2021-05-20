# Laboratorio 5
## SQL
### Enunciado
 - Usando el shell (sqlite3):
 - Crear Tabla EMPLOYEES con 6 columnas
   - Fields:  ID(entero),  NAME(text),  GENDER(M/F/U),  AGE(flotante), JOB(texto)
 - Crear Tabla JOBS con 2 columnas
   - Fields:  ID(entero),  NAME(texto)
 - Inserte en la tabla JOBS 5 tipos de trabajo(escoja el nombre que quiera, IDs del 0 al 4)
 - Inserte en la tabla EMPLOYEES 10 empleados(escoja el nombre, género, edad, trabajo que quiera, IDs del 0 al 9), el rango de edad debe ser entre 18 y 70.
 - Cree dos **queries** donde encuentre(asegúrese de usar datos que puedan ser seleccionados por ambos queries):
   - Los nombres de los empleados con edad mayor a 30 años, mujeres, donde JOB tenga el ID 3
   - Los nombres de los trabajos hechos por personas entre 20 y 30 años(inclusivos)
 - Documente los comandos necesarios para lograr esto, y los resultados de cada query.
### Solución
Primero instalar sqlite si no se tiene:
```bash
sudo apt install sqlite3
```
Crear la Base de datos:
```bash
sqlite3 laboratorio5.db
```
Esto accede al shell de sqlite3. 
Se crea la tabla EMPLOYEES con las columnas requeridas:
```sql
CREATE TABLE EMPLOYEES(ID integer, NAME text, GENDER text, AGE real, JOB integer);
```
Se crea la tabla JOBS con las columnas requeridas:
```sql
CREATE TABLE JOBS(ID integer, NAME text);
```
Se ingresan los trabajos:
```sql
INSERT INTO JOBS VALUES(0, "Bombero/a");
INSERT INTO JOBS VALUES(1, "Doctor/a");
INSERT INTO JOBS VALUES(2, "Maestro/a");
INSERT INTO JOBS VALUES(3, "Policia");
INSERT INTO JOBS VALUES(4, "Deportista");
```
Se ingresan los empleados:
```sql
INSERT INTO EMPLOYEES VALUES(0, "Juan", "M", 18, 4);
INSERT INTO EMPLOYEES VALUES(1, "Ariel", "U", 25, 2);
INSERT INTO EMPLOYEES VALUES(2, "Maria", "F", 58, 1);
INSERT INTO EMPLOYEES VALUES(3, "Damian", "M", 70, 3);
INSERT INTO EMPLOYEES VALUES(4, "Diana", "F", 33, 0);
INSERT INTO EMPLOYEES VALUES(5, "Sebastian", "M", 26, 4);
INSERT INTO EMPLOYEES VALUES(6, "Elena", "F", 35, 3);
INSERT INTO EMPLOYEES VALUES(7, "Pedro", "U", 24, 4);
INSERT INTO EMPLOYEES VALUES(8, "Elisa", "F", 45, 3);
```
Ahora se tienen las tablas:
#### JOBS
| ID | NAME       |
| -- | ---------- |
| 0  | Bombero/a  |
| 1  | Doctor/a   |
| 2  | Maestro/a  |
| 3  | Policia    |
| 4  | Deportista |
#### EMPLOYEES
| ID | NAME      | GENDER | AGE  | JOB |
| -- | --------- | ------ | ---- | --- |
| 0  | Juan      | M      | 18.0 | 4   |
| 1  | Ariel     | U      | 25.0 | 2   |
| 2  | Maria     | F      | 58.0 | 1   |
| 3  | Damian    | M      | 70.0 | 3   |
| 4  | Diana     | F      | 33.0 | 0   |
| 5  | Sebastian | M      | 26.0 | 4   |
| 6  | Elena     | F      | 35.0 | 3   |
| 7  | Pedro     | U      | 24.0 | 4   |
| 8  | Elisa     | F      | 45.0 | 3   |
| 9  | Mariela   | F      | 32.0 | 3   |

Se seleccionan los nombres(columna NAME) de la tabla EMPLOYEES que tengan edad(columna AGE) mayor a 30 años, mujeres(columna GENDER), donde JOB tenga el ID 3:
```sql
SELECT 
  EMPLOYEES.NAME 
FROM 
  EMPLOYEES 
WHERE 
  EMPLOYEES.AGE > 30 AND 
  EMPLOYEES.GENDER IS "F" AND 
  EMPLOYEES.JOB IS 3;
```
Lo que devuelve lo siguiente:
```
Elena
Elisa
Mariela
```

Se seleccionan los nombres de los trabajos hechos por personas entre 20 y 30 años(inclusivos):
```sql
SELECT DISTINCT 
  JOBS.NAME 
FROM 
  JOBS, EMPLOYEES 
WHERE 
  EMPLOYEES.JOB=JOBS.ID AND 
  EMPLOYEES.AGE >= 20 AND 
  EMPLOYEES.AGE <= 30;
```
Lo que devuelve lo siguente:
```
Maestro/a
Deportista
```
