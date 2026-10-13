# Executive Risk Briefing

**TO:** Board of Directors
**FROM:** Omotayo Akinola, GRC Analyst
**DATE:** October 12, 2026
**SUBJECT:** Q4 2026 Web Application Vulnerability and Risk Translation

### Executive Summary

Our online store currently carries a High overall cyber risk, driven by two Critical flaws that could expose our customer database and payment records. If exploited, the five identified issues carry a combined estimated financial exposure of $725,000 to $2.41 million, against annual revenue of approximately $5 million.

These estimates combine industry breach cost benchmarks, regulatory penalties under the NDPA, GDPR and PCI DSS, legal fees, and expected customer churn. The full workings are in the risk register.

Most of this exposure can be substantially reduced through targeted engineering fixes over the next 30 days, at a fraction of the cost of a single data breach. An independent retest will confirm the remaining risk after the fixes.

### Top 3 Business Risks

**Customer Database Theft (RISK_2026_001, Critical)**
An unauthenticated external attacker can extract sensitive customer profiles and payment records.
* Financial Exposure: $500,000 to $1,500,000
* Impact Scope: Statutory fines under the NDPA and GDPR, PCI DSS compliance penalties, legal fees and immediate customer churn.

**Account Takeover Flaw (RISK_2026_002, Critical)**
Weaknesses in application authentication allow attackers to log into arbitrary user accounts without valid credentials.
* Financial Exposure: $100,000 to $400,000
* Impact Scope: Fraudulent orders, merchant chargebacks, and legal and customer support costs.

**Malicious Scripts on Customer Pages (RISK_2026_003, High)**
Stored cross site scripting (XSS) allows attackers to place malicious code on profile pages that runs silently in customer browsers.
* Financial Exposure: $75,000 to $300,000
* Impact Scope: Stolen user sessions or shoppers silently redirected to fraudulent payment pages, damaging customer trust.

### Strategic Roadmap

**By October 19, 2026 (7 day target):**
Fix the critical database access and authentication flaws (RISK_2026_001 and 002) at code level, by securing database queries and correcting the authentication logic. Add multi factor authentication (MFA) and enhanced login monitoring as supporting controls.

**By October 26, 2026 (14 day target):**
Fix the stored script injection in customer profile input fields (RISK_2026_003).

**By November 11, 2026 (30 day target):**
Resolve the public search parameter and guestbook input validation bugs, and deploy HTTP security headers (RISK_2026_004 and 005).

**By November 25, 2026:**
Complete an independent retest to confirm every fix works, then formally close the risks in the register.

**Ongoing:**
Quarterly automated security testing and secure code review before every major release.

### Decision Requested

Approve emergency engineering resources for the 7 day mitigation sprint, led by the Head of Technology, and approve the budget for the independent validation retest.
