# Troubleshooting Guide (GitHub API)

This document describes common issues during GitHub REST API extraction and how to resolve them.

## 1) 401 Unauthorized — “Bad credentials”
**Symptoms**
- Status: `401`
- JSON message: `Bad credentials`

**Fix checklist**
1. Token is actually loaded (not None/empty)
2. Header is correct:
   - `Authorization: Bearer <TOKEN>`
3. Token is not expired / not revoked
4. You are using the token value, not the token name

## 2) 403 Forbidden — permissions or rate limit
**Symptoms**
- Status: `403`
- Message can indicate forbidden or rate limit

**Fix checklist**
1. Confirm token permissions (fine-grained token is allowed for required resources)
2. Check rate limit headers:
   - `X-RateLimit-Remaining`
   - `X-RateLimit-Reset`
3. If remaining = 0 → wait until reset time, then retry

## 3) 429 Too Many Requests
**Symptoms**
- Status: `429`

**Fix checklist**
1. Add waiting/backoff logic:
   - sleep for a short period (e.g., 2–10 seconds)
2. Reduce request frequency
3. Use pagination responsibly (avoid huge loops)

## 4) 5xx errors (GitHub server issues)
**Symptoms**
- Status: `500`, `502`, `503`, `504`

**Fix checklist**
1. Retry with exponential backoff
2. Limit retries (e.g., 3 attempts), then fail gracefully
3. Log status code and response snippet for diagnosis

## 5) JSON parsing or unexpected structure
**Symptoms**
- KeyError / missing fields

**Fix checklist**
1. Print a small response sample
2. Use safe access:
   - `.get("items", [])`
3. Validate response type (dict vs list)

## General Best Practices
- Validate auth early using `GET /user`
- Log: status code + endpoint + main params
- Keep samples small (per_page low, limited pagination pages)
- Never print or commit the token
