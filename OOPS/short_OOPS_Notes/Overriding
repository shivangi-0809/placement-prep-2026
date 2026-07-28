'What is Method Overriding?'
Method Overriding happens when a child class provides its own implementation of a method that already exists in the parent class.
The child method replaces the parents implementation.

-------- Example ----------
class Parent {
    void show() {
        System.out.println("Parent method");
    }
}

class Child extends Parent {
    @Override
    void show() {
        System.out.println("Child method");
    }
}
public class Main {
    public static void main(String[] args) {
        Child c = new Child();
        c.show();
    }
}
--------- output = Child method --------

'Compile Time vs Runtime'
.)Compilation
        Animal a = new Dog();
 Compiler only checks
 Does Animal have sound() ?
 Yes.
Compilation succeeds.

.)Runtime
 JVM asks
 Actual object?
 Dog
Execute Dogs version.

'This is called Dynamic Method Dispatch.'
Dynamic Method Dispatch is the mechanism through which a call to an overridden method is resolved at runtime instead of compile time.




'Rules of Overriding'
Rule 1  Method name must be same.
Rule 2  Parameters must be same.
Rule 3  Return type must be same (or covariant)
Rule 4  Cannot reduce access modifier.
Rule 5  Cannot override final methods.
Rule 6  Static methods cannot truly be overridden.
Rule 7  Private methods cannot be overridden.
Rule 8  Constructors cannot be overridden.
        Constructors are not inherited.
        Each class has its own constructor.
Rule 9  Cannot override with broader checked exceptions.




'The @Override Annotation'
                           @Override
                            void show() {
                            }

===============Benefits===============
Compiler checks that youre actually overriding.
Prevents spelling mistakes.
Makes code easier to read.


Can We Call Parent Method?

Yes.

Using

super.methodName();





==========Overriding vs Overloading=========
  Feature	          Overriding     	    Overloading
Class	             Parent and Child	  Same class (or inherited)
Method Name	          Same	               Same
Parameters	          Same	             Different
Return Type      	Same/Covariant	       Can differ (but not by itself)
Polymorphism	        Runtime            	Compile time
Inheritance          	Required	         Not required




================Interview Questions===================
1. Can constructors be overridden?
No. Constructors are not inherited.

2. Can static methods be overridden?
No. They are hidden, not overridden.

3. Can private methods be overridden?
No. They are not visible to subclasses.

4. Can final methods be overridden?
No.

5. Can abstract methods be overridden?
Yes. In fact, they must be implemented by the first concrete subclass.






