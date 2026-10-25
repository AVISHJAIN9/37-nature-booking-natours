# System Design & Scalability: Natours (Wanderly)

This section examines how the frontend-only Wanderly platform scales to handle tens of millions of concurrent global travelers when connected to a cloud edge infrastructure.

```mermaid
flowchart TD
    Client([Global Traveler Browser]) --> Route53[AWS Route 53 GeoDNS]
    Route53 --> Cloudflare[Cloudflare Edge CDN & WAF]
    Cloudflare --> S3[Static S3 Origin Bucket: HTML/CSS/Assets]
    Cloudflare --> API[Serverless API Gateway (Booking Submissions)]
    API --> Lambda[AWS Lambda: Booking Validator]
    Lambda --> Dynamo[DynamoDB: Global Reservations]
```

### Module Index
- [14.1 Requirements & Capacity Estimation](/system-design/14.1-requirements-and-estimation)
- [14.2 Architecture Styles](/system-design/14.2-architecture-styles)
- [14.3 Networking & CDN Edge Protocols](/system-design/14.3-networking-and-communication)
- [14.4 Load Balancing & Edge Caching](/system-design/14.4-load-balancing-and-scaling)
- [14.5 Static Asset Storage & Provenance](/system-design/14.5-databases-and-storage)
- [14.6 Browser & CDN Cache Strategies](/system-design/14.6-caching)
- [14.7 Asynchronous Reservation Pipelines](/system-design/14.7-messaging-and-queues)
- [14.8 Client Concurrency & Idempotency](/system-design/14.8-consistency-and-concurrency)
- [14.9 Reliability, CDNs & Failover](/system-design/14.9-reliability-and-resilience)
- [14.10 Edge Rate Limiting & Abuse Prevention](/system-design/14.10-api-design-and-rate-limiting)
- [14.11 Security Architecture & CSP](/system-design/14.11-security-architecture)
- [14.12 Edge Search & Visual Discovery](/system-design/14.12-search-and-ai-architecture)
- [14.13 Real-Time Tour Availability](/system-design/14.13-real-time-systems)
- [14.14 Observability & Real-User Monitoring](/system-design/14.14-observability-and-operations)
- [14.15 Frontend Performance & Web Vitals](/system-design/14.15-performance-engineering)
- [14.16 Cloud Economics & Cost Breakdown](/system-design/14.16-cost-and-trade-offs)
- [14.17 Classic System Designs Applied](/system-design/14.17-classic-system-design)
- [Architectural Decision Records (ADRs)](/system-design/decisions)
