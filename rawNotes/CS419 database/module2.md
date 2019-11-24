# SQL
- Data Query Language(DQL)

## general:
only use '' to enclose strings

# Data query language
### SELECT
#### required clauses
- SELECT lists the desired columns
- FROM: the source tables
- SELECT FROM to table can join the table together, yields cartesian product

**example**
```SQL
SELECT HORSE_ID, HORSE_NAME, BIRTH_DATE
    FROM HORSE;
    ORDER BY BIRTH_DATE DESC;
    WHERE GENDERR='M'OR BIRTH_DATE>'2010-01-01'
```



**note** 
not equal:  `<>`

#### MATCH
**AND processed before OR**

**nonpositional wildcards**
`%N_w`: matches any string that ends with `N?w`, where `?` can be anything

**IN**
```SQL
WHERE OWNER_ID IN ('0000','0000')
```
```SQL
WHERE OWNER_ID IN (SELECT OWNER_ID FROM OWNER WHERE CITY = 'shit')
```

**exmaple alise and join**
```SQL
SELECT A.HORSE_NAME, A.HORSE_ID, B.OWNER_LAST_NAME, B.OWNER_FIRST_NA<E
    FROM HORSE A, OWNER B
    WHERE A.OWNER_ID = B.OWNDER_ID;
```
same with 
```SQL
SELECT A.HORSE_NAME, A.HORSE_ID, B.OWNER_LAST_NAME, B.OWNER_FIRST_NA<E
    FROM HORSE A
    JOIN OWNER B
    ON A.OWNER_ID = B.OWNDER_ID;
```

#### self join
```SQL
SELECT H.HORSE_ID, H.HORSE_NAME, S.HORSE_NAME AS SIRE, D.HORSE_NAME AS DAM
    FROM HORSE H
    JOIN HORSE S
    ON H.SIRE_HORSE_ID = s.HORSE_ID
    JOIN HORSE d
    ON H.DAM_HORSE_ID = D.HORSE_ID
    RODERED BY H.HORSE_NAME
```
**inner and outer join**
inner join is exclusive join

ourter join is an inclusive join
```SQL
SELECT H.HORSE_ID, H.HORSE_NAME, S.HORSE_NAME AS SIRE, D.HORSE_NAME AS DAM
    FROM HORSE H
    JOIN HORSE S
    ON H.SIRE_HORSE_ID = s.HORSE_ID
    JOIN HORSE d
    ON H.DAM_HORSE_ID = D.HORSE_ID
    RODERED BY H.HORSE_NAME
```


## functions
### UPPER

### SUM, AVG. MIN. MAX, MAX

### COUNT
- COUNT(*) count all the rows
- COUNT(column_value)  counts only non-null values

### GROUP BY
```SQL
SELECT HORSE_ID, SUM(PURSE), COUNT(*) AS NUM_RACES
    FROM RACE_RESULT
    GROUP BY HORSE_ID
```
#### HAVING
**It has syntax like the WHERE clause, but it is applied to each group after grouping has taken place**

```SQL
SELECT HORSE_ID, SUM(PURSE), COUNT(*) AS NUM_RACES
    FROM RACE_RESULT
    GROUP BY HORSE_ID
    HAVING COUNT(*)>1
```
# data definition language (DDL)

manipulate data objects
- ALTER
- DROP
- TRUNCATE



## Create table statement
```SQL
CREATE TABLE RACE_RESULT
    (
    TRACK_ID                 VARCHAR(20)         NOT NULL,
    RACE_NUMBER        CHAR(2)                 NOT NULL,
    RACE_DATE               DATE                     NOT NULL,
    HORSE_ID                  CHAR(6)                NOT NULL,
    PLACE                        DECIMAL(2,0),
    PURSE                        DECIMAL(8,2),
    LENGTHS_BEHIND    DECIMAL(5,2)
    );
```

### ALTER TABLE statement
- Adding columns to the table
- Removing columns from the table
- Altering the data type for existing table columns
- Changing physical storage properties of the table
- Adding, removing, or altering constraints


## Merge statement
example:
two tables: CD_INVENTORY and MERGE_INVENTORY
```SQL
MERGE INTO CD_INVENTORY
USING MERGE_INVENTORY ON (CD_NAME = MERGE_CD_NAME)
WHEN MATCHED THEN
   UPDATE SET MUSIC_TYPE = MERGE_MUSIC_TYPE,
               PUBLISHER = MERGE_PUBLISHER,
               IN_STOCK   = MERGE_IN_STOCK
WHEN NOT MATCHED THEN
   INSERT (CD_NAME, MUSIC_TYPE, PUBLISHER, IN_STOCK)
     VALUES (MERGE_CD_NAME, MERGE_MUSIC_TYPE,
             MERGE_PUBLISHER, MERGE_IN_STOCK);
```

