# Interview Task: Threat Feed Aggregator API

This assignment tasks you with building a threat intelligence API that aggregates data from multiple security providers. You'll create a service that accepts IP addresses and URLs as inputs, queries external threat intelligence platforms (AbuseIPDB and VirusTotal), and returns normalized security assessments. This exercise evaluates your ability to develop type-safe APIs, integrate with third-party services, and design clean data models.

## Recommended Tech Stack
Candidates are encouraged to use NestJS or another TypeScript-based API framework.

Suggested Stack:
- Backend: NestJS + TypeScript
- HTTP Client: HttpService or Axios
- Env Management: @nestjs/config

## Objective
Build a REST API that:
- Accepts a list of IP addresses or URLs
- Queries the following third-party APIs:
  - AbuseIPDB – for IP addresses
  - VirusTotal – for IPs and URLs
- Returns a unified threat report per input

## Endpoint Specification
POST /threat-report

Request Body:
```json
{
  "targets": [
    "8.8.8.8",
    "https://malicious-site.com"
  ]
}
```

Expected Response:
```json
[
  {
    "target": "8.8.8.8",
    "malicious": false,
    "abuseConfidenceScore": 0,
    "virusTotalReports": 0,
    "tags": []
  },
  {
    "target": "https://malicious-site.com",
    "malicious": true,
    "abuse_confidence_score": null,
    "virus_total_reports": 11,
    "tags": [
      "malware",
      "phishing"
    ]
  }
]
```

## API Key Setup
You will need free API keys to use the following services:
- VirusTotal – Sign up and access your key from your profile. `https://www.virustotal.com/gui/join-us`
- AbuseIPDB – Register for a free account to get your key. `https://www.abuseipdb.com/register?plan=free`

Use environment variables or configuration files to store your API keys securely during development.

## What You're Evaluating

| Category | What to Look For |
|----------|------------------|
| API Design | RESTful, well-structured controller/service modules |
| Type Safety | Interfaces and DTOs used correctly in NestJS |
| API Integration | Proper HTTP handling, retries, error paths |
| Data Modeling | Unified response structure regardless of source |
| Code Quality | Clean, modular, and easy to follow |
| Error Handling | Graceful handling of partial failures (e.g., one API succeeds, another fails) |

## Stretch Goals
If time allows, candidates are encouraged to add:

### Frontend App
Build a simple frontend UI that:
- Accepts IPs or URLs as input
- Sends requests to the backend
- Displays the threat reports clearly

Frontend can be built using any framework (React, Vue, etc.) or even plain HTML/JS. Focus on functionality, not styling. 

### Caching
Add basic caching of recent results using in-memory storage or Redis to reduce external API calls.

### More
Think about other enhancements you would make to this app to make it production ready
