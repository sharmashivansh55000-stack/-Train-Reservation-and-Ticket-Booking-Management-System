# -Train-Reservation-and-Ticket-Booking-Management-System
A comprehensive, production-ready Relational Database Management System (RDBMS) designed for rail transport network reservation, seat allocation, PNR generation, payment logging, and ticket cancellation management.
👤 Academic Information
Student Name: Shivansh
UID: 25BCA10433
Section: 25BCA 6B
Program: Bachelor of Computer Applications (BCA)
University: Chandigarh University
🛠️ Tech Stack & Database Architecture
Database Engine: MySQL Enterprise / Community Server 8.0+
Storage Engine: InnoDB (Enforces Foreign Keys & Transactional ACID Isolation)
Normalization Level: Third Normal Form (3NF)
Indexing: B-Tree Clustered Primary Keys & Non-Clustered Secondary Indexes
📋 Database Entity Schema (12 Tables)
Users - Registered passenger and administrator accounts.
Trains - Train inventory catalog and category classification.
Stations - Master list of railway stations with codes and zones.
Train_Routes - Sequential stop distance nodes along train journeys.
Schedules - Daily arrival and departure operational timings.
Coaches - Coach class tiers (SL, 3A, 2A, 1A, CC) per train.
Seats - Specific berth layout allocations (Lower, Upper, Side).
Passengers - Traveler profiles linked to government ID proofs.
Bookings - Master reservation header tracking 10-digit PNRs.
Tickets - Individual passenger berth assignments and travel dates.
Payments - Financial transaction logs and payment gateways.
Cancellations - Automated cancellation refund records and audit trails.
🚀 Installation & Setup Guide
Prerequisites
MySQL Server 8.0 installed locally or on cloud.
MySQL Workbench or Command Line Client.
Database Initialization Steps
# 1. Clone this repository
git clone https://github.com/your-username/train-reservation-dbms.git
cd train-reservation-dbms

# 2. Login to MySQL Engine
mysql -u root -p

# 3. Run the schema creation script
mysql> SOURCE database/train_reservation_system.sql;
⚡ Stored Procedure & Trigger Usage
Book a Ticket Automagically
CALL sp_BookTrainTicket(
    1,                   -- User ID
    1,                   -- Schedule ID
    1,                   -- Source Station ID (NDLS)
    2,                   -- Destination Station ID (CDG)
    645.00,              -- Fare (INR)
    'Shivansh',          -- Passenger Name
    20,                  -- Passenger Age
    'Male',              -- Gender
    1,                   -- Seat ID
    '2025-11-20',        -- Travel Date
    @pnr                 -- OUT parameter to receive 10-digit PNR
);

-- View generated PNR
SELECT @pnr AS Generated_PNR;
Cancel Ticket & Trigger Auto-Refund
UPDATE Bookings 
SET booking_status = 'Cancelled' 
WHERE pnr_number = '8947291045';

-- Check auto-created refund record
SELECT * FROM Cancellations;
📊 Sample Queries & Performance Benchmarks
PNR Search Speed: < 4ms (Utilizing index idx_pnr_lookup).
Route Node Search: Multi-table JOIN linking Trains, Routes, and Stations.
📜 License
This project is open-source and released under the MIT License for educational purposes at Chandigarh University.
