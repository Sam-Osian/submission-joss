---
title: 'PFD Toolkit: Unlocking Prevention of Future Death Reports for Research'
tags:
  - Python
  - Prevention of Future Deaths
  - Coroners' Reports
  - Open Data
  - United Kingdom
  - Public Health
  - Natural Language Processing (NLP)
  - Large Language Models (LLMs)
authors:
 - name: Sam Osian
   corresponding: true
   orcid: 0009-0000-7644-6218
   affiliation: 1
 - name: Jonathan Pytches
   orcid: 0000-0000-0000-0000
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

Prevention of Future Death (PFD) reports are issued by coroners in England and Wales 
when an inquest identifies risks that, if left unaddressed, could lead to further deaths. 
Despite being freely available online, PFD reports are persistently underused by 
researchers. This is largely because they are difficult to find, search, and analyse in bulk.

*PFD Toolkit* is a Python package designed to overcome these barriers. The toolkit automates 
the full pipeline of accessing, cleaning, structuring and analysing PFD data, making 
information contained within them readily usable. By integrating advanced natural language 
processing – including large language models (LLMs) and vision-based models – the toolkit 
can extract structured data from both text-based and scanned, image-based reports. Users 
can search thousands of reports with flexible, plain-English queries and assign custom 
thematic labels or extract specific features at scale.

The toolkit transforms a fragmented archive into a living resource for research and public 
health, enabling rapid identification of emerging risks and timely policy response.



# Statement of need

Governmental and Parliamentary reviews repeatedly describe PFD reports as “under-utilised” 
(Home Office, 2023), citing minimal repository functionality (Justice Committee, 2021). the 
current system is noted as a “missed opportunity” for learning and reform (BMJ, 2024).

This underuse largely stems from a series of practical and technical barriers: reports are 
published with inconsistent formats, incomplete metadata, and widespread use of digitally 
scanned images that are invisible to conventional search and text analysis tools. Around 
73% of reports lack thematic labels, and those that exist are inconsistently applied and 
frequently inaccurate (Bremmer et al., 2023; Zhang and Richards, 2023). As a result, 
researchers and policymakers who wish to learn from this resource may have to screen, 
collate, and extract relevant information report by report, demanding months of researcher 
capacity.

Existing initiatives such as the *Preventable Deaths Tracker* offer summary statistics and 
metadata, but do not support full-text search, custom coding, or detailed information 
extraction. There remains a critical gap in infrastructure for automating the myiad of manual 
tasks in PFD report analysis and lowering the barrier to research.

*PFD Toolkit* addresses this need by providing robust automation for every stage of PFD data 
processing. It reliably scrapes, cleans, and standardises both text and image-based data, 
enabling flexible thematic coding and feature extraction across the national archive. 

This makes possible, for the first time, timely, up-to-date, and flexible analysis of the 
entire national archive of PFD reports. In doing so, the toolkit closes the gap between 
available evidence and actionable learning, ultimately supporting efforts to prevent 
future deaths.



# Key Features

- **Rapid data access.** Instantly loads the latest Prevention of Future Deaths data, updated weekly.
- **Three-layer scraping.** Handles HTML, .pdf, and scanned image reports using OCR and Vision-LLMs for comprehensive data extraction.
- **Automated text cleaning.** Corrects spelling, grammar, and formatting issues across diverse report formats.
- **Flexible natural language querying.** Screens and filters thousands of reports using plain-English research queries.
- **Topic modelling.** Discovers recurring themes contained within a selection of PFD reports.
- **Custom feature extraction.** Pulls structured fields and variables from unstructured report text.
- **Batch AI processing.** Parallelises CPU and LLM tasks for highly efficient handling of large datasets.


# Example usage

<!-- Not sure if I like having this much code; not quite in keeping with other JOSS papers. What else could go here?
 -->

Below, we've automated a previously manual workflow among PFD researchers. [...]


```python
#!pip install pfd_toolkit
from pfd_toolkit import load_reports, LLM, Screener, Extractor

# -- Load reports into a pandas DataFrame --
reports = load_reports(
  start_date="2020-01-01", end_date="2025-01-01"
)

# -- Set up LLM client --
llm_client = LLM(api_key=<YOUR_OPENAI_API_KEY>)

# -- Screen/filter reports by a natural language query --
screener = Screener(
  reports=reports,
  llm=llm_client,
  query="Concerns related to the Mental Health Act"
)
screened_reports = screener.screen_reports()

# -- Discover and assign themes --
extractor = Extractor(
  reports=screened_reports,
  llm=llm_client)

extractor.discover_themes(assign=True)
```

# Evaluation

The toolkit’s effectiveness is demonstrated in a companion publication where it automated 
an Office for National Statistics (ONS) research workflow. [...]


# Availability and documentation

*PFD Toolkit* is available on [GitHub](https://github.com/Sam-Osian/PFD-toolkit) and PyPI 
(via `pip install pfd_toolkit`). Full documentation is available at: 
https://sam-osian.github.io/pfd-toolkit/. Both the documentation and the GitHub repository 
contain tutorials for all core features. 

The package is unit-tested with 73% coverage. 


# References
