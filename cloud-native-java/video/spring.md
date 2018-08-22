# Spring

## Terms
* Environment profile
	* let you describe sets of beans that need to be created differently in one environment versus another
	* labels a grouping of beans that changes from one environment to another
	* Beans that do not have a profile assigned to them are always activated.
	* Beans that have the profile `default` are activated only when there are no other active profiles.
	* You can specify the profile attribute in bean definitions with `@Bean`-provider methods with `@Profile`.

## Conjunctive APIs
* JNDI
	* mechanism for organizing configuration information and discovering and listening to services via `EventContext`.
	* can lookup and listen to any object (not just `DataSource`), assuming your JNDI service provider supports it. 


## Design Patterns
* HATEOAS
	* Hypermedia as the Engine of Application State

## Notable Classes
* `Environment`
	* has a `Profile`
* `DataSource`
	* database connection reference

* `DataSourceAutoConfiguration`
	* will contribute an embedded H2 datasource 

* `NamedParameterJdbcTemplate`
	* 

* `JdbcTemplateAutoConfiguration`
	* creator of JdbcTemplate objects

* `JdbcTemplate`
	* Implementation of template pattern
	* provides convenient utility methods that make working with JDBC easy.
	* handles resource initialization and acquisition, destruction, exception handling, and more

* `RowMapper`
	* Allows easy bridging between `ResultSet` and respective object types

	```java
RowMapper<Customer> rowMapper =
(rs, i) -> new Customer(rs.getLong("ID"), rs.getString("EMAIL"));
	```

* `PropertySourcesPlaceholderConfigurer`
	* implementation of `BeanFactoryPostProcessor`
	* must be registered as a static bean


## Fancy urls
* `localhost:8080/configprops`

## `application.properties`
* `	server.port={integervalue}`
	* tells `Spring` which port to run this application on
* `management.context-path`
	* tells `Spring`
* 

## Annotations
* `@ConfigurationProperties("prefix")`
	* annotates a class signature
	* Annotate a POJO and specify a prefix, and Spring will attempt to map all properties that start with that prefix to the POJO’s properties
	* tells Spring that this bean is to be used as the root for all properties starting with `prefix`.
* `@PropertySource`
	* configures a `PropertySource` from a `.properties` file.
* `@Value`
	* annotates a constructor parameters, setter methods, or fields (ill advised)
	* provides a way to inject environment values into constructors, setters, fields, etc.
	* values can be computed using the Spring Expression Language or using the property placeholder syntax, assuming one registers a `PropertySourcesPlaceholderConfigurer`
* `@Aspect`
	* Decorates `@Component`
* `@EnableAspectJAutoProxy`
	* Decorates
* `@RefreshScope`
	* Given a bean whose properties are dependent on dynamic requests, this annotation allows the bean to requery for the value, effectively refreshing it.
* `@SpringBootApplication`
	* annotates class signature
	* An aggregatory annotation of
		* `@Configuration`
		* `@ComponentScan`
		* `@EnableAutoConfiguration`
		
* `@Configuration`
	* annotates class signature
	* tells Spring to seek for `@Bean` definitions within scope of class
* `@Bean`
	* annotates non-void method
	* creates an instance of an object as a singleton
	* tells Spring to manage a dependency;
		* i.e. - instantiate it, make it available, manage the life cycle
* `@Scope("some-scope")`
	* decorates `@Bean` annotation to denote the scope within which the `Bean` lives
* `@ImportResource("myResourceFile.xml")`
	* annotates class signature
* `@Repository`
	* annotates class signature
	* denotes CRUD object
* `@Component`
	* annotates class signature
	* implementation of stereotype pattern
	* implementation of singleton pattern
	* does not implicitly persist a table?
* `@RepositoryRestResource`
	* annotates class signature
	* Enforces HATEOAS design pattern
* `@RestResource(path = "")`
	* annotates field declaration

* `@ConditionalOnMissingBean(Class<?> cls)`
	* decorates `@Configuration`
	* is self explanatory...

* `@ComponentScan`
	* tells Spring to discover other beans in the application context by scanning the current package (or below) and looking for all objects annotated with stereotype annotations like `@Component`
	* Spring perceives them on components and creates a new instance of the object on which they’re applied

* `@SpringBootTest`
	* indicates that this class is a Spring Boot test class
	* provides support to scan for a `ContextConfiguration` that tells the test class how to load the ApplicationContext.
	* If no `ContextConfiguration` classes are specified as a parameter to the `@SpringBootTest` annotation, the default behavior is to load the `ApplicationContext` by scanning for a `@SpringBootConfiguration` annotation on a class in the package root.

* `@AutoConfigureMockMvc`
	* injects a `MockMvc` instance in `MockMvc` fields annotated with `@Autowired`



## `pom.xml`

```xml
<plugin>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-maven-plugin</artifactId>
	<configuration>
		<executable>
			true
		</executable>
	</configuration>
</plugin>
```

* the code body below ensures that the jar generated by the project is executable upon reference rather than having to prefix it with `javac` etc.

```
<configuration>
	<executable>
		true
	</executable>
</configuration>
```