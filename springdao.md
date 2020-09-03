## Spring DAO

1. `ORM` is a programming techinique for converting data between relational databases and object oriented programming languages such as Java, C#, etc. 

```
ORM :

1. An API to perform basic CRUD operations on objects of persistent classes. 
2. A language or API to specify queries that refer to classes and properties of classes. 
3. A configurable facility for specifying mapping metadata.
4. A technique to interact with transactional objectt to perform dirty checking , lazy association fetching and other optimization functions.
```

2. `Java Database Connectivity (JDBC)`. It provides a set of Java API for accessing the relational databases from Java program. These Java APIs enable Java programs to execute SQL statements and interact wuth any SQL compliant database. 
    * `ORM` comes in as more often than not, there is a mis-match between the objects in Java and the data in database. Therefore `ORM` is a technique to resolve this mis-match.
    
3. `Spring Data Access Object(DAO)` is one of the frameworks for `JAVA ORM(Object Relational Mapping) Framework`.

```
DAO pattern is a structural pattern that allows us to isolate the application/business layer from the persistence layer (usually a relational database, but it could be any other persistence mechanism) using an abstract API.
```
* Composition 
* [Dependency injection](https://github.com/JYL123/Notes/blame/master/principles.md#L3)

DAO coding example: https://www.baeldung.com/java-dao-pattern#using-the-pattern-with-jpa


Reference: 
* https://www.tutorialspoint.com/hibernate/orm_overview.htm
* https://www.baeldung.com/java-dao-pattern

