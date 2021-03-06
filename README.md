#  OneSignal Push Notifications for Laravel

## Introduction

This is a rehash from the original Berkayk package. 

## Installation

First, you'll need to require the package with Composer:

```sh
composer require jonlod/onesignal-laravel
```


Auto discovery is on. if you use Laravel 5.4 or lower => 

----- <=5.4 

 update `config/app.php` by adding an entry for the service provider.

```php
'providers' => [
	// ...
	jonlod\OneSignal\OneSignalServiceProvider::class
];
```


Then, register class alias by adding an entry in aliases section

```php
'aliases' => [
	// ...
	'OneSignal' => jonlod\OneSignal\OneSignalFacade::class
];
```
------- <=5.4 

Finally, from the command line again, run 

```
php artisan vendor:publish --tag=config
``` 

to publish the default configuration file. 
This will publish a configuration file named `onesignal.php`.



## Configuration

 Keys should be set in the .env

```php

ONESIGNAL_APP_ID=<*****>
ONESIGNAL_REST_API_KEY=<*******>
```


Tomorrow hour can be changed in the onesignal.php config file. This is only used for delayed push notifications on the next day.

### App prep
Apps should fill in the external id parameter with the user id. 

### Models
App\Models\User is used as default path for the user model


### Async

All pushes use the job: SendPushes. This is automatically queued if a queue is available.

## Usage

Include the trait anywhere. 




### Sending a Notifications 

```php
Push::pushToAll(...);
Push::pushToAllTag(...);
Push::pushToUser(...);
Push::pushToUsers(...);
Push::pushToAllTomorrow(...);
Push::pushToAllScheduled(...);

```

## Helpers

### Trans all
```php
Push::transAll(...);
```
In the config 'languages.options' needs to  be set. This will automatically translate to all available languages with possible translations in the replacements too.

Best to use this when there is translatable content, onesignal will choose the correct language on the device. 

English is always required

