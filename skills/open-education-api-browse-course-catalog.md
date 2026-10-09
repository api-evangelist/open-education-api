---
generated: '2026-10-09'
method: generated
name: browse-course-catalog
description: 'Browse an institution''s course catalogue: list organisations, list the courses an organisation offers, fetch a course, then list its offerings (scheduled instances).'
api: openapi/open-education-api-openapi.yml
operations:
- listOrganisations
- listCoursesByOrganisationId
- listCourseById
- listCourseOfferingsByCourseId
source: Grounded in openapi/open-education-api-openapi.yml (OpenAPI 3.1.1, OEAPI 6.0-rc.3, https://oeapi.eu/specification/v6.0/oeapi-6.0-rc.3.yaml); all operationIds verified verbatim.
---

# Browse course catalog

Browse an institution's course catalogue: list organisations, list the courses an organisation offers, fetch a course, then list its offerings (scheduled instances).

## Steps
1. Call `listOrganisations` and pick the organisation (faculty, school or root institution) to browse.
2. Call `listCoursesByOrganisationId` with its `organisationId`; page with `pageSize`/`pageNumber`.
3. Call `listCourseById` for the full course description.
4. Call `listCourseOfferingsByCourseId` to see when and where the course is actually run.

## Operations
- `listOrganisations` — `GET /organisations`
- `listCoursesByOrganisationId` — `GET /organisations/{organisationId}/courses`
- `listCourseById` — `GET /courses/{courseId}`
- `listCourseOfferingsByCourseId` — `GET /courses/{courseId}/course-offerings`

## Conventions (from the OEAPI 6.0-rc.3 contract)
- Base URL is the implementing institution's own OEAPI host (`https://{host}/v6`); OEAPI is a standard, not a central API. The spec's only server, the SURF demo `https://demo01.eduapi.nl/v6`, did not resolve on 2026-10-09.
- Auth: the contract defines no global security ("security" tag) — use whatever the implementing institution requires.
- Collections page with `pageSize` and `pageNumber` (page numbers start at 1); filter with `filter_query[field][operation]=value`; trim payloads with `fields`; request consumer-specific data with `consumer`.
- Responses documented include 400, 401, 403, 404, 405, 406, 429 and 500; back off and retry on 429.
