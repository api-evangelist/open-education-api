---
generated: '2026-10-09'
method: generated
name: explore-programme-structure
description: 'Walk a study programme: list programmes, fetch one, then list its sub-programmes, its courses and its programme offerings.'
api: openapi/open-education-api-openapi.yml
operations:
- listProgrammes
- listProgrammeById
- listProgrammesByProgrammeId
- listCoursesByProgrammeId
- listOfferingsByProgrammeId
source: Grounded in openapi/open-education-api-openapi.yml (OpenAPI 3.1.1, OEAPI 6.0-rc.3, https://oeapi.eu/specification/v6.0/oeapi-6.0-rc.3.yaml); all operationIds verified verbatim.
---

# Explore programme structure

Walk a study programme: list programmes, fetch one, then list its sub-programmes, its courses and its programme offerings.

## Steps
1. Call `listProgrammes` (filter with `filter_query` or `primaryCode` if you know the institution's code).
2. Call `listProgrammeById` for the programme record.
3. Call `listProgrammesByProgrammeId` for nested programmes (specialisations, tracks).
4. Call `listCoursesByProgrammeId` for the courses in the programme.
5. Call `listOfferingsByProgrammeId` for the scheduled programme offerings.

## Operations
- `listProgrammes` — `GET /programmes`
- `listProgrammeById` — `GET /programmes/{programmeId}`
- `listProgrammesByProgrammeId` — `GET /programmes/{programmeId}/programmes`
- `listCoursesByProgrammeId` — `GET /programmes/{programmeId}/courses`
- `listOfferingsByProgrammeId` — `GET /programmes/{programmeId}/programme-offerings`

## Conventions (from the OEAPI 6.0-rc.3 contract)
- Base URL is the implementing institution's own OEAPI host (`https://{host}/v6`); OEAPI is a standard, not a central API. The spec's only server, the SURF demo `https://demo01.eduapi.nl/v6`, did not resolve on 2026-10-09.
- Auth: the contract defines no global security ("security" tag) — use whatever the implementing institution requires.
- Collections page with `pageSize` and `pageNumber` (page numbers start at 1); filter with `filter_query[field][operation]=value`; trim payloads with `fields`; request consumer-specific data with `consumer`.
- Responses documented include 400, 401, 403, 404, 405, 406, 429 and 500; back off and retry on 429.
