# Shell (shell)

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

Royal Dutch Shell plc is a global energy company operating across oil, gas, renewable energy, lubricants, aviation fuel, and mobility sectors. The Shell Developer Portal provides APIs for B2B mobility card management, loyalty programs, lubricants ordering, aviation fuel reselling, and fleet management. SDKs are available in Java, .NET, TypeScript, PHP, Python, and Ruby.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/apis.yml)

## Scope

- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Aviation
- Electric Vehicle Charging
- Energy
- Fleet Management
- Fuel
- Gas
- Loyalty
- Lubricants
- Mobility
- Oil and Gas
- Renewable Energy

## Timestamps

- **Created:** 2025-03-01
- **Modified:** 2026-05-19

## APIs

### Shell B2B Mobility Card Management API

The Shell B2B Mobility Card Management API enables fleet operators and business customers to manage fuel cards, control spending limits, restrict usage by fuel type, location, or time, and monitor card status. Supports card issuance, updates, and lifecycle management for corporate fuel card programs.

- **Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- B2B
- Cards
- Fleet
- Mobility

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [OpenAPI](openapi/shell-b2b-mobility-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-b2b-mobility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-b2b-mobility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/shell-fuel-card-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/shell-transaction-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [Spectral Rules](rules/shell-rules.yml)

### Shell B2B Mobility Card Transaction Data API

Provides access to fuel card transaction data for B2B customers. Enables retrieval of transaction history, spend analytics, fuel type breakdowns, and location-based purchase data for corporate fleet management and expense reporting.

- **Human URL:** [https://developer.shell.com/api-catalog/v2.1.0/b2b-mobility-card-transaction-data](https://developer.shell.com/api-catalog/v2.1.0/b2b-mobility-card-transaction-data)

#### Tags

- B2B
- Fleet
- Mobility
- Transactions

#### Properties

- [Documentation](https://developer.shell.com/api-catalog/v2.1.0/b2b-mobility-card-transaction-data)
- [OpenAPI](openapi/shell-b2b-mobility-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-b2b-mobility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-b2b-mobility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell B2B Mobility Invoice API

Enables business customers to retrieve and manage invoices for Shell fuel card programs. Supports invoice download, payment status queries, and reconciliation workflows for fleet finance teams.

- **Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- B2B
- Finance
- Fleet
- Invoices

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [OpenAPI](openapi/shell-b2b-mobility-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-b2b-mobility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-b2b-mobility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell Loyalty Catalogue API

The Shell Loyalty Catalogue API provides access to the Shell Go+ loyalty program product and rewards catalogue. Partners can retrieve available rewards, offers, and redemption options to display within their applications and loyalty program integrations.

- **Human URL:** [https://developer.shell.com/api-catalog/v1.0.2/loyalty-catalogue](https://developer.shell.com/api-catalog/v1.0.2/loyalty-catalogue)

#### Tags

- Loyalty
- Rewards
- Retail

#### Properties

- [Documentation](https://developer.shell.com/api-catalog/v1.0.2/loyalty-catalogue)
- [OpenAPI](openapi/shell-loyalty-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-loyalty.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-loyalty.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell Loyalty Account Management API

Enables partners to manage Shell loyalty accounts, including enrolment, profile management, points balance queries, and account status updates. Integrates Shell Go+ loyalty program into partner digital platforms.

- **Human URL:** [https://developer.shell.com/use-cases/shell-loyalty-api-partners](https://developer.shell.com/use-cases/shell-loyalty-api-partners)

#### Tags

- Loyalty
- Rewards
- Accounts

#### Properties

- [Documentation](https://developer.shell.com/use-cases/shell-loyalty-api-partners)
- [OpenAPI](openapi/shell-loyalty-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-loyalty.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-loyalty.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell Loyalty Points Balance API

Provides real-time query access to Shell loyalty points balances for program members. Enables partners to display current points, tier status, and points expiry information within their applications.

- **Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- Loyalty
- Points
- Rewards

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [OpenAPI](openapi/shell-loyalty-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-loyalty.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-loyalty.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell Loyalty Points Redemption API

Enables partners to process loyalty points redemptions within Shell Go+ loyalty program. Supports redeeming points for fuel savings, partner rewards, and gift cards through the Shell Loyalty platform.

- **Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- Loyalty
- Points
- Redemption

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [OpenAPI](openapi/shell-loyalty-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-loyalty.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-loyalty.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell Lubricants Order Management API

The Shell Lubricants Order Management API enables business customers and distributors to place and manage orders for Shell lubricants products. Supports order creation, status tracking, delivery scheduling, and product catalogue queries.

- **Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- Lubricants
- Oil
- Orders
- B2B

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [OpenAPI](openapi/shell-lubricants-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-lubricants.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-lubricants.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell Aviation Fuel Reseller API

The Shell Aviation Fuel Reseller API enables aviation fuel resellers and operators to manage fuel procurement, pricing queries, order placement, and delivery logistics for Shell Aviation fuel products at airports and FBOs worldwide.

- **Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- Aviation
- Fuel
- B2B

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [Postman Collection](collections/shell-b2b-mobility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-b2b-mobility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/shell-loyalty.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-loyalty.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/shell-lubricants.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-lubricants.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Shell B2B Mobility Sites API

Provides access to the Shell network of fuel and EV charging sites for B2B mobility customers. Enables applications to query site locations, available fuel types, EV charging availability, amenities, and opening hours across the Shell station network.

- **Human URL:** [https://developer.shell.com/api-catalog/b2b-mobility-sites/quick-start-guide](https://developer.shell.com/api-catalog/b2b-mobility-sites/quick-start-guide)

#### Tags

- B2B
- Fleet
- Locations
- Mobility

#### Properties

- [Documentation](https://developer.shell.com/api-catalog/b2b-mobility-sites/quick-start-guide)
- [OpenAPI](openapi/shell-b2b-mobility-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/shell-b2b-mobility.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/shell-b2b-mobility.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/shell)
- [Developer  Portal](https://developer.shell.com)
- [A P I  Catalog](https://developer.shell.com/api-catalog)
- [Getting Started](https://developer.shell.com/docs/welcome-shell-developer-portal)
- [A P I  Key  Registration](https://developer.shell.com/signup)
- [Authentication](https://developer.shell.com/docs/authentication)
- [Terms of Service](https://www.shell.com/terms-and-conditions)
- [Privacy Policy](https://www.shell.com/privacy)
- [Support](https://developer.shell.com/support)
- [Status Page](https://developer.shell.com/support/api-status)
- [Blog](https://developer.shell.com/latest-updates)
- [GitHub Organization](https://github.com/shell)
- [Website](https://www.shell.com)
- [JSON-LD](json-ld/shell-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Vocabulary](vocabulary/shell-vocabulary.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
**FN:** Shell Digital Services
**Email:** api-maintainers@shell.com
