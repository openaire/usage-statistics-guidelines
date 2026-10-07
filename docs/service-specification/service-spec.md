# Usage Counts Service Specification

## OpenAIRE Analytics platform

OpenAIRE's Usage Counts service uses the open-source [Matomo analytics platform][matomo] to track usage activity.

**OpenAIRE hosts and operates its own Matomo instance. Data providers do not install Matomo**: they only install a lightweight tracker (Tier 1) or expose existing statistics (Tier 2), as described below.

Because the instance is self-hosted by OpenAIRE, all usage data stays on OpenAIRE infrastructure and is not shared with third parties. This supports compliance with the EU General Data Protection Regulation (GDPR).

## Description of the Service

OpenAIRE Usage Counts Service operates as a basis for:

* reliable, comparable standards-based statistics (COUNTER-conformant, bot filtering)
* reporting to stakeholders (e.g. as a repository dashboard feature)  
* accumulated usage statistics of repository items which are hosted in multiple data providers (de-duplication)
* provision of usage statistics as an open metric via a standardized API (SUSHI-Lite) for 3rd party re-use.

Two approaches are available for the collection of usage data, named Tier 1 and Tier 2, both depicted in Figure 1.

### Tier 1 – Push (tracker)

Tier 1 is the default workflow. It uses a *Push* model with server-side tracking: the repository installs a tracker (a DSpace patch, an EPrints plugin, or the Generic Matomo Tracker, which reads web server logs). The tracker sends each usage event to OpenAIRE's Matomo instance through Matomo's HTTP API. Events are logged in real time. Data is then transferred offline, using Matomo’s API, to OpenAIRE’s DBs for further processing using the COUNTER Code of Practice and statistical analysis. The resulting statistics are published in the OpenAIRE portal, in the PROVIDE dashboard and through the SUSHI-Lite API endpoint. The tracker sends the following parameters:


| Parameter | Description
------------ | -------------
| rec | Required for tracking, must be set to one
| idsite | the ID of the repository
| idVisit | a visitor/session ID (an 8 byte binary string) automatically created by Matomo  
| cip |the IP address of the visitor (can be anonymized by the tracker before sending)
| action_name | the title of the item being accessed
| url |the url of the requested item
| download | the url of the item, in case of a download
| timestamp | the date & time of the request, automatically created by Matomo
| cvar | A custom variable to store the OAI-PMH Identifier, of the item being viewed/downloaded
| ua | the Web Browser and the operating system of the visitor
| urlref | The URL from which the item request was sent (the HTTP referrer header value)
| token_auth | 32 character authorization key used to authenticate the API request


### Tier 2 – Pull (existing statistics)

Tier 2 uses a *Pull* model. It is meant for data providers, or usage statistics aggregators (e.g. IRUS-UK), that already produce consolidated COUNTER reports and offer a way to download them in bulk, e.g. via SUSHI-Lite. **No installation is needed on the repository side**: OpenAIRE harvests the reports and stores them in its database. The statistics are then published through the same channels as Tier 1.


In both tiers, the Usage Counts service interacts with other parts of the OpenAIRE infrastructure, namely the repository dashboard, the data source profile management and the OpenAIRE portal.


<!-- <img width="700"  height="700" align="center" src="img/TiersCollectionWorkflows.png"> -->
![](img/TiersCollectionWorkflows.png)

*Fig. 1 – Tier 1 (push) and Tier 2 (pull) collection workflows*

## Application of COUNTER Code of Practice rules on usage events

An important step of the Usage Counts Service process is the cleaning of usage activity which is caused by machines like web bots or spiders. Such software systematically browses websites in order to enhance web indexing but their activities affect usage traffic statistics since they result in the logging of non-legitimate usage activity. To avoid such non-legitimate traffic Matomo maintains a community-contributed list of referrer spammers. The list is stored in a file named spammers.txt and contains one (bot/spider) host per line. This list is included in each Matomo release so that referrer spam is filtered automatically. Matomo also automatically updates this list to its latest version every week.

The main cleaning process in usage logs, is the application of the COUNTER Code of Practice rules, as described in the last version of the COUNTER framework. COUNTER framework provides an international, extendible Code of Practice for e-Resources that allows the usage of online information products and services to be measured in a credible, consistent and compatible way using vendor-generated data.

COUNTER specifies the following return codes and time filters for data processing :

<ol type="a">
  <li>Only successful and valid requests should be counted. For web server logs successful requests are those with specific NCSA return codes. (200 and 304). The standards for return codes are defined and maintained by NCSA. In case key events are used their definition should match the NCSA standards. (For more information see Appendix D: Guidelines for Implementation.)</li>
  <li>Records generated by the server together with the requested page (e.g. images, gif’s, style sheets (.css)) should be ignored.</li>
  <li>All users’ double-clicks on an http-link should be counted as only 1 request. The time window for occurrence of a double-click should be set at 10 seconds between the first and the second mouse-click.</li>
</ol>

There are a number of options to make sure that a double click comes from one and the same user:

1.	where only the IP address of a user is logged that IP should be taken as the field to trace double-clicks
2.	when a session-cookie is implemented and logged, the session-cookie should be used to trace the double-clicks.
3.	when user-cookies are available and logged, the user-cookie should be used to trace double- clicks
4.	when the username of a registered user is logged, this username should be used to trace double-clicks.

Options 1 to 4 above have an increasing level of reliability for filtering out double-clicks: option 1 has the lowest level of precision (and may lead to under reporting from the vendor perspective) while with option 4 the result will be optimal. The downloading and rendering of a PDF, image, video clip or audio clip may take longer than the rendering of an HTML page. Therefore, requests by one and the same IP/username/session- or user cookie for one and the same PDF, image, video clip or audio clip should be counted as a single request if these multiple requests occur within a 30 seconds time window. These multiple requests may also be triggered by pressing a refresh or back button on the desktop by the user.

In OpenAIRE's case, the 10-second window is applied to views and the 30-second window to downloads. Sessions are automatically identified by Matomo. Regarding repository records with multiple files associated (e.g. multiple book chapters), downloads of different files are counted separately, even though they share the same item identifier (e.g. Handle, DOI).


## Representation and Provision of Usage Statistics

After COUNTER rules are applied, the resulting usage statistics are represented in the PROVIDE dashboard for repository managers, in the OpenAIRE portal per data source and document using a variety of charts. The statistics can also be requested as COUNTER Reports from the [SUSHI-Lite endpoint][sushiliteendpoint]. The relevant usage reports generated by OpenAIRE are:

* AR-1 - Article Report 1, number of successful article download requests by month and repository
* IR-1 - Item Report 1, number of successful item download requests by month and repository
* JR-1 - Journal Report 1, number of successful full-text article requests by month and journal
* RR-1 - Repository Report 1, number of successful item downloads for all repositories participating in the Usage Counts service
* BR-1 - Book Report 1, number of successful title requests by month and title
* BR-2 - Book Report 2, number of successful section requests by month and title

[sushiliteendpoint]: https://services.openaire.eu/usagestats/sushilite/
[matomo]: https://matomo.org/
