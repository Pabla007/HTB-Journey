
```
Let's create and customize a new Dashboard targeted to catch streaming.
```


```
Now let's customize the Web Console even further. We can use Lucene Syntax with our widgets, dashboards, and the Analyze page to customize and filter within our Web Console.
```


Lucene is an open-source text retrieval library that allows us to filter the data displayed based on our criteria. As a result, we are able to perform complex searches that can assist us using LogRhythm’s Web Console.


## Node-Link Graph Widget

Clicking on the "+" sign within the Node-Link Graph widget will reveal information regarding the connected hosts and users, such as IP addresses.

## TopX Widgets: Top vs. Bottom

The default state of TopX Widgets is to show the top number, but we can go into the Inspector panel and change this setting to show us the "Bottom X." This is especially helpful to focus on less frequently occurring events.

## Filtering with a "Wildcard"

Lucene Search Syntax has the ability to run a wildcard query. For example, you may want to find data on any classification name that contains Malware in its name (Malware X, Malware Y, Malware Z, etc). If you run a query using the term Malware, your search results will display only exact matches. 

For one-word wildcard filtering, remove the quotation marks and place an asterisk (*) where you would like to use a wildcard. 

For instance, to search for all classifications containing the word Malware:

- classificationName: *Malware*



