<img width="200"  height="200" align="right" src="img/Logo_Vertical.png">
# OpenAIRE Usage Counts Guidelines

## Purpose

These guidelines explain to data source managers (repositories, e-journals, CRIS) how to join the OpenAIRE Usage Counts Service, and describe the methods and standards OpenAIRE uses to turn usage data into comparable, standards-based statistics. The guidelines follow Release 4 of the COUNTER Code of Practice for e-Resources, supplemented by the IRUS-UK Code of Practice.

## In short: what do I need to install?

!!! note "You do **not** need to install Matomo"
    OpenAIRE hosts and operates the Matomo analytics platform used by the service. Data providers never install or maintain Matomo themselves.

What you need depends on how you take part:

| | **Option 1 – Tracker (Tier 1, default)** | **Option 2 – Existing statistics (Tier 2)** |
|---|---|---|
| **When it fits** | Your repository does not yet produce COUNTER statistics | Your repository already exposes COUNTER-compliant reports via SUSHI, or takes part in a usage statistics aggregator (e.g. IRUS) |
| **What you install** | A small tracker for your platform (DSpace patch, EPrints plugin, or a generic log-based script) | Nothing |
| **How data reaches OpenAIRE** | The tracker *pushes* usage events to OpenAIRE's Matomo | OpenAIRE *pulls* your consolidated reports |
| **What you get from OpenAIRE** | A Matomo **Site ID** and an **authentication token** | — |

Details of both workflows are in the [Service Specification](service-specification/service-spec.md#description-of-the-service).

## How to participate

### Option 1 – Tracker (Tier 1)

| # | Who | Action |
|---|---|---|
| 1 | Repository manager | In the [PROVIDE dashboard][providedashboard], check that your repository is registered (or register it) and request participation in Usage Counts. |
| 2 | Repository manager | Get the **Site ID** and the **authentication token** for your repository. The Site ID is stored in your data source profile. If you cannot find them, contact [repositoryusagestats@openaire.eu](mailto:repositoryusagestats@openaire.eu). |
| 3 | Repository manager | Install and configure the tracker for your platform (see [Trackers](#trackers) below), entering the Site ID and token. |
| 4 | Repository manager | Deploy the tracker in production and inform OpenAIRE that it is active. |
| 5 | OpenAIRE | Check that usage events arrive correctly and tell the repository manager the result of the validation. |
| 6 | OpenAIRE | Process the events every month according to COUNTER rules and publish the statistics in PROVIDE, in the OpenAIRE portal and through the [SUSHI-Lite endpoint][sushiliteendpoint]. |

### Option 2 – Existing statistics (Tier 2)

| # | Who | Action |
|---|---|---|
| 1 | Repository manager | Register your repository in the [PROVIDE dashboard][providedashboard] (if not already registered). |
| 2 | Repository manager | Contact [OpenAIRE support][support] and provide the SUSHI endpoint of your repository, or the aggregator that already collects your statistics. |
| 3 | OpenAIRE | Test the harvesting of your reports and confirm participation. |
| 4 | OpenAIRE | Harvest your reports regularly and publish them as in Option 1, step 6. |

### Trackers

The trackers and their installation instructions are maintained on GitHub:

| Platform | Tracker | Notes |
|---|---|---|
| DSpace 4, 5, 6, 7 | [OpenAIRE-Piwik-DSpace](https://github.com/openaire/OpenAIRE-Piwik-DSpace) | Patch applied to the DSpace source; DSpace must be rebuilt and redeployed |
| EPrints 3 | [EPrints-OAPiwik](https://github.com/openaire/EPrints-OAPiwik) | Plugin; requires an Apache restart |
| Any other platform | [Generic Matomo Tracker](https://github.com/openaire/Generic-Matomo-Tracker) | Python 3 script that reads your web server log files and sends usage events to OpenAIRE's Matomo |

The DSpace and EPrints trackers can anonymize the visitor's IP address before it is sent, by setting how many bytes of the address are zeroed. See each tracker's README.

## Why take part

The service collects usage data from OpenAIRE's network of data providers and turns it into reliable, comparable metrics (item downloads and metadata views) that conform to the COUNTER Code of Practice. Its added value is:

* **for repository managers and hosting institutions:** a way to measure how well the publication platform is used;
* **for authors and readers:** visibility of the most used items;
* **for funders and evaluators:** an indicator that complements citations and altmetrics. For research data and software it is often the only indicator available;
* **for everyone:** usage of the same publication is added up across all the repositories that host it.

Statistics are available in the PROVIDE dashboard, in the OpenAIRE portal and, for third-party reuse, through the SUSHI-Lite API.

## Privacy

The service complies with the EU General Data Protection Regulation (GDPR). Only the data listed in the [Service Specification](service-specification/service-spec.md#description-of-the-service) is collected, and IP addresses can be anonymized at the source by the tracker. Usage data is stored on OpenAIRE's own Matomo instance and is not shared with third parties.

## Responsibilities

*Data provider managers*

* Keep the usage statistics information in the PROVIDE dashboard up to date.
* Tell [OpenAIRE support][support] before platform changes (migrations, new releases) that may change record identifiers or URLs, since these can break tracking.

*OpenAIRE*

* Validates every new tracker or SUSHI endpoint with the data provider manager before participation starts.
* Produces statistics and reports every month.
* Keeps data processing and cleaning rules aligned with the latest COUNTER release.

## Maintenance of the guidelines

The guidelines are reviewed regularly. They are updated when new versions of usage statistics standards are released, or when OpenAIRE services that record, process or expose usage statistics change. Participating data provider managers are informed of the changes.

[sushiliteendpoint]: https://services.openaire.eu/usagestats/sushilite/
[providedashboard]: https://provide.openaire.eu/
[support]: https://www.openaire.eu/support
