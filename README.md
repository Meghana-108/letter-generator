1. Project Overview

The Letter Automation System allows users to generate formal and informal letters automatically. Users can log in, choose a letter type from the dashboard, fill a dynamic form, and generate a structured letter. All user inputs and generated letters are stored in a database for future access.

This system reduces repetitive manual writing and ensures consistent formatting.

2. Features
User Features

Secure login system

Dashboard displaying multiple letter types

Dynamic forms for each letter type

Auto-generated letter in a formatted structure

Print-ready output

User-specific letter history

View previously generated letters

Admin Features (if included)

View user statistics

Manage templates

Track generated letters

3. System Architecture
Frontend

Static pages created using HTML, CSS, and JavaScript

Separate pages for each letter type

AJAX/Fetch API calls to backend

Client-side validation

Backend

Node.js with Express.js

RESTful API structure

Session handling for user authentication

Template processing (placeholder replacement)

Database operations

Database

MySQL relational database

Stores user info, templates, user inputs, and generated letters

4. Technology Stack

Frontend:
HTML, CSS, JavaScript

Backend:
Node.js, Express.js

Database:
MySQL

Tools:
Git, GitHub, VS Code

5.SQL Queries

USE letter_generator_dbms;

CREATE TABLE invitation_letter(

LETTERID INT auto_increment PRIMARY KEY,

USERID int ,

SENDERADDRESS varchar(100),

LETTER_DATE date,

RECEIVERNAME VARCHAR(100),

EVENTTYPE VARCHAR(100),

EVENTDATE date,

EVENTVENUE VARCHAR(100),

SENDERNAME VARCHAR(100), 

constraint foreign key(USERID) references USER_DETAILS(USERID) ON DELETE CASCADE

);

CREATE TABLE birthday_wish(

LETTERID INT auto_increment PRIMARY KEY,

USERID int ,

SENDERADDRESS varchar(100),

LETTER_DATE date

RECEIVERNAME VARCHAR(100),

SENDERNAME VARCHAR(100),

constraint foreign key(USERID) references USER_DETAILS(USERID)

);

CREATE TABLE congratulations_letter(

LETTERID INT auto_increment PRIMARY KEY,

USERID int,

SENDERADDRESS varchar(100),

LETTER_DATE date,

RECEIVERNAME VARCHAR(100),

REASON VARCHAR(1000),

SENDERNAME VARCHAR(100),

CONSTRAINT FOREIGN KEY(USERID) REFERENCES USER_DETAILS(USERID) ON DELETE CASCADE
);

CREATE TABLE leave_letter(

LETTERID INT auto_increment PRIMARY KEY,

USERID int,

SENDERADDRESS varchar(100),

LETTER_DATE date,

RECIPIENTNAME VARCHAR(255),

RECIPIENTDESIGNATION varchar(100),

ORGANIZATIONNAME varchar(100),

ORGANIZATIONADDRESS varchar(100),

STARTDATE date, 

ENDDATE date,

REASON VARCHAR(1000),

SENDERNAME VARCHAR(100),

CONTACTDETAILS INT,

CONSTRAINT FOREIGN KEY(USERID) REFERENCES USER_DETAILS(USERID) ON DELETE CASCADE

);

DROP TABLE leave_letter;

DROP TABLE invitation_letter;

SELECT * FROM invitation_letter;

SELECT * FROM user_details;

desc user_details;

SELECT * FROM leave_letter;

SELECT COUNT(*) AS Total_Letters

FROM (

    SELECT LETTERID FROM invitation_letter
    
    UNION ALL
    
    SELECT LETTERID FROM birthday_wish
    
    UNION ALL
    
    SELECT LETTERID FROM congratulations_letter
    
    UNION ALL
    
    SELECT LETTERID FROM leave_letter
    
) AS all_letters;


CREATE TABLE letter_logs (

    LOGID INT AUTO_INCREMENT PRIMARY KEY,
    
    LETTERID INT,
    
    USERID INT,
    
    LETTER_TYPE VARCHAR(50),
    
    OPERATION_DATE DATETIME DEFAULT CURRENT_TIMESTAMP
    
);



DELIMITER $$


CREATE TRIGGER log_invitation_letter_insert

AFTER INSERT ON invitation_letter

FOR EACH ROW

BEGIN

    INSERT INTO letter_logs (LETTERID, USERID, LETTER_TYPE)
    
    VALUES (NEW.LETTERID, NEW.USERID, 'Invitation Letter');
    
END$$


DELIMITER ;


DELIMITER $$


CREATE TRIGGER log_birthday_wish_insert

AFTER INSERT ON birthday_wish

FOR EACH ROW

BEGIN

    INSERT INTO letter_logs (LETTERID, USERID, LETTER_TYPE)
    
    VALUES (NEW.LETTERID, NEW.USERID, 'Birthday Wish');
    
END$$


DELIMITER ;



DELIMITER $$


CREATE TRIGGER log_congratulations_letter_insert

AFTER INSERT ON congratulations_letter

FOR EACH ROW

BEGIN

    INSERT INTO letter_logs (LETTERID, USERID, LETTER_TYPE)
    
    VALUES (NEW.LETTERID, NEW.USERID, 'congratulations letter');
    
END$$


DELIMITER ;


DELIMITER $$


CREATE TRIGGER log_leave_letter_insert

AFTER INSERT ON leave_letter

FOR EACH ROW

BEGIN

    INSERT INTO letter_logs (LETTERID, USERID, LETTER_TYPE)
    
    VALUES (NEW.LETTERID, NEW.USERID, 'leave letter');
    
END$$


DELIMITER ;


DELETE FROM invitation_letter;

DELETE FROM birthday_wish;

DELETE FROM congratulations_letter;

delete FROM leave_letter;


TRUNCATE TABLE invitation_letter;

select * from invitation_letter;

truncate table birthday_wish;

truncate TABLE congratulations_letter;

truncate table leave_letter;


select * from letter_logs;

select * from user_details;


