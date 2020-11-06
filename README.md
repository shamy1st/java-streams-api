# Streams API
**Streams API** process collection of data in a declarative way (functional way) like SQL queries.

        movies.stream()
            .filter(movie -> movie.getLikes() > 100)
            .count();

### create

**1. from collections**

        ArrayList<Integer> list = new ArrayList<>();
        list.stream()

**2. from array**

        int[] numbers = {1, 2, 3};
        Arrays.stream(numbers)

**3. from arbitrary number of objects**

        Stream.of(1, 2, 3)

**4. infinite streams**

        Stream stream = Stream.generate(() -> Math.random());
        stream.limit(5)
                .forEach(n -> System.out.println(n));

**5. finite streams**

        Stream.iterate(1, n -> n+1)
            .limit(5)
            .forEach(n -> System.out.println(n));

### mapping

### filtering

### slicing

### sorting

### unique

### peeking

### reducers

### collectors

### grouping

### partioning

### primitive type streams

