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
     └── Call Another AWS Service
