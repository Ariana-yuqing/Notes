# Learning Spark

## Creating RDDs
- loading an external dataset

   `val lines = sc.textFile("/path/to/README.md")`

- parallelizing a collection in your driver program (easier for prototyping and testing)

   `val lines = sc.parallelize(List("pandas", "i like pandas"))`

## RDD Operations

### Transformations

> Transformations are operations on RDDs that **return a new RDD**, such as map() and filter().

 Transformed RDDs are computed lazily, only when you use them in an action.

### Actions

> Actions are operations that return **a result** to the driver program or write it to storage, and kick off a computation, such as count() and first().

- count(): return the count as a number

- take(): collect a number of ele‐ ments from the RDD
   ```scala
   println("Input had " + badLinesRDD.count() + " concerning lines")
   println("Here are 10 examples:")
   badLinesRDD.take(10).foreach(println)
   ```

- collect(): retrieve the entire RDD 
   
   your entire dataset must fit in memory on a single machine to use collect() on it, so collect() **shouldn’t** be used on large datasets.

### Lazy Evaluation

> Spark will not begin to execute until it sees an action.

   Although transformations are lazy, you can force Spark to execute them at any time by running an action, such as count(). This is an easy way to test out just part of your program. 

### Passing Functions to Spark

#### Scala

```scala
class SearchFunctions(val query: String) { 
		def isMatch(s: String): Boolean = {
	    	s.contains(query)
		}

	def getMatchesFunctionReference(rdd: RDD[String]): RDD[String] = {
		// Problem: "isMatch" means "this.isMatch", so we pass all of "this" 
		rdd.map(isMatch)
	}
	
	def getMatchesFieldReference(rdd: RDD[String]): RDD[String] = {
		// Problem: "query" means "this.query", so we pass all of "this"
		rdd.map(x => x.split(query)) 
	}

	def getMatchesNoReference(rdd: RDD[String]): RDD[String] = { 
		// Safe: extract just the field we need into a local variable 
		// to avoid needing to pass the whole object
		val query_ = this.query
		rdd.map(x => x.split(query_))
	} 
}
```
   If `NotSerializableException` occurs in Scala, a reference to a method or field in a nonserializable class is usually the problem. Note that passing in local serializable variables or functions that are members of a top-level object is always safe.

## Common Transformations and Actions

### Basic RDDs

#### Element-wise transformations
- map()

- filter()

-  flatMap(): the function we provide to flatMap() is called individually for each element in our input RDD. Instead of returning a single element, we return **an iterator** with our return values. Rather than producing an RDD of iterators, we get back an RDD that consists of the elements from all of the iterators.

   ```scala
   val lines = sc.parallelize(List("hello world", "hi")) 
   val words = lines.flatMap(line => line.split(" ")) 
   words.first() // returns "hello"
   // flatMap() => words: {"hello", "world", "hi"}
   // map() => words: {["hello", "world"], ["hi"]}
   ```

#### Pseudo set operations

- distinct()

- union(), if there are duplicates in the input RDDs, the result of Spark’s union() will contain duplicates (which we can fix if desired with distinct()).

- intersection(), also removes all duplicates (including duplicates from a single RDD) while running. While intersection() and union() are two sim‐ ilar concepts, the performance of intersection() is much worse since it requires a shuffle over the network to identify common elements.

- subtract(other) takes in another RDD and returns an RDD that has only values present in the first RDD and not the second RDD. (it performs a shuffle.)

- cartesian(other) transformation returns all possible pairs of (a, b) where a is in the source RDD and b is in the other RDD. We can also take the Carte‐ sian product of an RDD with itself, which can be useful for tasks like user **similarity**. Be warned, however, that the Cartesian product is very expensive for large RDDs.

#### Actions

- reduce(), which takes a function that operates on two elements of the type in your RDD and returns a new element of **the same type**. (This criteria can be met by using map() first.) 

  ```scala
  val sum = rdd.reduce((x, y) => x + y)
  ```

- fold(), requires that the return type of our result be the same type as that of the elements in the RDD we are operating over.

- aggregate(), like fold(), we supply an initial zero value of the type we want to return. We then supply a function to combine the elements from our RDD with the accumulator. Finally, we need to supply a second function to merge two accumulators, given that each node accumulates its own results locally.

  ```scala
  val result = input.aggregate((0, 0))(
  				(acc, value) => (acc._1 + value, acc._2 + 1),
  				(acc1, acc2) => (acc1._1 + acc2._1, acc1._2 + acc2._2)) 
  val avg = result._1 / result._2.toDouble
  ```

- collect(), all of your data must fit on a single machine

- take(n), returns n elements from the RDD and attempts to minimize the number of partitions it accesses, so it may represent a biased collection.

- top(), will use the default ordering on the data, but we can sup‐ ply our own comparison function to extract the top elements.

- takeSample(withReplacement, num, seed), allows us to take a sample of our data either with or without replacement.

- foreach(), lets us perform computations on each element in the RDD without bringing it back locally.

- count(), returns a count of the elements, and countByValue() returns a map of each unique value to its count. 



















