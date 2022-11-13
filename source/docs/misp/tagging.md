# Tagging

Information from [feeds](feeds.md) and [taxonomies](taxonomies.md), tags can be placed on events and attributes to 
identify them based on the indicators or threats identified correctly. Tagging allows for effective sharing of 
threat information between users, communities and other organisations using MISP to identify various threats.

Tags can be added by clicking on the buttons in the Tags section and searching from the available options appropriate 
to the case. The buttons represent global tags and local tags, respectively. It is also important to note that you 
can add your unique tags to your MISP instance as an analyst or organisation that would allow you to ingest, navigate 
through and share information quickly within the organisation.

## Tagging at event level vs attribute level

Tags can be added to an event and attributes. Tags are also inheritable when set. It is recommended to set tags on the entire event and only include tags on attributes when they are an exception from what the event indicates. This will provide a more fine-grained analysis.

## The minimal subset of tags

The following tags can be considered a must-have to provide a well-defined event for distribution:

* [Traffic Light Protocol](https://www.first.org/tlp/): Provides a colour schema to guide how intelligence can be shared.
* Confidence: Provides an indication whether the data being shared is of high quality and has been vetted so that it can be trusted to be good for immediate usage.
* Origin: Describes the source of information and whether it was from automation or manual investigation.
* Permissible Actions Protocol: An advanced classification that indicates how the data can be used to search for compromises within the organisation.