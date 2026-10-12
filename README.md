# Cyber Risk Translation

## Project Overview
This project simulates the GRC workflow of receiving a technical VAPT (Vulnerability Assessment and Penetration Testing) report, analysing the findings, and translating them into business, financial and compliance risk for executive decision making.

## Scenario and Assumptions
The source is a public sample pentest report for a deliberately vulnerable demo site (the Acunetix test site). I assumed the target is the web store of a fictional online art retailer, Acuart Gallery.
* Annual revenue of $5 million
* 10,000 customer records, including card data
* Customers in Nigeria and the EU
All dollar figures are illustrative assumptions, not real data. CVSS scores are my own estimates, and CWE IDs are used because custom application flaws have no CVE numbers.

## Deliverables
* Risk Register and Translation Matrix: five findings mapped to likelihood, impact, financial exposure, compliance controls and a treatment decision with owner and deadline.
* Executive Risk Briefing: a one page board memo with a summary, top 3 business risks and a remediation roadmap.

## Method
Risk score is likelihood (1 to 5) multiplied by impact (1 to 5), following the NIST SP 800 30 approach. Bands: 20 to 25 Critical, 12 to 19 High, 6 to 11 Medium, 1 to 5 Low. Ratings reflect business context, so some differ from the pentester's technical ratings.

## Frameworks Mapped
ISO/IEC 27001:2022 Annex A, NIST CSF 2.0, PCI DSS, OWASP Top 10, GDPR Article 32 and the Nigeria Data Protection Act.

## Skills Demonstrated
* Risk assessment aligned to NIST SP 800 30
* Simplified cyber risk quantification using stated assumptions
* Control mapping to ISO 27001:2022, NIST CSF 2.0 and PCI DSS
* Regulatory impact analysis (NDPA and GDPR)
* Business impact analysis through asset criticality and operational impact
* Executive communication and risk treatment decisions

## Repository Structure
README.md
Risk_Register
Executive_Briefing
Methodology_and_Assumptions

## Credit and Disclaimer
Findings are based on a publicly available sample pentest report. The original report is not included here. This is a learning project and not a real client engagement.

