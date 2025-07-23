# Unlocking a New Market: How Backend Integration Fueled Coupang's Success in Taiwan

## The Business Context & The Strategic Challenge
Coupang, often dubbed the "Amazon of South Korea," is a dominant e-commerce leader known for its hyper-efficient logistics and signature "Rocket Delivery" service. While I was there, the company began leveraging its domestic success to launch a strategic international expansion, with Taiwan identified as a key growth market.
![image](https://github.com/user-attachments/assets/61bf71b8-88d2-4edf-a383-e755c45a5f4e)
As part of this expansion, our team was tasked with building the foundational logistics infrastructure in Taiwan. The goal was to integrate our modern, automated systems with local partners, including convenience store (CVS) chains like Family Mart and Seven Eleven, for last-mile delivery.

Our initial approach utilized a third-party broker for this integration, but they proved to be unreliable, causing frequent service disruptions and a poor customer experience. To solve this and gain control over our logistics network, a strategic decision was made to build direct integrations with the CVS partners, cutting out the intermediary. The primary challenge was that these major partners operated on legacy technology stacks and relied on manual FTP file transfers—a stark contrast to Coupang's fully automated, API-driven architecture.

## My Role: Leading a Cross-Border Technical Integration
As a key engineer on the Coupang Partner Integration team, I took a leading role in architecting and executing the direct integration with Family Mart and Seven Eleven. My responsibilities went beyond coding; I drove the technical discovery process, managed complex cross-company communications (often with interpreters), and designed a solution to bridge the significant technology gap between our systems and our partners'.

## The Action: Reverse-Engineering and Automating Legacy FTP Workflows
The most significant hurdle was the partners' inability to provide technical specifications for their own FTP servers. Faced with a lack of documentation, I adopted a proactive, hands-on approach:

* Reverse-Engineering: I directly connected to the partners' FTP servers using command-line tools to perform a series of test uploads and downloads. By analyzing the behavior and file structures, I successfully reverse-engineered their undocumented protocols and data format requirements.

* Designing a Resilient Batch System: Since our partners' systems could not support real-time API calls, I designed a robust, automated batch-processing system to mimic their required manual workflow. This system was architected to be both resilient and scalable.

## Technical Implementation Details
The core of the solution was a scheduled, stateful service that managed the entire data exchange lifecycle without manual intervention:

* Automated Order Dispatch: A scheduled job was configured to run every 30 minutes, pulling new order information from Coupang's internal systems, formatting it into the required file type, and securely uploading it to the respective partner's FTP server.

* Asynchronous Status Polling: Another scheduled process ran every 3 hours to poll the partners' FTP servers for new delivery status files. It would download these files, parse them, and update the order status within Coupang's ecosystem, providing timely tracking information to our customers.

* Error Handling & Monitoring: The system included comprehensive logging and alerting to immediately flag any failed FTP connections, file parsing errors, or unexpected data, ensuring high reliability.

This entire integration was managed amidst complex communications involving two project managers, two engineers, and language interpreters in our meetings.

## Technology Stack
* Primary Languages: Java, Kotlin
* Frameworks: Spring Boot
* Protocols & Data Formats: FTP/SFTP, HTTP, CSV, JSON
* Tools & Platforms: Jenkins (for CI/CD and job scheduling), Git, JIRA, Docker, Kubernetes

![image](https://github.com/user-attachments/assets/ee4c58df-cae3-4a2c-bf7f-3ced8158a5d7)

## The Results: A Foundation for Explosive Growth
The direct integration was a resounding success and a critical enabler for Coupang's expansion in Taiwan.

By removing the unreliable broker, we established a direct line of communication with CVS operators, allowing for rapid issue resolution (e.g., handling sudden store closures). This dramatically improved service reliability. Furthermore, the project resulted in immediate cost savings on shipping fees.

Most importantly, this robust and scalable integration provided the technical foundation that allowed our Taiwan operations to grow from approximately $100K to $8M in revenue in just over a year and a half.

## Key Takeaways
This project was a pivotal experience in my growth as a backend engineer. It taught me that "standard" technology practices are not universal and underscored the importance of adaptability. When faced with legacy systems, the solution is not to demand they modernize, but to build an intelligent bridge. If I were to tackle a similar project, I would begin with the same assumption-free, manual-first testing approach to validate a partner's true technical capabilities before writing a single line of production code.
