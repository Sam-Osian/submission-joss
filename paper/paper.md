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
 - name: John Pytches
   affiliation: 2
affiliations:
 - name: Department of Primary Care and Mental Health, University of Liverpool, United Kingdom
   index: 1
 - name: Independent Researcher, United Kingdom
   index: 2
date: 9 June 2025
bibliography: paper.bib
---


# Summary

Prevention of Future Death (PFD) reports are issued by coroners in England and Wales when an inquest identifies risks that, if left unaddressed, could lead to further deaths. These reports are published online as a public resource, aiming to alert relevant organisations and the public to preventable hazards. However, despite their potential for system learning and improvement, PFD reports remain persistently underused in research and policy. Much of their value is lost because the reports are difficult to find, search, and analyse in bulk.  

*PFD Toolkit* is a Python package created to address these challenges. The toolkit automates the full pipeline of accessing, cleaning, and structuring PFD data, making this vital information readily available and usable. By integrating advanced natural language processing – including large language models (LLMs) and vision-based models – the toolkit can extract structured data from both text-based and scanned, image-based reports. Users can search thousands of reports with flexible, plain-English queries and assign custom thematic labels or extract specific features at scale.

This approach eliminates the need for laborious manual screening and coding, dramatically reducing the time and expertise required to turn PFD data into actionable insights. In effect, the toolkit transforms an underused, fragmented archive into a living resource for research, public health, and safety policy, enabling the rapid identification of emerging risks and timely policy response.

# Statement of need

Both UK Government and independent reviews repeatedly describe PFD reports as “under-utilised” (Home Office, 2023), and highlight the repository’s minimal functionality (Justice Committee, 2021). In the literature, the current system is noted as a “missed opportunity” for learning and reform (BMJ, 2024).

The persistent underuse of PFD reports is rooted in a series of practical and technical barriers. The official Courts and Tribunals website hosts the reports in a variety of inconsistent formats, often with missing or incomplete metadata. Many reports are available only as scanned images, rendering them invisible to conventional search and text analysis tools. Even basic categorisation is lacking; around 73% of PFD reports have no assigned thematic label at all, and the labels that do exist are inconsistently applied and frequently inaccurate (Bremmer et al., 2023; Zhang and Richards, 2023). As a result, researchers and policymakers who wish to learn from this resource face a burdensome, error-prone process: manually screening, collating, and extracting relevant information report by report, often accepting incomplete or partial datasets as a compromise.

Previous efforts to improve access, such as the **Preventable Deaths Tracker**, provide summary statistics and basic metadata, but do not allow users to search within the full report text, apply custom thematic coding, or extract features from the reports. There remains a critical gap in the infrastructure needed to systematically analyse the detailed content of PFD reports and connect case-level findings to wider trends.

**PFD Toolkit** addresses this unmet need by providing robust automation for every stage of PFD data processing. It reliably scrapes and updates the latest reports, uses LLMs and vision-based models to extract and standardise both text and image-based data, and offers users fine-grained control over thematic coding and feature extraction. This makes possible, for the first time, comprehensive, up-to-date, and flexible analysis of the entire national archive of PFD reports. By lowering the technical barriers and enabling new forms of analysis, the toolkit supports researchers, clinicians, and policymakers to make meaningful use of PFD data. This closes the gap between available evidence and actionable learning, ultimately supporting efforts to prevent future deaths.


# Key Features

- **Rapid data access.** Instantly loads the latest Prevention of Future Deaths data, updated weekly.
- **Automated text cleaning.** Corrects spelling, grammar, and formatting issues across diverse report formats.
- **Flexible natural language querying.** Screens and filters thousands of reports using plain-English research queries.
- **Topic modelling.** Discovers recurring themes contained within a selection of PFD reports.
- **Custom feature extraction.** Pulls structured fields and variables from unstructured report text.
- **Batch AI processing:** Parallelises LLM tasks for efficient handling of large datasets.

# Example usage

```python
#!pip install pfd_toolkit
from pfd_toolkit import load_reports, LLM, Screener, Extractor

# -- Load reports into a pandas DataFrame --
reports = load_reports()

# -- Set up LLM client --
llm_client = LLM(api_key=<YOUR_OPENAI_API_KEY>)

# -- Filter reports by a custom query --
screener = Screener(
  reports=reports,
  llm=llm_client,
  user_query="Concerns related to the Mental Health Act's failure to protect"
)
screened_reports = screener.screen_reports() # Filtered df - only relevant cases

# -- Discover & assign themes --
extractor = Extractor(
  reports=screened_reports,
  llm=llm_client)

extractor.discover_themes(assign=True)
```

# References
