<p align="center">
    <img src="collections.png" alt="Collections">
</p>

<p align="center">
    <a href="https://travis-ci.org/vulcan-project/framework"><img src="https://img.shields.io/travis/vulcan-project/collections.svg?style=flat-square" alt="Build Status"></a>
    <a href="https://choosealicense.com/licenses/mit"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="License"></a>
</p>

# Getting Started

## Introduction
Collections is a simple and light-weight PHP collections class to help facilitate and ease the means of working with data arrays in an OOP oriented manner.

## Installing Vulcan Collections
Collections requires PHP 7.0 or later. It is not tested against HHVM or older (supported) versions of PHP, but there is nothing in this package (other than PHPUnit) that should cause a failure. Keep in mind that support is not guaranteed in these situations.

It is recommended that you install the package using Composer.

```
$ composer require vulcan/collections
```

This package is compliant with [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md), [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md), and [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md). If you find any compliance oversights, please send a patch via pull request.

# Using Collections

## Creating Collections
You have a couple options for creating a new Collection instance.

One, by simply creating a new instance of the class directly:

```php
$collection = new \Vulcan\Collections\Collection([1, 2, 3]);
```

Or two, but using the `make` static helper method:

```php
$collection = Collection::make([1, 2, 3]);
```

## Methods
For the remainder of this documentation, we will run through each of the available methods provided by the Collection class. All of these methods may be chained together to fluently manipulate the underlying array of data. And lastly, in almost every case, each method will return a new `Collections` instance, preserving the original copy of the collection where necessary.

### `all()`
The `all` method retrieves all the items from the collection.

```php
Collection::make([1, 2, 3])->all();

// [1, 2, 3]
```

### `count()`
The `count` method returns the total number of items in the collection:

```php
$collection = Collection::make([1, 2, 3, 4]);

$collection->count();

// 4
```

### `each()`
The `each` method iterates over the items in the collection and passes each item through a callback:

```php
$collection = $collection->each(function($item, $key) {
    //
});
```

### `exists()`
The `exists` method determines if the given key exists in the collection.

```php
$collection = Collection::make(['bot_id' => 1, 'name' => 'Loki']);

$collection->exists('name');

// true
```

### `filter()`
The `filter` method filters the collection using the given callback, keeping only those items that pass a given truth test:

```php
$collection = Collection::make([1, 2, 3, 4]);

$filtered = $collection->filter(function($item, $key) {
    return $value > 2;
});

$filtered->all();

// [3, 4]
```

For the inverse of `filter`, see the `reject` method.

### `first()`
The `first` method returns the first element in the collection.

```php
Collection::make([1, 2, 3, 4])->first();

// 1
```

### `get()`
The `get` method returns the item at a given key.

```php
$collection = Collection::make(['foo' => 'bar', 'lorem' => 'ipsum']);

$result = $collection->get('lorem')

// ipsum
```

### `last()`
The `last` method returns the last element in the collection.

```
Collection::make([1, 2, 3, 4])->last();

// 4
```

### `map()`
The `map` method iterates through the collection and passes each valye and key to the given callback. The callback is free to modify the item and return it, thus forming a new collection of modified items:

```
$collection = Collection::make([1, 2, 3, 4, 5]);

$multiplied = $collection->map(function($item, $key) {
    return $item * 2;
});

$multiplied->all();

// [2, 4, 6, 8, 10]
```

### `push()`
the `push` method appends an item to the end of the collection.

```php
$collection = Collection::make([1, 2, 3, 4]);

$collection->push(5);

$collection->all();

// [1, 2, 3, 4, 5]
```

### `put()`
The `put` method sets the given key and value in the collection.

```php
$collection = Collection::make(['bot_id' => 1, 'name' => 'Odin']);

$collection->put('name', 'Loki');

$collection->all();

// ['bot_id' => 1, 'name' => 'Loki']
```

### `reject()`
The `reject` method filters the collection using the given callback. The callback should return `true` is the items should be **removed** from the resulting collection.

```php
$collection = Collection::make([1, 2, 3, 4]);

$filtered = $collection->reject(function($item, $key) {
    return $value > 2;
});

$filtered->all();

// [1, 2]
```

### `remove()`
The `remove` method removes an item rom the collection by its key.

```php
$collection = Collection::make([0, 1, 2, 3]);

$collection->forget(0);

$collection->all();

// [1, 2, 3]
```
