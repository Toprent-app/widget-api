## Endpoint: Get Available Vehicles

### URL
`https://cloud.toprent.app/api/public/get-available-vehicles`

### Method
`POST`

### Request Body
The request body should be a JSON object with the following fields:

| Field     | Type   | Required | Description                                                                                        |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------|
| widgetId  | String | Yes      | The ID of the widget making the request. Used to identify the company and associated vehicles.     |
| dateFrom  | String | Yes      | The start date for the vehicle availability search in ISO 8601 format (e.g., `2023-07-17T00:00:00Z`). |
| dateTo    | String | Yes      | The end date for the vehicle availability search in ISO 8601 format (e.g., `2023-07-20T23:59:59Z`).  |
| locale    | String | Yes      | The 2-letter language code representing the locale. Available options are specified in the `Locale` enum. |
| office    | String | No       | The office ID to filter available vehicles for a specific office.                                 |

### Example Request
```json
{
    "widgetId": "exampleWidgetId123",
    "dateFrom": "2023-07-17T00:00:00Z",
    "dateTo": "2023-07-20T23:59:59Z",
    "locale": "en",
    "office": "officeId456"
}
```

### Locale Enum
The `locale` field must be one of the following values:

| Code | Language      |
|------|---------------|
| ru   | Russian       |
| en   | English       |
| it   | Italian       |
| de   | German        |
| fr   | French        |
| es   | Spanish       |
| pt   | Portuguese    |
| pl   | Polish        |
| zh   | Chinese       |
| nl   | Dutch         |
| cs   | Czech         |
| lt   | Lithuanian    |

### Response
The response will be a JSON object containing the following fields:

| Field                        | Type    | Description                                                                                           |
|------------------------------|---------|-------------------------------------------------------------------------------------------------------|
| data                         | Array   | An array of short vehicle information.                                                                |
| messages                     | Array   | An array of messages.                                                                                 |
| companyName                  | String  | The name of the company.                                                                              |
| logo                         | Object  | An object containing the company logo and website link:                                               |
|                              |         | - `image`: URL of the company logo.                                                                   |
|                              |         | - `link`: URL of the company website.                                                                 |
| days                         | Number  | The number of days.                                                                                   |
| currency                     | String  | The symbol of the currency used.                                                                      |
| addresses                    | Array   | An array of formatted addresses.                                                                      |
| categories                   | Array   | An array of vehicle categories filtered by type and locale.                                           |
| includeDelivery              | Boolean | A flag indicating whether delivery is included and if Google addresses are used.                      |
| sortByIncreasingDeliveryPrice| Boolean | A feature used for sorting vehicles by distance from their base, based on delivery price and Google addresses. |
| gtagId                       | String  | The Google Tag Manager ID for tracking.                                                               |
| vehicleTypes                 | Array   | An array of vehicle types.                                                                            |

### Example Response
```json
{
    "data": [
        {
            "vehicleId": "vehicle123",
            "modelName": "Model X",
            "price": 100.00,
            "currency": "USD",
            "availableFrom": "2023-07-17T00:00:00Z",
            "availableTo": "2023-07-20T23:59:59Z"
        }
    ],
    "messages": [
        {
            "type": "info",
            "text": "Limited time offer!"
        }
    ],
    "companyName": "Example Company",
    "logo": {
        "image": "https://example.com/logo.png",
        "link": "https://example.com"
    },
    "days": 3,
    "currency": "$",
    "addresses": [
        {
            "street": "123 Main St",
            "city": "Anytown",
            "country": "USA"
        }
    ],
    "categories": [
        {
            "type": "SUV",
            "locale": "en"
        }
    ],
    "includeDelivery": true,
    "sortByIncreasingDeliveryPrice": true,
    "gtagId": "GTM-XXXXXX",
    "vehicleTypes": [
        {
            "type": "car",
            "description": "A comfortable car."
        }
    ]
}
