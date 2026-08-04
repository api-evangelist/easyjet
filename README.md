# easyJet (easyjet)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

easyJet Airline Company Limited is a British low-cost short-haul carrier registered in England (company number 03034606, registered office Hangar 89, London Luton Airport, Luton, Bedfordshire, LU2 9PF), flying a point-to-point network that its own trade pages describe as connecting more than 155 airports across 35 countries. Its home market is the United Kingdom and its commercial centre of gravity is intra-European leisure and short-haul business traffic, extended by the easyJet holidays package business and by ancillary products. easyJet sits at the direct end of the airline distribution chain: it was built without a GDS dependency and still sells the overwhelming majority of its seats through its own website and app, with agency and OTA access governed by a published Distribution Charter and delivered through fourteen approved aggregator and GDS channels. Its API posture, stated honestly, is commercial-agreement-gated and undocumented — there is no developer portal and no machine-readable contract of any kind.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/easyjet/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/easyjet/refs/heads/main/apis.yml)

## Tags

- Travel
- United Kingdom
- Aviation
- Airline
- Low Cost Carrier
- Europe
- Distribution
- Booking
- Ancillaries
- Partner Gated

## Timestamps

- **Created:** 2026-07-28
- **Modified:** 2026-07-28

## APIs

"the easyJet API" is named in easyJet's own Distribution Charter and is demonstrably in production — fourteen approved aggregators sell easyJet flights and ancillaries against it — but easyJet publishes no reference documentation, no OpenAPI or Swagger definition, no AsyncAPI or GraphQL schema, no authentication metadata and no rate limits. Two real API hostnames exist, `api.easyjet.com` and `b2b.easyjet.com`; both are fronted by Akamai and return HTTP 403 "Access Denied" on every path probed. Listing either as an API would be fabrication, so neither is listed.

One surface **is** listed, found on the second enrichment pass (2026-07-28):

- **easyJet Brand Widget Service (easyDom)** — `https://brand.easyjet.com/en/`. easyJet's hosted client-side widget platform for partner and white-label sites. `Header.js` and `Footer.js` answer anonymously with HTTP 200 and real JavaScript; `Script.js`, `SignIn.js`, `Registration.js` and `VRPanel.js` are partner-scoped by a `partner` query-string identifier and return a zero-byte body to an unrecognised caller. Behind them sits the `easyDom` library — `AuthenticationControl`, `AuthenticationHandler`, `RegistrationControl`, three authentication methods (Redirect, Dialog, Embedded), two styles (Classic, Modern), thirteen callback events and a `{Success, Result, ReturnUri, ErrorMessage}` result envelope. It is undocumented, unversioned, unsupported and built on jQuery 1.7.2, and it is not a data API — no flight search, booking or ancillary operation is exposed. It is nonetheless the only easyJet interface that answers a stranger with a 200, and the parameter and callback contract in [`components/easyjet-components.yml`](components/easyjet-components.yml) was read verbatim off easyJet's own publicly indexed sample partner implementation rather than inferred.

## Artifacts

- [`components/easyjet-components.yml`](components/easyjet-components.yml) — the easyWidget / easyDom component catalogue: hosts, widgets, parameters, library objects, events, result envelope, observed authentication model and gaps.
- [`conformance/easyjet-conformance.yml`](conformance/easyjet-conformance.yml) — standards posture. Fifteen standards assessed, recorded as verified negative or unknown evidence: no NDC, no OpenTravel/OTA, no OpenAPI, no GraphQL, no AsyncAPI, no WSDL, no RFC 9457, no RFC 9116, no RFC 9727, no llms.txt, no MCP; OAuth2 and OIDC unknowable because the hosts 403 before any metadata is served.
- [`security/easyjet-domain-security.yml`](security/easyjet-domain-security.yml) — TLS, HSTS, DNSSEC, CAA, SPF and DMARC across six easyJet hosts. TLS 1.3 everywhere, HSTS nowhere, no DNSSEC and no CAA, DMARC at `p=reject` with `sp=reject`.
- [`well-known/easyjet-well-known.yml`](well-known/easyjet-well-known.yml) — the `/.well-known/` probe record across five hosts. Zero documents found.
- [`llms/easyjet-llms.txt`](llms/easyjet-llms.txt) — generated llms.txt (easyJet serves none; `/llms.txt` is a 404).

## Distribution

easyJet is **not** an NDC carrier. The Distribution Charter (version March 2026) never mentions NDC, easyJet does not appear on ndctracker.com's list of 73 airlines with launched or in-development NDC programmes, and its approved channels describe the link as a direct-connect proprietary API — Duffel labels it "Direct Connect". easyJet never needed IATA's remedy for GDS intermediation because it never had a GDS dependency to escape; it solved the same commercial problem a decade earlier with its own API and a charter.

Agency access runs through the fourteen Approved Channels named at [easyjet.com/en/business/approved-channels-](https://www.easyjet.com/en/business/approved-channels-), each of which holds an API agreement with easyJet, or through a bilateral Direct API Agreement:

| Approved channel | Full nine-capability coverage (as of end May 2026) |
| --- | --- |
| Amadeus | No — missing Flex, Pass Extra, Smart+ |
| Anaxys | No |
| Bewotec | No |
| Duffel | No — missing Flex, Pass Extra |
| JFA Systems | No |
| Kyte | Yes |
| Paxport | Yes |
| Peakwork | No |
| Sabre | No — missing Flex, Pass Extra |
| Travelfusion | Yes |
| Travelport | No — missing Flex, Pass Extra, Smart+ |
| Traveltek | No |
| Viaxoft | Listed |
| Ypsilon | No |

## Switching cost

- **Interface shape:** proprietary-undocumented. No standard is referenced — no NDC, no OpenTravel/OTA, no OpenAPI. An easyJet integration is reusable against nothing else.
- **Second source:** alternatives-with-migration. There is no second source for easyJet's own inventory, but fourteen approved channels are alternative routes to it — with materially different content coverage, so switching is a re-integration project plus a coverage regression.
- **Exit path:** export-on-request. UK GDPR Article 20 data portability, scoped in the privacy notice to "your flight and holiday history", requested via the online privacy notice or `data.protection@easyJet.com`. No bulk export operation, and nothing published for resellers.
- **Identifier portability:** IATA airport codes and the EZY flight designator travel; the six-character easyJet booking reference does not, and no mapping to a GDS record locator or IATA ticket number is published.
- **Contractual lock-in:** the Distribution Charter is published and citable. easyJet "may amend the Distribution Charter from time to time, without notice", and reserves the right to restrict, suspend or terminate a reseller's access **and cancel bookings already made**. Governed by the laws of England and Wales. Commercial terms — term, fees, exclusivity, notice — are not published anywhere.
- **Access gate:** commercial-agreement. Either a Direct API Agreement with easyJet (no published application route, contact, pricing or eligibility criteria) or the contract of an Approved Channel. No self-serve signup, no sandbox, no trial.

Full evidence, including every URL probed with its HTTP status and the verbatim charter clauses, is in [`review.yml`](review.yml).

## Common Properties

- [Website](https://www.easyjet.com/)
- [Distribution charter (version March 2026)](https://www.easyjet.com/en/business/distribution-charter)
- [Approved aggregator and GDS channels](https://www.easyjet.com/en/business/approved-channels-)
- [Travel trade partners hub](https://www.easyjet.com/en/business/travel-trade-partners)
- [Acceptable use policy](https://www.easyjet.com/en/policy/acceptable-use)
- [Privacy notice](https://www.easyjet.com/en/policy/privacy)
- [Terms and conditions](https://www.easyjet.com/en/terms-and-conditions)
- [Help Centre](https://www.easyjet.com/en/help)
- [Create a myeasyJet account](https://www.easyjet.com/en/register)
- [Business fares](https://www.easyjet.com/en/business/business-fares)
- [LinkedIn](https://www.linkedin.com/company/easyjet)
- [Careers](https://careers.easyjet.com/)
- [Investor relations](https://corporate.easyjet.com/)

## Maintainers

- Kin Lane — kin@apievangelist.com
