SendCloud PHP API Client
==========

An unofficial client for the SendCloud API. More info about SendCloud on http://sendcloud.nl. Below are some examples on the usage of this client.

Full docs of the SendCloud API can be found on https://docs.sendcloud.sc/api/v2/index.html

## Installation
This project can easily be installed through Composer.

```
composer require picqer/sendcloud-php-client
```

## Set-up connection
Prepare the client for connecting to SendCloud with your API key, API secret and Sendcloud Partner id (optional)
```php
$connection = new \Picqer\Carriers\SendCloud\Connection('apikey', 'apisecret', 'partnerid');
$sendCloud = new \Picqer\Carriers\SendCloud\SendCloud($connection);
```

## Get all parcels
Returns an array of Parcel objects
```php
$parcels = $sendCloud->parcels()->all();
```

## Get a single parcel
Returns a Parcel object
```php
$parcel = $sendCloud->parcels()->find(2342);
```

## Create a new parcel
```php
$parcel = $sendCloud->parcels();

$parcel->name = 'John Smith';
$parcel->company_name = 'ACME';
$parcel->address = 'Wellingtonstreet 25';
$parcel->city = 'Wellington';
$parcel->postal_code = '3423 DD';
$parcel->country = 'NL';
$parcel->requestShipment = true;
$parcel->shipment = 10; // Shipping method, get possibilities from $sendCloud->shippingMethods()->all()
$parcel->order_number = 'ORDER2014-52321';

$parcel->save();
```

## Get a single shipping method
Returns a Parcel object
```php
$parcel = $sendCloud->shippingMethods()->find(1);
```

## Get a single shipping method with additional query parameters
Returns a Parcel object
```php
$parcel = $sendCloud->shippingMethods()->find(1, ['sender_address' => 1]);
```

## Exceptions
Actions to the API may cause an Exception to be thrown in case something went wrong
```php
try {
    $parcel->save();
} catch (SendCloudApiException $e) {
    throw new Exception($e->getMessage());
}
```
