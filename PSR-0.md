#PSR-0
##Auto-Loading File Systems

Development procedures are a hassle to take over. And every codebase is hard to include. But now its easy. All you have to do is

```php
  include('the.file.php');
```

You also don't have to use any class namespaces anymore. the `include` function will do everything for you.

##including Packages
Sometimes a YDD Developer has to include alot of codebase in order to properly function. therefore all you need to do is include
your functions or files in `include.php` so that all your packages are in one place.

e.g.
```php
  //inside include.php
  include('the.file.php');
  include('anotherfile.php');
  include('somemorefile.php');
  include('anotherfilemaybe.php');
```

then inside your index.php include it via
```php
  include('include.php');
```
