<img width="200"  height="200" align="right" src="img/Logo_Vertical.png"> 
# OpenAIRE Usage Statistics Guidelines

## Purpose

The guidelines are aimed to provide orientation for data source managers about participation in the OpenAIRE Usage Statistics Service and about the methods and standards used to collect and process usage data in order to generate comparable, standards-based usage statistics. The guidelines follow the Release 4 of the COUNTER Code of Practice for e-Resources supplemented by the IRUS-UK Code of Practice.

## Introduction

The OpenAIRE Usage Statistics Service gathers usage data and consolidated usage statistics reports respectively, from its distributed network of data providers (repositories, e-journals, CRIS) by utilizing open standards and protocols and exploiting reliable, consolidated and comparable usage metrics like counts of item downloads and metadata views conformant to COUNTER Code of Practice.

The Usage Statistics Service, allows the sharing of statistics across the above distributed network and provides significant added value for different stakeholders. On the data-provider level, it can serve repository managers and hosting institutions as a tool to evaluate the success of the publication platform. On the individual item level, it can demonstrate popular publications to authors and readers. In addition  to  other  traditional  (e.g.  citation  counts)  and  alternative  metrics  (e.g. mentions, recommendations) it can inform funding authorities in research evaluation processes.

Usage statistics on the item level can reflect relevance of a particular research output, of topics, of (disciplinary) data sources over the course of time and up to the present, e.g. they are an important indicator to analyze trends. For non-traditional output types (e.g. research data, research software), usage statistics are often the only indicator available, while the implementation of data citation standards lags behind.

The  OpenAIRE  Usage  Statistics  Service  aims  to  facilitate  the  above  added-value  services by tracking, collecting, analyzing and monitoring usage data from its network of data providers and exploiting usage metrics like downloads and metadata views. Moreover, OpenAIRE’s distributed network of data providers allows the aggregation of usage data about publications which are published in several places.

Being aware of the sensitivity of this usage data, legal constraints are considered regarding the EU General Data Protection Regulation (GDPR). The aim is to allow COUNTER-conformant reports on usage statistics to be generated and thus enable the results of this process to be used to examine correlations with other types of metrics, e.g. bibliometric and webometric. This service is integrated with the repository dashboard, the OpenAIRE portal and API for 3rd party reuse.

## How to participate in the OpenAIRE Usage Statistics Service

Integration of repository usage statistics comprises the following steps:

*  registration of the repository in the [Matomo platform][matomo] via the Content Provider Dashboard
*  installation of the tracking code
*  tracking of usage events from the repository in Matomo
*  validation of tracking of usage events from the repository in Matomo
*  application of COUNTER rules on usage data and storing them to the OpenAIRE statistics Database
*  application of the COUNTER Code of Practice Release 4 for processing the usage events and generating usage statistics reports presented in the OpenAIRE Portal, or via a [SUSHI-Lite API endpoint][sushiliteendpoint].

### Usage Statistics Service Registration

The first step of the usage tracking process is the registration of the repository to the [Matomo platform][matomo] running in OpenAIRE. This is done by the data provider manager via the repository dashboard. A unique identifier of the Matomo instance is generated and associated with the repository, together with an authentication token, required to access the platform. The identifier is stored and accessible in the data source profile.

### Usage Statistics Service Configuration

There are four steps that need to be performed in order to configure and use the Usage Statistics Service. These steps require the co-operation of the repository and given below:

On the Repository's side

1. Download the tracking code for the repository platform.
2. Configure the tracking code according to the instructions. The code and the instructions are maintained on Github:

	* as a patch for various versions of [DSpace](https://github.com/openaire/OpenAIRE-Piwik-DSpace)
	* as an [Eprints](https://github.com/openaire/EPrints-OAPiwik) plugin for version 3
	* as a python script in the form of a [Generic Matomo Tracker](https://github.com/openaire/Generic-Matomo-Tracker)

3. Deploy the tracking code in your repository platform.

On the OpenAIRE's side

4. OpenAIRE's usage statistics staff will validate the installation of the tracking code and inform the repository manager accordingly.

## Responsibilities

Before data providers can officially participate in OpenAIRE Usage Statistics the implementation
and configuration of the tracker plugins and SUSHI-Lite endpoints respectively will be tested and
validated between the data provider manager and the OpenAIRE support.

*Data Provider Managers*

Data Provider Managers keep the configuration information regarding usage statistics in the data provider
dashboard up to date.
In case of platform software updates (e.g. by migration, new releases) which may affect existing
metadata record identifiers the data provider manager informs the OpenAIRE support.

*OpenAIRE*

The OpenAIRE Usage Statistics service complies with the EU General Data Protection Regulation with regard to the protection of
personally identifiable information.
The Usage Statistics Service will generate visualizations and reports on a monthly basis. In order
to conform with the COUNTER Code of Practice the data processing and cleaning rules will be
maintained to comply with the lastest release of COUNTER.

## Maintenance of the Guidelines

The guidelines are continuously reviewed for their validity and will be updated with regards to
new releases of standards for the recording and exchange of usage statistics and new releases
of OpenAIRE services that record, process, represent or expose usage statistics. Participating
data provider managers will be informed accordingly.

[sushiliteendpoint]: http://services.openaire.eu/usagestats/sushilite/
[matomo]: https://matomo.org/
