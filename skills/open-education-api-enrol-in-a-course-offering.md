---
generated: '2026-10-09'
method: generated
name: enrol-in-a-course-offering
description: Enrol the authenticated person in a course offering at another institution via the external association endpoint, then read back the resulting association.
api: openapi/open-education-api-openapi.yml
operations:
- listPersonByMyOauthId
- listCourseOfferingsById
- createExternalCourseOfferingAssociationByopenId
- listCourseOfferingAssociationById
source: Grounded in openapi/open-education-api-openapi.yml (OpenAPI 3.1.1, OEAPI 6.0-rc.3, https://oeapi.eu/specification/v6.0/oeapi-6.0-rc.3.yaml); all operationIds verified verbatim.
---

# Enrol in a course offering

Enrol the authenticated person in a course offering at another institution via the external association endpoint, then read back the resulting association.

## Steps
1. Call `listPersonByMyOauthId` (`GET /persons/me`) to confirm who the authenticated person is.
2. Call `listCourseOfferingsById` to confirm the target offering exists and is open.
3. Call `createExternalCourseOfferingAssociationByopenId` (`POST /course-offering-associations/external/me`) with the person, the offering (by `offeringId` or full details) and the issuing root organisation. Expect 201; 409 signals a conflict such as an existing enrolment. POST is not idempotent — do not blindly retry; confirm with the user first.
4. Call `listCourseOfferingAssociationById` with the returned association id to read its state.

## Operations
- `listPersonByMyOauthId` — `GET /persons/me`
- `listCourseOfferingsById` — `GET /course-offerings/{courseOfferingId}`
- `createExternalCourseOfferingAssociationByopenId` — `POST /course-offering-associations/external/me`
- `listCourseOfferingAssociationById` — `GET /course-offering-associations/{courseOfferingAssociationId}`

## Conventions (from the OEAPI 6.0-rc.3 contract)
- Base URL is the implementing institution's own OEAPI host (`https://{host}/v6`); OEAPI is a standard, not a central API. The spec's only server, the SURF demo `https://demo01.eduapi.nl/v6`, did not resolve on 2026-10-09.
- Auth: the contract defines no global security ("security" tag) — use whatever the implementing institution requires.
- Collections page with `pageSize` and `pageNumber` (page numbers start at 1); filter with `filter_query[field][operation]=value`; trim payloads with `fields`; request consumer-specific data with `consumer`.
- Responses documented include 400, 401, 403, 404, 405, 406, 429 and 500; back off and retry on 429.
