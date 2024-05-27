
```
At this point, a comparison can be made between the MaxMessageCount value at the log source level and the Read entries within the Agent log.
```

![[Pasted image 20240528015732.png]]

If the read entries continuously meet the MaxMessageCount value, this translates to the Agent collecting the maximum number of logs from this log source during each cycle and the likelihood that the log source is generating more than 100 logs in that cycle.

Ordinarily, a MaxMessageCount value of 100 would suffice for most log sources in an environment. However, due to the continually high activity of this log source, **the Agent is unable to collect logs at the rate of generation and, as a result, is gradually falling behind.**

**Based on these findings...** A possible troubleshooting step **c****an be to increase the MaxMessageCount value from 100 to a higher number, either on a temporary basis or permanently.**

Note: Increasing MaxMessageCount is not a ‘be all end all’ solution. If you do this for every log source, you may do more harm than good.


>[! bug] ****Important!** 
>

>MaxMessageCount adjustments should only be conducted when necessary and under the guidance and instruction of Professional Services or LogRhythm Support. A negative impact to performance may result.**

