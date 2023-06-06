# JAVA-KOTLIN

1. [What’s the Target Platform of Kotlin? How is Kotlin-Java interoperability possible?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-target-platform-of-kotlin-how-is-kotlin-java-interoperability-possible)
    
    Java Virtual Machine(JVM) is the Target Platform of Kotlin. Kotlin is 100% interoperable with Java since both, on compilation produce bytecode. Hence Kotlin code can be called from Java and vice-versa.
    
2. [How do you declare variables in Kotlin? How does the declaration differ from the Java counterpart?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#how-do-you-declare-variables-in-kotlin-how-does-the-declaration-differ-from-the-java-counterpart)
    
    There are two major differences between Java and Kotlin variable declaration:
    
    - **The type of declaration** In Java the declaration look like this:
        
        ```
        String s = "Java String";
        int x = 10;
        
        ```
        
        In Kotlin the declaration looks like:
        
        ```
        val s: String = "Hi"
        var x = 5
        
        ```
        
        In Kotlin, the declaration begins with a `val` and a `var` followed by the optional type. Kotlin can automatically detect the type using type inference.
        
    - **Default value** The following is possible in Java:
        
        ```
        String s:
        
        ```
        
        The following variable declaration in Kotlin is not valid.
        
        ```
        val s: String
        
        ```
        
3. [What’s the difference between val and var declaration? How to convert a String to an Int?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-difference-between-val-and-var-declaration-how-to-convert-a-string-to-an-int)
    
    `val` variables cannot be changed. They’re like final modifiers in Java. A `var` can be reassigned. The reassigned value must be of the same data type.
    
    ```
    fun main(args: Array<String>) {
        val s: String = "Hi"
        var x = 5
        x = "6".toInt()
    }
    
    ```
    
    We use the `toInt()` method to convert the String to an Int.
    
4. [What’s Null Safety and Nullable Types in Kotlin? What is the Elvis Operator?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-null-safety-and-nullable-types-in-kotlin-what-is-the-elvis-operator)
    
    Kotlin puts a lot of weight behind null safety which is an approach to prevent the dreaded Null Pointer Exceptions by using nullable types which are like `String?`, `Int?`, `Float?` etc. These act as a wrapper type and can hold null values. A nullable value cannot be added to another nullable or basic type of value. To retrieve the basic types we need to use safe calls that unwrap the Nullable Types. If on unwrapping, the value is null we can choose to ignore or use a default value instead. The Elvis Operator is used to safely unwrap the value from the Nullable. It’s represented as `?:` over the nullable type. The value on the right hand side would be used if the nullable type holds a null.
    
    ```
    var str: String?  = "JournalDev.com"
    var newStr = str?: "Default Value"
    str = null
    newStr = str?: "Default Value"
    
    ```
    
    ![https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-null-safety-elvis-operator.png](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-null-safety-elvis-operator.png)
    
5. [What’s a `const`? How does it differ from a `val`?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-a-const-how-does-it-differ-from-a-val)
    
    By default `val` properties are set at runtime. Adding a const modifier on a `val` would make a compile-time constant. A `const` cannot be used with a `var` or on its own. A `const` is not applicable on a local variable.
    
    ![https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-const-val.png](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-const-val.png)
    
6. [Does Kotlin allow us to use primitive types such as int, float, double?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#does-kotlin-allow-us-to-use-primitive-types-such-as-int-float-double)
    
    At the language level, we cannot use the above-mentioned types. But the JVM bytecode that’s compiled does certainly have them.
    
7. [What’s the entry point of every Kotlin Program?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-entry-point-of-every-kotlin-program)
    
    The `main` function is the entry point of every Kotlin program. In Kotlin we can choose not to write the main function inside the class. On compiling the JVM implicitly encapsulates it in a class. The strings passed in the form of `Array<String>` are used to retrieve the command line arguments.
    
8. [How is `!!`different from ?. in unwrapping the nullable values? Is there any other way to unwrap nullable values safely?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#how-is-different-from-in-unwrapping-the-nullable-values-is-there-any-other-way-to-unwrap-nullable-values-safely)
    
    `!!` is used to force unwrap the nullable type to get the value. If the value returned is a null, it would lead to a runtime crash. Hence a `!!` operator should be only used when you’re absolutely sure that the value won’t be null at all. Otherwise, you’ll get the dreaded null pointer exception. On the other hand, a ?. is an Elvis Operator that does a safe call. We can use the lambda expression `let` on the nullable value to unwrap safely as shown below.Here the let expression does a safe call to unwrap the nullable type.
    
    ![https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-let.png](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-let.png)
    
9. [How is a function declared? Why are Kotlin functions known as top-level functions?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#how-is-a-function-declared-why-are-kotlin-functions-known-as-top-level-functions)
    
    ```
    fun sumOf(a: Int, b: Int): Int{
        return a + b
    }
    
    ```
    
    A function’s return type is defined after the `:` Functions in Kotlin can be declared at the root of the Kotlin file.
    
10. [What’s the difference between == and === operators in Kotlin?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-difference-between-and-operators-in-kotlin)

```
\== is used to compare the values are equal or not. === is used to check if the references are equal or not.

```

1. [List down the visibility modifiers available in Kotlin. What’s the default visibility modifier?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#list-down-the-visibility-modifiers-available-in-kotlin-what-s-the-default-visibility-modifier)

```
-   public
-   internal
-   protected
-   private

`public` is the default visibility modifier.

```

1. [Does the following inheritance structure compile?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#does-the-following-inheritance-structure-compile)

```
```
class A{
}

class B : A(){

}
```

**NO**. By default classes are final in Kotlin. To make them non-final, you need to add the `open` modifier.

```
open class A{
}

class B : A(){

}
```

```

1. [What are the types of constructors in Kotlin? How are they different? How do you define them in your class?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-are-the-types-of-constructors-in-kotlin-how-are-they-different-how-do-you-define-them-in-your-class)

```
Constructors in Kotlin are of two types: **Primary** - These are defined in the class headers. They cannot hold any logic. There's only one primary constructor per class. **Secondary** - They're defined in the class body. They must delegate to the primary constructor if it exists. They can hold logic. There can be more than one secondary constructors.

```
class User(name: String, isAdmin: Boolean){

constructor(name: String, isAdmin: Boolean, age: Int) :this(name, isAdmin)
{
    this.age = age
}

}
```

```

1. [What’s init block in Kotlin](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-init-block-in-kotlin)

```
`init` is the initialiser block in Kotlin. It's executed once the primary constructor is instantiated. If you invoke a secondary constructor, then it works after the primary one as it is composed in the chain.

```

1. [How does string interpolation work in Kotlin? Explain with a code snippet?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#how-does-string-interpolation-work-in-kotlin-explain-with-a-code-snippet)

```
String interpolation is used to evaluate string templates. We use the symbol $ to add variables inside a string.

```
val name = "Journaldev.com"
val desc = "$name now has Kotlin Interview Questions too. ${name.length}"
```

Using `{}` we can compute an expression too.

```

1. [What’s the type of arguments inside a constructor?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-type-of-arguments-inside-a-constructor)

```
By default, the constructor arguments are `val` unless explicitly set to `var`.

```

1. [Is new a keyword in Kotlin? How would you instantiate a class object in Kotlin?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#is-new-a-keyword-in-kotlin-how-would-you-instantiate-a-class-object-in-kotlin)

```
**NO**. Unlike Java, in Kotlin, new isn't a keyword. We can instantiate a class in the following way:

```
class A
var a = A()
val new = A()
```

```

1. [What is the equivalent of switch expression in Kotlin? How does it differ from switch?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-is-the-equivalent-of-switch-expression-in-kotlin-how-does-it-differ-from-switch)

```
when is the equivalent of `switch` in `Kotlin`. The default statement in a when is represented using the else statement.

```
var num = 10
    when (num) {
        0..4 -> print("value is 0")
        5 -> print("value is 5")
        else -> {
            print("value is in neither of the above.")
        }
    }
```

`when` statments have a default break statement in them.

```

1. [What are data classes in Kotlin? What makes them so useful? How are they defined?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-are-data-classes-in-kotlin-what-makes-them-so-useful-how-are-they-defined)

```
In Java, to create a class that stores data, you need to set the variables, the getters and the setters, override the `toString()`, `hash()` and `copy()` functions. In Kotlin you just need to add the `data` keyword on the class and all of the above would automatically be created under the hood.

```
data class Book(var name: String, var authorName: String)

fun main(args: Array<String>) {
val book = Book("Kotlin Tutorials","Anupam")
}
```

Thus, data classes saves us with lot of code. It creates component functions such as `component1()`.. `componentN()` for each of the variables. [![kotlin interview questions data classes](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-data-classes.png)](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-data-classes.png)

```

1. [What are destructuring declarations in Kotlin? Explain it with an example.](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-are-destructuring-declarations-in-kotlin-explain-it-with-an-example)

```
Destructuring Declarations is a smart way to assign multiple values to variables from data stored in objects/arrays. [![kotlin interview questions destructuring declarations](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-destructuring-declarations.png)](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-destructuring-declarations.png) Within paratheses, we've set the variable declarations. Under the hood, destructuring declarations create component functions for each of the class variables.

```

1. [What’s the difference between inline and infix functions? Give an example of each.](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-difference-between-inline-and-infix-functions-give-an-example-of-each)

```
[Inline functions](/community/tutorials/kotlin-inline-function-reified) are used to save us memory overhead by preventing object allocations for the anonymous functions/lambda expressions called. Instead, it provides that functions body to the function that calls it at runtime. This increases the bytecode size slightly but saves us a lot of memory. [![kotlin interview questions inline functions](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-inline-functions.png)](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-inline-functions.png) [infix functions](/community/tutorials/kotlin-functions) on the other are used to call functions without parentheses or brackets. Doing so, the code looks much more like a natural language. [![kotlin interview questions infix notations](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-infix-notations.png)](https://journaldev.nyc3.digitaloceanspaces.com/2018/04/kotlin-interview-questions-infix-notations.png)

```

1. [What’s the difference between lazy and lateinit?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-difference-between-lazy-and-lateinit)

```
Both are used to delay the property initializations in Kotlin `lateinit` is a modifier used with var and is used to set the value to the var at a later point. `lazy` is a method or rather say lambda expression. It's set on a val only. The val would be created at runtime when it's required.

```
val x: Int by lazy { 10 }
lateinit var y: String
```

```

1. [How to create Singleton classes?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#how-to-create-singleton-classes)

```
To use the singleton pattern for our class we must use the keyword `object`

```
object MySingletonClass
```

An `object` cannot have a constructor set. We can use the init block inside it though.

```

1. [Does Kotlin have the static keyword? How to create static methods in Kotlin?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#does-kotlin-have-the-static-keyword-how-to-create-static-methods-in-kotlin)

```
**NO**. Kotlin doesn't have the static keyword. To create static method in our class we use the `companion object`. Following is the Java code:

```
class A {
  public static int returnMe() { return 5; }
}

```

The equivalent Kotlin code would look like this:

```
class A {
  companion object {
     fun a() : Int = 5
  }
}
```

To invoke this we simply do: `A.a()`.

```

1. [What’s the type of the following Array?](https://www.digitalocean.com/community/tutorials/kotlin-interview-questions#what-s-the-type-of-the-following-array)

```
```
val arr = arrayOf(1, 2, 3);
```

The type is Array<Int>.
```

    
    1-**Difference between method overloading and overriding:**

- Overloading happens at compile-time while Overriding happens at runtime: The binding of overloaded method call to its definition happens at compile-time however binding of overridden method call to its definition happens at runtime. More info on static vs. dynamic binding: [StackOverflow](https://stackoverflow.com/questions/19017258/static-vs-dynamic-binding-in-java).
- Static methods can be overloaded which means a class can have more than one static method of same name. Static methods cannot be overridden, even if you declare a same static method in child class it has nothing to do with the same method of parent class as overridden static methods are chosen by the reference class and not by the class of the object.
- The most basic difference is that overloading is being done in the same class while for overriding base and child classes are required. Overriding is all about giving a specific implementation to the inherited method of parent class.
    
    Static binding is being used for overloaded methods and dynamic binding is being used for overridden/overriding methods. Performance: Overloading gives better performance compared to overriding. The reason is that the binding of overridden methods is being done at runtime.
    
    Private and final methods can be overloaded but they cannot be overridden. It means a class can have more than one private/final methods of same name but a child class cannot override the private/final methods of their base class.
    
    Return type of method does not matter in case of method overloading, it can be same or different. However in case of method overriding the overriding method can have more specific return type (meaning if, for example, base method returns an instance of Number class, all overriding methods can return any class that is extended from Number, but not a class that is higher in the hierarchy, like, for example, Object is in this particular case).
    
    Argument list should be different while doing method overloading. Argument list should be same in method Overriding. It is also a good practice to annotate overridden methods with `@Override` to make the compiler be able to notify you if child is, indeed, overriding parent's class method during compile-time.
    
    2-What is the difference between java and kotlin for “Protected” mofier?
    
    • The protected modifier in Kotlin means that it is strictly accessible only by the declaring class and subclasses. This is the same as most people expect Java to work, but subtly different from how Java works. In Java, the protected modifier also allows access to the element from anything else in the same package.
    

3- what is Internal modifier and what is module in kotlin?

Internal is a new modifier available in Kotlin that’s not there in Java. Setting a declaration as internal means that it’ll be available in the same module only. By module in Kotlin, we mean a group of files that are compiled together.

4-**[What is the difference between init block and constructor in kotlin?](https://stackoverflow.com/questions/55356837/what-is-the-difference-between-init-block-and-constructor-in-kotlin)**

The **init** block will execute immediately after the primary constructor. Initializer blocks effectively become part of the primary constructor.

The **constructor** is the secondary constructor. Delegation to the primary constructor happens as the first statement of a secondary constructor, so the code in all initializer blocks is executed before the secondary constructor body.

5-**Can an Interface implement another Interface?**

- Yes, an interface can implement another interface (and more than one), but it needs to use `extends`, rather than `implements` keyword. And while you can not remove methods from parent interface, you can add new ones freely to your sub-interface.

6-**What are the design patterns?**

a software design pattern is a general, reusable solution to a commonly occurring problem within a given context in software design.

- Creational patterns
    - Builder [Wikipedia](https://en.wikipedia.org/wiki/Builder_pattern?oldformat=true)
    - Factory [Wikipedia](https://en.wikipedia.org/wiki/Factory_method_pattern?oldformat=true)
    - Singleton [Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)
    - Monostate [Wikipedia](http://wiki.c2.com/?MonostatePattern)
    - Fluent Interface Pattern [Wikipedia](https://martinfowler.com/bliki/FluentInterface.html)
- Structural patterns
    - Adapter [Wikipedia](https://en.wikipedia.org/wiki/Adapter_pattern?oldformat=true)
    - Decorator [Wikipedia](https://en.wikipedia.org/wiki/Decorator_pattern?oldformat=true)
    - Facade [Wikipedia](https://en.wikipedia.org/wiki/Facade_pattern?oldformat=true)
- Behavioural patterns
    - Chain of responsibility [Wikipedia](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern?oldformat=true)
    - Iterator [Wikipedia](https://en.wikipedia.org/wiki/Iterator_pattern?oldformat=true)
    - Strategy [Wikipedia](https://en.wikipedia.org/wiki/Strategy_pattern?oldformat=true)
