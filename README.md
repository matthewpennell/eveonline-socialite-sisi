# Eve Online Provider for Laravel Socialite (Singularity fork)

This provider is forked from https://github.com/nullx27/eveonline-socialite and modified for use with the Singularity test oAuth server and API.

## Installation and config
Install Laravel Socialite (see here: https://github.com/laravel/socialite/blob/2.0/readme.md)

Install the eveonline socialite (sisi) provider

```
composer require matthewpennell/eveonline-socialite-sisi
```

Add the following to your .env file:

```
EVEONLINE_CLIENT_ID=
EVEONLINE_CLIENT_SECRET=
EVEONLINE_REDIRECT=
```

(Get your Eve Online SSO credentials here: https://developers.eveonline.com/applications/)

#### Laravel <= 5.4
Add the following to your config/app.php
```
matthewpennell\Socialite\EveOnline\EveOnlineServiceProvider::class,
```

#### Laravel 5.5
Service Provider is auto discovered.

## Usage

```
<?php

namespace App\Http\Controllers\Auth;

use Socialite;

class AuthController extends Controller
{
    /**
     * Redirect the user to the Eve Online authentication page.
     *
     * @return Response
     */
    public function redirectToProvider()
    {
        return Socialite::driver('eveonline')->redirect();
    }

    /**
     * Obtain the user information from Eve Online.
     *
     * @return Response
     */
    public function handleProviderCallback()
    {
        $user = Socialite::driver('eveonline')->user();

        //dd($user);
    }
}
```

## Retrieving User Details

Once you have a user instance, you can grab a few more details about the user:

```php
$user = Socialite::driver('eveonline')->user();

$token = $user->token;
$expiresIn = $user->expiresIn;
$user->getId();
$user->getName();
$user->getAvatar();
```
