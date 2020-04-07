# Annual Tickets

After the purchase of an annual ticket, the customer receives an e-mail with a link to the shop with a token. Only one personalization will be allowed per `ticket_sale`. You can personalize with `customer` and `customer_address` which are belong to each `order` or the personalization can reference other customer or none at all.

## Find an order

`GET https://demo.gomus.de/api/v4/annual/order?token=:token`

```shell
curl "https://demo.gomus.de/api/v4/annual/order?token=:token"
```

> The above command returns JSON structured like this:

```json
{
  "order": {
    "id": 85,
    "customer": {
      "id": 18,
      "name": "Bärbel",
      "surname": "Monkey",
      "email": "baerbel@giantmonkey.de",
      "salutation_id": 1,
      "addresses": [
        {
          "id": 18,
          "zip": "10119",
          "street": "Brunnstr. 7d",
          "country_id": 60,
          "city": "Berlin"
        }
      ]
    },
    "shipping_address_id": 18,
    "ticket_sales": [
      {
        "id": 51,
        "title": "Jahreskarte",
        "description": "",
        "start_at": "2019-11-16T00:00:10+01:00",
        "sent_at": null,
        "status": "ready_to_send",
        "is_personalizable": true,
        "personalizations": [
          {
            "id": 10,
            "ready": true,
            "customer": {
              "id": 46,
              "name": "Adrian",
              "surname": "Fuhrmann",
              "email": "adrian@giantmonkey.de",
              "salutation_id": 1,
              "addresses": [
                {
                  "id": 46,
                  "zip": "10119",
                  "street": "Brunnenstr. 7D",
                  "country_id": 60,
                  "city": "Berlin"
                }
              ]
            },
            "address_id": 12,
            "dispatch_mode_id": 3
          }
        ]
      }
    ]
  }
}
```

### Response

The JSON response contains a data of an order you requested.

- id (integer), the unique database id of the order
- customer (object, the buyer of the order), contains id, name, e-mail address, salutation_id and adresses (array)
- addresses (object `customer_addresses`, array of the addresses of the buyer of the order), contains id, zip, street, country_id and city
- shipping_address_id (integer), the unique database id of the shipping address
- ticket_sales (array of ticket_sales), contains id, title, description, start_at, sent_at, status, is_personalizable (boolean) and personalizations
- personalizations (object), contains id, customer (object, on whom this annual ticket is personalized), customer_addresses (array of all addresses of the customer), address_id (integer, the address of the customer who is personalized to this annual ticket) and dispatch_mode_id (integer)


## Create new customer

Create new `customer` and `customer_address` if the buyer wants to personalize the ticket for another customer.

`POST https://demo.gomus.de/api/v4/annual/customers?token=:token`

```shell
curl "https://demo.gomus.de/api/v4/annual/customers?token=:token"
```

> The above command assumes the JSON is structured like this:

```json
{
  "customer": {
    "name": "Peter",
    "surname": "Pan",
    "email": "peter@giantmonkey.de",
    "customer_salutation_id": 1,
    "addr_city": "Berlin",
    "addr_country_id": 60,
    "addr_street": "Brunnenstraße 7D",
    "addr_zip": "10119"
  }
}
```

### Required attributes

- name (string)
- surname (string)
- email (string)
- customer_salutation_id (integer)
- addr_city (string)
- addr_country_id (integer)
- addr_street (string)
- addr_zip (string)



## Update personalization

The existing personalization can be updated (the customer and the address can be changed).
dispatch_mode_id is also accepted.

`PUT https://demo.gomus.de/api/v4/annual/personalizations/:id?token=:token`

```shell
curl "https://demo.gomus.de/api/v4/annual/personalizations/:id?token=:token"
```

> The above command assumes the JSON is structured like this:

```json
{
  "personalization": {
    "customer_personalization_token": "13fe3a0d-5983-4db5-a316-eef2f0da8603",
    "customer_adress_id": 44
  }
}
```


### Required attributes

- customer_personalization_token (string), the unique identifier generated randomly for each customer
- customer_adress_id (integer), the unique database id of the customer_adress

### Available parameters:

- dispatch_mode_id (integer), the unique database id of the dispatch_mode

## Update a Ticket Sale

The start time (`start_at`) of the annual ticket can be changed.

`PUT https://demo.gomus.de/api/v4/annual/ticket_sales/:id?token=:token`

```shell
curl "https://demo.gomus.de/api/v4/annual/ticket_sales/:id?token=:token"
```

> The above command assumes the JSON is structured like this:

```json
{
  "ticket_sale": {
    "start_at": "2019-11-12 10:00:00"
  }
}
```

### Required attributes

- start_at (datetime)

### Available parameters:

- dispatch_mode_id (integer), the unique database id of the dispatch_mode
