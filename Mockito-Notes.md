# Test Driven Development
* The reference video is [here](https://app.pluralsight.com/player?course=test-driven-development-java&author=mike-nolan&name=test-driven-development-java-m4&clip=2&mode=live)
* practice of making tests 1 step ahead of code to help drive design of system
* design in conjunction with test in order to achieve more structured and modular design that supports testing immediately
* Ensures that issues are likely small segments that can be identified and repaired quickly.




## Problems with Guess-Driven-Development
* identify complexities of methods
* deferring the focus on a method's compositon risks inadvertently making a method too complex
* lacks the benefits of automation; cannot add features without knowing that you did not unintentionally break functionality
	* deferring automation increases the likelihood of unintentionally breaking core features by introducing future features.
* more testing allows you to more accurately estimate the required effort for each developmental step.






-
# Mocking Concepts

## Challenges with Testing with Dependendencies
* Live database needed
* Multiple users may need to interact with database
* Dependent component is not yet developed; you may have the contract of the interface defined, but the module's implementation may not be fully realized

## Mocking Frameworks give control
* Allow you to replace the dependency on implementation classes with a mocked implementation during test execution.
* Resolve the issue of:
	*  database dependency
	*  external system dependency
	*  implementation classes which are not yet developed
* Leverages the proxy pattern to provide dynamic and generic implementation of the dependent interface or extension of the dependent class
* Spring contains its own set of mocking capabilities



## Mockito Nuance
### Annotation Processor Configuration
* It has been commonly reported that Mockito may not be able to read annotations because it is not configured by your compiler.
* To configure this, open your IDE, and navigate to the `Annotation Processor` menu located in the `Compiler` option of your `Preferences` in Intellij.
	* 






-
# Mockito
