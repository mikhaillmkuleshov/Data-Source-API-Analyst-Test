# API Documentation (GitHub)

This document will describe:
- endpoints used (Search Repos, Commits, Contents)
- request logic (headers, params)
- pagination approach
- rate limits handling
- error handling

## Search Repositories

Endpoint:
GET /search/repositories

Parameters:
- q (string): search keyword
- per_page (int): number of results per page
- page (int): page number

Response:
Returns a JSON object containing repository metadata.
