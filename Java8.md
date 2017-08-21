##Java 8

Lamdas:



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

1. What is a Lambda expression? => Functional interface; an interface with only one `abstract` method (until Java 7 you couldn't put anything other than abstract methods in an interface)
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
All objects in Java extend the Object class

2.
