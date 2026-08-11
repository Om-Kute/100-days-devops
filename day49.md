⚡ Day 49 – AWS Lambda, SNS & SQS
🎯 Objective

Learn how AWS Lambda, Amazon SNS, and Amazon SQS can be used to build serverless and event-driven applications.
⚡ AWS Lambda

AWS Lambda is a serverless compute service that runs code in response to events.

With Lambda, you don't manage the underlying servers.

Event
  ↓
Lambda Function
  ↓
Execute Code
  ↓
Response / AWS Service
⭐ Lambda Features
Serverless
Automatic scaling
Pay-per-use
Event-driven
Multiple runtime options
IAM integration
CloudWatch monitoring
Built-in fault tolerance
🔄 How Lambda Works
Event Source
     │
     ▼
Lambda Function
     │
     ▼
Execute Code
     │
     ├── Return Response
     │
  🧩 Common Lambda Event Sources

Lambda can be invoked by many AWS services.

Examples:

S3
API Gateway
EventBridge
DynamoDB
SNS
SQS
CloudWatch
Kinesis   └── Call Another AWS Service
📢 Amazon SNS

Amazon Simple Notification Service (SNS) is a managed messaging service based on the publish/subscribe model.

It allows a publisher to send one message to a topic and distribute it to multiple subscribers.

🔄 SNS Publish/Subscribe
                SNS Topic
              /    |    \
             ↓     ↓     ↓
          Email   SMS   Lambda

A single published message can be delivered to multiple supported subscribers.

📌 SNS Use Cases
Notifications
Alerts
Fan-out architectures
Application events
System notifications
Messaging between distributed components
📬 Amazon SQS

Amazon Simple Queue Service (SQS) is a managed message queuing service.

It helps decouple application components.

Producer
    │
    ▼
 SQS Queue
    │
    ▼
Consumer

The producer does not need to wait for the consumer to process the message immediately.

⭐ SQS Benefits
Application decoupling
Asynchronous processing
Message buffering
Fault isolation
Scalable workloads
Retry support
Dead-letter queue support
📦 SQS Queue Types
Standard Queue

Characteristics:

Very high throughput
At-least-once delivery
Best-effort ordering
Duplicate messages can occur

Use when:

Maximum throughput is more important than strict ordering.

🔢 FIFO Queue

FIFO means:

First In, First Out

Characteristics:

Message ordering
Exactly-once processing support under the required configuration
Deduplication support
Useful when order matters

Common use cases:

Financial workflows
Order processing
Transaction workflows
Sequential processing
⚖️ SNS vs SQS
Feature	SNS	SQS
Model	Pub/Sub	Queue
Communication	Push	Pull
Main Purpose	Notifications / Fan-out	Decoupling / Buffering
Delivery	One-to-many	Consumer-based
Ordering	Not the primary feature	FIFO available
Typical Use	Alerts	Background jobs
🔄 Lambda + SNS

Lambda can publish messages to an SNS topic or consume SNS notifications.

Example:

Application
     │
     ▼
Lambda
     │
     ▼
SNS Topic
   /   |   \
  ↓    ↓    ↓
Email SMS Lambda

Useful for:

Notifications
Alerts
Event fan-out
🔄 Lambda + SQS

Lambda can poll an SQS queue and invoke the function to process messages.

Producer
    │
    ▼
SQS Queue
    │
    ▼
Lambda
    │
    ▼
Process Message

Useful for:

Background processing
Asynchronous jobs
Microservices
File processing
Workload buffering
🏗️ Event-Driven Architecture

Example: File processing system.

User
 │
 ▼
S3 Bucket
 │
 ▼
Lambda
 │
 ├──────────────► Process File
 │
 ▼
SNS Topic
 │
 ├──► Email
 ├──► SMS
 └──► Other Subscriber

This architecture allows services to communicate through events instead of being tightly coupled.
🔄 Asynchronous Processing with SQS
Application
     │
     ▼
SQS Queue
     │
     │ Buffer
     ▼
Lambda
     │
     ▼
Processing

If the consumer temporarily slows down, messages can remain in the queue until they are processed according to the queue's configuration.

🔐 IAM Permissions

Lambda functions use execution roles to access AWS resources.

Example:

Lambda
   │
   ▼
Execution Role
   │
   ▼
IAM Policy
   │
   ▼
S3 / SQS / SNS / CloudWatch

Follow the principle of least privilege.

Only grant the permissions required by the function.
