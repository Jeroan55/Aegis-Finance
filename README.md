# Aegis Finance

**Unified Net Worth Intelligence Platform**

Aegis is a multi-source financial aggregation platform designed to consolidate financial accounts, investment portfolios, payment processors, and digital collectibles into a unified wealth management system.

The platform provides a centralized view of personal net worth by collecting, normalizing, and analyzing financial data from multiple sources.

## Overview

Managing wealth across multiple financial platforms can make it difficult to maintain an accurate picture of personal finances.

Aegis addresses this problem by integrating different financial data sources into a single platform, providing consolidated asset valuation, transaction tracking, historical net worth analysis, and financial insights.

### Supported Data Sources

| Provider | Data | Integration Method |
|---|---|---|
| Stockbit | Stock holdings and portfolio valuation | CSV / Manual |
| BCA | Account balances and transactions | CSV / API (subject to access) |
| PayPal | Wallet balances and transactions | API / CSV |
| Stripe | Available balances, pending balances, and payouts | API / CSV |
| Steam (CS2) | Inventory items and estimated market value | Inventory import / Market data |

Aegis is designed to support multiple integration methods, including official APIs, CSV imports, and manual data entry.

## Core Features

### 1. Unified Net Worth Tracking
- Consolidated net worth across multiple financial accounts.
- Multi-currency asset valuation.
- Historical net worth tracking.
- Asset allocation visualization.
- Total assets and liabilities overview.

### 2. Financial Account Management
- Centralized financial account management.
- Multiple accounts across different providers.
- Account balance tracking.
- Historical balance snapshots.
- Account-level asset breakdown.

### 3. Transaction Management
- Consolidated transaction history.
- Income and expense categorization.
- Transaction filtering and searching.
- Internal transfer detection.
- Duplicate transaction prevention.
- Manual transaction management.

### 4. Portfolio Management
- Stock portfolio tracking.
- Asset quantity and average acquisition cost.
- Market price tracking.
- Unrealized profit and loss.
- Digital collectible valuation.

### 5. Data Integration
- External API integrations.
- CSV import and processing.
- Manual asset entry.
- Data normalization.
- Automated synchronization.
- Import validation and error reporting.

### 6. Financial Intelligence
- Net worth performance analysis.
- Monthly income and expense reports.
- Asset allocation analytics.
- Currency exposure analysis.
- Historical asset valuation.
- Financial reconciliation.

## Technology Stack

| Component | Technology |
|---|---|
| Backend | Python, FastAPI |
| Frontend | React, TypeScript |
| Database | PostgreSQL |
| ORM | SQLAlchemy |
| Database Migrations | Alembic |
| Background Processing | Celery |
| Message Broker / Cache | Redis |
| Data Visualization | Recharts |
| Containerization | Docker |
| Testing | Pytest |
| CI/CD | GitHub Actions |

## Architecture

Aegis follows a **modular monolith architecture** with asynchronous background processing.

The system separates business domains into independent modules while maintaining a centralized application and database.

```text
                    AEGIS FINANCE
                          |
              +-----------+-----------+
              |                       |
         React Frontend          FastAPI Backend
              |                       |
              |              +--------+--------+
              |              |        |        |
              |          Services  Repositories Workers
              |              |        |        |
              |              +--------+--------+
              |                       |
              |                PostgreSQL
              |                       |
              |                Redis / Celery
              |                       |
              |              External Providers
              |                       |
              |       +-------+-------+-------+
              |       |       |       |       |
              |     BCA   PayPal  Stripe  Stockbit
              |                               |
              |                             Steam
              |
          Dashboard
```

### Data Processing Pipeline

External financial data follows a standardized processing pipeline:

1. Data acquisition through APIs, CSV imports, or manual entry.
2. Raw data validation.
3. Data normalization into a unified internal format.
4. Duplicate detection and idempotency checks.
5. Database persistence.
6. Financial reconciliation.
7. Asset valuation and currency conversion.
8. Net worth calculation.
9. Historical snapshot generation.

## Project Structure

```text
aegis/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── repositories/
│   │   ├── services/
│   │   ├── integrations/
│   │   ├── imports/
│   │   ├── workers/
│   │   └── database/
│   ├── tests/
│   ├── alembic.ini
│   └── Dockerfile
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── features/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   └── pages/
│   └── Dockerfile
│
├── infrastructure/
│   ├── docker-compose.yml
│   └── monitoring/
│
├── docs/
│   ├── architecture/
│   ├── adr/
│   ├── api/
│   └── database/
│
├── .env.example
├── .gitignore
├── README.md
└── LICENSE
```

## Financial Data Model

Aegis uses a normalized financial data model to support different asset classes and financial providers.

Core entities include:

- **Users:** User identity and preferences.
- **Financial Sources:** External providers and data sources.
- **Source Connections:** Provider integration configurations.
- **Financial Accounts:** Bank accounts, wallets, investment accounts, and digital inventories.
- **Assets:** Stocks, digital collectibles, and other asset types.
- **Asset Positions:** Asset ownership and quantities.
- **Transactions:** Financial activities and account movements.
- **Import Batches:** CSV import operations and processing status.
- **Transfer Links:** Relationships between internal transfers.
- **Asset Price History:** Historical market valuations.
- **Net Worth Snapshots:** Historical consolidated wealth records.
- **Liabilities:** Outstanding financial obligations.

Financial values are stored using precise decimal types rather than floating-point arithmetic.

## Net Worth Calculation

Aegis calculates net worth using the following formula:

```text
Net Worth = Total Assets - Total Liabilities
```

Assets denominated in foreign currencies are converted into the user's configured base currency.

```text
Asset Value =
    Quantity × Market Price × Exchange Rate
```

All valuations retain their original currency, valuation timestamp, and pricing source to support historical analysis and data transparency.

Internal transfers are identified separately to prevent double counting of financial movements.

## Security

Security is a fundamental part of Aegis's architecture.

Planned security measures include:

- Secure authentication and authorization.
- Password hashing using Argon2id.
- Encrypted external API credentials.
- HTTPS communication.
- User-level resource access control.
- Secure environment variable management.
- Audit logging.
- API rate limiting.
- Database backups.
- CSV upload validation.

Aegis is designed as a read-only financial aggregation platform. It does not execute financial transactions, transfer funds, or perform investment operations.

## Development Roadmap

| Phase | Scope | Status |
|---|---|---|
| Phase 0 | Engineering foundation and infrastructure | Planned |
| Phase 1 | Core backend and database | Planned |
| Phase 2 | Financial calculation and analytics engine | Planned |
| Phase 3 | External integrations and CSV processing | Planned |
| Phase 4 | Frontend dashboard | Planned |
| Phase 5 | Testing, security, and deployment | Planned |

## Getting Started

Development setup instructions will be added as the initial infrastructure and application modules are implemented.

### Prerequisites

- Python 3.12+
- Node.js
- PostgreSQL
- Redis
- Docker
- Git

### Environment Configuration

Create a `.env` file using `.env.example` as a template.

Never commit secrets, API keys, or personal financial information to version control.

## Testing

Aegis uses Pytest for automated testing.

Planned testing coverage includes:

- Unit testing.
- API testing.
- Database integration testing.
- External provider integration testing.
- Financial calculation validation.
- CSV import validation.
- Transaction idempotency.
- Authorization and security testing.
- Performance benchmarking.

## Documentation

Additional technical documentation will be maintained in the `/docs` directory.

Planned documentation:

- System Architecture
- Entity Relationship Diagram
- Database Schema
- API Reference
- Integration Specifications
- Security Model
- Architecture Decision Records

## Project Goals

Aegis is developed as a practical software engineering project with an emphasis on:

- Backend architecture and API development.
- Database design and data integrity.
- External service integrations.
- Financial data processing.
- Asynchronous task processing.
- Full-stack application development.
- Software testing and production readiness.

The long-term goal is to build a reliable, extensible, and maintainable financial aggregation platform.

## Disclaimer

Aegis is an independent software project and is not affiliated with Stockbit, BCA, PayPal, Stripe, Valve, or Steam.

External integrations are subject to provider API availability, access permissions, and applicable terms of service.

Financial valuations are estimates and should not be considered official account statements or investment advice.

---

**Aegis Finance**  
*One platform. Every asset. One complete financial picture.*
