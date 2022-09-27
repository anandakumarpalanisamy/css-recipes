# OAT Diagrams

```mermaid
%%{init: {'theme':'base','themeVariables': { 'lineColor': '#ffffff', }}}%%
graph TB
    subgraph SystemContext [System Context - Order At Table Application]
    Waiter((fa:fa-users Waiters)) -. "Uses PDQ device to take<br/>payments at the<br/>table" .-> OAT(<strong>Order at Table</strong><br/><br/>Provide users ability to<br/>join a table, order food and <br/>pay for food at<br/>one of Zizzi<br/>or ASK Italian restaurants )
    end

    Customer((fa:fa-users Customers)) -. "Visits oat website to order<br/>food and pay at<br/> the table" .-> OAT
    OAT -. "Allows OAT application<br/> to submit order<br/> to kitchen,<br/> retrieve price,<br/> update payment and<br/> payment-post process" .-> Comtrex(Comtrex<br/></br/>POS System)
    OAT-. "Process customer<br/> order and<br/> payments transactions to<br/> allocate loyalty Z<br/> points to<br/> customer" .-> Atreemo(Atreemo <br/><br/> Customer Loyalty <br/> Platform)
    OAT -. "Manage card<br/> payments" .-> Stripe(Stripe <br/><br/> Payment Provider)
    OAT -. "Manage gift card<br/> payments" .-> EagleEye(Eagle Eye <br/><br/> Gift Cards<br/> Payment Provider)
    OAT -. "Manage card payments" .-> Yext(Yext <br/><br/> Menu & Restaurant<br> Data Provider)
    OAT -. "Calculate &<br/> submit donation<br/> by bill value to<br/> charities<br/> supported by<br/> Pennies" .-> Pennies(Pennies <br/><br/> Donation system)
    OAT -. "Collect customer<br/> reviews" .-> Yumpingo(Yumpingo <br/><br/> Review System)
```

# OAT Container Diagram v1
```mermaid
%%{init: {'theme':'base','themeVariables': { 'lineColor': '#ffffff', }}}%%
graph TB

    subgraph SystemContext [Containers - Order At Table Application]
    PDQPaymentApp -. "Wraps the OAT web app into a web view (React Native Web view)" .-> OATFrontEnd(<strong>OAT Frontend PWA</strong><br/><br/> Provides the ordering and<br/> payment functionality to <br/>customers via mobile/web<br/> browswer)
    OATFrontEnd -. "Makes API calls to<br/>retrieve OAT restaurant,<br/> menu and customer session data" .-> PATGateway(<strong>Gateway API</strong><br/><br/>Front facing API for<br/> the Azzurri OAT application.<br/> User interface layers<br/> must interact with<br/> Gateway API)
    PATGateway -. "Makes API calls to<br/>manage order &<br/>post payment with<br/>POS System" .-> PATOperator(<strong>Operator API</strong><br/><br/>API for handling<br/>order and post-payment<br/>management capabilities<br/> via API Calls to Comtrex)
    PATGateway -. "Makes API calls to<br/>retrieve and store menu,<br/>restaurant data<br/>from Yext and expose<br/>expose endpoints for<br/>OAT consumption" .-> OATRestaurant(<strong>Restaurant API</strong><br/><br/>)
    PATGateway -. "Makes API calls to<br/>store and retrieve<br/>configuration data for<br/>OAT application" .-> OATConfig(<strong>Config API</strong><br/><br/>)
    PATGateway -. "Makes API calls to<br/>manage payment<br/>transactions<br/>made from OAT application" .-> PATPayment(<strong>Payment API</strong><br/><br/>)
    PATGateway -. "Reads and write<br/>sessions, basket,<br/>table, table stats<br/>items and<br/>payments data" .-> DynamoDB(<strong>OAT DynamoDB</storng><br/><br/>)
    PATPayment -. "Reads and write<br/>payment commitments<br/>and transactions<br/>includes stripe<br/>payments and<br/>gift card <br/>payments" .-> PaymentsV2DB(<strong>OAT PaymentsV2 DB</strong><br/><br/>) 
    PATPayment -. "Reads and writes<br/>payment commitments<br/>and transactions<br/>includes stripe<br/>payments and<br/>gift card <br/>payments" .-> DynamoDB
    OATConfig -. "Reads and write<br/>configuration<br/>data" .-> DynamoDB
    OATRestaurant -. "Reads and write<br/>menus, prices &<br/>restaurant data." .-> DynamoDB
    end

    Customer((fa:fa-users Customers)) -. "Visits oat website to order<br/>food and pay at<br/> the table" .-> OATFrontEnd
    Waiter((fa:fa-users Waiters)) -. "Uses PDQ device to take<br/>payments at the<br/>table" .-> PDQPaymentApp(<strong>PDQ Paymnent App</strong><br/><br/> Provides the payment<br/> capabilities to waiters <br>via PDQ Device)
    Waiter((fa:fa-users Waiters)) -. "Manage table,<br/>order, take<br/>payment and<br/>post payment<br/>process" .-> Comtrex(<strong>Comtrex POS System</strong><br/><br/>Allows OAT app to<br/>submit order<br/>to kitchen,<br/>retrieve prices,<br/>update payment<br/>and kick start<br/>payment post<br/>process)
    PATOperator -. "Retrieve and<br/>update table<br/>order and<br/>post pament<br/>management data<br/>[JSON/HTTPS]" .-> Comtrex
    PATGateway -. "Send customer<br/>review data<br/>[JSON/HTTPS]" .-> Yumpingo(Yumpingo <br/><br/> Review System)
    PATPayment -. "Check balance<br/> and redeem gift<br/>cards to pay for<br/>the order [JSON/HTTPS]" .-> EagleEye(Eagle Eye <br/><br/> Gift Cards<br/> Payment Provider)
    PATPayment -. "Makes API Calls<br/> via SDK to manage<br/>payment transacitons<br/> [JSON/HTTPS]" .-> Stripe(Stripe <br/><br/> Payment Provider)
    direction LR
    OATRestaurant -. "Retrieves menu<br/>and restaurant<br/>data [JSON/HTTPS]" .-> Yext(Yext <br/><br/> Menu & Restaurant<br> Data Provider)
    OATRestaurant -. "Calculate<br/> and log donations<br/>made to charities<br/>on Pennies System[JSON/HTTPS]" .-> Pennies(Pennies <br/><br/> Donation system) 
    OATRestaurant -. "Post transaction <br/>process to allocate<br/> loyalty Z points <br/>to customer" .-> Atreemo(Atreemo <br/><br/> Customer Loyalty <br/> Platform) 

```

# OAT Container Diagram v2
```mermaid
%%{init: {'theme':'base','themeVariables': { 'lineColor': '#ffffff', }}}%%
graph TB

    PDQPaymentApp -. "Wraps the OAT web app into a web view (React Native Web view)" .-> OATFrontEnd(<strong>OAT Frontend PWA</strong><br/><br/> Provides the ordering and<br/> payment functionality to <br/>customers via mobile/web<br/> browswer)
    OATFrontEnd -. "Makes API calls to<br/>retrieve OAT restaurant,<br/> menu and customer session data" .-> PATGateway(<strong>Gateway API</strong><br/><br/>Front facing API for<br/> the Azzurri OAT application.<br/> User interface layers<br/> must interact with<br/> Gateway API)
    PATGateway -. "Makes API calls to<br/>manage order &<br/>post payment with<br/>POS System" .-> PATOperator(<strong>Operator API</strong><br/><br/>API for handling<br/>order and post-payment<br/>management capabilities<br/> via API Calls to Comtrex)
    PATGateway -. "Makes API calls to<br/>retrieve and store menu,<br/>restaurant data<br/>from Yext and expose<br/>expose endpoints for<br/>OAT consumption" .-> OATRestaurant(<strong>Restaurant API</strong><br/><br/>)
    PATGateway -. "Makes API calls to<br/>store and retrieve<br/>configuration data for<br/>OAT application" .-> OATConfig(<strong>Config API</strong><br/><br/>)
    PATGateway -. "Makes API calls to<br/>manage payment<br/>transactions<br/>made from OAT application" .-> PATPayment(<strong>Payment API</strong><br/><br/>)
    PATGateway -. "Reads and write<br/>sessions, basket,<br/>table, table stats<br/>items and<br/>payments data" .-> DynamoDB(<strong>OAT DynamoDB</storng><br/><br/>)
    PATPayment -. "Reads and write<br/>payment commitments<br/>and transactions<br/>includes stripe<br/>payments and<br/>gift card <br/>payments" .-> PaymentsV2DB(<strong>OAT PaymentsV2 DB</strong><br/><br/>) 
    PATPayment -. "Reads and writes<br/>payment commitments<br/>and transactions<br/>includes stripe<br/>payments and<br/>gift card <br/>payments" .-> DynamoDB
    OATConfig -. "Reads and write<br/>configuration<br/>data" .-> DynamoDB
    OATRestaurant -. "Reads and write<br/>menus, prices &<br/>restaurant data." .-> DynamoDB

    Customer((fa:fa-users Customers)) -. "Visits oat website to order<br/>food and pay at<br/> the table" .-> OATFrontEnd
    Waiter((fa:fa-users Waiters)) -. "Uses PDQ device to take<br/>payments at the<br/>table" .-> PDQPaymentApp(<strong>PDQ Paymnent App</strong><br/><br/> Provides the payment<br/> capabilities to waiters <br>via PDQ Device)

    Waiter((fa:fa-users Waiters)) -. "Manage table,<br/>order, take<br/>payment and<br/>post payment<br/>process" .-> Comtrex(<strong>Comtrex POS System</strong><br/><br/>Allows OAT app to<br/>submit order<br/>to kitchen,<br/>retrieve prices,<br/>update payment<br/>and kick start<br/>payment post<br/>process)
    PATOperator -. "Retrieve and<br/>update table<br/>order and<br/>post pament<br/>management data<br/>[JSON/HTTPS]" .-> Comtrex
    PATGateway -. "Send customer<br/>review data<br/>[JSON/HTTPS]" .-> Yumpingo(Yumpingo <br/><br/> Review System)
    PATPayment -. "Check balance<br/> and redeem gift<br/>cards to pay for<br/>the order [JSON/HTTPS]" .-> EagleEye(Eagle Eye <br/><br/> Gift Cards<br/> Payment Provider)
    PATPayment -. "Makes API Calls<br/> via SDK to manage<br/>payment transacitons<br/> [JSON/HTTPS]" .-> Stripe(Stripe <br/><br/> Payment Provider)
    OATRestaurant -. "Retrieves menu<br/>and restaurant<br/>data [JSON/HTTPS]" .-> Yext(Yext <br/><br/> Menu & Restaurant<br> Data Provider)
    OATRestaurant -. "Calculate<br/> and log donations<br/>made to charities<br/>on Pennies System[JSON/HTTPS]" .-> Pennies(Pennies <br/><br/> Donation system) 
    OATRestaurant -. "Post transaction <br/>process to allocate<br/> loyalty Z points <br/>to customer" .-> Atreemo(Atreemo <br/><br/> Customer Loyalty <br/> Platform) 
```

## OAT Restaurant API - Endpoints summary

```mermaid
%%{init: {'theme':'base','themeVariables': { 'lineColor': '#ffffff', }}}%%
graph TB

  style Atreemo fill:#FDDCDC,stroke:#333,stroke-width:2px,color:#333
  style Yext fill:#FDDCDC,stroke:#333,stroke-width:2px,color:#333
  style PatOperator fill:#FDDCDC,stroke:#333,stroke-width:2px,color:#333
  style PATPayment fill:#FDDCDC,stroke:#333,stroke-width:2px,color:#333
  style Yumpingo fill:#FDDCDC,stroke:#333,stroke-width:2px,color:#333
  style Pennies fill:#FDDCDC,stroke:#333,stroke-width:2px,color:#333

  Client -. "Makes API calls <br/>for menu, menu item<br/> & price data" .-> MenuRouter(Menu<br/>Router)
  Client -. "Makes API calls <br/>for restaurant data" .-> RestaurantRouter(Restaurant<br/>Router)
  Client -. "Get Review Url" .-> YumpingoRouter(Yumpingo<br/>Router)
  Client -. "Send Email" .-> EmailRouter(Email<br/>Router)
  Client -. "Calculate<br/>& Submit donation" .-> DonationRouter(Donation<br/>Router)
  Client -. "Get FAQs" .-> FAQRouter(FAQ<br/>Router)
  Client -. "Post Transaction" .-> StatsRouter(Stats<br/>Router)

  subgraph "FAQs"
    FAQRouter
  end

  subgraph "DynamoDB"
    MenuStore
    PriceStore
    RestaurantStore
  end

  subgraph "Restaurant endpoints"
    RestaurantRouter -. "Makes method calls <br/>to retrieve restaurant<br/>data" .-> RestaurantController(Restaurant<br/>Controller)
  end

  subgraph "Yumpingo endpoints"
    YumpingoRouter -. getReviewUrl .-> YumpingoController(Yumpingo<br/>Controller)
  end

  subgraph "Email endpoints"
    EmailRouter -. "sendEmail" .-> EmailController(Email<br/>Controller)
  end

  subgraph "Donation endpoints"
    DonationRouter -. "calculate<br/>Donation" .-> DonationController(Donation<br/>Controller)
    DonationRouter -. "submit<br/>Donation" .-> DonationController
    DonationController -. "getSuggested<br/>Donation" .-> DonationService(Donation<br/>Service)
    DonationController -. "submit<br/>Donation" .-> DonationService
  end

  subgraph "stats endpoint"
    StatsRouter -. "post<br/>Transaction" .-> StatsController(Stats<br/>Controller)
    StatsController -. "getOrder<br>Snapshot" .-> OperatorService
    StatsController -. "getTransactions" .-> PaymentService(Payment<br/>Service)
    StatsController -. "getAll<br/>Completed<br/>Payments" .-> PaymentService
  end

  subgraph "Menu endpoitns"
    MenuRouter -. "Makes method calls <br/>for menu, menu item<br/> & price data" .-> MenuController(Menu<br/>Controller)
    MenuController -. "getAvailability" .-> OperatorService(Operator<br/>Service)
  end

  MenuController -. "getByLookUpId" .-> MenuStore(DynamoDB<br/>menu-store)
  MenuController -. "getPrices<br/>ByBrandTier" .-> PriceStore(DynamoDB<br/>price-store)
  OperatorService -. "getAvailability" .-> PatOperator(PAT Operator API)
  MenuController -. "getMenu<br/>ItemV3<br/>(getPOSMenuItem)" .-> Yext
  MenuController -. "getMenu<br/>ItemV3<br/>(getItemModifiers)" .-> Yext
  MenuController -. "getById" .-> RestaurantStore("DynamoDB<br/>restaurant-store")

  RestaurantController -. "getById" .-> RestaurantStore
  RestaurantController -. "getRestaurant<br/>ByBrand" .-> RestaurantStore

  YumpingoController -. "getById" .-> RestaurantStore
  YumpingoController -. "getReviewUrl" .-> Yumpingo(Yumpingo<br/>API)

  EmailController -. "getById" .-> RestaurantStore
  EmailController -. "postContact" .-> Atreemo
  EmailController -. "communication<br/>Preference" .-> Atreemo
  EmailController -. "sendElement" .-> Atreemo

  DonationController -. "getById" .-> RestaurantStore
  DonationService -. "sendCalculation<br/>Request" .-> Pennies(Pennies<br/>API)
  DonationService -. "logDonation" .-> Pennies

  StatsController -. "postTransaction" .-> Atreemo

  PaymentService -. "getTransactions" .-> PATPayment(PAT Payment API<br/><br/>pat-payment)
  PaymentService -. "getAll<br/>Completed<br/>Payments" .-> PATPayment


  FAQRouter -. "getFAQs" .-> Yext
```

## OAT Restaurant API - C3 Diagram
```mermaid
%%{init: {'theme':'base','themeVariables': { 'lineColor': '#ffffff', }}}%%
graph TB

  Client -. "Get Restaurant<br/> By Id<br/>/v1/restaurants/:id" .-> RestaurantRouter(Restaurant<br/>Router)
  Client -. "Get Restaurant<br/> By Brand<br/>v1/restaurants/" .-> RestaurantRouter
  Client -. "Get Timezone<br/>v1/restaurants<br/>/:id/timezone" .-> RestaurantRouter

  Client -. "Get Items<br/>/v1/menus/<br/>:restaurantId/items" .-> MenuRouter(Menu<br/>Router)
  Client -. "Get Availability<br/>/v1/menus/<br/>:restaurantId/availability" .-> MenuRouter(Menu<br/>Router)
  Client -. "Get Prices<br/>/v1/menus/:restaurantId/prices" .-> MenuRouter(Menu<br/>Router)
  Client -. "Get Menus<br/>/v2/menus" .-> MenuRouter(Menu<br/>Router)

  subgraph "<strong>OAT Restaurant API Restaurant endpoints</strong>"
  RestaurantRouter -. "getRestaurant<br/>ById" .-> RestaurantController(Restaurant<br/>Controller)
  RestaurantController -. "getById" .-> DynamoDB(Dynamo DB<br/>restaurant-store)
  RestaurantRouter -. "getRestaurant<br/>ByBrand" .-> RestaurantController
  RestaurantController -. "getBrand<br/>Enabled" .-> DynamoDB(<strong>Dynamo DB</strong><br/><br/>restaurant-store)
  RestaurantRouter -. "getTimezone" .-> RestaurantController
  end

  subgraph "<strong>OAT Restaurant API - Menu endpoints</strong>"
  MenuRouter -. "getItems" .-> MenuController(Menu<br/>Controller)
  MenuController -. "getById" .-> RestaurantStore(Dynamo DB<br/>restaurant-store)
  MenuController -. "getByLookUpId" .-> MenuStore(Dynamo DB<br/>menu-store)
  MenuRouter -. "getAvailability" .-> MenuController(Menu<br/>Controller)
  MenuController -. "getAvailability" .-> OperatorService(Operator<br/>Service)
  MenuRouter -. "get<br/>Prices" .-> MenuController(Menu<br/>Controller)
  MenuController -. "getPricesByBrandTier" .-> PriceStore(Dynamo DB<br/>price-store)
  MenuRouter -. "getMenus" .-> MenuController(Menu<br/>Controller)
  end
```

## OAT Context Diagram

```mermaid
graph TB
  linkStyle default fill:#ffffff

  subgraph enterprise [Azzurri Group OAT System]
    style enterprise fill:#ffffff,stroke:#444444,color:#444444

    2["<div style='font-weight: bold'>Waiter</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Waiter of Zizzi or ASK<br />Italian restaurants who look<br />to accept payment for the<br />table using PDQ application</div>"]
    style 2 fill:#999999,stroke:#6b6b6b,color:#ffffff
    3("<div style='font-weight: bold'>Order at Table</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows customer to join a<br />table, order food and pay for<br />food at one of Zizzi or ASK<br />Italian restaurants</div>")
    style 3 fill:#1168bd,stroke:#0b4884,color:#ffffff
  end

  1["<div style='font-weight: bold'>Customer</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Customer of Zizzi or ASK<br />Italian who looks at order<br />and pay at the table using<br />online Progressive web app</div>"]
  style 1 fill:#08427b,stroke:#052e56,color:#ffffff
  13("<div style='font-weight: bold'>Comtrex POS System</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows Order at Table<br />application to submit order<br />to kitchen, retrieve prices,<br />update payment and kick start<br />payment post process</div>")
  style 13 fill:#999999,stroke:#6b6b6b,color:#ffffff
  14("<div style='font-weight: bold'>Atreemo</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Customer Loyalty Platform</div>")
  style 14 fill:#999999,stroke:#6b6b6b,color:#ffffff
  15("<div style='font-weight: bold'>Stripe</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Payment Provider</div>")
  style 15 fill:#999999,stroke:#6b6b6b,color:#ffffff
  16("<div style='font-weight: bold'>Eagle Eye</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Gift Cards Payment Provider</div>")
  style 16 fill:#999999,stroke:#6b6b6b,color:#ffffff
  17("<div style='font-weight: bold'>Yext</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Menu & Restaurant Management</div>")
  style 17 fill:#999999,stroke:#6b6b6b,color:#ffffff
  18("<div style='font-weight: bold'>Pennies</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Donation system</div>")
  style 18 fill:#999999,stroke:#6b6b6b,color:#ffffff
  19("<div style='font-weight: bold'>Yumpingo</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Review system</div>")
  style 19 fill:#999999,stroke:#6b6b6b,color:#ffffff

  1-. "<div>Visits to order food and pay<br />at the table</div><div style='font-size: 70%'></div>" .->3
  2-. "<div>Uses to take payments at the<br />table via PDQ device</div><div style='font-size: 70%'></div>" .->3
  3-. "<div>Manage table, order and<br />post-payment process</div><div style='font-size: 70%'></div>" .->13
  2-. "<div>Manage table, order, take<br />payment, and post-payment<br />process</div><div style='font-size: 70%'></div>" .->13
  3-. "<div>Process customer order and<br />payments transactions to<br />allocate loyalty Z points to<br />customer</div><div style='font-size: 70%'></div>" .->14
  3-. "<div>Manage card payments</div><div style='font-size: 70%'></div>" .->15
  3-. "<div>Manage gift card payments</div><div style='font-size: 70%'></div>" .->16
  3-. "<div>Manage common menu and<br />restaurant data</div><div style='font-size: 70%'></div>" .->17
  3-. "<div>Calculate & submit donation<br />by bill value to charities<br />supported by Pennies</div><div style='font-size: 70%'></div>" .->18
  3-. "<div>Collect customer reviews</div><div style='font-size: 70%'></div>" .->19
```

## OAT Container Diagram

```mermaid
graph TB
  linkStyle default fill:#ffffff

  13("<div style='font-weight: bold'>Comtrex POS System</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Allows Order at Table<br />application to submit order<br />to kitchen, retrieve prices,<br />update payment and kick start<br />payment post process</div>")
  style 13 fill:#999999,stroke:#6b6b6b,color:#ffffff
  14("<div style='font-weight: bold'>Atreemo</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Customer Loyalty Platform</div>")
  style 14 fill:#999999,stroke:#6b6b6b,color:#ffffff
  15("<div style='font-weight: bold'>Stripe</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Payment Provider</div>")
  style 15 fill:#999999,stroke:#6b6b6b,color:#ffffff
  16("<div style='font-weight: bold'>Eagle Eye</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Gift Cards Payment Provider</div>")
  style 16 fill:#999999,stroke:#6b6b6b,color:#ffffff
  17("<div style='font-weight: bold'>Yext</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Menu & Restaurant Management</div>")
  style 17 fill:#999999,stroke:#6b6b6b,color:#ffffff
  18("<div style='font-weight: bold'>Pennies</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Donation system</div>")
  style 18 fill:#999999,stroke:#6b6b6b,color:#ffffff
  19("<div style='font-weight: bold'>Yumpingo</div><div style='font-size: 70%; margin-top: 0px'>[Software System]</div><div style='font-size: 80%; margin-top:10px'>Review system</div>")
  style 19 fill:#999999,stroke:#6b6b6b,color:#ffffff
  1["<div style='font-weight: bold'>Customer</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Customer of Zizzi or ASK<br />Italian who looks at order<br />and pay at the table using<br />online Progressive web app</div>"]
  style 1 fill:#08427b,stroke:#052e56,color:#ffffff
  2["<div style='font-weight: bold'>Waiter</div><div style='font-size: 70%; margin-top: 0px'>[Person]</div><div style='font-size: 80%; margin-top:10px'>Waiter of Zizzi or ASK<br />Italian restaurants who look<br />to accept payment for the<br />table using PDQ application</div>"]
  style 2 fill:#999999,stroke:#6b6b6b,color:#ffffff

  subgraph 3 [Order at Table]
    style 3 fill:#ffffff,stroke:#444444,color:#444444

    10("<div style='font-weight: bold'>Payment API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div><div style='font-size: 80%; margin-top:10px'>API for handling payment made<br />by Order at table payments</div>")
    style 10 fill:#438dd5,stroke:#2e6295,color:#ffffff
    11[("<div style='font-weight: bold'>OAT DynamoDB</div><div style='font-size: 70%; margin-top: 0px'>[Container: NoSQL Database]</div><div style='font-size: 80%; margin-top:10px'>Stores client session, table,<br />table stats, restaurants and<br />payments data</div>")]
    style 11 fill:#438dd5,stroke:#2e6295,color:#ffffff
    12[("<div style='font-weight: bold'>OAT PaymentsV2 DB</div><div style='font-size: 70%; margin-top: 0px'>[Container: SQL Database]</div><div style='font-size: 80%; margin-top:10px'>Stores payments transaction<br />data</div>")]
    style 12 fill:#438dd5,stroke:#2e6295,color:#ffffff
    4("<div style='font-weight: bold'>Progressive Web Application</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript and React]</div><div style='font-size: 80%; margin-top:10px'>Provides the ordering and<br />payment functionality to<br />customers via mobile/web<br />browser</div>")
    style 4 fill:#438dd5,stroke:#2e6295,color:#ffffff
    5("<div style='font-weight: bold'>PDQ Application</div><div style='font-size: 70%; margin-top: 0px'>[Container: Native App]</div><div style='font-size: 80%; margin-top:10px'>Provides the payment<br />capabilities to waiters via<br />PDQ Device</div>")
    style 5 fill:#438dd5,stroke:#2e6295,color:#ffffff
    6("<div style='font-weight: bold'>Gateway API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div><div style='font-size: 80%; margin-top:10px'>Front facing API for the<br />Azzurri Group Order at Table<br />application. User Interface<br />layers only interacts with<br />Gateway API</div>")
    style 6 fill:#438dd5,stroke:#2e6295,color:#ffffff
    7("<div style='font-weight: bold'>Config API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div><div style='font-size: 80%; margin-top:10px'>Provides capability to<br />retrieve and store<br />configuration data as json<br />payload as a whole or by<br />property</div>")
    style 7 fill:#438dd5,stroke:#2e6295,color:#ffffff
    8("<div style='font-weight: bold'>Restaurant API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div><div style='font-size: 80%; margin-top:10px'>API for handling restaurant<br />information like menu,<br />prices, table stats,<br />donation, reviews and<br />provides email capability</div>")
    style 8 fill:#438dd5,stroke:#2e6295,color:#ffffff
    9("<div style='font-weight: bold'>Operator API</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript Microservice]</div><div style='font-size: 80%; margin-top:10px'>API for handling order and<br />post-payment management<br />capabilities via API calls to<br />Comtrex</div>")
    style 9 fill:#438dd5,stroke:#2e6295,color:#ffffff
  end

  2-. "<div>Manage table, order, take<br />payment, and post-payment<br />process</div><div style='font-size: 70%'></div>" .->13
  1-. "<div>Visits oat websiste using<br />mobile/web browswer</div><div style='font-size: 70%'>[HTTPS]</div>" .->4
  2-. "<div>Uses Optomany Payment Device</div><div style='font-size: 70%'>[HTTPS]</div>" .->5
  5-. "<div>Wraps the oat web app into a<br />web view</div><div style='font-size: 70%'>[React Navtive Web View]</div>" .->4
  4-. "<div>Makes API calls to retrieve<br />oat customer state data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->6
  4-. "<div>Makes API calls to retrieve<br />configuration data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->7
  4-. "<div>Makes API calls to complete<br />payment</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->15
  6-. "<div>Makes API calls to retrieve<br />and store menu, restaurant<br />dat from Yext and expose<br />endpoints for OAT consumption</div><div style='font-size: 70%'>[JSON/HTTP]</div>" .->8
  6-. "<div>Makes API calls to manage<br />order & post-payment with POS<br />system</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->9
  6-. "<div>Makes API calls to manage<br />payment transactions made<br />from OAT application</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->10
  6-. "<div>Makes API calls to store and<br />retrieve configuration data<br />for OAT application</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->7
  10-. "<div>Makes API calls via SDK to<br />manage payment transactions</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->15
  10-. "<div>Reads and writes payment<br />commitments and transactions<br />includes stripe payments and<br />gift card payments</div><div style='font-size: 70%'>[SQL]</div>" .->12
  10-. "<div>Reads and writes payment<br />commitments and transactions<br />includes stripe payments and<br />gift card payments</div><div style='font-size: 70%'>[NoSQL]</div>" .->11
  6-. "<div>Reads and write sessions,<br />basket, table, table stats,<br />items and payments data</div><div style='font-size: 70%'>[NoSQL]</div>" .->11
  7-. "<div>Reads and writes<br />configuration data</div><div style='font-size: 70%'>[NoSQL]</div>" .->11
  8-. "<div>Reads and writes menus prices<br />and restaurants data</div><div style='font-size: 70%'>[NoSQL]</div>" .->11
  8-. "<div>Retrieves menu and restaurant<br />data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->17
  8-. "<div>Post transaction process to<br />allocate loyalty Z points to<br />customer</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->14
  8-. "<div>Calculate donation amount on<br />bill value and log donations<br />made to charities on Pennies<br />system</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->18
  9-. "<div>Retrieve and update table,<br />order and post-payment<br />management data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->13
  10-. "<div>Check balance and redeem gift<br />cards to pay for the order</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->16
  6-. "<div>Send customer review data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->19
```

## OAT Restaurant API Component Diagram
```mermaid
graph TB
  linkStyle default fill:#ffffff

  4("<div style='font-weight: bold'>OAT Frontend (PWA)</div><div style='font-size: 70%; margin-top: 0px'>[Container: JavaScript and React]</div><div style='font-size: 80%; margin-top:10px'>Provides the ordering and<br />payment functionality to<br />customers via mobile/web<br />browser</div>")
  style 4 fill:#438dd5,stroke:#2e6295,color:#ffffff

  subgraph 8 [Restaurant API]
    style 8 fill:#ffffff,stroke:#444444,color:#444444

    9("<div style='font-weight: bold'>Menus Router</div><div style='font-size: 70%; margin-top: 0px'>[Component: KOA JS Router]</div><div style='font-size: 80%; margin-top:10px'>Exposes endpoints to GET menu<br />data</div>")
    style 9 fill:#85bbf0,stroke:#5d82a8,color:#000000
  end

  4-. "<div>Makes API calls to retrieve<br />menu data</div><div style='font-size: 70%'>[JSON/HTTPS]</div>" .->9
```

## Context Diagram - Mermaid v2
```mermaid
graph TB

    subgraph SystemContext [OAT System Context]
    style SystemContext fill:#fff,stroke:#ccc,stroke-width:1px,color:#fff,stroke-dasharray: 5 5
    Waiter[fa:fa-user Waiter] -. "Uses to take<br/>payments at the<br/>table via PDQ<br/>device" .-> OAT[Order at Table]
    
    end

    Customer[fa:fa-user Customer] -. "Visits to order<br/>food and pay at<br/> the table" .-> OAT
    linkStyle 0 stroke:#ccc,stroke-width:1px,color:#fff,stroke-dasharray: 5 5
    linkStyle 1 stroke:#ccc,stroke-width:1px,color:#fff,stroke-dasharray: 5 5
```
