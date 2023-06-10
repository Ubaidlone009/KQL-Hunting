
# Alternate Datastream

We will use regex to detect Alternate Datastream


## Query

```KQL
DeviceFileEvents
| where InitiatingProcessCommandLine matches regex @"\.[a-z]{2,9}:[a-z0-9\-_]{1,9}\.[a-z]{1,9}(\s+|$)"


```




## Appendix

This query is influenced by  [this article.](https://www.sciencedirect.com/topics/computer-science/alternate-data-stream#:~:text=Alternate%20Data%20Streams%20(ADS)%20is,them%20execution%20without%20being%20detected)


