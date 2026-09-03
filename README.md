Bases de Datos I (INF322) - SQL Implementation
==============================================

A comprehensive educational project for **INF322 - Bases de Datos I** at UAGRM (Universidad Autónoma Gabriel René Moreno), focused on fundamental concepts of relational databases and SQL.

📋 Overview
-----------

This repository provides clean, practical implementations of database concepts using **SQL Server / MariaDB**. It is designed as a learning resource to understand the internal mechanics of relational models, normalization, and query design.

 🚀 GOOGLE COLAB
-----------------------------

*   **[Google Colab for SQL practice](https://colab.research.google.com/drive/1ARAIzmY_CVT8On6VRrI9u3qDAfbIgoGK?usp=sharing)**    

📘 EXERCICES - HOMEWORK
-----------------------

- 📝 **[UNIDAD 1 - Interview and conceptual design](https://github.com/vladimuji/uagrm_comp_science_sem05_inf312/blob/unit_1_interview_and_uml_diagram/unit_1/README.md)**

- 📝 **[UNIDAD 2 - Logical design](https://github.com/vladimuji/uagrm_comp_science_sem05_inf312/blob/unit_2_conceptual_design/unit_2/README.md)**
    

📁 Project Structure
--------------------

```
00-code/  
├── assets/  
│   └── img/  
│       └── 002-empresa-logistica-carga.png     # Captura del diagrama StarUML  
├── unit_1/  
│   └── README.md                               # Documentación y requerimientos de la Unidad 1  
├── LICENSE                                     # Licencia del proyecto  
└── README.md                                   # README principal del repositorio  

```

🗄️ Database Concepts
---------------------

### Features

*   **Relational Model**: Entities, attributes, and relationships
    
*   **Normalization**: Up to 3NF for clean schema design
    
*   **Constraints**: Primary keys, foreign keys, unique, check
    
*   **SQL Queries**: From basic SELECT to advanced joins
    

### Example

sql
```
-- Create a Students table  
CREATE TABLE Students (      
    id INT PRIMARY KEY,      
    name VARCHAR(50),      
    email VARCHAR(100) UNIQUE  
    );

-- Insert sample data 
INSERT INTO Students (id, name, email)  VALUES (1, 'Ana', 'ana@mail.com'),         
    (2, 'Luis', 'luis@mail.com');

-- Query data  
SELECT name, email 
FROM Students WHERE id = 1;   
```

📊 Topics Covered
-----------------

*   Relational schema design
    
*   Normalization (1NF, 2NF, 3NF)
    
*   SQL queries (SELECT, INSERT, UPDATE, DELETE)
    
*   Joins and subqueries
    

🛠️ Technologies
----------------

*   **DBMS**: SQL Server / MariaDB
    
*   **Language**: SQL
    
*   **Tools**: SSMS, Termux, Google Colab (with SQLite/MariaDB)
    

📚 Standards & Best Practices
-----------------------------

The project emphasizes:

*   Proper schema design
    
*   Clear naming conventions
    
*   Normalization for data integrity
    
*   Clean query organization
    

🚀 Getting Started
------------------

### Prerequisites

*   SQL Server / MariaDB installed
    
*   Basic knowledge of relational algebra
    

### Usage

sql

```
-- Load schema  SOURCE schema/create_tables.sql;  -- Run queries  SOURCE queries/basic_queries.sql;
```

📖 Course Information
---------------------

*   **Course**: INF322 - Bases de Datos I
    
*   **Institution**: UAGRM (Universidad Autónoma Gabriel René Moreno)
    
*   **Semester**: 5th Semester
    
*   **Author**: Vladimir Mújica
    

📝 Notes
--------

This is an educational project focused on:

*   Understanding relational database fundamentals
    
*   Practicing SQL queries
    
*   Building strong foundations for advanced database courses
    

📄 License
----------

Educational project for academic purposes.