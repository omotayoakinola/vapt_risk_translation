# Methodology and Assumptions

This explains how the risk scores and dollar figures in the Risk Register were produced. This is a simulated scenario built on a public sample pentest report. All figures are illustrative estimates, not real client data.

## Scenario
* Business: Acuart Gallery, a fictional online art retailer taking card payments
* Customers in Nigeria and the EU
* Annual revenue of $5 million, about $13,700 per day
* 10,000 customer records, including PII and card details

## Scoring Method
Risk score is likelihood multiplied by impact, following the NIST SP 800 30 approach. Each factor is scored from 1 to 5, so the maximum score is 25.

### Likelihood scale
* 1 Rare
* 2 Unlikely
* 3 Possible
* 4 Likely
* 5 Almost certain

Likelihood was raised where the flaw can be exploited by anyone on the internet, needs no login, and can be exploited with free, automated tools such as `sqlmap`. It was lowered where exploitation needs complex user interaction or an already authenticated account.

### Impact scale (financial guide)
* 1 Under $10,000
* 2 $10,000 to $30,000
* 3 $30,000 to $150,000
* 4 $150,000 to $400,000
* 5 Above $400,000

Impact is placed using the midpoint of each finding's financial exposure range, then adjusted upward where regulatory or reputational harm is expected to be severe.

### Score bands
* 20 to 25 Critical
* 12 to 19 High
* 6 to 11 Medium
* 1 to 5 Low

## Financial Assumptions
Each exposure range is built from the cost categories that apply to the finding.
* **Regulatory fines and legal costs:** Scaled to the revenue and record count above, with reference to GDPR and NDPA penalty rules.
* **Forensics and recovery:** Independent investigation, system clean up, and post remediation validation testing.
* **Customer notification:** Estimated at roughly $20 per record, equating to approximately $200,000 for a compromise of all 10,000 records.
* **Fraud and chargebacks:** Fraudulent transactions, payment gateway integration penalties, and card dispute fees.
* **Lost business and brand damage:** Estimated as a share of annual revenue, using the daily revenue figure for outage time and subsequent customer churn.
* **Overall check:** A full data breach costs roughly $100 per record in this model, which gives about $1 million for 10,000 records. This sits inside the $500,000 to $1,500,000 range for RISK_2026_001.

Ranges are given instead of single numbers because real breach costs vary widely. The combined total is a ceiling, since the findings would not all be exploited in one event.

## Technical Rating Notes
* CVE numbers do not apply to custom application flaws, so CWE IDs are used.
* CVSS v3.1 scores are my own estimates and should be verified with the FIRST CVSS calculator.
* Business ratings can differ from the pentester's technical ratings. For example, reflected XSS was rated Medium in the technical report but mapped to a High business impact here due to the high volume of daily storefront traffic and the severe reputational risk of targeted customer phishing campaigns mimicking the company's corporate domain.

## Compliance Mapping Approach
Each finding is mapped to ISO/IEC 27001:2022 Annex A controls, NIST CSF v2.0 categories, PCI DSS v4.0 requirements and, where personal data is at risk, GDPR Article 32 and the Nigeria Data Protection Act (NDPA).

## Findings Selection

The source report contains six findings. Five were selected for translation into business risk, and one was left out.

### Selected
* **WEB_VUL_01 SQL injection (High in report):** Selected because it exposes the full customer database, including card data. It carries the largest regulatory and financial impact.
* **WEB_VUL_04 Login bypass (High in report):** The report labels this broken authentication, but it is exploited through SQL injection. It is kept as a separate risk because the business impact is different: account takeover and fraud, not data extraction. It also leads to different controls, such as multi factor authentication and login monitoring.
* **WEB_VUL_03 Stored XSS (High in report):** Selected because the malicious script persists and affects every visitor to the page, which makes it a customer trust and fraud risk.
* **WEB_VUL_02 Reflected XSS (Medium in report):** Selected because it affects the public storefront and enables phishing in the company's name. It is rated High here because of the business context.
* **WEB_VUL_06 Clickjacking and iframe injection (Low in report):** Selected because it shows a different type of control. The fix is configuration based (security headers) and not a code fix, and the harm is credential theft and reputation damage.

### Not selected
* **WEB_VUL_05 HTML injection (Low in report):** Left out because it shares the same root cause and the same fixes as the two XSS findings (input filtering and output encoding). Including it would repeat the same business risk.

### Selection criteria
* Business impact: financial, regulatory and customer harm
* Exploitability: how easily an outsider can exploit the flaw
* Variety: data exposure, authentication, client side attacks and configuration, so the register shows different risk themes and control types
* Avoiding duplication: findings with the same root cause and same remediation are covered once

The original report is a publicly available sample and is not included in this repository.

## Limitations
* The business context is invented to make the findings meaningful.
* Dollar figures are assumptions and not based on real incident data.
* A real engagement would use asset values, historical threat intelligence, and input from internal business risk owners.
