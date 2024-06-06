
### **Group By fields are parsed metadata fields available for selection within each rule block that allow for establishing rule block relationships within a rule.** 

Group By selections directly affect the triggering capability of an AIE Rule. This relationship is a way for metadata values from one block to be examined by a successive block. Remember, **you want the** **AIE Rule to compare similar data in logs**. For example, to identify activity from the same user or same host.

**While Group By selections automatically become AIE Summary Fields, additional fields can be selected as needed without affecting the functionality of an AIE Rule.**


![[Pasted image 20240607033855.png]]

Present within each rule block type, Group By selections **place emphasis on specific metadata fields** to be used for actions such as correlation or Smartresponse.


**The Group By tab is used to establish a relationship of data between rule blocks,** but this is not its only function.

A Group By selection is **required** for every rule block in an AIE Rule, even when the rule only utilizes one block. The reason for this is that, as a log meets rule block criteria, it is often necessary to group logs by a specific metadata field in order to establish a commonality between logs.


**Consider the following scenarios rule blocks being used:**

SCENARIO: TWO RULE BLOCKS

**A rule is built to detect multiple authentication failures by a user,** **followed by an authentication success.**

- This rule uses two rule blocks, one to detect multiple authentication failures, one to detect an authentication success based on previous failed attempts by the same user. 
- The logs are being grouped by a User (Origin) who is conducting the authentication activity, and to emphasize the relationship of data between rule blocks, the User (Origin) metadata values are passed from the first rule block to the second.



SCENARIO: ONE RULE BLOCK

**A rule is built to detect when 3 account lockouts due to failed password attempts by one user occur within 2 minutes.**

- This is a single block rule (a Threshold rule – covered in a later module), but the rule still needs a way to group logs by the User (Origin) who is generating the lockout activity. 
- It is often easier to visualize the function of Group By values when describing them to establish a relationship of data between rule blocks. However, even if a rule being built only uses one block, it may help to consider what the overall purpose of the rule is.   
    

In other words, if a rule is essentially centered around User (Origin) activity or Host (Impacted) activity, this provides a starting point to determine which Group By selections would be most effective.



**When deciding which Group By selections to make, consider the overall purpose of the rule and commonality between the logs to be detected.**

For example, if the rule is meant to capture User-generated behavior, selecting _**User (Origin)**_ may be the appropriate choice.

Choosing a Group By that does not appear in the metadata will mean the AI Engine rule will not trigger as is it doesn’t meet its criteria. If in doubt use Group By fields that always appear in the Metadata rather than occasional metadata fields.

