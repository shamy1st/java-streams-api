# Streams API
**Streams API** process collection of data in a declarative way (functional way) like SQL queries.

        movies.stream()
            .filter(movie -> movie.getLikes() > 100)
            .count();

### Create

1. **from collections**

        ArrayList<Integer> list = new ArrayList<>();
        list.stream()

2. **from array**

        int[] numbers = {1, 2, 3};
        Arrays.stream(numbers)

3. **from arbitrary number of objects**

        Stream.of(1, 2, 3)

4. **infinite streams**

        Stream stream = Stream.generate(() -> Math.random());
        stream.limit(5)
                .forEach(n -> System.out.println(n));

5. **finite streams**

        Stream.iterate(1, n -> n+1)
            .limit(5)
            .forEach(n -> System.out.println(n));

### Mapping

* **map()**

        movies.stream()
            //here we have stream of movies names
            .map(movie -> movie.getName())
            .forEach(name -> System.out.println(name));

* **flatMap()**

        Stream<List> stream = Stream.of(List.of(1,2,3), List.of(4,5,6));
        //merge two lists together
        stream.flatMap(list -> list.stream())
            .forEach(n -> System.out.println(n));

### Filtering

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .forEach(movie -> System.out.println(movie.getName()));

### Slicing
useful in pagination

* **limit(n)**

        movies.stream()
            .limit(pageSize)
            .forEach(movie -> System.out.println(movie.getName()));

* **skip(n)**

        movies.stream()
            .skip((currentPage-1) * pageSize)
            .limit(pageSize)
            .forEach(movie -> System.out.println(movie.getName()));

* **takeWhile(predicate)**
example: 15 20 35 10 50 70 100
output: 15 20

        movies.stream()
            .takeWhile(movie -> movie.getLikes() < 30)
            .forEach(movie -> System.out.println(movie.getName()));

* **dropWhile(predicate)**
example: 15 20 35 10 50 70 100
output: 35 10 50 70 100

        movies.stream()
            .dropWhile(movie -> movie.getLikes() < 30)
            .forEach(movie -> System.out.println(movie.getName()));

### Sorting
you should implement Comparable interface with compareTo() method.

        movies.stream()
            .sorted(Comparator.comparing(movie -> movie.getName()))
            //.sorted(Comparator.comparing(movie -> movie.getName()).reversed())
            .forEach(movie -> System.out.println(movie.getName()));

### Unique
you should override equals & hashcode functions.

        movies.stream()
            .distinct()
            .forEach(movie -> System.out.println(movie.getName()));

### Peeking
print inside

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .peek(movie -> System.out.println("filter: " + movie.getName()))
            .forEach(movie -> System.out.println(movie.getName()));

### Reducers

* **count()**

* **anyMatch(predicate)** true/false - if any element match the condition return true.

* **allMatch(predicate)** true/false - if all elements match the condition return true.

* **noneMatch(predicate)** true/false - if none elements match return true.

* **findFirst()** return the first element in Optional<>

* **findAny()** return any element in the stream.

* **max(comparator)**

* **min(comparator)**

* **reduce(BinaryOperator)**

        movies.stream()
            .map(movie -> movie.getLikes())
            .reduce((a,b) -> a+b)// return Optional<Integer> sum
            .get();

### Collectors

* **collect to List**

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .collect(Collectors.toList());

* **collect to Set**

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .collect(Collectors.toSet());

* **collect to Map**

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .collect(Collectors.toMap(Movie::getName, Movie::getLikes));

* **sum of movies likes in Integer**

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .collect(Collectors.summingInt(Movie::getLikes));

* **sum of movies likes in Double**

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .collect(Collectors.summingDouble(Movie::getLikes));

* **statistics on movies likes (count, sum, min, max, average)**

        movies.stream()
            .filter(movie -> movie.getLikes() > 10)
            .collect(Collectors.summarizingInt(Movie::getLikes)); //summarizingDouble, summarizingLong

* **join movies names in one string separated by comma**

        movies.stream()
            .map(Movie::getName)
            .collect(Collectors.joining(","));

### Grouping

* **Map{Genre, List\<Movie>}**

        movies.stream()
            .collect(Collectors.groupingBy(Movie::getGenre));

* **Map{Genre, Set\<Movie>}**

        movies.stream()
            .collect(Collectors.groupingBy(Movie::getGenre), Collectors.toSet());

* **Map{Genre, Count}**

        movies.stream()
            .collect(Collectors.groupingBy(Movie::getGenre), Collectors.counting());

* **Map{Genre, String}**

        movies.stream()
            .collect(Collectors.groupingBy(Movie::getGenre)
                        , Collectors.mapping(Movie::getName, Collectors.joining(",")));

### Partioning

* **Map with two keys (true, false)**
  * false, List<Movie>
  * true, List<Movie>

        movies.stream()
            .collect(Collectors.partitioningBy(movie -> movie.getLikes()>20));

### Primitive type streams


