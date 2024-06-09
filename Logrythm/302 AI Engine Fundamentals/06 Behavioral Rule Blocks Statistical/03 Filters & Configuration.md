
Because Statistical rules evaluate data over time...

- Configure the filters to monitor specific data. 
- Avoid retaining a large number of logs in memory.
- Avoid wide searches from many different log sources.

![[Pasted image 20240609094253.png]]


## General Practices

As with every AI Engine rule, it is best to examine logs and their populated metadata fields to **determine the most efficient criteria and filters** to apply.

AI Engine recommended practices can be considered while determining selections for criteria and data filters.


## Best Practices

Statistical Rule Blocks evaluate data over a time period as opposed to in real-time. They are configured to collect data for a specified Live Time Period and then evaluate that data.

They should be specifically configured to **only search for data that is critical** to the rule. **Avoid “wide net” searches** from many different Log Sources to prevent retaining many logs in memory.

The Statistical Block, along with all other AI Engine Blocks, contains the standard data filtering tabs. However, unlike most of the AI Engine Rules, which usually evaluate a wide array of log messages in real-time, **the Statistical Rule Block performs a periodic evaluation of the data collected over a defined time period**. 

Therefore, you are cautioned to keep the focus of the data filters narrow to **prevent the Statistical block from retaining many logs in memory during run-time**.

