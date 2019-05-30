DROP TABLE IF EXISTS bus;

CREATE TABLE bus( 
id SERIAL PRIMARY KEY,
mac VARCHAR(30) NOT NULL UNIQUE,
route int NOT NULL,
latitude numeric(10,6) NOT NULL,
longitude numeric(10,6) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP);