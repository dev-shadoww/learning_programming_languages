# Learning Java

## Hello, World

```java
public class main{
  public static void main(String[] args){
    System.out.print("Hello World!");
  }
}
```

## Data types and Variables

```java
byte byteVariable;
short shortVariable;
int intVariable;
long longVariable;

float floatVariable;
double doubleVariable;

char charVariable;
boolean booleanVariable;
```

```java
int intMaxValue = Integer.MAX_VALUE;
byte byteMaxValue = Byte.MAX_VALUE;
```

## Reading Values

```java
public class main{
  public static void main(String[] args){
    String user = System.console().readLine("Enter the value: ");

    int intValue = Number.parseInt(user);
    double doubleValue = Double.parseDouble(user);
  }
}
```

```java
import java.util.Scanner;

public class main{
  public static void main(String[] args){
    Scanner scanConsole = new Scanner(System.in);
    int intValue = scanConsole.next();
    String stringValue = scanConsole.nextLine();
    // Or

    Scanner scanFile = new Scanner(new file("input.txt"));
  }
}
```

## OOP

Class is a template for creating objects, and object is an instance of class.

The `static` values are on the main copy, that is class, but in case of `instance` fields, the value is associated with each instance, `static` and `instance` methods also work in a similar way.

Classes can be `public` meaning any other class can access it, `public` means no other class can access it, `protected` allows classes and subclasses in the same package.

```java
public class main{
  public static void main(String[] args){
    ExampleClass example = new ExampleClass();
    example.printIntValues();
  }
}
```

`ExampleClass.java`

```java
public class ExampleClass{
  private int privateIntValue = 2;
  public int publicIntValue = 4;
  protected protectedIntValue = 6;

  public void printIntValues(){
    System.out.println(privateIntValue, publicIntValue, protectedIntValue);
  }
}
```

### Constructors

```java
public class ExampleClass{
  private int privateIntValue = 2;
  public int publicIntValue = 4;
  protected protectedIntValue = 6;

  public ExampleClass(){
    System.out.println("Constructor is called!!");
  }
}
```

Constructor chaining is calling multiple constructor, which are overloaded, using `this` keyword.

```java
public class ExampleClass{
  private int privateIntValue = 2;
  public int publicIntValue = 4;
  protected protectedIntValue = 6;

  public ExampleClass(){
    this(8, 10, 12);
    System.out.println("Constructor is called!!");
  }

  public ExampleClass(int privateIntValue, int publicIntValue, int protectedIntValue){
    System.out.println("Constructor with arguments is called!!");

    this.privateIntValue = privateIntValue;
    this.publicIntValue  = publicIntValue;
    this.protectedIntValue = protectedIntValue;
  }
}
```

### Static and Instance Variables

If `Static` variable are changed, then it is changed in all of the instances, whereas `instance` variable change doesn't apply to other instances.

```java
public class ExampleClass(){
  public static intStaticValue;
  public intInstanceValue;
}
```

### Static methods and Instance methods

The `static` methods can be directly called from the class itself, without calling it on the object, but `instance` methods needs to be called from an instance of that class.

If a method doesn't use any fields or instance methods then it should probably be a static method.

```java
public class ExampleClass(){
  public static void greet(){
    System.out.println("Hello World!");
  }

  public void greetAgain(){
    System.out.println("Hello Again!");
  }
}

public class main{
  public static void main(String[] args){
    ExampleClass.greet();

    ExampleClass example = new ExampleClass();
    example.greetAgain();
  }

  public
}
```

### Plain Old Java Object

The `POJO` is a class that has only instance fields, in java it's called as `bean` or `javaBeans` or `Data Transfer Object`,

### Record

The `Record` type is the alternate for `POJO`.

```java
public record ExampleRecord(int intValue){}
```

The java declares each of the value as field (private and final), and it automatically creates a `toString()` method, and public access methods for each argument is also created, which have the same name as the argument, in this case `intValue()`.

### Annotations

Annotations are a type of metadata, which describes additional information about the code, it can be used by the compiler or preprocessor, to get additional info.

```java
@override
public void greet(){
  System.out.println("Hello World!!, Override");
}
```

### Inheritance

```java
public class ParentClassDefinition(){
  public intParentValue = 2;

  public ParentClassDefinition(){
    System.out.println("Parent Class Constructor!");
  }

  public void parentMethod(){
    System.out.println("From Parent Class!!");
  }
}
```

```java
public class ChildClassDefinition extends ParentClassDefinition(){
  public intChildValue = 4;

  public ChildClassDefinition(){
    super();

    System.out.println("Child Class Constructor!");
  }

  public void childMethod(){
    parentMethod();
    System.out.println("From Child Class!!");
  }
}
```

In `Inheritance` we can `override` a method, using the same method name, then the one from which it is called will be executed first, we can also use `super.parentMethod()` to call the method from parent.

### this and super

`this` is used for current class members, `super` is used for parent class members, `this()` is used to call the overloaded constructor, `super()` is used to call the parent constructor.

### Method overloading and overriding

Method `overloading` is providing two or more methods with the same name, but different parameters, it is also called as compile time polymorphism.

Method `overriding` is defining a method that already exists in the parent class with same name and arguments, it is also called as run time polymorphism.

Only instance methods can be overridden.

### String methods

- length
- charAt
- indexOf, lastIndexOf
- isEmpty
- isBlank
- contentEquals
- equals
- equalsIgnoreCase
- contains
- endsWith, startsWith
- regionMatches
- indent
- strip, stripLeading, stripTrailing, trim
- toLowerCase, toUpperCase

```java
public class main{
  public static void main(String[] args){
    StringBuilder stringExample = new StringBuilder("Hello World!");
  }
}
```

## Composition

Inheritance defines an `IS A` relationship, whereas Composition defines `HAS A` relationship, composition helps to add multiple classes and build one main class, it's more flexible than the inheritance.

```java
public class ParentClassDefinition(){
  public intParentValue = 2;

  public ParentClassDefinition(){
    System.out.println("Parent Class Constructor!");
  }

  public void parentMethod(){
    System.out.println("From Parent Class!!");
  }
}
```

```java
public class ChildClassDefinition extends ParentClassDefinition(){
  public intChildValue = 4;

  public ChildClassDefinition(){
    super();

    System.out.println("Child Class Constructor!");
  }

  public void childMethod(){
    parentMethod();
    System.out.println("From Child Class!!");
  }
}
```

```java
public class CompositionExample{
  public ChildClassDefinition childClass;

  public compositionExample(ChildClassDefinition childClass){
    super();
    this.childClass = childClass;
  }

  public void getChildClass{
    return childClass;
  }
}
```

```java
public class main{
  public static void main(String[] args){
    ChildClassDefinition childExample = new ChildClassDefinition();

    CompositionExample example = new CompositionExample(childExample);

    example.getChildClass().childMethod();
  }
}
```

## Encapsulation

It is hiding things, or making them private or inaccessible.
