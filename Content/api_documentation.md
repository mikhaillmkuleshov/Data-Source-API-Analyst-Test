# GitHub REST API — Documentation (for the assignment)

## Base
- Base URL: `https://api.github.com`
- API style: REST over HTTP
- Response format: JSON

## Authentication
- Token type: Fine-grained Personal Access Token (PAT)
- Used in header:
  - `Authorization: Bearer <TOKEN>`
  - `Accept: application/vnd.github+json`
  - `X-GitHub-Api-Version: 2022-11-28`

## Endpoints Used (Reports)

### Report 1 — Search Public Repositories
**Endpoint**
- `GET /search/repositories`

**Example**
- URL: `https://api.github.com/search/repositories`
- Query params:
  - `q` — search query (e.g., `data`)
  - `per_page` — results per page (e.g., 5)
  - `page` — page number (e.g., 1)

**Response Notes**
- Top-level fields include:
  - `total_count`
  - `items[]` (array of repositories)

---

### Report 2 — Commits (with Pagination)
**Endpoint**
- `GET /repos/{owner}/{repo}/commits`

**Example**
- URL: `https://api.github.com/repos/{owner}/{repo}/commits`
- Query params:
  - `per_page` (e.g., 10)
  - `page` (e.g., 1..N)

**Pagination**
- GitHub returns commits in pages.
- In this assignment, pagination is handled via a loop over `page` until:
  - empty response, or
  - desired max pages is reached (to keep samples small)

**Response Notes**
- Response is an array of commit objects
- Important fields:
  - `sha`
  - `commit.author.date`
  - `commit.message`
  - `html_url`

---

### Report 3 — Repository Contents
**Endpoint**
- `GET /repos/{owner}/{repo}/contents/{path}`

**Example**
- Root contents:
  - `https://api.github.com/repos/{owner}/{repo}/contents/`
- Optional `path` can be a folder path to inspect deeper.

**Response Notes**
- Response is an array of items (files/folders)
- Common fields:
  - `name`
  - `path`
  - `type` (file/dir)
  - `download_url` (for files)

---

## Rate Limits
GitHub enforces request limits.
The workflow:
- checks status codes
- when receiving `403` or `429`, reads response headers (when available)
- uses backoff / waiting logic (sleep) before retrying

Common headers:
- `X-RateLimit-Remaining`
- `X-RateLimit-Reset`

## Error Handling (High Level)
- `401 Unauthorized`: token missing/invalid
- `403 Forbidden`: permissions or rate limit exceeded
- `429 Too Many Requests`: too many requests in short time
- `5xx`: server-side issues → retry with backoff

## Output Samples
Saved as JSON for review:
- `Content/Samples/search_repositories_sample.json`
- `Content/Samples/commits_sample_page1.json`
- `Content/Samples/commits_sample_paginated.json`
- `Content/Samples/repo_contents_root_sample.json`
