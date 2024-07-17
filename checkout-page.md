# API Documentation

## Endpoint: Checkout Page

### URL
`https://cloud.toprent.app/api/public/checkout-page`

### Method
`POST`

### Description
This API returns data for displaying the checkout page form. It provides details about the company and payment method associated with the given widget.

### Request Body
The request body should be a JSON object with the following field:

| Field    | Type   | Required | Description                                                              |
|----------|--------|----------|--------------------------------------------------------------------------|
| widgetId | String | Yes      | The ID of the widget to retrieve the company and payment method details. |

### Example Request
```json
{
    "widgetId": "exampleWidgetId123"
}
```

### Example Response
```json
{
    "companyName": "Example Company",
    "logo": "https://example.com/logo.png",
    "widgetLocale": "en",
    "currency": "USD",
    "paymentVariant": "preAuthorization",
    "paymentPercent": 20,
    "status": "active",
    "gtagId": "GTM-XXXXXX"
}
```