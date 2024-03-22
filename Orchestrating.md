# Research: Temporal. Dealign with distributed transactioning system without a headache

Abstract

In this research, we embark on an exploration of orchestrating distributed processing systems, elucidating fundamental concepts through the lens of an illustrative example. Our focus centers on the intricate interplay between three services, exemplifying the construction of a scalable architecture tailored for the management of complex state changes.

The primary objective of this study is to delve into thought-provoking inquiries that have surfaced as pertinent research avenues within this domain. As we acquire more knowledge, our goal is to understand the transition details from a queue-based choreography architecture to orchestration. Therefore, we are solely exploring the application of Temporal for one specific use case and examining its benefits and disadvantages solely related to this case.

In the second practical section, we transition towards practical implementation, delving into the integration of Temporal concepts into real-world scenarios. Throughout this journey, we aim to offer insightful reflections on the implications of our findings.

## 1. The role

One such consideration arises from the knowledge that a Temporal Cluster meticulously archives every state alteration within the system. This prompts the following question:

**Can Temporal replace logging, tracing, or other observability systems (and also data persisting for historical purpose) strategies?**

> The answer depends on the use case. Temporal workflows are stateful, so all data related to the process of fulfilling an order doesn't need to be stored in a separate database. However, Temporal lacks advanced querying capabilities across multiple workflows. For example, listing orders, especially those closed last year, is not something it can provide. Additionally, Temporal is not designed to store other data such as customer addresses, payment information, etc. My approach is that workflows should be queried directly for the current state of an order while it is open. The database is used to list and search for specific orders and maintain 2historical information. It is not ideal for workflows to poll the database for a state field. [1]

In a more granular examination of the issue, it becomes evident that the Workflow paradigm is particularly beneficial under the following circumstances:

- Synchronization Across Actors (e.g., Microservices): When there is a need to synchronize state across multiple actors or components, such as microservices within a distributed system.

- Desire for Fault Tolerance and Replayable Logic: In scenarios where fault tolerance and the ability to perfectly replay logic are essential requirements.

- Seeking a Scalability Abstraction with Minimal Resource Overhead: When aiming for a scalable solution that abstracts scalability concerns without incurring unnecessary hardware resource wastage.

These criteria are notably tailored for execution models centered around microservices. However, to broaden the scope and applicability of Workflow paradigms, it's beneficial to move away from hardware and network-related guarantees.

In essence, backend services are inherently stateless, relying instead on a persistent storage system. Meanwhile, Temporal provides a reliable code execution environment where state manipulations are deterministic and atomic.

*The core concept* introduced by the Workflows paradigm is the Inversion of Execution, emphasizing the existence of a coordination layer where execution and execution planning are abstracted. This abstraction allows for a more generalized understanding of the utility of Workflow paradigms beyond specific hardware or network constraints.

References:

1. [Response](https://community.temporal.io/t/should-i-maintain-separate-database-for-my-data/9430)
2. [Integration with Nest JS](https://www.restack.io/docs/temporal-knowledge-temporal-io-nestjs-integration)
