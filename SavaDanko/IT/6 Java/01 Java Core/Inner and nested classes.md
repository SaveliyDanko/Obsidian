#java 

---
###### ==Nested Classes==
A _nested class_ is any class whose declaration occurs within the body of another class or interface declaration. A nested class may be a member class, a local class, or an anonymous class.

Some kinds of nested class are an _inner class_ , which is a class that can refer to enclosing class instances, local variables, and type variables.

The `static` modifier specifies that a nested class is not an inner class. Just as a `static` method of a class has no current instance of the class in its body, a `static` nested class has no immediately enclosing instance in its body.

References from a `static` nested class to type parameters, instance variables, local variables, formal parameters, exception parameters, or instance methods of lexically enclosing class, interface, or method declarations are disallowed.

he `static` modifier does not pertain to all nested classes. It pertains only to member classes, whose declarations may use the `static` modifier, and not to local classes or anonymous classes, whose declarations may not use the `static` modifier. However, some local classes are implicitly `static`, namely local enum classes and local record classes, because all nested enum classes and nested record classes are implicitly `static`.

###### ==Inner Classes==
An _inner class_ is a nested class that is not explicitly or implicitly `static`.
