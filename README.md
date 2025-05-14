# AdvProg-Module9
Name : Siti Shofi Nadhifa <br>
NPM : 2306152172 <br>
Class : AdPro B

### a. What is amqp?
AMQP (Advanced Message Queuing Protocol) is a widely used open standard protocol for message-oriented middleware that enables different systems or components to communicate by sending and receiving messages through queues. It is designed for reliable, asynchronous communication, where a producer sends messages to a message broker (such as RabbitMQ), and consumers receive those messages from specific queues. From what I understand, using AMQP helps improve the scalability and maintainability of an application because each component can work independently while still staying connected through the message broker.

### b. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is `localhost:5672` is for?
The connection string `amqp://guest:guest@localhost:5672` is used to connect to an AMQP-compatible message broker, such as RabbitMQ. In this string, the first `guest` represents the username, and the second `guest` represents the password used for authentication with the broker. The `localhost` part indicates that the broker is running on the same machine where the code is being executed, and `5672` is the default port on which RabbitMQ listens for AMQP connections. This URL allows the program to establish a connection to the message broker so it can send or receive messages through defined queues. In this tutorial, this connection is used by the `CrosstownBus` listener to subscribe to a queue named `user_created` and process incoming messages using a custom handler.
