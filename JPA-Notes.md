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
	* A single object in a list is a [transient](https://en.wikipedia.org/wiki/Transient_(computer_programming)) instance.
	* Each instance has a value associated with each of their properties.
	* Each instance is defined by a [class](https://en.wikipedia.org/wiki/Class_(computer_programming))
	* Each instance can be uniquely identified by their [memory address](https://en.wikipedia.org/wiki/Memory_address).

### OOP Relationships
* Associations between objects cause one object to cause another to perform an action its behalf; these associations have `multiplicity` which is composed of `cardinality` and `direction`.
* `object oriented cardinality` - models the aspect of how many entities exist on each side of the relationship; denoted by a range of numbers (i.e. `0..1`)
	* View [PluralSight's tutorial on cardinality](https://app.pluralsight.com/player?course=java-persistence-api-21&author=antonio-goncalves&name=java-persistence-api-21-m4-relinh&clip=2&mode=live)
	* `one-to-one`
	* `one-to-many`
	* `many-to-one`
	* `many-to-many`
* `object oriented direction` - models the fact that an object refers to another object
	* `unidirection` - `A` can reference `B`, `B` cannot reference `A`  .
	* `bidirectional` `A` and `B` can refer to `B` and `A` respectively.
	* 



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
* Abstraction above JDBC that makes it possible model databases as objects.
* Has two main purposes:
	1. ability to map objects to relational database.
	2. ability to query these mapped objects.
* Maps an entity to an already existing table using sets of annotation.
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

## JPA Inheritance
* JPA has 3 strategies for modeling inheritance
	* `table-per-concrete-class`
		* all columns on root entity must be mapped to columns on child entity
		* no shared table
		* no shared column
		* no discriminator column
	* `single-table-per-class`
		* default inheritance strategy.
		* requires all child fields are nullable.
		* introduces redundancies.
	* `joined-subclass`
		* all columns on root entity must will be mapped to columns on child entity via join statements of two tables modeling each of entity's fields separately.
* JPA inheritance ensures that common fields within a hierarchy (i.e. `Id`) are abstracted into the superclass; Subclasses refer to the superclass's `Id` field.


## API

### Annotations
* After annotating each entity properly, JPA offers the ability to query them and their relationships in an object oriented way, without having to use the underlying database foreign keys and columns.



#### `@Entity`
* Annotates class signature
* **Description:**
	* Allows the persistence provider to recognize it as a persistence class.
	* An object representative of a snap shot of data from a database.
	* By default, maps this entity to a table whose name is the name of the annotated class. Can be rerouted via the `@Table` annotation
* **Pre-requesites for use:**
	* An interface cannot be an entity.
	* An enum cannot be an entity.
	* The class can be abstract or concrete.
	* The class must define a no-arg constructor.
	* Each `Entity` must be annotated with a respective `ID`.



#### `@Id`
* Annotates field declarations
* **Description:**
	* Denotes the primary key for this `Entity`.
	* Can be generated manually by application or by automatically by the persistence provider.
* **Pre-requisites for use:**
	* Class must be annotated with `@Entity`

	
	
	
#### `Table(name = "TABLE_NAME")`
* Annotates class signatures
* **Description:**
	* Routes this entity to a table whose name is the specified value.
* **Attributes:**
	* **Required:**
		* `name` - specifies the name of the table to route this entity to.
	* **Optional:**
		* `catalog` - respective named collection of schemas in an SQL-environment. 
		* `schema`- used to differentiate one set of tables from another

* **Pre-requesites for use:**
	* Class must be annotated with `@Entity`.
	
	
	
#### `@GeneratedValue(strategy = GenerationType.ENUM_VALUE)`
* Annotates `Id` fields.
* **Description:**
	* Specifies how the persistence provider will generate this value.
	* `GenerationType.SEQUENCE` - specifies the use of database SQL sequence
	* `GenerationType.IDENTITY` - uses a database identity column
	* `GenerationType.TABLE` - instructs provider to store the sequence name and its current value in a table, increasing the value of each time a new instance of the entity is persisted.
	* `GenerationType.AUTO` - default when nothing specified. Provider does generation of a key automatically. It will select an appropriate strategy for a particular database.
* **Pre-requesites for use:**
	* Field must be annotated with `@Id`.

	
#### `@DiscriminatorColumn`
* View [Pluralsight's Intro-to-JPA-Inheritance video](https://app.pluralsight.com/player?course=java-persistence-api-21&author=antonio-goncalves&name=java-persistence-api-21-m4-relinh&clip=9&mode=live)
* **Description:**
	* Allows the provider to know which row belongs to which entity.
	* Used as part of JPA's inheritance-modeling strategy.
	* Declared by the superclass.
* **Attributes:**
	* `discriminatorType = DiscriminatorType.ENUM_VALUE`
	* `name = "COLUMN_NAME"`
	* `columnDefinition = "TINYINT(1)"`
	
#### `@Column(name = "COLUMN_NAME")`
* **Description:**
	* This annotation reroutes the mapping of this field to a column with the specified name.
	* By defualt in JPA, fields map to a column whose name is the name of the instance variable. (i.e. - `firstName` field maps to `firstName` column).
* **Attributes:**
	* **Required:**
		* `name` - specifies the column name to route this field  to.
	* **Optional:**
		* `length` - specify the length of characters this `String` field can hold.
		* `nullable` - can be null.
* **Pre-requesites for use:**
	* Class must be annotated with `@Entity`.
	* Must annotate a `getter`, or field declaration.
	
	
	
#### `@Temporal(TemporalType.ENUM_VALUE)`
* Annotates a field / instance variable
* Specifies has to represent this `Temporal` java object in the database.
* **Valid arguments:**
	* `TemporalType.DATE` - least precision
	* `TemporalType.TIME` - higher precision
	* `TemporalType.TIMESTAMP` - highest precision
* **Pre-requesites for use:**
	* Class must be annotated with `@Entity`.
	* Field must be of a java `Temporal` type: `Date`, `LocalDate`, `TimeStamp`, etc.

#### `@Transient`
* Ensures JPA does not map this attribute.

#### `@Enumerated(EnumType.HOW_TO_PERSIST)`
* `EnumType.ORDINAL` - Instructs JPA to map this enumeration's `ordinal()` value to a respective `integer` value in the database.
* `EnumType.STRING` Instructs JPA to map this enumeration's `name()` value to a respective `varchar` in the database.



#### Cardinal Relationships
* `OneToOne`
* `@OneToMany`
* `@ManyToMany`
* `@ManyToOne`

* **Optional Attributes:**
 	* `cascade = ALL`
	* `cascade = {PERSIST, REMOVE, MERGE}`
		* if `EntityManager` invokes `persist`,`remove`, or `merge` on this entity, then its composite `cascaded` members be affected by the same method invokation.



## Frequently Asked Questions (FAQs)

### What is a discriminator column?
* Always in the table of the base entity.

### What is a cascading event?
* Process whereby something information is successively passed on


### What is fetching?
* The mechanism by which a client gets from one side of a relationship to another.
	* eager fetch - immediately
	* lazy fetch - defferered



### What is a Join Table?
* A join is a view of two tables linked by two foreign keys referring to each other's primary key.


### What is a Database Catalog?
* [Catalogs](https://stackoverflow.com/questions/7022755/whats-the-difference-between-a-catalog-and-a-schema-in-a-relational-database) are named collections of schemas in an SQL-environment. 



### What is Configuration by Exception?
* Unless specified differently, the JPA provider should apply default rules.
	* Having to supply a configuration is an exception to the rule.
* An entity's instance variables also become persistent following default mapping, also called `configuration by exception`.
* JDBC rules apply for mapping Java primitives through relational data-types.
	* `String` is mapped to `VARCHAR(255)`.
	* `Long` is mapped to `BIGINT`.
	* `Boolean` is mapped to `SMALLINT`
	* `Enum` is mapped to `INTEGER`

* **Other aliases for this phrase:**
	* Programming by exception
	* Convention over configuration

### What is an `Entity`?
* An entity is object which lives shortly in-memory, and persistently in a database.
* An entity is denoted using the `@Entity` annotation on a respective class signature.
* Entity's can be configured via `@Entity` annotation or `XML` configuration.]
	* **XML configuration takes precedence!**
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
	et.begin(); // begin a set of operations; a transaction

	em.merge(entity); // begin managing entity
	em.persist(entity); // begin persisting entity
	
	et.commit(); // execute all operations since transaction began
	```

### What is a `Managed Entity`?


### What is a `Query`?
* A query is a statement which describes a selection of entities from a database.
* Queries allow a client to search,  sort, aggregate, and analyze data.

### What is a `Service Object`?
* An application's business logic or individual functions are modularized and presented as services for consumer/client applications.
* Defines `CRUD` operations

### What is `CRUD`?
* `CRUD` is an interface which ensures an object can
	* `create` persist new entities into a database.
	* `read` entities into an application from a database.
	* `update` entities in a database.
	* `delete` entities from a database.


### What is `Java Persistence Query Language` (`JPQL`)?
* object oriented language for querying from relation database.
* retrieve an entity by any criteria.
* mocks SQL syntax, but rather than retrieving rows, it retrieve collections of entities.
* query is executed on underlying database with `SQL` and `JDBC` calls and the entity instances are the attributes set and are returned to the application.

* **SQL Syntax:**

```SQL
SELECT		*
FROM		item
WHERE		unit_cost > 100.00
ORDER BY	title;
```


* **JQL Syntax:**

```SQL
SELECT		i
FROM		Item i
WHERE		i.unitCost > 100.00
ORDER BY	i.title;
```

* Notice that JPQL uses the dot-notation to express reference to the _item's attribute_ as opposed to SQL using the _table's column-name_.
* JPQL manipulates objects and attributes, not tables and columns.




### What is `Persistence`?
* Persisting an entity is the operation of taking a transient object and storing its state to the database.
* This is typically done by an intermediate service object which references an `EntityManager`.


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

		* [Hibernate implementation](https://mvnrepository.com/artifact/org.hibernate/hibernate-entitymanager/3.3.2.GA)
			* `persistence.xml`

				```xml
				<provider>org.hibernate.ejb.HibernatePersistence</provider>
				```
			* `pom.xml`

				```xml
				<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-entitymanager -->
				<dependency>
				    <groupId>org.hibernate</groupId>
				    <artifactId>hibernate-entitymanager</artifactId>
				    <version>3.3.2.GA</version>
				    <type>pom</type>
				</dependency>
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
