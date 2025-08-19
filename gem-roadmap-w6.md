Let's get into Week 6.

This week, you'll tackle one of the most fundamental requirements of modern web applications: user authentication. You'll learn how to securely register users, log them in, and protect specific parts of your application from unauthorized access. This is a critical skill for any full-stack developer.

Here's the detailed, day-by-day plan for **Week 6**.

-----

## Week 6: Advanced Authentication & Security

**Project of the Week:** A user authentication system for a "Social Media Dashboard." You'll build the backend and frontend for users to sign up, log in, and view a protected profile page that only they can access.

**Key Concepts:** Authentication vs. Authorization, Password Hashing, JSON Web Tokens (JWT), Protected Routes, Middleware.

-----

### **Day 1: Authentication Theory & Secure Password Storage**

  * **Today's Goal:** Understand core security concepts and learn how to handle passwords responsibly.
  * **Topics:**
      * **Authentication vs. Authorization:** Learn the difference. **Authentication** is proving who you are. **Authorization** is checking if you have permission to do something.
      * **Password Security:** Understand why you **must never, ever** store passwords in plain text.
      * **Hashing:** Learn how hashing algorithms create a one-way, non-reversible fingerprint of a password.
      * **bcrypt:** The industry-standard library for hashing and comparing passwords in Node.js.
  * **Tasks:**
    1.  **Project Setup:** Create a new `social-dashboard` project with `backend` and `frontend` folders.
    2.  **Backend Setup:** Initialize a new Node.js, Express, and Prisma project in the `backend` folder.
    3.  **Create User Model:** In your `schema.prisma` file, define a `User` model with fields like `id`, `email` (must be unique), and `password`.
    4.  **Install `bcryptjs`:** In your backend, run `npm install bcryptjs`.
    5.  **Practice Hashing:** In a temporary test file, use `bcryptjs` to hash a sample password and then use its `compare` function to see how it verifies the original password against the hash.
  * **Learning Resources:**
      * [Hashing vs. Encryption](https://www.okta.com/identity-101/hashing-vs-encryption/)
      * [`bcrypt.js` on npm](https://www.google.com/search?q=%5Bhttps://www.npmjs.com/package/bcryptjs%5D\(https://www.npmjs.com/package/bcryptjs\))

-----

### **Day 2: Building the User Registration Endpoint**

  * **Today's Goal:** Create the backend API endpoint for new users to sign up.
  * **Topics:**
      * **API Route Design:** Structuring your authentication routes (e.g., `/api/auth/register`).
      * **Input Validation:** Basic checks to ensure the user provides a valid email and password.
      * **Controller Logic:** Writing the function that handles the registration request.
  * **Tasks:**
    1.  **Create Auth Routes:** Create a new file for your authentication routes (`routes/auth.js`).
    2.  **Build the `/register` Endpoint:** Create a `POST /api/auth/register` endpoint.
    3.  **Write Controller Logic:** In the controller function for this endpoint:
          * Extract the `email` and `password` from the request body.
          * Check if a user with that email already exists in the database. If so, send back an error.
          * Use `bcrypt.hash()` to hash the user's password.
          * Use Prisma Client to create and save the new user in the database with the hashed password.
          * Send back a success response.
    4.  **Test with Postman:** Use Postman to create a new user by sending a `POST` request to your `/register` endpoint. Check your database using `pgAdmin` or Prisma Studio (`npx prisma studio`) to verify that the user was created and the password is a long, hashed string.
  * **Learning Resources:**
      * Review Week 3's notes on Express routing and controllers.

-----

### **Day 3: User Login and Issuing JSON Web Tokens (JWT)**

  * **Today's Goal:** Allow users to log in and receive a special token (JWT) that proves they are authenticated.
  * **Topics:**
      * **What is a JWT?** A compact, URL-safe means of representing claims to be transferred between two parties. It's essentially a digitally signed, stateless credential.
      * **JWT Structure:** Header, Payload (the data, e.g., user ID), and Signature (for verification).
      * **Login Logic:** How to verify a user's password and generate a token.
  * **Tasks:**
    1.  **Install `jsonwebtoken`:** In your backend, run `npm install jsonwebtoken`.
    2.  **Set JWT Secret:** Add a `JWT_SECRET` to your `.env` file. This is a secret key used to sign your tokens. Make it long and random.
    3.  **Build the `/login` Endpoint:** Create a `POST /api/auth/login` endpoint.
    4.  **Write Controller Logic:**
          * Find the user in the database by their email. If not found, send an error.
          * Use `bcrypt.compare()` to check if the password from the request body matches the hashed password in the database.
          * If the passwords match, create a JWT using `jwt.sign()`. The payload should contain the user's ID.
          * Send the generated token back to the user in a JSON response.
    5.  **Test with Postman:** Use Postman to test the `/login` endpoint with the user you created yesterday. You should receive a long JWT string in the response.
  * **Learning Resources:**
      * [Introduction to JSON Web Tokens](https://jwt.io/introduction)

-----

### **Day 4: Protecting Backend Routes with Middleware**

  * **Today's Goal:** Create a mechanism to protect certain API endpoints so they can only be accessed by logged-in users.
  * **Topics:**
      * **Express Middleware:** A deeper dive. Middleware functions have access to the request, response, and the `next` function.
      * **Authorization Header:** The standard way to send a token to a server (`Authorization: Bearer <token>`).
      * **Token Verification:** Using `jwt.verify()` to check if a token is valid and was signed with our secret key.
  * **Tasks:**
    1.  **Create `authMiddleware`:** Write a middleware function (e.g., in `middleware/auth.js`).
    2.  **Implement Middleware Logic:**
          * Check for the `Authorization` header in the request.
          * Extract the token from the header string.
          * If no token is found, send a `401 Unauthorized` error.
          * Use a `try...catch` block to run `jwt.verify()`. If it fails (invalid token), send a `401` error.
          * If it succeeds, the decoded payload (containing the user ID) is attached to the request object (e.g., `req.user`).
          * Call `next()` to pass control to the next function in the chain.
    3.  **Apply Middleware:** Create a new endpoint, like `GET /api/profile`. Apply your `authMiddleware` to this route.
    4.  **Test with Postman:** Try to access `/api/profile` without a token (it should fail). Then, copy the token you got from logging in, add it as a Bearer Token in Postman's Authorization tab, and try again (it should succeed).
  * **Learning Resources:**
      * [Express.js Docs - Using middleware](https://expressjs.com/en/guide/using-middleware.html)

-----

### **Day 5: Building Frontend Login & Registration Pages**

  * **Today's Goal:** Create the React UI for users to sign up and log in.
  * **Topics:**
      * **Form Handling:** Building controlled components for registration and login forms.
      * **API Service Layer:** Creating helper functions to organize your `fetch` calls to the backend (e.g., `api.js` with `loginUser()` and `registerUser()` functions).
      * **Storing the JWT:** On successful login, securely store the received JWT in the browser's **localStorage**.
  * **Tasks:**
    1.  **Set Up React Router:** Install and configure `react-router-dom` in your frontend project.
    2.  **Create Pages:** Create components for `RegisterPage.jsx` and `LoginPage.jsx`.
    3.  **Build Forms:** Implement the JSX and state management for the forms on both pages.
    4.  **Implement API Calls:** Write the `handleSubmit` functions. They should call your backend API endpoints.
    5.  **Save the Token:** In the login form's submission handler, after you receive a successful response from the backend, save the token to `localStorage` using `localStorage.setItem('token', data.token);`.
  * **Learning Resources:**
      * [MDN - Window.localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

-----

### **Day 6: Frontend Protected Routes & Global State**

  * **Today's Goal:** Protect frontend routes and manage the user's login status across the entire application.
  * **Topics:**
      * **React Context:** A way to share state (like the user's authentication status) across your entire app without having to pass props down manually through every level.
      * **Auth Context:** Creating a specific context to manage user data and the auth token.
      * **Protected Route Component:** A custom React component that conditionally renders its children or redirects to the login page.
  * **Tasks:**
    1.  **Create `AuthContext`:** Create a new context file. It should provide the user's token, login status (`isAuthenticated`), and functions for `login` and `logout`.
    2.  **Wrap Your App:** Wrap your entire application with the `AuthProvider` in `main.jsx`.
    3.  **Create `ProtectedRoute` Component:** This component will check the `isAuthenticated` value from the `AuthContext`.
          * If `true`, it renders its `children`.
          * If `false`, it uses the `<Navigate>` component from React Router to redirect the user to `/login`.
    4.  **Implement on Routes:** In your `App.jsx`, wrap the route for your new `ProfilePage.jsx` with your `ProtectedRoute` component.
  * **Learning Resources:**
      * [React Docs - Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)

-----

### **Day 7: Polishing the Flow & Logout**

  * **Today's Goal:** Implement logout functionality and ensure the entire authentication flow is smooth and secure.
  * **Tasks:**
    1.  **Implement Logout:** Create a logout button. Its `onClick` handler should call the `logout` function from your `AuthContext`. This function should remove the token from `localStorage` and update the context's state.
    2.  **Fetch Profile Data:** On the `ProfilePage`, use `useEffect` to make an API call to your protected `GET /api/profile` endpoint. Remember to include the token from localStorage in the `Authorization` header of your `fetch` request.
    3.  **End-to-End Testing:** Go through the entire user journey:
          * Try to access the profile page directly (should redirect to login).
          * Register a new user.
          * Log in with that user.
          * You should be taken to the profile page, and it should display their data.
          * Click logout. You should be redirected, and the token should be gone.
    4.  **Review and Refactor:** Clean up your code in both the frontend and backend. Add comments and update your `README.md`.

You've now implemented one of the most important features of any non-trivial web application. This knowledge is essential and highly valuable.

You're well-equipped for the next step, where we'll explore more advanced ways to manage data. Let me know when you're ready for **Week 7**.
