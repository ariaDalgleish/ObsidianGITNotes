
Java Fundamentals
	Define/Declare Classes and Objects
	Standard I/O
	Program Entry - Main Method

OOP Concepts
	Encapsulation
	Abstraction
	Inheritance
	Polymorphism

OO Concepts in Java
	An object is a collection of: 
		Fields (object state, data members, instance variables)
		Methods (behaviors)
	Each obj has its own memory for maintaining state

`````js
class [ClassName] // This type objects are
{ // this type objects have
	field 1 
	field 2
	.... // How to create/initialise and object of this type
	constructor 1
	constructor 2
	.... // This type objects do
	method 1
	method 2
} 
`````

#### Polymorphism 

Car --> FerrariCar & HondaFitCar 

```
class Drive {
	public String driverName;
	public void drive (HondaFitCat hfitCar) {
		hfitCat.run();
	}
	public void drive (FerrariCar ferrariCar) {
		ferrariCar.run();
	}
}
````

```
class HondafitCar {
public void run(){
....
	}
}
````

```
class FerrariCar {
public void run(){
....
	}
}
````