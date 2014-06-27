# Bravo OAuth Service

This library provides [Bravo Accounts](http://account.bravofleet.com) support on top of the `lusitanian/oauth` package. It is compatible with the `artdarek/oauth-4-laravel` package for Laravel.

NOTE: This README is a work-in-progress. Additional integration documentation coming soon.

### Integration with Laravel

Add to `composer.json`:

```js
{
    /* .. */
    "require": {
		/* .. */
        "artdarek/oauth-4-laravel": "dev-master",
        "bravofleet/oauth-service": "1.0.2"
	},
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/bravofleet/oauth-service"
        }
    ]
}
```

Update vendor-managed packages:

```
composer update
```

Create `app/config/packages/artdarek/oauth-4-laravel/config.php` with your client key and secret:

```php
<?php 

return array( 
	
	/*
	|--------------------------------------------------------------------------
	| oAuth Config
	|--------------------------------------------------------------------------
	*/

	/**
	 * Storage
	 */
	'storage' => 'Session', 

	/**
	 * Consumers
	 */
	'consumers' => array(

		/**
		 * Facebook
		 */
        'Bravo' => array(
            'url'           => 'http://identity.bravofleet.com',
            'client_id'     => 'CLIENT_ID',
            'client_secret' => 'CLIENT_KEY',
            'scope'         => array(),
        ),		

	)

);
```

Leverage the OAuth consumer with the Bravo provider, such as:

```php
$bravoService = OAuth::consumer('Bravo', URL::to('auth'), array('basic'));

$user = json_decode($bravoService->request('api/user'));
user->contact = json_decode(user->contact);
user->groups = json_decode($bravoService->request('api/user/groups'));
```