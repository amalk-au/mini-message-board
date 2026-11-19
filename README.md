# Mini Message Board

A lightweight, server-rendered message board built with Node.js, Express.js, PostgreSQL and EJS, featuring a Star Trek-inspired theme.

## Table of Contents

- [Overview](#overview)

- [Features](#features)

- [Screenshots](#screenshots)

- [Live Demo](#live-demo)

- [Tech Stack](#tech-stack)

- [Architecture](#architecture)

- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)

  - [Installation](#installation)

  - [Environment Variables](#environment-variables)

- [Project Structure](#project-structure)

- [Available Commands](#available-commands)

- [Development](#development)

- [Testing](#testing)

- [API Reference](#api-reference)

- [Deployment](#deployment)

- [Troubleshooting](#troubleshooting)

- [Contributing](#contributing)

- [License](#license)

- [Acknowledgements](#acknowledgements)

- [Contact](#contact)

---

## Overview

Mini Message Board is a server-rendered web application that allows users to create, view and browse messages.

Built as a Node.js and Express.js project, it demonstrates fundamental backend development concepts, including routing, controller-based request handling, database integration and server-side template rendering.

The application uses PostgreSQL to persist messages and EJS to dynamically render HTML pages.

Its interface features a Star Trek: The Next Generation-inspired theme.

The project provides a practical demonstration of building a simple full-stack web application using a traditional server-side rendering architecture.

## Features

- **Message Board:** Display existing messages on the homepage, including the author's name, message content and timestamp.

- **Create Messages:** Submit new messages through a dedicated form.

- **Message Details:** Retrieve and view individual messages using their message ID.

- **Persistent Storage:** Store messages in a PostgreSQL database.

- **Server-Side Rendering:** Dynamically generate HTML pages using EJS templates.

- **Form Handling:** Process submitted form data using Express middleware.

## Screenshots

#### Main View

<p align="center"> <img src="./docs/screenshots/main-view.png" alt="Main view" width="800"> </p>

#### Message View

<p align="center"> <img src="./docs/screenshots/message.png" alt="Message view" width="300"> </p>

#### New Message

<p align="center"> <img src="./docs/screenshots/new-message.png" alt="New message form" width="400"> </p>

## Tech Stack

| Category                  | Technology            |
| ------------------------- | --------------------- |
| Runtime                   | Node.js               |
| Backend                   | Express.js            |
| Language                  | JavaScript (CommonJS) |
| Frontend                  | HTML5, CSS3           |
| Templating Engine         | EJS                   |
| Database                  | PostgreSQL            |
| Database Driver           | node-postgres (`pg`)  |
| Environment Configuration | dotenv                |
| Package Manager           | pnpm (preferred)      |
| Version Control           | Git                   |
| Repository Hosting        | GitHub                |

## Architecture

The application follows a simple server-side rendering architecture using Express.js.

Requests are handled through Express routes, which delegate application operations to controller functions. Controllers interact with database query functions, which communicate with PostgreSQL through a shared connection pool.

EJS templates render dynamic HTML responses using data retrieved from the database.

### Request Flow

1.  A user accesses a route through their browser.

2.  Express.js receives the HTTP request.

3.  The messages router directs the request to the appropriate controller.

4.  The controller retrieves or modifies data through the database query module.

5.  The database module executes SQL queries against PostgreSQL.

6.  The controller returns an HTML response or redirects the user.

### Application Components

| Component                          | Responsibility                                                                                |
| ---------------------------------- | --------------------------------------------------------------------------------------------- |
| `app.js`                           | Initialises Express, configures middleware, registers routes and starts the server.           |
| `routes/messagesRouter.js`         | Defines message-related application routes.                                                   |
| `controllers/messageController.js` | Handles message listing, form rendering, message submission and individual message retrieval. |
| `db/pool.js`                       | Configures the PostgreSQL connection pool.                                                    |
| `db/queries.js`                    | Contains SQL operations for retrieving and inserting messages.                                |
| `db/populatedb.js`                 | Creates the messages table and inserts initial sample messages.                               |
| `views/`                           | Contains EJS templates used to render application pages.                                      |
| `public/`                          | Contains static assets, including CSS and images.                                             |

## Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

Ensure the following tools and services are installed:

- **Node.js:** Required to run the application.

- **pnpm:** Preferred package manager.

- **PostgreSQL:** Required for persistent message storage.

- **Git:** Required to clone the repository.

You will also need access to a PostgreSQL database and its connection string.

### Installation

1.  Clone the repository:

    ```
    git clone https://github.com/amalk-au/mini-message-board.git
    ```

2.  Navigate to the project directory:

    ```
    cd mini-message-board
    ```

3.  Install dependencies:

    ```
    pnpm install
    ```

    The repository includes a `pnpm-lock.yaml` file. pnpm is the preferred package manager.

4.  Configure environment variables:

    Create a `.env` file in the project root:

    ```
    CONNECTION_URI=postgresql://USERNAME:PASSWORD@HOST:PORT/DATABASE
    ```

    Replace the placeholder values with your PostgreSQL connection details.

5.  Initialise the database:

    Run the database initialisation script:

    ```
    node db/populatedb.js
    ```

    This script creates the `messages` table if it does not already exist and inserts the initial sample messages.

    **Note:** The script inserts sample messages each time it runs. Running it repeatedly can create duplicate records.

6.  Start the application:

    ```
    node app.js
    ```

7.  Open the application in your browser:

    ```
    http://localhost:3000
    ```

### Environment Variables

The application uses dotenv to load environment variables from a `.env` file.

| Variable         | Description                            | Required |
| ---------------- | -------------------------------------- | -------- |
| `CONNECTION_URI` | PostgreSQL database connection string. | Yes      |

**Important:**

- Create the `.env` file manually; an `.env.example` file is not currently included.

- Never commit database credentials or other secrets to version control.

- Ensure the PostgreSQL database exists before running the application.

- The database connection must be accessible from the machine running the application.

## Project Structure

```
mini-message-board/
├── .github/
│   └── workflows/          # GitHub Actions workflow directory
├── controllers/
│   └── messageController.js
├── db/
│   ├── pool.js              # PostgreSQL connection pool
│   ├── queries.js           # Database queries
│   └── populatedb.js        # Database initialisation and sample data
├── public/
│   ├── styles.css           # Application styles
│   └── Enterprise_Forward.jpg
├── routes/
│   └── messagesRouter.js    # Express application routes
├── views/
│   ├── index.ejs            # Message board homepage
│   └── form.ejs             # New message form
├── .gitignore
├── LICENSE
├── app.js                   # Express application entry point
├── package.json
├── package-lock.json
├── pnpm-lock.yaml
└── README.md
```

## Available Commands

The project currently has a minimal command configuration.

The following commands are supported by the existing implementation:

| Command                 | Description                                         |
| ----------------------- | --------------------------------------------------- |
| `pnpm install`          | Install project dependencies.                       |
| `node app.js`           | Start the Express application.                      |
| `node db/populatedb.js` | Initialise the database and insert sample messages. |

There are currently no dedicated development, production build or start scripts configured in `package.json`.

## Development

The application uses CommonJS modules and a straightforward separation of responsibilities.

When making changes, follow the existing project conventions:

1.  **Routes:** Define HTTP endpoints in `routes/`.

2.  **Controllers:** Implement request-handling logic in `controllers/`.

3.  **Database:** Keep database connection and SQL operations in `db/`.

4.  **Views:** Use EJS templates for server-rendered HTML.

5.  **Static Assets:** Store stylesheets and images in `public/`.

Keep database operations separate from HTTP request-handling logic.

Use parameterised SQL queries when interacting with PostgreSQL to avoid SQL injection vulnerabilities.

Keep environment-specific configuration outside the source code.

## Testing

An automated testing framework and test suite are not currently configured.

The existing `package.json` contains a placeholder `test` script that deliberately exits with an error indicating that no tests have been specified.

Testing currently requires manual verification.

Recommended manual checks:

- Confirm the homepage displays existing database records.

- Submit a new message using the message form.

- Verify that submitted messages are persisted in PostgreSQL.

- Open an individual message and verify its displayed details.

- Confirm that the application handles database connection failures appropriately.

Automated tests can be introduced as the project evolves.

## API Reference

The application exposes the following HTTP routes through Express.js.

**Base URL:**

```
http://localhost:3000
```

| Method | Endpoint      | Description                                 |
| ------ | ------------- | ------------------------------------------- |
| GET    | `/`           | Retrieve and display all messages.          |
| GET    | `/new`        | Display the new message form.               |
| POST   | `/new`        | Submit and store a new message.             |
| GET    | `/:messageID` | Retrieve and display an individual message. |

### Database Schema

The application uses a PostgreSQL table named `messages`.

| Column  | Type          | Description                                                 |
| ------- | ------------- | ----------------------------------------------------------- |
| `id`    | INTEGER       | Primary key, automatically generated.                       |
| `text`  | VARCHAR(1024) | Message content.                                            |
| `users` | VARCHAR(256)  | Message author's name.                                      |
| `added` | TIMESTAMP     | Message creation timestamp, defaulting to the current time. |

The database table is created by `db/populatedb.js`.

### Authentication

The application does not currently implement user authentication or authorisation.

## Deployment

A live deployment is not currently available.

The application requires a Node.js-compatible hosting environment and an accessible PostgreSQL database.

### Deployment Requirements

| Configuration           | Details          |
| ----------------------- | ---------------- |
| Runtime                 | Node.js          |
| Database                | PostgreSQL       |
| Environment Variable    | `CONNECTION_URI` |
| Application Entry Point | `node app.js`    |
| Application Port        | `3000`           |

### Deployment Considerations

Before deploying to a production environment:

1.  Provision a PostgreSQL database.

2.  Configure the `CONNECTION_URI` environment variable.

3.  Initialise the database schema.

4.  Install production dependencies.

5.  Configure the hosting platform to start the application using `node app.js`.

6.  Ensure the application listens on the port expected by the hosting platform.

**Important:** The current application uses a hardcoded port (`3000`). Hosting platforms that provide a dynamic `PORT` environment variable will require an application configuration update before deployment.

## Troubleshooting

| Issue                               | Possible Solution                                                               |
| ----------------------------------- | ------------------------------------------------------------------------------- |
| Dependency installation fails       | Verify that Node.js and pnpm are installed correctly.                           |
| PostgreSQL connection fails         | Check the `CONNECTION_URI` value and confirm that the database is accessible.   |
| Missing environment variables       | Ensure a `.env` file exists in the project root and contains `CONNECTION_URI`.  |
| Database table does not exist       | Run `node db/populatedb.js` to initialise the database.                         |
| Application fails to start          | Check the terminal output for errors and confirm that port `3000` is available. |
| Application cannot display messages | Verify the PostgreSQL connection and confirm that the `messages` table exists.  |
| Message details cannot be retrieved | Check that the requested message ID exists in the database.                     |

## Contributing

Contributions and suggestions are welcome.

To contribute:

1.  Fork the repository.

2.  Create a feature branch:

    ```
    git checkout -b feature/your-feature-name
    ```

3.  Implement your changes following the existing project conventions.

4.  Test the application locally.

5.  Commit your changes:

    ```
    git commit -m "Add: your feature description"
    ```

6.  Push your branch and open a pull request.

For significant changes, consider opening an issue before submitting a pull request.

## License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

You are free to use, modify and distribute this software in accordance with the terms and conditions of the licence.

See the [LICENSE](LICENSE) file for the complete licence text.

## Acknowledgements

- **Star Trek: The Next Generation** — USS Enterprise-themed message board.

- **Express.js** — Web application framework.

- **EJS** — Server-side templating engine.

- **PostgreSQL** — Relational database management system.

- **The open-source community** — For maintaining the tools and libraries used in this project.

## Contact

- **Author:** Amal K.

- **GitHub:** [@amalk-au](https://github.com/amalk-au)

- **Repository:** [mini-message-board](https://github.com/amalk-au/mini-message-board)

- **Portfolio:** [https://amalk.au](https://amalk.au)

- **Issues:** [GitHub Issues](https://github.com/amalk-au/mini-message-board/issues)

---

Developed by [amalk-au](https://github.com/amalk-au)
