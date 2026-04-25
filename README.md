# SmartParking (ParkIQ)

A comprehensive, full-stack parking management system designed to optimize urban mobility and operational efficiency. ParkIQ leverages real-time data and automated payment processing to provide a seamless experience for both administrators and users.

## Project Overview
SmartParking addresses the challenges of modern parking logistics by automating the tracking of vehicle occupancy and securing financial transactions. Built with a focus on scalability and data integrity, the system ensures that parking resources are managed effectively while reducing manual oversight.

## Key Features
* **Real-time Occupancy Tracking:** Dynamic monitoring of available parking spots to provide users with up-to-date information.
* **Secure Payment Integration:** Automated transaction processing using the **Stripe API**, ensuring PCI-compliant handling of financial data.
* **Operational Dashboards:** Administrative views for monitoring usage patterns and financial reports.
* **Automated Notifications:** Real-time alerts for occupancy changes or payment confirmations.

## Tech Stack
* **Backend:** Node.js, Express.js
* **Database:** PostgreSQL (Relational data management and ACID compliance)
* **Payments:** Stripe API
* **Frontend:** HTML5, CSS3, JavaScript (ES6+)
* **Version Control:** Git & GitHub

## Security Implementation
To ensure the highest standards of software engineering and data protection:
* **Credential Masking:** All API keys and database credentials are managed via environment variables and are strictly excluded from the repository using `.gitignore`.
* **Input Validation:** Robust server-side validation to prevent SQL injection and cross-site scripting (XSS).
* **Transaction Integrity:** Leveraging Stripe's secure infrastructure to handle sensitive payment information.
