## Introduction
- things systems should not do: They should not crash, hang, lose data, violate privacy, lose money, destroy your company, or kill your customers.
- Your early decisions make the biggest impact on the eventual shape of your system.
- Systems spend much more of their life in operation than in development.
- Design and architecture decisions are also financial decisions.
- the pragmatic architect constantly thinks about the dynamics of change.
- The worst problem here is that the bug in one system could propagate to all the other affected systems.
- A highly stable design usually costs the same to implement as an unstable one.
- Run longevity tests. It’s the only way to catch longevity bugs.
- What are all the ways this can go wrong?
- big systems fail faster than small systems.
- the main point to remember is that things will break.

## Stability Anti Patterns
1. Integration Points (P59)
- Integration points are the number one killer of systems.
- TCP/IP
* The simplest failure mode occurs when the remote system refuses connections. The calling system must deal with connection failures.
* a slow response is a lot worse than no response.
- HTTP
* mainly centered around the client library.
- 3rd party
* the best thing you can do is decompile the code, find issues, and report them as bugs
* The prime stability killer with vendor API libraries is all about blocking
- The most effective patterns to combat integration point failures are Circuit Breaker and Decoupling Middleware. Testing helps, too.
- you should make a test harness: a simulator that provides controllable behavior.

2. Chain Reactions (P62)
- A chain reaction occurs when there is some defect in an application, usually a resource leak or a load-related crash.

3. Cascading Failures (P66)
- A cascading failure occurs when problems in one layer cause problems in callers.
- Integration Points without Timeouts is a surefire way to create Cascading Failures.
- Cascading failures are the number one crack accelerator. The most effective patterns to combat cascading failures are Circuit Breaker and Timeouts.
- A cascading failure often results from a resource pool. Defend with Timeouts and Circuit Breaker.

4. Users
- How does your system react to excessive demand?
- The best thing you can do about expensive users is test aggressively.

5. Blocked Threads (P87)
- The best way to improve your chances is to carefully craft your code. Use a small set of primitives in known patterns. It’s best if you download a well-crafted, proven library.
- Use proven primitives

6. Attacks of Self-Denial (P90)
- Good marketing can kill you at any time.

7. Scaling Effects (P95)
- Because the development and test environments rarely replicate production sizing, it can be hard to see where scaling effects will bite you.
- Do the simplest thing that will work.
- The most scalable architecture is the shared-nothing architecture.
- Point-to-point communication scales badly

8. Unbalanced Capacities
- Unbalanced capacities is another problem rarely observed during QA.
- Be ready for anything.
- backend: huge volumn, front end: stop response or very slow

9. Slow Responses (P101)
- Slow responses usually result from excessive demand.
- give your system the ability to monitor its own performance. such as moving average
- any such refusal to provide service must be well-documented and expected by the callers.

10. SLA Inversion (P105)
- A service-level agreement are quantitative measures of service delivery with financial penalties if the service provider does not meet them.
- the best you can possibly do is the SLA of the worst of your service providers.
- When calling third parties, service levels only decrease.
- First, you can decouple from the lower-SLA system. Second, be careful when crafting your service-level agreements.

11. Unbounded Result Sets (P109)
- Design with skepticism, and you will achieve resilience.
- Ask, “What can system X do to hurt me?”
- query for the full results but break out of the processing loop after reaching the maximum number of rows.


## Stability Patterns
- develop a recovery-oriented mind-set.
- expect failures.

1. Use Timeouts (P114)
- networks are fallible.
- Well-placed timeouts provide fault isolation
- You may find that half your code is devoted to error handling instead of providing features.
- An approach to dealing with pervasive timeouts is to organize long-running operations into a set of primitives that you can reuse in many places.
- Timeouts are often observed together with retries. Under the philosophy of “best effort”
- but fast retries are very likely to fail again.
- In any case, just come back with an answer.
- queuing the work for a slow retry later is a very good thing, making the system much more robust.
- Timeouts have natural synergy with circuit breakers.

2. Circuit Breaker (P117)
- The principle is: detect excess usage, fail first and open the circuit.
- the circuit breaker may track different types of failures separately.
- a way to automatically degrade functionality when the system is under stress.
- Changes in a circuit breaker’s state should always be logged, and the current state should be exposed for querying and monitoring.

3. Bulkheads (P122)
- Protect critical clients by giving them their own pool to call.
- Physical redundancy is the most common form of bulkheads.
- The goal is to identify the natural boundaries that let you partition the system in a way that is both technically feasible and financially beneficial.
- it is often helpful to reserve a pool of request-handling threads for administrative use.
- Pick a useful granularity

4. Steady State (P129)
- Every single time a human touches a server is an opportunity for unforced errors and it’s best to keep people off of production systems.
- for every mechanism that accumulates a resource, some other mechanism must recycle that resource.
- Data purging never makes it into the first release, but it should.
- the logging filesystem is separate from any critical data storage.
- Don’t leave log files on production systems. Copy them to a staging area for analysis.
- The simplest mechanism is a time-based cache flush.

5. Fail Fast (P129)
- be sure to report a system failure differently than an application failure

6. Handshaking
- The sad truth is that HTTP doesn’t handshake well.
- Handshaking is all about letting the server protect itself by throttling its own workload.
- Your best bet is to build handshaking into any custom protocols that you implement.
- Health-check requests are an application-level workaround for the lack of Handshaking in the protocols.

7. Test Harness
- Integration test environments can verify only what the system does when its dependencies are working correctly.
- every system will eventually end up operating outside of spec
- A better approach to integration testing would allow you to test most or all of these failure modes.
- Consider building a test harness that substitutes for the remote end of every web services call.
- One trick I like is to have different port numbers indicate different kinds of misbehavior.

8. Decoupling Middleware (P143)
- Done well, middleware simultaneously integrates and decouples systems.
- letting the participating systems removing specific knowledge of and calls to the other systems.
- Less tightly coupled forms of middleware allow the calling and receiving systems to process messages in different places and at different times.
- Message-oriented middleware decouples the endpoints in both space and time.
- Decoupling Middleware is an architecture decision.

9. Summary
- The key to applying these patterns successfully is judgment.



## Capacity Introduction
- Performance measures how fast the system processes a single transaction.
- Throughput describes the number of transactions the system can process in a given time span.
- End users care about performance while customers care about capacity.
- Throughput is always limited by a constraint in the system - a bottleneck.
- Capacity = maximum normal throughput
- The hardest thing about dealing with capacity is working with nonlinear effects.
- In every system, exactly one constraint determines the system’s capacity.
- Understanding the capacity of any system requires systems thinking.
- Place safety limits on everything.


## Capacity Antipatterns
1. Resource Pool Contention (P176)

2. Excessive JSP fragment (P180)

3. AJAX Overkill (P182)
- The best places to apply AJAX are those interactions that represent a single task in the user’s mind.

4 Reload button (P191)
- There is no good answer about what to do with the Reload button. Just make sure your site is fast enough that users don’t click it.

5. Minimize handcrafted SQL (P193)
- One solution would be to achieve perfect knowledge, with perfect specifications, before developing the application.
- The best answer to slowdowns due to data growth in the database is a rigorous routine of archival and elimination.
- In particular, reporting and ad hoc analysis should never be done in the production database.
- “location transparency”  has been widely discredited.


## Capacity Patterns
1. Pool Connections (P206)
- resource pools can dramatically improve capacity.
- Connection pool sizing is a vital issue.

2. Use Caching Carefully (P208)
- The maximum memory usage of all application-level caches should be configurable.

3. Precompute (P210)
- Precompute content that changes infrequently

4. Others
- The principle of “least privilege” mandates that a process should have the lowest level of privilege needed to accomplish its task.
- guaranteed availability necessarily increases costs
- SLA definitions are like the details in your medical insurance plan.
- synthetic transaction
- When the servers are aware of each other and actively participate in distributing load, then they form a cluster.
- for administrtor, just understand their motivations, and commit to making their work easier.
- Property files suffer from hidden linkages and high complexity—two of the biggest factors leading to operator error.
- keep production configuration properties separate from the basic wiring and plumbing of the application.
- the production configuration files should not be anywhere underneath the installation directory of the software itself.
- Don’t accept connections until start-up is complete.

## Transparency (P265)
- Transparency refers to the qualities that allow operators, developers, and business sponsors to gain understanding of the system’s historical trends, present conditions, instantaneous state, and future projections.
- transparent systems will mature faster than opaque ones
- Good data enables good decision making.
- It’s better to catch the aberrant behavior before users start walking away.
- In designing for transparency, keep a close eye on coupling.
- good old log files are still the most reliable, versatile information vehicle.
- In fact, administrators and engineers in operations will spend far more time with these log files than developers will.
- Logging should be aimed at production operations rather than development or testing.
- Reserve “ERROR” for a serious system problem.
- One of the common requests from operations is a list of all the log messages the system can produce.
- Messages should include an identifier that can be used to trace the steps of a transaction.
- Interesting state transitions should be logged.
- Linking operations to business results requires the ability to correlate “systems” information with “business” information.
- Within the application, the ideal is to expose every state variable, counter, and metric. A list on P297: Traffic indicators, Resource pool health, Database connection health, Integration point health, Cache health
- Observations are the heart of the OpsDb.
- creating a client-side API to feed observations to the OpsDb
- Deviation greater than or less than that expectation would trigger alerts.
- The best data in the world can’t help if nobody is looking.
- acting responsively to meaningful data. P305
- build an operational rhythm weekly or monthly that makes improvement P307
- Once a metric stops producing useful information, stop reviewing it.

## Adaptation (P310)
- The true birth of a system comes on the day it launches into production.
- “form follows failure.”
- somewhere between 40% and 90% of a system’s cost of development will be incurred after the first release.
- Defining and using interfaces is the main key to successfully achieving flexibility with dependency injection.
- every object suits exactly one purpose to which it is supremely adapted.
- database schemas must change.
- Every schema should include a table that indicates the current structure revision.
- Does it make IT better at responding to its users’ needs?
- good architecture embraces the need for change as fundamental.
- We must design protocols so that either endpoint can change independently of the other. The solution is protocol versioning.
- wrap a web service around the database
- Transporting large volumes of data out of production is sometimes necessary.
- Release: a closed feed-back loop is essential to improvement.
- The right response is to reduce the effort needed, remove people from the process, and make the whole thing more automated and standardized.
- If the software is totally self-contained, then the presence of two versions doesn’t pose a problem.
- The key is to break up the deployment into phases (P335)
* The first step is to add new “stuff”. The receiving application must support multiple versions of the protocol.
* Rollout
* Cleanup