# Spring AOP

## Classes
* ProceedingJoinPoint
	* 
* 


## Terms
* aspect
	* a modularization of a concern that cuts across multiple classes.
	* Transaction management is a good example of a crosscutting concern in J2EE applications. 

* advice
	* is associated with a pointcut expression
	* runs before, after, or around method executions matched by the pointcut
	* The pointcut expression may be a reference to a named pointcut or declared in place

* join point
	* a step of the program execution, such as the execution of a method or the handling of an exception.
	* always represents a method executionin Spring AOP.

* pointcut
	* a predicate that matches the join points

* pointcut expression language
	* is a way of describing pointcuts programmatically.

* pointcut signature
	* the method declaration of a pointcut

* pointcut designator (PCD)
	* a keyword telling Spring AOP what to match


# Annotations
* `@Aspect`
* `@EnableAspectJAutoProxy`
	* activate Spring’s AOP functionality

* `@Pointcut("")`
	* annotates a method signature
	* can be referenced by other Pointcuts via method name
		* `@Poincut("methodName1() && methodName2()")`
	* takes an argument of a pointcut designator
		* `@Pointcut("execution(...)")`
		* `@Pointcut("within(...)")`
		* `@Pointcut("target(...)")`
		* `@Pointcut("this(...)")`
 		* `@Pointcut("@target(...)")`
 		* `@Pointcut("@args(...)")`
 		* `@Pointcut("@within(...)")`
 		* `@Pointcut("@annotation(...)")`


	