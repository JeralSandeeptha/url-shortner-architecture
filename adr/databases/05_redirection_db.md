# ADR 04: Use MongoDB as the URL Generation Database

## Status
Accepted

## Context

The URL redirection service is responsible for resolving short URLs to their corresponding long URLs and handling redirect logic efficiently.
This service operates under high read loads and must provide low-latency lookups while supporting analytics and lifecycle management for URLs.

Key considerations include:
    - `Performance`: The service must support high-throughput, low-latency reads to handle large volumes of redirection requests.
    - `Scalability`: The system should scale horizontally to support sudden traffic spikes.
    - `Durability`: The mapping between short and long URLs must be persisted reliably.
    - `Flexibility`: We may extend redirection logic to include metadata (e.g., expiration time, click counters, user segmentation).
    - `Integration`: Seamless integration with Node.js and shared infrastructure (e.g., URL generation service).

We evaluated several database options — PostgreSQL, Redis, and MongoDB — to determine the best fit for the redirection workload.

## Decision

We decided to use MongoDB as the primary database for the URL redirection service.

Implementation approach:
    - Store mappings between short URLs and their corresponding long URLs in MongoDB.
    - Use the same managed MongoDB instance (e.g., MongoDB Atlas, AWS DocumentDB) as the URL generation service, potentially in separate collections or databases.
    - Apply indexes on short URL keys for O(1) lookup performance.
    - Utilize TTL indexes to automatically delete expired links.
    - Use Mongoose or the MongoDB native driver for integration with Node.js.
    - Implement read replicas to offload read traffic and ensure high availability.

## Consequences

Positive:
    - Fast and efficient lookups for short-to-long URL resolution.
    - Shared technology stack with the URL generation service reduces operational complexity.
    - Built-in scalability through sharding and replica sets supports high-traffic use cases.
    - Flexible schema allows easy addition of metadata such as click tracking, user info, or access rules.
    - TTL indexes handle expiration automatically without manual cleanup.

Negative:
    - Slightly higher latency compared to an in-memory store like Redis (though acceptable for this use case).
    - Not fully ACID-compliant for multi-document operations (acceptable for redirection lookups).
    - Requires careful index management to maintain consistent lookup performance under heavy read traffic.

## Alternatives Considered (optional)

Redis:
    - Pros: Extremely low latency and high throughput.
    - Cons: Primarily in-memory; additional effort required for persistence and metadata storage.

PostgreSQL:
    - Pros: Strong consistency and mature ecosystem.
    - Cons: Less suited for high-frequency key-value lookups; schema rigidity adds maintenance overhead.

Cassandra:
    - Pros: Scales horizontally with strong write performance.
    - Cons: Complex operational setup and limited flexibility for ad-hoc queries.

## Date
2025-11-09

## Authors / Reviewers
Backend Team Lead
Software Architect