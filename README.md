CREATE TABLE aid_requests (
    request_id SERIAL PRIMARY KEY, 
    user_id INT NOT NULL REFERENCES users(user_id) ON DELETE CASCADE,
    event_id INT NOT NULL REFERENCES event_locations(event_id),
    aid_type_id INT NOT NULL REFERENCES aid_types(aid_type_id),
    family_size INT NOT NULL,
    status VARCHAR(50) NOT NULL CHECK (status IN ('Pending', 'In Progress', 'Fulfilled')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

INSERT INTO aid_requests (user_id, event_id, aid_type_id, family_size, status) 
VALUES (5, 2, 3, 6, 'In Progress');

SELECT * 
FROM aid_requests 
WHERE status = 'Pending' 
ORDER BY created_at DESC;

UPDATE aid_requests 
SET status = 'Fulfilled', updated_at = CURRENT_TIMESTAMP 
WHERE request_id = 1;

DELETE FROM aid_requests WHERE request_id = 1;

SELECT * FROM public.aid_requests
ORDER BY request_id ASC 
