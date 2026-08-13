The latest beta introduce methods to run shell command with root, shizuku, adbwifi and default one.

**Now with this we can create one function for all run shell action!**
```java
import com.joaomgcd.taskerm.shell.CommandResult;
import com.joaomgcd.taskerm.action.java.JavacommandException;

public CommandResult runShell(String command, int timeout) {
	int NONE = 0;
	int ROOT = 1;
	int SHIZUKU = 2;
	int ADBW = 3;
	boolean hasRoot = tasker.isRootAvailable();
	boolean hasShizuku = tasker.isShizukuAvailable();
	boolean hasAdbWifi = tasker.isAdbWifiAvailable();
	int[] order = { ROOT, SHIZUKU, ADBW, NONE };

	for (int method: order) {

		if (method == NONE) {
			return tasker.runShell(command, timeout);
		}

		else if (method == ROOT && hasRoot) {
			return tasker.runShellRoot(command, timeout);
		}

		else if (method == SHIZUKU && hasShizuku) {
			return tasker.runShellShizuku(command, timeout);
		}

		else if (method == ADBW && hasAdbWifi) {
			return tasker.runShellAdbWifi(command, timeout);
		}
	}
}

public CommandResult runShell(String command) {
	return runShell(command, 30);
}
```

&nbsp;

To make this easier, you can store the script into global variable or create a task. Or store this to a file.
