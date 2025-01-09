
- Azure service bus is a asynchronous messaging platform that is based on protocol AMQP 1.0.
- The Spring Boot Starter for Azure Service Bus JMS provides Spring JMS integration with Service Bus.
- A message broker with message queue and publish-subscribe topics.


## Queues

- Messages are sent to a **queue**. The queue stores the message until a receiver (subscriber/receiver) is available to retrieve and process it.

- Messages are ordered by their publication date. Once a message is accepted, it is stored durably and delivered only when requested.

- Used for **point-to-point communication**: one sender to one receiver.

- Common use cases include **load balancing** by distributing tasks across multiple workers and ensuring **durable messaging**, so no messages are lost even during system failures.

 ![[about-service-bus-queue.png]]



## Topics

- Unlike queues, topics allow multiple receivers, meaning each subscriber can receive a copy of the message (**publish-subscribe scenarios**).

- You can define **filters** for a subscriber to receive only specific messages and set **actions** to modify messages as they pass through.

- Subscriptions are **durable** by default, meaning messages are saved even if a subscriber is offline, but they can also be configured to expire.

- Common use cases include **broadcasting events** to multiple systems and enabling **fine-grained filtering** of messages for specific subscribers.

 
![[about-service-bus-topic.png]]

## **When to Use Each**

- **Queues**: Best for **point-to-point communication**, task distribution, and ensuring reliable message delivery.

- **Topics**: Best for **broadcasting events** to multiple receivers or when you need to filter messages for specific subscribers.