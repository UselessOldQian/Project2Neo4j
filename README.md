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


