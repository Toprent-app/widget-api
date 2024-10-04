# API Documentation Overview

Each request must include a widget ID, which allows the request to be associated with the correct company. All responses include a Google Tag Manager (gtag) ID for analytics.

## Step 1: Get Available Vehicles
The user first retrieves a list of available vehicles.

### Endpoint
`https://cloud.toprent.app/api/public/get-available-vehicles`

## Step 2: Get Vehicle By ID
When the user selects a vehicle, they request details for the future rental. The rental details are calculated in real-time considering discounts, seasonality, and reducing coefficients. Therefore, the request for rental details includes dates.

### Endpoint
`https://cloud.toprent.app/api/public/get-vehicle-by-id`

## Step 3: Checkout Page
The next step is the form for creating an order.

### Endpoint
`https://cloud.toprent.app/api/public/checkout-page`

## Step 4: Post Order
After the user fills out the form and submits it, an order is created on the server. The response contains variables that allow constructing a URL for the next steps, which vary based on the payment configuration.

### Endpoint
`https://cloud.toprent.app/api/public/post-order`


## Step 5: Order Status
This API shows the status of the order. The response contains detailed information about the order status, company, and contact information.

### Endpoint
`https://cloud.toprent.app/api/public/order-status`

### FAQ
`https://docs.google.com/document/d/17QcZ19DAdUjf0UnY8v3usG8SnR0NBlhc6cfhqv80muE/edit`