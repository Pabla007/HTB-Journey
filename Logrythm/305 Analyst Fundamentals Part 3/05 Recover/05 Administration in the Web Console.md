
```
Analysts can use some, but not all, features in the Administration Dropdown related to Contextualize Actions, Lists, and Playbooks.
```


Even though it is called Administration, those of us with Analyst permissions can still access four sections in this dropdown (if we've been given these role-based permissions).  
  
**At this point I feel pretty confident that you can do some exploring on your own.** I'll just call out a few features, and let you dig deeper into this on your own time. Remember, LogRhythm Docs is a great resource!




## Prefer to read Raheema's Steps? Click here!

- Click Contextualize Actions from the Administration icon's dropdown menu.
- If you click **New Contextualize Action** the Inspector panel will open. 
- In a separate browser tab, **go to logrhythm.community.com** **and** **search "Contextualize Action Configurations"** to find an article listing known contextualize action configurations.
- Use the listed information to fill in the Inspector panel's required details, such as the "URL Path" and the "Fields" dropdown
    - "Field" indicates which information can be pivoted upon when you want to run your new Contextualize Action.
- Don't forget to update the permissions, and then Save.

**Now that you've configured your new Contextualize Action,** when you pivot on the specified Field in the Analyzer grid, an "Additional Contextualize Actions" section will appear in the Inspector panel. 

- Simply selecting the Action and clicking "Go" will open a new browser tab. It will show you the information that the 3rd party found in relation to your search term.





## **SecondLook **- Create & Run SecondLook Searches****

You can use SecondLook to easily pull archived data back into the Web Console to be utilized for Reports, Audits, or any other tasks related to stored log data.

Note: to use SecondLook in the Web Console you will need:

- An Administrator to have configured and enabled SecondLook for the Web Console.

- To have been granted access, with appropriate role-based permissions.

Watch how to create and run a new SecondLook Search from within the Web Console:





**To access SecondLook in the Web Console & Create a New Search:** 

- Select the **Administration button** from the top right of the Web Console
- Select **SecondLook**.
- Select the **New SecondLook Search** button from the top right of the Saved Searches tab of the SecondLook page.

**Configure the search criteria (of the logs that need to be restored:** 

- Select your desired time frame, log source filter, and search filters. (It is important to be as specific as possible in order to reduce the runtime of the SecondLook search).
- You also have the following options in the Properties pane:
    - Name: Provide a name for the search to be saved and displayed on the Executed Searches tab. It is not necessary that the name must be unique.
    - **Select Log Repositories**: Allows users to select the exact repository to which the logs need to be restored.
    - Specify Recovery Settings:
        - Maximum log messages to recover
        - Entity
        - Read Permission
        - Write Permission
    - **Disable Data Masking for Restore** - Personally Identifiable Information (PII), in which information will be masked when restored from the archive file.
    - Description - Enter a description to describe what this search is about.
    - Select **Save.** Once saved, the newly-created search will appear on the Saved Searches tab of the SecondLook page.

**Run the SecondLook Search that you just created:** 

- Select the **Play icon** next to your saved SecondLook Search to run it.
- Select the **Executed Searches tab** from the top left.
- Once the search's **Status** is "Completed" you can hover over the **Messages field** to see a preview of the restored data.
- To see the logs themselves, select the **Drilldown icon**.
- Once loaded, selected the search card to see the logs on the Analyze page.


