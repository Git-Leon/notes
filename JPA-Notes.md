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


## What is JPA?
* Abstraction above JDBC that makes it possible to be independent of databases
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
* To denote an entity is stored in a table, (e.g. a table named `people`), annotate the class signature with `@Table` (e.g. `@Table(name = "people")`
	* For example, given a Table of `Person` objects named `People`, one expects a `Person` entity to be declare a signature of

	```java
	@Entity
	@Table(name = "person")
	public class Person { ... }
	```
