# ADR 03: Use PostgreSQL as the User Database

## Status
Accepted

## Context

Our application requires a reliable, scalable, and secure database to manage user data — including credentials, profile information, and related entities.

Key considerations include:
    - Data consistency: User data must be reliable and transactional (ACID-compliant).
    - Scalability: The system should handle growth in the number of users and requests.
    - Integration: The database should integrate easily with existing tools and frameworks (e.g., Keycloak, Node.js ORM like Prisma or Sequelize).
    - Maintainability: The chosen technology should be well-supported and familiar to the engineering team.

We evaluated several database options — MySQL, MongoDB, and PostgreSQL — to determine the best fit.

## Decision

We decided to use PostgreSQL as the primary database for storing user-related data.

Implementation approach:
    - Use PostgreSQL as the main relational database engine.
    - Connect via an ORM (e.g., Prisma or Sequelize) for schema management and migrations.
    - Host PostgreSQL in a managed environment (e.g., AWS RDS, Azure Database for PostgreSQL, or Cloud SQL).
    - Apply standard security practices such as SSL connections, role-based access control, and encryption at rest.

## Consequences

Positive:
    - Strong data integrity and ACID compliance ensure reliable transactions.
    - Excellent support for relations and complex queries fits user data models well.
    - Broad community support and documentation.
    - Seamless integration with Keycloak and Node.js applications.
    - Built-in support for JSON fields provides flexibility for semi-structured data.

Negative:
    - Slightly more complex setup and management compared to NoSQL databases.
    - Horizontal scalability requires more planning (e.g., sharding or partitioning).
    - May require tuning for high concurrency scenarios.

## Alternatives Considered (optional)

- MySQL:
    - Pros: Widely supported, simple to use.
    - Cons: Weaker JSON support, slightly less feature-rich for advanced queries.


- MongoDB:
    - Pros: Flexible schema, easy to scale horizontally.
    - Cons: Lacks strong ACID compliance for complex relational data, not ideal for strict consistency requirements.

- SQLite:
    - Pros: Lightweight and easy for local development.
    - Cons: Not suitable for multi-user production environments.

## Date
2025-11-04

## Authors / Reviewers
Backend Team Lead
Software Architect