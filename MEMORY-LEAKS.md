# [Untitled](https://proandroiddev.com/everything-you-need-to-know-about-memory-leaks-in-android-d7a59faaf46a)

### **1. What is a memory leak?**

A memory leak is when a piece of software allocates memory but fails to properly deallocate it when it is no longer needed. This can lead to the software gradually using up more and more memory over time, eventually causing it to crash.

### **2. Can you explain the difference between a dangling pointer and a wild pointer?**

A dangling pointer is a pointer that points to an object that no longer exists. A wild pointer is a pointer that points to an invalid memory address.

### **3. Can you give me some examples of real-world applications that have suffered from memory leaks in production?**

Yes, there are many examples of real-world applications that have suffered from memory leaks in production. One example is the Microsoft Windows operating system, which has been known to suffer from memory leaks that can cause the system to become unstable and eventually crash. Other examples include web browsers such as Mozilla Firefox and Google Chrome, which can also suffer from memory leaks that can cause the browser to slow down or crash.

### **4. How can you avoid memory leaks when programming?**

One way to avoid memory leaks is to make sure that you free any memory that you have allocated when you are finished using it. Another way to avoid memory leaks is to use reference counting, which can help to automatically keep track of how many references there are to a particular piece of data and free it when there are no more references.

### **5. What are memory maps?**

A memory map is a representation of how memory is laid out for a particular process. It shows which areas of memory are being used for what purposes, and can be very helpful in debugging memory-related issues.

### **6. Can you explain what last level cache (LLC) is and how it relates to memory leaks?**

LLC is a type of cache memory that is located between the CPU and main memory. It is used to store frequently accessed data that is likely to be reused. A memory leak can occur when data that is no longer needed is stored in the LLC, taking up space that could be used for other data. This can lead to performance issues and can eventually cause the system to run out of memory.

### **7. What are the ways to prevent memory leaks?**

The best way to prevent memory leaks is to avoid them in the first place by writing code that is clean and well-organized. However, if you do find yourself with a memory leak, there are a few ways to try and fix it. One way is to try and identify the source of the leak and then remove it. Another way is to try and increase the amount of memory available to the program so that it can continue to run without issue.

### **8. How do you debug an application if there’s a memory leak?**

The first step is to identify where the memory leak is occurring. This can be done by using a tool like Valgrind. Once you have identified the location of the leak, you can then start to look at the code to try and identify what is causing the leak.

### **9. What kind of problems can be caused by memory leaks in a system?**

Memory leaks can cause a number of problems in a system, including decreased performance, instability, and crashes. If a memory leak is not fixed, it can eventually lead to the system running out of memory and becoming unusable.

### **10. Can you explain what a red zone is?**

A red zone is an area of memory that is reserved for critical data structures. When a program allocates memory for a data structure, it also sets aside a small amount of memory in the red zone. If the program tries to access this memory, it will trigger a memory protection fault, which can be caught and handled by the program. This allows the program to detect and recover from buffer overflows and other memory corruption errors.

### **11. Why are memory leaks considered such a big issue?**

Memory leaks can cause big issues because they can gradually eat away at a computer’s available RAM, eventually leading to crashes or other stability problems. Additionally, if a memory leak is left unchecked, it can eventually lead to a situation where the program is using up so much RAM that it starts to negatively impact other programs running on the computer.

### **12. What is your understanding about heaps and stacks?**

The heap is a region of memory where data is allocated dynamically, while the stack is a region of memory where data is allocated statically. The heap is typically larger than the stack, and data is stored in the heap for a longer period of time than data in the stack. When a program allocates memory on the heap, it is responsible for deallocating that memory when it is no longer needed. If the program does not deallocate memory on the heap, then a memory leak will occur.

### **13. What does Garbage Collection mean? Is it related to memory leaks?**

Garbage collection is the process of automatically freeing up memory that is no longer being used by a program. It is related to memory leaks in the sense that it can help to prevent them. Memory leaks occur when a program allocates memory but fails to properly free it up when it is no longer needed, and over time this can lead to the program using up more and more memory until it eventually crashes. Garbage collection can help to prevent this by automatically freeing up memory that is no longer being used.

### **14. What types of tools are available for detecting memory leaks?**

There are a few different types of tools that can be used for detecting memory leaks. One type of tool is a memory profiler, which can be used to take snapshots of an application’s memory usage over time. This can help to identify which parts of the code are using the most memory, and where potential leaks might be occurring. Another type of tool is a memory debugger, which can be used to track down the source of a leak by monitoring memory allocations and deallocations.

### **15. What is virtual memory?**

Virtual memory is a memory management technique that is used by operating systems to provide each process with its own private address space. This address space is created by the operating system when the process is created and is destroyed when the process is terminated.

### **16. What is the best way to find out which code block is causing a particular memory leak?**

The best way to find out which code block is causing a particular memory leak is to use a memory profiler. A memory profiler is a tool that can help you to identify which code blocks are using up the most memory. This can be extremely helpful in pinpointing which code blocks are causing a memory leak.

### **17. What are good practices to follow when designing a software architecture to prevent memory leaks?**

There are a few good practices to follow when designing a software architecture to prevent memory leaks:

1. Use object pools: Object pools can help to reuse objects and prevent memory leaks by keeping track of objects that are no longer in use.

2. Use reference counting: Reference counting can help to keep track of how many references there are to an object. If an object is no longer referenced, then it can be freed.

3. Use garbage collection: Garbage collection can automatically free objects that are no longer in use.

### **18. What is heap overflow?**

A heap overflow is a type of memory corruption that can occur when a program allocates too much memory for an object on the heap. This can lead to a situation where the program can no longer access the object, and may cause the program to crash.

### **19. Can you explain what pointers mean in programming?**

Pointers are variables that store the address of another variable. In other words, they point to the location of another value in memory. When you create a pointer, you are essentially creating a new variable that points to the location of another variable.

### **20. What happens when there’s a memory leak?**

A memory leak is when a program fails to release memory that it no longer needs. This can cause the program to use up more and more memory over time, eventually leading to it crashing.

A memory leak is basically a failure of releasing unused objects from the memory. As a developer one does not need to think about memory allocation, memory deallocation, and garbage collection. All of these are the automatic process that the **[garbage collector](https://www.geeksforgeeks.org/garbage-collection-java/)** does by itself, but the situation becomes difficult for the garbage collector when the user is referencing the object, which is in not use anymore, but since that object is being referenced by another object, garbage collector feels that the unused object is being used by another object and due to this garbage collector does not free-up the memory of that object, due to which available heap memory get decreases leading to memory shortage and memory leak. **The unfreed object is basically called as leaks.**

Memory leaks are the common causes of application crashes in android apps. Every developer must know how to avoid memory leaks and what are the circumstances which can lead to memory leaks in android applications. When the RAM resources are not released when they are no longer needed and if this is done several times, the part of the memory that the operating system has assigned to that particular application may exceed the upper limit and the system can terminate the application causing the application to crash. **Holding the references of the object and resources that are no longer needed is the main cause of the memory leaks in android applications.**  As it is known that the memory for the particular object is allocated within the heap and the object point to certain resources using some object reference. But when the work is completed, the object references should be freed. But when it is not done, the heap space increases continuously and the rest of the application has to run on whatever heap space that is left, and ultimately there are high chances that it can lead to memory leaks in the application. Thus it can be said that memory leaks are a term used when our app goes short of the memory because some object which is not used but still there are being pointed out by the references and continually occupying the heap space, which ultimately leads to a shortage of space for the other components of the application and thus eventually causing the app to crash.

> Note: One needs to remember that whenever there is a shortage of space in the heap and the system needs to allocate space for some new objects, the garbage collector is being called in the frequent intervals, causing to slow down of the application or sometime the application may crash.
> 

### Causes of Memory Leaks and Their Solutions

**1. Using Static Views**

One should not use static views while developing the application, as static views are never destroyed.

**2. Using Static Context**

One should never use the **[Context](https://www.geeksforgeeks.org/what-is-context-in-android/)** as static, because that context will be available through the life of the application, and will not be restricted to the particular activity.

> public class MainActivity extends AppCompatActivity {     // this should not be done     private static Button button;}
> 

**3. Using Code Abstraction Frequently**

Developers often take the advantage of the abstraction property because it provides the code maintenance and flexibility in code, but using abstraction might cost a bit to the developer, as while using abstraction one needs to write more code, more code means more time to execute the space and more RAM. So whenever one can avoid the abstraction in the code, it is code as it can lead to fewer memory leaks.

**4. Unregistered  Listeners**

When the developer uses any kind of listener in his application code, then the developer should not forget to unregister the listener.

**5. Unregistered  Receivers**

Many times the developer needs to register the local broadcast receiver in an activity. However, if the developer does not unregisters the broadcast receiver there is a strong chance that our app can lead to the memory leak problem as the receiver will hold a strong reference to the activity. So even if the activity is of no use, it will prevent the garbage collector to collect the activity for garbage collection, which will ultimately cause the memory leak.

# Kotlin

```kotlin
// sample kotlin program for broadcast receiver 
import android.app.Activity
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.content.IntentFilter
import android.os.Bundle
import com.example.myapplication.R
  
class LocalBroadcastReceiverActivity : Activity() {
  
    private var localBroadcastReceiver: BroadcastReceiver? = null
  
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
  
    private fun registerBroadCastReceiver() {
        localBroadcastReceiver = object : BroadcastReceiver() {
            override fun onReceive(context: Context, intent: Intent) {
                // Write your code here
            }
        }
        registerReceiver(localBroadcastReceiver, IntentFilter("android.net.conn.CONNECTIVITY_CHANGE"))
    }
  
    override fun onStart() {
        super.onStart()
        // registering the broadcast receiver
        registerBroadCastReceiver()
    }
  
    override fun onStop() {
         super.onStop()
          
         // Broadcast receiver holds the implicit reference of Activity.
           // Therefore even if activity is destroy,
         // garbage collector will not be able to remove its instance.
         if (localBroadcastReceiver != null) {
            unregisterReceiver(localBroadcastReceiver)
        }
    }
}// sample kotlin program for broadcast receiver 
import android.app.Activity
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.content.IntentFilter
import android.os.Bundle
import com.example.myapplication.R
  
class LocalBroadcastReceiverActivity : Activity() {
  
    private var localBroadcastReceiver: BroadcastReceiver? = null
  
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
  
    private fun registerBroadCastReceiver() {
        localBroadcastReceiver = object : BroadcastReceiver() {
            override fun onReceive(context: Context, intent: Intent) {
                // Write your code here
            }
        }
        registerReceiver(localBroadcastReceiver, IntentFilter("android.net.conn.CONNECTIVITY_CHANGE"))
    }
  
    override fun onStart() {
        super.onStart()
        // registering the broadcast receiver
        registerBroadCastReceiver()
    }
  
    override fun onStop() {
         super.onStop()
          
         // Broadcast receiver holds the implicit reference of Activity.
           // Therefore even if activity is destroy,
         // garbage collector will not be able to remove its instance.
         if (localBroadcastReceiver != null) {
            unregisterReceiver(localBroadcastReceiver)
        }
    }
}
```

---

**6. Inner class Reference**

An inner class is often used by the android developers within their code. However, the nonstatic class will hold the implicit reference of the parent class which can cause the memory leak problem. So there can be two solutions that can be proposed to solve this problem:

- One can make the inner class static
- If one wants to pass the reference of the non-static inner class, then it can be passed using weak reference.

### Tools to Detect Memory Leak

As it is known that when something cannot be seen, it is very difficult to fix it, same is the case with the memory leak, **it cannot be seen, so it is very difficult to fix**. But there are some tools that help us to detect the memory leaks in the android application and helps us to fix it. Let’s see some of the most popular tools:

**1. Leak Canary**

Leak Canary is a memory detection library in Android. It is developed by a square cup company. This library has a unique ability to decrease down the memory leak and helping developers to get less “MemoryOutOfError”. Leak canary even helps us to notify where the leak is actually happening. To use Leak-Canary, add the following dependency in the **[build.gradle(app level file)](https://www.geeksforgeeks.org/android-build-gradle/)**.

> dependencies { // debugImplementation because LeakCanary should only run in debug builds. debugImplementation ‘com.squareup.leakcanary:leakcanary-android:2.4’}
> 

Once the leak canary is installed it automatically detects and reports memory leaks in 4 steps:

- Detecting retained objects.
- Dumping the heap.
- Analyzing the heap.
- Categorizing leaks.

If one wants to dig deeper and learn how to leak canary report memory leaks can refer to the **[official documentation of leak canary](https://square.github.io/leakcanary/fundamentals/)**.

**2. Android Profiler**

It is basically a tool that helps to keep track of memory usage of every application in android. It replaced Android Monitor in the android version 3.0 and higher. The Android Profiler is compatible with Android 5.0 (API level 21) and higher. Android Profiler detects the performance of the application in the real-time on the parameters like:

- Battery
- Memory (In MB)
- CPU Usage (In %)
- Network Rate(Rate of uploading and receiving)

To open the android profiler within the Android project in android studio, perform the following steps: **Choose View > Tool Windows > Profiler > Select deployment target and choose the device.** The performance of the app will be listed as shown as in the image below:

![https://media.geeksforgeeks.org/wp-content/uploads/20200923172750/AndroidProfiler.PNG](https://media.geeksforgeeks.org/wp-content/uploads/20200923172750/AndroidProfiler.PNG)

To know more about how the android profiler works, refer to the **[official documentation of the android profiler](https://developer.android.com/studio/profile/android-profiler)**.
