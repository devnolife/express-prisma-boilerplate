# Express Prisma Boilerplate

This repository provides a **clean and scalable boilerplate** for building modern web applications using **Express**, **Prisma**, and **JavaScript**. The boilerplate is designed to follow clean architecture principles and is aimed at making backend development simpler and more organized.

## Key Technologies

- **Express**: A minimal and flexible Node.js web application framework that provides a robust set of features to build web and mobile applications.
- **Prisma**: A next-generation ORM (Object-Relational Mapper) that makes database access easy with an auto-generated query builder for TypeScript & JavaScript.
- **JavaScript (ES6+)**: Modern JavaScript for building scalable server-side logic.

## Features

- Pre-configured with **Express** for server setup and routing.
- Integrated with **Prisma ORM** for database management.
- Follows **clean architecture** principles to ensure code modularity and maintainability.
- Ready to use with **PostgreSQL** (can be configured for other databases).
- Includes a flexible **generic handler** for CRUD operations to keep controllers clean and reusable.
- **Error handling** and **validation** built-in.

## Project Structure

The project is structured to follow clean code practices. Here is an overview of the key folders and files:

```
├── prisma                       Prisma schema and migrations
│   ├── schema.prisma           # Database schema
│   └── migrations/             # Database migrations
├── src                         # Source code directory
│   ├── controllers             # Express route controllers
│   ├── middlewares             # Express middlewares
│   ├── routes                  # API routes definitions
│   ├── services                # Database interaction and business logic
│   ├── utils                   # Helper functions and utility modules
│   └── app.js                  # Main Express application setup
├── .env                        # Environment variables
├── package.json                # Node.js dependencies and scripts
└── README.md                   # Project documentation
```

## Prerequisites

- **Node.js** (v14.x or later)
- **npm** or **yarn**
- **PostgreSQL** (or other databases supported by Prisma)
- **Prisma CLI** (installed globally)

## Getting Started

### 1. Clone the repository:

```bash
git clone https://github.com/devnolife/express-prisma-boilerplate.git
cd express-prisma-boilerplate
```

### 2. Install dependencies:

```bash
npm install
```

or

```bash
yarn install
```

### 3. Set up the environment variables:

Create a `.env` file in the root directory and configure it with your database URL.

```
DATABASE_URL="postgresql://username:password@localhost:5432/mydb?schema=public"
```

### 4. Run Prisma migrations:

To apply the Prisma migrations and set up the database schema, run:

```bash
npx prisma migrate dev
```

### 5. Start the development server:

```bash
npm run dev
```

or

```bash
yarn dev
```

The app will be available at `http://localhost:3000`.

## How to Use

### Generic CRUD Handler

This boilerplate comes with a **generic handler** for CRUD operations that simplifies the creation of routes and controllers. You can configure CRUD operations for any table using the `genericHandler` utility, which automatically detects HTTP methods (GET, POST, PUT, DELETE).

Example for handling a resource like `users`:

```javascript
const { genericHandler } = require('../utils/genericHandler');

// Controller for 'users' resource
const userController = genericHandler(
  'users', 
  'User created successfully', 
  'User updated successfully', 
  'User retrieved successfully', 
  'User deleted successfully',
  'Failed to handle user data'
);

module.exports = { userController };
```

### Example Routes

You can define routes like this in `src/routes/users.js`:

```javascript
const express = require('express');
const { userController } = require('../controllers/users');
const router = express.Router();

router.route('/users/:id?')
  .get(userController)
  .post(userController)
  .put(userController)
  .delete(userController);

module.exports = router;
```

## Deployment

To deploy this project:

1. Set up your database (e.g., on **Heroku**, **AWS RDS**, etc.).
2. Set up environment variables in your production environment (especially the `DATABASE_URL`).
3. Install dependencies and run migrations in the production environment.
4. Start the server using a process manager like **PM2**.

## Prisma CLI Commands

Here are some useful Prisma CLI commands:

- **`npx prisma migrate dev`**: Apply database schema changes and generate Prisma Client.
- **`npx prisma db push`**: Push the schema to the database without creating migrations.
- **`npx prisma studio`**: Open the Prisma Studio GUI to view and edit your database.

## Contributing

Feel free to fork this repository and submit pull requests. Contributions are welcome!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
