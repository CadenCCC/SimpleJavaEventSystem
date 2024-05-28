# Java Event System
This is a basic proof of concept. How you use it is up to you.
Zero updates will be given to this repo unless a problem happens with new Java versions or someone points out a problem to me.

# How to Use
In order to use we need to invoke the `EventManager`.
If you are using a `Listener` or using the `Subscribe` annotation, 
you're going to need to have an `Event`.

```java 
import net.nerites.event.manager.EventManager;

public class MyTestClass {
    EventManager EVENT_BUS = new EventManager();
}
```

Creating an `Event` is super easy, you can use the `Cancelable` annotation to give it the possibility to be canceled.
if `Cancelable` is not present, the event will become uncancelable.

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

Creating a `Listener` is just as easy, you can do this by just creating a **class** and extending `Listener`
and adding the annotation `EventInfo`. Adding that annotation is important because the `Listener` will not work without it as it needs to be there to identify the `Event`.
It is also important to put your parent in the `Listener` as it allows it to access the parent.
When the `Listener` is sent to the `EventManager` it looks for `Listen`, which it uses the **method** that is connected with that annotation and invokes it.

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

Using the `Subscribe` is pretty simple as well, you need the `EventManager` to use the **subscribe** method on the **class** you have the method with the `Subscribe` annotation in.
Using the **subscribe** method in the same class as any method with the `Subscribe` annotation, and an `Event` for it's **only parameter**.
Will allow the `EventManager` to put it in its map.

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

<details>

<summary>All Test Code</summary>

## All Test Code

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
</details>
