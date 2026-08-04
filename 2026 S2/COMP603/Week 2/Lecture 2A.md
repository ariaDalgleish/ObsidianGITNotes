Contents:
- Java Arrays
- Java Collection Interfaces
- Iterator
- Set and HashSet
- List, ArrayList and LinkedList
- Map and HashMap
- Generics

### Java Arrays
- Declaring an array 
	- int[] myArray; 
	- int[] myArray = new int[5] 
		- give size when declared
	- String[] strings = new string[] {"one","two"} 
		- give values when declared
- Checking an arrays length
	- int arrayLength = myArray.length; 
		- gets size of the array
Looping over an array:
```
for (int i = 0; < myArray.length; i++) {....}
for (String string :stringArray2) {....}
```  

Advantages of arrays: Very efficient, fast access, type safe, Versatility (objects pointers characters, integers floating-point numbers)
Disadvantages: Fixed size. Expanding an array requires creating a new one.

### Collections:
Provides a set of **interfaces** (contains List, Set, and Map) and set of **classes** (ArrayList, HashSet, HashMap) that implement those interfaces.
Collections Framework is like a toolbox. Interfaces like List define what tools can do, and classes like ArrayList are the actual tools that do the work.

Common Interfaces with their classes:

| Interface | Common Classes                  | Description                               |
| --------- | ------------------------------- | ----------------------------------------- |
| List      | Array List, LinkedList          | Ordered collection that allows duplicates |
| Set       | HashSet, TreeSet, LinkedHashSet | Collection of unique elements             |
| Map       | HashMap, TreeMap, LinkedHashMap | Stores key-value pairs with unique keys   |

| Interface | Common Classes | Description                                                |
| --------- | -------------- | ---------------------------------------------------------- |
| List      | Array List,    | Resizable array that maintains order and allows duplicates |
|           | LinkedList     | List with fast insert and remove operations                |
| Set       | HashSet,       | Unordered collection of unique elements                    |
|           | TreeSet,       | Sorted set of unique elements (natural order)              |
|           | LinkedHashSet  | Maintains the order in which elements were inserted        |
| Map       | HashMap,       | Stores key-value pairs with unique keys                    |
|           | TreeMap,       | Sorted map based on the natural order of keys              |
|           | LinkedHashMap  | Maintains the order in which keys were inserted            |
|           |                |                                                            |
Use **List** classes when you care about order, you may have duplicates, and want to access elements by index
Use **Set** classes when you need to store unique values only. *No duplicate* elements
Use **Map** classes when you need to store pairs of keys and values, like a name and its phone number

Iterator 
Get an iterator from ArrayList by using the iterator() method
Loop through the items in the ArrayList
```
Iterator it = myList.iterator();
while(it.hasNext())
{
	System.out.print((String)it.next());
}
```

