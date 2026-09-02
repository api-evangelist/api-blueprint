---
generated: '2026-09-02'
method: generated
name: Validate an API description and read its annotations
description: >-
  Check whether an API Blueprint, Swagger or OpenAPI document is valid and get
  back only the warnings and errors, using the parsing service's /validate
  endpoint.
api: openapi/api-blueprint-parsing-service-openapi.yml
operations: [validateApiDescription]
source: >-
  operationId verified in openapi/api-blueprint-parsing-service-openapi.yml.
  /validate is NOT in the provider's published contract — the whole request and
  response shape below was established by unauthenticated probe on 2026-09-02
  and is recorded in that spec's x-probed block.
---

# Validate an API description and read its annotations

Base URL: `https://api.apiblueprint.org`

> **Undocumented endpoint.** `/validate` is advertised by the live service root
> but appears nowhere in the provider's published documentation. Everything here
> was established by probing the running service on 2026-09-02. Treat it as
> usable but unsupported, and re-verify before relying on it.

## Auth

None.

## Steps

1. **Validate** — `validateApiDescription` (`POST /validate`).
   - `Content-Type: application/json`. Unlike `/parser`, this endpoint takes a JSON
     envelope rather than a raw document.
   - Body:
     ```json
     {
       "input_document": "FORMAT: 1A\n\n# My API\n...",
       "input_type": "text/vnd.apiblueprint"
     }
     ```
   - `input_type` accepts `text/vnd.apiblueprint`, `text/vnd.legacyblueprint`,
     `application/swagger` and `application/vnd.oai.openapi`.
2. **Read the annotations.** A `200` returns
   `{"element":"parseResult","content":[...]}`. An **empty** `content` array means
   the document is clean. Each entry in a non-empty array is an `annotation` with
   `meta.classes` of `warning` or `error`, an integer `attributes.code`, a
   `sourceMap` giving character offset and length, and the message in `content`.

## Idempotency and retries

Pure function, no stored state, safe to retry.

## Errors

- `400 {"message":"Body is not valid JSON"}` — you sent the raw document instead of
  the JSON envelope.
- `400 {"message":"Missing input document (\`input_document\`)"}` — the envelope key
  is `input_document`, not `document` or `source`.
- `415` — `input_type` is missing or unsupported. Note the key is `input_type`;
  `content_type`, `input_content_type` and `input_mime_type` are all ignored and
  produce this error.
- `405` — you used `GET`. This endpoint is POST-only.

## Notes

`/validate` is the closest thing this API has to a dry run: it tells you what a
parse would complain about without asking you to handle the full parse result.
