
```
Once a time stamp has been displayed (though not necessarily a prerequisite), an Investigation or a Tail can be launched to examine how logs are being processed. Both are accessible within the Client Console and have their own buttons in the top bar.
```

## **Definition:** 

Investigations are the search mechanism within the Client Console and allow a search to be conducted against specific windows of time and various criteria, such as Classifications, Common Events, Log Sources, etc.

  
## **Location:**

Launch them from the Investigate button (located in the top bar of the Client Console), and an option to run a new or saved Investigation will be presented.

- Note: Saved Investigations provide a faster way of launching an investigation (by allowing you to preload search criteria).

![[Pasted image 20240524172749.png]]


## **Types of Investigations:**
  
Investigations offer a search option to specify the data repository to search against. Types include:

- **Platform Manager Search:** This type of search queries Events only. If a search should include Events and omit non-Events from the results, a search against the Platform Manager may be conducted.
- **Data Processor Search:** This type of search queries available Data Processors for any indexed logs, regardless of Event status. This search type is more common, as Event status does not play a factor and any logs of interest are returned.
- **LogMart Search:** This search option has been deprecated and is no longer recommended for searching.

**The following time specifications can be selected for an Investigation:**

- In the Last number of minutes, hours, days, or months
- Date is Before a specific date and time
- Date is After a specific date and time
- Date is Between two date and time selections
- Note: Selected dates and times do not guarantee log results. Results are dependent on log availability, based on Time-to-Live (TTL). For example, if a search is performed against the Data Processor but the selected date has surpassed the TTL of indexed data, search results will not be returned.
- **Log Sources to Query** offers the option to narrow a search scope to specific log sources. Narrowing the scope to applicable log sources only can reduce the time needed to return results. Available search query options include:
    - **All Available Log Sources:** Any registered log sources within the LogRhythm platform will be queried.
    - **Selected Log Source Lists:** A search will be performed against any selected log source lists, either created or made available from a Knowledge Base module import.
    - **Selected Log Sources:** A search will be performed against specifically selected log sources.



In the **Specify Event Selection window,** one or more metadata fields can be selected as part of the log search criteria. 

- For example, a Common Event of User Logon combined with a specific User (Origin) will perform a search for user logon activity generated by a user. 
- Metadata fields can be selected from the Add New Field Filter dropdown menu and clicking the Edit Values button will allow for defining populated values for selected metadata fields.


![[Pasted image 20240524190108.png]]



The last window of an Investigation presents the option to **save an Investigation for future use, launch an Investigation, or both.** If saved, name the investigation, and select read and write permissions from the available drop-down menus. To launch the investigation, click Next or Launch.

- Once launched, the Investigation will populate log results based on the search criteria and the availability of logs. It will display aggregate values within the Log/Event Analyzer tab, which allows for drilling down on groupings of logs.

**The Log Viewer tab** will display individual log messages and allows for filtering across populated metadata field columns. Double-clicking on a line item opens the Log Information window, displaying the raw log message and any metadata parsed by the MPE.

![[Pasted image 20240524190706.png]]

