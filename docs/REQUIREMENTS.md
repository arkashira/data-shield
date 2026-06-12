# Requirements

## Functional Requirements

### FR-1: Data Monitoring

* The system shall continuously monitor data for potential deletion or modification.
* The system shall detect changes in data storage, including but not limited to:
	+ Data deletion
	+ Data modification
	+ Data addition
* The system shall provide real-time notifications to users when data is detected as being deleted or modified.

### FR-2: Notification System

* The system shall send notifications to users before data deletion or modification.
* The notification shall include:
	+ A clear description of the data being deleted or modified
	+ The reason for the deletion or modification
	+ A link to the transparency portal for further information
* The system shall support multiple notification channels, including but not limited to:
	+ Email
	+ SMS
	+ In-app notifications

### FR-3: Transparency Portal

* The system shall provide a clear and transparent view of data modifications and deletions.
* The transparency portal shall include:
	+ A log of all data modifications and deletions
	+ A description of the reason for each modification or deletion
	+ A link to the user's control panel for further action
* The system shall support filtering and sorting of the log to facilitate easy navigation.

### FR-4: User Control Panel

* The system shall allow users to make informed decisions about their data preservation.
* The user control panel shall include:
	+ A list of all data modifications and deletions
	+ A description of the reason for each modification or deletion
	+ Options for the user to:
		- Approve or reject the modification or deletion
		- Request additional information or clarification
		- Take no action

## Non-Functional Requirements

### NFR-1: Performance

* The system shall respond to user input within 2 seconds.
* The system shall process data modifications and deletions within 5 seconds.
* The system shall maintain a throughput of at least 100 requests per second.

### NFR-2: Security

* The system shall ensure the confidentiality, integrity, and availability of user data.
* The system shall implement encryption for all data in transit and at rest.
* The system shall implement access controls to restrict unauthorized access to user data.

### NFR-3: Reliability

* The system shall maintain a uptime of at least 99.99%.
* The system shall implement redundancy to ensure continued operation in the event of hardware failure.
* The system shall implement monitoring and logging to facilitate easy debugging and troubleshooting.

## Constraints

* The system shall be built using the tech stack determined in tech-stack.md.
* The system shall be deployed on a cloud-based platform.
* The system shall be scalable to support a minimum of 10,000 users.

## Assumptions

* The system shall assume that users have a basic understanding of data management and preservation.
* The system shall assume that users have a stable internet connection and a compatible web browser.
* The system shall assume that the tech stack and deployment platform are determined and locked in tech-stack.md.

## Dependencies

* The system shall depend on the following external services:
	+ A cloud-based database for storing user data
	+ A notification service for sending notifications to users
	+ A logging service for monitoring and logging system activity

## Compatibility

* The system shall be compatible with the following browsers:
	+ Google Chrome
	+ Mozilla Firefox
	+ Microsoft Edge
* The system shall be compatible with the following operating systems:
	+ Windows
	+ macOS
	+ Linux

## References

* [tech-stack.md]: Tech stack and deployment platform
* [CONTRIBUTING.md]: Guidelines for contributing to Data Shield
* [LICENSE]: License agreement for Data Shield
