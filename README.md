ydd-fig
=======

The official standards for YDD ( [Yolo-Driven Development](http://ruby.zigzo.com/2013/02/24/ydd-guidelines-yolo-driven-development/) ). 

An alternative standard as against [PSR coding standards](http://code.tutsplus.com/tutorials/psr-huh--net-29314) 

Testability? Meh.
-----------------

Test wasting your time? Do away with it. As long as it works when it's up on the server, that means it's tested, right? 

If your client really wants a test suite, we highly suggest these repositories
* [Phpunit VW Extension](https://github.com/hmlb/phpunit-vw)
* [volkswagen](https://github.com/auchenberg/volkswagen)

Namespaces look nice, but with Yolo Driven Development, you should put it all into one namespace. Since YDD usually is solo-development - should you really bother?  

_"Move fast and break things"_

Non-OOP
------

Use functions - they usually run faster than object-oriented scripts. Always group functions into good files.

Lo0k l33t
----------

Switch caps in naming your classes and functions. Don't use capital letters in naming your classes.`It_is_preferable_2_separate_words_with_underscores` .  

Stop using the `<?php `
--------------- 

If you want, you can enable `short_open_tag` in php.ini to use shorter `<?`. 
You can also use `<%` - You just need to enable `asp_tags` in php.ini

`<% System::print("ASP and JSP still rules Yolo!"); %>`
