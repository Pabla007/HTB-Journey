
## Whitelist Rule Blocks will “learn” normal activity, then monitor behavior based on this saved set of data.

Whitelist Rules consist of a _Profile_ block, responsible for creating the whitelist and establishing approved log activity data, and a _Monitor_ block, which monitors live data against the whitelist. 

An example of a Whitelist use case may be a scenario where communications or protocols not previously observed or present in an approved whitelist would generate a notification or alarm.


<hr>

## Whitelist Rules employ a different approach to the Group By selection process

Selections are made based on the desired contents of the whitelist. 

As an example, if a whitelist is to contain an approved set of _User (Origin)_ and _Host (Impacted)_ values, these are the metadata fields to be selected in the _Group By_ tab.

<hr>

## Each Behavioral Rule Block includes time setting options to apply during their configuration.

The Whitelist Rule Block has a _Collection Interval_ setting in the Profile tab that determines how long the rule block will record behavioral data to be included in the Whitelist. 

Time settings for Behavioral Rules should be tuned in order to balance between rule effectiveness and system resource availability.

<hr>

