

![[Pasted image 20240529060931.png]]

![[Pasted image 20240529060945.png]]

Lists are managed via the **List Manager** or in the Lists section of the **Administration menu** (see above). The List Manager displays menu buttons, file menu options, and a standard context menu, which provides options to create and manage Lists.

All users have access to the List Manager, which enables users to view, read, create, or retire Lists as long as they have permissions to do so.

Lists are displayed in a searchable data table, allowing for quick filtering through use of the first-row data filters. Viewing and management options are available when right-clicking on the table of Lists.


## **Working with Lists**


![[Pasted image 20240529061221.png]]


**Available List Menu buttons**  (located in the top left of List Manager):
- Refresh
- Create
- Properties

![[Pasted image 20240529061255.png]]



**File Menu options related to Lists:**
- New
- Clone
- Properties
![[Pasted image 20240529061336.png]]


**The context menu includes many standard selections. You can:**
- Create a new List
- Clone an existing List
- Check and uncheck Lists
- Clear the filters of the List
- Activate or Retire Lists via the Actions menu
- Export the List grid to a file
- View active and retired Lists
- Edit the properties of a List

![[Pasted image 20240529061402.png]]



USING WILDCARDS IN LISTS

Lists support the use of wildcard values. Host and User Lists are the most common Lists that utilize this feature. 

SQL-style wildcards are used, which commonly involve the percent (%) symbol to replace zero or more characters.

![[Pasted image 20240529061530.png]]


Lists cannot be removed permanently, but they can be hidden from view and removed from utilization in filters, Alarm Rules, and Reports by retiring the List. 

**Lists can be retired and re-activated.**

![[Pasted image 20240529061645.png]]



## **Expiring Items**

LogRhythm Lists allow individual items to expire. An optional expiration setting removes List items after the configurable amount of time has passed from when the List items were added. 

List Expiring Values allows for reduced management and more accurate filtering for Lists containing content that can become stale, such as Watch Lists of users or hosts. Expiring values also enable the creation of new types of analytics where the content of a List changes.

**Examples:**

- When an employee leaves a company, the newly disabled account should be monitored for any activity for 90 days. After 90 days, monitoring on the account is no longer needed.
- An AI Engine Rule is set up to recognize an abnormal amount of connections from an external IP address. This activity by itself is not concerning but is suspicious. 
    - The AI Engine Rule automatically adds the IP to a List. This List is used by analysts to run daily investigations in order to understand more about any activities related to the IP addresses. After a week, the IP address can automatically be removed from the list using a SmartResponse.
- If a computer is infected by malware and then cleaned, it should be monitored for two weeks. A rule is created to monitor devices for the two weeks after they are cleaned.

**Lists should not contain more than 500,000 items, ideally. The larger the list, the slower the performance when used in AI Engine Rules, etc. Pattern matching will also influence list performance.**


