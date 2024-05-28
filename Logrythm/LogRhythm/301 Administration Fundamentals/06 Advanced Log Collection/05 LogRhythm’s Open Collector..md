
Let’s look at the fundamentals of Docker, which is the foundational technology of LogRhythm’s Open Collector.

**Access to the internet is required for Open Collector to work.**

However, once you have pulled down the images, you can copy them over to a host OS without internet connectivity.

Open Collector receives the output of a beat and then normalizes it to the LogRhythm schema:

1. Once Open Collector is installed, it's getting the information from the individual beats.
2. It transforms that and then sends it to the System Monitor Agent as a Log Source.
3. From there, it can be sent to the data processor for normal processing.

![[Pasted image 20240529034359.png]]


Open Collector currently requires outbound internet access to Github and grc.io. It is possible to configure a proxy for internet connections. Without internet connectivity, it is currently impossible to install Open Collector.

The below ports **must be open** to install Open Collector. Once installed, these ports can be closed. However, please note that updates will not be possible.

Docker uses the host Firewall for NAT rules and must be running for Docker to work.

![[Pasted image 20240529034522.png]]


Open Collector containers (running images) can be monitored via the command line or via LogRhythm’s centralized metrics.

The commands to monitor Open Collector are as follows:

- ./lrctl open collector status (or ./lrctl oc status) 
- ./lrctl metrics status

![[Pasted image 20240529034638.png]]




