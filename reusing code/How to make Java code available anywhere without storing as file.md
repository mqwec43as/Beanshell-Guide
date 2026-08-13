**We can do this by storing scripted object and make them as global java variable.**

What is **[Scripted Object](https://beanshell.org/manual/objects.html)**? To put it simply, it's a java variable that contains another variables and functions as well. 

This is an example of scripted object.

```java
import bsh.This;
This myObject() {
	String TEXT = "hello!";
	hello() {
		String hello = "Hello World!";
		tasker.showToast(hello);
		return hello;
	}
	return this;
};

This test = myObject();
tasker.setJavaVariable("myObject", test);
```

&nbsp;

By setting them as global java variables, we can now access them anywhere like this.

```java
myObject.hello();
myObject.TEXT;
```

&nbsp;

However it may not be convenient since we still need to write the variable first. We can work this around by using **[setNameSpace()](https://beanshell.org/manual/bshmanual.html#setNameSpace\(\))** to the caller name space.

```java
import bsh.This;

This myObject() {
	void call() {
		setNameSpace(this.caller.namespace);
		String TEXT = "hello!";
		hello() {
			String hello = "Hello World!";
			tasker.showToast(hello);
			return hello;
		}
	}
	return this;
};

This test = myObject();
tasker.setJavaVariable("myObject", test);
```

&nbsp;

Then we can use hello() directly like this.
```
myObject.call();

hello();
return TEXT;
```

&nbsp;

Now we can call use our codes from any instance of Java code action!

&nbsp;

# The Catch
The catch here is that we have to make sure that our global java variables is always available. 
It won't be a big deal as long as we manage their lifecycle.

Personally, I always initiate the code above with Tasker > Monitor Start event.

&nbsp;

# Example
Calling [my accessibility project here](https://github.com/mqwec43as/AccessibilityAction/blob/main/code/a11Y.java) to write UI macros easily.

```java
import bsh.This;
This a11y() {
	void set() {
		setNameSpace(this.caller.namespace);
		source(tasker.getVariable("ImportJava"));
		IMPORT("AccessibilityAction");
	}
	return this;
};

This a11y = a11y();
tasker.setJavaVariable("a11Y", a11y);
```

&nbsp;

In Java code action.
```java
a11y.set();

click("Add");
click("Perform Task");
```