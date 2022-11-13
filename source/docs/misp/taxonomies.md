# Taxonomies

A taxonomy is a means of classifying information based on standard features or attributes. On MISP, taxonomies are 
used to categorise events, indicators and threat actors based on tags that identify them.

Analysts can use taxonomies to:

* Set events for further processing by external tools such as VirusTotal.
* Ensure events are classified appropriately before the Organisation Admin publishes them.
* Enrich intrusion detection systems' export values with tags that fit specific deployments.

Taxonomies are expressed in machine tags:

* Namespace: Defines the tag's property to be used.
* Predicate: Specifies the property attached to the data.
* Value: Numerical or text details to map the property.

Taxonomies are listed under the Event Actions tab. The site admin can enable relevant taxonomies.