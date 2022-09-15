# css-recipes
A collection of css recipes from the w3schools

![ContextDiagram](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/anandakumarpalanisamy/css-recipes/main/uml/oatcontext2.puml)

```mermaid
  C4Context
    title System Context Diagram Order At Table System

    Person(ecommCustomer, Customer, "Customer of our online order at table system")
    Person(pdqWaiter, Customer, "Waiter at Zizzi or ASK Italian restaurant using a PDQ application")
    System(oat, "Order At Table System", "System enabling the customers to order and pay at table in one of Zizzi or ASK Italian restaurants")
    System_Ext(comtrex, "Point of Sale System", "System for enabling the OAT system to send the orders to kitchen at restaurants")

    Rel(ecommCustomer, oat, "makes requests to", "HTTPS/JSON")
    Rel(pdqWaiter, oat, "makes requests to", "HTTPS/JSON")
    Rel(oat, comtrex, "uses", "HTTPS/JSON")
    
    UpdateLayoutConfig($c4ShapeInRow="1", $c4BoundaryInRow="1")
```

```mermaid
graph TB
  linkStyle default fill:#ffffff

  1["<div style='font-weight: bold'>Customer</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div>"]
  style 1 fill:#08427b,stroke:#052e56,color:#ffffff
  2["<div style='font-weight: bold'>Waiter</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div>"]
  style 2 fill:#08427b,stroke:#052e56,color:#ffffff
  3("<div style='font-weight: bold'>Order At Table</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div>")
  style 3 fill:#1168bd,stroke:#0b4884,color:#ffffff

  1-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
  2-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
```
