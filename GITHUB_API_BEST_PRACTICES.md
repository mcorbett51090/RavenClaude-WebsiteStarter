# GitHub API Best Practices & Rate Limit Guidelines

> Documented for RavenClaude projects to avoid rate limiting and ensure reliable automation.

## Overview

GitHub enforces rate limits on its REST and GraphQL APIs. These limits apply **per account**, not per repository.

This document codifies safe practices when using the GitHub API for write operations (especially file creation/updates).

## Rate Limits

### Primary Rate Limit
- **Authenticated users**: 5,000 requests per hour
- Applies across **all repositories**

### Secondary Rate Limits (Most Relevant)
- GitHub does not publish exact thresholds.
- Triggered by making **too many requests too quickly**.
- Common with rapid successive `create_or_update_file` or `push_files` calls.
- Can temporarily block or throttle even if under the primary limit.

### Abuse Detection
- GitHub may temporarily restrict access if it detects patterns that appear abusive.
- Rapid file updates are a common trigger.

## Recommended Rules

| Rule | Recommendation | Reason |
|------|----------------|--------|
| **Minimum spacing** | Wait **at least 3 seconds** between write API calls | Avoids secondary rate limits |
| **Burst limit** | Max **5 write operations** per 60 seconds | Prevents triggering abuse detection |
| **Large files (>50KB)** | Prefer regular Git push over API | More reliable for big files |
| **Backoff strategy** | If rate limited: Wait 5 min, then 10 min on repeats | Respects GitHub retry behavior |
| **Batch updates** | Use `push_files` instead of multiple single-file calls | Reduces total API calls |
| **Monitoring** | Check rate limit headers when possible | Helps stay under limits |

## When Working with Large Files

- `index.html` (~90KB) and similar large files should be pushed using normal Git workflow when possible.
- Repeated API updates to large files increase the chance of hitting secondary limits.

## For RavenClaude Projects

This file should be included in repositories that involve:
- Automated file updates via API
- CI/CD or agent-driven changes
- Frequent content synchronization

## References

- [GitHub REST API Rate Limiting](https://docs.github.com/en/rest/overview/rate-limits-for-the-rest-api)
- [Secondary Rate Limits](https://docs.github.com/en/rest/overview/rate-limits-for-the-rest-api#about-secondary-rate-limits)

---

*Maintained for RavenClaude tooling reliability.*