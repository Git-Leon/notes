# Chapter 4. Testing
## testing notes
* A class annotated with a `@RunWith(SpringRunner.class)` annotation—indicating that no ApplicationContext will be loaded during test execution.
## Notable Classes
* `ApplicationContext`
	* 

* `TestEntityManager`
	* convenience class from Spring Boot that supports a useful subset of a proper JPA EntityManager along with some extra utility methods that simplify commonly used idioms in tests.
	* useful component used in the scope of JPA repository tests that allows you to interact with the underlying datastore to persist objects without needing to use a repository
* `MockRestServiceServer`
	* 

* 


## Terms
* mock objects
	* allow us to isolate parts of the system under test by replacing collaborating components of a module with a simulated object that targets testing behavior in a controlled way
* integration testing
	* focuses on writing and executing tests against a group of software modules that depend on one another.
	* any test that requires access to the Spring application context (the `ApplicationContext`) during test execution. 

* unit tests
	* written in such a way that a Spring application context is not required.
* end to end testing
	* ensures that release components of a distributed application can be changed without breaking consumers
	* focuses on validating the functionality of an application’s business features.
	* focuses on testing features from the user’s perspective
* Consumer-Driven Contract Testing (CDC-T)
	* practice of using published contracts to assert and maintain expectations between consumers and producers while preserving loose coupling between services
	* first introduced by Ian Robinson in 2006
* Spring Cloud Contract
	* open source project in the Spring portfolio that provides framework components using a variant of consumer-driven contracts.

## Annotations
* `@RunWith(SpringRunner.class)`
	* annotates a class
	* expresses that no `ApplicationContext` will be loaded during test execution.
* `@JsonTest`
	* annotates a class
	* allows activation of the configuration to test `JSON` serialization and deserialization
* `@MockBean`
	* instructs Spring to provide a mock of a bean in the application context, and to effectively mute the definition of the original, live bean in the application context.
	* creates a Mockito mock for a bean inside the ApplicationContext.

* `@SpringBootTest`
	* annotates a class
	* indicates that this class is a Spring Boot test class
	* provides support to scan for a `ContextConfiguration` that tells the test class how to load the ApplicationContext.
	* If no `ContextConfiguration` classes are specified as a parameter to the `@SpringBootTest` annotation, the default behavior is to load the `ApplicationContext` by scanning for a `@SpringBootConfiguration` annotation on a class in the package root.
	* should be used when you want to write integration tests on a fully configured `ApplicationContext` in a Spring Boot application.
	* allows configuration of the servlet environment for testing context.
	* supports a `webEnvironment` attribute to describe how Spring Boot should configure the embedded servlet container that your application uses at runtime	

* `@WebMvcTest`
	* annotates class signature
	* takes an argument of a `Controller` class
	* supports testing individual Spring MVC controllers in a Spring Boot application.
	* auto-configures the necessary Spring MVC infrastructure needed to test interactions with controller methods.

* `@DataJpaTest`
	* useful for Spring Boot applications that use the Spring Data JPA project
* `@RestClientTest`
	* provides support to test Spring’s `RestTemplate` and its interaction with REST services.
* `@AutoConfigureStubRunner`
	* 

*