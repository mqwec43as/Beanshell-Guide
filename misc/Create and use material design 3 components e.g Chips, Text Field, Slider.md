Tasker introduces Scene V2 and I saw a couple of fields use material design 3.

We can do the same as well via Java code with `com.google.android.material` library! Making it easier to create clean UI than theming manually.

&nbsp;

# [Example code](https://pastebin.com/raw/umXHhXsr)

**Mostly generated with AI.** The code will serve as an example to show the UI. Please read or pass it to LLM after reading the post.

&nbsp;

# [Demo video here.](https://i.imgur.com/KC5tYe8.mp4)
**We could test the example code directly by running the following code via Java code action.**
```java
source(new URL("https://pastebin.com/raw/umXHhXsr"));
```

Example code contains:

1. TextInputLayout,
2. Slider,
3. Switch,
4. Checkbox,
5. Radio,
6. Chips,
7. Navigation Bar,
8. Floating Action Bar.

**The library that Tasker ships is the old material design 3,** not the new expressive one.

&nbsp;

# HOW TO

**To use the material library, we have to set the theme for the context first before creating the component.**
```java
import android.content.Context;
import android.content.res.Resources;

// Function to set the theme for the context

setTheme(Context ctx, String identifier) {
  Resources res = ctx.getResources();
  String pkg = ctx.getPackageName();
  int themeId = res.getIdentifier(identifier, "style", pkg);
  if (themeId != 0) ctx.setTheme(themeId);
}


// Say activity context from tasker.doWithActivity();
import java.util.function.Consumer;
import android.app.Activity;
import android.widget.LinearLayout;

/*──────────────────── Material: Text Fields ────────────────────*/
import com.google.android.material.textfield.TextInputLayout;
import com.google.android.material.textfield.TextInputEditText;

Consumer consumer = new Consumer() {
  accept(Activity activity) {
// Set the theme first with the function above
setTheme(activity, "Theme.Material3.DynamicColors.Dark"); // Light or DayNight
TextInputLayout userLayout = new TextInputLayout(activity);
userLayout.setHint("Username");
// Other codes;
  }
};

tasker.doWithActivity(consumer);
```

&nbsp;

To make it easier, we could write a reusable scripted object like **themeManager** in the example to:
1. Setting the theme.
2. Retrieving color or other attributes.


```java
This tm = themeManager(activity);

// Setting the theme 
tm.setThemeDark();

// Retrieving color token 
int color = tm.attr("colorPrimary");
```

&nbsp;


# REMINDER

Tasker doesn't ship most of the components in the [**library**](https://github.com/material-components/material-components-android/tree/master/lib/java/com/google/android/material), e.g dialog etc. [**Joao said that they will appear once Tasker uses them later in Scene V2.**](https://www.reddit.com/r/tasker/comments/1rs0itz/comment/oaqc4ov)

**Library doc:**  
[https://developer.android.com/reference/com/google/android/material/classes.html](https://developer.android.com/reference/com/google/android/material/classes.html)

**Material design 3 guideline:**  
[https://m3.material.io/components](https://m3.material.io/components)