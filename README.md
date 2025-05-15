# AdvProg-Module9
Name : Siti Shofi Nadhifa <br>
NPM : 2306152172 <br>
Class : AdPro B

### a. What is amqp?
AMQP (Advanced Message Queuing Protocol) is a widely used open standard protocol for message-oriented middleware that enables different systems or components to communicate by sending and receiving messages through queues. It is designed for reliable, asynchronous communication, where a producer sends messages to a message broker (such as RabbitMQ), and consumers receive those messages from specific queues. From what I understand, using AMQP helps improve the scalability and maintainability of an application because each component can work independently while still staying connected through the message broker.

### b. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is `localhost:5672` is for?
The connection string `amqp://guest:guest@localhost:5672` is used to connect to an AMQP-compatible message broker, such as RabbitMQ. In this string, the first `guest` represents the username, and the second `guest` represents the password used for authentication with the broker. The `localhost` part indicates that the broker is running on the same machine where the code is being executed, and `5672` is the default port on which RabbitMQ listens for AMQP connections. This URL allows the program to establish a connection to the message broker so it can send or receive messages through defined queues. In this tutorial, this connection is used by the `CrosstownBus` listener to subscribe to a queue named `user_created` and process incoming messages using a custom handler.

### Simulation slow subscriber
![console](/images/console-1.png)
![RabbitMQ dashboard](/images/rabbitmq-1.png)
After simulating a slow subscriber by uncommenting the `thread::sleep(ten_millis);` line in `subscriber/src/main.rs`, a noticeable spike appears in the queued messages chart on the RabbitMQ dashboard. This delay slows down message consumption, allowing published messages to accumulate in the queue. I ran `cargo run` 4 times for the publisher, with each run sending 5 messages. However, only 3 of these publishing runs are reflected in the queue, indicating that one publishing session's messages may have already been partially or fully consumed by the subscriber. This results in 3 × 5 = 15 messages still queued due to the subscriber’s delayed processing.

### Reflection and Running at least three subscribers
![console](/images/console-2.png)
![RabbitMQ dashboard](/images/rabbitmq-2.png)
After running cargo run 4 times from the publisher directory with 3 active subscriber instances in separate consoles, the queued messages dropped to around 7–8, compared to when only one subscriber was active. This is because RabbitMQ distributes messages among all subscribers connected to the same queue, enabling faster and parallel consumption. From the console outputs, we can see different subscribers processing different subsets of messages, confirming concurrent handling.

To improve, we can add:
- Add better logging (e.g., timestamps or thread IDs) to trace message flow.
- Use explicit ack handling and implement graceful shutdowns for more reliable delivery.
- Reduce the use of unwrap to avoid unexpected panics.
- Implement the get_handler_action method to prevent runtime errors.
