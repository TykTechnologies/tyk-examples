# Coffee Shop API

The Coffee Shop API allows you to manage coffee shop operations, including viewing the menu, placing orders, and retrieving order details. The API is secured using an API key, which must be passed in the `Authorization` header of each request.

## Base URLs

The API is accessible at the following base URLs:

- Production: `https://continuing-grammar-gw.aws-euc1.cloud-ara.tyk.io/coffee-shop`
- Development: `http://continuing-grammar-gw.aws-euc1.cloud-ara.tyk.io`

## Authentication

The API uses API Key authentication. Include your API key in the `Authorization` header of every request:

```
Authorization: <your-api-key>
```

## Endpoints

### 1. Get the Full Menu

**Endpoint:** `/menu`  
**Method:** `GET`

Retrieve the complete menu of available coffee and food items.

#### Request Example:

```bash
curl -X GET \
  -H "Authorization: <your-api-key>" \
  https://continuing-grammar-gw.aws-euc1.cloud-ara.tyk.io/coffee-shop/menu
```

#### Response Example:

```json
[
  {
    "id": 1,
    "name": "Tykspresso",
    "description": "A shot of rich, dark coffee",
    "price": 2.5
  },
  {
    "id": 2,
    "name": "CappuTyko",
    "description": "Espresso with steamed milk and foam",
    "price": 3.5
  }
]
```

### 2. Place an Order

**Endpoint:** `/orders`  
**Method:** `POST`

Create a new order by specifying customer details and the items they wish to purchase.

#### Request Example:

```bash
curl -X POST \
  -H "Authorization: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{
    "customerName": "John Doe",
    "address": "123 Coffee St, Barista City",
    "contactNumber": "123456789",
    "items": [
      {"itemId": 1, "quantity": 2},
      {"itemId": 3, "quantity": 1, "specialInstructions": "No sugar"}
    ]
  }' \
  https://continuing-grammar-gw.aws-euc1.cloud-ara.tyk.io/coffee-shop/orders
```

#### Response Example:

```json
{
  "orderId": 123
}
```

### 3. Get Order Details

**Endpoint:** `/orders/{orderId}`  
**Method:** `GET`

Retrieve details of a specific order by its ID.

#### Request Example:

```bash
curl -X GET \
  -H "Authorization: <your-api-key>" \
  https://continuing-grammar-gw.aws-euc1.cloud-ara.tyk.io/coffee-shop/orders/123
```

#### Response Example:

```json
{
  "orderId": 123,
  "customerName": "John Doe",
  "address": "123 Coffee St, Barista City",
  "contactNumber": "123456789",
  "items": [
    {"itemId": 1, "name": "Tykspresso", "quantity": 2},
    {"itemId": 3, "name": "Latte", "quantity": 1, "specialInstructions": "No sugar"}
  ],
  "status": "Preparing",
  "totalPrice": 8.5
}
```

### Error Responses

- `404 Not Found`: The requested resource could not be found.
- `422 Unprocessable Entity`: The request is invalid or incomplete.

## Additional Information

### Mock Responses

The API has mock responses enabled for testing purposes. Use the API without interacting with the actual backend.

### Middleware

- **Traffic Logs**: Enabled to log traffic for debugging purposes.
- **Request Validation**: Ensures that requests match the expected structure, returning `422` for invalid inputs.

## Notes

- Replace `<your-api-key>` with the API key provided to you.
- The `Authorization` header is mandatory for all endpoints.
- Contact the support team for any issues or questions about the API.

