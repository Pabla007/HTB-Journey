Antivirus Evasion: 
It's a constant dance b/w hackers and developers.

AV evasion have two primary types:
- On-Disk Evasion 
Is when we try to get a file saved on the target than executed (.exe file)

- In-Memory Evasion 
Is when we try to import a script directly into memory execute it there.
So to overcome that Microsoft implemented a feature called AMSI.

If we already have a shell we can use programs such as SharpEDRChecker and Seatbelt to identify the antivirus solution installed.
So once we know the OS version and AV of the target we can replicate the environment in a virtual machine which we can use to test payloads against.

