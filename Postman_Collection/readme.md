# Postman_Collection (Colab Notebook)

The assignment mentions Postman, but I used **Google Colab** for extraction (bonus approach).
This folder contains the executable notebook:

- `github_api_test_notebook.ipynb` — GitHub API extraction notebook

## What the notebook does
1) Loads GitHub token from Colab secrets (`GITHUB_TOKEN`)
2) Builds request headers for GitHub REST API
3) Validates authentication (`GET /user`)
4) Runs required reports:
   - Search public repositories
   - Fetch commits (with pagination)
   - Fetch repository contents
5) Saves output samples as JSON files (stored in `Content/Samples/`)
