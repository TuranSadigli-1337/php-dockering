PHP Docker Web Application

**INTRODUCTION**

This is a simple PHP web application running in a Dockerized environment, designed to demonstrate a basic web stack with PHP, MySQL, and phpMyAdmin. The application connects to a MySQL database and displays records from a table in a web browser.

Project Structure

php_docker_table.sql – SQL dump to create and populate the database table.
docker-compose.yml – Docker Compose configuration to set up the web stack.
index.php – Main PHP script to fetch and display data from the database.
test.php – Simple PHP test script.
Quick Start

1. Clone and Navigate

```
git clone <your-repo-url>
cd <your-project-folder>
```

2. Start the Application
   
``` docker-compose up -d ```

This will start three services:

MySQL database (db)
PHP + Apache web server (www)
phpMyAdmin (phpmyadmin)
3. Access the Application

```
Web App: http://localhost
Displays data from php_docker_table.
phpMyAdmin: http://localhost:8001
Use credentials:
Server: db
Username: php_docker
Password: password
```

4. Stop the Application
``` docker-compose down ```

**Database Details**

``Database name: php_docker``

``Table: php_docker_table``

``Columns: id, name, age, creation_date``

The SQL file automatically creates the table and inserts sample data when the db container starts.


File Descriptions: ``docker-compose.yml``

Defines three services:

``db: MySQL with persistent volume for initial SQL scripts.``

``www: PHP Apache server mapping local files to /var/www/html.``

``phpmyadmin: Admin interface for MySQL.``

Connects to the database and displays all records from php_docker_table.

**NOTES:**

The database is persisted via Docker volumes.
The web server serves files from the current directory.
phpMyAdmin is accessible on port 8001 for easy database management.

Troubleshooting

If the web page shows no data:

Check if the database container is running:

```docker ps```

Verify the SQL was imported:

```docker exec -it <db-container-id> mysql -u php_docker -p php_docker```

Then run:

```SELECT * FROM php_docker_table;```

Reset Everything

To completely reset the environment (removes containers, volumes, and networks):

```docker-compose down -v```
```docker system prune -f```


