---
title: 'PFD Toolkit: Unlocking Prevention of Future Death Reports for Research'
tags: 
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
   corresponding: true
   orcid: 0009-0000-7644-6218
   affiliation: "1, 2, 3"
 - name: Jonathan Pytches
   orcid: 0000-0000-0000-0000 # Stop forgetting to ask John to get an orcid!!!
   affiliation: 4
affiliations:
 - name: Department of Primary Care and Mental Health, University of Liverpool, United Kingdom
   index: 1
 - name: Mental health Research for Innovation Centre (M-RIC), Liverpool, United Kingdom
   index: 2
 - name: Civic Health Innovation Labs (CHIL), Liverpool, United Kingdom
   index: 3
 - name: Independent Researcher, United Kingdom
   index: 4
date: 3 June 2025
bibliography: paper.bib
---


# Summary

Prevention of Future Death (PFD) reports are the official mechanism by which coroners in
England and Wales alert individuals, organisations, and agencies to circumstances that may
lead to further deaths. Each report sets out the context of an individual case, details the
factors believed to have contributed, and identifies concerns that, if addressed, could prevent
similar tragedies in the future.

While these documents represent a rare, ground-level view into public safety risks, research
involving PFD reports has been notoriously challenging. The process of assembling a usable 
dataset demands extensive manual effort: locating, downloading, and extracting information from 
thousands of inconsistently formatted documents, many only available as scanned images. This 
labour-intensive process has placed effective analysis out of reach for many researchers 
and policymakers.

*PFD Toolkit* is a Python package developed to overcome these barriers. It automates the 
end-to-end workflow of loading, screening, and analysing PFD data. By combining 
large language models (LLMs) and Vision-LLMs, the toolkit extracts structured information 
from both text and scanned reports. Users can perform plain-English searches of reports, 
assign custom thematic labels, and extract features (such as recurring themes) at scale, 
enabling timely analysis and supporting rapid policy responses.


# Statement of need

Despite repeated calls for reform, PFD reports remain persistently underused in research 
and policy. Governmental and Parliamentary assessments have identified the current system as 
"under-utilised" for public safety, with no existing mechanisms to track recurring issues
[@home_office_hillsborough_2023; @HCJustice2021_CoronerService]. Families of the deceased have 
accused PFD reports as being "nothing more than a paper exercise," criticising a system that
essentially allows known risks to recur without scrutiny [@IAPDC_2023_pfdimpact].

This underuse is largely driven from a series of practical and technical barriers on the
Courts and Tribunals Judiciary website. Users cannot mass-download reports, while the 
reports themselves are published with inconsistent formats, incomplete metadata, and 
widespread use of digitally scanned images which are inaccessible to standard search and 
analysis tools. Around 73% reports lack thematic labels, and those that exist are 
inconsistently applied [@zhang_lessons_2023; @anthony_preventable_2023].

Researchers must screen and extract information from potentially thousands of reports individually, 
an effort that may require months or even years of manual labour [@bremner_systematic_2023]. 
One review on opiod deaths manually screened as many as 3897 reports by hand 
[@dernie_preventable_2023].

The *Preventable Deaths Tracker*[^note] is an existing resource that provides valuable 
summary statistics and metadata on PFD reports, offering the only centralised resource of its 
kind. However, it does not currently support report-text searching, thematic discovery, or 
custom information extraction. There remains a critical gap in the infrastructure for supporting 
scalable analysis and reducing the manual burden associated with PFD research.

[^note]: Available at: <https://preventabledeathstracker.net/>

Researchers have specifically called for embedding technology within the PFD system to automate 
data collection, enhance data quality, and surface critical information from the unstructured
text [@bremner_systematic_2023; @zhang_lessons_2023]


*PFD Toolkit* addresses each of these longstanding challenges by enabling researchers to load and 
clean both text and image-based data; automate thematic discovery; and extract 
structured information at scale. This makes possible – for the first time – timely, comprehensive, 
and flexible analysis across the entire national archive of PFD reports.


# Key Features


1. **Rapid data access.** Instantly loads the latest Prevention of Future Deaths data, 
updated weekly.
2. **Three-layer scraping.** Handles HTML, .pdf, and scanned image reports using 
vision-enabled large language models (V-LLMs) for comprehensive data extraction.
3. **Automated text cleaning.** Corrects spelling, grammar, and formatting issues across 
diverse report structures.
4. **Flexible searching.** Allows users to automatically screen and filter thousands of 
reports using natural language queries.
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

# -- Set up an LLM client --
llm_client = LLM(api_key=<YOUR_OPENAI_API_KEY>)

# -- Screen/filter reports by a natural language query --
query="Reports **explicitly** mentioning detention under the Mental Health Act"

screener = Screener(reports=reports, llm=llm_client)

filtered_df = screener.screen_reports(
                          user_query=query)
```


# Availability and documentation

*PFD Toolkit* is available on PyPI (via `pip install pfd_toolkit`). Full source code is available on [GitHub](https://github.com/Sam-Osian/PFD-toolkit).

Package documentation is available at: https://sam-osian.github.io/PFD-toolkit/. 

We welcome (and actively encourage) community contributions, feedback and feature requests. Please see our [contributions page](https://sam-osian.github.io/PFD-toolkit/contribute/) for more.

The package is unit-tested with 74% coverage and is actively maintained. 


# References
