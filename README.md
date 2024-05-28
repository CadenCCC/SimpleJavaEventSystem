# Java Event System
This is a basic proof of concept. How you use it is up to you.
Zero updates will be given to this repo unless a problem happens with new Java versions or someone points out a problem to me.

# How to Use
In order to use we need to invoke the `EventManager`[^1].
If you are using a `Listener`[^2] or using the `Subscribe`[^3] annotation, 
you're going to need to have an `Event`[^4].

```java 
import net.nerites.event.manager.EventManager;

public class MyTestClass {
    EventManager EVENT_BUS = new EventManager();
}
```

Creating an `Event`[^4] is super easy, you can use the `Cancelable`[^5] annotation to give it the possibility to be canceled.
if `Cancelable`[^5] is not present, the event will become uncancelable.

```java
import net.nerites.event.Event;
import net.nerites.event.annotations.Cancelable;

@Cancelable // putting this here will allow it to be canceled
public class MyTestEvent extends Event {
    private int changeableValue = 0;
    
    public int getChangeableValue() {
        return changeableValue;
    }
    
    public void changeValue(int other) {
        this.changeableValue = other;
    }
}
```

Creating a `Listener`[^2] is just as easy, you can do this by just creating a **class** and extending `Listener`[^2]
and adding the annotation `EventInfo`[^6]. Adding that annotation is important because the `Listener`[^2] will not work without it as it needs to be there to identify the `Event`[^4].
It is also important to put your parent in the `Listener`[^2] as it allows it to access the parent.
When the `Listener`[^2] is sent to the `EventManager`[^1] it looks for `Listen`[^7], which it uses the **method** that is connected with that annotation and invokes it.

```java
import net.nerites.event.Listener;
import net.nerites.event.annotations.EventInfo;
import net.nerites.event.annotations.Listen;

@EventInfo(MyTestEvent.class) // has to be here or the EventManager won't be able to use this listener.
public class MyTestListener extends Listener<MyTestClass> {

    public MyTestListener(MyTestClass parent) {
        super(parent);
    }

    @Listen // this has a priority system attached to it.
    public void myTestEventInvoke(MyTestEvent event/* only 1 parameter */) { // this method has to be public or the EventManager will not be able to invoke it.
        System.out.println(event.getChangeableValue());
        event.changeValue(12);
        System.out.println(event.getChangeableValue());
    }
}
```

Using the `Subscribe`[^3] is pretty simple as well, you need the `EventManager`[^1] to use the **subscribe**[^8] method on the **class** you have the method with the `Subscribe`[^3] annotation in.
Using the **subscribe**[^8] method in the same class as any method with the `Subscribe`[^3] annotation, and an `Event`[^4] for it's **only parameter**.
Will allow the `EventManager`[^1] to put it in its map.

```java
import net.nerites.event.annotations.Subscribe;
import net.nerites.event.manager.EventManager;

public class MyTestClass {
    EventManager EVENT_BUS = new EventManager();

    public MyTestClass() {
        EVENT_BUS.subscribe(this);
    }

    @Subscribe // this has a priority system attached to it.
    public void myTestEventInvoke(MyTestEvent event) { // this method also HAS to be public
        System.out.println(event.getChangeableValue());
        event.changeValue(111);
        System.out.println(event.getChangeableValue());
    }
}
```

# All Test Code

```java
import net.nerites.event.Event;
import net.nerites.event.annotations.Cancelable;
import net.nerites.event.manager.EventManager;

public class MyTestClass {
    EventManager EVENT_BUS = new EventManager();

    public MyTestClass() {
        EVENT_BUS.subscribe(this);
        EVENT_BUS.subscribe(new MyTestListener(this));
    }

    @Subscribe // this has a priority system attached to it.
    public void myTestEventInvoke(MyTestEvent event) { // this method also HAS to be public
        System.out.println(event.getChangeableValue());
        event.changeValue(111);
        System.out.println(event.getChangeableValue());
    }

    /* MyTestEvent Class */
    @Cancelable
    public class MyTestEvent extends Event {
        private int changeableValue = 0;

        public int getChangeableValue() {
            return changeableValue;
        }

        public void changeValue(int other) {
            this.changeableValue = other;
        }
    }
    
    /* MyTestListener Class */
    @EventInfo(MyTestEvent.class) // has to be here or the EventManager won't be able to use this listener.
    public class MyTestListener extends Listener<MyTestClass> {

        public MyTestListener(MyTestClass parent) {
            super(parent);
        }

        @Listen // this has a priority system attached to it.
        public void myTestEventInvoke(MyTestEvent event/* only 1 parameter */) { // this method has to be public or the EventManager will not be able to invoke it.
            System.out.println(event.getChangeableValue());
            event.changeValue(12);
            System.out.println(event.getChangeableValue());
        }
    }
}
```


[^1]: link to eventmanager
[^2]: 
[^3]:
[^4]:
[^5]:
[^6]:
[^7]: 

[^8]:
