***All contents from the post is available in the*** [***beanshell documentation here***](https://beanshell.org/manual/bshmanual.html#Table_of_Contents)***.***

&nbsp;

# source()

`source()` will evaluate the string stored in a path or link. Any extension works as long as it's a plain text.

Say, we store this part inside a file called **/storage/emulated/0/Tasker/my\_script.java**
```java
String text = "Hello World!";
void toast(String text) {
   	tasker.showToast(text);
}
```

&nbsp;

Then we can use them inside Java code action like this.

```java
String example = "example";
source("/storage/emulated/0/Tasker/my_script.java");
toast(text);
```

It works the other way around too, so anything before `source()` will be available.

&nbsp;

We can also upload the file somewhere. And call it like this.
```java
URL url = new URL("direct url that returns text");
source(url);
```

&nbsp;

# addClassPath() and importCommands()

This is more advanced approach. This is used to store a function or scripted method instead.

&nbsp;

Say We have this script.
```java
void toast(String text) {
	tasker.showToast(text);
}
```

It has a variable text and a function called toast().

&nbsp;

We have to name the file the same name as the function we want to refer, and use .bsh as the extention. So the name should be `toast.bsh`

&nbsp;

Say we store it at **/storage/emulated/0/Tasker/toast.bsh**. We have to use it like this.
```java
addClassPath("/storage/emulated/0/Tasker");
importCommands(".");

String text = "text";
toast(text);
```

&nbsp;

We can also use `cd()` as well to change working directory;
```java
cd("/storage/emulated/0/Tasker");
addClassPath(".");
importCommands(".");
```

&nbsp;

You can also call the subfolder as well, say we have this tree.

```bash
/storage/emulated/0/Files/Github/Android/Java
├── AccessibilityAction
│   ├── main
│   ├── others
│   └── trash
├── Dialog
│   ├── confirmDialog.bsh
│   └── pickDirectory.bsh
├── GistManager
│   └── GistManager.java
└── import.java
```

&nbsp;

We can make the function available inside other folder like this

```java
addClassPath("/storage/emulated/0/Files/Github/Android/Java");
importCommands("AccessibilityAction/main");
importCommands("AccessibilityAction.gestures");
importCommands("dialog");
```