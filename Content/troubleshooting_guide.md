# Troubleshooting Guide

This document will include:
- 401 Unauthorized: token issues
- 403/429: rate limit handling
- 404: wrong repo/path
- 422: invalid search query
- 5xx: retries/backoff

# Troubleshooting Guide (GitHub API)

## Common errors

### 401 Unauthorized — Bad credentials
**Cause:** invalid/expired token or token not provided.
**Fix:**
- Re-check that token is copied correctly
- In Colab: ensure headers contain `Authorization: Bearer <TOKEN>`
- Make sure token is active in GitHub settings

### 403 Forbidden — Rate limit or insufficient permissions
**Cause:** GitHub API rate limit exceeded OR token has limited access.
**Fix:**
- Check rate limits via `GET /rate_limit`
- Look at headers:
  - `X-RateLimit-Remaining`
  - `X-RateLimit-Reset` (when quota resets)
- Reduce request frequency, use pagination carefully, cache results if possible

### 429 Too Many Requests
**Cause:** too many requests in a short time (less common in GitHub REST, but possible via abuse detection).
**Fix:**
- Add retries with backoff (wait and retry)
- Slow down request loops

### 5xx Server Errors
**Cause:** GitHub temporary issue.
**Fix:**
- Retry with backoff
- Log status code and response body
