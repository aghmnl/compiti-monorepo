# Task Management Application (Monorepo)

## Overview

This repository contains a **Task Management Application** built using a monorepo structure managed by **Turborepo**. The application allows users to manage a list of tasks with the following fields:

- **id**: Auto-incremental identifier.
- **title**: Required string field.
- **description**: Optional string field.
- **status**: Enum with values: `pending`, `in progress`, `done`.

This monorepo includes both the client-side and server-side code for the application.

## Technology Stack

The application utilizes the following technologies:

- **Monorepo Management**:
  - Turborepo
- **Frontend (Client)**:
  - Next.js (App Router, TypeScript)
  - shadcn/ui (UI Components)
  - Clerk (Authentication)
- **Backend (Server)**:
  - Node.js
  - Prisma (ORM with SQLite or PostgreSQL)
- **API & Communication**:
  - tRPC
- **Validation**:
  - Zod (Client & Server)
- **Development Tools**:
  - TypeScript
  - npm

## Features

The application includes the following functionalities:

- **Task Management**:
  - Create a new task.
  - View the list of tasks.
  - Edit an existing task.
  - Delete a task.
- **Validation**:
  - Client-side and Server-side validation using Zod.
- **User Interface**:
  - A clean and responsive UI built with shadcn/ui.
- **Authentication**:
  - User authentication using Clerk.
- **Architecture**:
  - Modular component structure (Client).
  - Modular structure for API routes and validations (Server).
  - Efficient build and development workflows powered by Turborepo.

## Monorepo Structure

This repository uses Turborepo to manage the workspaces. You'll typically find the code organized into directories like:

- `apps/client`: Contains the Next.js frontend application.
- `apps/server`: Contains the Node.js/tRPC backend application.
- `packages/*`: May contain shared code, configurations (like `tsconfig`, `eslint`), or UI components used across applications.

## Installation and Local Setup

Follow these steps to install and run the application locally:

### Prerequisites

- Node.js
- npm

### Steps

1.  **Clone the repository**

    ```bash
    git clone https://github.com/aghmnl/compiti-monorepo.git
    cd compiti-monorepo
    ```

2.  **Install dependencies**

    Install dependencies from the root of the monorepo. This will install dependencies for all workspaces (client, server, packages).

    ```bash
    npm install
    ```

3.  **Set up environment variables**

- Navigate to the server application directory `apps/server` and create a `.env` file.
- Add the database connection string:
  `env

  ```bash
  # In apps/server/.env
  DATABASE_URL="file:./dev.db"
  ```

- Navigate to the client application directory (e.g., `apps/client`) and create a `.env` file.
- Add your Clerk and server URL variables:

  ```bash
  # In apps/client/.env
  NEXT*PUBLIC_CLERK_PUBLISHABLE_KEY="your-clerk-publishable-key"
  CLERK_SECRET_KEY="your-clerk-secret-key"
  NEXT_PUBLIC_SERVER_URL="http://localhost:4000"
  ```

  > Note: Refer to Clerk documentation for the specific environment variables required.

4.  **Set up the database**

    Run Prisma migrations to create the database schema. You might need to run this command from the root or specify the server workspace depending on your Turborepo setup. A common way is:

    ```bash
    # Example using pnpm from the root, targeting the 'server' app's 'prisma:migrate' script
    # Adjust the command based on your package manager and package.json scripts
    pnpm --filter server run prisma:migrate

    # Or navigate to the server directory and run directly
    # cd apps/server
    # npx prisma migrate dev
    # cd ../..
    ```

    _Ensure you have a `prisma:migrate` script (e.g., `"prisma:migrate": "prisma migrate dev"`) in your `apps/server/package.json`._

5.  **Run the development servers**

    Use Turborepo to run the development servers for both the client and server concurrently.

    ```bash
    # This command assumes you have a "dev" script defined in the root package.json
    # that Turborepo uses to run the "dev" scripts in each app (`client` and `server`).
    npm run dev
    ```

6.  **Access the application**

    - The client application should be available at `http://localhost:3000`.
    - The server API endpoint (used by the client via tRPC) will be running on `http://localhost:4000`.

## Documentation Used

The following official documentation was referenced during the development process:

- [Turborepo Documentation](https://turborepo.com/docs)
- [Next.js Documentation](https://nextjs.org/docs)
- [shadcn/ui Documentation](https://ui.shadcn.com/docs)
- [Clerk Documentation](https://clerk.dev/docs)
- [tRPC Documentation](https://trpc.io/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Zod Documentation](https://zod.dev)

## Contributing

Feel free to fork this repository and submit pull requests for improvements or bug fixes. Please ensure your changes align with the project structure and coding standards.

## License

This project is licensed under the [MIT License](https://opensource.org/license/mit).
