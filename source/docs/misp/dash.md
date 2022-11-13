# Dashboard

MISP is effectively useful for the following use cases:

* Malware Reverse Engineering: Sharing of malware indicators to understand how different malware families function.
* Security Investigations: Searching, validating and using indicators in investigating security breaches.
* Intelligence Analysis: Gathering information about adversary groups and their capabilities.
* Law Enforcement: Using indicators to support forensic investigations.
* Risk Analysis: Researching new threats, their likelihood and occurrences.
* Fraud Analysis: Sharing of financial indicators to detect financial fraud.

## Dashboard

The analyst's view of MISP provides you with the functionalities to track, share and correlate events and IOCs identified during your investigation. The dashboard's menu contains the following options, and we shall look into them further:

* Home button: Returns you to the application's start screen, the event index page or the page set as a custom home page using the star in the top bar.
* Event Actions: All the malware data entered into MISP comprises an event object described by its connected attributes. The Event actions menu gives access to all the functionality related to the creation, modification, deletion, publishing, searching and listing of events and attributes.
* Dashboard: This allows you to create a custom dashboard using widgets.
* Galaxies: Shortcut to the list of MISP Galaxies on the MISP instance. More on these on the Feeds & Taxonomies Task.
* Input Filters: Input filters alter how users enter data into this instance. Apart from the basic validation of attribute entry by type, the site administrators can define regular expression replacements and blocklists for specific values and block certain values from being exportable. Users can view these replacement and blocklist rules here, while an administrator can alter them.
* Global Actions: Access to information about MISP and this instance. You can view and edit your profile, view the manual, read the news or the terms of use again, see a list of the active organisations on this instance and a histogram of their contributions by an attribute type.
* MISP: Simple link to your baseurl.
* Name: Name (Auto-generated from Mail address) of currently logged in user.
* Envelope: Link to User Dashboard to consult some of your notifications and changes since the last visit. Like some of the proposals received for your organisation.
* Log out: The Log out button to end your session immediately.

## Event management

The Event Actions tab is where you, as an analyst, will create all malware investigation correlations by providing descriptions and attributes associated with the investigation. Splitting the process into three significant phases, we have: 

* Event Creation.
* Populating events with attributes and attachments.
* Publishing.

## Event creation

In the beginning, events are a storage of general information about an incident or investigation. We add the description, time, and risk level deemed appropriate for the incident by clicking the Add Event button. Additionally, we specify the distribution level we would like our event to have on the MISP network and community. According to MISP, the following distribution options are available:

* Your organisation only: This only allows members of your organisation to see the event.
* This Community-only: Users that are part of your MISP community will be able to see the event. This includes your organisation, organisations on this MISP server and organisations running MISP servers that synchronise with this server.
* Connected communities: Users who are part of your MISP community will see the event, including all organisations on this MISP server, all organisations on MISP servers synchronising with this server, and the hosting organisations of servers that are two hops away from this one.
* All communities: This will share the event with all MISP communities, allowing the event to be freely propagated from one server to the next.

## Attributes & attachments

Attributes can be added manually or imported through other formats such as OpenIOC and ThreatConnect. To add them manually, click the Add Attribute and populate the form fields.

Some essential options to note are: 

* For Intrusion Detection System: This allows the attribute to be used as an IDS signature when exporting the NIDS data unless it overrides the permitted list. If not set, the attribute is considered contextual information and not used for automatic detection.
* Batch import: If there are several attributes of the same type to enter (such as a list of IP addresses, it is possible to join them all into the same value field, separated by a line break between each line. This will allow the system to create separate lines for each attribute.

## Publish event

Once the analysts have created events, the organisation admin will review and publish those events to add them to the pool of events. This will also share the events to the distribution channels set during the creation of the events.

