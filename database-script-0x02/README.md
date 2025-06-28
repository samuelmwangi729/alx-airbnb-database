-- USERS
INSERT INTO User (user_id, first_name, last_name, email, password_hash, phone_number, role, created_at)
VALUES
('11111111-1111-1111-1111-111111111111', 'Alice', 'Johnson', 'alice@example.com', 'hashedpassword1', '1234567890', 'guest', CURRENT_TIMESTAMP),
('22222222-2222-2222-2222-222222222222', 'Bob', 'Smith', 'bob@example.com', 'hashedpassword2', '0987654321', 'host', CURRENT_TIMESTAMP),
('33333333-3333-3333-3333-333333333333', 'Carol', 'Admin', 'admin@example.com', 'hashedpassword3', '1122334455', 'admin', CURRENT_TIMESTAMP);

-- PROPERTIES
INSERT INTO Property (property_id, host_id, name, description, location, pricepernight, created_at, updated_at)
VALUES
('aaaaaaa1-aaaa-aaaa-aaaa-aaaaaaaaaaaa', '22222222-2222-2222-2222-222222222222', 'Seaside Villa', 'A beautiful villa by the sea.', 'Mombasa, Kenya', 120.00, CURRENT_TIMESTAMP, CURRENT_TIMESTAMP),
('aaaaaaa2-aaaa-aaaa-aaaa-aaaaaaaaaaaa', '22222222-2222-2222-2222-222222222222', 'Mountain Retreat', 'Cozy cabin in the mountains.', 'Nakuru, Kenya', 85.00, CURRENT_TIMESTAMP, CURRENT_TIMESTAMP);

-- BOOKINGS
INSERT INTO Booking (booking_id, property_id, user_id, start_date, end_date, status, created_at)
VALUES
('bbbbbbb1-bbbb-bbbb-bbbb-bbbbbbbbbbbb', 'aaaaaaa1-aaaa-aaaa-aaaa-aaaaaaaaaaaa', '11111111-1111-1111-1111-111111111111', '2025-07-01', '2025-07-05', 'confirmed', CURRENT_TIMESTAMP),
('bbbbbbb2-bbbb-bbbb-bbbb-bbbbbbbbbbbb', 'aaaaaaa2-aaaa-aaaa-aaaa-aaaaaaaaaaaa', '11111111-1111-1111-1111-111111111111', '2025-08-15', '2025-08-20', 'pending', CURRENT_TIMESTAMP);

-- PAYMENTS
INSERT INTO Payment (payment_id, booking_id, amount, payment_date, payment_method)
VALUES
('ccccccc1-cccc-cccc-cccc-cccccccccccc', 'bbbbbbb1-bbbb-bbbb-bbbb-bbbbbbbbbbbb', 480.00, CURRENT_TIMESTAMP, 'credit_card');

-- REVIEWS
INSERT INTO Review (review_id, property_id, user_id, rating, comment, created_at)
VALUES
('ddddddd1-dddd-dddd-dddd-dddddddddddd', 'aaaaaaa1-aaaa-aaaa-aaaa-aaaaaaaaaaaa', '11111111-1111-1111-1111-111111111111', 5, 'Fantastic stay at the seaside villa!', CURRENT_TIMESTAMP),
('ddddddd2-dddd-dddd-dddd-dddddddddddd', 'aaaaaaa2-aaaa-aaaa-aaaa-aaaaaaaaaaaa', '11111111-1111-1111-1111-111111111111', 4, 'Beautiful location, very quiet.', CURRENT_TIMESTAMP);

-- MESSAGES
INSERT INTO Message (message_id, sender_id, recipient_id, message_body, sent_at)
VALUES
('eeeeeee1-eeee-eeee-eeee-eeeeeeeeeeee', '11111111-1111-1111-1111-111111111111', '22222222-2222-2222-2222-222222222222', 'Hi, is your property available for next weekend?', CURRENT_TIMESTAMP),
('eeeeeee2-eeee-eeee-eeee-eeeeeeeeeeee', '22222222-2222-2222-2222-222222222222', '11111111-1111-1111-1111-111111111111', 'Yes, it is available. Looking forward to hosting you!', CURRENT_TIMESTAMP);
