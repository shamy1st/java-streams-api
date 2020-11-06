# Streams API
**Streams API** is the process collection of data in a declarative way (functional way) like SQL queries.

        movies.stream()
            .filter(movie -> movie.getLikes() > 100)
            .count();
