---
title: 'PFD Toolkit: Unlocking Prevention of Future Death Reports for Research'
tags: # Dan: are these tags okay? Not sure if they're for searching on JOSS or if they're for SEO or something
  - Python
  - Prevention of Future Deaths
  - Coroners' Reports
  - Open Data
  - United Kingdom
  - Public health
  - Public safety
  - Natural Language Processing (NLP)
  - Large Language Models (LLMs)
  - Web scraping
authors:
 - name: Sam Osian
   corresponding: true    # Corr. author isn't getting rendered rn; not sure why
   orcid: 0009-0000-7644-6218
   affiliation: 1
 - name: Jonathan Pytches
   orcid: 0000-0000-0000-0000 # Stop forgetting to ask John to get an orcid!!!
   affiliation: 2
affiliations:
 - name: Department of Primary Care and Mental Health, University of Liverpool, United Kingdom
   index: 1
 - name: Independent Researcher, United Kingdom
   index: 2
date: 3 June 2025
bibliography: paper.bib
---


# Summary


Prevention of Future Death (PFD) reports are the official mechanism by which coroners in
England and Wales alert individuals, organisations, and agencies to circumstances that may
lead to further deaths. Each report sets out the context of an individual case, details the
factors believed to have contributed, and identifies concerns that, if addressed, could prevent
future deaths from occurring.

While these documents represent a rare, ground-level view into public safety risks, their potential for analysis
has long been obstructed. Reports are scattered across a judicial website whose topic filters omit
entire swathes of content. The website offers no ability to mass-download reports into a single
dataset, and many older reports exist only as scanned, image-based .pdfs, which cannot be 
text-searched or analysed using conventional methods. 

*PFD Toolkit* is a Python package designed to overcome these barriers. The toolkit automates 
the full pipeline of loading, cleaning, structuring and analysing PFD data, making 
information contained within them readily usable. By integrating large language models (LLMs) 
and vision models, the toolkit extracts structured data from both text and scanned, image-based reports. 
Users can search thousands of reports with flexible, plain-English queries, assign custom thematic labels, 
and extract specific features at scale.

The toolkit transforms a once fragmented archive into a living resource for research and public 
health, enabling rapid identification of emerging risks and timely policy responses.



# Statement of need

<!-- Maybe should cite the paper where Georgia Richards called for technological innovation... 
...Word limit is tight though!
-->

Governmental and Parliamentary reviews have described PFD reports as "under-utilised" 
(Home Office, 2023), citing minimal repository functionality (Justice Committee, 2021). The 
current system is noted as a “missed opportunity” for learning and reform (BMJ, 2024).

This underuse largely stems from a series of practical and technical barriers: reports are 
published with inconsistent formats, incomplete metadata, and widespread use of digitally 
scanned images that are invisible to conventional search and text analysis tools. Around 
73% of reports lack thematic labels, and those that exist are inconsistently applied and 
frequently inaccurate (Bremmer et al., 2023; Zhang and Richards, 2023). As a result, 
researchers and policymakers who wish to learn from this resource must screen, collate, 
and extract relevant information report-by-report, demanding months or even years of 
researcher capacity. One review manually screened and categorised as many as 3897 reports 
by hand (Dernie, et al., 2023).

Existing resources, notably the *Preventable Deaths Tracker*, provide summary statistics and 
metadata, but lack support for report-text searching, thematic discovery, or automatic information 
extraction. There remains a critical gap in the infrastructure for automating the myriad of 
manual tasks in PFD report analysis and for lowering the barrier to research.

*PFD Toolkit* addresses this need by providing robust automation for every stage of PFD data 
processing. It reliably scrapes, cleans, and standardises both text and image-based data, 
enabling flexible thematic coding and feature extraction across the repository.

This makes possible – for the first time – timely, up-to-date, and flexible analysis of the 
entire national archive of PFD reports. In doing so, the toolkit closes the gap between 
available evidence and actionable learning, ultimately supporting efforts to prevent 
future deaths.



# Key Features

<!-- Dan: do you think I should mention the span identification here? It's not really a core
feature imo, though it does seem to reduce/eliminate false positives. -->

1. **Rapid data access.** Instantly loads the latest Prevention of Future Deaths data, 
updated weekly.
2. **Three-layer scraping.** Handles HTML, .pdf, and scanned image reports using OCR and 
vision-enabled large language models (V-LLMs) for comprehensive data extraction.
3. **Automated text cleaning.** Corrects spelling, grammar, and formatting issues across 
diverse report structures.
4. **Flexible natural language querying.** Screens and filters thousands of reports using 
plain-English research queries.
5. **Topic modelling.** Discovers recurring themes contained within a given selection of 
PFD reports.
6. **Custom feature extraction.** Pulls structured fields and variables from unstructured 
report text.
7. **Batch processing.** Supports parallel batch processing of both CPU and LLM tasks, 
enabling efficient handling of large datasets.


# Example usage

The example below showcases key features #1 and #4. With just a few lines of code and
minutes-long runtime, users can automate what would otherwise take months of manual 
effort: downloading and screening thousands of reports into a research-ready dataset.


```python
from pfd_toolkit import load_reports, LLM, Screener

# -- Load reports into a pandas DataFrame --
reports = load_reports(
  start_date="2013-01-01", end_date="2025-07-01")

# -- Set up LLM client --
llm_client = LLM(api_key=<YOUR_OPENAI_API_KEY>)

# -- Screen/filter reports by a natural language query --
query="Concerns related to detention under the Mental Health Act"

screener = Screener(reports=reports, llm=llm_client)

filtered_df = screener.screen_reports(
                          user_query=query)
```

# Evaluation

The toolkit’s effectiveness is demonstrated in a companion publication, where it automated 
an Office for National Statistics (ONS) research workflow - reducing months of manual screening 
and analysis to a matter of minutes, matching human-level extraction accuracy.


# Availability and documentation

*PFD Toolkit* is available on [GitHub](https://github.com/Sam-Osian/PFD-toolkit) and PyPI 
(via `pip install pfd_toolkit`). Full documentation and tutorials are available at:
https://sam-osian.github.io/pfd-toolkit/. The package is unit-tested with 74% coverage and 
is actively maintained. 

Community contributions and feedback are welcome via 
[GitHub Issues](https://github.com/Sam-Osian/PFD-toolkit/issues).


# References
