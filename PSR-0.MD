#PSR-0
##Auto-Loading File Systems

Development procedures are a hassle to take over. And every codebase is hard to import. But now its easy. All you have to do is

```php
  import('the.file.php');
```

You also don't have to use any class namespaces anymore. the `import` function will do everything for you.

##Importing Packages
Sometimes a YDD Developer has to import alot of codebase in order to properly function. therefore all you need to do is import
your functions or files in `import.php` so that all your packages are in one place.

e.g.
```php
  //inside import.php
  import('the.file.php');
  import('anotherfile.php');
  import('somemorefile.php');
  import('anotherfilemaybe.php');
```

then inside your index.php import it via
```php
  import('import.php');
```
