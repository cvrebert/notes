The accessor problem:

```
class Foo {
    private List<Int> bar;
    public List<Int> getBar() {
        /* This should be an error! */
        return bar;
    }
}
```
Why that should be an error:
```
Foo().getBar().append(2);
/* We've now unwittingly altered Foo's internal state */
```

It should be illegal, by default, to return a mutable member of an object.
