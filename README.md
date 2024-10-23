# salon-appointment-scheduler
Salon Appointment Scheduler
Overview
The Salon Appointment Scheduler is a bash-based system that allows salon customers to book appointments for various services. The project utilizes PostgreSQL as the database system, stores information about customers, services, and appointments, and provides a simple Command-Line Interface (CLI) for users to interact with the system.

This project implements user stories such as creating customers, scheduling appointments, and displaying services offered by the salon. The purpose of the project is to manage the scheduling process in a smooth and organized manner.

Table of Contents
Features
Technologies
Installation
Database Schema
How to Run
User Stories
Sample Output
Contributing
License

Features
Displays available salon services with unique IDs.
Books appointments for customers.
Recognizes returning customers via phone numbers.
Prompts new customers to input their details.
Confirms scheduled appointments with service and time details.
Uses PostgreSQL to manage customer, service, and appointment data.

Technologies
Bash scripting: For creating a Command-Line Interface (CLI) to interact with the database.
PostgreSQL: As the database management system to store and manipulate the data.
psql: PostgreSQL command-line tool to execute SQL commands.

Installation
Prerequisites:
Bash shell
PostgreSQL installed
psql command-line tool
Steps:
Clone the Repository: Clone the project from GitHub to your local machine.

bash
Copy code
git clone https://github.com/yourusername/salon-appointment-scheduler.git
cd salon-appointment-scheduler
Create the PostgreSQL Database: Log in to PostgreSQL and create the database.

bash
Copy code
psql --username=smilelink --dbname=postgres
Create the salon database:

sql
Copy code
CREATE DATABASE salon;
Create Tables: Connect to the database and create the necessary tables:

bash
Copy code
psql --username=smilelink --dbname=salon
Run the following SQL commands to create the required tables:

sql
Copy code
-- Create customers table
CREATE TABLE customers (
  customer_id SERIAL PRIMARY KEY,
  name VARCHAR(50),
  phone VARCHAR(15) UNIQUE
);

-- Create services table
CREATE TABLE services (
  service_id SERIAL PRIMARY KEY,
  name VARCHAR(50)
);

-- Create appointments table
CREATE TABLE appointments (
  appointment_id SERIAL PRIMARY KEY,
  customer_id INT REFERENCES customers(customer_id),
  service_id INT REFERENCES services(service_id),
  time VARCHAR(20)
);
Insert Service Data: Add at least three services into the services table:

sql
Copy code
INSERT INTO services (name) VALUES 
('cut'), 
('color'), 
('perm'),
('style'), 
('trim');
Make the Script Executable: After copying or writing the bash script (salon.sh), make it executable:

bash
Copy code
chmod +x salon.sh
Database Schema
The database consists of three tables:

customers:

customer_id: Unique identifier for each customer (Primary Key).
name: Name of the customer.
phone: Customer's phone number (Must be unique).
services:

service_id: Unique identifier for each service (Primary Key).
name: Name of the service (e.g., cut, color, perm).
appointments:

appointment_id: Unique identifier for each appointment (Primary Key).
customer_id: Foreign key referring to the customers table.
service_id: Foreign key referring to the services table.
time: The time for the appointment (stored as a VARCHAR).
How to Run
Run the bash script to start the Salon Appointment Scheduler:

bash
Copy code
./salon.sh
The script will:

Display a list of available services.
Prompt the user to select a service by entering the service ID.
Ask for the customer's phone number to identify the customer.
If the phone number doesn't exist, it will prompt for the customer's name and add them to the system.
Ask for the desired time for the appointment.
Confirm the booking by outputting the service and time.

User Stories
As a user, I want to see a list of all services offered so I can choose one to book.
As a user, I want to be asked for my phone number so I can log in to the system.
As a user, if I haven't booked before, I want to be prompted to provide my name so I can create an account.
As a user, I want to book an appointment at a specific time for a service so that I can schedule my visit.
As a user, I want to receive confirmation of my appointment including the service and the time.
Sample Output
Example 1: New customer booking an appointment.

bash
Copy code
~~~~~ MY SALON ~~~~~

Welcome to My Salon, how can I help you?

1) cut
2) color
3) perm
4) style
5) trim
1

What's your phone number?
555-555-5555

I don't have a record for that phone number, what's your name?
Fabio

What time would you like your cut, Fabio?
10:30

I have put you down for a cut at 10:30, Fabio.
Example 2: Existing customer booking a new appointment.

bash
Copy code
~~~~~ MY SALON ~~~~~

Welcome to My Salon, how can I help you?

1) cut
2) color
3) perm
4) style
5) trim
2

What's your phone number?
555-555-5555

What time would you like your color, Fabio?
11am

I have put you down for a color at 11am, Fabio.

Contributing
Feel free to fork this project and contribute! Here’s how you can get started:

Fork the repository.
Create a feature branch (git checkout -b feature-branch).
Commit your changes (git commit -am 'Add some feature').
Push to the branch (git push origin feature-branch).
Create a new Pull Request.

License
This project is open source and available under the freeCodeCamp & afbaslasu License.
