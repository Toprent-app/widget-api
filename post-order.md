## Endpoint: Post Order

### URL
`https://cloud.toprent.app/api/public/post-order`

### Method
`POST`

### Description
This API creates an order in the system. You provide all customer data as well as rental information. If the customer already exists in the system, a new one will not be created. We use `FormData` to attach customer document files to the request. After the order is created, the user is redirected to the `/paydone` page.

### Request Body
The request body should be sent as `FormData`. The following fields should be included:

| Field                   | Type   | Required | Description                                                                 |
|-------------------------|--------|----------|-----------------------------------------------------------------------------|
| driverLicensePhoto      | File   | No       | The driver's license photo file.                                            |
| driverLicenseValidDate  | String | No       | The validity date of the driver's license.                                  |
| driverLicenseNumber     | String | No       | The driver's license number.                                                |
| passportPhoto           | File   | No       | The passport photo file.                                                    |
| passportValidDate       | String | No       | The validity date of the passport.                                          |
| passportNumber          | String | No       | The passport number.                                                        |
| startAddress            | String | Yes      | The JSON stringified start address.                                         |
| endAddress              | String | Yes      | The JSON stringified end address.                                           |
| name                    | String | Yes      | The name of the person making the order.                                    |
| surname                 | String | Yes      | The surname of the person making the order.                                 |
| email                   | String | Yes      | The email address of the person making the order.                           |
| phone                   | String | Yes      | The phone number of the person making the order.                            |
| vehicleId               | String | Yes      | The ID of the vehicle being ordered.                                        |
| dateFrom                | String | Yes      | The start date for the vehicle rental in ISO 8601 format.                   |
| dateTo                  | String | Yes      | The end date for the vehicle rental in ISO 8601 format.                     |
| widgetId                | String | Yes      | The ID of the widget making the request.                                    |
| cancelUrl               | String | No       | The URL to redirect to if the payment is canceled.                          |
| successUrl              | String | No       | The URL to redirect to if the payment is successful.                        |
| deliveryPrice           | String | Yes      | The delivery price as a string.                                             |
| extraServices           | String | No       | A JSON stringified array of extra services, e.g., `'[{ "id": "extra1" }]'`. |
| currency                | String | No       | The currency for the payment.

```gql
  type Address {
    id: ID!
    country: String!
    state: String
    city: String!
    street: String
    number: String
    zipCode: String
    formattedAddress: String!
    addressNote: String
    coordinates: [Float!]
  }
```

```js
const formData = new FormData();
formData.append("driverLicensePhoto", fileInput.files[0]);
formData.append("driverLicenseValidDate", "2023-07-17");
formData.append("driverLicenseNumber", "DL123456");
formData.append("passportPhoto", fileInput.files[1]);
formData.append("passportValidDate", "2023-07-17");
formData.append("passportNumber", "P123456");
formData.append("startAddress", JSON.stringify({ /* Address */ })); // type Address
formData.append("endAddress", JSON.stringify({ /* Address */ })); // type Address
formData.append("name", "John");
formData.append("surname", "Doe");
formData.append("email", "john.doe@example.com");
formData.append("phone", "+1234567890");
formData.append("vehicleId", "vehicle123");
formData.append("dateFrom", "2023-07-17T00:00:00Z");
formData.append("dateTo", "2023-07-20T23:59:59Z");
formData.append("widgetId", "exampleWidgetId123");
formData.append("deliveryPrice", "10.00");
formData.append("extraServices", JSON.stringify([{ id: "extraService1" }]));

const response = await fetch('https://cloud.toprent.app/api/public/post-order', {
    method: 'POST',
    body: formData
});
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

### Handling URLs for Payment
In the response from the `checkout-page` API, you will receive a variable `paymentVariant`. Depending on its value, you can compose the values for the `cancelUrl` and `successUrl` variables.

#### When Payment is Involved
If payment is required, the URLs should include the payment variant and status:

```javascript
if (paymentVariant === "preAuthorization") {
  const successUrl = `${SITE_URL}${nextStepPath}?paymentVariant=preAuthorization&status=success?locale=${locale}`;
  const cancelUrl = `${SITE_URL}${resolvedUrl}&paymentVariant=preAuthorization&status=cancel?locale=${locale}`;
  formData.append("cancelUrl", cancelUrl);
  formData.append("successUrl", successUrl);
}

if (paymentVariant === "cardVerification") {
  formData.append("cancelUrl", `${SITE_URL}${nextStepPath}?paymentVariant=cardVerification&status=cancel&?locale=${locale}`);
  formData.append("successUrl", `${SITE_URL}${nextStepPath}?paymentVariant=cardVerification&status=success&?locale=${locale}`);
}
```
