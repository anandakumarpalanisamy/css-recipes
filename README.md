# css-recipes
A collection of css recipes from the w3schools

# Diagrams

## Context Diagram

```mermaid
graph TB
  linkStyle default fill:#ffffff

  subgraph enterprise [Azzurri Group]
    style enterprise fill:#ffffff,stroke:#444444,color:#444444

    10("<div style='font-weight: bold'>Review system</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Review system</div>")
    style 10 fill:#999999,stroke:#6b6b6b,color:#ffffff
    2["<div style='font-weight: bold'>Waiter</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Waiter of Zizzi or ASK<br />Italian restaurants who look<br />to accept payment for the<br />table using PDQ application</div>"]
    style 2 fill:#999999,stroke:#6b6b6b,color:#ffffff
    3("<div style='font-weight: bold'>Order At Table</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows customer to join a<br />table, order food and pay for<br />food at one of Zizzi or ASK<br />Italian restaurants</div>")
    style 3 fill:#1168bd,stroke:#0b4884,color:#ffffff
    4("<div style='font-weight: bold'>Comtrex POS System</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows Order at Table<br />application to submit order<br />to kitchen, retrieve prices,<br />update payment and kick start<br />payment post process</div>")
    style 4 fill:#999999,stroke:#6b6b6b,color:#ffffff
    5("<div style='font-weight: bold'>Customer Loyalty Platform</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Loyalty</div>")
    style 5 fill:#999999,stroke:#6b6b6b,color:#ffffff
    6("<div style='font-weight: bold'>Payment Provider</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Pay</div>")
    style 6 fill:#999999,stroke:#6b6b6b,color:#ffffff
    7("<div style='font-weight: bold'>Gift Cards</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Gift Cards</div>")
    style 7 fill:#999999,stroke:#6b6b6b,color:#ffffff
    8("<div style='font-weight: bold'>Menu store</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Menu Store</div>")
    style 8 fill:#999999,stroke:#6b6b6b,color:#ffffff
    9("<div style='font-weight: bold'>Donation system</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Donation system</div>")
    style 9 fill:#999999,stroke:#6b6b6b,color:#ffffff
  end

  1["<div style='font-weight: bold'>Customer</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Customer of Zizzi or ASK<br />Italian who looks at order<br />and pay at the table using<br />online Progressive web app</div>"]
  style 1 fill:#08427b,stroke:#052e56,color:#ffffff

  1-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
  2-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->4
  2-. "<div>Uses</div><div style='font-size: 70%'></div>" .->4
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->5
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->6
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->7
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->8
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->9
  3-. "<div>Uses</div><div style='font-size: 70%'></div>" .->10
```

## Container Diagram

```mermaid
graph TB
  linkStyle default fill:#ffffff

  1["<div style='font-weight: bold'>Customer</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Customer of Zizzi or ASK<br />Italian who looks at order<br />and pay at the table using<br />online Progressive web app</div>"]
  style 1 fill:#08427b,stroke:#052e56,color:#ffffff
  2["<div style='font-weight: bold'>Waiter</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Waiter of Zizzi or ASK<br />Italian restaurants who look<br />to accept payment for the<br />table using PDQ application</div>"]
  style 2 fill:#999999,stroke:#6b6b6b,color:#ffffff
  3("<div style='font-weight: bold'>Comtrex POS System</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows Order at Table<br />application to submit order<br />to kitchen, retrieve prices,<br />update payment and kick start<br />payment post process</div>")
  style 3 fill:#999999,stroke:#6b6b6b,color:#ffffff
  4("<div style='font-weight: bold'>Customer Loyalty Platform</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Loyalty</div>")
  style 4 fill:#999999,stroke:#6b6b6b,color:#ffffff
  5("<div style='font-weight: bold'>Stripe Payment Provider</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Card & Wallet Payments</div>")
  style 5 fill:#999999,stroke:#6b6b6b,color:#ffffff
  6("<div style='font-weight: bold'>Gift Cards Payment Provider</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Gift Cards Payment</div>")
  style 6 fill:#999999,stroke:#6b6b6b,color:#ffffff
  7("<div style='font-weight: bold'>Menu store</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Menu Store</div>")
  style 7 fill:#999999,stroke:#6b6b6b,color:#ffffff
  8("<div style='font-weight: bold'>Donation system</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Donation system</div>")
  style 8 fill:#999999,stroke:#6b6b6b,color:#ffffff
  9("<div style='font-weight: bold'>Review system</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Review system</div>")
  style 9 fill:#999999,stroke:#6b6b6b,color:#ffffff

  subgraph 10 [Order At Table]
    style 10 fill:#ffffff,stroke:#444444,color:#444444

    11("<div style='font-weight: bold'>Progressive Web Application</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript and React]</div><div style='font-size: 80%; margin-top:10px'>Provides the ordering and<br />payment functionality to<br />customers via mobile/web<br />browser</div>")
    style 11 fill:#438dd5,stroke:#2e6295,color:#ffffff
    12("<div style='font-weight: bold'>PDQ Application</div><div style='font-size: 70%; margin-top: 0px'>[Container: Native App]</div><div style='font-size: 80%; margin-top:10px'>Provides the payment<br />capabilities to waiters via<br />PDQ Device</div>")
    style 12 fill:#438dd5,stroke:#2e6295,color:#ffffff
    13("<div style='font-weight: bold'>Gateway API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div>")
    style 13 fill:#438dd5,stroke:#2e6295,color:#ffffff
    14("<div style='font-weight: bold'>Restaurant API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div>")
    style 14 fill:#438dd5,stroke:#2e6295,color:#ffffff
    15("<div style='font-weight: bold'>Operator API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div>")
    style 15 fill:#438dd5,stroke:#2e6295,color:#ffffff
    16("<div style='font-weight: bold'>Payment API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div>")
    style 16 fill:#438dd5,stroke:#2e6295,color:#ffffff
    17("<div style='font-weight: bold'>Config API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div><div style='font-size: 80%; margin-top:10px'>Provides capability to<br />retrieve and store<br />configuration data as json<br />payload as a whole or by<br />property</div>")
    style 17 fill:#438dd5,stroke:#2e6295,color:#ffffff
    18[("<div style='font-weight: bold'>OAT DynamoDB</div><div style='font-size: 70%; margin-top: 0px'>[Container: NoSQL Database]</div><div style='font-size: 80%; margin-top:10px'>Stores client session, table,<br />table stats, restaurants and<br />payments data</div>")]
    style 18 fill:#438dd5,stroke:#2e6295,color:#ffffff
    19[("<div style='font-weight: bold'>PaymentsV2 Database</div><div style='font-size: 70%; margin-top: 0px'>[Container: SQL Database]</div><div style='font-size: 80%; margin-top:10px'>Stores payments transaction<br />data</div>")]
    style 19 fill:#438dd5,stroke:#2e6295,color:#ffffff
  end

  2-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
  1-. "<div>Visits oat websiste using<br />mobile/web browswer</div><div style='font-size: 70%'>[HTTPS]</div>" .->11
  2-. "<div>Uses Optomany Payment Device</div><div style='font-size: 70%'>[HTTPS]</div>" .->12
  12-. "<div>Wraps the oat web app into a<br />web view</div><div style='font-size: 70%'>[React Navtive Web View]</div>" .->11
  11-. "<div>Makes API calls to retrieve<br />oat customer state data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->13
  11-. "<div>Makes API calls to retrieve<br />configuration data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->17
  11-. "<div>Makes API calls to complete<br />payment</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->5
  13-. "<div>Makes API calls to retrieve<br />menu data</div><div style='font-size: 70%'>[JSON/HTTP]</div>" .->14
  13-. "<div>Makes API calls to manage<br />order with POS system</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->15
  13-. "<div>Makes API calls to manage<br />payment transactions</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->16
  13-. "<div>Makes API calls to retrieve<br />configuration data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->17
  16-. "<div>Makes API calls via SDK to<br />manage payment transactions</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->5
  16-. "<div></div><div style='font-size: 70%'></div>" .->19
  16-. "<div></div><div style='font-size: 70%'></div>" .->18
  13-. "<div></div><div style='font-size: 70%'></div>" .->18
  17-. "<div></div><div style='font-size: 70%'></div>" .->18
  14-. "<div></div><div style='font-size: 70%'></div>" .->18
  14-. "<div></div><div style='font-size: 70%'></div>" .->7
  14-. "<div></div><div style='font-size: 70%'></div>" .->4
  14-. "<div></div><div style='font-size: 70%'></div>" .->8
  15-. "<div></div><div style='font-size: 70%'></div>" .->3
  16-. "<div></div><div style='font-size: 70%'></div>" .->5
  16-. "<div></div><div style='font-size: 70%'></div>" .->6
  13-. "<div></div><div style='font-size: 70%'></div>" .->9
```
