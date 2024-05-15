
```
Want to easily update your Agent version? 

The System Monitor Package Manager enables you to schedule automatic or on-demand software updates for multiple System Monitor Agents at one time.
```


**1.** **From LogRhythm Community, download the package manager for the version of the Agent you want.** Packages can be downloaded from LogRhythm Community (see image to the right). Packages for both Windows and Linux Agents are available.

To get to SysMon downloads on Community:

Community > Documents & Downloads > SysMon > SysMon Downloads > select Version of SIEM/SysMon.

![[Pasted image 20240515145238.png]]


**2.** **Load the update package to the LogRhythm Client Console**, and then schedule it to be applied now or at a future date and time. 

Available Package Managers in LogRhythm Community

**3.** When the System Monitors receive the package, they shut down, update, and then restart automatically. 


>[! Bug] Note: Upgrading a System Monitor Agent requires that pre-requisites be met before an upgrade is successful, i.e. .NET requirements. 

A .NET 4.7.2 upgrade may require a reboot (so consider planning this for a time that doesn't disrupt business!)

![[Pasted image 20240515145351.png]]


