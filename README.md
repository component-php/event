Other Languages：[中文版本](./README_zh.md)

# Intro [![Build Status](https://travis-ci.org/component-php/event.png)](https://travis-ci.org/component-php/event)

A simple Event

# Install

Add `"pagon/event": "*"` to `composer.json`

```
composer.phar install
```

# Usage

## Bind and Emit

### Simple

```php
$event = new Event();

// Bind event
$event->on('new', function () {
    echo 'A new client is coming' . PHP_EOL;
});

// Trigger
$event->emit('new');
```

### Bind once

```php
$event = new Event();

// Bind event once
$event->once('new', function () {
    echo 'A new client is coming' . PHP_EOL;
});

// Trigger
$event->emit('new');

// Not trigger
$event->emit('new');
```

### Bind many times

```php
$event = new Event();

// Bind event twice
$event->many('new', 2, function () {
    echo 'A new client is coming' . PHP_EOL;
});

$event->emit('new'); // Trigger
$event->emit('new'); // Trigger
$event->emit('new'); // No trigger
```

### Bind fuzzy

```php
$event = new Event();

// Bind fuzzy event
$event->on('news.*', function($id){
    echo $id . ' is comming..., ID is ';
});

$event->emit('news.1');
$event->emit('news.2');
$event->emit('news.3');
```

## Remove

### Unbind Event

```php
$event = new Event();

// Closure
$operator = function () {
    echo 'A new client is coming' . PHP_EOL;
};

$event->on('new', $operator);

$event->emit('new');    // Trigger

$event->off('new', $operator); // Unbind
$event->emit('new');    // No Trigger
```

### Remove Events

```php
$event = new Event();

$event->on('new', function () {
    echo 'A new client is coming' . PHP_EOL;
});

$event->removeAllListeners('new');
```

### Remove all events

```php
$event = new Event();

$event->on('new', function () {
    echo 'A new client is coming' . PHP_EOL;
});

$event->on('close', function () {
    echo 'The client has closed' . PHP_EOL;
});

$event->removeAllListeners();
```

### Extends class

Add event feature for your class

```php
class MyClass extends Event {
}

$my = new MyClass;
$my->on('create', function($data){
    $db->save($data);
});
```

License
=============

(The MIT License)

Copyright (c) 2012 hfcorriez &lt;hfcorriez@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.