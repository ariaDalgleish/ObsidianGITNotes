
howtodoinJava.com/java-best-practices/ 
#### 1. Naming packages
Package names must be a group of words stating with all lowercase domain names ( com, org, net). Subsequent parts of the package name may be different according to an organization's own internal naming conventions.
``` 
package com.howtodoinjava.webapp.controller;
package com.company.myapplication.web.controller;
package com.google.searh.common; 
```
#### 2. Naming classes
In Java, class names generally should be **nouns**, in title-case with the first letter of each separate word capitalized.
```
public class ArrayList {}
public class Employee {}
```
#### 3. Naming Interfaces
Interface names should be **adjectives**. Interfaces should be in the title case with the first letter of each separate word capitalized. In some cases, interfaces can be **nouns** when they present a family of classes e.g. List and Map.
```
public interface Serializable {}
public interface Clonable {}
public interface Iterable {}
public interface List {}
``` 
#### 4. Naming Methods
Methods always **verbs**. They represent action and the method name should clearly state the action they perform. The method name can be single or 2-3 words as needed to clearly represent the action. Words should be in camel case notation.
```
public Long getID() {}
public void remove(Object o) {}
public Object update(Object o) {}
public Report getReportById(Long id){}
public Report getReportByName(String name) {}
```
#### 5. Naming Variables
All instance, static, and method parameter variable names should be in camel case notation. They should be short and enough to describe their purpose. Temporary variables can be a single character e.g. the counter in the loops.
	Java rules for naming variables:
	- names are case-sensitive;
	- a name can include Unicode letters, digits, and two special characters ($, _);
	- a name cannot start with a digit;
	- a name must not be a keyword (class, static, int, etc. are illegal names)
	- whitespaces are not allowed in the name of a variable.

Here are some valid names of variables
```
public Long id;
public EmployeeDao employeeDao;
private Properties properties;
for (int i = 0; i < list.size(); i++){
}
```
Invalid:
```
@ab, 1c, !ab, class
```

#### 6. Constant Naming Conventions
Java constants all **UPPERCASE** where words are separated by **underscore** character. Make sure to use the *final* modifier with constant variables.
```
public final String SECURITY_TOKEN = "...";
public final int INITIAL_SIZE = 16;
public final Integer MAX_SIZE = Integer.MAX;
```
#### 7. Naming Generic Types
Uppercase single letters. The letter 'T' for type is typically recommended. In JDK classes, 'E' is used for collection elements, 'S' is used for service loaders, and 'K' and 'V' are used for map keys and values.
```
public interface Map <K,V> {}
public interface List<E> extends Collection<E> {}
Iterator<E> iterator(){}
```
#### 8. Naming Enums
Enumeration names all uppercase letters.
```
enum Direction {NORTH, EAST, SOUTH, WEST}
```
#### 9. Naming Annotations
Title case notation. Can be adjectives, verbs, or nouns based on the requirements
```
public @interface FunctionalInterface {}
public @interface Deprecated {}
public @Async Documented {}
public @Test Documented {}
```