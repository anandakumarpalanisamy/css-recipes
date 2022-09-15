```mermaid
C4Container
title Order At Table System

Person_Ext(person_ext_public, "User")
System_Boundary(system, "OAT") {
  Container(container_oat_front_end, "OAT Front End PWA", "Enables user to join a table, order and pay", "javascript")
  Container(container_pat_gateway, "PAT Gateway Microservice", "Orchestrates OAT API calls to downstream microservices", "javascript")
}

```
