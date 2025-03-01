# ML_COURSERA
Repository for Andrew NG's course on coursera.


# Database Systems Concepts and Architecture - Comprehensive Revision Sheet

## 1. Core Database Concepts

### Data Models and Abstraction

- **Data Abstraction**: Suppression of details of data organization and storage while highlighting essential features for improved understanding. Allows different users to perceive data at their preferred levels of detail.

- **Data Model**: A collection of concepts describing the structure (data types, relationships, constraints) of a database. Includes:
  - Basic operations for specifying retrievals and updates
  - Dynamic aspects/behavior of database applications
  - User-defined operations on database objects (e.g., COMPUTE_GPA for a STUDENT object)

### Types of Data Models

- **Conceptual Data Model**: High-level concepts close to user perception of data. Uses entities, attributes, and relationships.

- **Physical Data Model**: Low-level concepts describing storage details. Used by specialists and contains information about formats, record orderings, access paths, etc.

- **Representational (Implementation) Data Model**: Provides concepts understandable by end users but not too far from storage organization. Hides storage details but can be implemented directly.
  - Examples: Relational data model, network data model, hierarchical data model
  - New models include "self-describing data models" combining data description with values

### Key Entities and Relationships

- **Entity**: Represents a real-world object, concept, or project described in the database (e.g., employee).

- **Attribute**: Property of interest that further describes an entity (e.g., employee's name).

- **Relationship**: Association between two or more entities (e.g., "works-on" relationship between employee and project).

- **Object Data Model**: Higher-level implementation data model closer to conceptual models.

### Access Methods

- **Access Path**: Search structure for efficiently searching database records (e.g., indexing, hashing).

- **Index**: Access path allowing direct data access using an index term or keyword (similar to a book index), organized in linear, hierarchical, or tree structure format.

## 2. Schemas, Instances and Database State

- **Database Schema** (scheme or intension): Description of the database specified during design and not expected to change frequently. Changes (schema evolution) are required when the DB application changes.

- **Schema Diagram**: Visual display of a database schema.

- **Database State** (snapshot or extension): The data in the database at a particular moment in time. Also called the current set of occurrences or instances.

- **Schema Construct**: In a given DB state, each schema construct has its own current set of instances.

- **Database Initialization**: 
  - New DB definition requires schema specification, with the DB initially in empty state
  - When DB is populated/loaded with data, its initial state is obtained
  - Each insert/delete/change operation creates a new state
  - At any point, the DB has a current state/snapshot/instance

## 3. Three-Schema Architecture and Data Independence

### Characteristics of the Database Approach

1. Use of catalog to store schema
2. Insulation of program and data (program-data and program-operation independence)
3. Support of multiple user views

### Three Schema Levels

1. **Internal Level (Internal Schema)**: Describes physical storage structure using a physical data model, including details of data storage and access paths.

2. **Conceptual Level (Conceptual Schema)**: Describes the structure of the whole database, hiding physical storage details and focusing on entities, data types, relationships, user operations, and constraints.

3. **External Level (External Schemas/User Views)**: Multiple schemas describing parts of the DB relevant to particular user groups, hiding the rest. Usually implemented using a representational data model.

- **Important Note**: The three schemas are only descriptions of data; actual data is stored at the physical level.

- **Mapping**: The process of transforming requests and results between schema levels.

### Data Independence

1. **Logical Data Independence**: Ability to change the conceptual schema without changing external schemas (application programs).
   - Examples: Adding record types/data items, changing constraints, removing records
   - Only view and mapping need changes
   - Application programs referencing external schema constructs must work as before

2. **Physical Data Independence**: Ability to change the internal schema without changing the conceptual schema (and thus external schemas remain unchanged).
   - Examples: Reorganizing files, creating additional access structures for performance improvement
   - Physical data details (location, storage encoding, compression, etc.) remain hidden from users

- **Key Principle**: Data independence occurs because when a schema changes at one level, the schema at the next higher level remains unchanged; only the mapping between levels changes.

## 4. Database Languages and Interfaces

### Database Languages

- **Data Definition Language (DDL)**: Used by database administrators and designers to define conceptual and internal schemas and their mapping.
  - Processed by DDL compiler which stores schema descriptions in DBMS catalog

- **Storage Definition Language (SDL)**: Used to specify the internal schema in DBs with separate conceptual and internal schema levels.
  - Modern RDBMS have no specific SDL; internal schema is specified through functions, parameters, and storage specifications

- **View Definition Language (VDL)**: Used to specify user views and their mappings to the conceptual schema.
  - In most DBMSs, DDL defines both conceptual and external schemas
  - Example: SQL is used as VDL to define user views

- **Data Manipulation Language (DML)**: Used to manipulate database operations (retrieval, insertion, deletion, modification).
  - **High-level/Nonprocedural DML**: Specifies operations as statements interactively or through programming languages
    - Set-at-a-time or set-oriented
    - Example: SQL retrieving multiple records in a single statement
  
  - **Low-level/Procedural DML**: Embedded in programming languages, processes individual records through loops
    - Record-at-a-time DMLs

- **Structured Query Language (SQL)**: Comprehensive integrated language including DDL, VDL, and DML constructs.

- **Host Language**: Programming language in which DML commands are embedded.

- **Data Sublanguage**: DML embedded in a host language.

- **Query Language**: High-level DML used in standalone interactive manner.

### User Interfaces

#### For Naive/Parametric/Casual Users
- **Menu-based interfaces**: Lists of options guiding users through request formulation
- **Mobile device apps**: Limited menu options for specific services
- **Forms-based interfaces**: Forms for naive users (e.g., Oracle Forms)
- **Graphical User Interfaces (GUIs)**: Diagrammatic schema presentation
- **Natural language interfaces**: Accept requests in natural language
- **Keyword-based DB search**: Similar to web search engines
- **Speech input/output**: Applications with limited vocabularies

#### For Parametric Users
- Interfaces designed for routine operations with abbreviated commands

#### For Database Administrators
- Privileged commands for account creation, system parameter setting, authorization granting, schema changes, storage reorganization, etc.

## 5. Database System Environment

### DBMS Component Modules

#### Top Part (User Interfaces)
- **DBA Interface**: For database definition and tuning using DDL
- **DDL Compiler**: Processes schema definitions and stores metadata in DBMS catalog
- **Interactive Query Interface**: For casual users needing information
- **Query Compiler**: Parses and validates query correctness
- **Query Optimizer**: Rearranges operations, eliminates redundancies, selects efficient algorithms
- **Application Programs**: Written in host languages (C, C++, Java, PHP, Python)
- **Precompiler**: Extracts DML commands from application programs

#### Bottom Part (Processing)
- **Runtime Database Processor**: Executes privileged commands, query plans, transactions
- **Stored Data Manager**: Uses OS services for I/O operations
- **Client Programs/Computers**: Access data from DB servers or through application servers

### Database System Utilities

1. **Loading**: Converts and loads existing data files into the database
2. **Backup**: Creates backup copies for disaster recovery, including incremental backups
3. **Database Storage Reorganization**: Reorganizes files and creates new access paths
4. **Performance Monitoring**: Provides statistics for optimization decisions

**Other utilities**: Sorting files, data compression, user access monitoring, network interfacing

### Additional Tools and Environments

- **CASE** (Computer Aided Software Engineering)
- **Data Dictionary**: Stores catalog information, design decisions, usage standards, etc.
- **Application Development Environments**: For database application development, design, GUI development, etc.
- **Communication Software**: Enables remote database access through networks

## 6. Client/Server Architectures

### Centralized DBMS Architecture

- Most users access DBMS through terminals/devices with display capabilities but limited processing power
- All processing occurs on a remote system housing the DBMS
- Only display information and controls are sent to terminals through communication channels

### Two-Tier Client/Server Architecture

- **Client**: User machine providing interface capabilities and local processing
- **Server**: System providing services to clients (file access, printing, database services, etc.)
- In RDBMS, query and transaction functionality reside on the server side
- Client programs establish connection to servers through ODBC (Open Database Connectivity) or APIs
- Client programs can connect to multiple RDBMS servers

### Three-Tier Client/Server Architecture

- Adds an intermediate layer between client and database server
- **Intermediate/Middle Layer**: Application server or Web server that:
  - Handles rules and constraints
  - Verifies client credentials
  - Forwards requests to the database server
  - Passes partially processed data from DB server to clients
- Three tiers: user interface, application rules, data access
- Sometimes further divided into n-tier architectures (n = 4 or 5)
- Uses data compression technologies for encrypted data transfer

## 7. Classification of DBMS

### By Data Model
- **Relational Data Model (DM)**: Represents DB as collection of tables/files; uses SQL
- **Object DM**: Defines DB in terms of objects, properties, and operations
- **Big Data Systems**:
  - Key-value DM: Associates unique keys with records for fast access
  - Document DM: Stores data as documents (based on JSON)
  - Graph DM: Stores objects as graph nodes and relationships as edges
  - Column-based DM: Clusters columns on disk pages for fast access
- **Hierarchical DM**: Represents data as hierarchical tree structures
- **Network DM**: Represents data as record types and limited 1:N relationships
- **XML Model**: Standard for web data exchange using hierarchical tree structures

### By Other Criteria
- **Users**: Single vs. Multiple
- **Sites**: Centralized vs. Distributed (Homogeneous, Heterogeneous, Federated)
- **Cost**: Free/Open Source vs. Proprietary
- **Access Path**: Various types (e.g., inverted file structure)
- **Purpose**: General vs. Special
