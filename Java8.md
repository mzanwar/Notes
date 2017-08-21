##Java 8

###Lamdas:



FileFilter is an interface with one function, accept. We can do this in two ways:

1. New Class which implements interface

```Java
public class JavaFileFilter implements FileFilter{

  public boolean accept(File file) {
    return file.getName().endsWith(".java");
  }
}
```
2. Anonymous Class

```Java
FileFilter fileFilter = new FileFilter() {
            @Override
            public boolean accept(File file) {
                return file.getName().endsWith(".java");
            }
        };
        File dir = new File("/Users/zeshan.anwar/learning/FileFilterTest");

        File[] javaFiles = dir.listFiles(fileFilter);
```



The new way with Lamdas is:

3. `FileFilter filter = (File file) -> file.getName().endsWith(".java");`

Several other examples:

If more than one line of code:
```Java
Runnable r = () -> {
  for ...
  .. more code
}
```
Even multiple parameters:
```Java
Comparator<String> c = (String s1, String s2) -> Integer.compare(s1.length(), s2.length());
```

###1. What is a Lambda expression? => Functional interface;

an interface with only `one` abstract method (until Java 7 you couldn't put anything other than abstract methods in an interface)
Some examples:
```Java
public interface Runnable() {

  run();
};
```
```Java
public interface Comparator<T> {

  int compare(T t1, T t2);
};
```
```Java
public interface FileFilter {

  boolean accept(File pathname);
};
```
All objects in Java extend the Object class; thus they don't count as only one.
You can define functional interface like such @FunctionalInterface
This way, the compiler will check to see if it really is a functional interface (contains one abstract method only), and return an error if not.

###2. Can a lambda be put in a variable? => YES!
Example:
```Java
Comparator<String> c = (String s1, String s2) -> Integer.compare(s1.length(), s2.length());
```
Can be used everywhere a variable can; passed as a parameter, passed around etc.

###3. Is a Lambda an Object? No, but an object without an identity.
Anonymous class uses `new`, thus that is an object. Not free; lots of overhead!
This overhead does not exist when using a Lambda expression since there is no new. Performance is much, much better. DO NOT CALL OBJECT METHODS ON A LAMDA. Think of Lambdas as piece of code.

### Functional Interfaces Toolbox (new package in Java 8) 43 total interfaces
####4 categories
- Supplier; single interface provides new object:
```Java
@FunctionalInterface
public interface Supplier<T> {
  T get();
}
```
- Consumer / Biconsumer
```Java
@FunctionalInterface
public interface Consumer<T> {
  T accept(T t);
}

@FunctionalInterface
public interface BiConsumer<T, U> {
  T accept(T t, U u);
}
```
- Predicate / BiPredicate
```Java
@FunctionalInterface
public interface Predicate<T> {
  T test(T t);
}

@FunctionalInterface
public interface BiPredicate<T, U> {
  T test(T t, U u);
}
```
- Function / BiFunction - takes a function, and return a new function
```Java
@FunctionalInterface
public interface Function<T, R> {
  R apply(T t);
}

@FunctionalInterface
public interface Function<T, U, R> {
  R apply(T t, U u);
}
```

#### More Lamda Syntax
You can omit types; ie
```Java
Comparator<String> c = (String s1, String s2) -> Integer.compare(s1.length(), s2.length());
```
===>
```Java
Comparator<String> c = (s1, s2) -> Integer.compare(s1.length(), s2.length());
```
Java 8 will infer those types from the abstract method in the interface.


#### Method Reference
Consumer<String> c = s -> System.out.println(s);
Consumer<String> c = System.out::println;

Comparator<Integer> c = (i1, i2) -> Integer.compare(i1, i2);
Comparator<Integer> c = (i1, i2) -> Integer::compare;


####How can we use all these tools to process data?

Where are our objects most of the time? => Collection API (List, Set, Map)

Can I process these data structures with lamdas? Yes :)

```Java
// Normal Lambda
List<Customer> list = ...?
list.forEach(customer -> System.out.println(customer));

//Method Reference Lambda
List<Customer> list = ...?
list.forEach(customer -> System.out::println);
```

You can add code into the interface! This is revolutionary in Java; this gave rise to new patterns. We can also add static methods in interfaces.
