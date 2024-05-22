
```
Network Records define a range of IP addresses.  
  
This helps you assign a risk-based-priority (RBP)vto logs and determine traffic direction.
```

![[Pasted image 20240516122811.png]]

Network Records define segments of your infrastructure (a range of IP addresses) and allow you to define which networks are more important relative to other networks within your company. 

In the example above:

- The "LR Training Network" record has been assigned to the "Primary Site" **Entity** 
- The IP address range begins with 10.6.0.1 and ends with 10.6.0.254. (This is a unique range, network record ranges don't overlap with others in the same Entity.)
- It has been assigned a medium **risk** and medium **threat** level.
- It's **zone** is internal.

Note: Network records must contain a unique IP address range within a single Entity. There cannot be two Networks with overlapping IP addresses within a single Root- or Child- level Entity.

## Additional Details

IP ranges can be defined by department, geography, function, etc. 

Administrators will be able to define the IP groups based on the needs of the business.  This gives you an advantage with being able to discover the Direction of flow from your SIEM.


