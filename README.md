# ✈️ AIRBOOK PH  
### Technical Specifications Document (TSD)

## 1. Title Page
- **Project Name**: **AIRBOOK PH** Airline Booking System
- **Version**: 1.4 (Revised)
- **Date**: April 22, 2026
- **Author(s)**: Chinee Marasigan & Shae Padilla

---

## 2. Table of Contents
1. [Introduction](#3-introduction)  
2. [Overall Description](#4-overall-description)  
3. [Technology Stack](#5-technology-stack)   
4. [Visual Mockup Reference](#6-visual-mockup-reference)  
5. [Features](#7-features)  
6. [Functional Requirements](#8-functional-requirements)  
7. [Non-Functional Requirements](#9-non-functional-requirements)  
8. [Data Requirements](#10-data-requirements)  
9. [External Interface Requirements](#11-external-interface-requirements)  
10. [API Endpoints](#12-api-endpoints)  
11. [Glossary](#13-glossary)  
12. [Appendices](#14-appendices)  

---

## 3. Introduction

### Purpose
To develop a mobile-responsive airline booking system focusing on user security and seamless flight management. The application allows users to search for flights, select available itineraries, enter passenger information through a validated booking form, perform seat selection, and confirm reservations securely.

### Scope
The application includes secure user registration, login, dynamic flight search, a multi-step booking process, seat assignment, and itinerary retrieval. It does not include live payment gateways, real-time flight tracking, or automated check-in systems.

### Definitions, Acronyms, and Abbreviations
- **Bcrypt:** A library used for secure password hashing and salting to protect user credentials in the database.  
- **CORS (Cross-Origin Resource Sharing):** A security mechanism that allows the backend API to securely communicate with a frontend hosted on a different origin or port.  
- **dotenv:** A zero-dependency module used to manage environment variables and secure sensitive data.  
- **JWT (JSON Web Token):** Used for secure authentication and session handling.  
- **Mongoose:** ODM library for MongoDB used for schema-based data modeling.  
- **Node.js:** JavaScript runtime environment for backend execution.  
- **REST:** Architectural style for scalable web services.  
- **Bootstrap:** CSS framework for responsive UI design.  
- **ERD:** Entity-Relationship Diagram representing database structure.  

---

## 4. Overall Description

### Product Perspective
The application is a standalone single-page web application simulating an end-to-end airline booking workflow.

### Product Functions
- User authentication (Secure Registration/Login)
- Dynamic flight search and filtering
- Passenger data collection via validated forms
- Seat selection and assignment per passenger
- Booking storage and retrieval

### User Classes and Characteristics
- **Guest User:** Can browse flights but must register/login to book  
- **Registered User:** Can book flights and manage itineraries  
- **Admin User:** Has full CRUD access to flights, bookings, and users  

### Operating Environment
- Frontend: Chrome, Edge, Safari (mobile responsive)  
- Backend: Node.js and Express.js  
- Database: MongoDB Atlas  

### Assumptions and Dependencies
- Requires internet connectivity  
- MongoDB cluster must be active  

---

## 5. Technology Stack

### Frontend
- Next.js  
- React  
- CSS Modules  
- Axios  

### Backend
- Node.js  
- Express.js  

### Database
- MongoDB (Mongoose ODM)  

### Security
- JWT  
- Bcrypt  

---

## 6. Visual Mockup Reference

- **Figma Link:**  
https://www.figma.com/design/A1FVt00i3WJf3zmFgQfs13/Airline-Booking-System-Mock-up?node-id=1-3&t=AxokIMXwPXin9wi9-1  

---

## 7. Features

- Secure Authentication & Authorization  
- Dynamic Flight Search  
- Booking System  
- Seat Assignment per Passenger  
- Booking Management Dashboard
- Simulated Payment Processing  

---

## 8. Functional Requirements

### Use Cases

- **Use Case 1**: Secure User Registration
  - **Title**: User Registration with Password Encryption
  - **Description**: A new user creates an account to access booking features.
  - **Actors**: Guest User
  - **Preconditions**: User is on the Registration page.
  - **Postconditions**: User account is created; password is encrypted via Bcrypt in MongoDB.
  - **Main Flow**: User enters registration details > Clicks 'Register' > System validates input and hashes password > Account is saved.
  - **Alternate Flows**: User provides an existing email or leaves fields blank > System displays validation error.

---

- **Use Case 2**: End-to-End Flight Booking
  - **Title**: Flight Search, Selection, Seat Assignment, and Reservation
  - **Description**: A logged-in user searches for available flights, selects a flight, assigns seats to passengers, and completes a reservation.
  - **Actors**: Registered User
  - **Preconditions**: User is authenticated via JWT and on the Search page.
  - **Postconditions**: A booking record is created in MongoDB referencing the User and Flight IDs, including assigned seat and passenger details.
  - **Main Flow**:  
    User enters search criteria >  
    System displays results >  
    User selects a flight >  
    User selects seat(s) >  
    User enters passenger details >  
    User confirms booking >  
    System saves booking with assigned seat and passenger information
  - **Alternate Flows**: No flights match criteria > System displays "No Flights Found" message.

---

- **Use Case 3**: Itinerary Retrieval
  - **Title**: View and Manage Bookings
  - **Description**: User views their previous and upcoming flight reservations.
  - **Actors**: Registered User
  - **Preconditions**: User has at least one existing booking record.
  - **Postconditions**: System displays stored booking details.
  - **Main Flow**: User navigates to 'Manage Booking' > System retrieves data using Mongoose populate() > Details are displayed on a mobile-responsive dashboard.

---

### System Features

- **Feature 1**: Secure User Registration & Authentication
  - **Description**: Allows users to create accounts and securely log in to access booking management tools.
  - **Priority**: High
  - **Inputs**: User's name, email, password, and contact number.
  - **Processing**: The server receives data, hashes the password using Bcrypt, and stores the new user document in MongoDB.
  - **Outputs**: Successful account creation and session establishment via JWT.
  - **Error Handling**: Displays validation errors for missing fields, invalid email formats, or existing accounts.

---

- **Feature 2**: Dynamic Flight Search & Advanced Filtering
  - **Description**: Allows users to search for flights with trip-type toggles (Round-trip/One-way) and refine results using a FilterSidebar.
  - **Priority**: High
  - **Inputs**: Origin, destination, dates, price range, number of stops, and preferred airlines.
  - **Processing**: Mongoose queries filter documents based on sidebar selections. Results can be sorted by price, duration, or departure time.
  - **Outputs**: Detailed FlightCards showing airline info, duration, stops, and real-time pricing.
  - **Error Handling**: Displays an "Empty State" or "No Results Found" message if no flights match the criteria.

---

- **Feature 3**: Validated Booking Form with Seat Assignment
  - **Description**: Collects and validates passenger information and selected seat details to finalize a reservation.
  - **Priority**: High
  - **Inputs**: Passenger names, passport details (if applicable), contact details, selected flight reference, and selected seat(s).
  - **Processing**: Validates data integrity, assigns seats to each passenger, and creates a new booking document using Object ID referencing.
  - **Outputs**: Booking confirmation including seat assignments and unique reference number.
  - **Error Handling**: Displays errors for invalid data, missing fields, or unavailable seats.

---

- **Feature 4**: Manage Booking (Itinerary Retrieval)
  - **Description**: Users can search and view their booking history with status indicators.
  - **Priority**: High
  - **Inputs**: User authentication token or specific booking reference number.
  - **Processing**: Uses Mongoose `populate()` to link user data with flight documents and applies Status Filters (Upcoming vs. Completed).
  - **Outputs**: Searchable list of booking cards with status labels and action buttons.
  - **Error Handling**: Show a "Booking Not Found" error if the reference is invalid or the session has expired.

---

## 9. Non-Functional Requirements

- **Performance:** System should respond within a few seconds  
- **Security:** Password hashing and secure environment variables  
- **Usability:** Intuitive UI and smooth navigation  
- **Reliability:** The system ensures accurate seat allocation and prevents double-booking through seat availability tracking.
- **Maintainability:** Code should be clean and modular  

---

## 10. Data Requirements

### Seat Assignment Design Decision
The system uses an array of objects within the Bookings collection to store seat and passenger information. Each entry represents a passenger assigned to a specific seat, allowing support for multiple passengers per booking.
This approach improves scalability and eliminates the limitations of a single passengerDetails object, enabling accurate seat-level tracking and better alignment with real-world airline booking systems.

### Users

{
	_id: objectID,
	firstName: String,
	lastName: String,
	email: String,
	password: Hashed String,
	isAdmin: Boolean,
	mobileNumber: String
}
### Airlines

{
	_id: objectID,
	name: String,
	countryOfOperation: String
}
### Flights

{
	_id: objectID,
	airlineID: objectID,
	flightNumber: String,
	origin: String,
	destination: String,
	departureTime: Date,
	arrivalTime: Date,
	stops: Number,
	duration: Number,
	price: Number,
	isActive: Boolean,
	seatsAvailable: Number,
	totalSeats: Number,
	createdAt: Date,
	updatedAt: Date
}
### Bookings

{
	_id: objectID,
	bookingReference: String,
	userID: objectID,
	flightID: objectID,
	totalAmountPaid: Number,
	currency: String,
	paymentMethod: String,
	paymentStatus: String,
	status: String,
	numberOfPassengers: Number,
	seats: [
		{
		seatNumber: String,
		passengerName: String,
		class: String,
		passportNumber: String // Optional
		}
	],
	bookedOn: Date,
	createdAt: Date,
	updatedAt: Date
}
### Key Design Decisions
- Seat assignment is stored as an array of objects within bookings  
- Each passenger is mapped to a seat  
- ObjectID referencing is used for relationships  

### Database Requirements
- **Database Architecture:**  
  The system utilizes MongoDB, a document-oriented NoSQL database, to provide high scalability and flexible data structures for managing users, flights, airlines, and bookings.

- **Password Security:**  
  The `password` field is stored as a **Hashed String** using **Bcrypt** to ensure secure storage of user credentials.

- **Booking Reference:**  
  A unique alphanumeric `bookingReference` is generated for each booking record. This serves as a primary identifier for retrieving and managing reservations.

- **Object ID Referencing:**  
  The system uses MongoDB ObjectIDs to establish relationships between collections:
  - `userID` in **Bookings** references the **Users** collection  
  - `flightID` in **Bookings** references the **Flights** collection  
  - `airlineID` in **Flights** references the **Airlines** collection  
  This supports efficient data retrieval using Mongoose `populate()`.

- **Seat Assignment Structure:**  
  Instead of a single passengerDetails object, the system now uses a `seats` array of objects within the **Bookings** collection. Additional optional fields such as passportNumber may be included to support airline and travel requirements.

  Each object contains:
  - `seatNumber`
  - `passengerName`
  - `class`  
  - `passportNumber` 
  This enables support for multiple passengers per booking and seat-level tracking.

- **Flight Capacity Management:**  
  The **Flights** collection includes:
  - `totalSeats`
  - `seatsAvailable`  
  These fields are used to track seat availability and prevent overbooking.

- **Flight & Airline Relationship:**  
  Each flight document includes an `airlineID` that links to the Airlines collection, establishing a one-to-many relationship between airlines and flights.

- **Data Aggregation:**  
  The backend, built using Node.js and Express, utilizes Mongoose’s `populate()` method to combine related data across collections during operations such as flight search and itinerary retrieval.

---

### Data Storage and Retrieval

All data storage and retrieval operations are handled through a Node.js and Express backend using the Mongoose ODM. CRUD operations are performed on MongoDB collections, with relationships resolved using ObjectID referencing and population.

---

### Entity-Relationship Summary

- A **One-to-Many** relationship exists between Airlines and Flights  
- A **One-to-Many** relationship exists between Users and Bookings  
- A **Many-to-One** relationship exists between Bookings and Flights  
- The **Bookings collection acts as the central linking entity** connecting users and flights, while also storing seat assignment and transaction details

---

### ERD Implementation

The physical database structure is implemented based on the finalized Entity-Relationship Diagram (ERD), which defines the relationships between users, flights, airlines, and bookings.

### ERD Link
https://app.moqups.com/EN8380imW6sj1R9WzaXPj9HkuKREfei8/view/page/ad4e74bdc?ui=0  

- **Design Specifications:**  
  - Primary Palette: Brand Blue (#1A56DB), Success Green, Warning Yellow, Danger Red  
  - Typography: Inter (UI), JetBrains Mono (codes)  
  - Layout: 12-column Bootstrap grid  
  - Components: Rounded UI elements and mobile-first design

---

## 11. External Interface Requirements

### User Interfaces
- Homepage  
- Login/Register Page  
- Flight Search Page  
- Booking Page  
- Booking Management Page  

### API Interfaces
- REST API via Express.js  

### Hardware Interfaces
- Accessible via desktop and mobile devices  

### Software Interfaces
- Node.js backend  
- MongoDB database  
- Bootstrap frontend  

---

## 12. API Endpoints
### Admin – Flights
GET /admin/flights  
POST /admin/flights  
PATCH /admin/flights/:id  
DELETE /admin/flights/:id  

### Admin – Bookings
GET /admin/bookings  
PATCH /admin/bookings/:id  
DELETE /admin/bookings/:id  

### Admin – Users
GET /admin/users  
PATCH /admin/users/:id  
DELETE /admin/users/:id  

---

## 13. Glossary
- **Booking Reference** – Unique reservation ID  
- **Collection** – MongoDB equivalent of a table  
- **Document** – MongoDB record  
- **Field** – Data attribute  

---

## 14. Appendices

### Future Enhancements
- Seat Hold System (temporary reservation before confirmation)  
- Audit Logging for admin activity tracking  
- Real Payment Gateway Integration  
- Dynamic Pricing per seat/class  

---

## Revision History
- v1.0 (2026-03): Initial setup  
- v1.1 (2026-04): Security and filtering enhancements  
- v1.2 (2026-04): Updated Figma and ERD links  
- v1.3 (2026-04): Initial seat assignment design  
- v1.4 (2026-04):  
  - Implemented seat assignment (arrayOfObjects)  
  - Removed class from flights and moved it to seat-level structure
  - Added paymentStatus, currency, numberOfPassengers  
  - Added totalSeats and seatsAvailable  
  - Added timestamps  
  - Updated ERD and aligned TSD  
