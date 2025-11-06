# ADR 04: Use MongoDB as the URL Generation Database

## Status
Accepted

## Context

Our application includes a URL generation and shortening service that requires fast read/write operations, flexible schema handling, and efficient storage for high volumes of short-lived or semi-structured data.

Key considerations include:
    - `Performance`: The system must handle high-frequency insertions and lookups efficiently.
    - `Flexibility`: URL data (e.g., metadata, expiration settings, analytics counters) can vary in structure.
    - `Scalability`: The database should scale horizontally to support traffic spikes and long-term growth.
    - `Durability`: While consistency is important, URL redirection can tolerate eventual consistency for analytics or non-critical fields.
    - `Integration`: The chosen database should integrate smoothly with Node.js and existing infrastructure.

We evaluated several databases — PostgreSQL, Redis, and MongoDB — to identify the best fit for the URL generation use case.

## Decision

We decided to use MongoDB as the database for storing URL generation and redirection data.

Implementation approach:
    - Use MongoDB as the primary data store for URLs, click analytics, and metadata.
    - Connect via a Node.js ODM (e.g., Mongoose) for schema modeling and validation.
    - Host MongoDB in a managed service (e.g., MongoDB Atlas, AWS DocumentDB).
    - Apply appropriate indexes (e.g., on short URL keys and expiration dates) for optimal performance.
    - Implement TTL indexes for automatic cleanup of expired URLs.
    - Use replica sets for fault tolerance and sharding for horizontal scalability if needed.

## Consequences

Positive:
    - Flexible schema supports evolving data models (e.g., adding analytics or user tracking).
    - High performance for read-heavy and write-heavy workloads.
    - Easy to scale horizontally with built-in sharding capabilities.
    - Simple integration with Node.js using Mongoose or the native driver.
    - Supports TTL and compound indexing for managing URL lifecycles.

Negative:
    - Lacks full ACID compliance for multi-document transactions (though often acceptable for this use case).
    - Requires additional setup for complex relational joins (if ever needed).
    - Query performance can degrade without proper indexing.

## Alternatives Considered (optional)

PostgreSQL:
    - Pros: Strong consistency and relational modeling.
    - Cons: More rigid schema and less suited for highly dynamic URL metadata.

Redis:
    - Pros: Extremely fast read/write performance, ideal for caching or ephemeral data.
    - Cons: Not ideal for persistent storage or complex queries.

Cassandra:
    - Pros: Excellent horizontal scalability.
    - Cons: Complex operational overhead and limited ad-hoc query capabilities.

## Date
2025-11-06

## Authors / Reviewers
Backend Team Lead
Software Architect