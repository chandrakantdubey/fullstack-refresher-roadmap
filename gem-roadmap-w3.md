Alright, let's build the backend.

This week, we shift our focus from the client-side (what the user sees) to the server-side. You'll learn how to build the engine that powers a web application using Node.js and Express. This is a crucial step in becoming a full-stack developer.

Here is the detailed, day-by-day plan for **Week 3**.

-----

## Week 3: Backend Development with Node.js & Express

**Project of the Week:** A RESTful API for a simple blogging platform. This API will handle creating, reading, updating, and deleting blog posts. We will test it using Postman.

**Key Concepts:** Server-Side JavaScript, REST Architecture, HTTP Methods, Middleware, API Endpoints.

-----

### **Day 1: Introduction to Node.js & Backend Concepts**

  * **Today's Goal:** Understand what Node.js is and set up a basic server.
  * **Topics:**
      * **What is Node.js?** Learn how JavaScript can be used outside the browser. Understand its event-driven, non-blocking I/O model.
      * **NPM:** Deeper dive into Node Package Manager. Learn about `package.json` and managing dependencies.
      * **Built-in Modules:** Explore core Node.js modules like `http` (to create a server) and `fs` (to interact with the file system).
  * **Tasks:**
    1.  **Project Setup:** Create a new folder for your blog API project. Run `npm init -y` to create a `package.json` file.
    2.  **Create a Simple Server:** Write a `server.js` file. Use the built-in `http` module to create a basic server that listens on a port (e.g., 3001) and sends back a "Hello, World\!" response.
    3.  **Run the Server:** Start your server from the terminal using `node server.js`. Visit `http://localhost:3001` in your browser to see the result.
  * **Learning Resources:**
      * [Node.js Docs - Introduction to Node.js](https://nodejs.dev/en/learn/)
      * [MDN - What is a web server?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)

-----

### **Day 2: Building with Express.js**

  * **Today's Goal:** Simplify server creation and routing with the Express.js framework.
  * **Topics:**
      * **What is Express?** Understand why it's the most popular framework for Node.js.
      * **Installation & Setup:** Learn how to add Express to your project.
      * **Basic Routing:** Define your first "route" or API endpoint.
  * **Tasks:**
    1.  **Install Express:** In your terminal, run `npm install express`.
    2.  **Refactor Server:** Modify your `server.js` file to use Express instead of the `http` module. The code will be much cleaner and more readable.
    3.  **Create First Route:** Create a GET route for the root path (`/`) that sends back a JSON response like `{ "message": "Welcome to the Blog API" }`.
  * **Learning Resources:**
      * [Express.js Docs - Hello world example](https://expressjs.com/en/starter/hello-world.html)

-----

### **Day 3: RESTful Routing & Controllers**

  * **Today's Goal:** Design and implement the core API endpoints for your blog.
  * **Topics:**
      * **REST Principles:** Understand the conventions of building a RESTful API (using nouns for URLs and HTTP verbs for actions).
      * **HTTP Methods:** Learn the purpose of `GET`, `POST`, `PUT`, and `DELETE`.
      * **Route Parameters:** Learn how to get dynamic values from the URL (e.g., `/posts/:id`).
  * **Tasks:**
    1.  **Mock Data:** Create a simple JavaScript array of objects to act as your in-memory "database" for blog posts.
    2.  **Implement `GET` Routes:**
          * `GET /api/posts`: Should return all blog posts.
          * `GET /api/posts/:id`: Should return a single blog post by its ID.
    3.  **Implement `POST` Route:**
          * `POST /api/posts`: Should add a new blog post to your array. You'll need to use the `express.json()` middleware to parse the request body.
  * **Learning Resources:**
      * [REST API concepts and examples](https://www.google.com/search?q=https://www.restapitutorial.com/lessons/whatisrest.html)
      * [Express.js Docs - Basic routing](https://expressjs.com/en/starter/basic-routing.html)

-----

### **Day 4: Introduction to Postman for API Testing**

  * **Today's Goal:** Learn to use a professional tool for testing and interacting with your API.
  * **Topics:**
      * **What is Postman?** Understand why it's an essential tool for backend developers.
      * **Making Requests:** Learn how to use Postman to send `GET`, `POST`, `PUT`, and `DELETE` requests to your API.
      * **Request Body:** Learn how to send JSON data in the body of a request.
  * **Tasks:**
    1.  **Install Postman:** Download and install the Postman desktop application.
    2.  **Create a Collection:** Organize your API requests in a new Postman collection for your blog API.
    3.  **Test Existing Routes:** Use Postman to test the `GET` and `POST` routes you created yesterday. Verify that they work as expected.
    4.  **Implement `PUT` and `DELETE`:** Now that you can test them, implement the `PUT /api/posts/:id` (update a post) and `DELETE /api/posts/:id` (delete a post) routes in your Express app.
  * **Learning Resources:**
      * [Postman Learning Center - Sending your first request](https://learning.postman.com/docs/getting-started/sending-the-first-request/)

-----

### **Day 5: Middleware & Environment Variables**

  * **Today's Goal:** Understand middleware and learn how to manage configuration securely.
  * **Topics:**
      * **Middleware:** Grasp this fundamental concept in Express. Understand the `request`, `response`, `next` flow.
      * **Custom Middleware:** Write your own simple middleware (e.g., a logger that prints request details to the console).
      * **Environment Variables:** Learn why you shouldn't hardcode sensitive information (like API keys or port numbers) and how to use `.env` files.
  * **Tasks:**
    1.  **Create Logger Middleware:** Write a function that logs the HTTP method and URL of every incoming request to the console. Use `app.use()` to apply it to all routes.
    2.  **Install `dotenv`:** Run `npm install dotenv`.
    3.  **Create `.env` file:** Create a `.env` file in your project's root. Add a `PORT=3001` variable.
    4.  **Update Server:** Modify `server.js` to use `process.env.PORT` instead of the hardcoded port number. Remember to add `.env` to your `.gitignore` file\!
  * **Learning Resources:**
      * [Express.js Docs - Writing middleware](https://expressjs.com/en/guide/writing-middleware.html)
      * [A guide to environment variables in Node.js](https://www.google.com/search?q=https://www.freecodecamp.org/news/how-to-use-environment-variables-in-nodejs/)

-----

### **Day 6: Project Structure & Error Handling**

  * **Today's Goal:** Organize your code for better maintainability and handle potential errors gracefully.
  * **Topics:**
      * **Code Organization:** Separate your routes and controller logic into different files/folders.
      * **Error Handling:** Implement a basic error handling middleware to catch and respond to errors consistently.
  * **Tasks:**
    1.  **Refactor:** Create a `routes` folder and a `controllers` folder.
          * Move your route definitions (`app.get`, `app.post`, etc.) into a file like `routes/postRoutes.js`.
          * Move the functions that handle the logic for each route into `controllers/postController.js`.
    2.  **Error Middleware:** Create a "catch-all" error handling middleware at the end of your `server.js` file that sends back a generic 500 status code and error message.
  * **Learning Resources:**
      * [Best practices for structuring an Express app](https://www.terlici.com/2014/08/25/best-practices-express-structure.html)
      * [Express.js Docs - Error handling](https://expressjs.com/en/guide/error-handling.html)

-----

### **Day 7: Review and Prepare for Databases**

  * **Today's Goal:** Solidify your understanding of this week's topics and look ahead.
  * **Tasks:**
    1.  **Review:** Go through all the code you've written this week. Add comments to explain complex parts.
    2.  **Postman Documentation:** Use Postman's features to add descriptions to each of your API requests, explaining what they do.
    3.  **Update README:** Update your project's `README.md` on GitHub. Explain the API's purpose and list all the available endpoints.
    4.  **Look Ahead:** Read the high-level concepts of what a database is and the difference between SQL and NoSQL. This will prepare you for next week.

Fantastic work\! You've now built the foundation of a backend service. The API you've created is the crucial link that will eventually connect your React frontend to a real database.

Let me know when you're ready to tackle **Week 4: Databases with PostgreSQL & ORMs**.
