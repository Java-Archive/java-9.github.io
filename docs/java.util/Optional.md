# New Methods inside the class Optional

### public Stream<T> stream()

In Java8, if a method wrapped a result into an Optional, you had to make sure to test with ```isPresent``` 
if a value was wrapped. After this you could map it to the value itself. The new Method ```stream``` will 
create a Stream with one value if the value is present. If no value is present it will create an emtpy Stream.

With this you could combine the two steps ( ```filter``` and ```map``` ) to  one ```flatMap```

```java
    final Function<Integer, Optional<Integer>> function
        = (value) -> (value <= 4) ? Optional.of(value) : Optional.empty();

    final List<Integer> collectionJava8 = Stream
        .of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
        .map(function) // only to wrap
        .filter(Optional::isPresent)
        .map(Optional::get)
        .collect(Collectors.toList());

    final List<Integer> collectionJava9 = Stream
        .of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
        .map(function) // only to wrap
        .flatMap(Optional::stream)
        .collect(Collectors.toList());

    System.out.println("collectionJava8 = " + collectionJava8);
    System.out.println("collectionJava9 = " + collectionJava9);

```

### public Optional<T> or(Supplier<? extends Optional<? extends T>> supplier)
In Java8  

### public void ifPresentOrElse(Consumer<? super T> action, Runnable emptyAction)
