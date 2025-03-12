# PHP 8.2 FPM Custom Docker Project

This project provides a customized Docker image based on `php:8.2-fpm` with installed PHP extensions for working with web applications, databases, and additional tools. It also includes an example configuration for connecting to MySQL using Docker Compose.

## Requirements

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Installed PHP Extensions

- `mysqli`, `pdo_mysql`, `pdo_pgsql`, `pgsql` - for working with MySQL and PostgreSQL databases
- `bcmath`, `mbstring`, `xml`, `gd`, `exif`, `zip`, `soap`, `intl`, `xsl` - general utilities and data processing
- `pcntl`, `sockets`, `sysvmsg`, `sysvsem`, `sysvshm` - for process management and inter-process communication
- `opcache` - for performance optimization
- `imap`, `gmp` - additional utilities
- `xdebug` - for debugging
- `redis` - for working with Redis
- `apcu` - for caching
- `ssh2` - for SSH connections

## Project Structure
.
├── Dockerfile          # Docker image configuration for PHP
├── docker-compose.yml  # Configuration of services (PHP + MySQL)
├── public_html/        # Directory with your PHP code
└── README.md           # This file


## Installation and Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd <repository-name>
```
2. Configure Environment Variables
Create a .env file in the root directory and add the following variables:

DB_HOST=db
DB_USER=mysql
DB_PASS=mysql
DB_NAME=development

 OR
DB_HOST=db
DB_USER=root
DB_PASS=root
DB_NAME=development

3. Build and Run Containers
```bash
docker-compose up -d --build
```
-d - runs in the background

--build - rebuilds images if necessary

4. Check Status
```bash
docker ps
```
You should see two running containers: php_app and mysql-server.

5. Access the Application
Place your PHP code in the public_html/ directory.

Then open http://localhost in your browser.

Useful Commands
Stop containers:

docker-compose down

View PHP logs:
```bash
docker logs php_app
```
Access the PHP container:
```bash
docker exec -it php_app bash
```
Connect to MySQL:
```bash
docker exec -it mysql-server mysql -u root -p
```
OR
Open http://localhost:8080 in your browser.

Troubleshooting
Database Connection Error
If you encounter mysqli_sql_exception: No such file or directory:
Ensure the MySQL container is running:
```bash
docker ps
```
Verify the environment variables in .env.

Ensure your PHP code uses the correct connection parameters:
$conn = new mysqli(getenv('DB_HOST'), getenv('DB_USER'), getenv('DB_PASS'), getenv('DB_NAME'));

Build Error
If the build fails, check for the presence of all dependencies and internet access for downloading packages.
Additional Configuration
To add a web server (e.g., Nginx), include the corresponding service in docker-compose.yml.

Customize php.ini inside the container if needed:
```bash
docker cp custom-php.ini php_app:/usr/local/etc/php/php.ini
```
License
This project is distributed under the MIT License (or specify your own license).

### Notes
1. Add your code to the `public_html/` directory or adjust the path in `docker-compose.yml` based on your project structure.
2. Replace `<repository-url>` and `<repository-name>` with the actual details of your repository if it’s hosted on GitHub or another service.
3. Use real values in `.env` for `DB_PASS` and `DB_NAME`.
4. If you’re using a different web server (e.g., Nginx), add instructions for its setup.

Let me know if you need further adjustments or additional details!






