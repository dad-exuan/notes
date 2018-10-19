## Microservice Architecture at Medium

* What is Microservice Architecture?
  * Single purpose 
  * Loose coupling 
  * High cohesion
  ![Modeling Microservices](https://cdn-images-1.medium.com/max/2000/1*f5yQlyPApGNPfauFBe0pTA.png "Three Principles of Modeling Microservices")

  * A microservice is not:
    * a service that has a small number of lines of code or does "micro" tasks
    * a service that is built with new technology all the time
    * a service that has to be built from scratch

* Why Now?
  * Node.js monolithic app has become a bottleneck:
    * performance
    * slows down the product development
    * difficult to scale up or isolate resource concerns for different types of tasks
    * prevents us from trying out new technology

* Microservice Strategies
  * Build new services with clear value
    * there must be clear product value and/or engineering value 
  * Monolithic persistent storage considered harmful
    * A big part of modeling microservices is to model their persistent data storage, because it is: 
      * about implementation details
      * not service behaviors
    * only one service should be responsible for a specific type of data 
    * Monolithic model
      * Caching can be tricky
      * Reimplement the logic if change data storage
      * Reimplement the posts logics in the recommendation service
      * The recommendation service is stuck with post service
    * Decoupled model
      * Ideally, there should be a Post Service that owns the post data and other services can only access post data through the Post Service’s APIs. However, it could be an expensive upfront investment
      *  Option B queue updates
      *  Option C ETL read-only copy
  * Decouple “building a service” and “running services”
    * The service management should be completely decoupled from each individual service’s implementation, so that app engineers can fully focus on each service’s own business logic
    * Medium use [Istio](https://istio.io/) and [Envoy](https://www.envoyproxy.io/) for networking, [gRPC](https://grpc.io/) for communication protocol and containers for deployment
  * Thorough and consistent observability
    * **Observability** includes the processes, conventions, and tooling that let us understand how the system is working and triage issues when it isn’t working 
    * Every service gets consistent  detailed [DataDog](https://www.datadoghq.com/) dashboards, alerts, and log
    * Medium use [LightStep](https://lightstep.com/) heavily
  * Not every new service needs to be built from scratch
  * Respect failures because they will happen
    * First and foremost, we should expect everything will fail at some point
    * For RPC calls, put extra effort to handle failure cases
    * Make sure we have good observability to failures when they happen
    * Always test failures when bringing a new service online. It should be part of the new service check-list
    * Build auto-recovery if possible
  * Avoid "microservice syndromes" from day one
    * Poorly modeled microservices cause more harm than good
    * Allow too many different choices of languages/technology, which increase the operational cost and fragment the engineering organization
    * Couple running services with building services
    * Overlook data modeling and end up with monolithic data storage
    * Lack of observability
    * Tend to create a new service instead of fixing the existing one
    * Lack of a holistic picture of the whole system

## Should We Stop Building Monolithic Services?
* microservice architecture still involves a high level of complexity and complication
* architect the monolithic app in a way that is easier to migrate to a microservice architecture later 
* Each data type has two layers of implementation: data layer and service layer

## Conclusion
* benefit and potential
  * dramatically increased the development productivity
  * allowed us to think big and make substantial product improvement
  * unlocked the engineering team to safely test new technologies

Please refer to the [original article](https://medium.engineering/microservice-architecture-at-medium-9c33805eb74f)