#java 

---
```java
public interface Iterable<T> {
    Iterator<T> iterator();

    default void forEach(Consumer<? super T> action){
	    Objects.requireNonNull(action);  
		// за счёт специального механизма компилятора: 
		// `for-each` цикл на самом деле разворачивается в использование `Iterator`.
		for (T t : this) {  
		    action.accept(t);  
		}
    }
}
```
