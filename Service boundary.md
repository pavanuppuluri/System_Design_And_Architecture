> In simple terms, it answers four questions:
> 1. What business capability does this service own?
> 2. What data is it responsible for?
> 3. What operations can it perform?
> 4. How does it interact with other services?
> 
> The objective is to ensure that each microservice has a clear business responsibility and can evolve independently without creating unnecessary dependencies on other services.

I generally start defining microservice boundaries from business capabilities rather than technology or existing application modules.

First, I understand the end-to-end business process and identify the different capabilities involved. I then use Domain-Driven Design concepts, particularly Bounded Contexts, to identify logical boundaries.

For each proposed service, I look at its business responsibility, data ownership, transaction boundaries, and interactions with other services.

I also evaluate cohesion and coupling. My objective is to ensure that each service has strong internal cohesion, minimal external dependencies, and can evolve and scale independently.

For cross-service workflows, I evaluate whether synchronous or asynchronous communication is appropriate and consider patterns such as Saga for distributed transactions.

Finally, I validate the boundaries with architects, developers, and business stakeholders, considering operational complexity, deployment independence, scalability, and long-term maintainability.

One thing I am particularly careful about is avoiding over-decomposition. Microservices should solve business and organisational problems, not introduce unnecessary distributed-system complexity.

Ultimately, I define a service boundary around a business capability that has clear ownership, data responsibility, and a well-defined contract with the rest of the ecosystem.
