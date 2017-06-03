- Scala interactive
  `:help` for all the commands available for Scala terminal

- Data and Control Flow
    - `var:` mutable  `val:` immutable
> why immutable?
> - avoid unexpected reuse
> - threads safety (different threads may try to change the same objects at the same time)
> - performance (immutable variables can be embedded into the binary code, instead of fetching from memory every time)

    - statements vs. expressions
        - `import util.Random._ import` all the contents for the object `Random` (a companion object) , thus we can use `nextBoolean` directly. If we import as `import util.Random` , then we have to call Random.nextBoolean .
        - if a method has no params, e.g., `str.length()` , in Scala, we can leave the brackets.
        - `Predef` is automatically imported to convert objects when necessary, e.g., `str.toInt` convert a String
 to a `StringOps` (no `toInt` method for Java String)

    - Type Inference
        - `==` is for value equality, `eq` is for reference equality

    - Methods
        + explicit return type is optional except recursion
        + explicit params type is mandatory.
        + there is not static in Scala, so the fastest way to create a static class or method is using object
        + tail recursion:
        + We can define a function inside of another, but the inside function will not be testable

        ```Scala
        object Factorial {
          @tailrec
          def factorial(n: Int): Int = {
            if (n <= 1) 1
            else n * factorial(n-1)
          }
        }
        ====> StackOverFlow ===> except for recursion, we did something else with the result, violate the tail recursion principle
        ```
        
        ```
        object Factorial {
          @tailrec
          def factorial(n: Int, acc: Int): Int = {
            if (n <= 1) acc
            else factorial(n-1, n * acc)
          }
        }
        ```
        
        
    - Sequence/ collection
        + Array
            * The size of array is fixed, but the elements are mutable `arr2 = arr1 :+ "e"` , `arr3 = "f" +: arr2`
        + Vector
        + List
            * `list =  list.head  + list.tail`
            * append: `newList = "newEle" :: list`   `val list = 1 :: 2 :: List[Int]()`

    - Set
        + Tuple: 1-based index `tuple._1`

     - Pattern Matching
          + Either has left and right value. Conventionally, left value is failure, right value is success
          + Twitter.util

- Object-Oriented Programming
     + Classes and Objects
        No need for getters and setters in functional language. Direct access to instance fields .
        ```
        class Recipe {
          var ingredients: List[String] = _ // Scala won't allow to leave field uninitialized. _ initializes the field with default
          var directions: List[String] = _
        }
        ```

        ```
        class Person {
             var name: String = ""
             var id: Long = 0
        }
        ===> val person = new Person
        ===> person.name = "Ken"
        ===> person.id = 7 >> actually invoke Java setter function  // ===> person.id_ = 7
        ```

        ```
        class Person {
             var name: String = ""
             private[this] var id_: Long = 0
        // more private than Java private
        }
        ```
        ```
        class Recipe private (val ingredients: List[String], val directions: List[String])
        // private ==> the constructor is private, only companion object can call the constructor
        // if it changed to private class Recipe , then the whole class will be private
          object Recipe {
            val pbj = new Recipe(
              ingredients = List("peanut butter", "jelly", "bread"),
              directions = List("put the peanut butter and jelly on the bread"))
            val baconPancakes = new Recipe(
              ingredients = List("bacon", "pancakes"),
              directions = List("take some bacon", "put it in a pancake"))

          def make(ingredients: List[String], directions: List[String]): Option[Recipe] =
            if (ingredients.isEmpty || directions.isEmpty)
              None
            else
              Some(new Recipe(ingredients, directions))
          }
          // companion object === static
        ```

    - Case class
          + Case class cannot be subclassed. Case classes are FINAL.
            ```
            > case class Person (name: String, id: Long = 0)
            > val p1 = Person(“Amy”)
            > p1 match {
                Case Person(n, i) => s”Name: $n, Id: $I"
              }
            > p1.toString
            > val p2 = p1.copy() // shadow copy
            > p2.hashCode
            ```

     - Sealed class:
          all the subclasses have to be defined in the same source file

     - Traits
          Traits can have implemented methods, but traits don't have any constructors
          ```          
          class Bar extends Trait1 with Trait2 {
            override def foo = super.foo
          }
          // right to left depth first search if both Trait1 and Trait2 have foo function
          ```
          ```
          class Bar extends Trait1 with Trait2 {
            override def foo = super[Trait1].foo
          }
          ```

> Both Map and Filter will yield a new vector to hold all the elements every time. `withFilter` is a solution. It will hold all the elements until the end of processing.

Coursera- functional scala programming
Scala for the impatient
Scala cookbook