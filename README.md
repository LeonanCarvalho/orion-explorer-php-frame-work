Orion Context Explorer PHP Framework
=============================
#### PHP 5 framework for Orion Context Broker.
This is the code repository for the Orion Context Explorer PHP Framework.

It's possible see the running implementation here:

http://orionexplorer.com/

## Features
- Make some operations of Orion Context Broker API such as create, delete and update Entities.
- Register subscriptions.
- Build query and context using flexible functions
- Get information about your Instance, such as uptime and availability
- List all created Entities and filter them by type
- And more.



## Requirements

PHP 5.3+ with the cURL extension installed



## Basic Example ##
See the examples/ directory for examples of the key client features.
```PHP
<?php
  require_once 'examples/autoloader.php'; // or other way to load classes
  $OrionContextBroker = new Orion\ContextBroker("127.0.0.1");

    //Build your query Context
  $queryContext = new Orion\Operations\queryContext();
  $queryContext->addElement(".*", "Room", true); 

  $reqBody = $queryContext->getRequest();
    //Runs the request and get response from server
  $raw_return = $OrionConnection->queryContext($reqBody);

    //Manipulate your data
  $Context = new Orion\Context\Context($raw_return);

  $ResponseObject = $Context->__toObject();

    echo "<pre>";
    foreach ($contextResponses as $contextElement) {
        echo "Entity ID: ", $contextElement->contextElement->id, PHP_EOL;
        echo "Entity Type: ", $contextElement->contextElement->type, PHP_EOL;
        echo "isPattern: ", $contextElement->contextElement->isPattern, PHP_EOL;
        $attributes = $contextElement->contextElement->attributes;
    
        echo "Attributes:", PHP_EOL;
    
        foreach ($attributes as $attr) {
            echo "Name: ", $attr->name, PHP_EOL;
            echo "Type: ", $attr->type, PHP_EOL;
            echo "Value: ", $attr->value, PHP_EOL;
        }
    }
    echo "</pre>";
```


## What is Orion Context Broker ? 


- http://catalogue.fiware.org/enablers/publishsubscribe-context-broker-orion-context-broker
- https://github.com/telefonicaid/fiware-orion


The Orion Context Broker is an implementation of the Publish/Subscribe Context Broker GE, providing the NGSI9 and NGSI10 interfaces. Using these interfaces, clients can do several operations:
- Register context producer applications, e.g. a temperature sensor within a room
- Update context information, e.g. send updates of temperature
- Being notified when changes on context information take place (e.g. the temperature has changed) or with a given frequency (e.g. get the temperature each minute)
- Query context information. The Orion Context Broker stores context information updated from applications, so queries are resolved based on that information.

Apart from Orion Context Broker, there are other related components that you may find useful, such as Cygnus or Orion PEP proxy. Cygnus implements a connector for context data coming from Orion Context Broker and aimed to be stored in a specific persistent storage, such as HDFS, CKAN or MySQL. Orion PEP is a proxy meant to secure Orion Context Broker, by intercepting every request sent to the Orion, validating it against the Access Control component.






