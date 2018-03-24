* What is an ORM tool?
* What iw JPA?
* What is not JPA?
* JPA Mapping annotation
	* to map out objects into database

* API
	* Set of CRUD operations used to query objects in java



# Mechanisms for Storing Data

## Relational Database Perspective
* A database stores data in tables.
* Tables store data in rows and columns.
	* Each row represents a single entity in a table.
	* Each column represents a single property of an entity.
	* Each table is defined by a [schema](https://en.wikipedia.org/wiki/Database_schema)
	* Each table must specify a column or group of columns called the [primary key](https://en.wikipedia.org/wiki/Primary_key).
		* ensures each row has a unique way to be identified

## Object Oriented Perspective
* An application stores data in Lists.
* Lists store data in Objects.
	* A single object in a list is an instance.
	* Each instance has a value associated with each of their properties.
	* Each instance is defined by a [class](https://en.wikipedia.org/wiki/Class_(computer_programming))
	* Each instance can be uniquely identified by their [memory address](https://en.wikipedia.org/wiki/Memory_address).



## Object Relational Mapping
* ORMs delegate tools the task of mapping between objects and table.
* In Java EE, the framework is called Java Persistence API or JPA.
* Objects have transient state
	* Only available when the JVM is running.
	* Objects need to be persisted sometimes.
* Relational Databases are a component which store State
* The framework for implementing




# JPA


## What is JPA?
* Abstraction above JDBC that makes it possible to be independent of databases
* Generates SQL statements and executes them using JDBC onto the underlying database.
* Brings easy mechanism for mapping objects to relational databases thanks to meta data
* Manages lifecycle of persistent objects
* Features include
	* `EntityManager` API to perform CRUD and db-related operations
	* Java Persistence Query Language
	* object-oriented query language

## JPA Implementations
* JPA has 3 implementations
	* EclipseLink
	* Hibernate
	* Apache Open JPA

## API

### Annotations
* **Notes**
	* After annotating each entity properly, JPA offers the ability to query them and their relationships in an object oriented way, withut having to use the underling db foreign keys and columns


* **Definitions:**
	* `@Entity`
		* An object representative of a snap shot of data from a database.
	* `Table(name = "tableName")`
		* Used in conjunction with `@Entity`
		* Denotes the table the entity is stored in.

### What is an `Entity`?
* An entity is denoted using the `@Entity` annotation on a respective class signature.
* An entity is object which lives shortly in-memory, and persistently in a database.
* Each entity consists of metadata.
* Each entity has some metadata that describes its relationship with an underlying database

### What is `MetaData`?
* Metadata is information that is held as a description of stored data.
* Additional metadata can be specified using annotations to further describe relationships.
	* Examples: `@Table`, `@Id`, `@GeneratedValue`
* To denote an entity is stored in a table, (e.g. a table named `people`), annotate the class signature with `@Table` (e.g. `@Table(name = "people")`
	* For example, given a Table of `Person` objects named `People`, one expects a `Person` entity to be declare a signature of

	```java
	@Entity
	@Table(name = "people")
	public class Person { ... }
	```
	
### What is an `EntityManager` ?
* The centralized service to manipulate instance of entity.
* Provide an API to create, find, remove, and synchronize objects with the database.
	* does **not** make use of an explicit `update` method as its synchronization should automatically update the state of a managed entity.
* Can perform basic query operations given a unique identifier.
* Can be obtained through `EntityManagerFactory`
	* `Persistence.createEntityManagerFactory("persistenceUnitName")`
* Can perform JPQL querys

	```java
	em.createQuery("SELECT person FROM people ORDER BY person.name")
	```

* Entities are not persisted until an `EntityManager` explicitly persists the object.
	* When an object is persisted, it is manageable by the `EntityManager` and eligible to be inserted into the database upon committing the transaction.

	```java
	em.persist(new Person())
	```

* Can perform a `merge`
	* Merge takes a detached object and returns a managed entity.

### What is an `EntityTransaction`?
* An abstraction that is used to group together a series of operations.
	* Ensure all operations succeed, or none of them are executed.
* Begins and commits transactions performed by `EntityManager`

### What is `JPQL`?
* Java Persistence Query Language
	* object oriented language for querying from relation database


### What is `Persistence`?
* Persisting an entity is the operation of taking a transient object and storing its state to the database.
* This is typically done by an intermediate service object which references an `EntityManager`.

### What is a `Service Object`?
* An application's business logic or individual functions are modularized and presented as services for consumer/client applications.
* Defines `CRUD` operations

### What is `CRUD`?
* `CRUD` is an interface which ensures an object can
	* `create` persist new entities into a database.
	* `read` entities into an application from a database.
	* `update` entities in a database.
	* `delete` entities from a database.


### What is a `Persistence Context`?
* A managed set of entity instances is called a persistence context.
* Is configured by a persistence unit
* Can have several persistence units.
* A first level cache.

### What is a `Persistence Unit`?

* Bridge between persistence context and database.
* an xml file called `persistence.xml`
	* `persistence-unit` tag has a `name` attribute.
	* `class` tags within a `persistence-unit` wrap class-paths of classes to be persisted.
	* `properties` tag tells persistence context:
		* which JDBC driver to use
		* where the database is located
		* username
		* password
* Named configuration of this set of entities.
* Ensures entites are persisting as configured
	* i.e. - ensure instances to be persisted have non-repeating ids within this context
