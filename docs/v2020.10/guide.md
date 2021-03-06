The Purplship API is organized around REST. Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, \
returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

You can use the Purplship API with carriers sandbox servers by setting the `test` flag to `True` when you configure your carrier connection.\
The **carrier id** you specify in the request determines whether the request is live mode or test mode.

The Purplship API differs for every instances as we release new versions and tailor functionality.\
Check your local instance API reference to see docs customized to your version of the API.

---

## Clients

The Purplship team currently actively maintains the following client libraries

- [purplship-php-client](https://github.com/PurplShip/purplship-php-client)
- [purplship-python-client](https://github.com/PurplShip/purplship-python-client)
- [purplship-typescript-client](https://github.com/PurplShip/purplship-typescript-client)

For any other programming language use our API [OpenAPI specification](https://github.com/PurplShip/purplship-server/tree/main/OpenAPI) to generate a client from the [swagger online editor](https://editor.swagger.io/)

*We actively maintain libraries based on our clients needs so contact us for enterprise need.*

<!-- tabs:start -->

#### **Python**

```shell
pip install purplship-python
```

#### **PHP**

```shell
composer require purplship/purplship-php
```

#### **Typescript**

```shell
yarn add @purplship/purplship
```

<!-- tabs:end -->

---

## Authentication

The Purplship API uses API keys to authenticate requests. You can view and manage your API keys in the Purplship Administration panel.

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

Use your API key by assigning it to client `API_KEY`. The client library will then automatically send this key in each request. \
API requests without authentication will also fail.

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'
```

#### **PHP**

```php
require_once(__DIR__ . '/vendor/autoload.php');

$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';

const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');
```

<!-- tabs:end -->

---

## Errors

Purplship uses conventional HTTP response codes to indicate the success or failure of an API request. \
In general:\
Codes in the 2xx range indicate success. \
Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted). \
Codes in the 5xx range indicate an error with Purplship's servers.

| HTTP STATUS CODE SUMMARY     |                                                                                                  |
| ---------------------------: |:------------------------------------------------------------------------------------------------ |
|                     200 - OK | Everything worked as expected.                                                                   |
|            400 - Bad Request | The request was unacceptable, often due to missing a required parameter.                         |
|           401 - Unauthorized | No valid API key provided.                                                                       |
|              403 - Forbidden | The API key doesn't have permissions to perform the request.                                     |
|              404 - Not Found | The requested resource doesn't exist.                                                            |
|      429 - Too Many Requests | Too many requests hit the API too quickly. We recommend an exponential backoff of your requests. |
|               409 - Conflict | The API indicates a request conflict with current state of the target resource.                  |
|500, 502, 504 - Server Errors | Something went wrong on Purplship's end. (These are rare.)                                       |

---

## Addresses

|       | Endpoints          |
:-------|:------------------ |
`GET`   | /v1/addresses      |
`POST`  | /v1/addresses      |
`GET`   | /v1/addresses/{id} |
`PATCH` | /v1/addresses/{id} |

This is an object representing your Purplship shipping address. \
You can create, update and retrieve one or many addresses stored on your Purplship account.

- ### Retrieve addresses

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Addresses.list()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->addresses->list();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.addresses.list();
```

<!-- tabs:end -->

- ### Create an address

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Addresses.create({
    "address_line1": "5205 rue riviera",
    "person_name": "Jane Doe",
    "phone_number": "1 438 222-2222",
    "city": "Montreal",
    "country_code": "CA",
    "postal_code": "H8Z2Z3",
    "residential": True,
    "state_code": "QC"
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->addresses->create(new \Purplship\Model\Address([
    "address_line1" => "5205 rue riviera",
    "person_name" => "Jane Doe",
    "phone_number" => "1 438 222-2222",
    "city" => "Montreal",
    "country_code" => "CA",
    "postal_code" => "H8Z2Z3",
    "residential" => True,
    "state_code" => "QC"
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.addresses.create({
    "address_line1": "5205 rue riviera",
    "person_name": "Jane Doe",
    "phone_number": "1 438 222-2222",
    "city": "Montreal",
    "country_code": "CA",
    "postal_code": "H8Z2Z3",
    "residential": true,
    "state_code": "QC"
});
```

<!-- tabs:end -->

- ### Retrieve an address

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Addresses.retrieve('<addr_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->addresses->retrieve('<addr_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.addresses.retrieve('<addr_id>');
```

<!-- tabs:end -->

- ### Update an address

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Addresses.update(
    { "phone_number": "1 438 222-2222" },
    '<addr_id>'
)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->addresses->update(
    new \Purplship\Model\AddressData([ "phone_number" => "1 438 222-2222" ]),
    '<addr_id>'
);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.addresses.update(
    { "phone_number": "1 438 222-2222" },
    '<addr_id>'
);
```

<!-- tabs:end -->

---

## Carriers

|       | Endpoints                       |
:-------|:------------------------------- |
`GET`   | /v1/carriers                    |

You can retrieve one or many carriers configuration stored on your Purplship account.

- ### Retrieve configured carriers

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Carriers.list()
```

#### **PHP**

```php
$purplship->carriers->list();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.carriers.list();
```

<!-- tabs:end -->

---

## Customs Info

|        | Endpoints             |
:--------|:--------------------- |
`GET`    | /v1/customs_info      |
`POST`   | /v1/customs_info      |
`GET`    | /v1/customs_info/{id} |
`PATCH`  | /v1/customs_info/{id} |

This is an object representing your Purplship shipping customs info. \
You can create, update and retrieve one or many customs presets stored on your Purplship account.

- ### Retrieve Customs info presets

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Customs.list()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->addresses->list();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.addresses.list();
```

<!-- tabs:end -->

- ### Create a Custom info

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Customs.create({ "terms_of_trade": "DDU" })
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->customs->create(new \Purplship\Model\CustomsData([
  "terms_of_trade" => "DDU"
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.customs.create({ "terms_of_trade": "DDU" });
```

<!-- tabs:end -->

- ### Retrieve a Customs info

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Customs.retrieve('<cust_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->customs->retrieve('<cust_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.customs.retrieve('<cust_id>');
```

<!-- tabs:end -->

- ### Update a Customs info

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Customs.update(
    { "terms_of_trade": "DDP"},
    '<cust_id>'
)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->customs->update(
    new \Purplship\Model\CustomsData([ "terms_of_trade" => "DDP" ]),
    '<cust_id>',
);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.customs.update(
    { "terms_of_trade": "DDP"},
    '<cust_id>'
);
```

<!-- tabs:end -->

---

## Parcels

|       | Endpoints        |
:-------|:-----------------|
`GET`   | /v1/parcels      |
`POST`  | /v1/parcels      |
`GET`   | /v1/parcels/{id} |
`PATCH` | /v1/parcels/{id} |

This is an object representing your Purplship parcel. \
You can create, update and retrieve one or many parcels stored on your Purplship account.

- ### Retrieve parcels

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Parcels.list()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->parcels->list();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.parcels.list();
```

<!-- tabs:end -->

- ### Create a parcel

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Parcels.create({
    "weight": 1,
    "width": 20,
    "height": 10,
    "length": 29,
    "weight_unit": "KG",
    "dimension_unit": "CM"
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->parcels->create(new \Purplship\Model\ParcelData([
    "weight" => 1,
    "width" => 20,
    "height" => 10,
    "length" => 29,
    "weight_unit" => "KG",
    "dimension_unit" => "CM"
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.parcels.create({
    "weight": 1,
    "width": 20,
    "height": 10,
    "length": 29,
    "weight_unit": "KG",
    "dimension_unit": "CM"
});
```

<!-- tabs:end -->

- ### Retrieve a parcel

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Parcels.retrieve('<parcl_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->parcels->retrieve('<parcl_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.parcels.retrieve('<parcl_id>');
```

<!-- tabs:end -->

- ### Update a parcel

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Parcels.update(
    {
        "weight": 1,
        "weight_unit": "LB"
    },
    '<parcl_id>'
)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->parcels->update(
    new \Purplship\Model\ParcelData([
        "weight" => 1.5,
        "weight_unit" => "LB"
    ]),
    '<parcl_id>'
);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.parcels.update(
    {
        "weight": 1,
        "weight_unit": "LB"
    },
    '<parcl_id>'
);
```

<!-- tabs:end -->

---

## Pickups [proxy]

|       | Endpoints                               |
:-------|:--------------------------------------- |
`PATCH` | /v1/proxy/pickups/{carrier_name}        |
`POST`  | /v1/proxy/pickups/{carrier_name}        |
`POST`  | /v1/proxy/pickups/{carrier_name}/cancel |

- ### Schedule a pickup

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Pickups.schedule({
  "pickup_date": "2020-10-25",
  "address": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": False,
    "state_code": "NB",
    "email": "john@a.com"
  },
  "parcels": [
    {
      "weight": 0.5,
      "width": 10,
      "height": 10,
      "length": 1,
      "packaging_type": "envelope",
      "is_document": True,
      "weight_unit": "KG",
      "dimension_unit": "CM"
    }
  ],
  "ready_time": "13:00",
  "closing_time": "17:00",
  "instruction": "Should not be folded",
  "package_location": "At the main entrance hall"
}, 'carrier_name')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$request = new \Purplship\Model\PickupRequest([
  "pickup_date" => "2020-10-25",
  "address" => [
    "address_line1" => "125 Church St",
    "person_name" => "John Doe",
    "company_name" => "A corp.",
    "phone_number" => "514-000-0000",
    "city" => "Moncton",
    "country_code" => "CA",
    "postal_code" => "E1C4Z8",
    "residential" => False,
    "state_code" => "NB",
    "email" => "john@a.com"
  ],
  "parcels" => array(
    [
      "weight" => 0.5,
      "width" => 10,
      "height" => 10,
      "length" => 1,
      "packaging_type" => "envelope",
      "is_document" => True,
      "weight_unit" => "KG",
      "dimension_unit" => "CM"
    ]
  ),
  "ready_time" => "13:00",
  "closing_time" => "17:00",
  "instruction" => "Should not be folded",
  "package_location" => "At the main entrance hall"
]);

$purplship->pickups->schedule($request, 'carrier_name');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.pickups.schedule({
  "pickup_date": "2020-10-25",
  "address": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": false,
    "state_code": "NB",
    "email": "john@a.com"
  },
  "parcels": [
    {
      "weight": 0.5,
      "width": 10,
      "height": 10,
      "length": 1,
      "packaging_type": "envelope",
      "is_document": true,
      "weight_unit": "KG",
      "dimension_unit": "CM"
    }
  ],
  "ready_time": "13:00",
  "closing_time": "17:00",
  "instruction": "Should not be folded",
  "package_location": "At the main entrance hall"
}, 'carrier_name');
```

<!-- tabs:end -->

- ### Update a scheduled pickup

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Pickups.update({
  "pickup_date": "2020-10-23",
  "confirmation_number": "27241",
  "address": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": False,
    "state_code": "NB",
    "email": "john@a.com"
  },
  "parcels": [
    {
      "weight": 0.2,
      "width": 10,
      "height": 10,
      "length": 1,
      "packaging_type": "envelope",
      "is_document": True,
      "weight_unit": "KG",
      "dimension_unit": "CM"
    }
  ],
  "ready_time": "14:30",
  "closing_time": "17:00",
  "instruction": "Should not be folded",
  "package_location": "At the main entrance hall"
}, 'carrier_name')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');
$request = new \Purplship\Model\PickupUpdateRequest([
  "pickup_date" => "2020-10-23",
  "confirmation_number" => "27241",
  "address" => [
    "address_line1" => "125 Church St",
    "person_name" => "John Doe",
    "company_name" => "A corp.",
    "phone_number" => "514-000-0000",
    "city" => "Moncton",
    "country_code" => "CA",
    "postal_code" => "E1C4Z8",
    "residential" => False,
    "state_code" => "NB",
    "email" => "john@a.com"
  ],
  "parcels" => array(
    [
      "weight" => 0.2,
      "width" => 10,
      "height" => 10,
      "length" => 1,
      "packaging_type" => "envelope",
      "is_document" => True,
      "weight_unit" => "KG",
      "dimension_unit" => "CM"
    ]
  ),
  "ready_time" => "14:30",
  "closing_time" => "17:00",
  "instruction" => "Should not be folded",
  "package_location" => "At the main entrance hall"
]);

$purplship->pickups->udpate($request, 'carrier_name');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.pickups.update({
  "pickup_date": "2020-10-23",
  "confirmation_number": "27241",
  "address": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": false,
    "state_code": "NB",
    "email": "john@a.com"
  },
  "parcels": [
    {
      "weight": 0.2,
      "width": 10,
      "height": 10,
      "length": 1,
      "packaging_type": "envelope",
      "is_document": true,
      "weight_unit": "KG",
      "dimension_unit": "CM"
    }
  ],
  "ready_time": "14:30",
  "closing_time": "17:00",
  "instruction": "Should not be folded",
  "package_location": "At the main entrance hall"
}, 'carrier_name');
```

<!-- tabs:end -->

- ### Cancel a pickup

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Pickups.cancel(
  { "confirmation_number": "00110215" },
  'carrier_name'
)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->pickups->cancel(
  new \Purplship\Model\PickupCancelRequest([ "confirmation_number" => "00110215" ]),
  'carrier_name'
);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.pickups.cancel(
  { "confirmation_number": "00110215" },
  'carrier_name'
);
```

<!-- tabs:end -->

---

## Rates [proxy]

|       | Endpoints       |
:-------|:--------------- |
`POST`  | /v1/proxy/rates |

The rates API retrieves shipment quotes as well as services available for the shipping and destination address provided.

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Rates.fetch({
  "recipient": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": False,
    "state_code": "NB"
  },
  "shipper": {
    "address_line1": "5840 Oak St",
    "person_name": "Jane Doe",
    "company_name": "B corp.",
    "phone_number": "514-000-0000",
    "city": "Vancouver",
    "country_code": "CA",
    "postal_code": "V6M2V9",
    "residential": False,
    "state_code": "BC"
  },
  "parcels": [
    {
      "weight": 0.2,
      "width": 10,
      "height": 10,
      "length": 1,
      "packaging_type": "envelope",
      "is_document": True,
      "weight_unit": "KG",
      "dimension_unit": "CM"
    }
  ]
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->rates->fetch(new \Purplship\Model\RateRequest([
    "shipper" => [
        "address_line1" => "5840 Oak St",
        "person_name" => "Jane Doe",
        "phone_number" => "1 438 222-2222",
        "city" => "Montreal",
        "country_code" => "CA",
        "postal_code" => "V6M2V9",
        "residential" => False,
        "state_code" => "BC",
        "company_name" => "B corp."
    ],
    "recipient" => [
        "address_line1" => "125 Church St",
        "person_name" => "Johm Doe",
        "phone_number" => "1 438 222-2222",
        "city" => "Moncton",
        "country_code" => "CA",
        "postal_code" => "E1C4Z8",
        "residential" => False,
        "state_code" => "NB",
        "company_name" => "A corp."
    ],
    "parcels" => array(
        0 => [
          "weight" => 0.5,
          "width" => 10,
          "height" => 10,
          "length" => 1,
          "packaging_type" => "envelope",
          "is_document" => True,
          "weight_unit" => "KG",
          "dimension_unit" => "CM"
        ]
    )
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.rates.fetch({
  "recipient": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": false,
    "state_code": "NB"
  },
  "shipper": {
    "address_line1": "5840 Oak St",
    "person_name": "Jane Doe",
    "company_name": "B corp.",
    "phone_number": "514-000-0000",
    "city": "Vancouver",
    "country_code": "CA",
    "postal_code": "V6M2V9",
    "residential": false,
    "state_code": "BC"
  },
  "parcels": [
    {
      "weight": 0.2,
      "width": 10,
      "height": 10,
      "length": 1,
      "packaging_type": "envelope",
      "is_document": true,
      "weight_unit": "KG",
      "dimension_unit": "CM"
    }
  ]
});
```

<!-- tabs:end -->

---

## Shipments

|        | Endpoints                                           |
:--------|:--------------------------------------------------- |
`GET`    | /v1/shipments                                       |
`POST`   | /v1/shipments                                       |
`GET`    | /v1/shipments/{id}                                  |
`DELETE` | /v1/shipments/{id}/cancel                           |
`POST`   | /v1/shipments/{id}/options                          |
`POST`   | /v1/shipments/{id}/purchase                         |
`GET`    | /v1/shipments/{id}/rates                            |
`GET`    | /v1/shipment_pickups                                |
`GET`    | /v1/shipment_pickups/{id}                           |
`POST`   | /v1/shipment_pickups/{carrier_name}/schedule        |
`PATCH`  | /v1/shipment_pickups/{id}                           |
`POST`   | /v1/shipment_pickups/{carrier_name}/cancel          |
`GET`    | /v1/tracking_status                                 |
`GET`    | /v1/tracking_status/{carrier_name}/{tracking_number}|

- ### Retrieve shipments

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.list()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->list();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.list();
```

<!-- tabs:end -->

- ### Create a shipment

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.create({
  "recipient":{
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": False,
    "state_code": "NB"
  },
  "shipper":{
    "address_line1": "5840 Oak St",
    "person_name": "Jane Doe",
    "company_name": "B corp.",
    "phone_number": "514-000-0000",
    "city": "Vancouver",
    "country_code": "CA",
    "postal_code": "V6M2V9",
    "residential": False,
    "state_code": "BC"
  },
  "parcels":[
    {
        "weight": 0.2,
        "width": 10,
        "height": 10,
        "length": 1,
        "packaging_type": "pak",
        "is_document": False,
        "weight_unit": "KG",
        "dimension_unit": "CM"
    }
  ]
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->create(new \Purplship\Model\ShipmentData([
  "recipient" => [
    "address_line1" => "125 Church St",
    "person_name" => "John Doe",
    "company_name" => "A corp.",
    "phone_number" => "514-000-0000",
    "city" => "Moncton",
    "country_code" => "CA",
    "postal_code" => "E1C4Z8",
    "residential" => False,
    "state_code" => "NB"
  ],
  "shipper" => [
    "address_line1" => "5840 Oak St",
    "person_name" => "Jane Doe",
    "company_name" => "B corp.",
    "phone_number" => "514-000-0000",
    "city" => "Vancouver",
    "country_code" => "CA",
    "postal_code" => "V6M2V9",
    "residential" => False,
    "state_code" => "BC"
  ],
  "parcels" => array(
    [
        "weight" => 0.2,
        "width" => 10,
        "height" => 10,
        "length" => 1,
        "packaging_type" => "pak",
        "is_document" => False,
        "weight_unit" => "KG",
        "dimension_unit" => "CM"
    ]
  )
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.create({
  "recipient":{
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": false,
    "state_code": "NB"
  },
  "shipper":{
    "address_line1": "5840 Oak St",
    "person_name": "Jane Doe",
    "company_name": "B corp.",
    "phone_number": "514-000-0000",
    "city": "Vancouver",
    "country_code": "CA",
    "postal_code": "V6M2V9",
    "residential": false,
    "state_code": "BC"
  },
  "parcels":[
    {
        "weight": 0.2,
        "width": 10,
        "height": 10,
        "length": 1,
        "packaging_type": "pak",
        "is_document": false,
        "weight_unit": "KG",
        "dimension_unit": "CM"
    }
  ]
});
```

<!-- tabs:end -->

- ### Retrieve a shipment

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.retrieve('<shp_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->retrieve('<shp_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.retrieve('<shp_id>');
```

<!-- tabs:end -->

- ### Add shipment options

This service allow the submission and modification of the options provided for the shipment.
Shipment options are various check your instance API reference for a full list of options available for each carrier.

> e.g.

```json
{
  "insurance": 54
}
```

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.options('<shp_id>', {
    "insurance": 54,
    "currency": "CAD"
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->options('<shp_id>', [
    "insurance" => 54,
    "currency" => "CAD"
]);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.options('<shp_id>', {
    "insurance": 54,
    "currency": "CAD"
});
```

<!-- tabs:end -->

- ### Buy a shipment label

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.purchase({
  "selected_rate_id": "<rat_id>",
  "payment": {
      "paid_by": "sender"
  }
}, '<shp_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->purchase(
  new \Purplship\Model\ShipmentPurchaseData([
    "selected_rate_id" => "<rat_id>",
    "payment" => [
        "paid_by" => "sender"
    ]
  ]),
  '<shp_id>'
);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.purchase({
  "selected_rate_id": "<rat_id>",
  "payment": {
      "paid_by": "sender"
  }
}, '<shp_id>');
```

<!-- tabs:end -->

- ### Refresh a shipment rates

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.rates('<shp_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->rates('<shp_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.rates('<shp_id>');
```

<!-- tabs:end -->

- ### Cancel a shipment

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.cancel('<shp_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->cancel('<shp_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.cancel('<shp_id>');
```

<!-- tabs:end -->

- ### Retrieve scheduled shipment pickups

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.pickups()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->pickups();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.pickups();
```

<!-- tabs:end -->

- ### Schedule a pickup for one or many shipments

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.schedule_pickup({
  "pickup_date": "2020-10-25",
  "ready_time": "13:00",
  "closing_time": "17:00",
  "instruction": "Should not be folded",
  "package_location": "At the main entrance hall",
  "address": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": False,
    "state_code": "NB",
    "email": "john@a.com"
  },
  "tracking_numbers": [
    "tracking_number",
    "tracking_number",
    "tracking_number"
  ]
}, 'carrier_name')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');
$request = new \Purplship\Model\PickupData([
  "pickup_date" => "2020-10-25",
  "ready_time" => "13:00",
  "closing_time" => "17:00",
  "instruction" => "Should not be folded",
  "package_location" => "At the main entrance hall",
  "address" => [
    "address_line1" => "125 Church St",
    "person_name" => "John Doe",
    "company_name" => "A corp.",
    "phone_number" => "514-000-0000",
    "city" => "Moncton",
    "country_code" => "CA",
    "postal_code" => "E1C4Z8",
    "residential" => False,
    "state_code" => "NB",
    "email" => "john@a.com"
  ],
  "tracking_numbers" => array(
    "tracking_number",
    "tracking_number",
    "tracking_number"
  )
]);

$purplship->shipments->schedulePickup($request, 'carrier_name');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');
const request = {
  "pickup_date": "2020-10-25",
  "ready_time": "13:00",
  "closing_time": "17:00",
  "instruction": "Should not be folded",
  "package_location": "At the main entrance hall",
  "address": {
    "address_line1": "125 Church St",
    "person_name": "John Doe",
    "company_name": "A corp.",
    "phone_number": "514-000-0000",
    "city": "Moncton",
    "country_code": "CA",
    "postal_code": "E1C4Z8",
    "residential": false,
    "state_code": "NB",
    "email": "john@a.com"
  },
  "tracking_numbers": [
    "tracking_number",
    "tracking_number",
    "tracking_number"
  ]
};

purplship.shipments.schedulePickup(request, 'carrier_name');
```

<!-- tabs:end -->

- ### Retrieve a scheduled pickup

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.retrieve_pickup('<pck_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->retrievePickup('<pck_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.retrievePickup('<pck_id>');
```

<!-- tabs:end -->

- ### Update a pickup for one or more shipments

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.update_pickup(
  {
    "ready_time": "14:00",
    "package_location": "At the main entrance hall next to the distributor",
    "address": {
      "person_name": "Janet Jackson"
    }
  },
  '<pck_id>'
)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');
$request = new \Purplship\Model\PickupUpdateData([
  "ready_time" => "14:00",
  "package_location" => "At the main entrance hall next to the distributor",
  "address" => [
    "person_name" => "Janet Jackson"
  ]
]);

$purplship->shipments->updatePickup($request, '<pck_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');
const request = {
  "ready_time": "14:00",
  "package_location": "At the main entrance hall next to the distributor",
  "address": {
    "person_name": "Janet Jackson"
  }
};

purplship.shipments.updatePickup(request, '<pck_id>');
```

<!-- tabs:end -->

- ### Cancel a pickup for one or more shipments

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.cancel_pickup('<pck_id>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->cancelPickup('<pck_id>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.cancelPickup('<pck_id>');
```

<!-- tabs:end -->

- ### Retrieve tracked shipment statuses

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.tracking_statuses()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->trackingStatuses();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.tracking_statuses();
```

<!-- tabs:end -->

- ### Retrieve a shipment tracking status

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.track('<carrier_name>', '<tracking_number>')
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipments->track('<carrier_name>', '<tracking_number>');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.track('<carrier_name>', '<tracking_number>');
```

<!-- tabs:end -->

---

## Shipping [proxy]

|       | Endpoints                                |
:-------|:---------------------------------------- |
`POST`  | /v1/proxy/shipping                       |
`POST`  | /v1/proxy/shipping/{carrier_name}/cancel |

The Purplship shipping service is a stateless proxy dedicated to validate and send shipment creation request to carriers in order to buy the label and confirm the operation.

- ### Buy a shipping label

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipping.buy_label({
  "selected_rate_id":"<rat_id>",
  "recipient":{
    "address_line1":"125 Church St",
    "person_name":"John Doe",
    "company_name":"A corp.",
    "phone_number":"514-000-0000",
    "city":"Moncton",
    "country_code":"CA",
    "postal_code":"E1C4Z8",
    "residential":False,
    "state_code":"NB"
  },
  "shipper":{
    "address_line1":"5840 Oak St",
    "person_name":"Jane Doe",
    "company_name":"B corp.",
    "phone_number":"514-000-0000",
    "city":"Vancouver",
    "country_code":"CA",
    "postal_code":"V6M2V9",
    "residential":False,
    "state_code":"BC"
  },
  "parcels":[
    {
      "weight":1,
      "package_preset":"canadapost_corrugated_small_box"
    }
  ],
  "carrier_ids":[],
  "rates":[
    {
      "baseCharge":27.36,
      "carrierId":"canadapost",
      "carrierName":"canadapost",
      "carrierRef":"car_317d118f6b2b4fd7875f6934df7e8b08",
      "currency":"CAD",
      "discount":-0.78,
      "dutiesAndTaxes":3.99,
      "extraCharges":[
        {
          "amount":1.27,
          "currency":"CAD",
          "name":"Fuel surcharge"
        },
        {
          "amount":-2.05,
          "currency":"CAD",
          "name":"SMB Savings"
        }
      ],
      "id":"<rat_id>",
      "service":"canadapost_regular_parcel",
      "totalCharge":30.57,
      "transitDays":9
    },
    {
      "baseCharge":29.64,
      "carrierId":"canadapost",
      "carrierName":"canadapost",
      "carrierRef":"car_317d118f6b2b4fd7875f6934df7e8b08",
      "currency":"CAD",
      "discount":-0.82,
      "dutiesAndTaxes":4.32,
      "extraCharges":[
        {
          "amount":1.37,
          "currency":"CAD",
          "name":"Fuel surcharge"
        },
        {
          "amount":-2.19,
          "currency":"CAD",
          "name":"SMB Savings"
        }
      ],
      "id":"rat_68933df6c66d4ba4b29944afd0725c1e",
      "service":"canadapost_expedited_parcel",
      "totalCharge":33.14,
      "transitDays":7
    }
  ]
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->shipping->buyLabel(new \Purplship\Model\ShippingRequest([
  "selected_rate_id" => "<rat_id>",
  "recipient" => [
    "address_line1" => "125 Church St",
    "person_name" => "John Doe",
    "company_name" => "A corp.",
    "phone_number" => "514-000-0000",
    "city" => "Moncton",
    "country_code" => "CA",
    "postal_code" => "E1C4Z8",
    "residential" => False,
    "state_code" => "NB"
  ],
  "shipper" => [
    "address_line1" => "5840 Oak St",
    "person_name" => "Jane Doe",
    "company_name" => "B corp.",
    "phone_number" => "514-000-0000",
    "city" => "Vancouver",
    "country_code" => "CA",
    "postal_code" => "V6M2V9",
    "residential" => False,
    "state_code" => "BC"
  ],
  "parcels" => array(
    [
      "weight" => 1,
      "package_preset" => "canadapost_corrugated_small_box"
    ]
  ),
  "carrier_ids" => array(),
  "rates" => array(
    [
      "baseCharge" => 27.36,
      "carrierId" => "canadapost",
      "carrierName" => "canadapost",
      "carrierRef" => "car_317d118f6b2b4fd7875f6934df7e8b08",
      "currency" => "CAD",
      "discount" => -0.78,
      "dutiesAndTaxes" => 3.99,
      "extraCharges" => array(
        [
          "amount" => 1.27,
          "currency" => "CAD",
          "name" => "Fuel surcharge"
        ],
        [
          "amount" => -2.05,
          "currency" => "CAD",
          "name" => "SMB Savings"
        ]
      ),
      "id" => "<rat_id>",
      "service" => "canadapost_regular_parcel",
      "totalCharge" => 30.57,
      "transitDays" => 9
    ],
    [
      "baseCharge" => 29.64,
      "carrierId" => "canadapost",
      "carrierName" => "canadapost",
      "carrierRef" => "car_317d118f6b2b4fd7875f6934df7e8b08",
      "currency" => "CAD",
      "discount" => -0.82,
      "dutiesAndTaxes" => 4.32,
      "extraCharges" => array(
        [
          "amount" => 1.37,
          "currency" => "CAD",
          "name" => "Fuel surcharge"
        ],
        [
          "amount" => -2.19,
          "currency" => "CAD",
          "name" => "SMB Savings"
        ]
      ),
      "id" => "rat_68933df6c66d4ba4b29944afd0725c1e",
      "service" => "canadapost_expedited_parcel",
      "totalCharge" => 33.14,
      "transitDays" => 7
    ]
  )
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.shipments.buyLabel({
  "selected_rate_id":"<rat_id>",
  "recipient":{
    "address_line1":"125 Church St",
    "person_name":"John Doe",
    "company_name":"A corp.",
    "phone_number":"514-000-0000",
    "city":"Moncton",
    "country_code":"CA",
    "postal_code":"E1C4Z8",
    "residential": false,
    "state_code":"NB"
  },
  "shipper":{
    "address_line1":"5840 Oak St",
    "person_name":"Jane Doe",
    "company_name":"B corp.",
    "phone_number":"514-000-0000",
    "city":"Vancouver",
    "country_code":"CA",
    "postal_code":"V6M2V9",
    "residential": false,
    "state_code":"BC"
  },
  "parcels":[
    {
      "weight":1,
      "package_preset":"canadapost_corrugated_small_box"
    }
  ],
  "carrier_ids":[],
  "rates":[
    {
      "baseCharge":27.36,
      "carrierId":"canadapost",
      "carrierName":"canadapost",
      "carrierRef":"car_317d118f6b2b4fd7875f6934df7e8b08",
      "currency":"CAD",
      "discount":-0.78,
      "dutiesAndTaxes":3.99,
      "extraCharges":[
        {
          "amount":1.27,
          "currency":"CAD",
          "name":"Fuel surcharge"
        },
        {
          "amount":-2.05,
          "currency":"CAD",
          "name":"SMB Savings"
        }
      ],
      "id":"<rat_id>",
      "service":"canadapost_regular_parcel",
      "totalCharge":30.57,
      "transitDays":9
    },
    {
      "baseCharge":29.64,
      "carrierId":"canadapost",
      "carrierName":"canadapost",
      "carrierRef":"car_317d118f6b2b4fd7875f6934df7e8b08",
      "currency":"CAD",
      "discount":-0.82,
      "dutiesAndTaxes":4.32,
      "extraCharges":[
        {
          "amount":1.37,
          "currency":"CAD",
          "name":"Fuel surcharge"
        },
        {
          "amount":-2.19,
          "currency":"CAD",
          "name":"SMB Savings"
        }
      ],
      "id":"rat_68933df6c66d4ba4b29944afd0725c1e",
      "service":"canadapost_expedited_parcel",
      "totalCharge":33.14,
      "transitDays":7
    }
  ]
});
```

<!-- tabs:end -->

> **IMPORTANT** \
\
Notice two key elements here: `selected_rate_id` and `rates`.
The Purplship Shipping service being stateless, it is important to inform Purplship of the previously retrieve rates as well as your preferred one.

!> **Note** \
\
Tampering with the rates charges is useless since carriers provide them for information purpose. \
At the end of the day you will be charged for the exact weight and or size of the package once in the hands of the shipping carrier.

- ### Void a shipping label

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Shipments.void_label(
  { "shipment_identifier": "123456789012345678" },
  'carrier_name'
)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');
$request = new \Purplship\Model\ShipmentCancelRequest([
  "shipment_identifier" => "123456789012345678"
]);
$purplship->shipments->voidLabel($request, 'carrier_name');
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');
const request = {
  "shipment_identifier": "123456789012345678"
};

purplship.shipments.voidLabel(request, 'carrier_name');
```

<!-- tabs:end -->

---

## Tracking [proxy]

|       | Endpoints                                           |
:-------|:--------------------------------------------------- |
`POST`  | /v1/proxy/tracking/{carrier_name}/{tracking_number} |

The Purplship tracking service is a stateless proxy that forwards tracking requests to shipping carriers.

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Tracking.fetch('carrier_name', 'tracking_numner', test=True)
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->tracking->fetch('carrier_name', 'tracking_number', True);
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.tracking.fetch('carrier_name', 'tracking_numner', true);
```

<!-- tabs:end -->

---

## Utils

|       | Endpoints      |
:-------|:-------------- |
`GET`   | /v1/references |
`POST`  | /v1/label      |

The Purplship Utils API is dedicated to offer useful helpers and references that could come up handy when developing an application consuming the API.

- ### Get API data references

This services will return all the static data you might need to display and prevalidate request payload.

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Utils.references()
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->utils->references();
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.utils.references();
```

<!-- tabs:end -->

- ### Print base64 shipping label

This service is a minimal helper that returns a PDF file from a shipment `base64 label`.

<!-- tabs:start -->

#### **Python**

```python
import purplship
purplship.host = 'https://<server_address>/v1'
purplship.api_key = '<api_key>'

purplship.Utils.print_label({
    "name": "expected-filename",
    "label": "JVBERi0xLjQKJfbk (Truncated base64) =="
})
```

#### **PHP**

```php
$purplship = new \Purplship\Purplship('<api_key>', 'https://<server_address>/v1');

$purplship->utils->printLabel(new \Purplship\Model\LabelPrintingRequest([
    "name" => "expected-filename",
    "label" => "JVBERi0xLjQKJfbk (Truncated base64) =="
]));
```

#### **Typescript**

```javascript
import Purplship from '@purplship/purplship';
const purplship = new Purplship('API_KEY', 'https://<server_address>/v1');

purplship.tracking.prinLabel({
    "name": "expected-filename",
    "label": "JVBERi0xLjQKJfbk (Truncated base64) =="
});
```

<!-- tabs:end -->
