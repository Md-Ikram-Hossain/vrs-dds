-- Users Table
CREATE TABLE users (
user_id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
password TEXT NOT NULL,
phone VARCHAR(20),
role VARCHAR(20) CHECK (role IN ('admin', 'customer')) NOT NULL
);

INSERT INTO users (name, email, password, phone, role) VALUES
('John Doe', 'john@example.com', 'pass123', '01711111111', 'customer'),
('Alice Smith', 'alice@example.com', 'pass123', '01722222222', 'customer'),
('Bob Johnson', 'bob@example.com', 'pass123', '01733333333', 'customer'),
('Emma Brown', 'emma@example.com', 'pass123', '01744444444', 'customer'),
('Michael Lee', 'michael@example.com', 'pass123', '01755555555', 'customer'),
('Sophia Wilson', 'sophia@example.com', 'pass123', '01766666666', 'customer'),
('David Miller', 'david@example.com', 'pass123', '01777777777', 'customer'),
('Olivia Taylor', 'olivia@example.com', 'pass123', '01788888888', 'customer'),
('Admin One', 'admin1@example.com', 'admin123', '01911111111', 'admin'),
('Admin Two', 'admin2@example.com', 'admin123', '01922222222', 'admin');


-- Vehicles Table
CREATE TABLE vehicles (
vehicle_id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT NULL,
type VARCHAR(20) CHECK (type IN ('car', 'bike', 'truck')) NOT NULL,
model VARCHAR(50),
registration_number VARCHAR(50) UNIQUE NOT NULL,
price_per_day DECIMAL(10,2) NOT NULL CHECK (price_per_day > 0),
availability_status VARCHAR(20)
CHECK (availability_status IN ('available', 'rented', 'maintenance'))
NOT NULL
); 


INSERT INTO vehicles 
(name, type, model, registration_number, price_per_day, availability_status) 
VALUES
('Toyota Corolla', 'car', '2021', 'CAR-1001', 50.00, 'available'),
('Honda Civic', 'car', '2020', 'CAR-1002', 55.00, 'rented'),
('Ford Ranger', 'truck', '2019', 'TRK-2001', 80.00, 'available'),
('Yamaha R15', 'bike', '2022', 'BIK-3001', 30.00, 'available'),
('Suzuki Gixxer', 'bike', '2021', 'BIK-3002', 28.00, 'maintenance'),
('Nissan Sunny', 'car', '2018', 'CAR-1003', 45.00, 'available'),
('Isuzu D-Max', 'truck', '2020', 'TRK-2002', 85.00, 'rented'),
('BMW X5', 'car', '2022', 'CAR-1004', 120.00, 'available'),
('Kawasaki Ninja', 'bike', '2023', 'BIK-3003', 40.00, 'available'),
('Tesla Model 3', 'car', '2023', 'CAR-1005', 150.00, 'available');



-- Bookings Table
CREATE TABLE bookings (
booking_id SERIAL PRIMARY KEY,
user_id INT NOT NULL references users(user_id),
vehicle_id INT NOT NULL references vehicles(vehicle_id),
start_date DATE NOT NULL,
end_date DATE NOT NULL,
booking_status VARCHAR(20)
CHECK (booking_status IN ('pending', 'confirmed', 'completed', 'cancelled'))
NOT NULL,
total_cost DECIMAL(10,2) NOT NULL CHECK (total_cost >= 0)
);


INSERT INTO bookings
(user_id, vehicle_id, start_date, end_date, booking_status, total_cost)
VALUES
(1, 1, '2024-01-01', '2024-01-05', 'completed', 200.00),
(2, 2, '2024-01-03', '2024-01-06', 'confirmed', 165.00),
(3, 3, '2024-01-05', '2024-01-08', 'completed', 240.00),
(4, 4, '2024-01-07', '2024-01-09', 'completed', 60.00),
(5, 6, '2024-01-10', '2024-01-15', 'confirmed', 225.00),
(6, 1, '2024-01-12', '2024-01-14', 'completed', 100.00),
(7, 8, '2024-01-15', '2024-01-18', 'pending', 360.00),
(8, 9, '2024-01-18', '2024-01-20', 'confirmed', 80.00),
(1, 10, '2024-01-20', '2024-01-22', 'pending', 300.00),
(2, 1, '2024-01-25', '2024-01-28', 'completed', 150.00);


SELECT
  b.booking_id,
  u.name AS customer_name,
  v.name AS vehicle_name,
  b.total_cost
FROM bookings as b
INNER JOIN users as u
  ON b.user_id = u.user_id
INNER JOIN vehicles as v
  ON b.vehicle_id = v.vehicle_id;



SELECT
  v.vehicle_id,
  v.name,
  v.type,
  v.registration_number
FROM vehicles as v
WHERE NOT EXISTS (
  SELECT *
  FROM bookings as b
  WHERE b.vehicle_id = v.vehicle_id
); 


SELECT
  vehicle_id,
  name,
  model,
  price_per_day,
  availability_status
FROM vehicles
WHERE availability_status = 'available'
  AND type = 'car'; 


SELECT
  v.vehicle_id,
  v.name AS vehicle_name,
  COUNT(b.booking_id) AS total_bookings
FROM vehicles as v
INNER JOIN bookings as b
  ON v.vehicle_id = b.vehicle_id
GROUP BY v.vehicle_id, v.name
HAVING COUNT(b.booking_id) > 2;
