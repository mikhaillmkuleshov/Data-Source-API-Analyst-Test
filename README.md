# Data-Source-API-Analyst-Test (GitHub API)

Homework assignment for **Data Source API Analyst** role.

## Objective
Demonstrate:
- understanding of REST APIs (auth, requests, pagination, rate limits)
- ability to extract data for “client reports”
- troubleshooting approach (401/403/429/5xx)
- clear documentation and reproducible results

## Client Needs / Reports Covered
1) **Search public repositories**  
2) **Commits for a chosen repository** (with pagination)  
3) **Repository contents** (root folder)

## Deliverables (Artifacts)
- **Google Colab notebook (.ipynb)** with:
  - authentication via GitHub token
  - requests for required endpoints
  - pagination logic (commits)
  - rate limit / error handling approach
  - sample outputs saved to JSON
- **Documentation**:
  - `Content/api_documentation.md` — endpoints, parameters, pagination, rate limits
  - `Content/troubleshooting_guide.md` — common errors + how to debug/fix
- **Output samples (JSON)**:
  - `Content/Samples/search_repositories_sample.json`
  - `Content/Samples/commits_sample_page1.json`
  - `Content/Samples/commits_sample_paginated.json`
  - `Content/Samples/repo_contents_root_sample.json`

## Repository Structure
- `Content/` — documentation + samples
- `Content/Samples/` — JSON output samples
- `Content/Postman_Collection/` — notebook stored here (Colab approach used instead of Postman export)

> Note: The assignment mentions exporting a Postman collection, but I used **Google Colab** (bonus approach). The notebook is provided as the main executable artifact.

## How to Run (Quick)
1. Open the notebook: `Content/Postman_Collection/github_api_test_notebook.ipynb`
2. Add your GitHub token to Colab (Userdata / Secrets) under key `GITHUB_TOKEN`
3. Run cells top-to-bottom

## Reflection (short)
This test was focused on building a reliable extraction workflow:
- validate auth early (`GET /user`)
- log status codes + parse JSON safely
- implement pagination for endpoints that return partial results
- keep sample outputs small and reproducible
