
## **#1 Extract Tasker AI Instruction from Java Code Action**

First, we need to **extract Tasker's AI instruction** and save it into a file. We can do this by following these steps:

1. Inside any task, add a new **Java Code** action.  
2. **Click the magnifying glass/search icon** that is inline with the word "Code". 
3. Click **Copy System Instructions**.
4. **Save as file**.

&nbsp;

The instruction should have this section:

```
# Code Modification Rules
If the user's request is to **modify, change, add to, or fix** the existing code, you MUST use the following code block as your starting point and apply the requested changes. If the user is asking for entirely new code, you should ignore this section.

**Existing Code to Modify:**
\```

\```
Your final output MUST be the entire, complete, and modified script. Do not output only the changed lines.
```

&nbsp;

You can edit this however you like. However, I personally edit the later part to this:

```
# Code Modification Rules
If the user's request is to **modify, change, add to, or fix** the existing code, YOU MUST USE THE LATEST CODE IN THE CONVERSATION AND APPLY THE REQUESTED CHANGES. If the user is asking for entirely new code, you should ignore this section.

Your final output MUST be the entire, complete, and modified script. Do not output only the changed lines.
```

#### **[My custom instruction can be found here.](/AI%20Instructions.md)**

&nbsp;

# #2 Use AI Platform
We have two options to use the intruction file, ChatGPT project or Gemini Gem.

&nbsp;

## **ChatGPT Project**

1. Go to their site or their app, then create an account if you don't have one.
2. Click **New project** in the sidebar. 
   1. If you're on mobile, you can access the side bar by clicking the double line icon on the top left side.
   2. If you have already a project, hover on the project tab and click the plus button.
3. Give it a **name** and set the memory to project only memory.
4. Click **Create Project**.
6. In your newly created project, Click **Sources**.
7. Then **upload the saved instruction file** as source.
8. **Open a new chat.**
    

&nbsp;

## **Gemini Gem**

1. Go to the Gemini site/app and **sign in** with your Google account.
2. In the left sidebar, click **Gem**.
3. Create Gem.
   1. Go down to Gem Manager (Not gem from labs), and **click Create Gem**.
   2. Or click this link. https://gemini.google.com/u/1/gems/create
4. Fill in the **Name** (e.g., "Tasker Code Generator") and generate a custom **icon**.
5. In the **Instructions** box, clearly define its role (e.g., "You are an expert Tasker Java code generator that uses this URL for reference: https://tasker.joaoapps.com/userguide/en/help/ah_java_code.html.
6. Under **Knowledge**, click **Upload files** to give it the saved instruction file.
7. Click **Create**.
8. **Open a new chat**.

&nbsp;

> [!WARNING]
> If there's an update about Java code, we may need to redo the steps above to make sure it matches Tasker's internal instruction.
