Excellent. Let's get started on Week 5.

You've successfully built a full-stack application. Now, we'll build on that foundation to create a more complex, multi-page application. This week is all about mastering the flow of data between your client and server, handling asynchronous operations gracefully, and creating a seamless user experience with client-side routing.

Here is the detailed, day-by-day plan for **Week 5**.

-----

## Week 5: Connecting Frontend & Backend

**Project of the Week:** A full-stack "Recipe Book" application. Users will be able to view a list of recipes, click to see a detailed view of a single recipe, and add new recipes via a form.

**Key Concepts:** Client-Side Routing, Asynchronous JavaScript (Promises, `async/await`), Data Fetching Patterns, CORS.

-----

### **Day 1: Asynchronous JavaScript Deep Dive & Project Setup**

  * **Today's Goal:** Solidify your understanding of how JavaScript handles asynchronous operations and set up the new project.
  * **Topics:**
      * **The Event Loop:** A high-level conceptual understanding of how Node.js and browsers handle async code.
      * **Promises:** The core concept. Understand `pending`, `fulfilled`, and `rejected` states. Practice using `.then()`, `.catch()`, and `.finally()`.
      * **`async/await`:** Learn this modern, cleaner syntax for working with Promises. Understand `try...catch` for error handling.
      * **CORS (Cross-Origin Resource Sharing):** A deeper look at *why* it's needed and how the `cors` middleware works in Express.
  * **Tasks:**
    1.  **Project Setup:** Create a new monorepo folder for the `recipe-book` project. Inside it, set up two sub-folders: `backend` and `frontend`.
    2.  **Initialize Backend:** In the `backend` folder, set up a new Node.js/Express project with Prisma and PostgreSQL, just as you did in Week 4. Remember to install `cors`.
    3.  **Initialize Frontend:** In the `frontend` folder, use Vite to scaffold a new React application.
    4.  **Practice `async/await`:** In a separate practice file, rewrite a `.then()/.catch()` promise chain using the `async/await` syntax. Use a public API like the [JSONPlaceholder API](https://jsonplaceholder.typicode.com/) to fetch some dummy data.
  * **Learning Resources:**
      * [MDN - Asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)
      * [Visualizing a Promise](https://www.google.com/search?q=https://javascript.info/async-await)

-----

### **Day 2: Building the Recipe API Backend**

  * **Today's Goal:** Design and build a robust REST API to handle all the data operations for the recipe book.
  * **Topics:**
      * **Data Modeling:** Designing the `Recipe` model. What fields do we need? (e.g., `title`, `description`, `ingredients`, `instructions`, `imageUrl`).
      * **CRUD Endpoints:** Creating the full set of API endpoints for recipes.
  * **Tasks:**
    1.  **Define Prisma Schema:** In your backend's `schema.prisma` file, define the `Recipe` model. Think about data types (`String`, `String[]` for ingredients, etc.).
    2.  **Run Migration:** Execute `npx prisma migrate dev` to create the `recipes` table in your database.
    3.  **Create Controllers & Routes:** Build the Express routes and controller functions for:
          * `GET /api/recipes`: Get all recipes.
          * `POST /api/recipes`: Create a new recipe.
          * `GET /api/recipes/:id`: Get a single recipe by its ID.
          * (Optional for now) `PUT /api/recipes/:id`: Update a recipe.
          * (Optional for now) `DELETE /api/recipes/:id`: Delete a recipe.
    4.  **Test with Postman:** Use Postman to add a few sample recipes and test every endpoint to ensure they work correctly before touching the frontend.
  * **Learning Resources:**
      * [Prisma Docs - Modeling relations](https://www.google.com/search?q=https://www.prisma.io/docs/concepts/components/prisma-schema/relations) (useful for future projects).

-----

### **Day 3: Client-Side Routing with React Router**

  * **Today's Goal:** Transform your single-page React app into a multi-page experience using React Router.
  * **Topics:**
      * **What is Client-Side Routing?** Understand how it creates the illusion of multiple pages without a full page reload from the server.
      * **React Router:** The industry-standard library for routing in React.
      * **Core Components:** Learn about `<BrowserRouter>`, `<Routes>`, `<Route>`, and `<Link>`.
      * **Dynamic Routes:** How to create routes with parameters, like `/recipes/:id`.
  * **Tasks:**
    1.  **Install React Router:** In your `frontend` project, run `npm install react-router-dom`.
    2.  **Set Up Router:** In your `main.jsx` (or `index.js`), wrap your `<App />` component with `<BrowserRouter>`.
    3.  **Define Routes:** In `App.jsx`, set up your main `<Routes>`. Create routes for the homepage (`/`), the list of all recipes (`/recipes`), and the form to add a new recipe (`/add-recipe`).
    4.  **Create Page Components:** Create placeholder components for each route (e.g., `HomePage.jsx`, `RecipesListPage.jsx`, `AddRecipePage.jsx`).
    5.  **Add Navigation:** Create a simple `Navbar` component with `<Link>` tags to navigate between your new pages.
  * **Learning Resources:**
      * [React Router Docs - Main Concepts](https://www.google.com/search?q=https://reactrouter.com/en/main/start/concepts)

-----

### **Day 4: Fetching and Displaying Data in React**

  * **Today's Goal:** Connect your React components to the backend API to fetch and display the recipe data.
  * **Topics:**
      * **Data Fetching in `useEffect`:** The primary pattern for loading data when a component mounts.
      * **URL Parameters:** Using React Router's `useParams` hook to get the ID from the URL (e.g., in `/recipes/:id`).
      * **Conditional Rendering:** Displaying a "Loading..." message while data is being fetched.
  * **Tasks:**
    1.  **Build `RecipesListPage`:** In this component, use `useState` and `useEffect` to call your `GET /api/recipes` endpoint. Map over the returned array of recipes and display them as a list or a grid of cards.
    2.  **Make Cards Clickable:** Make each recipe card a `<Link>` that navigates to its detailed view, like `<Link to={`/recipes/${recipe.id}`}>`.
    3.  **Build `RecipeDetailPage`:** Create a new route for `/recipes/:id`. In the `RecipeDetailPage` component, use the `useParams` hook to get the `id`. Use that `id` to fetch data from your `GET /api/recipes/:id` endpoint and display all the recipe's details.
  * **Learning Resources:**
      * [React Docs - Fetching data with Effects](https://www.google.com/search?q=https://react.dev/learn/synchronizing-with-effects%23fetching-data)
      * [React Router Docs - `useParams` Hook](https://www.google.com/search?q=%5Bhttps://reactrouter.com/en/main/hooks/use-params%5D\(https://reactrouter.com/en/main/hooks/use-params\))

-----

### **Day 5: Handling Forms and Data Submission**

  * **Today's Goal:** Build the form for adding new recipes and handle the `POST` request to the backend.
  * **Topics:**
      * **Controlled Components:** The React pattern of linking form input values to component state.
      * **Handling Form Submission:** Using the `onSubmit` event handler.
      * **Making `POST` Requests:** Using `fetch` with the appropriate method, headers, and body to send JSON data to your API.
      * **Programmatic Navigation:** Using the `useNavigate` hook from React Router to redirect the user after a successful form submission.
  * **Tasks:**
    1.  **Build the Form:** In your `AddRecipePage` component, create a form with inputs for title, ingredients, instructions, etc.
    2.  **Control the Inputs:** For each input, use `useState` to manage its value.
    3.  **Implement `handleSubmit`:** Write the function that will be called on form submission. It should prevent the default form behavior, package the form data into an object, and send it to your `POST /api/recipes` endpoint.
    4.  **Redirect on Success:** After a successful API response, use the `useNavigate` hook to redirect the user to the main recipes page (`/recipes`) to see their newly added recipe.
  * **Learning Resources:**
      * [React Docs - Sharing State Between Components](https://react.dev/learn/sharing-state-between-components) (covers lifting state up, useful for forms)
      * [React Router Docs - `useNavigate` Hook](https://www.google.com/search?q=%5Bhttps://reactrouter.com/en/main/hooks/use-navigate%5D\(https://reactrouter.com/en/main/hooks/use-navigate\))

-----

### **Day 6: Improving User Experience (UX)**

  * **Today's Goal:** Make your application feel more professional by handling loading and error states.
  * **Topics:**
      * **Loading State:** Tracking when an API request is in progress.
      * **Error State:** Tracking when an API request fails.
      * **UI Feedback:** Providing clear visual feedback to the user (e.g., showing a spinner, displaying an error message).
  * **Tasks:**
    1.  **Add Loading State:** In your components that fetch data, add a new piece of state like `const [isLoading, setIsLoading] = useState(true);`. Set it to `true` before the fetch, and `false` inside a `.finally()` block. Use this state to conditionally render a loading indicator.
    2.  **Add Error State:** Add an error state: `const [error, setError] = useState(null);`. In your `catch` block, set the error message. Conditionally render the error message to the user if it's not `null`.
    3.  **Refactor Fetching Logic (Optional Challenge):** Create a custom hook called `useFetch` that encapsulates the logic for fetching data, including the loading and error states. This is a great way to practice writing reusable code.
  * **Learning Resources:**
      * [A simple guide to custom hooks](https://www.google.com/search?q=a+simple+guide+to+custom+hooks+react)

-----

### **Day 7: Review, Refactor, and Document**

  * **Today's Goal:** Consolidate your learning, clean up your project, and ensure it's well-documented.
  * **Tasks:**
    1.  **Refactor:** Read through your code. Are there any large components that could be broken down into smaller ones? Is your code easy to understand?
    2.  **Add Comments:** Add comments where the logic is complex. Explain *why* you did something, not just *what* it does.
    3.  **Populate More Data:** Use your app's form (or Postman) to add at least 5-6 more recipes with real data and images to make your app look complete.
    4.  **Update README:** This is your most complex project yet. Update the `README.md` in the root of your project. Include:
          * A brief description of the application.
          * Instructions on how to install dependencies and run the backend server.
          * Instructions on how to install dependencies and run the frontend development server.

Fantastic job\! You've now built a multi-page, data-driven application that mirrors the architecture of many real-world websites. You have a solid grasp of the full-stack development loop.

Next week, we dive into one of the most critical topics in web development: Authentication & Security. Let me know when you're ready for **Week 6**.
