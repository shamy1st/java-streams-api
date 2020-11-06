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



### Sorting

### Unique

### Peeking

### Reducers

### Collectors

### Grouping

### Partioning

### Primitive type streams

