## Qualities
- The best advice then is: when in doubt, leave it out
- Add Virtual Functions judiciously.
  * A class with no virtual functions tends to be more robust and requires less maintenance than one with virtual functions.
  * if your API does not call a particular method internally, then that method probably should not be virtual.
  * prefer to make virtual functions private or protected when required P48
  * Virtual function rules P48
- an API should only provide one way to perform one task
- do not mix your convenience API in the same classes as your core API.
- Indeed, coming up with clear, descriptive, and appropriate names can be one of the most difficult tasks in API design.
- should also be difficult to misuse. e.g.
  * Prefer enums to booleans to improve code readability.
  * Avoid functions with multiple parameters of the same type.
- orthogonality means that methods do not have side effects.
- different operations can all be applied to each available data type
- Use of these smart pointers
- coupling and cohesion P63-64
  * Coupling by Name Only P64
  * Scott Meyers recommends that whenever you have a choice, you should prefer declaring a function as a non-member non-friend function rather than as a member function. And you could declare both of these within a single namespace
- Data redundancy can sometimes be justified to reduce coupling between classes.
- Callbacks, Observers, and Notifications P70
  * callbacks are a popular technique to break cyclic dependencies in large projects
  * An alternative solution is to build a centralized mechanism to send notifications, or events P73

## Patterns
- Pimpl P77
  * in general, putting all private member variables and private methods in the Implclass.
  * Make your class uncopyable, or Explicitly define the copy semantics
  * Advantages P83
- Singleton
  * There are several alternatives to the Singleton pattern, including dependency injection, the Monostate pattern, and use of a session context
- Factory Method
  * registalbe mapping
- Observer
  * An Observer lets you decouple components and avoid cyclic dependencies

## Design
- good API design is a journey, not a first step.
- Good API design is about putting in place a stable logical interface to solve a problem.
- non-functional requirements P122
- Process P132
  * Constrains P133
  * Domains 6 types P136
-  architectural layers of an API P139
- Focus on designing 20% of the classes that define 80% of your API’s functionality.
- Class Design Options
  * Design for inheritance or prohibit it?
  * you should avoid the use of multiple inheritance, except to use abstract interfaces or mixin classes
  * The Law of Demeter P150
- Function Design Options P152
  * make sure that you use the right data type for your parameters
  * minimize the number of parameters to your public functions. five
  * each of the setter methods return a reference to its object instance
  * Error Handling P156

## Styles
- four very different API styles P161
  * C
  * OO
  * template
  * Data driven

## C++ Usage
- you should follow the rule of The Big Three
- Prefer to return the result of a function by value rather than const reference.
- Prefer the use of const references over pointers for input parameters where feasible.
- For output parameters, consider using pointers over non-const references to indicate explicitly to the client that they may be modified.
- Prefer overloaded functions to default arguments

## Performance
- you should never trust your instincts on which parts of your implementation you think will be slow.
- always remember Amdahl’s law
- Cluster member variables by their type to optimize object size
- don’t inline code. Only for getter/setter and template
- One of the best ways to save memory is to not allocate any until you really need to. Use copy-on-write semantics
- Adopt an iterator model for traversing simple linear data structures.

## Version
- version API P254

## Test
- Use assertions to document and verify programming errors that should never occur.
- Record and Play