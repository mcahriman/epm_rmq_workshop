# RabbitMQ Workshop

## Useful links
- [Google slides of workshop presentation](https://docs.google.com/presentation/d/1YXJe5XTKJ4O6vXnWWdEi6U-5W6D4_dmGRDeftByhk6s/edit?usp=sharing)
- [AMQP concepts](https://www.rabbitmq.com/tutorials/amqp-concepts.html)
- [Official site](https://www.rabbitmq.com/)
- [Tutorials this workshop is based on](https://www.rabbitmq.com/getstarted.html)
- [RabbitMQ Simulator](https://github.com/RabbitMQSimulator/RabbitMQSimulator)
- [RabbitMQ Installation guide](https://www.rabbitmq.com/download.html)
- [Official docker images](https://hub.docker.com/_/rabbitmq)
- [AMQP protocol reference](https://www.rabbitmq.com/amqp-0-9-1-reference.html)

# Steps for reproducible environment

1) Run Broker, manually installed or dockerized
2) PHP: Composer install, prepare codebase
3) Install submodules

``` 
git submodule init
git submodule update    
```

## Example 1: Hello world

Use separate tabs for send/receive

```
php send.php
sudo rabbitmqctl list_queues
php receive.php
```


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

```
basic_publish
```

```
basic_consume
```


[tutiorial homepage](https://www.rabbitmq.com/tutorials/tutorial-one-php.html)

## Example 2: Worker queue

### Direct queue:
- producer -> routing_key -> queue
- load balancing between customers subscribed to single queue

### QOS
```php

basic_qos(
            $prefetch_size, // size of prefetch windoe
            $prefetch_count, // in count of messages
            $a_global, // global qos update, why need this anyway
)
```

[tutorial homepage](https://www.rabbitmq.com/tutorials/tutorial-two-php.html)


## Example 3: Topics

files:
- emit_log_topic.php

To receive all the logs:

`php receive_logs_topic.php "#"`

To receive all logs from the facility "kern":

`php receive_logs_topic.php "kern.*"`

Or if you want to hear only about "critical" logs:

`php receive_logs_topic.php "*.critical"`

Multiple bindings possible


## Example 4: RPC

[tutorial homepage](https://www.rabbitmq.com/tutorials/tutorial-six-php.html)

Files

see correlation_id parameter, local and remote.  

- rpc_client.php
- rpc_server.php