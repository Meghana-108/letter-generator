Letter Automation System
Overview

The Letter Automation System is a full-stack web application that allows users to generate different types of letters automatically using predefined templates and user-provided inputs.
The system reduces manual effort by generating clean, structured, and print-ready letters.

Users can log in, select a letter type, fill a form, generate a formatted letter, and view their history.

Features
User Authentication

Secure login

Session management

User-specific data handling

Letter Types Dashboard

Multiple categories such as:

Birthday Wish

Congratulations

Invitation

Leave Letter

Each type opens its own input form

Template-Based Letter Generation

Templates stored in the database

Backend replaces placeholders with user inputs

Automatically generates a clean formatted letter

User Input Handling

Inputs captured for each letter type

Data stored for history tracking

Generated Letter

Displays final formatted content

Option to print

Stored in database for future reference

History Page
--------------------------------------------------------------------------------------------
Project Architecture
Frontend

HTML

CSS

JavaScript

Separate pages for each letter type, dashboard, history, and generated output

Backend

Node.js

Express.js

Routes for authentication, fetching templates, processing user input, and saving letters

Database

MySQL
View all previously generated letters

Revisit or reprint any letter
