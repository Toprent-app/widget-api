## Endpoint: Get Vehicle by ID

### URL
`https://cloud.toprent.app/api/public/get-vehicle-by-id`

### Method
`POST`

### Request Body
The request body should be a JSON object with the following fields:

| Field         | Type   | Required | Description                                                                                        |
|---------------|--------|----------|----------------------------------------------------------------------------------------------------|
| id            | String | Yes      | The ID of the vehicle.                                                                             |
| widgetId      | String | Yes      | The ID of the widget making the request. Used to identify the company and associated vehicles.     |
| dateFrom      | String | Yes      | The start date for the vehicle availability search in ISO 8601 format (e.g., `2023-07-17T00:00:00Z`). |
| dateTo        | String | Yes      | The end date for the vehicle availability search in ISO 8601 format (e.g., `2023-07-20T23:59:59Z`).  |
| locale        | String | Yes      | The 2-letter language code representing the locale. Available options are specified in the `Locale` enum. |
| extraServices | Array  | No       | An array of extra services. The array should be represented as a string, e.g., `'[{ "id": "extraService1" }]'`. |

### Example Request
```json
{
    "id": "vehicle123",
    "widgetId": "exampleWidgetId123",
    "dateFrom": "2023-07-17T00:00:00Z",
    "dateTo": "2023-07-20T23:59:59Z",
    "locale": "en",
    "extraServices": "[{ \"id\": \"extraService1\" }, { \"id\": \"extraService2\" }]"
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
The response will be a JSON object containing all the parameters of the vehicle and the price, including all discounts and calculations.
