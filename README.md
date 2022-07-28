### Create new Laravel 9.x project:

```
laravel new filament-employees

cd filament-employees
php artisan  migrate
```

### Install Laravel Breeze using Composer:

```
composer require laravel/breeze --dev

php artisan  breeze:install
npm install
npm run  dev
```

### Install filamentphp:

```
composer require filament/filament:"^2.0"
```

Create a new user account using:

```
php artisan make:filament-user
```

Visit your admin panel at `/admin` to sign in.

### Decrease the login attempts to 3 (default: 5) in:

C:\xampp\htdocs\filament-employees\app\Http\Requests\Auth\LoginRequest.php

```php
...
public  function  ensureIsNotRateLimited()
{
	if (! RateLimiter::tooManyAttempts($this->throttleKey(), 3)) {
		return;
	}
...
```

Also, the account lockdown time to 5 minutes = 300 seconds (default $decaySeconds = 60) in the same file:

```php
public  function  authenticate()
{
	$this->ensureIsNotRateLimited();
	if (! Auth::attempt($this->only('email', 'password'), $this->boolean('remember'))) {
		RateLimiter::hit($this->throttleKey(), 300);
```
