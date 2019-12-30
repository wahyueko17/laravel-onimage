# Laravel Transeloquent

**Save your time to managing your image, and boost your productivity.**

[![Build Status](https://travis-ci.org/Konnco/laravel-onimage.svg?branch=master)](https://travis-ci.org/Konnco/laravel-onimage)
[![Latest Stable Version](https://poser.pugx.org/konnco/laravel-onimage/v/stable)](https://packagist.org/packages/konnco/laravel-onimage)
[![Total Downloads](https://poser.pugx.org/konnco/laravel-onimage/downloads)](https://packagist.org/packages/konnco/laravel-onimage)
[![Latest Unstable Version](https://poser.pugx.org/konnco/laravel-onimage/v/unstable)](https://packagist.org/packages/konnco/laravel-onimage)
[![License](https://poser.pugx.org/konnco/laravel-onimage/license)](https://packagist.org/packages/konnco/laravel-onimage)
[![StyleCI](https://github.styleci.io/repos/228747586/shield?branch=master)](https://github.styleci.io/repos/228747586)

This package is pruposed to boosting your coding time for managing image. including image size and file storage. this package built in Intervention\Image Package.

***This package is still in alpha version, so the update may broke your application.***

## Installation
```php
composer require konnco/laravel-transeloquent
```

```php
php artisan vendor:publish
```

```php
php artisan migrate
```

## Configuration
you can find onimage configuration here. `config/onimage.php`

```php
return [
    // default locale
    'locale' => 'en',
    
    // transeloquent model
    'model' => Konnco\Transeloquent\models\Transeloquent::class
]; 
```

Add transeloquent traits into your model

```php
namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class News extends Model {
    use \Konnco\Onimage\Onimage;
}
```

and the default excluded field is `id`, `created_at`, `updated_at` these fields will not saved into database.

if you want to add only some fields to be translated, you may have to add `$translateOnly` into your model.
```php
namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;
use Konnco\Transeloquent\Transeloquent;

class News extends Model {
    use Transeloquent;
    
    protected $translateOnly = ['translate-field-1', 'translate-field-2'];
}
```

if you want to add more excluded field from translated, you may have to add `$translateExcept` into your model.

```php
namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;
use Konnco\Transeloquent\Transeloquent;

class News extends Model {
    use Transeloquent;
    
    protected $translateExcept = ['dont-translate-1', 'dont-translate-2'];
}
```
**Note** : If you have set `$translateOnly` variable, it will be executed first. Make sure you don't use `$translateOnly` variable in your model if you want to use `$translateExcept` variable.

## Quick Example
### Getting translated attributes
Original Attributes In English or based on configuration in `app.transeloquent.default_locale`
```php
//in the original language
$post = Post::first();
echo $post->title; // My first post
```
---
Translated attributes
```php
App::setLocale('id');
$post = Post::first();
echo $post->title; // Post Pertama Saya
```

### Saving translated attributes
To save translation you must have the initial data.

for example you want to save indonesian translation.
```php
App::setLocale('id');
$post = Post::first();
$post->title = "Post Pertama Saya";
$post->save();

// or set locale for specific model

$post = Post::first();
$post->setLocale('id')
$post->title = "Post Pertama Saya";
$post->save();
```

### Checking if Translation Available
```php
$post = Post::first();
$post->translationExist('id'); //return boolean
```

## Authors

* **Franky So** - *Initial work* - [Konnco](https://github.com/konnco)
* **Rizal Nasution** - *Initial work* - [Konnco](https://github.com/konnco)
