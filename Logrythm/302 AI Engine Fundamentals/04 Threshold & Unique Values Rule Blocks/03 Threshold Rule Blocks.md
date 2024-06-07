
### Threshold Rule Blocks will monitor for a specific number of related logs to cross a defined threshold within a defined time period.

The Threshold Blocks can be used to find when **the threshold of something exceeds a "normal" condition**. 

Usually for Threshold Rule Blocks, **quantitative** metadata types are an option (e.g. Bytes In/Out, Packets Sent, Size, etc.) because they carry a measurable value.

For example, the Threshold Blocks can be used whenever you would like to know when an amount of data is sent to a server whose job is to service requests, but not to send or receive data.

### **There are three types of Threshold Rule Blocks:**


![[Pasted image 20240607123209.png]]

![[Pasted image 20240607123224.png]]

![[Pasted image 20240607123237.png]]


**Use Case: Web Server Data Transfer**

Why would administrators watch for such a small amount of data to be transferred off of or onto their server ?

The answer to that question lies in what the server's job is. If the server were a mirror for file downloads, this scenario would not be valid. Its normal day-to-day job is to send large amounts of data to requesters (not to mention that large amounts of data must be copied to the server to be made available for downloading).



What if the web server were an e-commerce host ?

In this case, the scenario becomes much more valid. In this case, the web server is responsible for sending HTML source pages, images, and other resources to the requester. (Never underestimate caching, as well; if the visitor has visited the website in the past, even less data is sent to the visitor as it should reside in their local cache!) Usually, the total volume in data sent is very small.

The administrator in this case has identified that 10 MB transferred in a short time period may indicate that there has been some sort of compromise or attack on the web server (such as a SQL Injection attack that is proceeding to download the contents of the back-end database! Or possibly another kind of more traditional attack where an attacker has gained access to the server and is offloading valuable assets).


While this method of monitoring would not be used to directly detect a SQL Injection (for example), it is valid in alerting analysts that abnormal activity is taking place.


