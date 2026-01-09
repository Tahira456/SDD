Software Design Document
Smart HealthCare Management System with Patient Portal and Administrative Control 

 

Submitted by
Name: Tahira Malik
Roll no: F22BINFT1M01009

Submitted to
Ms. Sara Fareed


Department of Information Technology
Faculty of Computing
The Islamia University of Bahawalpur

Summery
The Smart HealthCare Management System is a web-based digital platform designed to streamline hospital operations. The primary goal is to provide centralized management for patient records, appointments, medical reports, billing, and complaints.
The system offers a secure patient portal allowing users to register, log in, book appointments, and access their medical records and billing history. Concurrently, the administrative dashboard allows authorized staff to manage patient profiles, reports, billing, and handle feedback efficiently.

Design Considerations:

Architecture: A three-tier Client-Server architecture is utilized, featuring Python (Django) for the backend and a centralized MySQL database for data storage.
Performance:
The design is optimized to achieve a fast response time of less than 2 seconds.
Security:
Measures include secure authentication and implementing role-based access to protect sensitive patient data.
Scalability:
The system is designed to be scalable to accommodate future growth and support up to 10,000 users.
This document details the software architecture, the specific data model schema (ERD), and the user interface design philosophy necessary for the implementation of this centralized, secure, and efficient healthcare management system.











Table of Content:

Section Number	Section Title	Content Focus
1.		Summary	Project Overview, Design Goals 
2.		Application Architecture	3-Tier Structure (Django, MySQL), MVC, System Components
3.		Diagrams	Class and Sequence Diagrams
4.		Data Model Schema	ERD and Details of Core Entities (User, Patient, Appointment, etc.) 
5.		User Interface	Design Philosophy, Screen List (Patient Portal, Admin Dashboard) 
6.		Conclusion	Final Summary






 

1.	Application Architecture
3.1 Architectural Style
The Smart HealthCare Management System employs a robust, industry-standard 3-Tier Client-Server Architecture. This architecture divides the application into three decoupled logical layers, enhancing scalability, security, and maintainability.
1.	Presentation Tier (Client):
2.	This is the user interface accessible via standard web browsers. It is built using HTML, CSS, JavaScript, and Bootstrap.
3.	Application Tier (Business Logic):
4.	This central layer manages all processing, control flow, and functional requirements. It is powered by Python utilizing the Django framework.
5.	Data Tier (Database):
6.	This layer provides centralized, persistent storage for all system data, utilizing MySQL.
3.2 System Context and Components
The system functions as a central hub, receiving input and providing output to three main external actors, as shown in the system context diagram:
•	Patient:
Interacts for registration, login, appointment requests, and viewing confirmation/details.
•	Admin:
Interacts for registration confirmation, login, adding/updating data, and managing patient records.
•	Doctor:
Interacts to request patient records (implicitly managed by the Admin Controller).
3.3 Proposed Models, Views, and Controllers (MVC Pattern)
The application development leverages the Model-View-Controller (MVC) architectural pattern, which is natively supported by Django (often referred to as Model-View-Template).

MVC Component	Description	Role in System
Models	Defines the data structure (schema) 10 for entities like Patient, Appointment, Medical_Report, and Billing. Models interact directly with the MySQL database.	Data integrity and persistence11.
Views (Templates)	Defines the User Interface (UI) and presentation logic. This includes the Patient Portal screens and the Admin Dashboard screens.	User experience and data presentation13.
Controllers (View in Django)	Handles incoming HTTP requests, executes business logic, interacts with the Models, and renders the appropriate View (Template).	Functional requirements processing15.
3.4 Controllers and Functions (Business Logic)
The Controller layer holds the core business logic. The following list details the functions within these controllers that manage the system's operational requirements16:
Controller/Module	List of Function/Methods	Description of Functionality
Authentication Controller	patient_register(), admin_login(), check_role_access()	Securely manages user registration and role-based login17171717.
Appointment Controller	request_appointment(), check_doctor_availability(), confirm_appointment()	Manages the workflow from slot selection to notification 18181818.
Admin Management Controller	add_patient_record(), update_patient_record(), delete_patient_record(), search_records()	Executes all CRUD (Create, Read, Update, Delete) operations on patient data 19191919.
Report&Billing Controller	upload_medical_report(), view_report_history(), track_billing()	Manages the secure access and storage of medical reports and financial records20202020.

3.5 API and External Library Specifications
•	Internal APIs:
The system will use Django's REST framework capabilities to expose internal APIs to handle data flow between the frontend (Bootstrap/JavaScript) and the backend controllers. These APIs facilitate fast and asynchronous data exchange, contributing to the required $<2$ seconds response time21.
•	External Libraries:
The system relies on Bootstrap for responsive design and a user-friendly interface22222222.
3.6 UML Diagrams
UML diagrams will be used to visualize system working2323:
•	Class Diagram:
To explain the structural relationships between the Models (Patient, Appointment, Report, etc.)24242424.
•	Sequence Diagrams:
To detail the flow of processes for key use cases, such as "Patient Books Appointment" and "Admin Manages Patient Records" 25252525.
3.7 Coding Conventions
Standard Python (PEP 8) and Django coding conventions will be followed to ensure the code is clean, readable, and maintainable26. This includes descriptive variable names, docstrings for all functions, and clear separation of logic within the MVC structure.

 
Health Care Administration System:
The Health Care Administration System is the core functional hub of the overall project, specifically encompassing the business logic and database management required to streamline hospital operations. It is the centralized component that supports the Administrative Dashboard and ensures data integrity.
Here is a summary of its role:
The Health Care Administration System serves as the central processing layer, built using the Python (Django) framework and connected to the MySQL database. Its primary purpose is to provide centralized management for all patient-related data and hospital workflows.

Diagram:
 
 
1.	UNML Class Diagram (Structural View)
The two UML diagrams provided visualize the design of the Smart HealthCare Management System on two critical levels: data structure (static view) and system behavior (dynamic flow).
1. UNML Class Diagram (Structural View)
This diagram visualizes the structure of the system's database, detailing the main entities (classes/tables) and their relationships.
•	Purpose:
To define the architecture of the Data Model Schema (Section 4) and ensure data integrity within the MySQL database.
•	Core Entities:
It features six main entities: User, Patient, Admin, Appointment, Medical_Report, Billing, and an assumed Doctor entity.
•	Key Relationships:
o	The User class is central, managing authentication and connecting on a one-to-one basis to either a Patient or an Admin.
o	The Patient class (which holds personal details) is linked to multiple transactional entities, specifically having a one-to-many relationship with Appointment, Medical_Report, and Billing.
o	The Appointment entity is linked to both the Patient and the Doctor, defining the booking structure.
 
Class Diagram:
 
 
Sequence Diagram: Patient Books an Appointment (Behavioral View)
This diagram illustrates the step-by-step, time-ordered sequence of interactions required to perform a critical functional requirement.
•	Purpose:
To detail the flow of processes for the key use case "Patient Books Appointment", showing how the various architectural components (Models, UI, Services) work together.
•	Objects Involved:
The main objects are the Patient (Actor), the UI (Frontend), the AppointmentModel (Controller Logic), the DoctorModel (Data Access for availability), and the NotificationService.
•	Flow:
The diagram shows the message passing, starting from the Patient initiating the request through the UI. The request is processed by the AppointmentModel, which must query the DoctorModel for availability before the appointment is treated (saved). Finally, a confirmation message is sent via the NotificationService and displayed back to the browser. This visual flow ensures the system meets the functional requirement for appointment management.

Sequence Diagram:
 
 
2.	Data Model Schema
Here is the revised text with all extras removed and formatted for a Microsoft Word document:

4.1 Conceptual Schema Overview
The Smart HealthCare Management System utilizes a relational database structure managed by MySQL. The data model is designed to be centralized, ensuring data consistency and integrity across all system functionalities, including patient management, appointment scheduling, and report access. The schema is comprised of six core entities that manage user authentication, patient demographic details, and all transactional data (appointments, reports, and billing).

4.2 Entity Relationship Diagram (ERD)
A formal Entity Relationship Diagram (ERD) is used to visually represent the relationships between the entities. This diagram illustrates how the primary entities (User, Patient, Admin, Appointment, Medical Report, Billing) connect via foreign keys to support the system's operational requirements, such as linking a patient to their medical reports and appointment history.

4.3 Detailed Data Model Entities

4.3.1 User Entity
This entity acts as the primary access control point for the entire application. It stores credentials and roles for both patients and administrators. The User_ID serves as the primary key. Essential properties include Username, which is unique, and a Password_Hash for secure storage. The Role property defines the user type, controlling access based on role-based security requirements.

4.3.2 Patient Entity
This entity stores all demographic and relevant clinical data specific to the patient. It has a one-to-one relationship with the User entity via a foreign key reference to User_ID, ensuring every patient can securely log in. The Patient_ID is the primary key. Other key properties include Name, DOB, and contact information
4.3.3 Admin Entity
This entity stores details for authorized hospital administrators. Like the Patient entity, it has a one-to-one relationship with the User entity. The Admin_ID is the primary key. Administrators require access to manage patient profiles, reports, and feedback.

4.3.4 Appointment Entity
This transactional entity manages all appointment bookings. It includes foreign key relationships to link the specific patient (Patient_ID) to the appointment. The Appt_ID is the primary key. Other properties include the Date, Time_Slot, and a Status (e.g., 'Confirmed', 'Pending') to manage the appointment lifecycle. This entity facilitates the patient use case of booking appointments.

4.3.5 Medical Report Entity
This entity facilitates the management and access of medical history and reports. It has a one-to-many relationship with the Patient entity, as one patient can have multiple reports. The Report_ID is the primary key. Key properties include Report_Type, Date_Issued, and the secure File_Path to the actual report document. This supports the administrator function of uploading/updating reports and the patient function of viewing/downloading them.

4.3.6 Billing Entity
This entity tracks patient billing and payment information. It maintains a one-to-many relationship with the Patient entity. The Bill_ID is the primary key. Properties include a Service_Description, the Amount billed, and a Payment_Status (e.g., 'Paid', 'Pending') to allow patients to track their financial records.








3.	User Interface
Here is the content formatted for Microsoft Word with all asterisks removed.

5. User Interface
5.1 Overall Design Philosophy
The overall design philosophy is centered on creating a user-friendly and highly accessible digital platform. The UI is segmented into distinct views for patients and administrators, ensuring role-based functionality and simplicity.

Design Niche:
The design adopts a clean, professional aesthetic suitable for a modern healthcare management system. The goal is to simplify workflow and enhance patient engagement.

Color Scheme and Font:
A professional and readable color scheme will be employed, prioritizing visual hierarchy and clarity. A clean, legible sans-serif font will be used throughout.

Screen Constraints and Responsiveness:
The system is a web-based platform. The user interface will be built using HTML, CSS, and JavaScript with Bootstrap. This choice ensures the application is fully responsive, running smoothly across various web browsers (Chrome, Firefox, Edge) and screen sizes.

5.2 List of Screens/Pages and Data Display
The system provides two main dashboards: the Patient Portal and the Administrator Dashboard.

5.2.1 Patient Login and Registration
This screen provides secure authentication for both patient and admin roles.
Data Display: Input fields for user credentials (Username, Password). Registration includes fields for personal details.
5.2.2 Patient Dashboard
The central hub for the registered patient.
Data Display: Quick access links and summaries for appointment management, medical history, reports, and billing records.

5.2.3 Appointment Booking Screen
This screen handles the core functionality of scheduling.
Data Display: Calendar view or form to select the desired doctor, date, and time slot. A confirmation notification is displayed upon successful booking.

5.2.4 Medical Reports View
Allows the patient to review their medical records.
Data Display: A chronological, filterable list of available medical reports. Patients can view and download reports.

5.2.5 Admin Dashboard (Patient Management)
The primary workspace for administrators.
Data Display: A searchable and filterable list view of all registered patients. Navigation controls to manage patient profiles (CRUD operations), medical reports, billing, and system complaints.
5.3 Controls and Input Constraints
Standard web controls (Textboxes, Drop Down, Buttons) will be used.
Authentication Controls: Password fields will require strong constraints (minimum length and complexity) and employ secure login mechanisms.
Appointment Controls: Drop-down lists will be used to restrict selection to valid doctors and time slots, preventing incorrect data entry.
Admin Data Management Controls: Textboxes used by administrators for updating patient records will have constraints to ensure data consistency, such as ensuring numeric fields contain only numbers and date fields follow the correct format.
Performance Constraint: All UI operations, including form submissions and data retrieval, are constrained by the non-functional requirement of a response time of less than 2 seconds.
 
Conclusion
The design phase for the Smart HealthCare Management System has successfully established a robust, scalable, and secure architecture that fully addresses all functional and non-functional requirements .
Design Success Summary
•	Architectural Clarity: The 3-Tier Client-Server Architecture , utilizing the Python/Django framework and a MySQL database, provides a decoupled and highly maintainable foundation for development.
•	Data Integrity: The detailed Data Model Schema (Section 4), visualized by the UML Class Diagram , ensures data consistency for critical entities like Patient, Appointment, and Billing.
•	Functional Compliance: The design supports all key use cases, including secure role-based access for both Patient and Admin users , as demonstrated in the System Context Diagram and the Appointment Booking Sequence Diagram.
•	Performance and Scalability: Specific design choices, such as using internal APIs for fast, asynchronous data exchange , directly support the non-functional goals of achieving a response time less than 2 seconds and supporting up to 10,000 users.
This Software Design Document serves as the definitive blueprint for the implementation phase, providing clear, detailed instructions across the application, data, and presentation tiers. The system is well-positioned for efficient development, ensuring the resulting application is a centralized, secure, and highly effective management tool for hospital operations.

