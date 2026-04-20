# API Blueprint (api-blueprint)
API Blueprint is a high-level API description language using Markdown-based syntax for designing, documenting, and prototyping web APIs. Created by Apiary and released under the MIT License, API Blueprint uses .apib files with a concise Markdown format that makes APIs accessible to both technical and non-technical stakeholders. The project is no longer actively maintained (all apiaryio GitHub repos are archived as of 2024) but remains a notable specification in API design history, influencing later formats like OpenAPI.

**URL:** [https://raw.githubusercontent.com/api-evangelist/api-blueprint/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/api-blueprint/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - API Design, Specification Language, Markdown, Documentation

## Timestamps

- **Created:** 2026-03-25
- **Modified:** 2026-04-19

## APIs

### API Blueprint
API Blueprint is a high-level API description language using Markdown-based syntax for designing, documenting, and prototyping APIs. Files use the .apib extension with media type text/vnd.apiblueprint. The project was archived in 2024 after being developed by Apiary (acquired by Oracle).

**Human URL:** [https://apiblueprint.org](https://apiblueprint.org)

#### Tags:

 - API Design, Specification Language, Markdown

#### Properties

- [Documentation](https://apiblueprint.org/documentation/)
- [GitHubRepository](https://github.com/apiaryio/api-blueprint)
- [Specification](https://github.com/apiaryio/api-blueprint/blob/master/API%20Blueprint%20Specification.md)
- [GettingStarted](https://apiblueprint.org/documentation/tutorial.html)

## Common Properties

- [Website](https://apiblueprint.org)
- [Documentation](https://apiblueprint.org/documentation/)
- [GitHubOrganization](https://github.com/apiaryio)
- [TermsOfService](https://github.com/apiaryio/api-blueprint/blob/master/LICENSE)

## Features

| Name | Description |
|------|-------------|
| Markdown-Based Syntax | API Blueprint uses concise Markdown syntax making API descriptions readable by both developers and non-technical stakeholders. Files use the .apib extension with media type text/vnd.apiblueprint. |
| Data Structure Modeling | Supports reusable data structure definitions using MSON (Markdown Syntax for Object Notation) for describing complex request and response schemas. |
| Mock Server Generation | API Blueprint documents can drive mock server generation for rapid prototyping and front-end development before backend implementation. |
| Testing with Dredd | The Dredd HTTP testing tool uses API Blueprint specs to run contract tests validating that API implementations match their documented contracts. |
| RFC-Driven Governance | API Blueprint evolution was governed through an RFC process similar to Rust and Django, with proposals submitted to the api-blueprint-rfcs repository. |

## Use Cases

| Name | Description |
|------|-------------|
| API Documentation | Write human-readable API documentation in Markdown that doubles as a machine-parseable specification for tooling. |
| Contract Testing | Use API Blueprint specs with Dredd to verify that API implementations conform to their documented contracts in CI pipelines. |
| API Prototyping | Rapidly prototype APIs by writing Blueprint specs first, then generating mock servers from the specification. |

## Integrations

| Name | Description |
|------|-------------|
| Apiary | API Blueprint was the native specification format of the Apiary platform (acquired by Oracle), which provided hosted documentation, mock servers, and testing. |
| Drafter Parser | The canonical API Blueprint parser written in C++ with bindings for Node.js (drafter.js, drafter-npm) and other languages. |
| Dredd Testing Framework | Language-agnostic HTTP API testing tool that validates live API implementations against API Blueprint or Swagger/OpenAPI specs. |
| Swagger Conversion | The swagger2blueprint tool converted Swagger API descriptions into API Blueprint format for migration workflows. |

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
