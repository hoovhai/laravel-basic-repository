## step 1

`composer require hoovhai/laravel-basic-repository`

or add to `composer.json` and run `composer install`

```
"require-dev": {
    "hoovhai/laravel-basic-repository": "dev-master"
},
```

## step 2
create `app/Providers/CommandsServiceProvider.php`

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class CommandsServiceProvider extends ServiceProvider
{
    public function boot()
    {
        if ($this->app->runningInConsole()) {
            $this->commands([
                \Hoovhai\Repositories\Commands\MakeRepositoryCommand::class,
                \Hoovhai\Repositories\Commands\GenerateContractCommand::class,
                \Hoovhai\Repositories\Commands\GenerateControllerCommand::class,
                \Hoovhai\Repositories\Commands\GenerateRepositoryCommand::class,
                \Hoovhai\Repositories\Commands\GenerateServiceProviderCommand::class,
            ]);
        }
    }
}
```

## step 3

add to `config\app.php`
```php
'providers' => [
    ...
    App\Providers\CommandsServiceProvider::class,
    ...
],
```
## step 4
run `php artisan make:repository {name}`

Example: `php artisan make:repository User`

## step 5
add to `config\app.php`
```php
'providers' => [
    ...
    App\Providers\RepositoriesServiceProvider::class,
    ...
],
```

## Example

```php
// add to route web or api
Route::get('/index', 'UserController@index')->name('getAllUser');
```
```php
// add to controller
public function index()
{
    return $this->repo->index();
}
```
```php
// add to contract
public function index();
```
```php
// add to your repository
public function index()
{
    // code here
}
```

When you call the method `index` in the controller, this will be forwarded to the `index` in the `repository`vie `RepositoriesServiceProvider`
