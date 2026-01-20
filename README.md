# Library Management System

A console-based Library Management System built with Core Java and Oracle Database. This application allows users to manage library books, members, and track book issuance/returns.

## Features

- **📚 Add Books** - Add new books with ISBN, name, description, author, subject, and available units
- **👥 Add Members** - Register new library members with ID, name, and join date
- **📖 Issue Books** - Issue a book to a member (tracks date of issue, prevents duplicate issuance)
- **🔄 Return Books** - Process book returns (updates return date and restores available units)

## Technologies Used

- **Language:** Java (Core Java)
- **Database:** Oracle XE
- **Database Connectivity:** JDBC
- **Build Tool:** Apache Ant

## Database Setup

### Prerequisites
- Oracle Database XE installed and running on `localhost:1522`
- User credentials: `scott/tiger` (can be modified in `src/DBProperties`)

### Create Tables

Run the following SQL scripts in your Oracle database:

```sql
-- Members table
CREATE TABLE members (
    member_id NUMBER(10),
    member_name VARCHAR2(100),
    doj DATE
);

-- Books table
CREATE TABLE books (
    isbn_code VARCHAR2(50),
    book_name VARCHAR2(50),
    book_desc VARCHAR2(1000),
    author_name VARCHAR2(100),
    subject_name VARCHAR2(100),
    units_available NUMBER(5)
);

-- Member-Book Record table (for tracking issuance)
CREATE TABLE member_book_record (
    rec_id NUMBER(18),
    member_id NUMBER(10),
    isbn_code VARCHAR2(50),
    doi DATE,
    dor DATE
);

-- Sequence for record IDs
CREATE SEQUENCE lib_seq START WITH 101 INCREMENT BY 1;
```

## Project Structure

```
CoreJavaProject/
├── src/
│   ├── UserMenu.java        # Main entry point with menu interface
│   ├── AddBookMenu.java     # Book addition functionality
│   ├── AddMemberMenu.java   # Member registration functionality
│   ├── LibFunctions.java    # Issue and return book operations
│   ├── LibUtil.java         # Database utility class
│   ├── Book.java            # Book model class
│   ├── Member.java          # Member model class
│   └── DBProperties         # Database configuration file
├── build/
│   └── classes/             # Compiled class files
├── build.xml                # Ant build configuration
├── CreateTableScript.txt    # SQL scripts for table creation
└── README.md
```

## How to Run

### Using Command Line

1. **Compile the project:**
   ```bash
   cd src
   javac -d ../build/classes *.java
   ```

2. **Run the application:**
   ```bash
   cd ../build/classes
   java UserMenu
   ```

### Using Apache Ant

```bash
ant build
ant run
```

## Configuration

Database connection settings can be modified in `src/DBProperties`:

```properties
DBDriver=oracle.jdbc.driver.OracleDriver
DBName=jdbc:oracle:thin:@localhost:1522:xe
User=scott
Password=tiger
```

## Usage

When you run the application, you'll see the following menu:

```
---------------------------------------------------------
Select the following options
Enter 1 for adding a book
Enter 2 for adding a member
Enter 3 for issuing a book
Enter 4 for returning a book
Enter 5 to exit
```

Simply enter the number corresponding to your desired action and follow the prompts.

## Author

testuser

## License

This project is open source and available for educational purposes.
