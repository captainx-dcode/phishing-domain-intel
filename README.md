# Phishing Domain Passive Intelligence Collector

A Python command-line tool that gathers publicly available intelligence about a suspicious domain (WHOIS registration data and VirusTotal reputation) to help a threat intelligence team decide whether to block or report it.

> **Status:** Phase 1 (Planning) complete. Update the checklist below after each step.

## SDLC Progress

- [x] Phase 1: Planning and Scope
- [ ] Phase 2: Design
- [ ] Phase 3: Implementation
- [ ] Phase 4: Testing
- [ ] Phase 5: Deployment and Usage
- [ ] Phase 6: Maintenance and Improvements

---

## Phase 1: Planning and Scope

### 1.1 Overview

| Item | Detail |
|---|---|
| Name | Phishing Domain Passive Intelligence Collector |
| Purpose | Collect WHOIS and VirusTotal data on a suspect domain to support block/report decisions |
| Users | Threat intelligence analysts and security team members |
| Language | Python 3 |

### 1.2 Goals and Objectives

1. Accept a domain name from the analyst and validate it.
2. Retrieve WHOIS data (registrar, creation/expiry dates, name servers, registrant organization if public).
3. Query VirusTotal for domain reputation (detection counts, categories, resolved IPs, last analysis date).
4. Present findings in a clear, consistent format, with optional JSON output.
5. Handle errors gracefully (invalid input, API failures, rate limits, missing WHOIS fields) without crashing.

**Success criteria:** For a given domain, the script returns a readable summary combining WHOIS and VirusTotal data in a reasonable time, and fails safely with a clear message when a source is unavailable.

### 1.3 Scope

**In scope**
- Passive, read-only lookups against third-party sources (WHOIS and the VirusTotal API)
- Domain input validation and normalization
- Parsing, summarizing, and displaying results
- Basic error handling, timeouts, and rate-limit awareness
- Secure handling of the API key

**Out of scope (this version)**
- Active reconnaissance: port scanning, vulnerability scanning, crawling, or connecting to the target domain
- Submitting domains or URLs to VirusTotal for fresh scanning (can make data public)
- Automated blocking or reporting actions
- Bulk or continuous monitoring
- Database storage or a web UI

### 1.4 Constraints and Assumptions

- A valid VirusTotal API key is required. The free tier is rate limited and the script must respect it.
- WHOIS data varies by registrar and TLD and is often redacted, so missing fields are expected.
- The tool provides evidence for human decision-making. It does not issue final verdicts.

### 1.5 Ethical and Legal Considerations

**Passive-only principle**
- The script only queries third-party services and never sends traffic to the suspect domain's infrastructure.
- Analysts should not open the suspect domain in a normal browser as part of this workflow.

**Authorization and purpose limitation**
- Use is limited to legitimate defensive purposes within the team's mandate.
- Follow organizational policy and the computer misuse laws of your jurisdiction.

**Terms of service compliance**
- Follow VirusTotal's API terms and rate limits. The free public API is for non-commercial use; confirm licensing suits your team.
- Use lookup (GET) endpoints only, to avoid publishing internal or sensitive indicators.

**Privacy and data protection**
- WHOIS records may contain personal data. Collect and store only what is needed and comply with regulations such as GDPR.
- Do not repurpose or publicly share personal registrant data.

**Responsible data handling**
- Never hardcode the API key. Load it from an environment variable and keep it out of version control.
- Do not log secrets.
- Defang indicators in reports (for example `example[.]com`).
- Treat results as intelligence, not proof. Verify before blocking or reporting.

**Accuracy and accountability**
- Record data sources and timestamps in the output so findings can be audited.

### 1.6 High-Level Requirements

| Type | Requirement |
|---|---|
| Functional | Validate domain input |
| Functional | Fetch and parse WHOIS data |
| Functional | Fetch VirusTotal domain report |
| Functional | Display a combined summary (optionally export to JSON) |
| Non-functional | Timeouts on all network calls |
| Non-functional | Clear error messages and no unhandled exceptions |
| Non-functional | API key stored securely |
| Non-functional | Readable, commented, modular code |

### 1.7 Risks and Mitigations

| Risk | Mitigation |
|---|---|
| API rate limiting | Handle HTTP 429; add delays or retries |
| Redacted or inconsistent WHOIS data | Treat fields as optional; display "Not available" |
| API key leakage | Environment variables and `.gitignore` |
| Malformed or malicious input | Strict domain validation before any lookup |
| Misinterpreting results | Include a disclaimer; recommend analyst review |

---

## Phase 2: Design

_To be completed._

Planned contents:
- Function structure (e.g., `validate_domain()`, `get_whois()`, `get_virustotal_report()`, `display_results()`)
- Data flow diagram
- Output format (console and JSON)
- Error handling strategy

## Phase 3: Implementation

_To be completed._

Planned contents:
- Dependencies and setup
- Notes on key implementation decisions
- Changelog of steps completed

## Phase 4: Testing

_To be completed._

Planned contents:
- Test cases (valid/invalid domains, missing WHOIS fields, API errors, rate limits)
- Results and fixes

## Phase 5: Deployment and Usage

_To be completed._

### Setup (draft)

```bash
git clone <your-repo-url>
cd <repo-folder>
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
export VT_API_KEY="your_api_key_here"   # Windows (PowerShell): $env:VT_API_KEY="your_api_key_here"
python main.py
```

## Phase 6: Maintenance and Improvements

_To be completed._

Ideas backlog:
- Bulk domain input from a file
- Defanged report export
- Additional passive sources

---

## Disclaimer

This tool is for authorized, defensive security research only. Results are intelligence to support human review and are not proof of malicious activity. Always verify findings before taking blocking or reporting action.

## Changelog

| Date | Phase | Change |
|---|---|---|
| YYYY-MM-DD | 1 | Initial planning and scope documented |
