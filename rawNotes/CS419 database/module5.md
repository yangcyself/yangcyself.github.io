
# Cluster Server Architecture
- MPP (massively parallel processing) “shared nothing” 
- SMP (symmetric multiprocessing) “shared everything” 
- hybrid “shared disk” 

## MPP
**advantage**
- Cost: Hardware/software costs are minimized because commodity (commercial off-the-self) hardware and operating systems are used.
- Scalability: The cluster can be expanded easily by simply adding more nodes.
Widely Supported: There are many DBMS vendors that support this architecture.
**disadvantages** 

- Cross-node Performance: If data is not carefully segmented across nodes, operations that require data stored on different nodes must have the data transmitted across the network, which can considerably slow down processing. I present some design guidelines for avoiding this situation later in this topic.
- Processing Must Be Asymmetric:


## SMP
**ADV**
- Support for Complex Symmetric Operations: When performing complex calculations that require a lot of memory and CPU resources, this solution is hard to beat.
- Higher Performance: The SMP environments are generally high-powered units that perform well above the levels of comparable MPP systems.

**DISADV**
- Cost: Hardware/software costs are higher than MPP clusters because specialized hardware is required.
- Scalability Has Limits: The servers can be expanded by adding or upgrading internal CPU and memory units, but there is always a maximum amount that can fit within a given environment. In other words, scalability is not as open-ended as with MPP systems.
- Limited DBMS Support: 


# Topic 5.4: NoSQL Database Implementations
- mapreduce 
- columnar
- document databases
- Key-value Databases
- Graph Databases

## document databases
In MongoDB, the term used for distribution is known as **sharding**. larger documents can be distributed (aplit) across cluster nodes



## quiz

Question 1
1 / 1 pts
When defining a one-to-one relationship between two tables, a foreign key should be defined…
  a. In both of the tables 
  **b. In either one of the tables**
  c. Neither of the above 
 
Question 2
1 / 1 pts
On cluster servers, the best way to optimize joins is to:
  **a. Segment tables across nodes based on join keys**
  b. Segment tables across nodes based on primary keys 
  c. Segment tables across nodes based on foreign keys 
  d. Segment tables across nodes randomly 
  e. None of the above 
 
Question 3
1 / 1 pts
The leaf layer of a B-tree index contains
  **a. One logical record for each indexed value**
  b. An RBA pointer to the root node 
  c. A list of pointers to the branch nodes of the index 
  d. A bitmap of all keys to all the rows in the indexed table 
  e. Foreign key values for the indexed table 
 
Question 4
1 / 1 pts
Is it possible to define multiple unique constraints on the same physical table?
  a. No 
  **b. Yes**
 
Question 5
1 / 1 pts
Each server in a cluster server architecture is known as a(n):
  a. RAID device 
  b. SMP CPU 
  c. MPP CPU 
  **d. Node**
  e. None of the above 
 
Question 6
1 / 1 pts
The most commonly used cluster server architecture is:
  a. Shared disk (SMP Hybrid) 
  b. Shared everything (SMP) 
  **c. Shared nothing (MPP)**
 
IncorrectQuestion 7
0 / 1 pts
Which data type is best for a column that will contain the name of the current month?
  a. DATE 
  b. TIMESTAMP 
  **c. CHAR**
  d. VARCHAR 
  e. NUMBER 
 
IncorrectQuestion 8
0 / 1 pts
The branch nodes of a B-tree index contain
  a. One logical record for each indexed value 
  **b. An RBA pointer to the root node**
  c. Pointers to associated leaf nodes of the index 
  d. A bitmap of all keys to all the rows in the indexed table 
  e. Foreign key values for the indexed table 
 
Question 9
1 / 1 pts
How should a many-to-many relationship between two tables be defined in the physical database design?
  a. By placing the primary key of one of the tables in the other table as a foreign key 
  b. By placing the primary key of each table in the other table as a foreign key 
  c. Using a database trigger 
  d. By placing the primary key of just one of the tables in an intersection table 
  **e. By placing the primary keys of both of the tables in an intersection table**
 
Question 10
1 / 1 pts
Is it acceptable for columns included in a unique constraint to contain NULL values?
  **a. Yes** 
  b. No 

# Homework
**HW5 is dependent on HW4**