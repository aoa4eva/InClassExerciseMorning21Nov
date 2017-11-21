Create a model for actors:

***Create a class called Actor:***
```
package me.afua.demo.models;

import javax.persistence.*;
import java.util.HashSet;
import java.util.Set;

@Entity
public class Actor {

    @Id
    @GeneratedValue(strategy= GenerationType.AUTO)
    private long id;
    private String name;
    private String realname;
    private String headshot;


    @ManyToMany(mappedBy="cast")
    private Set<Movie> movies;


    public Actor()
    {
        //Why is this needed?
        movies = new HashSet<Movie>();
    }

    public void addMovie(Movie m)
    {
        //Why is this needed?
        movies.add(m);
    }
}
```
****Don't forget to add getters and setters!****

***Create a model for movies:***

Create a class called Movie:

```
package me.afua.demo.models;

import javax.persistence.*;
import java.util.HashSet;
import java.util.Set;

@Entity
public class Movie {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    private String title;
    private long year;
    private String description;

    public Movie() {
        this.cast = new HashSet<Actor>();
    }

    @ManyToMany()
    private Set<Actor> cast;

    public void addActor(Actor a)
    {
        this.cast.add(a);
    }
}
```

Don't forget to add getters and setters!
