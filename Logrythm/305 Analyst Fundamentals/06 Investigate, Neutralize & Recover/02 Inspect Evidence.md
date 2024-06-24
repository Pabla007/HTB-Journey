
```
Need more information? Run a search.   
Search helps uncover relevant, contextual data and visualize it.
```

![[Pasted image 20240624152434.png]]


## Overlapping Qualification & Investigation

The way I qualified this is not what really ended up being the bigger problem in this case. Sometimes this happens.  
  
We qualified it because somebody was trying to go to Dropbox. This could have been pretty innocent. But after calling Adam, we knew we had to investigate more. The bigger, more suspicious problem we discovered here was that Adam didn't make this attempt. A PowerShell script seems to be doing something malicious.


## Value False Negatives and False Positives

Do you think you would have investigated this further if by coincidence Adam had tried to go to Dropbox at the same time as the script was running? False Negatives are just as import to consider and investigate as False Positives.


## Evaluate Log Collection Practices

Notice how I checked each log message from my search along the way. This goes back to what I said earlier about verifying the facts and evaluating whether everything is getting parsed out. This is about being accurate and continually improving. If I notice something isn't parsed out that should be, then I can contact my Administrator and make improvements that will speed up my process in the future.



## Alarm Suppression

You may have noticed that we had 2 attempts to access Dropbox, but only 1 alarm.  

- This is because the AI Engine rule is set up to do suppression, and therefore trigger only once.  
- If suppression wasn't enabled then you would get multiple alarms telling you the same thing occurred with only two minutes difference in time. 
- It is best practice to enable suppression for multiple events that occur from 1 minute to 60 minutes. This helps reduce alarms and improve the quality of actual alarms to investigate vs. false positives.



## Additional Search Filters

In this case. Our search returned a reasonable number of logs.

However, searches sometimes give you too much information. If this happens, the search page's Widgets and Analyzer Grid may give you ideas for how you might filter your search even more.

For example, instead of searching the whole log message, we could change our search to network deny access, access authentication success, etc.


