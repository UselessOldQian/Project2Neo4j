# Neo4j
## Introduction
Graph database is a new type of noSql database based on graph theory. Its database storage structure and data query method are all based on graph theory. The basic elements of graphs in graph theory are nodes and edges, which correspond to nodes and relationships in graph databases.  

Neo4j is an open source NoSQL graph database implemented in Java. The source code for Neo4j is hosted on GitHub, and technical support is hosted on Stack Overflow and the Neo4j Google discussion group. Neo4j is now used by hundreds of thousands of companies and organizations in a variety of industries. Neo4j use cases cover network management, software analysis, scientific research, routing analysis, organization and project management, decision making, social networking, and many more.

Neo4j implements the storage of graph data models at the professional database level. Unlike ordinary graph processing or memory-level databases, Neo4j provides complete database features, including ACID transaction support, cluster support, backup and failover, etc., which makes it suitable for various applications in enterprise-level production environments.

## Installation
1. Download and unzip Neo4j-community.   
   Download Link: https://neo4j.com/download-center/#community 
   
 
2. Install JDK 11  
   Download Link: https://www.oracle.com/java/technologies/downloads/  
   Download java11, if you download 8, neo4j does not support it and will report an error.


3. Use Neo4j  
   - Start  
   Go to the installation directory and input in the terminal.
   ```Bash
   cd neo4j/bin
   ./neo4j  start
   ```
   - Login  
     Enter localhost:7474 in your browser. The initial username and password are both neo4j.  
     

4. Close Neo4j
   ```Bash
   ./neo4j  stop
   ```

## Basic elements and concepts in Neo4j graph data  
- Node  
  A node is a basic element in a graph database, used to represent an entity record, just like a record in a relational database. In Neo4j a node can contain multiple properties and multiple labels.  


- Relationship  
  Relationships are also fundamental elements in graph databases. When nodes already exist in the database, the nodes need to be connected to form a graph. A relationship is used to connect two nodes. A relationship is also called an edge in graph theory. Its beginning and end must be nodes. A relationship cannot point to or originate from empty space.


- Attribute  
  Both nodes and relationships can have multiple attributes. Attributes are composed of key-value pairs, just like a Java hash table, the attribute name is similar to the variable name, and the attribute value is similar to the variable value. Property values can be primitive data types, or arrays of primitive data types.  
  
## How to Use Neo4j - Tutorial for CQL  

Cypher is designed for dealing with graph data in Neo4j. CQL stands for Cypher Query Language, just like
SQL for Oracle.

| |CQL command|Usage|
|---|----|-----|
|1|`CREATE`|Create node, relationship, or attribute|
|2|`MATCH`| Search all the related nodes, relationships, or attributes |
|3|`RETURN`| Return all the search results |
|4|`WHERE`| Filter the search result by the clauses |
|5|`DELETE`| Delete nodes and attributes |
|6|`REMOVE`| Delete nodes and attributes of relationships |
|7|`ORDER BY`| Order the search data |
|8|`SET`| Add or Update labels |

### 1. Create Nodes
- ###1.1 Create single node

Creating a single node:
```Cypher
CREATE (n)
```
Result:
```
Created 1 node, completed after 11 ms.
```

- ###1.2 Create multiple nodes
Creating multiple nodes is done by separating them with a comma.
```Cypher
CREATE (n),(m)
```
Result:
```
Created 2 nodes, completed in less than 1 ms.
```

- ###1.3 Create a node with a label
You can use the following code to add a node with a label:
```Cypher
CREATE (n:Person)
```
Result:
```
Added 1 label, created 1 node, completed after 24 ms.
```

- ###1.4 Create a node with multiple labels
To add labels when creating a node, use the syntax below. In this case, we add two labels.
```Cypher
CREATE (n:Person:Xingjian)
```
Result:
```
Added 2 labels, created 1 node, completed after 39 ms.
```

- ###1.5 Create node and add labels and properties
When creating a new node with labels, you can add properties at the same time.
```Cypher
CREATE (n:Person {name: 'Xingjian', title: 'Student'})
```
Result:
```
Added 1 label, created 1 node, set 2 properties, completed after 61 ms.
```

- ###1.6. Return created node
Creating a single node is done by issuing the following query:
```Cypher
CREATE (a {name: 'Xingjian'})
RETURN a.name
```
Result:
```
╒══════════╕
│"a.name"  │
╞══════════╡
│"Xingjian"│
└──────────┘
```
### 2. Create Relationships
- ### 2.1 Create a relationship between two nodes
To create a relationship between two nodes, we first get the two nodes. Once the nodes are loaded, we simply create a relationship between them.
```
MATCH
  (a:Person),
  (b:Person)
WHERE a.name = 'Xingjian' AND b.name = 'Craig'
CREATE (a)-[r:RELTYPE]->(b)
RETURN type(r)
```
Result:
```
╒═════════╕
│"type(r)"│
╞═════════╡
│"RELTYPE"│
└─────────┘
```
- ### 2.2 Create a relationship and set properties
Setting properties on relationships is done in a similar manner to how it’s done when creating nodes. Note that the values can be any expression.
```
MATCH
  (a:Person),
  (b:Person)
WHERE a.name = 'Xingjian' AND b.name = 'Craig'
CREATE (a)-[r:RELTYPE {name: a.name + '<->' + b.name}]->(b)
RETURN type(r), r.name
```
Result:
```
╒═════════╤══════════════════╕
│"type(r)"│"r.name"          │
╞═════════╪══════════════════╡
│"RELTYPE"│"Xingjian<->Craig"│
└─────────┴──────────────────┘
```
- ### 2.3 Create Multiple Nodes and Relationships

```
CREATE
(ee:Person { name: "Emil", from: "Sweden", klout: 99})
(js:Person { name: "Johan",  from: "Sweden", learn: "surfing" }),
(ir:Person { name: "Ian", from: "England", title: "author" }),
(rvb:Person { name: "Rik", from:"Belgium", pet: "Orval" }),
(ally:Person { name: "Allision", from:"California", hobby: "surfing" }),
( ee )-[:KNOWS {since: 2001}]->(js),
( ee )-[:KNOWS]->(rvb),
( js )-[:KNOWS]->(js),
( ir )-[:KNOWS]->(ally),
( rvb )-[:KNOWS]->(ally)
```
Result:
```
Added 5 labels, created 5 nodes, set 16 properties, created 5 relationships, completed after 22 ms.
```
The graph constructed.   
![image](https://github.com/UselessOldQian/Project2Neo4j/blob/main/pic/graph.png)

### 3. Search
- ### 3.1 Search All Nodes
Use MATCH clause to search all the nodes.
```
MATCH (n) RETURN n
```
- ### 3.2 Search Nodes with Specific Lables and Attributes
Like SQL, you can use Where clause to search nodes with specific attributes or labels and use return to get
the result.
```
MATCH (ee:Person) WHERE ee.name = "Emil" and ee.from = "Sweden" RETURN ee
```
Result:
```
╒══════════════════════════════════════════╕
│"ee"                                      │
╞══════════════════════════════════════════╡
│{"name":"Emil","from":"Sweden","klout":99}│
└──────────────────────────────────────────┘
```
- ###3.3 Related nodes
The symbol -- means related to, without regard to type or direction of the relationship.
```
MATCH (ee:Person)--(friends) WHERE ee.name = "Rik"
RETURN ee,friends
```
Result:
```
╒═════════════════════════════════════════════╤═════════════════════════════════════════════════════════╕
│"ee"                                         │"friends"                                                │
╞═════════════════════════════════════════════╪═════════════════════════════════════════════════════════╡
│{"name":"Rik","from":"Belgium","pet":"Orval"}│{"name":"Allision","from":"California","hobby":"surfing"}│
├─────────────────────────────────────────────┼─────────────────────────────────────────────────────────┤
│{"name":"Rik","from":"Belgium","pet":"Orval"}│{"name":"Emil","from":"Sweden","klout":99}               │
└─────────────────────────────────────────────┴─────────────────────────────────────────────────────────┘
```
You can add '[:Relationship Type]' between '--' to specify the certain relationship to search. And you can use --> or <-- to identify the direction of relationship.
```
MATCH (ee:Person)-[:KNOWS]->(friends) WHERE ee.name = "Rik"
RETURN ee,friends
```
Result:
```
╒═════════════════════════════════════════════╤═════════════════════════════════════════════════════════╕
│"ee"                                         │"friends"                                                │
╞═════════════════════════════════════════════╪═════════════════════════════════════════════════════════╡
│{"name":"Rik","from":"Belgium","pet":"Orval"}│{"name":"Allision","from":"California","hobby":"surfing"}│
└─────────────────────────────────────────────┴─────────────────────────────────────────────────────────┘
```
- ### 3.4 Relationship variable in variable length relationships
When the connection between two nodes is of variable length, the list of relationships comprising the connection can be returned using the following syntax:
```
MATCH (n:Person {name: 'Rik'})-[:KNOWS*2]-(o:Person)
RETURN n.name,o.name
```
Result:
```
╒════════╤════════╕
│"n.name"│"o.name"│
╞════════╪════════╡
│"Rik"   │"Johan" │
├────────┼────────┤
│"Rik"   │"Ian"   │
└────────┴────────┘
```
- ### 3.5 Shortest Path
Finding a single shortest path between two nodes is as easy as using the shortestPath function. It is done like this:
```
MATCH
  (Rik:Person {name: 'Rik'}),
  (Johan:Person {name: 'Johan'}),
  p = shortestPath((Rik)-[*..3]-(Johan))
RETURN p
```
Result:
```
╒══════════════════════════════════════════════════════════════════════╕
│"p"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│[{"name":"Rik","from":"Belgium","pet":"Orval"},{},{"name":"Emil","from│
│":"Sweden","klout":99},{"name":"Emil","from":"Sweden","klout":99},{"si│
│nce":2001},{"learn":"surfing","name":"Johan","from":"Sweden"}]        │
└──────────────────────────────────────────────────────────────────────┘
```
![image](https://github.com/UselessOldQian/Project2Neo4j/blob/main/pic/path.png)

### 4 Update
- ### 4.1 Set a property
Use SET to set a property on a node or relationship:
```
MATCH (n {name: 'Rik'})
SET n.surname = 'Rikky'
RETURN n.name, n.surname
```
Result:
```
╒════════╤═══════════╕
│"n.name"│"n.surname"│
╞════════╪═══════════╡
│"Rik"   │"Rikky"    │
└────────┴───────────┘
```
- ### 4.2 Remove a property
```
MATCH (n {name: 'Rik'})
SET n.surname = null
RETURN n.name, n.surname
```
Result:
```
╒════════╤═══════════╕
│"n.name"│"n.surname"│
╞════════╪═══════════╡
│"Rik"   │null       │
└────────┴───────────┘
```
Or you can use Remove clause:
```
MATCH (n {name: 'Rik'})
Remove n.surname
RETURN n
```
Result:
```
╒═════════════════════════════════════════════╕
│"n"                                          │
╞═════════════════════════════════════════════╡
│{"name":"Rik","from":"Belgium","pet":"Orval"}│
└─────────────────────────────────────────────┘
```
### 5 Delete
To delete a node, use the DELETE clause.
```
MATCH (n:Person {name: 'UNKNOWN'})
DELETE n
```
This query is not for deleting large amounts of data, but is useful when experimenting with small example data sets.
```
MATCH (n)
DETACH DELETE n
```
When you want to delete a node and any relationship going to or from it, use DETACH DELETE.
```
MATCH (n {name: 'Andy'})
DETACH DELETE n
```
It is also possible to delete relationships only, leaving the node(s) otherwise unaffected.
```
MATCH (n {name: 'Andy'})-[r:KNOWS]->()
DELETE r
```