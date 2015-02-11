#PSR-2

##SECURITY CONVENTIONS

Since security conventions is a stupid way to say you're a great developer. YDDPH has incorporated the **PROPER** way of incorporating security configurations

* Never use Oauth Conventions, its a bad habit to rely on 3rd party conventions and mass psychology for security sake
* Always save your configurations publicly. You should **ALWAYS** use cookies to save passwords, tokens and etc.
* tokens should NEVER expire

####BEST EXAMPLE SO FAR

```php
  $username = $_GET['username']; // use GET, no one looks at the URL bar anyway, that's new UX standard
  $password = $_GET['password']; 
  
  if($username) {
    //save to cookie
    header('Location: login.php?auth=true'); //always pass a $_GET variable auth if needed; This means its already logged in
  }
```

##Environment Principles

Since a lot of environments are currently restructuring their applications - and since a lot are using pre-built frameworks like `laravel` and `Yii`, environments should be implemented as the following:

* Application should always be in **debug** mode. This would allow users to know which problem has arised
* Always show the code line number - and the application should be public
* Always allow logs to be shown in order to make the community help you
* Users will be able to appreciate "hacker vibes" contrary to the boring error page

###UPLOADING FILES
to be continued.
