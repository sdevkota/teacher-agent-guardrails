# Teacher Agent Guardrails

Guardrails for classroom AI agents that protect students and support teachers.

> Version: 1.0.0 | License: MIT | Status: production-oriented v1 foundation

## Problem

Education agents can personalize learning, but they also risk privacy leakage, over-surveillance, biased feedback, and replacing teacher judgment.

## What this project solves

A classroom deployment checker for student data, teacher oversight, age appropriateness, accommodations, and escalation workflows.

Teacher Agent Guardrails ships as a small, dependency-free CLI and library. It validates a domain-specific JSON packet, emits actionable findings, and gives contributors a concrete surface for adding adapters, richer checks, schemas, and integrations.

## Who it is for

Edtech builders, schools, teachers, student privacy advocates.

## Quick start

```bash
npm test
npm start -- sample
```

Analyze your own packet:

```bash
teacher-agent-guardrails ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | node src/cli.js
```

## Example packet

```json
{
  "classroom": {
    "gradeBand": "6-8",
    "subject": "math"
  },
  "privacy": {
    "storesStudentData": true,
    "retentionDays": 30,
    "parentNotice": true
  },
  "oversight": {
    "teacherCanOverride": true,
    "crisisEscalation": true
  }
}
```

## Library usage

```js
const { analyze } = require("./src/index.js");

const report = analyze({
  "classroom": {
    "gradeBand": "6-8",
    "subject": "math"
  },
  "privacy": {
    "storesStudentData": true,
    "retentionDays": 30,
    "parentNotice": true
  },
  "oversight": {
    "teacherCanOverride": true,
    "crisisEscalation": true
  }
});
console.log(report.summary);
```

## v1 behavior

- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Suggests next actions and contributor extension points.
- Runs fully offline with no API keys and no network access.

## Contribution map

Good first contributions:

- Add FERPA/COPPA policy packs.
- Add teacher dashboards.
- Add bias evals.
- Add accommodation templates.

Larger contributions:

- Add a JSON Schema and compatibility tests.
- Build import/export adapters for popular AI frameworks.
- Add real-world fixtures from public, non-sensitive examples.
- Improve scoring with transparent, documented heuristics.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.

## GitHub Pages

The marketing site lives in `site/index.html`. Enable GitHub Pages from the `site` folder or use the included Pages workflow after publishing.

## Security

This project does not process secrets by default. If you build adapters that touch production systems, keep least privilege, explicit consent, and auditable logs in the design.
