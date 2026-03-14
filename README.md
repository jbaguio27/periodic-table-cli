# Periodic Table CLI

A Bash command line application that retrieves element information from a PostgreSQL periodic table database.

The program accepts an atomic number, element symbol, or element name and returns detailed information about that element including type, atomic mass, melting point, and boiling point.

## Features

• Query element by atomic number  
• Query element by symbol  
• Query element by element name  
• Connects to a PostgreSQL database  
• Clean CLI output for quick lookup  
• Handles missing arguments and invalid elements

## Tech Stack

• Bash  
• PostgreSQL  
• SQL

## Project Structure


periodic_table
│
├── element.sh
└── README.md


## Database Tables

This project uses three tables.

### elements
Stores basic element identifiers.

Columns:
- atomic_number (Primary Key)
- symbol
- name

### properties
Stores physical properties of each element.

Columns:
- atomic_number (Foreign Key)
- atomic_mass
- melting_point_celsius
- boiling_point_celsius
- type_id

### types
Stores the element classification.

Columns:
- type_id (Primary Key)
- type

## Setup

### 1. Clone the repository


git clone https://github.com/yourusername/periodic-table-cli.git

cd periodic-table-cli


### 2. Make the script executable


chmod +x element.sh


### 3. Make sure PostgreSQL is installed

The project expects a database named:


periodic_table


with the required tables and data.

## Usage

Run the script with an element identifier.

### No argument


./element.sh


Output


Please provide an element as an argument.


### Query by atomic number


./element.sh 1


Output


The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.


### Query by symbol


./element.sh H


### Query by name


./element.sh Hydrogen


### Invalid element


./element.sh Unknown


Output


I could not find that element in the database.


## Example Query Logic

The script joins three tables to retrieve element details.


SELECT e.atomic_number, e.name, e.symbol, t.type,
p.atomic_mass, p.melting_point_celsius, p.boiling_point_celsius
FROM elements e
JOIN properties p USING(atomic_number)
JOIN types t USING(type_id);


## Learning Goals

This project demonstrates:

• Bash scripting for CLI applications  
• SQL queries with JOIN operations  
• Database normalization  
• Working with PostgreSQL from a shell script  
• Git version control and commit history

## License

This project is open for educational use.
