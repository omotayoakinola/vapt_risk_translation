# Risk Register and Translation Matrix

## Assumptions (simulation only)
* Business: Acuart Gallery, a fictional online art retailer taking card payments, serving Nigerian and EU customers
* Annual revenue of $5 million, about $13,700 per day
* 10,000 customer records, including card details
* Likelihood and impact are each scored 1 to 5, and risk score is likelihood multiplied by impact (NIST SP 800 30 approach)
* Score bands: 20 to 25 Critical, 12 to 19 High, 6 to 11 Medium, 1 to 5 Low
* CVE numbers do not apply to custom application flaws, so CWE IDs and estimated CVSS v3.1 scores are used

## RISK_2026_001: SQL Injection on Artists Page
* **Source finding:** WEB_VUL_01
* **Technical finding:** SQL injection, CWE 89, estimated CVSS 9.8
* **Asset criticality:** High (customer database)
* **Threat scenario:** An unauthenticated attacker extracts the full users table, including card numbers, emails, phones and addresses
* **Financial exposure:** $500,000 to $1,500,000 (fines and legal $150,000 to $400,000, forensics and recovery $100,000 to $300,000, customer notification about $200,000, lost business $50,000 to $600,000)
* **Compliance mapping:** ISO 27001:2022 Annex A 8.28, 8.3 and 8.26; PCI DSS 6.2.4; GDPR Article 32; NDPA security of processing duty; NIST CSF 2.0 PR.DS
* **Score:** Likelihood 5, Impact 5, 25, Critical
* **GRC recommendation:** Mitigate. Use parameterised queries and input validation, and restrict database privileges. Owner: Head of Engineering. Due in 7 days, then retest

## RISK_2026_002: Login Bypass via SQL Injection
* **Source finding:** WEB_VUL_04
* **Technical finding:** Authentication bypass through SQL injection, CWE 89, estimated CVSS 9.8
* **Asset criticality:** High (customer accounts, possible admin access)
* **Threat scenario:** An attacker logs in as any user without a password, views saved card data and places fraudulent orders
* **Financial exposure:** $100,000 to $400,000 (fraud and chargebacks $30,000 to $150,000, support and recovery $20,000 to $80,000, lost customer trust $50,000 to $170,000)
* **Compliance mapping:** ISO 27001:2022 Annex A 8.5; PCI DSS Requirement 8 and 6.2.4; GDPR Article 32; NIST CSF 2.0 PR.AA
* **Score:** Likelihood 5, Impact 4, 20, Critical
* **GRC recommendation:** Mitigate. Fix query handling, add multi factor authentication, account lockout and login monitoring. Owner: Engineering with IT Security. Due in 7 days

## RISK_2026_003: Stored XSS in Profile Page
* **Source finding:** WEB_VUL_03
* **Technical finding:** Stored cross site scripting, CWE 79, estimated CVSS 5.4
* **Asset criticality:** High (the page holds customer card and contact data)
* **Threat scenario:** Malicious script saved in a profile runs for every viewer, stealing sessions or redirecting shoppers to a fake payment page
* **Financial exposure:** $75,000 to $300,000 (incident response $25,000 to $75,000, customer remediation $20,000 to $75,000, lost sales and brand damage $30,000 to $150,000)
* **Compliance mapping:** ISO 27001:2022 Annex A 8.28 and 8.26; PCI DSS 6.2.4 and 6.4; GDPR Article 32; NIST CSF 2.0 PR.DS
* **Score:** Likelihood 4, Impact 4, 16, High
* **GRC recommendation:** Mitigate. Encode output, validate input and deploy a Content Security Policy. Owner: Engineering. Due in 14 days

## RISK_2026_004: Reflected XSS in Search and Guestbook
* **Source finding:** WEB_VUL_02
* **Technical finding:** Reflected cross site scripting, CWE 79, estimated CVSS 6.1
* **Asset criticality:** High (public storefront)
* **Threat scenario:** A crafted link that looks like it comes from the brand runs attacker script in a customer's browser, enabling phishing and session theft
* **Financial exposure:** $40,000 to $150,000 (incident handling $15,000 to $50,000, fraud losses $15,000 to $60,000, brand damage $10,000 to $40,000)
* **Compliance mapping:** ISO 27001:2022 Annex A 8.28 and 8.29; PCI DSS 6.2.4; NIST CSF 2.0 PR.PS
* **Score:** Likelihood 4, Impact 3, 12, High
* **GRC recommendation:** Mitigate. Apply the same code fixes as RISK_2026_003, then retest. Owner: Engineering. Due in 30 days

## RISK_2026_005: Iframe Injection and Clickjacking in Guestbook
* **Source finding:** WEB_VUL_06
* **Technical finding:** Improper UI layer restriction, CWE 1021, estimated CVSS 4.3
* **Asset criticality:** Medium (guestbook page)
* **Threat scenario:** A fake login box embedded on the trusted site captures customer passwords
* **Financial exposure:** $10,000 to $60,000 (response costs $5,000 to $20,000, credential misuse $5,000 to $40,000)
* **Compliance mapping:** ISO 27001:2022 Annex A 8.9 and 8.28; PCI DSS 6.4; NIST CSF 2.0 PR.PS
* **Score:** Likelihood 3, Impact 3, 9, Medium
* **GRC recommendation:** Mitigate. Add the X Frame Options header and CSP frame ancestors, and sanitise guestbook input. Owner: Engineering. Due in 30 days

## Summary
* Combined exposure: $725,000 to $2.41 million. Findings 1 and 2 account for most of it, so they are fixed first.
* Some ratings differ from the pentester's technical ratings. For example, reflected XSS was rated Medium in the report and High here because it affects the public storefront. GRC rates risk by business context, not only technical severity.
* All dollar figures and CVSS scores are illustrative estimates for a simulated scenario.
