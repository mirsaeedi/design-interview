# Cracking Design Interview Questions

As I'm preparing for Microsoft interview, I'm trying to organize my knowledge on different software engineering topics. Having your mind organized helps you to go through design questions smoothly. It enables you to break down the question into smaller sub-problems. Also, it helps you to ask clarifying questions from the interviewer which in turn lets you dive into the details with more insight.

I decided to prepare a framework for myself as a way for tackling design questions. The framework provides you with steps on how a question should be broken and clarified. Unlike most other articles on this topic, I do not intend to provide a guidance for juniors or folks who have just started learning about these kinds of interviews. The presented framework here is designed for myself and can be helpful for people with some years of real-world experience.

1. Design interview questions are meant to be vague and unclear. You should ask clarifying questions. 

2. There's no right answer for design problems. Though, some answers are better and some answers are entirely wrong. 

3. Scalability is one of the most important goals need to achieve by the suggested design. 

4. In design interview questions, interviewee should have a dialog with the interviewer. You are expected to lead the interview. Imagine you're having a discussion with your team. 

5. When working on your design do not forget to mention about the trade-offs you're making 

    * Cost 
    * Storage vs Memory 
    * Consistency vs Availability 
    * Simplicity vs performance 

6. Define the scope of the problem with your interviewer.  The final proposed solution should satisfy the requirements. 

7. Requirements should be discussed and clarified. 

    * Who is going to use it? 
    * Understand use-cases? 
    * How are they going to use it? 
    * What does the system do? 
    * What are the inputs and outputs of the system? 
    * Do we want to discuss the end-to-end experience or just the API? 
    * What clients do we want to support (mobile, web, etc)? 
    * Do we require authentication? Analytics? Integrating with existing systems? 
    * Ask about timezones? 
    * Ask about geographical distributions of users? almost all products deployed in multiple locations 

 8. Constraints and assumptions should be identified. 

    * How many requests per second do we expect? 
    * What is the expected read to write ratio? 
    * How many users are there? 
    * How much data do we expect to handle? 
    * Do we need to have one database per service? Do we need to have one single data storage for business data? What are pros and cons? 

 9. Start with a general overview of your system. Display what each component does and how they interact with each other. 

 10. When the broad design is finalized, dive into the details. Ask the interviewer about which component should be discussed in depth. 

    * Data layer (Schema, infrastructure) 
    * Web app layer 
    * API (REST) 
    * Front-end 

 11. When designing the data layer, consider the following concerns: 
 
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

 12. When designing the service layer, consider the following concerns: 
 
  * How services talk to each other?  
    * Protocols 
      * GRPC for communicating between internal systems 
      * HTTP for customer facing services (Leveraging Open API standard) 
      * Messaging 
        * Avoid chatty microservices 

  * How's the service discovery is implemented? 
    * Kubernetes services 
    * Zookeeper 

  * How do we send notifications to user? 
    * SignalR 
    * Azure Notification Service 

 * How we design the system? 

  * DDD 
    * Divide the application logic to three layers as Application Layer (API), Domain Layer (models and contracts, persistence ignorant, infrastructure ignorant), and Infrastructure Layer (communicates with external systems ) 
    * Use rich domain models instead of anemic models 
    * Use aggregates as a transaction boundary and validator gaurd 

  * CQRS: Do we need to scale write and read separately at application/data level? 
    * DDD is used in the write section of the architecture. For reads, we can use simpler approaches. 
    * We do not benfit from using rich domain models and aggregates in query side. They're meant to be used for writes. 
    * In CQRS, implementing repository pattern is not suggested. 
   
   * Onion Architecture 

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
    * ASPNET 
