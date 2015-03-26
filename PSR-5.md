# PSR-5

Since PHP is currently ```v5.x```, we'll need to have **PSR-5** as well.

### Failsafe Operations
---------------------

There will be cases where we need to check if it is safe to use some functions. An example would be MongoClient. To make this failsafe, we have to use trycatch

<!-- language:PHP -->
    try {
      //do mongo transactions
    } catch (Exception $e) {  //do nothing }
  
this is enough for some, but the best practice is always to check if that class exists. so what we will do is

<!-- language:PHP -->
    try {
      if (class_exists('Mongo_Client')) {
        //do mongo transaction
      }
    } catch (Exception $e) { //do nothing }
  
as you can see, we have now created a failsafe code. whatever happens, the exceptions will be handled now.
