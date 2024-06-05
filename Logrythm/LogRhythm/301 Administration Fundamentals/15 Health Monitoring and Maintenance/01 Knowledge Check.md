
### While SQL maintenance jobs are running, you should **not**...

Schedule reports or other tasks to run.

Do not schedule reports or other tasks when SQL maintenance jobs are running (as this can cause tables to be locked and times outs to occur).

When MS SQL Maintenance tasks are running, index rebuilding occurs offline, and the databases are not accessible to users.


<hr>

# Key Takeaways

## A variety of tools are available to help with monitoring and troubleshooting.

- Deployment Monitor 
- Performance Monitor Counters (for Windows)
- LogRhythm Diagnostic Logs
- LogRhythm Diagnostic Alarm Rules 
- LogRhythm Diagnostics Tool 
- Status Page (for the Web Console)
- Elasticsearch Monitoring (via web browser on Windows, or curl on Linux)
- Log Volume Reports

<hr>

## The Deployment Monitor allows for monitoring the health of a LogRhythm platform by displaying attributes such as heartbeats, database utilization, processing queues, and log volume.

Generated warnings and errors from the Deployment Monitor can be used in conjunction with diagnostic logs and LogRhythm’s Diagnostic Tool to investigate and address platform issues.


<hr>

Windows Performance Monitor counters can provide a real-time display of metrics related to platform components, applications, services, or the operating system itself.

<hr>

## LogRhythm health monitoring is also available via Grafana dashboards, accessible through a web interface at http://:3000.

These dashboards provide a graphical representation of LogRhythm’s components.

<hr>



