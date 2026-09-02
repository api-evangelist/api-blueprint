---
generated: '2026-09-02'
method: generated
name: Parse an API description into API Elements
description: >-
  Turn an API Blueprint, legacy Blueprint or Swagger 2.0 document into a Refract
  parse result (API Elements) using the free, unauthenticated API Blueprint
  parsing service.
api: openapi/api-blueprint-parsing-service-openapi.yml
operations: [listAffordances, parseApiDescription]
source: >-
  operationIds verified verbatim in
  openapi/api-blueprint-parsing-service-openapi.yml, which is itself derived
  from the provider's own API Blueprint contract in apib/ and reconciled against
  live probes on 2026-09-02.
---

# Parse an API description into API Elements

Base URL: `https://api.apiblueprint.org`

## Auth

None. There is no API key, token, account or sign-up. Call it directly. See
`authentication/api-blueprint-authentication.yml`.

## Steps

1. **(Optional) Discover the affordances** — `listAffordances` (`GET /`). Returns
   `application/hal+json` with a `_links` object. Use it to confirm the service is
   up before sending a large document.
2. **Parse the document** — `parseApiDescription` (`POST /parser`).
   - Set `Content-Type` to the input format: `text/vnd.apiblueprint`,
     `text/vnd.legacyblueprint`, `application/swagger+json` or
     `application/swagger+yaml`.
   - Set `Accept` to the output you want:
     `application/vnd.refract.parse-result+json` (or `+yaml`), optionally with
     `; version=1.0` or `; version=0.6`.
   - Send the document as the raw request body — it is not JSON-wrapped, and
     there are no query parameters.
3. **Read the result.** The body is a Refract element with
   `element: "parseResult"`. Walk `content[]`: the `category` element (classes
   `["api"]`) is the parsed API; every `annotation` element is a warning or error.

## Idempotency and retries

The operation stores nothing and is a pure function of the request body, so it is
safe to retry any number of times. No `Idempotency-Key` header exists or is needed.
See `conventions/api-blueprint-conventions.yml`.

## Errors

- `415` — the input media type is not supported. The message lists the ones that are.
- `406` — the `Accept` media type is not supported. The message lists the ones that are.
- `422` — the document did not parse. The body is a parse result, not an error
  envelope; read its `annotation` elements and their `sourceMap` offsets.
- Errors use `application/vnd.error+json` with a single `message` field — there is
  no error code to switch on. See `errors/api-blueprint-problem-types.yml`.

## Notes

- A `200` can still carry problems. Non-fatal issues come back as `annotation`
  elements with `meta.classes: ["warning"]` inside a successful parse result.
  Always inspect the annotations even on success.
- The whole `apiaryio` GitHub organization was archived on 2024-11-08. This service
  was live on 2026-09-02 but has no SLA, no status page and no deprecation policy.
  Do not put it on a critical path without a local fallback — `drafter` and
  `protagonist` do the same parse offline. See `lifecycle/api-blueprint-lifecycle.yml`.
