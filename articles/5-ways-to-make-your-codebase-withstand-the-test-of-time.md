## 5 ways to make your codebase withstand the test of time

1. Split your code based on domain concepts to focus on a small part of your codebase, not tech concepts
2. Provide a public contract (API) for all your domain concepts
  * A clear picture of the expected behavior
  * A minimum test coverage everyone can agree upon and commit to
  * The freedom to change anything from the underlying implementation
  * this API to know as little as possible of external concepts 
3. Rely on small interfaces to create well-defined tests and choose the best strategy for each action depending on the environment
4. Decouple your data from your storage strategy
  * We should be able to harness the full power of the language we are using
  * We should be able to store our data in different formats and databases
5. Use events to keep your application connected and your code decoupled
  * All events are published through the event bus, and any observers can subscribe and react to interesting events without bothering the other components too much
  * Event-driven programming avoids long functions with many different side effects, and makes your tests nicer and more isolated

Please refer to the [original article](https://medium.com/@larribas/5-ways-to-make-your-codebase-withstand-the-test-of-time-9f9192ff1763)