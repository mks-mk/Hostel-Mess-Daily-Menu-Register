# Hostel Mess Daily Menu Register

A Java application for viewing and managing a hostel's weekly mess menu. It includes a desktop interface built with Swing and a web interface served by the application.

## What It Does

- Shows the menu by day and meal, with dish search.
- Provides an admin interface to add, edit, and delete menu items.
- Stores menu data in MySQL or SQLite through JDBC.
- Runs as a desktop application and includes a built-in web server.

## Requirements

- Java Development Kit (JDK) 17 or later.
- Windows to use the included `.bat` launch scripts.
- MySQL is optional. The application uses the bundled SQLite driver if it cannot connect to MySQL.

## Run on Windows

From the project directory, run one of these:

```bat
run.bat
```

Starts the desktop application. The built-in web server also starts on port `8080`.

```bat
run_web_browser.bat
```

Starts the application and opens the web menu in your browser. The public menu is at [http://localhost:8080/](http://localhost:8080/); the admin page is at [http://localhost:8080/admin](http://localhost:8080/admin).

Alternatively, run the PowerShell launcher:

```powershell
.\run.ps1
```

## Database

Database settings are in `db.properties`. The checked-in configuration selects MySQL at `localhost:3306`, using database `hostel_mess_db` and the default `root` account with no password. If the MySQL connection fails, the application falls back to SQLite and creates `hostel_mess.db` in the working directory. Set `db.type=sqlite` to select SQLite directly.

On startup, the application creates its tables. It inserts the sample menu when the menu table is empty.

## Admin Access

The current demo credentials are:

- Username: `admin@gmail.com`
- Password: `admin123`

These credentials are stored in the application source and are not suitable for a public deployment. Change the authentication implementation before exposing the admin interface to untrusted users.

## Docker

The included `Dockerfile` builds and runs the web server in headless mode:

```sh
docker build -t hostel-mess .
docker run --rm -p 8080:8080 hostel-mess
```

Open [http://localhost:8080/](http://localhost:8080/) to view the menu. The SQLite database is inside the container; data will not be retained when a container started with `--rm` is removed.

## Project Layout

```text
src/com/hostel/mess/   Java application, data access, UI, and web server
lib/                   JDBC drivers and logging libraries
documents/             Project reference documents
db.properties          Database configuration
run.bat                Windows desktop launcher
run_web_browser.bat    Windows launcher that opens the web menu
run.ps1                PowerShell desktop launcher
Dockerfile             Headless web-server container
```

For implementation details and more, see [TECHNICAL_DOCUMENTATION.md](TECHNICAL_DOCUMENTATION.md).
