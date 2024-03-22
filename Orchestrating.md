# Research: Temporal. Dealign with distributed transactioning system without blood

In this research, we embark on an exploration of orchestrating distributed processing systems, elucidating fundamental concepts through the lens of an illustrative example. Our focus centers on the intricate interplay between three services, exemplifying the construction of a scalable architecture tailored for the management of complex state changes.

The primary objective of this study is to delve into thought-provoking inquiries that have surfaced as pertinent research avenues within this domain. As we acquire more knowledge, our goal is to understand the transition details from a queue-based choreography architecture to orchestration. Therefore, we are solely exploring the application of Temporal for one specific use case and examining its benefits and disadvantages solely related to this case.

In the subsequent section, we transition towards practical implementation, delving into the integration of Temporal concepts into real-world scenarios. Throughout this journey, we aim to offer insightful reflections on the implications of our findings.

One such consideration arises from the knowledge that a Temporal Cluster meticulously archives every state alteration within the system. This prompts the following question:

**Can Temporal replace logging, tracing systems, or other data persisting strategies?**

> The answer depends on the use case. Temporal workflows are stateful, so all data related to the process of fulfilling an order doesn't need to be stored in a separate database. However, Temporal lacks advanced querying capabilities across multiple workflows. For example, listing orders, especially those closed last year, is not something it can provide. Additionally, Temporal is not designed to store other data such as customer addresses, payment information, etc. My approach is that workflows should be queried directly for the current state of an order while it is open. The database is used to list and search for specific orders and maintain 2historical information. It is not ideal for workflows to poll the database for a state field. [1]

References:

1. [Response](https://community.temporal.io/t/should-i-maintain-separate-database-for-my-data/9430)
2. [Integration with Nest JS](https://www.restack.io/docs/temporal-knowledge-temporal-io-nestjs-integration)
