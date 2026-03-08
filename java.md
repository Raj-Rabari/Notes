```markdown
* `javac` compiler compile java source code and convert it into bytecode(which is platform independent).
* JVM will run bytecode on any machine but the JVM is platform dependent.
* JRE is a java run time environment that provides packages or class libraries to run the java program.



## Data types : 
`int`, `float`, `double`, `long`, `boolean`, `String`

## type casting =>
automatic type conversion occurs if both the types are compatible and the destination type is greater than the source type.
	
## String pool => 
all the String variables declared like below will be stored in speacial memory area called "String constant pool". which is part of JVM's method area.
	
```java
String name1 = "raj";

```

now if you create another variable like `String name2 = "raj"` then it will check in string pool if `"raj"` exist or not. if it exist it will assign reference of `"raj"` to the `name2`.
If you want to create two different string objects you have to create it using `String` constructor.

If you create two string variables with same value using `String` class constructor then it will create two new objects whose value will get stored in heap memory area and reference variable will be stored in stack memory area. If you still want to store string object in string pool area you can use `.intern()` method.

## function overloading =>

java allows multiple function definitions with same name but different return type,no. of arguments or different type of arguments. this concept known as function overloading.
which definition needs to be run when function is called is determinded during compilation phase.
