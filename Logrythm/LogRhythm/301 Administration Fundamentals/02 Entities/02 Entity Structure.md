
```
Entities are containers that logically group assets (network and host records).
```


**Entities are important because they:**

- **Help you stay organized.**  
    Entities are containers that organize network and entity records. These containers start broad, but you can make them more specific:   
    Global entity > Parent/Root entity > Child entity.
- **Allow you to grant permissions by location, department, or role.** For example, someone in Denver Sales likely does not need access to London IT. LogRhythm suggests granting only the minimum access and permissions that someone needs to do their job.
- **Help you assign risk levels.**  
    The IT department likely has a higher risk than Marketing. If a bad actor gained access to credentials from someone in IT, they could likely inflict a lot of damage.
- **Help you quickly understand direction.** Is a problem **originating** from within your organization or outside of it? What location is being **impacted**?

To see your entity structure, go to the Client Console > Deployment Manager > Entities tab.

![[Pasted image 20240516110123.png | 400]]
In this example, we have:

- **Global entity**
    - The **Parent Entity** is the company name  
        (Bumble Bee Toy Emporium)
        - The **Child Entities** are divided by location and department.



## Naming Child Entities

It is helpful to fully label Child Entities. 

- For example, your Parent Entities might be organized by city, and each city might contain an IT department (child entity). 
    - In that case, it would be important to label each Child Entity with the parent's name: "Denver - IT" and "London - IT" 
    - Otherwise, you might see a vague log that says there is a problem in the IT Child Entity... but it wouldn't be immediately apparent whether it was from Denver IT or London IT!


## Entities &. Organizational Units

In some ways, entities can be compared to Active Directory (AD), Organizational Units (OUs) since you can create OUs for locations, departments, user types, etc.


