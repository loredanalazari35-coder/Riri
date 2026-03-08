The goal of this project is to use Python and PostgreSQL to automate the establishment of a data warehouse ingestion layer. The program breaks the whole workflow down into multiple reusable functions, each of which does a different job.

The first thing to do is to connect to the PostgreSQL server. The check_postgres() function connects to the system's default database and gets information about the current session, like the name of the database, the active user, and the version of the server. This step is a short check of the system to make sure the connection settings are correct.

After confirming that the connection is working, the code moves on to set up the warehouse environment. The ensure_database() function checks to see if there is already a database called DWH. The function doesn't just create the database, it first checks PostgreSQL's internal metadata to see if it already exists. It makes the database automatically if it isn't there. So running the code more than once won't produce any duplicate objects.

The next step is to work on the structure. The software makes a schema called ingestion inside the warehouse database using the ensure_schema() function. The ingestion schema is a specific place where raw data from source systems is stored. This approach is in line with standard data warehouse procedures, which say that incoming data should be stored independently before being transformed or modeled.

After the schema is ready, the code lists the tables that need to be made to hold the new datasets. The ensure_tables() method runs SQL commands that construct six tables that show data sources for CRM and ERP. The structure of each table matches the fields in the CSV files that will be imported later.

The upload_files() method takes care of data ingestion. This version uses a helper function called copy_into_table() to do the COPY operation instead of writing the same code for each dataset. This makes the code cleaner and easier to work with. The program reads each CSV file and sends its information directly to the right database table.

The code ends with a validation step in check_loaded_data() to make sure that the data was loaded successfully. This function counts how many rows are in each table and then prints the results. The user can make sure that the ingestion procedure worked by comparing these counts to the source files.

In conclusion, this code breaks the ingestion process down into smaller parts: server verification, warehouse preparation, schema creation, table formation, file ingestion, and post-load validation. This modular approach makes the code easier to read and makes it easier to add new features or reuse it in future data engineering projects.
