
# Android application component and life cycle:

## App components

App components are the essential building blocks of an Android app. Each component is an entry point through which the system or a user can enter your app. Some components depend on others.

There are four types of app components:

- Activities
- Services
- Broadcast receivers
- Content providers

Each type serves a distinct purpose and has a distinct lifecycle that defines how a component is created and destroyed. The following sections describe the four types of app components.

**Activities**An *activity* is the entry point for interacting with the user. It represents a single screen with a user interface. For example, an email app might have one activity that shows a list of new emails, another activity to compose an email, and another activity for reading emails. Although the activities work together to form a cohesive user experience in the email app, each one is independent of the others.
A different app can start any one of these activities if the email app allows it. For example, a camera app might start the activity in the email app for composing a new email to let the user share a picture.
An activity facilitates the following key interactions between system and app:
• Keeping track of what the user currently cares about—what is on-screen—so that the system keeps running the process that is hosting the activity.
• Knowing which previously used processes contain stopped activities the user might return to and prioritizing those processes more highly to keep them available.
• Helping the app handle having its process killed so the user can return to activities with their previous state restored.
• Providing a way for apps to implement user flows between each other, and for the system to coordinate these flows.

.**Services**A *service* is a general-purpose entry point for keeping an app running in the background for all kinds of reasons. It is a component that runs in the background to perform long-running operations or to perform work for remote processes. A service does not provide a user interface.
For example, a service might play music in the background while the user is in a different app, or it might fetch data over the network without blocking user interaction with an activity. Another component, such as an activity, can start the service and let it run or bind to it to interact with it.
There are two types of services that tell the system how to manage an app: started services and bound services.
**Started services** tell the system to keep them running until their work is completed. This might be to sync some data in the background or play music even after the user leaves the app. Syncing data in the background or playing music represent different types of started services, which the system handles differently:
• Music playback is something the user is directly aware of, and the app communicates this to the system by indicating that it wants to be in the foreground, with a notification to tell the user that it is running. In this case, the system prioritizes keeping that service's process running, because the user has a bad experience if it goes away.
• A regular background service is not something the user is directly aware of, so the system has more freedom in managing its process. It might let it be killed, restarting the service sometime later, if it needs RAM for things that are of more immediate concern to the user.
**Bound services** run because some other app (or the system) has said that it wants to make use of the service. A bound service provides an API to another process, and the system knows there is a dependency between these processes. So if process A is bound to a service in process B, the system knows that it needs to keep process B and its service running for A. Further, if process A is something the user cares about, then it knows to treat process B as something the user also cares about.
Because of their flexibility, services are useful building blocks for all kinds of higher-level system concepts. Live wallpapers, notification listeners, screen savers, input methods, accessibility services, and many other core system features are all built as services that applications implement and the system binds to when they run.
A service is implemented as a subclass of `[Service](https://developer.android.com/reference/android/app/Service)`. 
er.android.com/training/monitoring-device-state/doze-standby) API. For more information about using this class, see the **`[JobScheduler]

**Broadcast receivers**A *broadcast receiver* is a component that lets the system deliver events to the app outside of a regular user flow so the app can respond to system-wide broadcast announcements. Because broadcast receivers are another well-defined entry into the app, the system can deliver broadcasts even to apps that aren't currently running.
So, for example, an app can schedule an alarm to post a notification to tell the user about an upcoming event. Because the alarm is delivered to a `BroadcastReceiver` in the app, there is no need for the app to remain running until the alarm goes off.
Many broadcasts originate from the system, like a broadcast announcing that the screen is turned off, the battery is low, or a picture is captured. Apps can also initiate broadcasts, such as to let other apps know that some data is downloaded to the device and is available for them to use.
Although broadcast receivers don't display a user interface, they can [create a status bar notification] to alert the user when a broadcast event occurs. More commonly, though, a broadcast receiver is just a *gateway* to other components and is intended to do a very minimal amount of work.
For instance, a broadcast receiver might schedule a `[JobService]` to perform some work based on an event using `[JobScheduler]`. Broadcast receivers often involve apps interacting with each other, so it's important to be aware of the security implications when setting them up.
A broadcast receiver is implemented as a subclass of `[BroadcastReceiver]`, and each broadcast is delivered as an `[Intent]` object. 

**Content providers**A *content provider* manages a shared set of app data that you can store in the file system, in a SQLite database, on the web, or on any other persistent storage location that your app can access. Through the content provider, other apps can query or modify the data, if the content provider permits it.
For example, the Android system provides a content provider that manages the user's contact information. Any app with the proper permissions can query the content provider, such as using `[ContactsContract.Data](https://developer.android.com/reference/android/provider/ContactsContract.Data)`, to read and write information about a particular person.
It is tempting to think of a content provider as an abstraction on a database, because there is a lot of API and support built in to them for that common case. However, they have a different core purpose from a system-design perspective.
To the system, a content provider is an entry point into an app for publishing named data items, identified by a URI scheme. Thus, an app can decide how it wants to map the data it contains to a URI namespace, handing out those URIs to other entities which can in turn use them to access the data. There are a few particular things this lets the system do in managing an app:
• Assigning a URI doesn't require that the app remain running, so URIs can persist after their owning apps exit. The system only needs to make sure that an owning app is still running when it retrieves the app's data from the corresponding URI.
• These URIs also provide an important fine-grained security model. For example, an app can place the URI for an image it has on the clipboard, but leave its content provider locked up so that other apps cannot freely access it. When a second app attempts to access that URI on the clipboard, the system can let that app access the data using a temporary *URI permission grant* so that it accesses the data only behind that URI, and nothing else in the second app.
Content providers are also useful for reading and writing data that is private to your app and not shared.
A content provider is implemented as a subclass of `[ContentProvider]` and must implement a standard set of APIs that enable other apps to perform transactions. For more information, see the [Content providers](https://developer.android.com/guide/topics/providers/content-providers) developer guide

## **[Managing the application life cycle]

[Application]
The application object is already the first components started. It is also always the last component of the application, which is terminated.

This object provides the following main life-cycle methods:

- `onCreate()` - called before the first components of the application starts
- `onLowMemory()` - called when the Android system requests that the application cleans up memory
- `onTrimMemory()` - called when the Android system requests that the application cleans up memory. This message includes an indicator in which position the application is. For example the constant TRIM_MEMORY_MODERATE indicates that the process is around the middle of the background LRU list; freeing memory can help the system keep other processes running later in the list for better overall performance.
- `onTerminate()` - only for testing, not called in production
- `onConfigurationChanged()` - called whenever the configuration changes

****[Activity life cycle]

| onCreate() | Called then the activity is created. Used to initialize the activity, for example create the user interface. |
| --- | --- |
| onResume() | Called if the activity get visible again and the user starts interacting with the activity again. Used to initialize fields, register listeners, bind to services, etc. |
| onPause() | Called once another activity gets into the foreground. Always called before the activity is not visible anymore. Used to release resources or save application data. For example you unregister listeners, intent receivers, unbind from services or remove system service listeners. |
| onStop() | Called once the activity is no longer visible. Time or CPU intensive shut-down operations, such as writing information to a database should be down in the onStop() method. This method is guaranteed to be called as of API 11. |

****[Activity instance state]

*Instance state* describes the UI state of an activity. This is non-persistent application data. It is passed between activities restarts due to a configuration change. The activity is responsible for saving and restoring its instance state.

The `onSaveInstanceState()` can be used to store this instance state as a `Bundle`. A `Bundle` can contain:

- primitive data types
- Strings
- objects which are of the `Parcelable` or `Serialisable` type
- Arrays of the above types

The persisted `Bundle` data is passed at restart of the activity to the `onCreate()` method and `onRestoreInstanceState()` as parameter.

|  | If you override onSaveInstanceState() and onRestoreInstanceState(), you must call super. Android views store their data via a call to View.onSaveInstanceState from the onSaveInstanceState() method of the activity. For example, EditText stores its content via the default call of this method.
For this, the layout needs to define id’s for these views. |
| --- | --- |

The `onRestoreInstanceState()` or the `onCreate()` methods can be used to recreate the instance scope.

|  | Prefer using the onRestoreInstanceState() method for restoring the instance state. This approach separates the initial setup from restoring the state. |
| --- | --- |

If the user interacts with an activity and presses the **Back** button or if the `finish()` method of an activity is called, the activity is removed from the current activity stack and recycled. In this case there is no instance state to save and the `onSaveInstanceState()` method is not called.

If the user presses the **Home** button, the activity instance state must be saved. The `onSaveInstanceState()` method is called. If the user switches again to the activity and if Android terminated it, its activity stack is recreated. The saved bundle is then provided to the `onRestoreInstanceState()` and `onCreate()` methods

**Fragment Lifecycle**

![Untitled](Android%20application%20component%20and%20life%20cycle%209a01e2dbf0c242fe95d174b89d981ab2/Untitled.png)

### Methods of the Android Fragment

| Methods | Description |
| --- | --- |
| onAttach() | The very first method to be called when the fragment has been associated with the activity. This method executes only once during the lifetime of a fragment. |
| onCreate() | This method initializes the fragment by adding all the required attributes and components. |
| onCreateView() | System calls this method to create the user interface of the fragment. The root of the fragment’s layout is returned as the View component by this method to draw the UI. |
| onViewCreated() | It indicates that the activity has been created in which the fragment exists. View hierarchy of the fragment also instantiated before this function call. |
| onStart() | The system invokes this method to make the fragment visible on the user’s device. |
| onResume() | This method is called to make the visible fragment interactive. |
| onPause() | It indicates that the user is leaving the fragment. System call this method to commit the changes made to the fragment. |
| onStop() | Method to terminate the functioning and visibility of fragment from the user’s screen. |
| onDestroyView() | System calls this method to clean up all kinds of resources as well as view hierarchy associated with the fragment. |
| onDestroy() | It is called to perform the final clean up of fragment’s state and its lifecycle. |
| onDetach() | The system executes this method to disassociate the fragment from its host activity. |

### Types of Android Fragments

1. **Single Fragment:** Display only one single view on the device screen. This type of fragment is mostly used for mobile phones.
2. **List Fragment:** This Fragment is used to display a list-view from which the user can select the desired sub-activity. The menu drawer of apps like Gmail is the best example of this kind of fragment.
3. **Fragment Transaction:** This kind of fragments supports the transition from one fragment to another at run time. Users can switch between multiple fragments like switching tabs.



### **1. What is an Activity in Android?**

An activity is a single, focused thing that the user can do. Almost all activities interact with the user, so the Activity class takes care of creating a window for you in which you can place your UI with setContentView(View). While activities are often presented to the user as full-screen windows, they can also be used in other ways: as floating windows (via a theme with windowIsFloating set) or embedded inside of another activity (using ActivityGroup).

### **2. Can you explain the different stages of the activity life cycle on Android?**

There are four different stages in the activity life cycle on Android: created, started, resumed, and destroyed. The created stage is when the activity is first created and initialized. The started stage is when the activity becomes visible to the user. The resumed stage is when the activity is in the foreground and the user can interact with it. The destroyed stage is when the activity is no longer visible to the user and is being removed from memory.

### **3. How can you easily remember the various stages of the activity lifecycle?**

There are four main stages in the activity lifecycle: onCreate(), onStart(), onResume(), and onPause(). You can easily remember these stages by thinking of them as the four C’s: Create, Start, Resume, and Pause.

### **4. When does your app go from being “inactive” to being “paused”?**

When an app is no longer the focus of the user’s attention, but is still running in the background, it is considered to be in the “paused” state. This can happen when the user switches to another app, or if the system needs to free up resources for another app.

### **5. What are some common scenarios for starting a new activity or stopping and existing one?**

Some common scenarios for starting a new activity include when the user presses a button or link, when the user selects an item from a list, or when the user starts a new task. Some common scenarios for stopping an existing activity include when the user presses the back button, when the user finishes a task, or when the user navigates to a new activity.

### **6. When do you need to call onPause(), onResume() and onStop()?**

You need to call onPause() when your activity is no longer visible to the user, onResume() when your activity becomes visible to the user again and onStop() when your activity is no longer visible to the user and is being destroyed.

### **7. What happens when you start another activity while your current activity is paused?**

When you start another activity while your current activity is paused, the new activity will be started and the current activity will be pushed to the background.

### **8. Is it possible to start a new activity without creating a backstack? If yes, then how?**

Yes, it is possible to start a new activity without creating a backstack. You can do this by using the FLAG_ACTIVITY_NO_HISTORY flag when starting the new activity. This will prevent the new activity from being added to the backstack, and as a result, the user will not be able to return to it.

### **9. What’s the difference between Activities and Fragments? Which one would you recommend using in certain situations?**

Activities are a core component of Android applications, and they are responsible for managing the lifecycle of an app. Fragments are a more recent addition to Android, and they are designed to be used within an Activity. They are essentially self-contained modules that can be used to build up a more complex user interface.

If you are looking to create a simple app with a single screen, then an Activity is probably all you need. However, if you are looking to create a more complex app with multiple screens, then you will need to use Fragments to build up the user interface.

### **10. When does an activity become non-interactive? Does this mean that onSaveInstanceState() should be called at this stage?**

An activity becomes non-interactive when it is no longer in the foreground, typically because another activity has been launched in front of it. This does not necessarily mean that onSaveInstanceState() will be called at this stage, as the activity may simply be paused rather than destroyed. However, if the activity is destroyed (for example, if the user presses the back button), then onSaveInstanceState() will be called.

### **11. Can you explain how passing data between activities works on Android?**

When an activity is started, it can be passed data from the activity that started it. This data is stored in the Intent object that is used to start the activity. The Intent object can be accessed by the activity that started it using the getIntent() method. The data that is stored in the Intent object is known as an “extra.” Extras can be of various types, such as strings, integers, and booleans. To add an extra to an Intent object, you use the putExtra() method. To retrieve an extra from an Intent object, you use the getStringExtra(), getIntExtra(), or getBooleanExtra() methods.

### **12. What’s the best way to pass data between two activities?**

The best way to pass data between two activities is to use the Intent class. You can putExtra() data into an Intent, and then get that data out in the second activity with getIntent().getExtra().

### **13. At what point during the activity lifecycle does the system run onCreate()?**

The system runs onCreate() when the activity is first created.

### **14. Do all android apps support multiple instances of the same activity?**

No, not all Android apps support multiple instances of the same activity. In fact, most Android apps only support a single instance of each activity. However, there are some apps that do support multiple instances of the same activity, such as certain productivity apps.

### **15. What is the purpose of the savedInstanceState parameter passed into the onCreate() method?**

The savedInstanceState parameter is used to store data that needs to be saved across activity lifecycles. This is important because when an activity is destroyed, any data that is not stored in the savedInstanceState parameter will be lost.

### **16. What’s the difference between calling finish() and moveTaskToBack(true) ?**

When you call finish() on an activity, it immediately destroys the activity and removes it from the activity stack. This means that the activity can no longer be accessed by the user. When you call moveTaskToBack(true) on an activity, it simply moves the activity to the back of the activity stack. The activity is not destroyed and can still be accessed by the user.

### **17. Why are fragments not used independently but always as part of an activity?**

Fragments are not used independently because they need to be attached to an activity in order to function. This is due to the fact that fragments rely on the activity’s lifecycle to know when to create, destroy, or pause.

### **18. What is the main reason why developers prefer fragments over activities?**

The main reason why developers prefer fragments over activities is that fragments are more modular and can be reused more easily. This means that developers can create more complex and dynamic user interfaces using fragments, without having to create a new activity for every single screen.

### **19. What is the proper way to add a fragment to an activity?**

The proper way to add a fragment to an activity is to first create a new FragmentManager and FragmentTransaction instance, then add the fragment to the activity using the FragmentTransaction.commit() method.

### **20. What are the three major components of the Android architecture?**

The three major components of the Android architecture are the operating system, the middleware, and the applications. The operating system is responsible for managing the hardware and software resources of the device. The middleware is responsible for providing a link between the operating system and the applications. The applications are responsible for providing the user with the functionality they are looking for.

One of the major component in Android is **Activity**, there are many questions related to Android, I tried putting it all together. This is also interview Questions.

1. **Explain Activity Life Cycle.Ans: [**Check Here](https://medium.com/@nithyanataraj/android-activity-life-cycle-32fcd0c2a973)

# ***Scenario Based Questions***

2. **From Activity A, then go to Activity B, then go back to Activity A, Activity A’s which method will be called. Explain.Ans.** onRestart() →onStart() →onResume()

3. **Home Button is pressed when your interacting with the Activity . What life cycle method will be called?Ans.** After hitting the Home ButtononPause() →onStop()

4. **Try to open the app from Launcher. What life cycle method will be called?**

On coming back to app

onRestart() →onStart →onResume

5. **Activity A is opened, then you open a dialog in that Activity, which life cycle method of Activity A will be called.Ans.** Onpause()

6. **When a new activity comes on top of your activity completely, then what is the life cycle function that gets executed in the old activity?Ans.** onPause() →onStop()

7. **What is the mandatory activity life cycle function that will get called in case of configuration changes?Ans.**onPause() →onStop()→onDestroy() →onCreate()→onStart()→onResume()

8. **When will onCreate() and onDestroy() method will be called, and how many times.Ans.** In general onCreate() and onDestroy() will be called only one times, but this two method gets executed twice if user rotates your device. For example, suppose you have an Activity called MainActivity, when you rotate, this life-cycle methods will be called,onPause() → onStop() →onDestroy() →onCreate() →onStart() →onResume()

9. **How to restart an activity programmatically?Ans.** *Intent intent = getIntent();finish();startActivity(intent);*

10. **Is it mandatory to implement onCreate() and onStart() of activity life cycle? Will it run if those methods are removed?Ans.** Not mandatory. Yes it will run even if those methods are removed.

11. **Is it possible to have an Activity without UI?**

**Ans.** Yes it is possible**. Android** provides a theme for this requirement.

Learn about Activity Lifecycle

[https://medium.com/@nithyanataraj/android-activity-life-cycle-32fcd0c2a973](https://medium.com/@nithyanataraj/android-activity-life-cycle-32fcd0c2a973)
