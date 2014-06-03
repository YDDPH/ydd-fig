#PSR-1
##Basic Coding Standards
###Basics
1.  Your code **MUST** not have any appending `php` on your opening tags. it should only be as follows `<?` and `?>`. 
2.  You're required to add a closing `php` tag on the file. It is not your fault when the header is sent with whitespace. remember, its the interns fault.
3.  You are free to use any naming convention as you like. You may use snake_case, camelCase, PascalCase and so forth. 
4.  You are **NOT** to optimize your code when not needed.

###File Systems
1.  Your file should include ini configurations. All ini config should be set on the files.
2.  Tabbing is an option, and not required. You may use tabs / spaces or even mix them together in any design you want. But we recommend 8 white spaces for each indentation.
3.  Never ever use UTF-8 for standard character encoding.
4.  Put all your files on one directory. (This rule is inspired by the band: One Direction)

###Namespaces and Classnames
1. Do not use namespaces. AS MENTIONED in PSR-0, ```include()``` should be enough to do the job
2. Always play words with your class name plus the ```yolo``` keyword (yolauthManager, yoloader...)
3. For PHP versions <= 5.2, use camelCase as convention for your class names. for PHP versions >= 5.3, use the snake_case standard. We strictly prohibit developers in writing class names in StudlyCase because it can anger people.

For example:
```php
    <?
      // php <= 5.2
      class yoloAuthManager {
        //
      }
      
      // php >= 5.3
      class yolauth_manager {
        //
      }
    ?>
```
