# Cracking Design Interview Questions

As I'm preparing for Microsoft interview, I'm trying to organize my knowledge on a wide array of software engineering topics. Having your mind organized helps you to go through design questions smoothly, start from the bird eye view and delve into details as necessary. It enables you to break down the question into smaller sub-problems. Also, it helps you to ask clarifying questions from the interviewer to define the technical scope of the problem.

The presented framework here does not dive into details. It's short and concise; gist of what is required to nail the interview. It is meant to serve folks with some years of real-world experience who are already have a degree of familiarity with the topics.

## Some general tips to have in mind

1. Design interview questions are meant to be vague and unclear. It's your job to clarify and define the the scope of the problem by asking **good** questions.
   * The final proposed solution should satisfy the requirements. As you work toward the final design make sure all requirments are met.
2. It's almost impossible to solve a deisgn problem in a 45 min session. They are not asked to get solved. The goal is to just measure your technical and critical thinking skills. 
3. There's no right answer to design problems. Though, some answers are better and some answers are entirely wrong. 
   * Your suggested design should be [scalable](https://www.allthingsdistributed.com/2006/03/a_word_on_scalability.html). In other words, the design should allow you to easilty add more resources to handle more load.  
4. In design interview questions, interviewee should have a dialog with the interviewer. You are expected to lead the interview. Imagine you're having a discussion with your team.
5. Start with a general overview of your system. Display what each component does and how they interact with each other.
6. When working on your design do not forget to mention the trade-offs you're making 
    * Cost vs Performance
    * Disk storage vs Memory 
    * Consistency vs Availability
    * Simplicity vs performance

## Some questions you might need to ask

1. Requirements should be discussed and clarified. 

    * Understand the use-cases or suggest a few use cases. 
    * Who is going to use it? 
    * How are they going to use it? 
    * What does the system do? 
    * What are the inputs and outputs of the system? 
    * What clients do we want to support (mobile, web, etc)? 
    * Do we require authentication? Analytics? Notification? Integrating with existing systems? 
    * Ask about timezones? 
    * Ask about geographical distributions of users? Do we need to deploy in multiple locations? 

 2. Constraints and assumptions should be identified. 

    * How many requests per second do we expect? 
    * What is the expected read to write ratio? 
    * How many users are there? 
    * How much data do we expect to handle? 
    * Do we need to have one database per service or do we need to have one single data storage? What are pros and cons? 
    * Can we use Kubernetes in our design?
    * Can we use cloud services in our design?
    * Do we have any concerns about the cost?
    
## How to tackle the design

When the broad design is finalized, dive into the details. Ask the interviewer about which component should be discussed in depth. 

   * Data layer (Schema, infrastructure) 
   * Web app layer 
   * API (REST) 
   * Front-end 
   * Infrastructure

**Data**: When designing the data layer, consider the following concerns: 
 
   * Read/Write ratio: Should we have separate databases for read and write? How do we deal with eventual consistency? Do we need to scale write and read separately? 
   * Do we need to have multiple write nodes? 
   * Do we need to implement replication? 
   * Do we need to think about storage cost and retention? 
   * Do we need to distribute data geographically? 
   * What types of data store we need to use? Do we need to use different data stores for different use cases? 
   * Can business tolerate eventual consistency? 
   * Should we implement distributed transactions? 
   * Is data structured or unstructured? 
   * Do we need to make joins on data to create complex reports?  
   * Can we denormalize data? 
   * How do you design non-relational schema? 
   * How do you store files? 
    * Azure Blob Storage
   * How do you deliver files to end users?
    * Azure CDN
   
**Service (API/APP)**: When designing the service layer, consider the following concerns: 
 
  * How do services talk to each other?  
    * Protocols 
      * GRPC for communicating between internal systems 
      * HTTP for customer facing services (Leveraging Open API standard) 
      * Messaging
        * Queue
        * Azure Service Bus
        * Event Hub
        * Event Grid
        * Kafka
        * RabbitMQ
     * Avoid chatty microservices 

  * How is the service discovery implemented? 
    * Kubernetes services 
    * Zookeeper 

  * Do you need distributed lock?
    * Redis
    * Azure Blob Storage: leasing technique
  
  * Do you need to handle distributed transactions?

  * How do we send notifications to user? 
    * SignalR 
    * Azure Notification Service 

 ## Some ideas for designing a service

  * DDD 
    * Divide the application logic to three layers as Application Layer (API), Domain Layer (models and contracts, persistence ignorant, infrastructure ignorant), and Infrastructure Layer (communicates with external systems ) 
    * Use rich domain models instead of anemic models 
    * Use aggregates as a transaction boundary and a validator gaurd 

  * CQRS
    * Do we need to scale write and read separately at application and data level? 
    * DDD is used in the write section of the architecture. For reads, we can use simpler approaches. 
    * We do not benfit from using rich domain models and aggregates in query side. They're meant to be used for writes. 
    * In CQRS, implementing repository pattern is not suggested. 
   
  * Onion Architecture 

 ## Nice things to not forget

  * How do you handle versioning? 
  
  * Resiliency 
    * Techniques 
      * Asynchronous messaging 
      * Circuit breaker 
      * Retry 
      * Timeout 

    * Solutions
      * Typed Http Clients
      * Polly 
      * Linkerd mesh 

  * Health checks 
