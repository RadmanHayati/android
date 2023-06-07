# Untitled

# Java Garbage Collections Interview Questions

**Q1) Which part of the memory is involved in Garbage Collection? Stack or Heap?**

**Ans)** Heap

**Q2)What is responsiblity of Garbage Collector?**

**Ans)** Garbage collector frees the memory occupied by the unreachable objects during the java program by deleting these unreachable objects.

It ensures that the available memory will be used efficiently, but does not guarantee that there will be sufficient memory for the program to run.

**Q3) Is garbage collector a daemon thread?**

**Ans)** Yes GC is a daemon thread. A daemon thread runs behind the application. It is started by JVM. The thread stops when all non-daemon threads stop.

**Q4)How is Garbage Collection managed?**

**Ans)**The JVM controls the Garbage Collector; it decides when to run the Garbage Collector. JVM runs the Garbage Collector when it realizes that the memory is running low. The behavior of GC can be tuned by passing parameters to JVM. One can request the Garbage Collection to happen from within the java program but there is no guarantee that this request will be taken care of by jvm.

**Q5) When does an object become eligible for garbage collection?**

**Ans)** An object becomes eligible for Garbage Collection when no live thread can access it.

**Q6) What are the different ways to make an object eligible for Garbage Collection when it is no longer needed?**

Ans)

- **Set all available object references to null** once the purpose of creating the object is served :
    
    ```
    public class GarbageCollnTest1 {
       public static void main (String [] args){
          String str = "Set the object ref to null";
            //String object referenced by variable str is not eligible for GC yet
            str = null;
        /*String object referenced by variable str becomes eligible for GC */
        }
      }
    ```
    
- **Make the reference variable to refer to another object** : Decouple the reference variable from the object and set it refer to another object, so the object which it was referring to before reassigning is eligible for Garbage Collection.
    
    ```
    publc class GarbageCollnTest2 {
      public static void main(String [] args){
      String str1 = "Garbage collected after use";
      String str2 = "Another String";
      System.out.println(str1);
      //String object referred by str1 is not eligible for GC yet
      str1 = str2;
      /* Now the str1 variable referes to the String object "Another String" and the object "Garbage collected after use" is not referred by any variable and hence is eligible for GC */
      }
    }
    ```
    
- **Creating Islands of Isolation** : If you have two instance reference variables which are referring to the instances of the same class, and these two reference variables refer to each other and the objects referred by these reference variables do not have any other valid reference then these two objects are said to form an Island of Isolation and are eligible for Garbage Collection.
    
    ```
    public class GCTest3 {
        GCTest3 g;
       public static void main(String [] str){
            GCTest3 gc1 = new GCTest3();
            GCTest3 gc2 = new GCTest3();
            gc1.g = gc2; //gc1 refers to gc2
            gc2.g = gc1; //gc2 refers to gc1
            gc1 = null;
            gc2 = null;
            //gc1 and gc2 refer to each other and have no other valid //references
            //gc1 and gc2 form Island of Isolation
          //gc1 and gc2 are eligible for Garbage collection here
        }
    }
    ```
    

**Q7) Can the Garbage Collection be forced by any means?**

Ans)No. The Garbage Collection can not be forced, though there are few ways by which it can be requested there is no guarantee that these requests will be taken care of by JVM.

**Q8) How can the Garbage Collection be requested?**

Ans) There are two ways in which we can request the jvm to execute the Garbage Collection.

- The methods to perform the garbage collections are present in the Runtime class provided by java. The Runtime class is a Singleton for each java main program. The method getRuntime() returns a singleton instance of the Runtime class. The method gc() can be invoked using this instance of Runtime to request the garbage collection.
- Call the System class System.gc() method which will request the jvm to perform GC.

**Q9) What is the purpose of overriding finalize() method?**

Ans) The finalize() method should be overridden for an object to include the clean up code or to dispose of the system resources that should to be done before the object is garbage collected.

**Q11) How many times does the garbage collector calls the finalize() method for an object?**

Ans) Only once.

**Q12) What happens if an uncaught exception is thrown from during the execution of the finalize() method of an object?**

Ans) The exception will be ignored and the garbage collection (finalization) of that object terminates.

**Q13) What are different ways to call garbage collector?**

Ans) Garbage collection can be invoked using **System.gc() or Runtime.getRuntime().gc()**.

**Q14) How to enable/disable call of finalize() method of exit of the application**

Ans) **Runtime.getRuntime().runFinalizersOnExit(boolean value)** . Passing the boolean value will either disable or enable the finalize() call.

# **Q1. What Does the Statement “Memory Is Managed in Java” Mean?**

Memory is the key resource an application requires to run effectively and like any resource, it is scarce. As such, its allocation and deallocation to and from applications or different parts of an application require a lot of care and consideration.

However, in Java, a developer does not need to explicitly allocate and deallocate memory – the JVM and more specifically the Garbage Collector – has the duty of handling memory allocation so that the developer doesn't have to.

This is contrary to what happens in languages like C where a programmer has direct access to memory and literally references memory cells in his code, creating a lot of room for memory leaks.

# **Q2. What Is Garbage Collection and What Are Its Advantages?**

Garbage collection is the process of looking at heap memory, identifying which objects are in use and which are not, and deleting the unused objects.

An in-use object, or a referenced object, means that some part of your program still maintains a pointer to that object. An unused object, or unreferenced object, is no longer referenced by any part of your program. So the memory used by an unreferenced object can be reclaimed.

The biggest advantage of garbage collection is that it removes the burden of manual memory allocation/deallocation from us so that we can focus on solving the problem at hand.

# **Q3. Are There Any Disadvantages of Garbage Collection?**

Yes. Whenever the garbage collector runs, it has an effect on the application's performance. This is because all other threads in the application have to be stopped to allow the garbage collector thread to effectively do its work.

Depending on the requirements of the application, this can be a real problem that is unacceptable by the client. However, this problem can be greatly reduced or even eliminated through skillful optimization and garbage collector tuning and using different GC algorithms.

# **Q4. What Is the Meaning of the Term “Stop-The-World”?**

When the garbage collector thread is running, other threads are stopped, meaning the application is stopped momentarily. This is analogous to house cleaning or fumigation where occupants are denied access until the process is complete.

Depending on the needs of an application, “stop the world” garbage collection can cause an unacceptable freeze. This is why it is important to do garbage collector tuning and JVM optimization so that the freeze encountered is at least acceptable.

# **Q5. What Are Stack and Heap? What Is Stored in Each of These Memory Structures, and How Are They Interrelated?**

The stack is a part of memory that contains information about nested method calls down to the current position in the program. It also contains all local variables and references to objects on the heap defined in currently executing methods.

This structure allows the runtime to return from the method knowing the address whence it was called, and also clear all local variables after exiting the method. Every thread has its own stack.

The heap is a large bulk of memory intended for allocation of objects. When you create an object with the *new* keyword, it gets allocated on the heap. However, the reference to this object lives on the stack.

# **Q6. What Is Generational Garbage Collection and What Makes It a Popular Garbage Collection Approach?**

Generational garbage collection can be loosely defined as the strategy used by the garbage collector where the heap is divided into a number of sections called generations, each of which will hold objects according to their “age” on the heap.

Whenever the garbage collector is running, the first step in the process is called marking. This is where the garbage collector identifies which pieces of memory are in use and which are not. This can be a very time-consuming process if all objects in a system must be scanned.

As more and more objects are allocated, the list of objects grows and grows leading to longer and longer garbage collection time. However, empirical analysis of applications has shown that most objects are short-lived.

With generational garbage collection, objects are grouped according to their “age” in terms of how many garbage collection cycles they have survived. This way, the bulk of the work spread across various minor and major collection cycles.

Today, almost all garbage collectors are generational. This strategy is so popular because, over time, it has proven to be the optimal solution.

# **Q7. Describe in Detail How Generational Garbage Collection Works**

To properly understand how generational garbage collection works, it is important to first **remember how Java heap is structured** to facilitate generational garbage collection.

The heap is divided up into smaller spaces or generations. These spaces are Young Generation, Old or Tenured Generation, and Permanent Generation.

The **young generation hosts most of the newly created objects**. An empirical study of most applications shows that majority of objects are quickly short lived and therefore, soon become eligible for collection. Therefore, new objects start their journey here and are only “promoted” to the old generation space after they have attained a certain “age”.

The term **“age”** in generational garbage collection **refers to the number of collection cycles the object has survived**.

The young generation space is further divided into three spaces: an Eden space and two survivor spaces such as Survivor 1 (s1) and Survivor 2 (s2).

The **old generation hosts objects that** **have lived in memory longer than a certain “age”**. The objects that survived garbage collection from the young generation are promoted to this space. It is generally larger than the young generation. As it is bigger in size, the garbage collection is more expensive and occurs less frequently than in the young generation.

The **permanent generation** **or more commonly called, *PermGen,* contains metadata required by the JVM** to describe the classes and methods used in the application. It also contains the string pool for storing interned strings. It is populated by the JVM at runtime based on classes in use by the application. In addition, platform library classes and methods may be stored here.

First, **any new objects are allocated to the Eden space**. Both survivor spaces start out empty. When the Eden space fills up, a minor garbage collection is triggered. Referenced objects are moved to the first survivor space. Unreferenced objects are deleted.

During the next minor GC, the same thing happens to the Eden space. Unreferenced objects are deleted and referenced objects are moved to a survivor space. However, in this case, they are moved to the second survivor space (S2).

In addition, objects from the last minor GC in the first survivor space (S1) have their age incremented and are moved to S2. Once all surviving objects have been moved to S2, both S1 and Eden space are cleared. At this point, S2 contains objects with different ages.

At the next minor GC, the same process is repeated. However this time the survivor spaces switch. Referenced objects are moved to S1 from both Eden and S2. Surviving objects are aged. Eden and S2 are cleared.

After every minor garbage collection cycle, the age of each object is checked. Those that have reached a certain arbitrary age, for example, 8, are promoted from the young generation to the old or tenured generation. For all subsequent minor GC cycles, objects will continue to be promoted to the old generation space.

This pretty much exhausts the process of garbage collection in the young generation. Eventually, a major garbage collection will be performed on the old generation which cleans up and compacts that space. For each major GC, there are several minor GCs.

# **Q8. When Does an Object Become Eligible for Garbage Collection? Describe How the Gc Collects an Eligible Object?**

An object becomes eligible for Garbage collection or GC if it is not reachable from any live threads or by any static references.

The most straightforward case of an object becoming eligible for garbage collection is if all its references are null. Cyclic dependencies without any live external reference are also eligible for GC. So if object A references object B and object B references Object A and they don't have any other live reference then both Objects A and B will be eligible for Garbage collection.

Another obvious case is when a parent object is set to null. When a kitchen object internally references a fridge object and a sink object, and the kitchen object is set to null, both fridge and sink will become eligible for garbage collection alongside their parent, kitchen.

# **Q9. How Do You Trigger Garbage Collection from Java Code?**

**You, as Java programmer, can not force garbage collection in Java**; it will only trigger if JVM thinks it needs a garbage collection based on Java heap size.

Before removing an object from memory garbage collection thread invokes finalize()method of that object and gives an opportunity to perform any sort of cleanup required. You can also invoke this method of an object code, however, there is no guarantee that garbage collection will occur when you call this method.

Additionally, there are methods like System.gc() and Runtime.gc() which is used to send request of Garbage collection to JVM but it’s not guaranteed that garbage collection will happen.

# **Q10. What Happens When There Is Not Enough Heap Space to Accommodate Storage of New Objects?**

If there is no memory space for creating a new object in Heap, Java Virtual Machine throws *OutOfMemoryError* or more specifically ***java.lang.OutOfMemoryError* heap space.**

# **Q11. Is It Possible to «Resurrect» an Object That Became Eligible for Garbage Collection?**

When an object becomes eligible for garbage collection, the GC has to run the *finalize* method on it. The *finalize* method is guaranteed to run only once, thus the GC flags the object as finalized and gives it a rest until the next cycle.

In the *finalize* method you can technically “resurrect” an object, for example, by assigning it to a *static* field. The object would become alive again and non-eligible for garbage collection, so the GC would not collect it during the next cycle.

The object, however, would be marked as finalized, so when it would become eligible again, the finalize method would not be called. In essence, you can turn this “resurrection” trick only once for the lifetime of the object. Beware that this ugly hack should be used only if you really know what you're doing — however, understanding this trick gives some insight into how the GC works.

# **Q12. Describe Strong, Weak, Soft and Phantom References and Their Role in Garbage Collection.**

Much as memory is managed in Java, an engineer may need to perform as much optimization as possible to minimize latency and maximize throughput, in critical applications. Much as **it is impossible to explicitly control when garbage collection is triggered** in the JVM, **it is possible to influence how it occurs as regards the objects we have created.**

Java provides us with reference objects to control the relationship between the objects we create and the garbage collector.

By default, every object we create in a Java program is strongly referenced by a variable:

```
StringBuilder sb =newStringBuilder();Copy
```

In the above snippet, the *new* keyword creates a new *StringBuilder* object and stores it on the heap. The variable *sb* then stores a **strong reference** to this object. What this means for the garbage collector is that the particular *StringBuilder* object is not eligible for collection at all due to a strong reference held to it by *sb*. The story only changes when we nullify *sb* like this:

```
sb = null;Copy
```

After calling the above line, the object will then be eligible for collection.

We can change this relationship between the object and the garbage collector by explicitly wrapping it inside another reference object which is located inside *java.lang.ref* package.

A **soft reference** can be created to the above object like this:

```
StringBuilder sb =newStringBuilder();
SoftReference<StringBuilder> sbRef =newSoftReference<>(sb);
sb = null;Copy
```

In the above snippet, we have created two references to the *StringBuilder* object. The first line creates a **strong reference** *sb* and the second line creates a **soft reference** *sbRef*. The third line should make the object eligible for collection but the garbage collector will postpone collecting it because of *sbRef*.

The story will only change when memory becomes tight and the JVM is on the brink of throwing an *OutOfMemory* error. In other words, objects with only soft references are collected as a last resort to recover memory.

A **weak reference** can be created in a similar manner using *WeakReference* class. When *sb* is set to null and the *StringBuilder* object only has a weak reference, the JVM's garbage collector will have absolutely no compromise and immediately collect the object at the very next cycle.

A **phantom reference** is similar to a weak reference and an object with only phantom references will be collected without waiting. However, phantom references are enqueued as soon as their objects are collected. We can poll the reference queue to know exactly when the object was collected.

# **Q13. Suppose We Have a Circular Reference (Two Objects That Reference Each Other). Could Such Pair of Objects Become Eligible for Garbage Collection and Why?**

Yes, a pair of objects with a circular reference can become eligible for garbage collection. This is because of how Java's garbage collector handles circular references. It considers objects live not when they have any reference to them, but when they are reachable by navigating the object graph starting from some garbage collection root (a local variable of a live thread or a static field). If a pair of objects with a circular reference is not reachable from any root, it is considered eligible for garbage collection.

# **Q14. How Are Strings Represented in Memory?**

A *String* instance in Java is an object with two fields: a *char[] value* field and an *int hash* field. The *value* field is an array of chars representing the string itself, and the *hash* field contains the *hashCode* of a string which is initialized with zero, calculated during the first *hashCode()* call and cached ever since. As a curious edge case, if a *hashCode* of a string has a zero value, it has to be recalculated each time the *hashCode()* is called.

Important thing is that a *String* instance is immutable: you can't get or modify the underlying *char[]* array. Another feature of strings is that the static constant strings are loaded and cached in a string pool. If you have multiple identical *String* objects in your source code, they are all represented by a single instance at runtime.

# **Q15. What Is a Stringbuilder and What Are Its Use Cases? What Is the Difference Between Appending a String to a Stringbuilder and Concatenating Two Strings with a + Operator? How Does Stringbuilder Differ from Stringbuffer?**

*StringBuilder* allows manipulating character sequences by appending, deleting and inserting characters and strings. This is a mutable data structure, as opposed to the *String* class which is immutable.

When concatenating two *String* instances, a new object is created, and strings are copied. This could bring a huge garbage collector overhead if we need to create or modify a string in a loop. *StringBuilder* allows handling string manipulations much more efficiently.

*StringBuffer* is different from *StringBuilder* in that it is thread-safe. If you need to manipulate a string in a single thread, use *StringBuilder* instead.

---

**1. Why is garbage collection necessary in Java?**

In many programming languages, such as [C and C++](https://www.theserverside.com/opinion/Is-Java-slow-Compared-to-C-its-faster-than-you-think), when an object is no longer needed by a program, the developer must take programmatic steps to reclaim any space the object was allocated in memory.

This approach can be incredibly efficient when implemented properly. However, history has shown that when this process is done poorly, [memory leaks](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Fix-Java-memory-leaks-JVM-heap-dumps-Recorder-Mission-Control) can occur and [crash an application](https://www.theserverside.com/post/The-benefits-and-drawbacks-of-Javas-fail-safe-iterators).

When the Java language was created, Sun engineers decided that developers should not be responsible for managing the memory used by the objects they create. Instead, a garbage collection routine would be part of the JVM; this routine identifies objects that are no longer in use and deletes them from memory.

**2. When does a Java object become available for garbage collection?**

An object becomes available for garbage collection when it is marked as null, goes out of scope or is no longer referenced by any non-null objects within an application. In simple terms, a Java object becomes available for garbage collection when it is no longer in use by the application.

**3. What does mark-and-sweep mean?**

You can break garbage collection in Java into two major stages. The first is the mark stage, where the JVM looks at every object in memory and identifies whether it is still needed or not. If the object is not needed, it is marked for garbage collection.

The sweep is the second stage, where the JVM performs the garbage collection and memory reclamation.

Garbage collection algorithms that employ this sequence of events are known as mark-and-sweep garbage collectors.

**4. What is the drawback to garbage collection?**

The primary drawback to garbage collection is that it freezes all active threads when the memory reclamation phase takes place.

A full garbage collection cycle will run for several seconds -- or potentially even several minutes. Furthermore, garbage collection routines can't be scheduled. Imagine you're running a high-volume trading program. Now imagine a garbage collection routine happening two minutes before the stock market closes. A stop-the-world event on the JVM at that moment in time would lead to a large number of unhappy application users.

Poorly timed garbage collection can make an enterprise system look unpredictable and unreliable. Understandably, a great deal of work has been done in the Java garbage collection arena in order to minimize the impact a Java garbage collection cycle has on active systems.

![https://cdn.ttgtmedia.com/rms/onlineimages/JVM_pause_times_mobile.jpg](https://cdn.ttgtmedia.com/rms/onlineimages/JVM_pause_times_mobile.jpg)

TECHTARGET

Most Java garbage collection interview questions include the topic of JVM pause times and the significance of stop-the-world events.

# 

**5. What is generational garbage collection?**

The JVM splits allocated memory into four separate spaces:

- eden
- survivor
- tenured
- metaspace

Low-level JVM components, such as the string buffer and compiled classes, are allocated memory in the metaspace. This space goes relatively unchanged over time. When people talk about garbage collection, the focus is typically on the eden, survivor and tenured spaces.

When an object is first created, it is placed in the eden space. If garbage collection occurs and the object is still referenced, it gets moved to the survivor space. If enough garbage collections happen and an object in the survivor space never gets collected, it is then moved to the tenured space.

Eden, survivor and the tenured space are all garbage collected separately, with eden collected the most often and the tenured space collected the least. This helps to improve performance, as the weak generational hypothesis tells us that long-lived objects are likely to remain active, making an inspection of their garbage collection eligibility a waste of time.

Furthermore, objects in the eden space are more likely to be short-lived and eligible for removal, so a scan of the eden space is more likely to free up a large block of memory.

Division of the garbage collector into eden, survivor, tenured and the metaspace areas greatly improves JVM performance.

![https://cdn.ttgtmedia.com/rms/onlineimages/Fig_2_mobile.jpg](https://cdn.ttgtmedia.com/rms/onlineimages/Fig_2_mobile.jpg)

JConsole provides insights on the time required to garbage collect young (eden + survivor) and old (tenured) sections of the Java heap.

# 

**6. What's the difference between a minor, major and full garbage collection?**

There is no official specification that defines how a major, minor and full garbage collection cycle differ. However, it is commonly understood that:

- A minor garbage collection does a mark-and-sweep routine on the eden space.
- A major garbage collection works on the survivor space.
- A full garbage collection works on the tenured space.

Since an event that triggers a full garbage collection will normally trigger a sweep of the eden, survivor and metaspace, a full garbage collection cycle is often said to include these areas of the Java heap as well.

**7. How does a Java memory leak affect garbage collection?**

A memory leak increases memory consumption, and the JVM is forced to run more often to clear space for new objects. Garbage collection routines will run more frequently, and free up less memory each time they run, until eventually there is no heap space left.

![https://cdn.ttgtmedia.com/rms/onlineimages/Java_Mission_Control_profiling_mobile.jpg](https://cdn.ttgtmedia.com/rms/onlineimages/Java_Mission_Control_profiling_mobile.jpg)

Java garbage collection interview questions often require the interviewee to answer questions about memory leaks, as seen profiled here in Java Mission Control.

# 

**8. When would you choose the parallel garbage collector (GC) over Concurrent Mark Sweep (CMS) or the G1 garbage collector?**

The G1 garbage collector works best when a system can dedicate a large amount of memory to the heap.

CMS uses extra threads and processing power to perform garbage collection routines without any perceived impact on application performance. It also works best with heaps smaller than 32 GB in size.

If a system does not have an extensive amount of memory dedicated to the heap or surplus processing power to allocate to CMS, a simple parallel GC is the correct choice.

Also, a parallel GC will often collect more garbage over a given period when compared to other algorithms. However, the tradeoff is longer stop-the-world pauses. If pause times are not a concern, parallel garbage collection can be the best choice.

**9. Can you trigger garbage collection from code?**

The System.gc() command can issue a request to the JVM to prioritize garbage collection, but the non-deterministic nature of the garbage collection algorithms means there is no guarantee on when the JVM will respond to such a request.

Common wisdom is to avoid the System.gc() command in code and find other ways to configure the JVM's Java garbage collection algorithms to achieve optimal memory management performance.

However, it's worth mentioning that while the specification says the JVM may ignore a call to System.gc(), the reality is that no current implementation does unless specifically configured to do so. "And even then, there is a tooling path that ignores that config," says Java performance expert [Kirk Pepperdine](http://www.kodewerk.com/about.html).

**10. What strategy can you use to minimize the impact of stop-the-world garbage collection routines in enterprise systems?**

One strategy is to cluster your server and assign more than enough memory to the Java heap than any individual cluster member would ever consume in a day.

Then, during non-peak hours, take one cluster member offline at a time, allowing the other members to handle the workload. At that point, either restart the JVM or force a Java garbage collection with the Java Diagnostic Command (JCMD):

C:>jdk11\bin\jcmd GC.run

When a tool like [Java Mission Control](https://www.theserverside.com/definition/Java-Mission-Control) or JConsole verifies that garbage collection successfully occurred, have the server rejoin the cluster and then perform the same steps on other cluster members.
