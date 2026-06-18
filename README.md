Title: HIPAA-Compliant Claims Processing Platform for Healthcare Adjudication
Note at top: This is a case study describing system design and my contributions on a production project. Source code is proprietary to my employer and is not included here.

Problem:
CVS Caremark's claims adjudication platform needed to process tens of thousands of healthcare claims daily, with full visibility into submission and status tracking, while strictly complying with HIPAA regulations for handling Protected Health Information (PHI). Synchronous processing was creating bottlenecks that delayed claims as volume grew, and any compliance gap in PHI handling carried serious regulatory risk.

My Role & Contribution:
I built end-to-end claims processing features spanning both the backend microservices and the frontend UI, with a specific focus on making PHI handling compliant at every layer of the stack — not just at the database level.

Architecture Approach:
The platform used Spring Boot microservices on the backend paired with Angular UI components on the frontend, giving users real-time claims submission and adjudication status tracking across 50,000+ daily claims. To remove synchronous bottlenecks, claims transactions moved through Kafka-based event-driven pipelines, decoupling claim submission from downstream adjudication processing so delays in one stage didn't cascade into others. Spring Security and OAuth2 were integrated directly into the data access layers handling PHI, ensuring authentication and authorization were enforced before any sensitive data was touched — not just at the API gateway level. Retry and fault-tolerance patterns were introduced to handle transient failures gracefully, since a dropped claim in healthcare isn't just a bug, it can directly affect a patient's care timeline. SQL Server and MongoDB queries were optimized through indexing and partitioning to keep performance steady as claim volume grew. The team shipped through Agile/Scrum sprints, with microservices deployed via Docker and Kubernetes on AWS ECS, and CI/CD automated through Azure DevOps.

Outcome:
Downstream service failures dropped by approximately 25% after the retry and fault-tolerance patterns were introduced. The platform maintained zero compliance incidents related to PHI handling during my time on the project. Claims throughput improved as the asynchronous pipeline removed the bottlenecks that previously slowed adjudication during high-volume periods.

