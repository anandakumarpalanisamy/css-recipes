<div hidden>
```
@startuml
!include /plantuml/C4_Container.puml

!define DEVICONS /plantuml-icon-font-sprites/devicons
!define FONTAWESOME /plantuml-icon-font-sprites/font-awesome-5
!include FONTAWESOME/user_check.puml

!include DEVICONS/go.puml
!include DEVICONS/postgresql.puml
!include DEVICONS/redis.puml
!include DEVICONS/database.puml
!include FONTAWESOME/users.puml

LAYOUT_TOP_DOWN()
LAYOUT_WITH_LEGEND()

title Container Diagram for Books System

Person_Ext(person_ext_public, "Public User via REST API",     "Backend Services / Frontend Service",  "users")
Person(person_authorized,     "Authorized User via REST API", "Backend Services / Frontend Services", "user_check")

System_Boundary(system, "Books System") {
  Container(container_public, "Public Web API", "Go, 1.15", "Allows getting books details.",       "go")
  Container(container_admin,  "Admin Web API",  "Go, 1.15", "Allows administering books details.", "go")
  Container(container_search, "Search Web API", "Go, 1.15", "Allows searching books records.",     "go")

  ContainerDb(container_db_rw,            "Read/Write Relational Database", "PostgreSQL 13.1",   "Stores books details.",            "postgresql")
  ContainerDb(container_db_ro,            "Read-Only Relational Database",  "PostgreSQL 13.1",   "Replicas for books details.",      "postgresql")
  ContainerDb(container_db_elasticsearch, "Search Database",                "ElasticSearch 7.x", "Stores searchable books details.", "elasticsearch")
  ContainerDb(container_db_memcached,     "Readers Cache",                  "Memcached 1.5.x",   "Caches books details.",            "memcached")

  Container(container_elasticsearch_updater, "ElasticSearch Events Consumer",   "Go, 1.15", "Updates details coming from domain events.", "go")

  Container(container_publisher_1, "Publisher 1 Recurrent Updater", "Go, 1.15", "Updates the RW db with details from Publisher 1.", "go")
  Container(container_publisher_2, "Publisher 2 Events Consumer",   "Go, 1.15", "Updates the RW db with details from Publisher 2.", "go")
}

System_Ext(system_ext_kafka_books,   "Books Kafka, 2.6.0",   "Handles book-related domain events.")
System_Ext(system_ext_authorization, "Authorization System", "Authorizes access to resources.")
System_Ext(system_ext_publisher_1,   "Publisher 1 System",   "Gives details about books published by them.")
System_Ext(system_ext_publisher_2,   "Publisher 2 System",   "Gives details about books published by them.")

'--

Rel_D(person_authorized, container_admin,  "Makes API calls", "JSON/HTTPS")
Rel_D(person_authorized, container_search, "Makes API calls", "JSON/HTTPS")

Rel(container_db_rw, container_db_ro, "Write data to", "SQL")

Rel(container_search,   container_db_elasticsearch, "Reads data to",                 "ElasticSearch")
Rel_L(container_search, system_ext_authorization,   "Authorizes access for records", "HTTPS")

Rel(container_admin,   system_ext_kafka_books,   "Publishes events to",           "Kafka")
Rel_L(container_admin, system_ext_authorization, "Authorizes access for records", "HTTPS")
Rel(container_admin,   container_db_rw,          "Reads from and writes data to", "SQL")

Rel(container_publisher_1,   system_ext_publisher_1, "Accesses Publiser details using", "HTTPS")
Rel_U(container_publisher_1, container_admin,        "Writes Publisher 1 details using", "HTTPS")

Rel(container_publisher_2,   system_ext_publisher_2, "Receives Publisher details using", "Kafka")
Rel_U(container_publisher_2, container_admin,        "Writes Publisher 2 details using", "HTTPS")

Rel(container_elasticsearch_updater, system_ext_kafka_books,     "Consumes events from", "Kafka")
Rel(container_elasticsearch_updater, container_db_elasticsearch, "Writes events to",     "ElasticSearch")

Rel_D(person_ext_public, container_public, "Makes API calls", "JSON/HTTPS")

Rel_U(container_public, container_db_ro,        "Reads data from",         "SQL")
Rel_R(container_public, container_db_memcached, "Reads/Writes data using", "Memcached")

@enduml
```
</div>
![](firstDiagram.svg)
