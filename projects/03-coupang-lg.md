# From 8.4% Failure to 95% Growth: Solving a Critical Business Flaw

## The Business Context & The Strategic Challenge
At Coupang, our "Rocket Installation" service for large appliances like those from LG faced a critical business challenge. The existing process had a fundamental flaw: customers would select a desired delivery date upon purchase, but our partner, LG, had to manually call each customer afterward to schedule a different, actual installation date based on their own separate logistics.

This disconnect created two severe problems:

* A high Promised Delivery Date (PDD) miss rate of 8.4%, which significantly eroded customer trust.

* An inability to sell products not yet physically in our warehouse ("future stock"), resulting in substantial lost revenue opportunities.

My objective was to lead the re-architecture of this service to eliminate the PDD miss rate and unlock future sales by creating a fully automated, reliable scheduling system.

## My Role: Leading the Backend Re-architecture
As the lead engineer for this initiative, I was responsible for diagnosing the core problem, designing a new system architecture, and executing the technical solution. This involved not only backend development but also navigating a key technical constraint: our partner, LG, would not build a custom API for us. My role was to find a creative technical solution that worked within these real-world limitations to achieve our business goals.

## The Action: A Pragmatic Two-Part Solution for System Integration
The turning point was discovering that LG had an internal API providing technician availability, which they agreed to let us use. This, however, introduced new technical hurdles that required a robust, multi-faceted solution.

Solving the System Mismatch (Stock vs. Availability): Coupang's e-commerce system required a product to have a stock count to be sellable. However, the LG API only provided available installation dates, not a quantifiable stock number. To bridge this gap, I designed and implemented a system to create "placeholder" virtual stock. This data-driven approach dynamically generated virtual stock units mapped to each available installation slot, allowing us to list and sell future-availability products for the first time.

Ensuring Performance and Stability: The LG API was designed for internal use and provided availability on a per-product basis. Calling this API for every user browsing our site would have overloaded their system and critically slowed down our user experience. To solve this, I built an efficient, asynchronous background batch process. This job periodically polled the LG API, cached the availability data, and updated the virtual stock in our system, ensuring our platform remained fast and stable while providing near-real-time accuracy.

## Technical Implementation Details
The solution was architected as a resilient, decoupled system that bridged the logic of two independent companies:

* Virtual Stock Generation: A service was developed to translate date-based availability from the LG API into discrete, sellable units within Coupang's inventory system. Each available date/technician slot became a unique, temporary stock unit that could be claimed by a customer purchase.

* Asynchronous Data Synchronization: A scheduled batch job (running on Jenkins) was configured to periodically fetch availability data from the LG API. The results were processed and stored in a Redis cache for fast access, dramatically reducing latency and the load on the partner's API.

* Transactional Integrity: When a customer completed a purchase, the system would perform a final, real-time check against the LG API to lock in the installation slot, ensuring no double-bookings and guaranteeing the promised date.

## Technology Stack
Primary Languages: Java,Kotlin
Frameworks: Spring Boot, Jenkins
Databases & Caching: MySQL
Tools & Protocols: RESTful APIs, Git, JIRA, Docker, Kubernetes

## The Results: A Transformative Business Impact
The re-architecture was a definitive success, delivering transformative results that directly impacted the company's bottom line.

The PDD miss rate, once a major source of customer dissatisfaction, was virtually eliminated, dropping from 8.4% to an incredible 0.002%.

Most significantly, by enabling the sale of future inventory, we unlocked a major, previously inaccessible revenue stream. This was a key factor in driving a 95% year-over-year increase in sales for LG products on our platform.

## Key Takeaways
This project reinforced the critical lesson that the most elegant technical solution is often the one that pragmatically works around real-world constraints. Instead of being blocked by our partner's inability to provide a custom API, we found a creative way to leverage their existing infrastructure to our advantage. It was a powerful demonstration of how thoughtful backend architecture can directly solve core business problems, build customer trust, and unlock significant financial growth.
