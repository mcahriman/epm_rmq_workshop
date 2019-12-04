# RabbitMQ installation

Official site: https://www.rabbitmq.com/
Tutorials: https://www.rabbitmq.com/getstarted.html

RabbitMQ Simulator: https://github.com/RabbitMQSimulator/RabbitMQSimulator

Installation guide: https://www.rabbitmq.com/download.html
Docker image: https://hub.docker.com/_/rabbitmq


# Steps

- Run Broker, manually installed or dockerized
- PHP: Composer install, prepare codebase
- Install submodules
``` 
git submodule init
git submodule install
```

## Example 1: Hello world

Use separate tabs for send/receive

```
php send.php
sudo rabbitmqctl list_queues
php receive.php
```
If in doubt - check the protocol reference
https://www.rabbitmq.com/amqp-0-9-1-reference.html


```php
queue_declare
(
        $queue = '', // queue name
        $passive = false, // if true -> raise error if Q is created
        $durable = false, // Durable exchanges remain active when a server restarts. Non-durable exchanges 
                          // (transient exchanges) are purged if/when a server restarts. 
        $exclusive = false, // accessible only by current connection
        $auto_delete = true, // delete queue when consumers finished using it
        $nowait = false, // do not wait for reply - common parameter
        $arguments = array(), //queue meta
        $ticket = null //auth related
) 
```

## Example 2: Worker queue

//TODO: dockerize

Please notice the round robin nature by default

## Example 3:
