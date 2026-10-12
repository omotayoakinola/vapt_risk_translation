# Risk Register & Technical-to-Business Translation Matrix

## 📋 Risk Context: Acuart Gallery
*This section establishes the operational baseline, regulatory scope, and analytical boundaries used to calculate risk exposure for the Acuart Gallery platform.*

### 🏢 Corporate Profile & Financial Baseline
* **Organization Name:** Acuart Gallery
* **Business Model:** Online art retail platform processing digital card payments.
* **Jurisdictional Scope:** Serves both Nigerian (NDPA) and European Union (GDPR) customer bases.
* **Financial Baseline:** Annual revenue of **\$5,000,000** (~\$13,700 daily operational volume).
* **Asset Footprint:** 10,000 active customer records containing PII and payment data environments.

### 📐 Risk Scoring Framework (NIST SP 800-30 Alignment)
The enterprise utilizes a standard **5x5 Likelihood and Impact Matrix**. Risk scores are calculated as: 
\[\text{Risk Score} = \text{Likelihood} \times \text{Impact}\]

* **Score Classifications:**
  * 🔴 **20 to 25:** Critical Risk
  * 🟠 **12 to 19:** High Risk
  * 🟡 **6 to 11:** Medium Risk
  * 🟢 **1 to 5:** Low Risk

* **Vulnerability Context Note:** Because the underlying technical assessment targeted custom application logic rather than commercial software, Common Weakness Enumeration (CWE) metrics and estimated CVSS v3.1 base scores are used in place of CVE identifiers.

---

## 📊 Acuart Gallery Enterprise Risk Register

| Risk ID | Technical Finding (VAPT / CWE) | Asset Criticality | Threat Scenario | Likelihood (1-5) | Impact (1-5) | Risk Score | Estimated Financial Exposure | Framework & Regulatory Mapping | GRC Recommendation & Treatment | Owner & SLA |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- |
| **RISK_2026_001** | SQL Injection on Artists Page <br><br>`Source: WEB_VUL_01`<br>`CWE-89`<br>`Est. CVSS: 9.8` | **High**<br>(Customer Database) | Unauthenticated external attacker extracts the full database user table, compromising card numbers, emails, phone numbers, and physical addresses. | 5 | 5 | **25**<br>🔴 *Critical* | **\$500,000 - \$1,500,000**<br><br>• Fines/Legal: \$150k-\$400k<br>• Forensics/Recovery: \$100k-\$300k<br>• Notifications: ~\$200k<br>• Lost Business: \$50k-\$600k | • **ISO 27001:** A.8.3, A.8.26, A.8.28<br>• **PCI DSS:** 6.2.4<br>• **GDPR:** Article 32<br>• **NDPA:** Security of Processing<br>• **NIST CSF:** PR.DS | **Mitigate:** Implement parameterized queries, strict input validation, and restrict backend database user privileges. Schedule a validation retest. | Head of Engineering<br><br>⏱️ **7 Days** |
| **RISK_2026_002** | Login Bypass via SQL Injection <br><br>`Source: WEB_VUL_04`<br>`CWE-89`<br>`Est. CVSS: 9.8` | **High**<br>(Customer Accounts / Admin Access) | Attacker bypasses authentication mechanisms to hijack arbitrary user profiles without credentials, viewing saved card profiles and initiating fraudulent transactions. | 5 | 4 | **20**<br>🔴 *Critical* | **\$100,000 - \$400,000**<br><br>• Fraud/Chargebacks: \$30k-\$150k<br>• Support/Ops Recovery: \$20k-\$80k<br>• Loss of Trust: \$50k-\$170k | • **ISO 27001:** A.8.5<br>• **PCI DSS:** Req 8, 6.2.4<br>• **GDPR:** Article 32<br>• **NIST CSF:** PR.AA | **Mitigate:** Remediate raw query logic, enforce system-wide Multi-Factor Authentication (MFA), configure account lockout policies, and deploy automated login monitoring alerts. | Engineering & IT Security<br><br>⏱️ **7 Days** |
| **RISK_2026_003** | Stored XSS in Profile Page <br><br>`Source: WEB_VUL_03`<br>`CWE-79`<br>`Est. CVSS: 5.4` | **High**<br>(User Profiles holding PII/Card data) | Persistent malicious script injected into customer profiles executes within the browsers of viewing users, compromising sessions or force-redirecting shoppers to credential harvesting landing pages. | 4 | 4 | **16**<br>🟠 *High* | **\$75,000 - \$300,000**<br><br>• Incident Response: \$25k-\$75k<br>• User Remediation: \$20k-\$75k<br>• Sales/Brand Damage: \$30k-\$150k | • **ISO 27001:** A.8.26, A.8.28<br>• **PCI DSS:** 6.2.4, 6.4<br>• **GDPR:** Article 32<br>• **NIST CSF:** PR.DS | **Mitigate:** Enforce strict contextual output encoding, sanitize user inputs on arrival, and deploy an enterprise Content Security Policy (CSP). | Engineering Team<br><br>⏱️ **14 Days** |
| **RISK_2026_004** | Reflected XSS in Search & Guestbook <br><br>`Source: WEB_VUL_02`<br>`CWE-79`<br>`Est. CVSS: 6.1` | **High**<br>(Public Storefront Front-end) | Crafted malicious links mimicking legitimate corporate domains target customers, executing arbitrary browser-side scripts to facilitate targeted phishing and session hijacking. | 4 | 3 | **12**<br>🟠 *High* | **\$40,000 - \$150,000**<br><br>• Incident Handling: \$15k-\$50k<br>• Fraud Losses: \$15k-\$60k<br>• Reputation Damage: \$10k-\$40k | • **ISO 27001:** A.8.28, A.8.29<br>• **PCI DSS:** 6.2.4<br>• **NIST CSF:** PR.PS | **Mitigate:** Apply standard cross-site scripting source code remediation (similar to RISK_2026_003) across public input forms and track verification retests. | Engineering Team<br><br>⏱️ **30 Days** |
| **RISK_2026_005** | Iframe Injection / Clickjacking <br><br>`Source: WEB_VUL_06`<br>`CWE-1021`<br>`Est. CVSS: 4.3` | **Medium**<br>(Guestbook Endpoint) | Malicious UI-layer framing embeds hidden inputs or fraudulent forms within trusted pages to trick users into disclosing authorization credentials. | 3 | 3 | **9**<br>🟡 *Medium* | **\$10,000 - \$60,000**<br><br>• Response Operations: \$5k-\$20k<br>• Credential Misuse: \$5k-\$40k | • **ISO 27001:** A.8.9, A.8.28<br>• **PCI DSS:** 6.4<br>• **NIST CSF:** PR.PS | **Mitigate:** Deploy the `X-Frame-Options` browser security header alongside explicit CSP `frame-ancestors` directives. Sanitize the public guestbook fields. | Engineering Team<br><br>⏱️ **30 Days** |

---

## 📈 Executive Aggregation & GRC Methodology Notes

### Combined Financial Exposure Portfolio
* **Total Simulated Enterprise Exposure:** **\$725,000 to \$2,410,000**
* **Strategic Sequencing Statement:** `RISK_2026_001` and `RISK_2026_002` account for over 75% of the organization's aggregate financial liability. Consequently, GRC has designated these for immediate, fast-tracked remediation sprints ahead of standard application maintenance cycles.

### The Value of GRC Translation vs. Technical Testing Rating
A key differentiator in this register is the intentional adjustment of risk profiles based on corporate context rather than pure automated scoring. 

For instance, **Reflected XSS (RISK_2026_004)** was designated as a **Medium** vulnerability by the automated penetration testing tool due to its non-persistent nature. However, because this vulnerability actively impacts the **public-facing storefront**—directly threatening the integrity of the checkout path for a company generating \$5M in e-commerce business—the GRC team escalated the business risk classification to **High**. 

This demonstrates how corporate context, revenue models, and legal liability (NDPA/GDPR) must override isolated software severity ratings to protect enterprise continuity.

