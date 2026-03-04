---
{"dg-publish":true,"permalink":"/knowledge/furps/","tags":["FURPS","requirements"]}
---

---

FURPS+ is a way to categorize software requirements, developed by Hewlett-Packard (HP):

- Functionality
- Usability
- Reliability
- Performance
- Supportability
- + => other requirements and constraints

## **F**unctionality
Functionality contains the functional requirements aka. capabilities. It also includes non-functional requirements that apply to the entire system like:
- Audit
- Licensing
- Printing
- Reporting
- Security
    - Confidentiality (e.g. only authorized users have access to the data)
    - Integrity (e.g. data is consistent and correct)
    - Availability (e.g. data is available all the time)
- Debugging
- Scheduling

## **U**sability
Also UX contains the requirements that ensure a understandable and easy to learn and use product. Like:
- Accessibility
- Consistency
- Navigation rules (e.g. it concerns the support of using the keyboard, mouse or keyboard shortcuts)
- Training time (e.g. the training of new users will take 2 days or 8 hours)
- Usability standards (e.g. the usability solution will be in line with company policy/standards)

## **R**eliability
The ability of a product to perform a function (action) under specified conditions for a specified period of time or a specified number of operation. It concerns:
- Availability
- Accuracy
- Recoverability

## **P**erformance
The performance of a product contains:
- Capacity (e.g. the system must store 5 TB of data)
- Throughput (e.g. the system must support 100k transactions per minute or the system must support the parallel operation of 200 users)
- Response time (e.g. the system must respond in a maximum of 2 seconds, the maximum login time cannot be longer than 1 second)
- Scalability (e.g. that the system must automatically scale)

## **S**upportability
Supportability defines the ability of the system to be operated during the entire life cycle of the system. It consists of:
- Adaptability
- Auditability
- Configurability
- Installability
- Testability
- Maintainability
- Compatibility
- Localization (e.g. the system supports the Polish and English languages)

## **+**
Other Requirements and constraints like:
- Design & implementation (e.g. regarding the need to use a PostgreSQL relational database)
- Interface (e.g. the SOAP standard will be used for integration between the systems)
- Physical elements (e.g. may relate to the selection of specific servers)
- Legal information (e.g. regarding copyright)
