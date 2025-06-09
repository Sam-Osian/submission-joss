---
title: 'PFD Toolkit: Unlocking Prevention of Future Death Reports for Research'
tags:
  - containers
  - docker
  - psychology
  - reproducibility
  - Docker
authors:
 - name: Sam Osian
   orcid: 0000-0002-4387-3819
   affiliation: 1
affiliations:
 - name: University of Liverpool
   index: 1
date: 9 June 2025
bibliography: paper.bib
---


## Summary

Prevention of Future Death (PFD) reports are issued by coroners in England and Wales when an inquest identifies risks that, if left unaddressed, could lead to further deaths. These reports are published online as a public resource, aiming to alert relevant organisations and the public to preventable hazards. However, despite their potential for system learning and improvement, PFD reports remain persistently underused in research and policy. Much of their value is lost because the reports are difficult to find, search, and analyse in bulk.  

**PFD Toolkit** is a Python package created to address these challenges. The toolkit automates the full pipeline of accessing, cleaning, and structuring PFD data, making this vital information readily available and usable. By integrating advanced natural language processing – including large language models (LLMs) and vision-based models – the toolkit can extract structured data from both text-based and scanned, image-based reports. Users can search thousands of reports with flexible, plain-English queries and assign custom thematic labels or extract specific features at scale.

This approach eliminates the need for laborious manual screening and coding, dramatically reducing the time and expertise required to turn PFD data into actionable insights. In effect, the toolkit transforms an underused, fragmented archive into a living resource for research, public health, and safety policy, enabling the rapid identification of emerging risks and timely policy response.

## Statement of need

Both UK Government and independent reviews repeatedly describe PFD reports as “under-utilised” (Home Office, 2023), and highlight the repository’s minimal functionality (Justice Committee, 2021). In the literature, the current system is noted as a “missed opportunity” for learning and reform (BMJ, 2024).

The persistent underuse of PFD reports is rooted in a series of practical and technical barriers. The official Courts and Tribunals website hosts the reports in a variety of inconsistent formats, often with missing or incomplete metadata. Many reports are available only as scanned images, rendering them invisible to conventional search and text analysis tools. Even basic categorisation is lacking; around 73% of PFD reports have no assigned thematic label at all, and the labels that do exist are inconsistently applied and frequently inaccurate (Bremmer et al., 2023; Zhang and Richards, 2023). As a result, researchers and policymakers who wish to learn from this resource face a burdensome, error-prone process: manually screening, collating, and extracting relevant information report by report, often accepting incomplete or partial datasets as a compromise.

Previous efforts to improve access, such as the **Preventable Deaths Tracker**, provide summary statistics and basic metadata, but do not allow users to search within the full report text, apply custom thematic coding, or extract features from the reports. There remains a critical gap in the infrastructure needed to systematically analyse the detailed content of PFD reports and connect case-level findings to wider trends.

**PFD Toolkit** addresses this unmet need by providing robust automation for every stage of PFD data processing. It reliably scrapes and updates the latest reports, uses LLMs and vision-based models to extract and standardise both text and image-based data, and offers users fine-grained control over thematic coding and feature extraction. This makes possible, for the first time, comprehensive, up-to-date, and flexible analysis of the entire national archive of PFD reports. By lowering the technical barriers and enabling new forms of analysis, the toolkit supports researchers, clinicians, and policymakers to make meaningful use of PFD data. This closes the gap between available evidence and actionable learning, ultimately supporting efforts to prevent future deaths.




<!-- # Summary

The Experiment Factory [@vanessa_sochat_2017_1059119] is Open Source software that makes it easy to generate reproducible behavioral experiments. It offers a browsable, and tested [library](https://expfactory.github.io/experiments/) of experiments, games, and surveys, support for multiple kinds of databases, and [robust documentation](https://expfactory.github.io/expfactory/) for the provided tools. A user interested in deploying a behavioral assessment can simply select a grouping of paradigms from the web interface, and build a container to serve them.

![img/portal.png](img/portal.png)


# Challenges with Behavioral Research

The reproducibility crisis [@Ram2013-km, @Stodden2010-cu, @noauthor_2015-ig, @noauthor_undated-sn, @Baker_undated-bx, @Open_Science_Collaboration2015-hb] has been well met by many efforts [@Belmann2015-eb, @Moreews2015-dy, @Boettiger2014-cz, @Santana-Perez2015-wo, @Wandell2015-yt] across scientific disciplines to capture dependencies required for a scientific analysis. Behavioral research is especially challenging, historically due to the need to bring a study participant into the lab, and currently due to needing to develop and validate a well-tested set of paradigms. A common format for these paradigms is a web-based format that can be done on a computer with an internet connection, without one if all resources are provided locally. However, while many great tools exist for creating the web-based paradigms [@De_Leeuw2015-zw, @McDonnell2012-ns], still lacking is assurance that the generated paradigms will be reproducible. Specifically, the following challenges remain:

 - **Dependencies** such as software, experiment static files, and runtime variables must be captured for reproduciblity.
 - Individual experiments and the library must be **version controlled.**
 - Each experiment could benefit from being maintianed and tested in an **Open Source** fashion. This means that those knowledgable about the paradigm can easily collaborate on code, and others can file issues and ask questions.
 - Tools must allow for **flexibility** to allow different libraries (e.g., JavaScript).
 - The final product should be **easy to deploy** exactly as the creator intended.

The early version of the Experiment Factory [@Sochat2016-pu] did a good job to develop somewhat modular paradigms, and offered a small set of Python tools to generate local, static batteries from a single repository. Unfortunately, it was severely limited in its ability to scale, and provide reproducible deployments via linux containers [@Merkel2014-da]. The experiments were required to conform to specific set of software, the lack of containerization meant that installation was challenging and error prone, and importantly, it did not meet the complete set of goals outlined above. While the `expfactory-docker` [@noauthor_undated-pi, @Sochat2016-pu] image offered a means to deploy experiments to Amazon Mechanical Turk, it required substantial setup and was primarily developed to meet the specific needs of one lab.

![img/expfactory.png](img/expfactory.png)

# Experiment Container Generation
The software outlined here, "expfactory," shares little with the original implementation beyond the name. Specifically, it allows for encapsulation of all dependencies and static files required for behavioral experimentation, and flexibility to the user for configuration of the deployment. For usage of a pre-existing experiment container, the user simply needs to run the Docker image. For generation of a new, custom container the generation workflow is typically the following:
 
 - **Selection** The user browses a [library](https://expfactory.github.io/experiments/) of available experiments, surveys, and games. A preview is available directly in the browser, and data saved to the local machine for inspection. The preview reflects exactly what will be installed into the container.
 - **Generation** The user selects one or more paradigms to add to the container, and clicks "Generate." The user runs the command shown in the browser on his or her local machine to produce the custom recipe for the container, called a Dockerfile.
 - **Building** The user builds the container (and optionally adds the Dockerfile to version control or automated building on Docker Hub) and uses it in production. The same container is then available for others that want to reproduce the experiment.

At runtime, the user is then able to select deployment customization such as database (MySQL, PostgreSQL, sqlite3, or default of filesystem), and a study identifier.


# Experiment Container Usage
Once a container is generated and it's unique identifier and image layers served in a registry like Docker Hub, it can be cited in a paper with confidence that others can run and reproduce the work simply by using it.

More information on experiment development and contribution to the expfactory tools, containers, or library is provided at the Experiment Factory  <a href="https://expfactory.github.io/expfactory/" target="_blank">official documentation</a>. This is an Open Source project, and so <a href="https://www.github.com/expfactory/expfactory/issues" target="_blank">feedback and contributions</a> are encouraged and welcome.

# References -->
