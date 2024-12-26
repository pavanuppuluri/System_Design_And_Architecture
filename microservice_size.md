## How to right size & identify service boundaries of microservices?

**Domain-Driven Sizing**  

Since many of our modifications or enhancements are driven by the business needs, we can size/define boundaries of our microservices that are closely aligned with Domain-driven Design and business capabilities. But this process takes a lot of time and needs good domain knowledge.

**Event Storming Sizing**  

Conducting an interactive fun session among various stakeholders to identify the important events in the system like
Completed payment, Searching a Product etc. Based on the events, we can identify 'Commands', 'Reactions' and can try to group them to a domain-driven services
