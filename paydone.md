# API Documentation

## Endpoint: Order Status

### URL
`https://cloud.toprent.app/api/public/order-status`

### Method
`POST`

### Description
This API returns the status of an order. It requires the order number, widget ID, and a secret order token to ensure that only the order owner can access the order details.

### Request Body
The request body should be a JSON object with the following fields:

| Field       | Type   | Required | Description                                                                 |
|-------------|--------|----------|-----------------------------------------------------------------------------|
| orderNumber | String | Yes      | The number of the order.                                                    |
| orderToken  | String | Yes      | The secret token received from the post-order API response.                 |
| widgetId    | String | Yes      | The ID of the widget to retrieve the company and payment method details.    |

### Example Request
```json
{
    "orderNumber": "exampleOrder123",
    "orderToken": "secretTokenXYZ",
    "widgetId": "exampleWidgetId123"
}
```

### Response
The response will be a JSON object containing the following fields:

| Field         | Type   | Description                                                                                           |
|---------------|--------|-------------------------------------------------------------------------------------------------------|
| companyName   | String | The name of the company.                                                                              |
| logo          | Object | An object containing the company logo and website link:                                               |
|               |        | - `image`: URL of the company logo.                                                                   |
|               |        | - `link`: URL of the company website.                                                                 |
| widgetLocale  | String | The locale code for the widget (e.g., "en", "ru").                                                    |
| order         | Object | Information about the order.                                                                          |
| currency      | String | The currency of the order.                                                                            |
| contacts      | Object | Contact information:                                                                                  |
|               |        | - `phone`: Phone number of the company.                                                               |
|               |        | - `email`: Email address of the company.                                                              |
|               |        | - `website`: Website of the company.                                                                  |
| status        | String | The status of the order (`requested`, `confirmed`, `declined`).                                       |
| gtagId        | String | The Google Tag Manager ID for tracking.                                                               |

### Example Response
```json
{
    "companyName": "Example Company",
    "logo": {
        "image": "https://example.com/logo.png",
        "link": "https://example.com"
    },
    "widgetLocale": "en",
    "order": { /* TODO */ },
    "currency": "USD",
    "contacts": {
        "phone": "+1234567890",
        "email": "contact@example.com",
        "website": "https://example.com"
    },
    "status": "confirmed",
    "gtagId": "GTM-XXXXXX"
}
```