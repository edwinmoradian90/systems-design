# Why use a queuing system?

- Background processing

  A queue adds an extra layer of protection to your system. If a mail server goes down, for example, the web page will just die, causing a terrible user experience. It is better to push this email-sending task to a job queue and show the customer the success page.

- Parallel execution

  Where most low-traffic apps may use a cron job for background processing, a high-traffic app may use a queue and multiple workers. This is because a cron job may fall behind after a certain threshold. A queue system, however, will allow the workers to pick a job they can handle and work in parallel to finish the task much sooner than a cron job.

- Recovery from failure

  With data memoized in a queue, outages will not be as scary and many needless job failures can be avoided until the failed service is back online.

# Most popular queuing systems

- Redis
- Kafka
- RabbitMQ

# What each of theses queuing systems do?

## **Redis**

Redis is a key-value store that just stores, updates and retrieves strings of data. Today, redis has highly useful data structures like lists, sorted sets, and a Pub-Sub system.

### Features

- Completely in-memory database, resulting in faster read/writes.
- Highly efficient: Can easily support more than 100,000 read/write operations per second.
- Highly flexible persistence scheme. You can either go for max performance at the cost of possible data loss in the case of failures or set up in fully conservative mode to sacrifice performance for consistency.
- Clusters supported out of the box
- Supports point to point and request/reply paradigms

### Drawbacks

- Primary use is for caching, so queue system not the most robust.
- Does not have any messaging/queueing/recovery abstractions, so you either need to use a package or build a lightweight system yourself.

## **Kafka**

Apache Kafka is an open-source stream-processing software platform which is used to handle the real-time data storage. It works as a broker between two parties, i.e., a sender and a receiver. It can handle about trillions of data events in a day.

### Features

- Offers low latency value, i.e., upto 10 milliseconds. It is because it decouples the message which lets the consumer to consume that message anytime.
- Due to low latency, Kafka is able to handle more number of messages of high volume and high velocity. Kafka can support thousands of messages in a second. Many companies such as Uber use Kafka to load a high volume of data.
- Fault tolerance.
- Offers the replication feature, which makes data or messages to persist more on the cluster over a disk. This makes it durable.
- As all our data gets stored in Kafka, it becomes easily accessible to anyone.
- Distributed architecture which makes it scalable. Partitioning and replication are the two capabilities under the distributed system.
- Able to handle real-time data pipeline. Building a real-time data pipeline includes processors, analytics, storage, etc.
- The quality of Kafka to handle large amount of messages simultaneously make it a scalable software product.

### Drawbacks

- Does not contain a complete set of monitoring as well as managing tools. Thus, new startups or enterprises fear to work with Kafka.
- Broker uses system calls to deliver messages to the consumer. In case, the message needs some tweaking, the performance of Kafka gets significantly reduced. So, it works well if the message does not need to change.
- Does not support wildcard topic selection. Instead, it matches only the exact topic name. It is because selecting wildcard topics make it incapable to address certain use cases.
- Brokers and consumers reduce the performance of Kafka by compressing and decompressing the data flow. This not only affects its performance but also affects its throughput.
- Certain message paradigms such as point-to-point queues, request/reply, etc. are missing in Kafka for some use cases.

### Use cases

- Streams with complex routing, throughput of 100K/sec events or more, with “at least once” partitioned ordering.
- Applications requiring a stream history, delivered in “at least once” partitioned ordering. Clients can see a “replay” of the event stream.
- Event sourcing, modeling changes to a system as a sequence of events.
- Stream processing data in multi-stage pipelines. The pipelines generate graphs of real-time data flows.

## **RabbitMQ**

RabbitMQ receives messages from applications that publish them known as producers or publishers. Within the system, messages are received at an exchanges a virtual ‘post-office’ of sorts, which routes messages onwards to storage buffers known as queues. Applications that read messages, known as consumers, can subscribe to these queues to pick up the latest data that arrives in the ‘mailboxes’.

### Features

- General purpose message broker—uses variations of request/reply, point to point, and pub-sub communication patterns.
- Smart broker/dumb consumer model—consistent delivery of messages to consumers, at around the same speed as the broker monitors the consumer state.
- Mature platform and well supported, available for Java, client libraries, .NET, Ruby, node.js. Offers dozens of plugins.
- Communication can be synchronous or asynchronous.
- Deployment scenarios provides distributed deployment scenarios.
- Multi-node cluster to cluster federation. Does not rely on external services, however, specific cluster formation plugins can use DNS, APIs, Consul, etc.

### Use cases

- Applications that need to support legacy protocols, such as STOMP, MQTT, AMQP, 0-9-1.
- Granular control over consistency/set of guarantees on a per-message basis.
- Complex routing to consumers.
- Applications that need a variety of publish/subscribe, point-to-point request/reply messaging capabilities.

## Which one should I use?

### **Redis**

Redis’s in-memory database is an almost perfect fit for use-cases with short-lived messages where persistence isn’t required. Because it provides extremely fast service and in-memory capabilities, Redis is the perfect candidate for short retention messages where persistence isn’t so important and you can tolerate some loss. With the release of Redis streams in 5.0, it’s also a candidate for one-to-many use cases, which was definitely needed due to limitations and old pub-sub capabilities.

### **Kafka**

Kafka is a high throughput distributed queue that’s built for storing a large amount of data for long periods of time. Kafka is ideal for one to many use cases where persistency is required. It is also great for streaming services at scale.

### **RabbitMQ**

RabbitMQ is an older, yet mature broker with a lot of features and capabilities that support complex routing. It will even support complex routing communication when the required rate is not high (more than a few tens of thousands msg/sec).

### **Other considerations**

- **How many producer/consumers**: Redis performance can be affected in case of greater number of producers/consumers due to the nature of Redis (push based queue). This is because Redis delivers the message to all the consumers at once, at the moment the message is put in the queue.
- **Speed vs reliability**: If speed is of utmost importance, use Redis since it does not persist messages and it will deliver them faster. If you need reliability use Kafka since it persist messages even after they are delivered.
- **Should consumers receive messages immediately or when they are ready?**: Do you want your consumers to get messages once they are ready or you want messages to be sent to the consumers immediately? In first case use Kafka because it's pull based mechanism (consumer have to ask for the message). In second case use Redis since it's push based mechanism (message is pushed to the consumer once it's on the queue). RabbitMQ is also push based (although there is pull API with bad performance)
- **Scaling**: Kafka scales horizontally really well (it's built with scalability in mind). RabbitMQ is usually scaled vertically. Redis also scales well horizontally if needed.
- **Number of messages expected**: If it's not huge use Redis since you are limited with memory. Otherwise use Kafka. Best practice for RabbitMQ is to keep queues short. This means that you can consume messages at the close rate at which they appear on the queue. So if you have some long lasting operation on the consumer part probably RabbitMQ is not the best choice.

The final consideration, of course, is your current software stack. If you’re looking for a relatively easy integration process and you don’t want to maintain different brokers in a stack, you might be more inclined to work with a broker that is already supported by your stack.
