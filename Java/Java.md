# Java
## Menu
1. [Collections](#collections)
	* [List](#list)
	* [Iterators](#iterators)
	* [Set](#set)
	* [Queue](#queue)
	* [Map](#map)
* [Exceptions](#exceptions)
* [Concurrency](#concurrency)

## 1. <a name="collections"></a>Collections

![Collection and Collections](http://www.programcreek.com/wp-content/uploads/2009/02/CollectionVsCollections.jpeg)

![Class hierarchy of Collection](http://www.programcreek.com/wp-content/uploads/2009/02/java-collection-hierarchy.jpeg)

### <a name="list"></a>List
**List** is a collection in which order is significant, accommodating duplicate elements.

* ***ArrayList***
	* excels at ==randomly accessing elements==
	* slower when inserting and removing elements in the middle of a List.
* ***LinkedList***
	* provides optimal sequential access
	* inexpensive insertions and deletions from the middle of the List. 
	* A LinkedList is relatively slow for random access, but it has a larger feature set than the ArrayList.
	* 使用LinkedList的唯一理由就是减少在中间插入和删除的代价。
* **ArrayList**和**LinkedList**都是按照被插入的顺序进行保存的。

### <a name="iterators"></a>Iterators
* ***Iterator***删除的时候是删除当前位置的元素，然后将计数器往前挪一个。
* ***Iterator***和***ListIterator***的区别，前者是单向循环，后者是双向循环，并且添加了==set()==，==add()==方法。
* 针对一个对象的多个Iterator实例，将所有的实例都用作读，用以避免产生ConcurrentModification-Exception。或者只用一个Iterator实例，既用于读又用于写。_但是多个实例可以调用set()方法_。

### <a name="set"></a>Set
**Set** is a collection, ==without duplicates==, in which order is not significant.

* ***TreeSet*** 
	* keeps elements ==sorted== into a red-black tree data structure. This way, you can extract an ordered sequence from a Set. 
	* Elements must also implement the **Comparable** interface.
* ***HashSet*** 
	* uses the hashing function. For Sets where fast lookup time is important. _Elements must also define *hashCode()*_.
	* You would only use a HashSet if you don’t care about the ordering of the elements in the collection.
* ***LinkedHashSet*** 
	* also uses hashing for lookup speed, but appears to maintain elements in ==insertion order== using a linked list. 
	* Has the lookup speed of a HashSet, but internally maintains the order in which you add the elements (the insertion order) using a linked list. 
	* when you iterate through the Set, the results appear in insertion order. _Elements must also define *hashCode()*_.

### <a name="queue"></a>Queue
**Queue** is a collection designed to accept elements at its tail for processing, yielding them up at its head in the order in which they are to be processed. Its subinterface Deque extends this by allowing elements to be added or removed at both head and tail.

* ***LinkedList***
* ***PriorityQueue***

### <a name="map"></a>Map
**Map** is a collection which uses ==key-value== associations to store and retrieve elements.

* ***HashMap*** (Use this class instead of Hashtable.) 
	* based on a hash table.
	* Provides constant-time performance for inserting and locating pairs.
	* bucket的大小是2的n次方来递增的，==默认为16==。
	* **rehash**，当原有的HashMap大小不能容纳下数据的时候，会自动扩大容量，并且将原有的数据重新计算hash值后放入新的HashMap当中，完成后丢弃旧HashMap。==load factor为0.75==
* ***LinkedHashMap*** Like a HashMap
	* when you iterate through it, you get the pairs in insertion order, or in least-recently-used (LRU) order. 
	* Only slightly slower than a HashMap, except when iterating
* ***TreeMap*** 
	* Implementation based on a red-black tree. 
	* When you view the keys or the pairs, they will be in ==sorted order== (determined by Comparable or Comparator). 
	* The point of a TreeMap is that you get the results in sorted order. 
	* TreeMap is the only Map with the ==subMap()== method, which allows you to return a portion of the tree.
* ***WeakHashMap*** 
	* A map of weak keys that allow objects referred to by the map to be released; designed to solve certain types of problems. If no references to a particular key are held outside the map, that key may be garbage collected.
* ***ConcurrentHashMap*** 
	* A thread-safe Map which does not involve synchronization locking.
* ***IdentityHashMap*** 
	* A hash map that ==uses '\==' instead of equals()== to compare keys. 
	* Only for solving special types of problems; not for general use.

### java.util.Collections
* sort()
* shuffle()
* binarySearch()
* reverse()
* min()
* max()

## 2. <a name="exceptions"></a>Exceptions
### Throwable
所有Errors和Exceptions的基类，只有该类极其子类的对象才可以被JVM抛出或者被**throw**语句抛出，同样只有这样才能被**catch**子句捕获。
#### Error
**Error**是**Throwable**的子类，表示程序出现严重错误，程序不该捕获该异常。
#### Exception
**Exception**是**Throwable**的子类，程序应该处理该异常。

* **Unchecked Exception**，包括**Error**和继承自**RuntimeException**的子类。**RuntimeException**本身继承自**Exception**。
* **Checked Exception**，其它继承自**Exception**的子类。

## 3. <a name="concurrency"></a>Concurrency
### Sychronization
#### Critical Section
临界区:⼀一段访问共享资源的代码,不能同时被多个线程执⾏行。#### Lock
##### ReentrantLock
##### ReentrantReadWriteLock
##### Fairless
##### Conditions