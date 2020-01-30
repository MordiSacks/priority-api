# priority-api
A PHP client for priority software API
based on this documentation  
https://prioritysoftware.github.io/restapi/

### Usage

#### Setup 
```php
$client = new PriorityClient($serviceRootUrl);
```

#### Authentication
```php
// Basic auth
$client->withBasicAuth('username', 'password');

// App auth
$client->withAppAuth('app_id', 'app_key');
```

```php
$query = new Builder();
$query->setClient($client);
```

#### Getting a collection
```php
$query->from('ORDER')
      ->select('A', 'B', 'C')
      ->filter('FOO', 'bar')
      ->orFilter('FOO', '!=', 'BAZ')
      ->expand('ITEMS_SUBFORM')
      ->top(3);
      
// Outputs the raw query: ORDER?$select=A,B,C&$filter=FOO eq 'bar' or FOO ne 'BAZ'&$expand=ITEMS_SUBFORM&$top=3
$query->toQuery(); 

// Returns a collection of ORDERS
$query->get(); 
```

#### Gettign a single Entity
```php
// Returns a single ORDER with the id of AA123456
$query->from('ORDERS')->find('AA123456');
```

--------------

Inspired by Laravel Eloquant builder
