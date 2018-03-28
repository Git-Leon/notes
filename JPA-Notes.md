# Mechanisms for Storing and Manipulating Data

## Relational Database Paradigm
* A database stores data in tables.
* Tables store data in rows and columns.
	* Each row represents a single entity in a table.
	* Each column represents a single property of an entity.
	* Each table is defined by a [schema](https://en.wikipedia.org/wiki/Database_schema)
	* Each table must specify a column or group of columns called the [primary key](https://en.wikipedia.org/wiki/Primary_key).
		* ensures each row has a unique way to be identified

## Object Oriented Paradigm
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
	* `EntityManager` API to perform CRUD and database-related operations
	* Java Persistence Query Language, an object-oriented query language

## JPA Implementations
* JPA has 3 implementations
	* EclipseLink
	* Hibernate
	* Apache Open JPA

## API

### Annotations
* **Notes**
	* After annotating each entity properly, JPA offers the ability to query them and their relationships in an object oriented way, without having to use the underlying database foreign keys and columns.


* **Definitions:**
	* `@Entity`
		* Annotates class signatures
		* An object representative of a snap shot of data from a database.
		* Each `Entity` must be annotated with a respective `ID`.
	* `@Id`
		* Annotates field declarations
		* Denotes the primary key for this `Entity`.
	* `Table(name = "tableName")`
		* Annotates class signatures
		* Used in conjunction with `@Entity`
		* Denotes the table the entity is stored in.

### What is an `Entity`?
* An entity is object which lives shortly in-memory, and persistently in a database.
* An entity is denoted using the `@Entity` annotation on a respective class signature.
* An entity consists of metadata.
* An entity has some metadata that describes its relationship with an underlying database

### What is `MetaData`?
* Metadata is information that is held as a description of stored data.
* Additional metadata can be specified using annotations to further describe relationships.
	* Examples: `@Table`, `@Id`, `@GeneratedValue`
* To denote an entity is stored in a table, (e.g. a table named `people`), annotate the class signature with `@Table` (e.g. `@Table(name = "people")`
	* For example, given a Table of `Person` objects named `People`, one expects a `Person` entity with an annotated class signature of

	```java
	@Entity
	@Table(name = "people")
	public class Person { ... }
	```
	
### What is an `EntityManager` ?
* The centralized service to manipulate instance of entity.
* Provides a `CRUD` API to create, find, remove, and synchronize objects with the database.
	* does **not** make use of an explicit `update` method as its synchronization should automatically update the state of a managed entity.
* Can be obtained through `EntityManagerFactory`

	```java
	EntityManagerFactory emf = Persistence.createEntityManagerFactory("persistenceUnitName")
	EntityManager em = emf.createEntityManager();
	```
	
* Can perform basic query operations given a unique identifier.

	```java
	Long id = 0;
	Person person = em.find(Person.class, id);
	```

* Can perform JPQL querys

	```java
	String jpql = "SELECT person FROM people ORDER BY person.name";
	Query query = em.createQuery(jpql);
	query.executeUpdate();
	```
	
* Can perform a `merge`
	* Merge takes a detached object and returns a managed entity.

	```java
	Person managedEntity = em.merge(new Person())
	```

* Can perform a `persist`
	* Entities are not persisted until an `EntityManager` explicitly persists the object.
	* When an object is persisted, it is manageable by the `EntityManager` and eligible to be inserted into the database upon committing the transaction.

	```java
	em.persist(new Person())
	```

### What is an `EntityTransaction`?
* An abstraction that is used to group together a series of operations.
	* Ensures all operations succeed, or none of them are executed.
* Can be obtained from `EntityManager`

	```java
	EntityTransaction et = em.getTransaction();
	```

* Begins and commits transactions performed by `EntityManager`
	
	```java
	et.begin();
	
	em.persist(entity);
	
	et.commit();
	```

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
* Named configuration of this set of entities.
* Ensures entites are persisting as configured
	* i.e. - ensure instances to be persisted have non-repeating ids within this context
* an xml file called `persistence.xml`
	* `persistence-unit` tag has a `name` attribute.
	* `class` tag must be embedded within `persistence-unit`
		* wraps around class-paths of classes to be persisted.


	* `property` tag tells persistence context:
		* which JDBC driver to use
		* where the database is located
		* username
		* password
		* a property with a name prefixed with `javax.persistence.` is _portable_; it will be interpreted by all JPA provider implementations.

		* The below xml snippet is an example of a property configuration such that
			* `javax.persistence.jdbc.driver`
				* tells persistence context which JDBC driver to use
			* `javax.persistence.jdbc.url`
				* where the database is located
			* `javax.persistence.jdbc.user`
				* user name
			* `javax.persistence.jdbc.password`
				* password

			* `database-product-name`
				* the persistence context must perform mapping on a specified-type database, `Derby`
					* (`Oracle`, `MySQL`, or `DB2` are also valid)
			* `schema-generation.database.action`
				* instructs provider to drop and create the database schema
			* `schema-generation.scripts.action`
				* the persistence context can generate the DDL scripts of the database.
				* this attribute enforces the setting of `schema-generation.scripts.create-target`
				* this attribute enforces the setting of `schema-generation.scripts.drop-target`
			* `schema-generation.scripts.create-target`
				* name of file which contains all `CREATE` statements
			* `schema-generation.scripts.drop-target`
				* name of file which contains all `DROP` statements


			```xml
			<properties>
				 <property name="javax.persistence.jdbc.driver"
				      value="org.hsqldb.jdbcDriver"/>
				
				<property name="javax.persistence.jdbc.url"
				      value="objectdb://localhost/my.odb"/>
				
				<property name="javax.persistence.jdbc.user"
				      value="root"/>
				
				
				<property name="javax.persistence.jdbc.password"
				      value=""/>
                      
				<property name="javax.persistence.database-product-name"
					value = "Derby"/>
					
				<property name="javax.persistence.schema-generation.database.action"
					value = "drop-and-create"/>

				<property name="javax.persistence.schema-generation.scripts.action"
					value="drop-and-create"/>

				<property name="javax.persistence.schema-generation.scripts.create-target"
					value="create.ddl"/>

				<property name="javax.persistence.schema-generation.scripts.drop-target"
					value="drop.ddl"/>
					
				<property name="eclipselink.logging.level"
					value="INFO"/>
			</properties>
			```
	



	* `provider` tag tells each persistence context
		* Having issues with this? 
		* Visit this [gist of different provider configuration](https://gist.github.com/sudiptasharif/7ef40d5a495bced5f15710cbe8fb268a)
			* [resource1](https://stackoverflow.com/questions/40683423/i-cant-find-resolve-persistenceexception-no-persistence-provider-for-entityman)
			* [resource2](https://stackoverflow.com/questions/39410183/hibernate-5-2-2-no-persistence-provider-for-entitymanager)

		* Hibernate implementation
			* `persistence.xml`

				```xml
				<provider>org.hibernate.ejb.HibernatePersistence</provider>
				```



		* [EclipseLink implementation](https://mvnrepository.com/artifact/org.eclipse.persistence/org.eclipse.persistence.jpa/2.7.1)
			* `persistence.xml`

				```xml
			<provider>org.eclipse.persistence.jpa.PersistenceProvider</provider>
			```

			* `pom.xml`

				```xml
				<dependency>
				    <groupId>org.eclipse.persistence</groupId>
				    <artifactId>eclipselink</artifactId>
				    <version>2.5.0</version>
				</dependency>
				```
