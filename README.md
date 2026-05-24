# FUTURE_CS_03 – API Security Risk Analysis

> **Future Interns | Cyber Security Track | Task 3**

---

## Overview

This repository contains my submission for **Task 3** of the Future Interns Cyber Security Internship — an **API Security Risk Analysis** conducted on a public demo REST API.

The goal of this task was to perform a read-only security audit of a public API, identify common vulnerabilities and misconfigurations, and document everything in a professional security report — similar to what real AppSec consultants deliver to SaaS clients.

---

## Target API

| Field | Details |
|---|---|
| **API Name** | JSONPlaceholder |
| **Base URL** | https://jsonplaceholder.typicode.com |
| **Type** | Public Demo / Test REST API |
| **Auth Required** | No |
| **Resources** | /posts, /comments, /users, /albums, /photos, /todos |

JSONPlaceholder is a free, public API built specifically for testing and learning. It serves ~3 billion requests per month and is widely used by developers to practice frontend and API work.

---

## Tools Used

- **Postman** – API endpoint testing and response inspection
- **Browser DevTools** (Chrome/Firefox, Network tab) – Header analysis, CORS inspection
- **OWASP API Security Top 10** – Risk classification framework
- **Google Docs / ReportLab** – Report writing and PDF generation

---

## Scope & Ethics

**What was done:**
- Read-only GET requests to all major endpoints
- Response header inspection
- Response body structure analysis
- Documentation-based risk assessment

**What was NOT done:**
- No exploitation or bypass attempts
- No brute force or credential testing
- No flooding or DoS testing
- No access to private or production APIs

> All testing was conducted ethically and for educational purposes only. JSONPlaceholder is a public demo API designed specifically for this kind of learning.

---

## Methodology

1. **Documentation Review** – Read the official API guide and understood endpoint structure
2. **Endpoint Testing** – Sent GET requests via Postman to all available resources
3. **Header Inspection** – Checked response headers for security misconfigurations
4. **Risk Identification** – Compared findings against OWASP API Top 10 categories
5. **Report Writing** – Documented each finding with severity, impact, and remediation

---

## Findings Summary

| ID | Finding | Severity |
|---|---|---|
| F-01 | No Authentication on Any Endpoint | 🔴 HIGH |
| F-02 | Excessive Data Exposure – /users | 🔴 HIGH |
| F-03 | Email Addresses Exposed in /comments | 🟠 MEDIUM |
| F-04 | No Rate Limiting Detected | 🟠 MEDIUM |
| F-05 | Missing Security Headers | 🟠 MEDIUM |
| F-06 | No Authorization / BOLA Pattern | 🟠 MEDIUM |
| F-07 | No Input Validation on Write Endpoints | 🟢 LOW |
| F-08 | API Versioning Not Implemented | 🟢 LOW |
| F-09 | Verbose Error Handling | 🟢 LOW |

**Total: 2 High | 4 Medium | 3 Low**

Full details, evidence, business impact, and remediation for each finding are in the report.

---

## Repository Structure

```
FUTURE_CS_03/
│
├── README.md                          ← You are here
│
├── report/
│   └── API_Security_Risk_Analysis_FUTURE_CS_03.pdf   ← Full report (PDF)
│
├── screenshots/
│   ├── 01_get_posts_response.png      ← Postman: GET /posts
│   ├── 02_get_users_response.png      ← Postman: GET /users (data exposure)
│   ├── 03_get_comments_emails.png     ← Postman: GET /comments (email fields)
│   ├── 04_get_user_1_detail.png       ← Postman: GET /users/1 (PII fields)
│   ├── 05_response_headers.png        ← DevTools: Header inspection
│   ├── 06_missing_auth_header.png     ← Postman: No auth required
│   ├── 07_rate_limit_test.png         ← Multiple requests, no 429 returned
│   └── 08_404_error_response.png      ← GET /posts/9999 error response
│
└── docs/
    └── methodology_notes.md           ← Personal notes on testing approach
```

---

## References

| Resource | Link |
|---|---|
| JSONPlaceholder | https://jsonplaceholder.typicode.com |
| OWASP API Security Top 10 | https://github.com/OWASP/API-Security |
| API Security Checklist (Shieldfy) | https://github.com/shieldfy/API-Security-Checklist |
| Public APIs for Testing | https://github.com/public-apis/public-apis |
| Postman | https://www.postman.com |
| Future Interns LinkedIn | https://www.linkedin.com/company/future-interns/ |

---

## About This Task

APIs are at the core of modern SaaS products. API security audits are a real, billable service offered by cybersecurity agencies and AppSec teams. This task simulates that work in a safe, educational environment.

Skills practised: API testing, authentication & authorization assessment, OWASP framework application, security documentation, risk communication in business language.

---

**Internship:** Future Interns – Cyber Security Track  
**Repository:** FUTURE_CS_03  
**Task:** Task 3 – API Security Risk Analysis  
**Intern:** Steven Anthony
