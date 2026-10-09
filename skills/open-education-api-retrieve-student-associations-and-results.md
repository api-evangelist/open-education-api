---
generated: '2026-10-09'
method: generated
name: retrieve-student-associations-and-results
description: Collect a person's enrolments and results across course, programme and test-component offerings.
api: openapi/open-education-api-openapi.yml
operations:
- listPersonById
- listCourseOfferingAssociationsByPersonId
- listProgrammeOfferingAssociationsByPersonId
- listTestComponentOfferingAssociationsByPersonId
source: Grounded in openapi/open-education-api-openapi.yml (OpenAPI 3.1.1, OEAPI 6.0-rc.3, https://oeapi.eu/specification/v6.0/oeapi-6.0-rc.3.yaml); all operationIds verified verbatim.
---

# Retrieve student associations and results

Collect a person's enrolments and results across course, programme and test-component offerings.

## Steps
1. Call `listPersonById` for the person record.
2. Call `listCourseOfferingAssociationsByPersonId` for course enrolments (associations carry results).
3. Call `listProgrammeOfferingAssociationsByPersonId` for programme enrolments.
4. Call `listTestComponentOfferingAssociationsByPersonId` for test/exam registrations and outcomes.

## Operations
- `listPersonById` — `GET /persons/{personId}`
- `listCourseOfferingAssociationsByPersonId` — `GET /persons/{personId}/course-offering-associations`
- `listProgrammeOfferingAssociationsByPersonId` — `GET /persons/{personId}/programme-offering-associations`
- `listTestComponentOfferingAssociationsByPersonId` — `GET /persons/{personId}/test-component-offering-associations`

## Conventions (from the OEAPI 6.0-rc.3 contract)
- Base URL is the implementing institution's own OEAPI host (`https://{host}/v6`); OEAPI is a standard, not a central API. The spec's only server, the SURF demo `https://demo01.eduapi.nl/v6`, did not resolve on 2026-10-09.
- Auth: the contract defines no global security ("security" tag) — use whatever the implementing institution requires.
- Collections page with `pageSize` and `pageNumber` (page numbers start at 1); filter with `filter_query[field][operation]=value`; trim payloads with `fields`; request consumer-specific data with `consumer`.
- Responses documented include 400, 401, 403, 404, 405, 406, 429 and 500; back off and retry on 429.
