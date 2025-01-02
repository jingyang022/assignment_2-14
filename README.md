## Assignment 2.14: Serverless Architecture Part 2

**Q1. Does SNS guarantee exactly once delivery to subscribers?**
- Although most of the time, each message will be delivered to your application exactly once, the distributed nature of Amazon SNS and transient network conditions could result in occasional, duplicate messages at the subscriber end. 
- Developers should design their applications such that processing a message more than once does not create any errors or inconsistencies.


**Q2. What is the purpose of the Dead-letter Queue (DLQ)? This is a feature available to SQS/SNS/EventBridge.**
- A dead-letter queue is an Amazon SQS queue that an Amazon SNS subscription can target for messages that cannot be delivered to subscribers successfully. 
- Messages that cannot be delivered due to client errors or server errors are held in the dead-letter queue for further analysis or reprocessing.


**Q3. How would you enable a notification to your email when messages are added to the DLQ**
- Create a CloudWatch Alarm on the Dead Letter Queue's `ApproximateNumberOfMessagesVisible` metric. Set the alarm condition to be when the value of that metric is greater than 0. 
- This will cause the Alarm to trigger whenever the Dead Letter Queue has 1 or more messages in it. 
- Configure the Alarm to trigger SNS to send an email to the subscriber.
