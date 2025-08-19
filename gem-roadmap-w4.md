Of course. Let's dive into Week 4.

This week is a major milestone. You'll move from temporary, in-memory data to a professional, persistent database. You'll learn how to store, structure, and retrieve data using PostgreSQL, the world's most advanced open-source relational database. We'll also introduce Prisma, a modern ORM that makes working with databases from your Node.js application intuitive and safe.

Here's the detailed, day-by-day plan for **Week 4**.

-----

## Week 4: Databases with PostgreSQL & ORMs

**Project of the Week:** A full-stack "To-Do List" application. You will build a new React front-end and connect it to a new Express API that uses a PostgreSQL database for persistence.

**Key Concepts:** Relational Databases, SQL (Structured Query Language), ORM (Object-Relational Mapping), Data Modeling, ACID Properties.

-----

### **Day 1: Introduction to Databases & PostgreSQL Setup**

  * **Today's Goal:** Understand what a relational database is and get PostgreSQL running on your local machine.
  * **Topics:**
      * **What is a Database?** The difference between a database, a DBMS (Database Management System), and SQL.
      * **Relational vs. Non-Relational (SQL vs. NoSQL):** A high-level overview of the two main types of databases and why we're starting with SQL.
      * **PostgreSQL:** Learn why it's a popular choice for modern applications.
      * **Data Modeling:** The concept of designing tables, columns, and relationships.
  * **Tasks:**
    1.  **Install PostgreSQL:** Follow the official guide to install PostgreSQL for your operating system.
    2.  **Install pgAdmin:** Install pgAdmin, a graphical user interface (GUI) for managing your PostgreSQL databases.
    3.  **Create Your First Database:** Use pgAdmin to connect to your local PostgreSQL server and create a new database named `todo_app`.
    4.  **Create a Table with the GUI:** Inside your `todo_app` database, use the pgAdmin interface to create your first table called `todos` with columns like `id` (a unique number), `title` (text), and `is_completed` (a boolean).
  * **Learning Resources:**
      * [PostgreSQL Official Downloads](https://www.postgresql.org/download/)
      * [pgAdmin Download](https://www.pgadmin.org/download/)
      * [What is a Relational Database?](https://www.oracle.com/database/what-is-a-relational-database/)

-----

### **Day 2: Fundamental SQL Commands**

  * **Today's Goal:** Learn the four fundamental SQL commands for interacting with data. These are known as CRUD operations (Create, Read, Update, Delete).
  * **Topics:**
      * **`SELECT`:** How to query and retrieve data from a table.
      * **`INSERT INTO`:** How to add new rows (records) to a table.
      * **`UPDATE`:** How to modify existing records in a table.
      * **`DELETE`:** How to remove records from a table.
      * **`WHERE` clause:** How to filter your queries to be more specific.
  * **Tasks:**
    1.  **Open SQL Tool:** In pgAdmin, open the "Query Tool" for your `todo_app` database.
    2.  **`INSERT` Data:** Write and run an `INSERT` command to add a few to-do items to your `todos` table. For example: `INSERT INTO todos (title, is_completed) VALUES ('Learn SQL', false);`
    3.  **`SELECT` Data:** Write a `SELECT * FROM todos;` query to see the data you just added. Then, practice using the `WHERE` clause to select a specific to-do item by its `id`.
    4.  **`UPDATE` Data:** Write an `UPDATE` command to change one of your to-dos to be completed. For example: `UPDATE todos SET is_completed = true WHERE id = 1;`
    5.  **`DELETE` Data:** Write a `DELETE` command to remove one of the to-dos.
  * **Learning Resources:**
      * [SQLBolt - Interactive SQL Tutorial](https://sqlbolt.com/) (Excellent for practice)
      * [PostgreSQL Docs - Chapter 2. The SQL Language](https://www.postgresql.org/docs/current/tutorial-sql.html)

-----

### **Day 3: Introduction to ORMs & Prisma Setup**

  * **Today's Goal:** Understand what an ORM is and set up Prisma in your backend project.
  * **Topics:**
      * **What is an ORM?** Learn how an ORM (Object-Relational Mapper) acts as a bridge, letting you write JavaScript/TypeScript instead of raw SQL.
      * **Why Prisma?** Understand its benefits: autocompletion, type safety, and an intuitive schema definition.
      * **Prisma Schema:** Learn how to define your database models in the `schema.prisma` file.
  * **Tasks:**
    1.  **Project Setup:** Create a new project folder for your `todo-app-backend`. Run `npm init -y` and install Express.
    2.  **Install Prisma:** In your project, run `npm install prisma --save-dev` and `npm install @prisma/client`.
    3.  **Initialize Prisma:** Run `npx prisma init`. This creates a `prisma` folder and a `.env` file.
    4.  **Configure `.env`:** Open the `.env` file and update the `DATABASE_URL` to point to your local PostgreSQL database. The format is: `postgresql://USERNAME:PASSWORD@localhost:5432/DATABASE_NAME`.
    5.  **Define Model:** Open `prisma/schema.prisma`. Define a `Todo` model that matches the table you created on Day 1.
  * **Learning Resources:**
      * [Prisma Docs - Why Prisma?](https://www.prisma.io/docs/concepts/overview/why-prisma)
      * [Prisma Docs - Set up Prisma in a new project](https://www.google.com/search?q=https://www.prisma.io/docs/getting-started/setup-prisma/start-from-scratch/relational-databases-npm-postgresql)

-----

### **Day 4: Integrating Prisma with your Express API**

  * **Today's Goal:** Replace raw SQL and in-memory arrays with Prisma Client to build a robust API.
  * **Topics:**
      * **Prisma Migrate:** The command that reads your schema and creates/updates your database tables automatically.
      * **Prisma Client:** The auto-generated and type-safe query builder you'll use in your code.
      * **API Logic:** Implementing the CRUD operations in your Express controllers using Prisma Client.
  * **Tasks:**
    1.  **Run Migration:** Run `npx prisma migrate dev --name init` in your terminal. This will create the `todos` table in your database based on your Prisma schema.
    2.  **Instantiate Prisma Client:** In your `server.js` (or a separate config file), import and create an instance of the Prisma Client.
    3.  **Build API Endpoints:** Create the five core RESTful routes for your To-Do app:
          * `GET /api/todos`: Fetches all todos using `prisma.todo.findMany()`.
          * `POST /api/todos`: Creates a new todo using `prisma.todo.create()`.
          * `GET /api/todos/:id`: Fetches a single todo using `prisma.todo.findUnique()`.
          * `PUT /api/todos/:id`: Updates a todo using `prisma.todo.update()`.
          * `DELETE /api/todos/:id`: Deletes a todo using `prisma.todo.delete()`.
    4.  **Test with Postman:** Thoroughly test every endpoint you just created using Postman.
  * **Learning Resources:**
      * [Prisma Docs - Basic CRUD queries](https://www.google.com/search?q=https://www.prisma.io/docs/concepts/components/prisma-client/crud)

-----

### **Day 5: Building the React Frontend**

  * **Today's Goal:** Create a clean, functional React application to interact with your new backend API.
  * **Topics:**
      * **Project Scaffolding:** Using Vite to create a new React project.
      * **State Management:** Using the `useState` hook to manage the list of to-dos and the input for new ones.
      * **Component Structure:** Breaking the UI down into components (e.g., `TodoList`, `TodoItem`, `AddTodoForm`).
  * **Tasks:**
    1.  **Create React App:** In a separate terminal window, run `npm create vite@latest todo-app-frontend -- --template react`.
    2.  **Basic UI:** Build the static JSX and CSS for your application. It should have an input field, a button to add a to-do, and a list to display the to-dos.
    3.  **Manage State:** Set up state variables for the list of todos (`todos`) and the text in the input field (`newTodo`).
  * **Learning Resources:**
      * [React Docs - Quick Start](https://react.dev/learn)
      * [React Docs - Managing State](https://react.dev/learn/managing-state)

-----

### **Day 6: Connecting Frontend & Backend (The Full Stack\!)**

  * **Today's Goal:** Make the frontend and backend communicate. This is the moment everything comes together. 🚀
  * **Topics:**
      * **`useEffect` Hook:** How to fetch data from the API when the component first loads.
      * **Fetching Data:** Using the `fetch` API or a library like `axios` to make HTTP requests.
      * **Handling User Events:** Connecting functions to `onClick` and `onChange` events to create, update, and delete to-dos.
      * **CORS:** Understanding and fixing Cross-Origin Resource Sharing errors by using the `cors` middleware in Express.
  * **Tasks:**
    1.  **Install CORS:** In your backend project, run `npm install cors` and add `app.use(cors())` to your `server.js`.
    2.  **Fetch To-Dos:** Use the `useEffect` hook in your main React component to fetch all to-dos from your `GET /api/todos` endpoint when the app loads and display them.
    3.  **Create To-Dos:** Implement the function that handles form submission. It should make a `POST` request to `/api/todos` with the new to-do's title and then refresh the list.
    4.  **Update & Delete:** Implement the functions for toggling the completion status (`PUT`) and deleting a to-do (`DELETE`). Pass these functions down as props to the `TodoItem` component.
  * **Learning Resources:**
      * [MDN - Using the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
      * [React Docs - Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)

-----

### **Day 7: Review, Refactor, and Deploy**

  * **Today's Goal:** Solidify what you've built, clean up the code, and push it to GitHub.
  * **Tasks:**
    1.  **Code Review:** Read through both your frontend and backend code. Is it clean? Can you add comments to explain the logic?
    2.  **Error Handling:** What happens if the API call fails? Add basic `.catch()` blocks to your fetch requests to log errors to the console.
    3.  **Final Polish:** Make sure the UI is simple and intuitive. Add some basic styling.
    4.  **Update GitHub:** Create a new GitHub repository for your full-stack To-Do app. Push both the `frontend` and `backend` folders to it.
    5.  **Write an Excellent README:** This is crucial. Your `README.md` should explain what the project is, how to run the backend, and how to run the frontend. This is your project's business card.

Congratulations\! You've successfully built and connected a complete full-stack application. You now understand how a user interface can interact with an API, which in turn interacts with a real, persistent database. This is the core pattern for the vast majority of web applications.

You're now ready for **Part 2: Full-Stack Integration & Intermediate Skills**. Let me know when you're ready to proceed to Week 5.
