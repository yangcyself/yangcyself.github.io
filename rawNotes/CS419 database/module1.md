## what is database

A **file** is a collection of related records that are stored as a single unit by an operating system. Databases use files for permanent storage of data.
An **instance** is a copy of the database software running in memory.
A **database object** is a named data structure that is stored in a database. For example, in a relational database, tables and views are types of database objects

## DBMS database management systems

### Layers of Abstraction
physical layer

**logical layer**,
presents the *database schema*

**external layer**
transforms the schema objects into *views*

also called *sub-schema*

### dataindependence
the ability to make non-destructive data structure changes without disrupting existing processes and queries that use the database.

- Data independence is not an absolute “have” or “have not” property, but rather a matter of degrees (having more or less data independence compared to another alternative).

- physical data independence
  - e.g. moving a data file does not disrupt existing processes
- logical data independence

## historically significant database models
### flat files
### Hierarchical database model
Record types are organized into a hierarchy that appears as an inverted tree. A parent record type may have many child record types, but a child record type may have only one parent record type.

Related records are connected via a physical address pointer

These pointers are typically relative byte (Links to an external site.) address (RBA) pointers that point to the block that contains the related record. A relative byte address refers to a location within a file in terms of how many bytes it is from the beginning of a file. 

### network Database Model
child record types (which are called members) may have multiple parent record types (which are called owners).

#### Benefits of Network Databases

- Like hierarchical databases, record access is faster than equivalent flat file systems thanks to the pointers used to implement the sets.
- Data access can start with any record type. This provides more flexibility than hierarchical databases, where all data access must begin with the root record type (the top of the hierarchy).
- Network databases are capable of modeling more complex data structures than flat files or hierarchical databases.
- It is easier to develop complex queries using network databases.

#### Drawbacks of Network Databases

- Data structures are difficult to modify, particularly if a new record type has to be added.
- Changes to the data structure often affect the applications that use the database. Once a network structure is modified, programming changes are usually required so that queries work as they did before the change.
- Users must understand the complex data structure. These structures can be positively daunting to less technical users.

### relational dtabase Model
The primary unit of storage is a table, which contains rows of data that are similar to the records that would be contained in a flat file. Instead of using pointers to implement relationships, the unique identifier (primary key) of the parent table is stored in the child table. This repeated key is known as a foreign key. Each table can be used independently, or joins may be used to combine table records (rows). Data integrity constraints may be added to preserve data integrity.


#### Benefits of Relational Databases

- Supports very fast retrieval in most cases
- The data structure can be easily changed.
- Users need no awareness of physical storage structures.
- Complex queries can be easily developed.
- Data is usually more accurate.
- Application programming is easier than with hierarchical or network databases.
- A standard query language (SQL) is supported.
- Drawbacks of Relational Databases

#### Tables must be joined to retrieve related data (joins can be hidden in views, however).
- Users must understand the relationships between tables.
- Users must learn SQL or a front-end query tool.


### Obeject Oriented Database Model
#### Benefits of Relational Databases

-  Supports very fast retrieval in most cases
- The data structure can be easily changed.
- Users need no awareness of physical storage structures.
- Complex queries can be easily developed.
- Data is usually more accurate.
- Application programming is easier than with hierarchical or network databases.
- A standard query language (SQL) is supported.
#### Drawbacks of Relational Databases

- Tables must be joined to retrieve related data (joins can be hidden in views, however).
- Users must understand the relationships between tables.
- Users must learn SQL or a front-end query tool.


## relational databases
### High-level conceptual database design
### Entities
### Attributes
### Relations

Relationships are often classified by their cardinality. In database terminology, cardinality refers to the number of records (rows of data) in a data structure that are associated with another data structure.

One-to-One
one-to-many
many-to-many

Recursive relationships
is a relationship between entity instances (records) of the same entity type.

### logical/physical deatabase design components
tables

#### data integrity
**constraints:** 

**primary key constraint**

**referential integrity**

many to many

Relational database cannot directly implement many-to-many relationships, so we must place an intersection entity between the two tables that have the many-to-many relationship, which essentially breaks the relationship down into two one-to-many relationships, each of which can be defined in the relational database. The **intersection table** resolves the many-to-many relationship. Note that the intersection table appears on the "many" side of the two one-to-many relationships.


