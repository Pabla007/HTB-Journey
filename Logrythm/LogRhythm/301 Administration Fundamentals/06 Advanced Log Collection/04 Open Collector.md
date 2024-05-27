
The Open Collector brings modern logs, usually in JSON format, from cloud log sources, flat file, or other formats, into the LogRhythm SIEM. It is designed for easy mapping of JSON fields to the LogRhythm Schema.

Open Collector uses `Elastic Beats` to grab the data from the device and pass it along to the Open Collector, where the normalization takes place. Eventually, the System Monitor Agent will do only what the name implies—monitor a single system.

LogRhythm is transitioning to Open Collector with popular logs for which the Open Collector's JSON-native log capabilities add a lot of value. This includes AWS, O365, and JSON logs that come in over flat file or syslog.


![[Pasted image 20240528051012.png]]


**Open Collector documentation is available in LogRhythm Docs and on the Community site. Make sure you are signed in to Docs, then** [**CLICK HERE**(opens in a new tab)](https://docs.logrhythm.com/OCbeats/docs/) **to access related docs and** [**CLICK HERE**(opens in a new tab)](https://community.logrhythm.com/t5/forums/searchpage/tab/message?advanced=false&allow_punctuation=true&q=open%20collector) **to access the Community site.**



## **Custom Beats**

Beats are essentially lightweight, purpose-built agents that acquire data and then feed it to Elasticsearch. The magic of beats is the libbeat framework that makes it easy to create customized beats for any type of data you’d like to send to Elasticsearch. Due to that flexibility, the number of Beats available and the capabilities of Beats overall are rapidly expanding.

![[Pasted image 20240528051216.png]]


LogRhythm does not support 3rd party beats. Any configuration or troubleshooting would be done by the customer.

Normally, a 3rd party beat would require custom parsing rules written in JQ on the Open Collector.

Check out [https://www.elastic.co/beats/(opens in a new tab)](https://www.elastic.co/beats/) for various options related to the beat types below.


