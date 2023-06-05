
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
