# Research: Temporal. Deal easy with distributed processing system

In this research, I will explain some basic concepts about orchestrating distributed processing systems using an example with the interconnection between three services to build a scalable system for managing complex state changes. The system will consist of three different services: `market-exchanger`, `request-splitter` and `order-executor`.

The purpose of this paper is to address interesting questions that have been identified as research topics.

You may have read that Temporal Cluster persists every state change of the system. This raises the question:

**Can Temporal replace logging, tracing systems, or other data persisting strategies?**

> The answer depends on the use case. Temporal workflows are stateful, so all data related to the process of fulfilling an order doesn't need to be stored in a separate database. However, Temporal lacks advanced querying capabilities across multiple workflows. For example, listing orders, especially those closed last year, is not something it can provide. Additionally, Temporal is not designed to store other data such as customer addresses, payment information, etc. My approach is that workflows should be queried directly for the current state of an order while it is open. The database is used to list and search for specific orders and maintain 2historical information. It is not ideal for workflows to poll the database for a state field. [1]

References:

1. [Response](https://community.temporal.io/t/should-i-maintain-separate-database-for-my-data/9430)
