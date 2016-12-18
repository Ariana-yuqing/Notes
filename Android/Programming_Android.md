# Programming Android
@(Android)

## Java for Android
> Effective Java by
Joshua Bloch (Prentice Hall)
### Java Type System
#### Objects
- **hashCode**_ and _**equals**_ should be considered a pair: if you override either, you should
override both. Many library routines treat _**hashCode**_ as an optimized rough guess as to
whether two objects are equal or not. These libraries first compare the hash codes of
the two objects. If the two codes are different, they assume there is no need to do any
more expensive comparisons because the objects are definitely different.

#### Static Declarations
##### Static class
![Alt text](./1463086822863.png)

#### Abstract
- Subtypes of an abstract class either must provide definitions for all the abstract methods in the superclass or must, themselves, be declared abstract.
- As hinted in the example, abstract classes are useful in implementing the common
template pattern, which provides a reusable piece of code that allows customization at
specific points during its execution. The reusable pieces are implemented as an abstract
class. Subtypes customize the template by implementing the abstract methods.

#### Interfaces
- Interfaces provide a way to define a type without defining its implementation. You can think of interfaces as abstract classes with all abstract methods. There is no limit on the number of interfaces that a class may implement.

### Java Collections Framwork
#### Collection implementation types
- **HashSet**
A HashSet is a set that is implemented as a hash. add , remove , contains , and size all
execute in constant time, assuming a well-behaved hash. A HashSet may contain
(no more than one) null .
- **HashMap**
A HashMap is an implementation of the Map interface that uses a hash table as its
index. add , remove , contains , and size all execute in constant time, assuming a well-
behaved hash. It may contain a (single) null key, but any number of values may
be null .
- **TreeMap**
A TreeMap is an ordered Map : objects in the map are sorted according to their natural
order if they implement the Comparable interface, or according to a Comparator
passed to the TreeMap constructor if they do not.

### Scope
#### Java Packages
- A typical package layout for an Android application might have a package for persistence, a
package for the UI, and a package for application logic or controller code.
- To declare a class as part of a package, use the package keyword at the top of the file
containing your class definition:
      - package your.qualifieddomainname.functionalgrouping

### Idioms of Java Programming
#### Synchronization and Thread Safety
![Alt text](./1463166063548.png)

### The Ingredients of an Android Application
#### Android Components
##### Service
The Android Service class is for background tasks that may be active but not visible
on the screen.
##### Content Providers
The ContentProvider class provides access to a data store for multiple applications. By providing a ContentProvider , your application can share data with other applications and manage the data model of an application. A companion class, ContentResolver , enables other components in an Android system to find content providers.

Instead of just enabling interprocess method calls, content providers allow developers to efficiently share entire SQL databases across processes: instead of sharing just objects, content providers manage entire SQL tables.

##### Broadcast Receiver 
Broadcast Receiver allows multiple parties to listen for intents broadcast by applications.
 Not signed in
