***Create a repository called ActorRepository and add the following methods:***
```
public interface ActorRepository extends CrudRepository<Actor,Long> {
    Iterable <Actor> findAllByRealnameContainingIgnoreCase(String s);
    Iterable <Actor> findAllByMoviesNotContaining(Movie thisMovie);
}
```

*** Create a repository called MovieRepository and add the following methods: ***
```
public interface MovieRepository extends CrudRepository<Movie,Long> {
    Iterable <Movie> findAllByCastIsIn(Iterable<Actor> actors);
}
```
