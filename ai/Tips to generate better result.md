

# Tips on getting better results

While we can ask an LLM anything, the chances of getting working code still entirely depends on our lead. In general, an LLM will perform better when we give it a much clearer context, and we can get the context by:

&nbsp;

### 1. Referencing Working Codes

You can get some examples from:

- **Stack Overflow:** We can easily google this like **"Generate code to call USSD code site:stacksoverflow.com"**
    
- **GitHub Repos:** Needs more work since usually we have to dive deeper to get the right part of the code. However you get better results this way especially if you quote on a working project. E.g., **["termux-api > CameraPhotoAPI"](https://github.com/termux/termux-api/blob/master/app/src/main/java/com/termux/api/apis/CameraPhotoAPI.java#L175C2-L195C69)**
    
&nbsp;

### 2. Quoting the Right API Documentation

This part may seem intimidating but I assure you that we can just ask google right away:

- We can reference to the site e.g., **"camera site:developer.android.com"**
    
- Or ask directly **"which api that we need to use for camera in android"**
    
&nbsp;

### 3. Utilizing Google Search AI Overview and AI mode

This is the simplest method we can use. However most of the time we still have to reference to the right API. E.g., **"I try to use TelephonyManager.UssdResponseCallback and catch USSD request."**

We can copy paste this information to our chat inside ChatGPT's project.

&nbsp;

### Prompt Example

So to put it in a nutshell, instead of just straight up asking a short prompt like this:

```
Create a code to call USSD code and get results
```

&nbsp;

You will have a better response if the prompt looks like this:

```
create script to get ussd result as text without dialog 

*Reference to this discussion on https://stackoverflow.com/questions/47239229/android-ussd-ussdresponsecallback-always-failed

*Copied result form https://www.google.com/search?q=I+try+to+use+TelephonyManager.UssdResponseCallback+and+catch+USSD+request.*
```

&nbsp;

**Remember that this doesn't guarantee that we can get a working code in just one query. We still need to make some exchanges, like supplying the error code and uses better references**