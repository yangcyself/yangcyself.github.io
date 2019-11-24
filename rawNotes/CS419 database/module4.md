
Over time, the process of visually representing entities, attributes, and relationships, known as **entity relationship modeling,** evolved. 

## Entity Relationship Diagram (ERD) Formats
**cardinality** Symbols placed on or next to the ends of the lines indicate the cardinality of the relationships.

Symbols placed near the ends of the lines indicate whether an instance of one entity is **mandatory or optional** compared with an instance of another entity.

### Chen’s ERD Format

For many-to-many relationships that require an intersection table in a relational DBMS, such as the one between Invoice and Product, many designers **draw a rectangle around the relationship’s diamond.** 

### The Relational Format
Relationship cardinality is shown with an arrowhead representing “one” and nothing on the line end representing “many”.


### The Information Engineering Format
- An identifying relationship is a relationship where the foreign key is part of the primary key of the table on the “many” side of the relationship (the so-called **“child” table**).
- A non-identifying relationship is a relationship where the foreign key is not part of the primary key of the table on the “many” side.
- Identifying relationships are shown with **solid lines**, which non-identifying relationships are shown with **dotted lines**.
- Minimum cardinality can be optionally shown with a symbol on the line just inboard from the maximum cardinality symbol. **A minimum of zero is denoted with a circle,** which a minimum of 1 is denoted with an additional tick mark. However, as you see in the second version of the diagram (the one with the surrogate key in INVOICE_LINE_ITEM), some variations show only one tick mark when the minimum and maximum cardinality are both 1.
- Dependent entities, noted by drawing the entity (table) rectangle with rounded corners as shown in the first IE diagram
- 

# Process Modeling

## The Flowchart

## The Function Hierarchy Diagram