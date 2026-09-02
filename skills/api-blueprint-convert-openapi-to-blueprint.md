---
generated: '2026-09-02'
method: generated
name: Convert between API description formats
description: >-
  Convert an OpenAPI, Swagger or API Blueprint document into API Elements, or
  compose an API Blueprint document back out of API Elements, using the parsing
  service's /transform and /composer endpoints.
api: openapi/api-blueprint-parsing-service-openapi.yml
operations: [transformApiDescription, composeApiDescription]
source: >-
  operationIds verified in openapi/api-blueprint-parsing-service-openapi.yml.
  composeApiDescription comes from the provider's contract (apib/composer.apib);
  transformApiDescription was established by probe on 2026-09-02.
---

# Convert between API description formats

Base URL: `https://api.apiblueprint.org`

Two directions are available. Pick by which way you are going.

## Auth

None.

## Direction 1 — any supported format into API Elements

Use `transformApiDescription` (`POST /transform`). This is the only surface that
accepts OpenAPI 3 (`application/vnd.oai.openapi`).

- `Content-Type: application/json`
- Body:
  ```json
  {
    "input_document": "<the document as a string>",
    "input_type": "text/vnd.apiblueprint",
    "output_type": "application/vnd.refract.parse-result+json"
  }
  ```
- `200` returns `application/hal+json`:
  `{"output_type": "...", "output_document": "<serialised result as a string>"}`.
  Note the result is a **string** inside the envelope — parse it a second time.

> **Undocumented endpoint.** `/transform` is advertised by the live service root
> but is absent from the provider's documentation. Shape established by probe on
> 2026-09-02.

## Direction 2 — API Elements back into API Blueprint

Use `composeApiDescription` (`POST /composer`). This one is documented.

- `Content-Type: application/vnd.refract+json` (an API Elements API Category) or
  `application/vnd.refract.parse-result+json` (a parse result).
- Send the API Elements document as the raw request body — no JSON envelope here.
- `200` returns `text/vnd.apiblueprint`: the composed blueprint.

## Idempotency and retries

Both operations are pure transformations and store nothing. Retry freely.

## Errors

- `/transform` `406` — `output_type` is missing or unsupported. The only supported
  outputs are the `application/vnd.refract.parse-result*` family; you cannot ask
  `/transform` for API Blueprint or OpenAPI out.
- `/composer` `415` — an unsupported `Content-Type`, or an unsupported Refract
  serialisation version. Only `0.6` and `1.0` are accepted. The retired API
  Blueprint AST (`application/vnd.apiblueprint.ast+json`) is explicitly rejected.
- See `errors/api-blueprint-problem-types.yml` for the verbatim messages.

## Notes

Round-tripping is asymmetric. `/transform` converts *into* API Elements only, and
`/composer` converts *out of* API Elements into API Blueprint only. To go OpenAPI
to API Blueprint, chain them: `/transform` first, then feed
`output_document` to `/composer`.
