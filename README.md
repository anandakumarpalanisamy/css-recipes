# css-recipes
A collection of css recipes from the w3schools

# Diagrams

```mermaid
graph TB
  linkStyle default fill:#ffffff

  subgraph enterprise [Azzurri Group]
    style enterprise fill:#ffffff,stroke:#444444,color:#444444

    2["<div style='font-weight: bold'>Waiter</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Waiter of Zizzi or ASK<br />Italian restaurants who look<br />to accept payment for the<br />table using PDQ application</div>"]
    style 2 fill:#999999,stroke:#6b6b6b,color:#ffffff
    3("<div style='font-weight: bold'>Comtrex POS System</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows Order at Table<br />application to submit order<br />to kitchen, retrieve prices,<br />update payment and kick start<br />payment post process</div>")
    style 3 fill:#999999,stroke:#6b6b6b,color:#ffffff
    4("<div style='font-weight: bold'>Customer Loyalty Platform</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Loyalty</div>")
    style 4 fill:#999999,stroke:#6b6b6b,color:#ffffff
    5("<div style='font-weight: bold'>Payment Provider</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Pay</div>")
    style 5 fill:#999999,stroke:#6b6b6b,color:#ffffff
    6("<div style='font-weight: bold'>Gift Cards</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Gift Cards</div>")
    style 6 fill:#999999,stroke:#6b6b6b,color:#ffffff
    7("<div style='font-weight: bold'>Order At Table</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows customer to join a<br />table, order food and pay for<br />food at one of Zizzi or ASK<br />Italian restaurants</div>")
    style 7 fill:#1168bd,stroke:#0b4884,color:#ffffff
  end

  1["<div style='font-weight: bold'>Customer</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Customer of Zizzi or ASK<br />Italian who looks at order<br />and pay at the table using<br />online Progressive web app</div>"]
  style 1 fill:#08427b,stroke:#052e56,color:#ffffff

  7-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
  2-. "<div>Uses</div><div style='font-size: 70%'></div>" .->3
  7-. "<div>Uses</div><div style='font-size: 70%'></div>" .->4
  7-. "<div>Uses</div><div style='font-size: 70%'></div>" .->5
  7-. "<div>Uses</div><div style='font-size: 70%'></div>" .->6
  1-. "<div>Uses</div><div style='font-size: 70%'></div>" .->7
  2-. "<div>Uses</div><div style='font-size: 70%'></div>" .->7
```
