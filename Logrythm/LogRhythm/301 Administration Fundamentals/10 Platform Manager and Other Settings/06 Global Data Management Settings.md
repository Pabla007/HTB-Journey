
Global Data Management Profiles determine how LogRhythm will perform.

![[Pasted image 20240531114232.png]]

## Global Data Management Settings

- Located in the Platform Manager tab. Allows you to specify the options for log data storage.
- Changing these settings will affect archiving, indexing, and Event generation at the Global Level (all Log Sources).


## Data Management Profile

**Simplify configuration based on your deployment's data management model.** 

- You have the option to manage these settings at a granular level. 
- Data Management Profiles are packaged, by default, into configurations that support common deployment models and uses of the LogRhythm Platform.


## Collection Optimized Profile

Select this profile to **optimize** the settings  for collecting and processing data at the **highest rate** possible:

- With this profile all data will be Archived.
- Only Event data will be Indexed for the  fastest search.



## Search Optimized Profile

Select this profile to **optimize** the LogRhythm Platform for the fastest access to **all data** when searching:

- With this profile all data will be Archived.
- All data will be Indexed for the fastest search.


## Search Optimized Profile

Select this profile to **optimize** the LogRhythm Platform for the fastest access to **all data** when searching:

- With this profile all data will be Archived.
- All data will be Indexed for the fastest search.


## Custom Profile

Select this profile to enable all the data management setting options so that you can **customize** **and** **configure** each one individually to specifically meet the needs of your organization.


## Classification Based Data Management (CBDM) Settings

![[Pasted image 20240531115314.png]]

CBDM settings are automatically configured, based on the Data Management Profile selected at the time of installation. 

Every Classification has settings that determine where logs assigned to that Classification are stored (Archive, Indexed).

These settings will **override** the settings configured at the Data Processor, Log Source, and MPE Policy levels.

