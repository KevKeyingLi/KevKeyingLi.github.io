## Intro
* Introduced in Java 8
* can be used to replace anonymous inner classes - used a lot in UI event handling. 

## Java 8
### Functional interfaces overview
Java 8 added two new packages:
* `java.util.function`
* `java.util.stream`

What is a functional interface?
* It is defined as an interface that contains only one abstract function or method. 
* Functional interfaces can represent abstract concepts such as functions, actions or predicates.
* To see a list of all the functional interfaces available, check out the Javadoc for java.util.function. 

#### Commonly used  interfaces
* `Predicate`. Predicates are Boolean valued functions of one argument
    - take in one argument, use a `test` method to evaluate it and return either true or false. Since this is an interface, we will have to override the `test` method with logic that determines what should be evaluated.
* `Consumer`: The Consumer interface consumes the argument. It `accept`s a single argument and does not return a result. 
* `Function` which transforms a value from one type to another. It accepts one argument and produces a result. `apply`
    - `IntFunction`...
* `Supplier` supplies a value. It produces a result of a given type. `get`
    - Suppliers do not accept arguments but they do return a result. `apply`
* `UnaryOperator` interface takes a single argument and returns a single value 
* `BinaryOperator` interface takes two arguments and returns one. `apply`

#### Examples
```
/*
 * Sample program to introduce functional interfaces with lambda notation
 */
package lambdas_01_01;
import java.util.function.*;
/**
 *
 * @author MFisher
 */
public class Lambdas_01_01 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        //using the test method of Predicate
        Predicate<String> stringLen  = (s)-> s.length() < 10;
        System.out.println(stringLen.test("Apples") + " - Apples is less than 10");

        //Consumer example uses accept method
         Consumer<String> consumerStr = (s) -> System.out.println(s.toLowerCase());
         consumerStr.accept("ABCDefghijklmnopQRSTuvWxyZ");
         
        //Function example        
        Function<Integer,String> converter = (num)-> Integer.toString(num);
        System.out.println("length of 26: " + converter.apply(26).length());

        //Supplier example
        Supplier<String> s  = ()-> "Java is fun";
        System.out.println(s.get());
        
        //Binary Operator example
        BinaryOperator<Integer> add = (a, b) -> a + b;
        System.out.println("add 10 + 25: " + add.apply(10, 25));
        
        //Unary Operator example
        UnaryOperator<String> str  = (msg)-> msg.toUpperCase();
        System.out.println(str.apply("This is my message in upper case"));
    }
    
}
```

When using lambda notation, data types of arguments are inferred. So since the BinaryOperator is returning an integer, it knows that the two values coming in as arguments, a and b, must also be integers.

### Lambda syntax


Lambda expressions let you express instances of single-method classes a lot more concisely.

#### Example 1: action handler
Instead of 
```
btn.setOnAction(new EventHandler<ActionEvent>() {
    @Override
    public void handle(ActionEvent event) {
        System.out.println("Hello World");
    }
})
```
we just need:
```
btn.setOnAction( event -> System.out.println("Hello World"));
//Consumer interface
```
#### Example 2: runnable in multi-thread
If you've ever written programs that involve threads, you're familiar with the concept of a Runnable interface. If you want to learn more about threads, check out my series on managing threads in Java.

```
// Anonymous Inner Class: Runnable
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("run 1");
    }
};

// Lambda version of Runnable (no arguments)
Runnable r2 = () -> System.out.println("run 2");

// Start both threads
r1.run();
r2.run();
```

The Runnable interface does not take any arguments, and we can use lambda notation to help us write the inner class needed to implement this interface. 

#### Example 3: Initializing functional interface
* `BiFunction<T, U, R>`
* `Consumer<>`
* Custom functional interface

```
        //using an existing functional interface BiFunction         
        BiFunction<String, String, String> concat = (a, b) -> a + b;
        String sentence = concat.apply("Today is ", "a great day");
        System.out.println(sentence);
        
        //example of the Consumer functional interface
        Consumer<String> hello = name -> System.out.println("Hello, " + name);
        for (String name : Arrays.asList("Duke", "Mickey", "Minnie")) {
            hello.accept(name);
        }
        
        //example of passing one value 
         GreetingFunction greeting = message ->
            System.out.println("Java Programming " + message);
    }
    //custom functional interface
    @FunctionalInterface
    interface GreetingFunction {
      void sayMessage(String message);
   }
```
So you have your argument, your arrow, and on the right-hand side, the body.

### Methods as lambdas
 Another feature of Java 8 is we can now take any type of method and convert it into a lambda including static method, instance methods, and even constructors. 
 
 integer::ToString. This is the structure that creates a lambda from a method. It's called a **method reference** and it enables us to pass references of methods or constructors via the colon colon syntax.
 

#### Examples
* IntFunction<> with regular lambda
* intFunction<> using method reference of a static method
* Function<,> using method reference of a constructor
* Comsumer using reference of an instance method

```
import java.math.BigInteger;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.IntFunction;
import java.util.function.UnaryOperator;
...
        IntFunction<String> intToString = num -> Integer.toString(num);
        System.out.println("expected value 3, actual value: " + 
                intToString.apply(123).length());
     
        //static method reference using ::
        IntFunction<String> intToString2 = Integer::toString;
        System.out.println("expected value 4, actual value:  " + 
                intToString2.apply(4567).length());
        
        //lambdas made using a constructor
        Function<String,BigInteger> newBigInt = BigInteger::new;
        System.out.println("expected value: 123456789, actual value: "+ 
                newBigInt.apply("123456789"));
        
        //example of a lambda made from an instance method
        Consumer<String> print = System.out::println;
        print.accept("Coming to you directly from a lambda...");
        
        //these two are the same using the static method concat
        UnaryOperator<String> greeting = x -> "Hello, ".concat(x);
        System.out.println(greeting.apply("World"));
        
        UnaryOperator<String> makeGreeting = "Hello, "::concat;
        System.out.println(makeGreeting.apply("Peggy"));
```

Unspecified data types are inferred by compiler. 

### Create new functional interfaces
We can create a new functional interface by
* creating a new file
* or we can include the functional interface inside of our class file.
Either way, it's helpful to add annotation that says `@FunctionalInterface` to help ensure this is a functional interface. It ensures the functional interface meets the criteria of single method. 

```
@FunctionalInterface
public interface Calculate {
    int calc(int x, int y); 

}

public class Lambdas_01_04 {
    public static void main(String[] args) {
        //example of passing multiple values to a method using lambda 
        //notice that I do NOT have to specify the data type of a and b
        Calculate add =(a,b)-> a + b;
        Calculate difference = (a,b) -> Math.abs(a-b);
        Calculate divide =(a,b)-> (b != 0 ? a/b : 0);

        System.out.println(add.calc(3,2));
        System.out.println(difference.calc(5,10));
        System.out.println(divide.calc(5, 0));
    } 
}
```

## Collections, Maps, and Streams
### Collections
#### Quick review
* The Collections API was introduced with Java 7.
* A collection is an object that groups multiple elements into a single unit. * Collections are used to store, retrieve, manipulate, and communicate aggregate data.
* The collections API provides the following interfaces
    - set: a collection that does not contain duplicates
    - list, an ordered collection based on the way the user entered the data
    - map is an object that maps keys to values.
* The collection interface contains methods that perform basic operations such as
    - `int size` gets the size of the collection
    - `boolean isEmpty` returns true if it's empty, false if it's not.
    - `boolean contains` checks to see if an element is inside the collection, returning true if it is and false if not
    - `boolean add(E element)` returns true if it was able to add the element, or false if there was an error
    - `boolean remove(Object element)`, which tries to remove an element. If the element is not found, it returns false. If it successfully removes it, it'll return true.
    - `Iterator<E> iterator()` returns an iterator over the elements in this collection.

Remember we don't have to specify the data types in the lambda notation because it can be inferred since there is only one method inside the Collections interface.

#### A few examples on collection and stream
```
        List<String> names = Arrays.asList("Paul", "Jane", "Michaela", "Sam");
        //way to sort prior to Java 8 lambdas
        Collections.sort(names, new Comparator<String>() {
            @Override
            public int compare(String a, String b) {
                return b.compareTo(a);
            }
        });
        //first iteration with lambda
        Collections.sort(names, (String a, String b) -> {
            return b.compareTo(a);
        });
        //now remove the return statement
        Collections.sort(names, (String a, String b) -> b.compareTo(a));
        
        //now remove the data types and allow the compile to infer the type
        Collections.sort(names, (a, b) -> b.compareTo(a));

   
        //total pages in your book collection
        Book book1 = new Book("Miss Peregrine's Home for Peculiar Children",
                "Ranson", "Riggs", 382);
        Book book2 = new Book("Harry Potter and The Sorcerers Stone",
                "JK", "Rowling", 411);
        Book book3 = new Book("The Cat in the Hat",
                "Dr", "Seuss", 45);
        
        List<Book> books = Arrays.asList(book1, book2, book3);
        int total = books.stream()
                .collect(Collectors.summingInt(Book::getPages));
        System.out.println(total);
        
        //create a list with duplicates
        List<Book> dupBooks = Arrays.asList(book1, book2, book3, book1, book2);
        System.out.println("Before removing duplicates: ");
        System.out.println(dupBooks.toString());
        
        Collection<Book> noDups = new HashSet<>(dupBooks);
        System.out.println("After removing duplicates: ");
        System.out.println(noDups.toString());


        //aggregate author first names into a list
        List<String> list = books.stream()
                .map(Book::getAuthorLName)
                .collect(Collectors.toList());
        System.out.println(list);
        
        //example of using Set to eliminate dups and sort automatically
        Set<Integer> numbers = new HashSet<>(asList(4, 3, 3, 3, 2, 1, 1, 1));
        System.out.println(numbers.toString());
```

In JDK 8 and later, the preferred method of iterating over a collection is to obtain a stream and perform aggregate operations on that. Aggregate operations are often used in conjunction with lambda operations to make programming more expressive and using less lines of code. For more information on collections, check out the Oracle tutorial here at https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html

### Streams
The new stream package:java.util.stream package
* contains the majority of the interfaces and classes for the stream functionality.
* not related at all to the Java IO streams.
* A stream in this case represents a sequence of elements.
* The stream package was added in Java 8 to help traverse collections.
* Most stream operations accept some kind of lambda expression parameter: a functional interface specifying the exact behavior of the operation.
* Stream operations are categorized as either intermediate or terminal. 
    - Terminal operations are either void or return a result of a certain type. 
    - intermediate operations return the stream itself. Intermediate operations are useful to allow us to chain multiple method calls in a row on a single stream.
* Some of the commonly used operations include
    - map: intermediate, map one value to another
    - filter: intermediate, filter the results using a Predicate
    - forEach: terminal.
    - sorted: intermediate, returns a sorted view of the stream but the original collection is not being changed
    - collect an extremely useful terminal operation to transform the elements of a stream into a different kind of result
* Elements in a collection cannot be changed or mutated with streams but you can save them to a new collection. 

#### Examples

```
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.function.BinaryOperator;
import java.util.stream.Collectors;
import java.util.stream.Stream;
//static import
import static java.util.Arrays.asList;
import static java.util.stream.Collectors.toList;

		Arrays.asList("red", "green", "blue")
                .stream()
                .sorted()
                .findFirst()
                .ifPresent(System.out::println);
        
        //example of Stream.of with a filter 
        Stream.of("apple", "pear", "banana", "cherry", "apricot")
                .filter(fruit -> {
                  //  System.out.println("filter: " + fruit);
                    return fruit.startsWith("a"); //predicate
                })
                //if the foreach is removed, nothing will print,
                //the foreach makes it a terminal event
                .forEach(fruit -> System.out.println("Starts with A: " + fruit));

        //using a stream and map operation to create a list of words in caps
        List<String> collected = Stream.of("Java", " Rocks")
                .map(string -> string.toUpperCase())
                .collect(toList());
        System.out.println(collected.toString());
```

Notable points in this example:
* collection.asList()
* Stream.of()
* Not like JavaScript. **The forEach makes it a terminal operation so the code actually invokes the filter and then the forEach. Otherwise, it will skip over the filter operation.**
* Not like JavaScript. the way that `filter` and `forEach` works is that, it executes `filter` and `forEach` on each element in same loop, instead of doing the `filter` and then iterate to run `forEach` again. So it's important to notice how each value goes through only one time. It's not going to search through the entire list looking for fruit that start with a and then go through and print them out. It's actually going to go through one, find the ones with a and pass them on to the forEach.


### Primitive streams
Special streams for some of the primitive data types **int, long, and double** They are intStream, longStream, and doubleStream.

Primitive streams use specialized lambda expressions as well. e.g. intFunction, intPredicate


Primitive streams support the additional terminal operations of `sum` and `average`. 

#### Examples:
```
        IntStream.range(1, 4)
                .forEach(System.out::println);

        //find the average of the numbers squared
        Arrays.stream(new int[]{1, 2, 3, 4})
                .map(n -> n * n)
                .average()
                .ifPresent(System.out::println);

        //map doubles to ints
        Stream.of(1.5, 2.3, 3.7)
                .mapToInt(Double::intValue)
                .forEach(System.out::println);
```

* `IntStream.range()`
* `.average()` `.ifPresent(Function)` 
* `Stream.of()` `.mapToInt()`. I can take a double and convert it to an int. A double cast it as an int, it truncates the decimal portion.
