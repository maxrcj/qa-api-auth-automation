# QA API Auth Automation

Automated API tests built with **Postman + Newman + JavaScript (Chai)**, targeting the [ReqRes](https://reqres.in) API to validate authentication flows, error handling, and API key requirements.

## What this project covers

- ✅ Positive login flow (`POST /api/login`) — validates status code, response schema, and captures the auth token into an environment variable for reuse in later requests
- ✅ Negative login flow (missing password) — validates status code `400` and the returned error message
- ✅ API key requirement discovery — documented that `/api/*` endpoints now require an `x-api-key` header, and added it across the collection
- ✅ Environment-based configuration (`base_url`, `token`, `api_key`) instead of hardcoded values

## Key finding: two separate auth systems

While building this suite, testing revealed that ReqRes actually has **two independent authentication mechanisms**, which is not obvious from a first read of the docs:

1. **Legacy demo auth** (`/api/login`) — returns a fixed token for tutorial/demo purposes. Does **not** grant access to `/app/*` endpoints.
2. **App-user sessions** (`/api/app-users/login` → `/api/app-users/verify`) — requires a magic-link token delivered by email before a session can be verified, which places it outside the scope of fully automated, headless API testing without an email-testing service (e.g. Mailosaur).

This was documented as a scoped limitation rather than worked around, since chasing it further would have meant testing an email delivery system, not the API itself — a deliberate call on test scope, not a blocker.

## Stack

- Postman (collection + environment)
- Newman (CLI test runner, for CI-style execution)
- JavaScript / Chai assertions

## How to run

```bash
newman run QA-Auth-Automation-ReqRes.postman_collection.json \
  -e ReqRes-Env.postman_environment.json
```

## Possible next steps

- Add a mocked/stubbed magic-link flow to demonstrate the full app-user session in isolation
- Add CRUD scenario tests against `/api/users`
- Wire up a GitHub Actions workflow to run the collection on every push
