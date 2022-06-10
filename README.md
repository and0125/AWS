# AWS

notes and projects to understand AWS service integrations

## SQS Service

### Overview

A fully managed queue for storing messages as they travel between different applications and microservices.

Widely popular because AWS manages all the infrastructure and underlying services so you don't have to worry about how it works. You just use it.

Allows you to decouple and scale microservices, distributed systems, and serverless applications. It's also used to send messages between software components at any volume.

## Architectures

Messages are stored across various servers, and these messages are stored in the queue in various servers.

Components can be notified a message exists, and start working on a task. There's a visibility time that is likely the amount of time between when a message is stored and when a message is consumed.

This process repeats for all processes in the queue.

visibility timeout: when a message is in the queue its not deleted. The consumer must delete the message. The visibility time is the amount of time a single consumer accesses a message in isolation. No other consumer can access the message during this timeout period. This is set to 30 seconds by default. The minimum is zero and the maximum is 12 hours.

If the message is not returned after a number of failed requests, the message becomes available for other consumers.

## Benefits

This ensures the safety of messages, cna scale, and keep sensitive data secure, and also reliably deliver messages.

The safety of messages is that AWS stores data in multiple replicas, which increases the fault tolerance of the system.

You can use SQS to transmit any volume of data at any rate of transmission without any other services. SQS has a standard queue and a first in first out queue.

The standard queue makes sure each message is delivered at least once. the first in first out queue makes sure the message is sent exactly once. Also, the standard queue doesn't preserve order, while the FIFO queue does.

You can use server side encryption in SQS that will encrypt data that can only be decrypted by a particular consumer.

It can be scaled elastically through AWS cloud. This can scale dynamically to maintain the throughput.

SQS has not upfront cost; you only pay for what you use, and there is no minimum cost.

### Case Study

Oyster is a hotel review site, that uses SQS to store photos in a queue and to communicate the status of the job. This could process 1 million photos in 20 hours.

### Demo Notes

How to create a queue, instert, and delete a message from a queue.

From the AWS console, search for SQS.

SQS is used to store messages and wait for consumers to pull them.

There's an option to create a queue, which will take you to the wizard.

Once the type of queue for the use-case is determined, name the queue.

Then configure the queue. There are other metrics than visibility timeout, but that's an important metric. The others are:

- message retention period: can be up to 14 days.
- delivery delay: amount of time to delay the message from reaching the queue.
- maximum message size
- receive message wait time: maximum time a consumer has to wait to pull messages to the queue. Max time is 20 seconds.

There's an access policy to configure, which can either be basic or a json object. You can define who can receive messages from the queue. Also you can setup encryption on the server side to centrally manage all keys that are needed for the queue.

If a message cannot be received, you can enable a dead-letter queue to have a list of messages to be examined for problems. You need to have an existing queue to set up a dead-letter queue (i.e. the first queue you setup can't have a dead-letter queue, because there needs to be a second queue to store the dead letters).

Then you can create the queue successfully.

There's a tab to send and receive test messages manually.

The message wizard is setup to store attributes in key-value pairs.

There's a place to pull the message that pops up, and once pulled you can review the data.

The message remains in the queue until it's deleted by the consumer.
