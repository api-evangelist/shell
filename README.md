# Shell (shell)

APIs and developer resources for Royal Dutch Shell plc, a global energy and petrochemical company.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Aviation, Electric Vehicle Charging, Energy, Fleet Management, Fuel, Gas, Loyalty, Lubricants, Mobility, Oil and Gas, Renewable Energy

## Timestamps

- **Created:** 2025-03-01
- **Modified:** 2026-05-02

## APIs

### Shell B2B Mobility Card Management API

The Shell B2B Mobility Card Management API enables fleet operators and business customers to manage fuel cards, control spending limits, restrict usage by fuel type, location, or time, and monitor card status. Supports card issuance, updates, and lifecycle management for corporate fuel card programs.

**Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- B2B, Cards, Fleet, Mobility

#### Properties

- [Documentation](https://developer.shell.com/api-catalog)
- [OpenAPI](openapi/shell-b2b-mobility-openapi.yml)
- [JSONSchema](json-schema/shell-fuel-card-schema.json)
- [JSONSchema](json-schema/shell-transaction-schema.json)
- [SpectralRules](rules/shell-rules.yml)
- [NaftikoCapabilities](capabilities/fleet-management.yaml)

### Shell B2B Mobility Card Transaction Data API

Provides access to fuel card transaction data for B2B customers. Enables retrieval of transaction history, spend analytics, fuel type breakdowns, and location-based purchase data for corporate fleet management and expense reporting.

**Human URL:** [https://developer.shell.com/api-catalog/v2.1.0/b2b-mobility-card-transaction-data](https://developer.shell.com/api-catalog/v2.1.0/b2b-mobility-card-transaction-data)

#### Tags

- B2B, Fleet, Mobility, Transactions

### Shell B2B Mobility Invoice API

Enables business customers to retrieve and manage invoices for Shell fuel card programs. Supports invoice download, payment status queries, and reconciliation workflows for fleet finance teams.

**Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- B2B, Finance, Fleet, Invoices

### Shell Loyalty Catalogue API

The Shell Loyalty Catalogue API provides access to the Shell Go+ loyalty program product and rewards catalogue. Partners can retrieve available rewards, offers, and redemption options to display within their applications and loyalty program integrations.

**Human URL:** [https://developer.shell.com/api-catalog/v1.0.2/loyalty-catalogue](https://developer.shell.com/api-catalog/v1.0.2/loyalty-catalogue)

#### Tags

- Loyalty, Rewards, Retail

#### Properties

- [OpenAPI](openapi/shell-loyalty-openapi.yml)
- [NaftikoCapabilities](capabilities/loyalty-program.yaml)

### Shell Loyalty Account Management API

Enables partners to manage Shell loyalty accounts, including enrolment, profile management, points balance queries, and account status updates. Integrates Shell Go+ loyalty program into partner digital platforms.

**Human URL:** [https://developer.shell.com/use-cases/shell-loyalty-api-partners](https://developer.shell.com/use-cases/shell-loyalty-api-partners)

#### Tags

- Loyalty, Rewards, Accounts

### Shell Lubricants Order Management API

The Shell Lubricants Order Management API enables business customers and distributors to place and manage orders for Shell lubricants products. Supports order creation, status tracking, delivery scheduling, and product catalogue queries.

**Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- Lubricants, Oil, Orders, B2B

#### Properties

- [OpenAPI](openapi/shell-lubricants-openapi.yml)

### Shell Aviation Fuel Reseller API

The Shell Aviation Fuel Reseller API enables aviation fuel resellers and operators to manage fuel procurement, pricing queries, order placement, and delivery logistics for Shell Aviation fuel products at airports and FBOs worldwide.

**Human URL:** [https://developer.shell.com/api-catalog](https://developer.shell.com/api-catalog)

#### Tags

- Aviation, Fuel, B2B

### Shell B2B Mobility Sites API

Provides access to the Shell network of fuel and EV charging sites for B2B mobility customers. Enables applications to query site locations, available fuel types, EV charging availability, amenities, and opening hours across the Shell station network.

**Human URL:** [https://developer.shell.com/api-catalog/b2b-mobility-sites/quick-start-guide](https://developer.shell.com/api-catalog/b2b-mobility-sites/quick-start-guide)

#### Tags

- B2B, Fleet, Locations, Mobility

## Capabilities

### Shared Definitions

| File | Description |
|---|---|
| [capabilities/shared/b2b-mobility.yaml](capabilities/shared/b2b-mobility.yaml) | Shell B2B Mobility API — card management, transactions, invoices, sites |
| [capabilities/shared/loyalty.yaml](capabilities/shared/loyalty.yaml) | Shell Loyalty API — account management, points, catalogue, offers |

### Workflow Capabilities

| Capability | Description | Tools |
|---|---|---|
| [fleet-management.yaml](capabilities/fleet-management.yaml) | Fuel card management, transaction reporting, invoice reconciliation, site location | 7 tools |
| [loyalty-program.yaml](capabilities/loyalty-program.yaml) | Shell Go+ loyalty enrollment, points balance, redemption, offers | 7 tools |

## Artifacts

| Type | File |
|---|---|
| OpenAPI | [openapi/shell-b2b-mobility-openapi.yml](openapi/shell-b2b-mobility-openapi.yml) |
| OpenAPI | [openapi/shell-loyalty-openapi.yml](openapi/shell-loyalty-openapi.yml) |
| OpenAPI | [openapi/shell-lubricants-openapi.yml](openapi/shell-lubricants-openapi.yml) |
| JSON Schema | [json-schema/shell-fuel-card-schema.json](json-schema/shell-fuel-card-schema.json) |
| JSON Schema | [json-schema/shell-transaction-schema.json](json-schema/shell-transaction-schema.json) |
| JSON Structure | [json-structure/shell-fuel-card-structure.json](json-structure/shell-fuel-card-structure.json) |
| JSON-LD | [json-ld/shell-context.jsonld](json-ld/shell-context.jsonld) |
| Examples | [examples/shell-list-transactions-example.json](examples/shell-list-transactions-example.json) |
| Spectral Rules | [rules/shell-rules.yml](rules/shell-rules.yml) |
| Vocabulary | [vocabulary/shell-vocabulary.yml](vocabulary/shell-vocabulary.yml) |

## Common Properties

- [Developer Portal](https://developer.shell.com)
- [API Catalog](https://developer.shell.com/api-catalog)
- [Getting Started](https://developer.shell.com/docs/welcome-shell-developer-portal)
- [API Key Registration](https://developer.shell.com/signup)
- [Authentication](https://developer.shell.com/docs/authentication)
- [Terms of Service](https://www.shell.com/terms-and-conditions)
- [Privacy Policy](https://www.shell.com/privacy)
- [Support](https://developer.shell.com/support)
- [Status Page](https://developer.shell.com/support/api-status)
- [Blog](https://developer.shell.com/latest-updates)
- [GitHub Organization](https://github.com/shell)
- [Website](https://www.shell.com)

## Maintainers

**FN:** Kin Lane  
**Email:** kin@apievangelist.com

**FN:** Shell Digital Services  
**Email:** api-maintainers@shell.com
