
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


## Filebeat

Filebeat is designed to read files from your system. It is particularly useful for system and application log files but can be used for any text files that you would like to index to Elasticsearch in some way. In the logging case, it helps centralize logs and files in an efficient manner by reading from your various servers and VMs, and then shipping to a central Logstash or Elasticsearch instance. Additionally, Filebeat eases the configuration process by including “modules” for grabbing common log file formats from MySQL, Apache, NGINX, and more. These modules reduce the Filebeat configuration to a single command.


## Metricbeat

As the name implies, Metricbeat is used to collect metrics from servers and systems. It is a lightweight platform dedicated to sending system and service statistics. Like Filebeat, Metricbeat includes modules to grab metrics from operating systems like Linux, Windows and Mac OS, and applications such as Apache, MongoDB, MySQL, and nginx. Metricbeat is extremely lightweight and can be installed on your systems without impacting system or application performance. As with all of the Beats, Metricbeat makes it easy to create your own custom modules.


## Packbeat

Packetbeat, a lightweight network packet analyzer, monitors network protocols to enable users to keep tabs on network latency, errors, response times, SLA performance, user access patterns, and more. With Packetbeat, data is processed in real time so users can understand and monitor how traffic is flowing through their network. Furthermore, Packetbeat supports multiple application layer protocols, including MySQL and HTTP.


## Winlogbeat

Winlogbeat is a tool specifically designed for providing live streams of Windows event logs. It can read events from any Windows event log channel, monitoring log-ons, log-on failures, USB storage device usage, and the installation of new software programs. The raw data collected by Winlogbeat is automatically sent to Elasticsearch and then indexed for convenient future reference. Winlogbeat acts as a security enhancement tool and makes it possible for a company to keep tabs on literally everything that is happening on its Windows-powered hosts.


## Auditbeat

Auditbeat performs a similar function on Linux platforms, monitoring user and process activity across your fleet. Auditd event data is analyzed and sent, in real time, to Elasticsearch for monitoring the security of your environment.


## Heartbeat

Heartbeat is a lightweight shipper for uptime monitoring. It monitors services, basically by pinging them, and then ships data to Elasticsearch for analysis and visualization. Heartbeat can ping using ICMP, TCP, and HTTP. It has support for TLS, authentication, and proxies. Its efficient DNS resolution enables it to monitor every single host behind a load-balanced server.

