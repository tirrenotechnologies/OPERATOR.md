# tirreno user guide

## Contents

- [Overview](#overview)
- [Getting started](#getting-started)
- [Installation](https://github.com/tirrenotechnologies/ADMIN.md#installation)
- [API integration](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration)
- [Console](#console)
  - [Dashboard](#dashboard)
  - [Review queue](#review-queue)
  - [Activity](#activity)
  - [Entities](#entities)
  - [IP addresses](#ip-addresses)
  - [Countries](#countries)
  - [Networks](#networks)
  - [Resources](#resources)
  - [Blacklist](#blacklist)
  - [Rules engine](#rules-engine)
    - [Rule weights](#rule-weights)
    - [Thresholds settings](#thresholds-settings)
    - [Rules settings reset](#rules-settings-reset)
  - [Logbook](#logbook)
  - [API](#api)
  - [Settings](#settings)
- [Operator procedures](#operator-procedures)
  - [Trust score review](#trust-score-review)
  - [Supplemental investigation](#supplemental-investigation)
    - [Rules review](#rules-review)
    - [IP address signals](#ip-address-signals)
  - [Procedures outline](#procedures-outline)
- [Glossary](#glossary)
- [Resources](#links-and-resources)
- [Found a mistake?](#found-a-mistake)

## Overview

tirreno is an open-source framework for building sovereign security, compliance and fraud prevention applications.

Our framework detects threats where they actually happen, inside your application. It adds a security layer to internal (workforce) or external (customer-facing) applications to identify malicious activity by analyzing user behavior, account activity, field audit trails, and business logic abuse that infrastructure tools cannot detect.

While classic cybersecurity focuses on infrastructure and network perimeter, most breaches occur through compromised accounts and application logic abuse that bypass firewalls, SIEM, WAFs, and other defenses.

### How it works

In order to achieve the declared objective, tirreno collects intelligence to detect signals related to user identity and behaviour. This solution enables a detailed investigation of anomalies and a manual review of complex fraudulent patterns and cybrer threats. It helps to maintain non-interrupted services and protect private information.

tirreno brings enterprise-level fraud prevention techniques to a wide variety of digital platforms and organizations. It is developed for platforms with a demand for utmost control or for integration into a complex defence system, facilitating risk assessment during user onboarding and ongoing monitoring for everyday use.

### Privacy

By saying that tirreno is an ethical tool, we highlight our commitment to not crossing a thin line between taking mandatory actions for cyber threat prevention and breaking user privacy.

In fact, tirreno does not use cookies or browser fingerprinting and does not expose more user data than is strictly necessary, running all operations on the application backend. This provides utmost privacy and an immutable approach for the tirreno security analytics.

### System workflow

The tirreno’s workflow consists of the following main parts:

1. Data ingestion through API calls from your application.
2. Enrichment and calculation of entity context from collected data.
3. Machine-led data processing through rule-engine system.
4. Manual review of suspicious activity or automatic entity suspension to prevent further access to your app.

In the next subsections, we briefly describe each of these stages. When applicable, materials covering the subject more fully are linked.

#### Data ingestion

This stage is an entry point to tirreno setup and further usage. It requires the installation of a lightweight script for sending user request data to tirreno. And this is the *only* requirement for tirreno to start operating!

For more information on this, see [API integration](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration).

#### Data enrichment

A perceived magic 🪄 is happening during this stage: raw pieces of data are carefully prepared and then intermingled with the tirreno’s internal as well as external proprietary and open-sourced data.

#### Machine processing

This is the backbone of the tirreno background workings. Each entity/user request data is processed through a set of specific conditions ([rules](#term-Rule)). During this stage, the [rules engine](#term-Rules-engine) detects irregularities and suspicious activities. The received results define the calculated [trust score](#term-Trust-score), which is a determinative characteristic to consider at the stage of manual review.

For more details, see the [Rules engine](#rules-engine) section.

#### Manual review

tirreno outputs the accumulated knowledge base via a web-accessible user interface. The interface is designed to be a convenient tool for human-led investigation of the machine-preprocessed data analytics. It provides varying ways to proceed with investigation and can thus be flexibly adapted to different workflows and undertakings.

For a description of all the capabilities provided, advance to the chapters [Console](#console) and [Operator procedures](#operator-procedures).

## Getting started

1. [Download and install](https://github.com/tirrenotechnologies/ADMIN.md#installation) tirreno.

2. Revise the configuration on the [console](#term-Console)’s *Settings* page.

3. Enable sending [events](#term-Event) data to the tirreno’s API.

   - Refer to the [Quick start](https://github.com/tirrenotechnologies/DEVELOPMENT.md#quick-start) in the developer documentation to get started quickly.
   - Check out the [API integration](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration) section of the developer documentation for further information.

4. Configure the [rules engine](#term-Rules-engine).

   - Consult the [Rules engine](#rules-engine) section on how to do it.

5. Examine [entity](#term-Entity) [identities](#term-Identity) and behavioural patterns.

   - See the [Procedures outline](#procedures-outline) section for an initial action plan.
   - Read the chapters [Console](#console) and [Operator procedures](#operator-procedures) to learn more.

Accomplishing these steps initializes the [system’s workflow](#system-workflow).

Afterward, the ongoing operations — for the most part — consist of repeatedly acting as indicated in the last two steps. Namely, an [operator](#term-Operator)’s routine includes examination of the collected intelligence and tuning up the [rules engine](#term-Rules-engine) in line with the exposed scenarios and particular cases.

In the subsequent chapters, we explore these topics in greater detail.

## Console

The web-accessible user interface ([console](#term-Console)) is the main instrument an [operator](#term-Operator) uses for reviewing gathered intelligence and adjusting the tirreno system’s functioning. The [console](#term-Console) consists of two parts: a sidebar with the menu on the left side and the main body for outputting a selected page’s data.

The pages expose the gathered information through a set of tables, charts, widgets, and controls. They enable multidimensional lookup, filtering, and ordering of data. This way, the [console](#term-Console) provides detailed intelligence on [entity](#term-Entity) [identities](#term-Identity) and their interaction with a platform, making suspicious activity notable.

As a rule of thumb, [warning signals](#term-Warning-signal) are coloured with yellow throughout the user interface. Outstanding abnormalities are coloured red (for instance, low [trust scores](#term-Trust-score)), ranging up to purple in extreme cases (such as in [rules](#term-Rule)). The green colour, in contrast, is typically used for marking presumably safe entities.

By default, most of the pages output data for the last day. One of the pre-defined periods can be selected in the upper-right corner of the interface. A selection of one hour (1H), one day (1D), three days (3D), one week (1W), one month (1M), and three months (3M) is available. To obtain the entire dataset, click the label MAX.

The top part of many pages contains a search bar that facilitates the lookup and reach of varying entities across the system by matching an [entity](#term-Entity) ID, IP address, or autonomous system number (ASN). In addition, the principal tables are accompanied by more focused, specialized search bars for easier exploration of large datasets. The specialized search bars are generally located near the upper-right corner of a table.

### Dashboard

The *Dashboard* page loads by default after a successful login. It provides a quick overview of [entity](#term-Entity) activity. This page comprises several widgets, each of which outputs information collected during a selected period of time and links to pages with more extended information on an entity of interest.

In particular, at the top row, we can glance through the number of [events](#term-Event), [entities](#term-Entity), IP addresses, countries, and [resources](#term-Resource) recorded during a selected period of time and in total. As well as see the number of blacklisted [entities](#term-Entity) and the ones with low [trust scores](#term-Trust-score), with the possibility to quickly access the corresponding pages for a thorough review.

The second row of widgets — *Activity by entities*, *Activity by countries*, and *Activity by resources* — displays [entities](#term-Entity), countries, and [resources](#term-Resource) with the highest level of activity during the set period of time.

The last row is akin to light defence weaponry. It serves well for the primary detection of malicious scenarios by analyzing IP addresses. Its widgets — *Shared IP addresses*, *Account login fail*, and *Multiple IP addresses* — list [entities](#term-Entity) sharing IP addresses, those with the most failed login attempts, and those utilizing many different IP addresses. (For more details, see [IP address signals](#ip-address-signals).)

### Review queue

The *Review queue* page enables the assessment of [entities](#term-Entity) with low [trust scores](#term-Trust-score): those below the *Manual review* threshold set on the [Rules engine](#thresholds-settings) page.

The chart on this page shows the daily count of such [entities](#term-Entity) identified within a chosen time frame, categorized by review status: `Whitelisted`, `In review`, `Blacklisted`.

The table below presents basic [entity](#term-Entity) information and allows an [operator](#term-Operator) to remove an [entity](#term-Entity) from the queue by performing a [trust score review](#trust-score-review), one of the most highly advisable [operator procedures](#operator-procedures).

Note that the [Settings](#settings) page configuration **Review queue notifications** permits to activate sending of daily or weekly email reminders to examine *Review queue* items.

### Activity

The *Activity* page (titled *Latest events*) lists [events](#term-Event) for a selected period of time. It features a chart that displays the number of daily [events](#term-Event).

The table below outputs the key [event](#term-Event)’s data: [entity](#term-Entity) essentials, [event](#term-Event) time and [type](https://github.com/tirrenotechnologies/DEVELOPMENT.md#event-types), IP address, and detected device.

Clicking an [event](#term-Event)’s row opens a panel with an extended report on the right side. The report reveals numerous details about the [event](#term-Event), the requested [resource](#term-Resource), as well as expanded [entity](#term-Entity) and [identity](#term-Identity)-based analytics.

### Entities

The *Entities* page outputs basic information about all the [entities](#term-Entity) reported during a selected period of time.

The chart shows the daily number of new visitors, ranked by their [trust score](#term-Trust-score) values.

The table beneath lists each [entity](#term-Entity)’s [trust score](#term-Trust-score), basic account information, and review status. The specialized search bar and the [rules](#rules-engine) filter placed at the top of the table simplify [entity](#term-Entity) lookup by utilizing entered entity name, ID, signup date, or selected [rules](#rules-engine) for narrowing down the results.

A page devoted to individual [entity](#term-Entity) analytics can be opened by clicking on a table row. This page comprises widgets, tables, and charts that reveal cumulative intelligence on [entity](#term-Entity) [identities](#term-Identity) (such as IP addresses) and associated activities. It also displays [entity](#term-Entity)-matching [rules](#term-Rule) and enables setting [entity](#term-Entity) review status.

A careful study of the data presented on an [entity](#term-Entity) page is one of the keys to the identification of a malicious actor and is often an essential part of threat hunting. (See the chapter on [Operator procedures](#operator-procedures).)

> **Caution**
>
> Clicking the `Delete entity` button at the bottom of the page triggers the removal of all recorded [entity](#term-Entity)-related information.

### IP addresses

This page presents information grouped by IP address. The data is shown for a specified period of time.

The chart illustrates the daily number of *Residential* (considered safe), *Privacy*, and *Suspicious* (considered a [warning signal](#term-Warning-signal)) IP addresses.

The table lists IP addresses with key details and indicators of suspicious activity. Particularly, the latter include non-residential IP addresses and a high number of related [events](#term-Event) and [entities](#term-Entity).

For a more in-depth analysis of the data gathered on a specific IP address, click on a table row. The subsequent page features widgets that output [warning signals](#term-Warning-signal) for the IP address, as well as lists associated [entities](#term-Entity), devices, and [events](#term-Event). The [events](#term-Event) table is accompanied by a chart summarizing the daily count of requests made from the IP address.

### Countries

This page presents information grouped by countries identified based on the requests’ IP addresses. The data is displayed for a specified time period.

The map shows the geolocated countries and the respective number of [entities](#term-Entity), while the table displays primary statistics for each country. Here, audit the relative change in the number of [entities](#term-Entity), [events](#term-Event), and IP addresses over the specified and preceding periods. Large discrepancies in these numbers can serve as a [warning signal](#term-Warning-signal).

To access more analytics related to a country, click on a table row. The subsequent page provides the total number of [entities](#term-Entity), IP addresses, and [events](#term-Event) attributed to the country. It also includes compiled data on [entities](#term-Entity), IP addresses, internet service providers (ISPs), and [events](#term-Event). The latter includes a chart visualizing the daily request count from that country.

### Networks

The *Networks* page exhibits analytics categorized by internet service providers (ISP), identified through IP addresses recorded over a chosen period.

The chart displays the daily count of unique and newly reported active ISPs.

The table presents ISPs with their key statistics. More in-depth data is exposed on a specific ISP’s page, which can be opened by clicking on a table row. This page offers compiled information on associated [entities](#term-Entity), IP addresses, and [events](#term-Event) through total counts, tables, and illustrative charts.

### Resources

The *Resources* page enables the review of [entity](#term-Entity) activity grouped by the requested [resource](#term-Resource) over a selected time period.

The chart on this page illustrates the HTTP response status codes user requests ended with. Namely, it displays the daily counts of `OK` (200), `Not Found` (404), and `Forbidden` (403) with `Internal Server Error` (500) responses.

To access detailed information regarding a [resource](#term-Resource), click on a table row. The page that opens provides aggregated data on the [entities](#term-Entity), IP addresses, internet service providers (ISPs), devices, and [events](#term-Event) recorded in connection with the [resource](#term-Resource) requests.

### Blacklist

The *Blacklist* page displays [entity](#term-Entity) [identities](#term-Identity) added to a blacklist within a specified time frame.

The chart visualizes the daily count of blacklisted [identities](#term-Identity).

Each [identity](#term-Identity)’s details are outlined in the table below. To remove an [identity](#term-Identity) from the blacklist, click the `Remove` button on the right side. A page with more details on a corresponding [entity](#term-Entity) can be opened by clicking on a table row.

### Rules engine

This page lists conditions ([rules](#term-Rule)) that can serve two purposes, namely:

1. When enabled, to be utilized by the [rules engine](#term-Rules-engine) for the [trust score](#term-Trust-score) calculations.
2. To be manually triggered to get a list of [entities](#term-Entity) matching it.

To enable the processing of a [rule](#term-Rule) by the [rules engine](#term-Rules-engine), set a [rule](#term-Rule)’s weight to one of the following values: `Extreme`, `High`, `Medium`, or `Positive`. Setting the value to `None` disables the processing of a [rule](#term-Rule). To save an adjusted value, click the button appearing on the right side.

The highest weight (`Extreme`) strongly affects the calculated [trust score](#term-Trust-score) of an [entity](#term-Entity) with the matching [rule](#term-Rule), resetting the [trust score](#term-Trust-score) to the critically low value at once. [Rules](#term-Rule) with the `High` and `Medium` weights reduce the [trust score](#term-Trust-score) at correspondingly diminishing rates. In opposite, the `Positive` [rule](#term-Rule) increases the [entity](#term-Entity)’s [trust score](#term-Trust-score) value.

To manually trigger a [rule](#term-Rule)’s processing (e.g., for testing it), click the button shown on the right side. A list of [entities](#term-Entity) matching the [rule](#term-Rule) will be shown below the [rule](#term-Rule)’s definition.

The [rules engine](#term-Rules-engine)’s configuration and analysis of the outcomes of its work are vital parts of an [operator](#term-Operator)’s daily routine. Notably, see the [Supplemental investigation](#supplemental-investigation) section for several exemplary cases.

#### Rule weights

Each weight corresponds to a value that the [rules engine](#term-Rules-engine) applies when a [rule](#term-Rule) matches:

| Weight | Value | Effect on the trust score |
|--------|-------|---------------------------|
| `Positive` | -20 | Increases it (trusted behaviour) |
| `None` | 0 | None: the rule is disabled |
| `Medium` | 10 | Moderate decrease |
| `High` | 20 | Significant decrease |
| `Extreme` | 70 | Major decrease |

#### Thresholds settings

The *Thresholds settings* form sets two [trust score](#term-Trust-score) thresholds:

- **Manual review (below this score)** — [Entities](#term-Entity) with a trust score below this value appear in the [Review queue](#review-queue) (for example, 33).
- **Auto-blacklisting (below this score)** — [Entities](#term-Entity) with a trust score below this value are added to the [Blacklist](#blacklist) automatically (for example, 20). This threshold is `Off` unless set. Use it only after prior testing, and only where truly necessary.

Click `Update` to save the thresholds.

#### Rules settings reset

The *Rules settings reset* form applies a preset: a ready-made set of [rule](#term-Rule) weights for a common scenario. Select a preset, click `Reset`, and confirm with `Reset rules`.

> **Caution**
>
> Applying a preset is irreversible: it replaces all current rule weights. Individual weights can be adjusted again afterwards.

| Preset | Use case |
|--------|----------|
| Empty rules settings | Start from scratch: no rule weights set |
| Account takeover | Detect compromised accounts via new devices, locations, password changes |
| Credential stuffing | Detect automated login attempts and brute force attacks |
| Content spam | Detect spam content and suspicious posting patterns |
| Account registration | Protect registration from fake accounts and bots |
| Fraud prevention | General fraud detection across multiple vectors |
| Insider threat | Detect unusual employee behavior and data exfiltration |
| Bot detection | Identify automated traffic and crawlers |
| Dormant account | Monitor reactivation of long-inactive accounts |
| Multi-accounting | Detect entities with multiple accounts |
| Promo abuse | Detect promotional code and offer abuse |
| API protection | Protect APIs from abuse and scanning |
| High-risk regions | Flag traffic from high-fraud geographic regions |

### Logbook

Visit this page to verify the statuses of the recent requests to the [tirreno’s API](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration).

The provided data is meant to help identify failing requests (including by sent IP address and event timestamp) and get more information for fixing such requests.

The *Logbook* may also serve as a way of confirming API communication is properly set up, making it a valuable tool at the [API integration](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration) stage.

The table lists the latest requests (how many are kept is set by `LOGBOOK_LIMIT`, see [Environment variables](https://github.com/tirrenotechnologies/ADMIN.md#environment-variables)) with the following columns:

- **Source IP** — Where the request came from.
- **Local timestamp** — When the request was received, in the [operator](#term-Operator)’s time zone.
- **Endpoint** — Which API endpoint was called.
- **Status** — The processing result (see below).
- **Raw POST data** — The fields that were sent.

The search bar filters the table by raw POST data, endpoint, IP address, or error. Clicking a row opens a panel with the request details. The chart shows the daily number of requests, split into *Success*, *Validation issues*, and *Failed*.

| Status | Meaning |
|--------|---------|
| `Success` | The [event](#term-Event) was recorded. |
| `Success with warnings` | The [event](#term-Event) was recorded, but some values were corrected (for example, truncated or invalid values). |
| `Request failed` | The [event](#term-Event) was not recorded: a required field was missing, or a server error occurred. |
| `Rate limit exceeded` | The request was rejected by the rate limiter (see [Rate limiting](https://github.com/tirrenotechnologies/DEVELOPMENT.md#rate-limiting)). |

Requests with a missing or unknown [Tracking ID](#term-Tracking-ID) do not appear in the *Logbook*; see [Sending data issues](https://github.com/tirrenotechnologies/ADMIN.md#sending-data-issues) for how to troubleshoot them.

### API

This page provides information necessary to complete and fine-tune [API integration](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration).

At the top of the page, you will see a [Tracking ID](#term-Tracking-ID). It authorizes a [client](#term-Client) platform to connect to the tirreno API. A [Tracking ID](#term-Tracking-ID) can be renewed by clicking the `Reset` button. Note that the reset action cancels the validity of the previously used [Tracking ID](#term-Tracking-ID).

The code examples on the *API* page demonstrate the format in which tirreno expects [event](#term-Event) data to be sent, including mandatory and optional parameters for passing [event](#term-Event) details. You can also find a similar set of examples, supported by instructions, in the [API integration](https://github.com/tirrenotechnologies/DEVELOPMENT.md#api-integration) section of the developer documentation.

Use the panels below to manage [data enrichment](#term-Enrichment-API) — a feature of the [Enterprise Edition](#term-Enterprise-edition) of tirreno. The panels allow the following:

- Add an [enrichment key](#term-Enrichment-key).
- Choose the data types to enrich.
- Check the currently enabled subscription status.
- Update a payment card.
- Trigger resetting of enriched information.

Generally, enabling only IP address enrichment may be sufficient for the internal risk evaluation. For external fraud prevention, enriching additional data types is typically recommended.

### Settings

This page provides the ability to configure and control an account, as listed below:

- **Time zone** — Select a time zone for representing timestamps in the user interface.
- **Data retention** — Use this panel to set the maximum duration for storing recorded information.
- **Review queue notifications** — Choose how often to send email reminders to inspect [Review queue](#review-queue) items. The notifications can be sent on a daily or weekly basis, or they can be disabled.
- **Share access** — Manage [operators](#term-Operator) that have access to the [console](#term-Console). This can be done by inviting new [operators](#term-Operator) via email or revoking access for the existing ones.
- **Change password** — Set a new password for the account login.
- **Change email address** — Configure an email address associated with the account.
- **Check for updates** — Check if a tirreno update is available.
- **Delete account** — ⚠️ *Use this action with caution!* ⚠️ Deletion of an account is unrecoverable and leads to the removal of all related information, including the entire recorded history of [events](#term-Event).

## Operator procedures

Since each digital platform has its own special needs, the approaches to the [console](#console) utilization for the information analysis may vary.

The main goal of this chapter is to provide an overview of several common (elementary and more advanced) techniques and give advice on how to use them for building a daily [operator](#term-Operator)’s routine from scratch. With time, the described methods can be adapted more precisely to the observable needs of a platform.

From this perspective, we discern two major groups of techniques an [operator](#term-Operator) can employ while putting gathered intelligence under scrutiny. That is:

1. [Trust score review](#trust-score-review)
2. [Supplemental investigation](#supplemental-investigation)
   - [Rules review](#rules-review)
   - [IP address signals](#ip-address-signals)

All the techniques in these groups mostly differ in the initially observed signals. At the subsequent stages of the inspection, they tend to intertwine, such that an attentive tracing of any signal may lead to uncovering illicit pathways across different entities.

However, we generally recommend starting an [operator](#term-Operator)’s daily routine with the first group of techniques and using the second group (more specifically, [rules review](#rules-review)) for further investigation of particular use cases.

### Trust score review

On a day-to-day basis, we suggest beginning an [operator](#term-Operator)’s session by proceeding to the [Review queue](#review-queue) page of a [console](#term-Console). This page displays [entities](#term-Entity) with the lowest [trust scores](#term-Trust-score). Here, inspecting data in each row of the queue table, an [operator](#term-Operator) has a choice of either:

- Setting [entity](#term-Entity) status right in the table’s row.
- First opening a page with more detailed [entity](#term-Entity) information by clicking on an [entity](#term-Entity) email.

In the latter case, on an [entity](#term-Entity) page, note the matched [rules](#term-Rule), [warning signals](#term-Warning-signal), and the overall activity of an [entity](#term-Entity). The more abnormalities an [operator](#term-Operator) discovers, the higher the chance this is a fraudulent account. The status can be set on this page (see the upper-right corner) without getting back to the queue.

To set the status of an [entity](#term-Entity), click the `Not reviewed` button and then choose an applicable action: `Whitelist` or `Blacklist`. Both actions remove an [entity](#term-Entity) from the [review queue](#review-queue). Additionally, clicking the `Blacklist` button triggers the move of all tracked [entity](#term-Entity) [identities](#term-Identity) onto a [blacklist](#blacklist).

A similar sequence of actions can be performed starting from the [Entities](#entities) page. This page gives access to all the [entities](#term-Entity), not just the ones with low [trust scores](#term-Trust-score), which can sometimes be a preferred approach for getting a bigger picture of the user base.

### Supplemental investigation

A supplemental investigation implies an analysis of the additional [warning signals](#term-Warning-signal). And since any characteristic that looks even vaguely unusual can be interpreted as a [warning signal](#term-Warning-signal), in this section we specify the things to focus on in the first place.

Predominantly, an [operator](#term-Operator) may undertake this part of the analysis by concentrating on such straightforward signals such as:

- Risky email addresses.
- [Blacklisted](#blacklist) entities.
- TOR network usage (the *IP belongs to TOR* rule).
- VPN detection.
- Shared entities.

We look at each in greater detail in the ensuing subsections.

#### Rules review

We advise beginning a supplemental investigation with the [rules](#term-Rule) review.

The foundational instructions on the [rules engine](#term-Rules-engine) utilization are laid out in the [Rules engine](#rules-engine) section. In the context of the supplemental investigation, use the second of the described methods. Namely,

1. Trigger [rules](#term-Rule) manually to get a list of matching [entities](#term-Entity).
2. Proceed with scrutinizing the [entity](#term-Entity)’s [identities](#term-Identity) and activity.

Alternatively, open the [Entities](#entities) page. On the page, note the [rules](#term-Rule) filter at the top part of the *Entities* table. This filter enables the selection of [entities](#term-Entity) with matching [rules](#term-Rule), thus easing access to the records that require an [operator](#term-Operator)’s attention.

#### IP address signals

[Rules review](#rules-review) is not the only type of supplemental investigation. In this subsection, we describe one more way to begin the examination.

Open the [Dashboard](#dashboard) page. Here, have a look at the bottom row of the widgets. Observe the following indications:

- **Shared IP addresses** — Several [entities](#term-Entity) with the same IP address can be a sign of a cyber-threat.
- **Account login fail** — A high number of failed login attempts can indicate credential stuffing or an attempted account takeover.
- **Multiple IP addresses** — It is typical for cybercriminals to hide their actual location and identity behind different IP addresses. The higher the number of IP addresses used, the more attention should be given to the examination of the corresponding [entity](#term-Entity) behaviour.

### Procedures outline

Consider the below action plan as the foundation of an [operator](#term-Operator)’s routine.

1. [Trust score review](#trust-score-review)

   A. Open the *Review queue* page.

   - Either assign a fitting status to each [entity](#term-Entity) in the queue table.
   - Or open an entity page by clicking on an email address.
     - Examine information presented on the page.
     - Set [entity](#term-Entity) status in the upper-right corner.

   B. Alternatively, open the *Entities* page.

   - Apply the steps in 1.A. to the rows marked as `Not reviewed`.

2. [Supplemental investigation](#supplemental-investigation)

   A. Open the *Rules engine* page.

   - Click `Action` button to get a list of [entities](#term-Entity) matching the [rule](#term-Rule).
   - Open each matched entity page for inspection.
     - Examine information presented on the page.
     - Set [entity](#term-Entity) status in the upper-right corner.

   B. Open the *Dashboard* page.

   - Set a time period in the upper-right corner of the page.
   - Scrutinize entities in the top rows of the following widgets:
     - Shared IP addresses
     - Account login fail
     - Multiple IP addresses

## Glossary

Even though tirreno is a system utilizing numerous sophisticated techniques inside, on the outside it is designed to be an approachable solution. Accordingly, in this user guide, we make an effort to introduce as little special terminology and concepts as possible without compromising the guide’s applicability and comprehensiveness for users of the system.

Following is a list of terms that may come in handy when acquainting oneself with tirreno. The terms are listed in the order corresponding to the [workflow of the system](#system-workflow).

- <a id="term-Community-edition"></a>**Community Edition** (open-source) — For developer teams that want to add a security layer to self-hosted applications. Get started today without getting into complex business relationships. Licensed under GNU Affero General Public License v3 (AGPL-3.0).

- <a id="term-Enterprise-edition"></a>**Enterprise Edition** — Built for client portals, SaaS, public sector portals, and digital platforms. Fraud and abuse prevention, and dedicated assistance for your SOC, product, and risk teams.

- <a id="term-White-label-edition"></a>**White-label Edition** — White-label is for companies that want to offer anti-fraud, security or risk-management products built on tirreno framework to their clients under their own brand. tirreno runs on your infrastructure, or even in your edge product. For Enterprise and White-label editions, contact team@tirreno.com.

- <a id="term-Enrichment-API"></a>**Enrichment API** — The tirreno API that supplies extended information on IP addresses.

- <a id="term-Enrichment-key"></a>**Enrichment key** — A key that grants access to the [Enrichment API](#term-Enrichment-API).

- <a id="term-Client"></a>**Client** — A digital platform that sends [entity](#term-Entity) request data to tirreno.

- <a id="term-Entity"></a>**Entity** — An actor that sends requests to the [client](#term-Client). Shown as *Entities* in the [console](#term-Console).

- <a id="term-Sensor"></a>**Sensor** — A tirreno-provided application programming interface (API) that enables the collection, enrichment, and management of information. The sensor is bundled with the tirreno source code in the “/sensor” directory. The default sensor URL is `https://your-domain.example/sensor`.

- <a id="term-Integration-script"></a>**Integration script** — Code that sends information from a [client](#term-Client) platform to the [sensor](#term-Sensor).

- <a id="term-Tracking-ID"></a>**Tracking ID** — An account-unique value that authorizes access to the tirreno API. This value must be included in the `Api-Key` header of each API request.

- <a id="term-Event"></a>**Event** — An [entity](#term-Entity) request registered with the tirreno’s API (see [sensor](#term-Sensor)). May also refer to the reported data associated with an event.

- <a id="term-Rules-engine"></a>**Rules engine** — A set of conditions for machine-performed analysis of [events](#term-Event).

- <a id="term-Rule"></a>**Rule** — One of the conditions utilized by the [rules engine](#term-Rules-engine).

- <a id="term-Trust-score"></a>**Trust score** — An [entity](#term-Entity)-specific value. It is calculated by the [rules engine](#term-Rules-engine) based on the reported [events](#term-Event). The trust score value ranges from 0 to 99. [Entities](#term-Entity) with fewer [warning signals](#term-Warning-signal) detected have higher scores. A low trust score denotes a significant risk of fraudulent [entity](#term-Entity) activity.

- <a id="term-Console"></a>**Console** — A web-accessible user interface that outputs the intelligence for manual review and enables control over the alterable parts of tirreno.

- <a id="term-Operator"></a>**Operator** — A person that performs tuning of the tirreno system and manual review of the collected intelligence via [console](#term-Console).

- <a id="term-Warning-signal"></a>**Warning signal** — An abnormality in [events](#term-Event) or [entity](#term-Entity) data, potentially indicating a fraudulent activity. Warning signals are commonly marked with colour throughout the [console](#term-Console).

- <a id="term-Resource"></a>**Resource** — An element of a [client](#term-Client) platform that can be accessed by an [entity](#term-Entity). For example, this can be a web page “/users/login” or “/index.html”.

- <a id="term-Identity"></a>**Identity** — A basic piece of information related to an [entity](#term-Entity), such as an email address, IP address, phone number, etc.

---

<a id="links-and-resources"></a>

## Resources

| Resource | URL |
|----------|-----|
| Live Demo | [play.tirreno.com](https://play.tirreno.com) (admin/tirreno) |
| Resource center | [tirreno.com/bat](https://www.tirreno.com/bat/) |
| Administration guide | [github.com/tirrenotechnologies/ADMIN.md](https://github.com/tirrenotechnologies/ADMIN.md) |
| Developers Guide | [github.com/tirrenotechnologies/DEVELOPMENT.md](https://github.com/tirrenotechnologies/DEVELOPMENT.md) |
| User Guide | [github.com/tirrenotechnologies/USER.md](https://github.com/tirrenotechnologies/USER.md) |
| API reference | [github.com/tirrenotechnologies/API.md](https://github.com/tirrenotechnologies/API.md) |
| GitHub | [github.com/tirrenotechnologies/tirreno](https://github.com/tirrenotechnologies/tirreno) |
| GitLab Mirror | [gitlab.com/tirreno/tirreno](https://gitlab.com/tirreno/tirreno) |
| Docker Hub | [hub.docker.com/r/tirreno/tirreno](https://hub.docker.com/r/tirreno/tirreno) |
| Packagist | [packagist.org/packages/tirreno/tirreno](https://packagist.org/packages/tirreno/tirreno) |
| PHP Tracker | [github.com/tirrenotechnologies/tirreno-php-tracker](https://github.com/tirrenotechnologies/tirreno-php-tracker) |
| Python Tracker | [github.com/tirrenotechnologies/tirreno-python-tracker](https://github.com/tirrenotechnologies/tirreno-python-tracker) |
| Node.js Tracker | [github.com/tirrenotechnologies/tirreno-nodejs-tracker](https://github.com/tirrenotechnologies/tirreno-nodejs-tracker) |
| WordPress Tracker | [github.com/tirrenotechnologies/tirreno-wordpress-tracker](https://github.com/tirrenotechnologies/tirreno-wordpress-tracker) |
| Community Chat | [chat.tirreno.com](https://chat.tirreno.com) |

---

## Found a mistake?

If you have found a mistake in the documentation, no matter how large or small, please let us know by [creating a new issue](https://github.com/tirrenotechnologies/tirreno/issues) in the tirreno repository.

---

## License

tirreno and this documentation are licensed under the **GNU Affero General Public License v3 (AGPL-3.0)**.

The name "tirreno" is a registered trademark of tirreno technologies sàrl.

---

*tirreno Copyright (C) 2026 tirreno technologies sàrl, Vaud, Switzerland.*
