# Scripted Objects
In BeanShell, methods can act like closures by returning `this`. This creates a scripted object with captured variables and nested methods.

Example:
```java
foo() {
    print("foo");
    x = 5;

    bar() {
        print("bar");
    }

    return this;
}
```
Usage:
```java
myfoo = foo();
print(myfoo.x);
myfoo.bar();
```

# Commands
BeanShell commands are scripted methods or compiled Java classes loaded from the classpath. The command file name must match the command name. Import commands with `importCommands()` after adding the path.

Example:
```java
// File: helloWorld.bsh
helloWorld() {
    print("Hello World!");
}
```

Add the path then import:
```java
addClassPath("/home/pat");
importCommands("/mycommands");
```
`importCommands()` accepts resource paths or package names. Relative paths are normalized by prepending `/`. Importing `/` loads loose commands from the top of the classpath. Imports are scoped and later imports override earlier ones.

Overloaded commands are allowed:
```java
helloWorld() { print("Hello World!"); }
helloWorld(String msg) { print("Hello World: " + msg); }
```

# setNameSpace
Use `setNameSpace(this.caller.namespace)` to make a command run in the caller's namespace.

Example:
```java
myCommand() {
    setNameSpace(this.caller.namespace);
    // work in caller namespace
}
```

You can switch to any object namespace and then restore the original one.

# addClassPath
`void addClassPath(string | URL)` adds a directory or JAR to the classpath.

Example:
```java
addClassPath("/home/pat/java/classes");
addClassPath("/home/pat/java/mystuff.jar");
addClassPath(new URL("http://myserver/~pat/somebeans.jar"));
```

# cp
`cp(String fromFile, String toFile)` copies a file like Unix `cp`.

# debug
`debug()` toggles debug mode.

# desktop
`void desktop()` starts the BeanShell GUI desktop.

# dirname
`String dirname(String pathname)` returns the directory portion of a path. Use `pathToFile(getSourceFileInfo()).getAbsolutePath()` to localize relative paths.

Example:
```java
path = pathToFile(getSourceFileInfo()).getAbsolutePath();
cd(dirname(path));
```

# eval
`Object eval(String expression)` evaluates a string in the current namespace and returns the result.

Example:
```java
a = 5;
eval("b = a * 2");
print(b);
```
Exceptions are returned as `bsh.EvalError`, including parse errors and target exceptions.

Custom eval that throws target exceptions directly:
```java
myEval(String expression) {
    try {
        return eval(expression);
    } catch (TargetError e) {
        throw e.getTarget();
    }
}
```

# extend
`This extend(This object)` creates a child object whose namespace inherits from a parent.

Example:
```java
foo = object();
bar = extend(foo);
```

# getBshPrompt
`String getBshPrompt()` returns the prompt string, default `bsh % `. You can override it in your namespace.

Example:
```java
String getBshPrompt() {
    return bsh.cwd + " % ";
}
```

# getClass
`Class getClass(String name)` loads a class using the current imports and classloader. It is like `Class.forName()` but uses BeanShell class manager state.

# getClassPath
`URL[] getClassPath()` returns the current classpath, including user and bootstrap entries.

# getResource
`URL getResource(String path)` loads a resource from the BeanShell classpath.

# getSourceFileInfo
`getSourceFileInfo()` returns the source file currently being interpreted.

# importCommands
`void importCommands(resource path | package name)` imports scripted or compiled commands.

Example:
```java
importCommands("/bsh/commands");
importCommands("bsh.commands");
```

# object
`This object()` returns an empty BeanShell object for storing fields.

Example:
```java
myStuff = object();
myStuff.foo = 42;
myStuff.bar = "blah";
```

# pathToFile
`File pathToFile(String filename)` resolves a filename relative to BeanShell's current working directory.

# reloadClasses
`void reloadClasses([package name])` reloads a class, package, or all classes.

Examples:
```java
reloadClasses();
reloadClasses("mypackage.*");
reloadClasses(".*");
reloadClasses("mypackage.MyClass");
```

# run
`run(String filename, Object runArgument)` executes a command in a private child namespace and returns that context.

# save
`void save(Object obj, String filename)` saves a serializable Java object.

# setClassPath
`void setClassPath(URL[])` replaces the classpath with the specified array.

# setNameSpace
`setNameSpace(ns)` switches the current namespace.

# source
`Object source(String filename)` and `Object source(URL url)` load scripts into the current namespace.

# sourceRelative
`sourceRelative(String file)` loads a file relative to the caller.

# super
`This super(String scopename)` returns a reference to an enclosing scope.

Example:
```java
foo() {
    x = 1;
    bar() {
        x = 2;
        gee() {
            x = 3;
            print(x);
            print(super.x);
            print(super("foo").x);
        }
    }
}
```

# unset
`void unset(String name)` undefines a variable so it becomes `void`.
