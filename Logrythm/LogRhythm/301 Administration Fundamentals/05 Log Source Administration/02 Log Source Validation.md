
Validation is an important step to be conducted at the start of log collection. It confirms that timely and accurate log information is available for reference later, if needed.


Once log sources have been onboarded using methods from the previous module, the next step is to validate the information being received from these log sources.

Log source validation involves:

- Ensuring that logs are **being received** as quickly as they are being generated.
- Ensuring that **logs are being accurately parsed** for metadata.

![[Pasted image 20240524163424.png]]


<hr>


## **Log Timestamps**

**After onboarding, the first indicator that a log has been received from a log source is the log timestamp,** located in the Log Sources tab under the column labeled Last Log Message. 

As logs are received, timestamps update to reflect when the last log message from that source occurred.

However, depending on the log source, **time stamps will vary;** it is not uncommon to see displayed times that are hours or even days old. Log generation rates are not identical for every log source. Settings, such as logging level, will produce log generation rates that differ between sources.

For example, you can expect that a log source in VERBOSE will reflect timestamps more frequently than a source that encounters limited or occasional activity.

![[Pasted image 20240524163917.png]]


>[!bug ] Note: 

While a timestamp will indicate that a log has been received, it is not an indicator of parsing accuracy. An Investigation or Tail will provide this result.


