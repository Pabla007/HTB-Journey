eyJpdiI6IlRhVlBYZElaT3V2YzJSbU83RzJVa1E9PSIsInZhbHVlIjoiakF1MlZGaGpsQWFmSzcwTG1nXC9PNVBXUEpBT1FhVEVVWmhDa1pzZkREZUhIUEE3SGp5XC8zTEFkTGpuOWtXRXBnUVVMbUNiSWk1MjRjME10dnZmOUdVZmU1blRIcVAzSjVrNmhQdGY5UVB5MnpaN3pGekxQZXJ2UzBOeGFxMFwvME1tTWlTQ0ZqNWlSWXlXcGw5Sys5ZnI5QVkwOHhVbjM1TjAwM2FtcTJvYUgyNkpxY1liSkRBY0pcLzFra21KQW5laGl2QitiRHU4UzczNFo1bEpZN0lodjN6NHVkaU1VdVwvVXVOaGNvZUdVMzZcL3kySjZhNDJPNTNvVlRrc2VNRzI0M1ZNSVlDNXFtVGU3dFpxQUZDcE9TazZ3amNsTFhnR0FOMDFwejBqWE54RnJuNVJFVE1qQ2RTYXNreUFMUld0WTFlNjZzYW1GRisrYWRxTU5yRlY1VnI0SzU2cGwrY0srK1VFVjRMNDllZFBTc1dQb0dsZDh2ZFhoWHRLcnRCSDlncXVpK0pQemdxbU9IcnMwblBaWWpBNWFsbnJrb1NpeEE3bUVQUjJNcVNzWDdpbjMzUytGR0lcLzl2TmdacnY0OW9RdTVOM1VCNWp1S3Qrd2c1NmFPeTJINUdHQUNaTzZXYUR5MmpuZ2hnSXZTNFVmV0JScVRRTzI5TFwvVDBFYUI0VGpmd3B6RlBhYnlSNWlQUFNiUkJHYTVuK2ZqSUk3OFh6QzRiaE9ybU5RemM9IiwibWFjIjoiYTA3YTljZTY5ZDZhNjY1YTY3YzI3ZjNkNjExZmVhZTlmOGY5ODdmZjBkOWU2NGIxOTk2M2U0ZDM3ODg5MjI0MiJ9

![[Pasted image 20230810050225.png]]


![[Pasted image 20230810050413.png]]
`Command : echo -n <data>  base64 -d | sed 's/,/\r\n/g'`


**Will analyze the value** 
![[Pasted image 20230810050816.png]]

![[Pasted image 20230810050927.png]]

As the entropy value is almost 8 bits per byte it could be encrypted based on the application Key.

Let's see how Laravel does encryption.
Laravel's encryption services provide a simple, convenient interface for encrypting and decrypting text via OpenSSL using AES-256 and AES-128 encryption.

All encrypted values are encrypted using OpenSSL and the AES-256-CBC cipher.
Will open CyberChef and select Aes decrypt
https://gchq.github.io/CyberChef/

IV  `TaVPXdIZOuvc2RmO7G2UkQ==`
Key `dBLUaMuZz7Iq06XtL/Xnz/90Ejq+DEEynggqubHWFj0=`
Input`jAu2VFhjlAafK70Lmg\/O5PWPJAOQaTEUZhCkZsfDDeHHPA7Hjy\/3LAdLjn9kWEpgQULmCbIi524c0Mtvvf9GUfe5nTHqP3J5k6hPtf9QPy2zZ7zFzLPervS0Nxaq0\/0MmMiSCFj5iRYyWpl9K+9fr9AY08xUn35N003amq2oaH26JqcYbJDAcJ\/1kkmJAnehivB+bDu8S734Z5lJY7Ihv3z4udiMUu\/UuNhcoeGU36\/y2J6a42O53oVTkseMG243VMIYC5qmTe7tZqAFCpOSk6wjclLXgGAN01pz0jXNxFrn5RETMjCdSaskyALRWtY1e66samFF++adqMNrFV5Vr4K56pl+cK++UEV4L49edPSsWPoGld8vdXhXtKrtBH9gqui+JPzgqmOHrs0nPZYjA5alnrkoSixA7mEPR2MqSsX7in33S+FGI\/9vNgZrv49oQu5N3UB5juKt+wg56aOy2H5GGACZO6WaDy2jnghgIvS4UfWBRqTQO29L\/T0EaB4TjfwpzFPabyR5iPPSbRBGa5n+fjII78XzC4bhOrmNQzc=`

Will select From base64 and put it above the aes decrypt and simply change the key to base64
![[Pasted image 20230810053628.png]]

It's doing PHP serialized Object
` PHP Object Injection is an application level vulnerability that could allow an attacker to perform different kinds of malicious attacks, such as Code Injection, SQL Injection, Path Traversal and Application Denial of Service, depending on the context.`

https://www.youtube.com/watch?v=HaW15aMzBUM&t=1640s

