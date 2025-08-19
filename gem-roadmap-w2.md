Of course\! Let's get into Week 2.

This week is a big one. We're moving from static websites to dynamic, interactive user interfaces with React. We'll use modern tools like Vite to make the development process fast and efficient. By the end of this week, you'll have built a proper single-page application (SPA).

Here's the detailed plan for **Week 2: React & Modern Frontend Tooling**.

-----

## Week 2: React & Modern Frontend Tooling

**Project of the Week:** An interactive "Movie Finder" application. Users can search for movies, and the app will fetch and display the results from a live API.

**Key Concepts:** Component-Based Architecture, JSX, State vs. Props, Hooks (`useState`, `useEffect`), API Data Fetching.

-----

### **Day 1: Intro to React & Setup with Vite**

  * **Today's Goal:** Understand what React is and set up a new project using the modern build tool, Vite.
  * **Topics:**
      * **What is React?** Learn about the component-based architecture and the virtual DOM. Understand why it's a library, not a framework.
      * **Modern Tooling:** Why use Vite over older tools like Create React App (hint: speed\!).
      * **Project Setup:** Learn the commands to create a new React project with Vite.
  * **Tasks:**
    1.  **Install Node.js:** If you haven't already, install the LTS version of Node.js, which includes `npm`.
    2.  **Create Project:** Open your terminal and run `npm create vite@latest your-movie-app -- --template react`.
    3.  **Explore:** `cd` into the new project directory, run `npm install`, and then `npm run dev` to start the development server.
    4.  **Cleanup:** Open the project in VS Code. Clean up the default `App.jsx` and `App.css` files, leaving a simple "Hello World" to start fresh.
  * **Learning Resources:**
      * [React Docs: Main Concepts](https://react.dev/learn)
      * [Vite Docs: Scaffolding Your First Project](https://vitejs.dev/guide/)

-----

### **Day 2: JSX & Components**

  * **Today's Goal:** Learn how to write UI with JSX and break the application down into reusable components.
  * **Topics:**
      * **JSX:** Understand this JavaScript syntax extension. Learn how to embed JavaScript expressions inside your markup.
      * **Functional Components:** The modern standard for writing React components.
      * **Component Composition:** The practice of building larger components from smaller, specialized ones.
  * **Tasks:**
    1.  **Plan Components:** On paper or in a notes app, sketch out the UI for your movie app and identify the components you'll need (e.g., `Header`, `SearchBar`, `MovieList`, `MovieCard`).
    2.  **Create Components:** In your `src` folder, create a new `components` directory. Inside, create the files for each component you planned.
    3.  **Build Static UI:** Build the static version of your app. In `App.jsx`, import and arrange your new components. Use placeholder data for now (e.g., hardcode a movie title and poster in `MovieCard`).
  * **Learning Resources:**
      * [React Docs: Writing Markup with JSX](https://react.dev/learn/writing-markup-with-jsx)
      * [React Docs: Your First Component](https://react.dev/learn/your-first-component)

-----

### **Day 3: State & Props**

  * **Today's Goal:** Make your components dynamic by managing their internal data (state) and passing data between them (props).
  * **Topics:**
      * **Props:** Learn how to pass data from a parent component to a child component.
      * **`useState` Hook:** The fundamental hook for adding state to a functional component.
  * **Tasks:**
    1.  **Pass Props:** In `App.jsx`, create a hardcoded array of movie objects. Pass this data down to the `MovieList` component as a prop.
    2.  **Render Props:** Inside `MovieList`, receive the prop and use the `.map()` method to render a `MovieCard` for each movie in the array, passing the individual movie data down as props to each `MovieCard`.
    3.  **Introduce State:** In your `SearchBar` component, use `useState` to create a state variable that will hold the user's search query.
  * **Learning Resources:**
      * [React Docs: Passing Props to a Component](https://react.dev/learn/passing-props-to-a-component)
      * [React Docs: `useState` Hook](https://www.google.com/search?q=%5Bhttps://react.dev/reference/react/useState%5D\(https://react.dev/reference/react/useState\))

-----

### **Day 4: Handling User Input & Events**

  * **Today's Goal:** Capture user input and make the application respond to events like button clicks.
  * **Topics:**
      * **Event Handling:** Learn how to use event handlers like `onClick` and `onChange`.
      * **Controlled Components:** The standard React pattern for handling form inputs, where the component's state is the "single source of truth."
  * **Tasks:**
    1.  **Control the Input:** In `SearchBar`, link the `useState` variable to the `<input>` element's `value` and `onChange` attributes. This makes it a controlled component.
    2.  **Handle Form Submission:** Create a function to handle the form submission. For now, just `console.log` the search query from your state when the form is submitted.
    3.  **Lift State Up:** The search query state is in `SearchBar`, but `App.jsx` needs it to fetch data. "Lift the state up" by moving the `useState` for the query into `App.jsx` and passing the state and the setter function down to `SearchBar` as props.
  * **Learning Resources:**
      * [React Docs: Responding to Events](https://react.dev/learn/responding-to-events)
      * [React Docs: Sharing State Between Components](https://react.dev/learn/sharing-state-between-components)

-----

### **Day 5: The Effect Hook & Fetching API Data**

  * **Today's Goal:** Fetch real movie data from an external API when the user performs a search.
  * **Topics:**
      * **`useEffect` Hook:** Learn how to perform "side effects" (like fetching data) in your components.
      * **API Fetching:** Use the browser's `fetch` API to make network requests.
      * **Async/Await:** Use modern JavaScript syntax to handle asynchronous operations cleanly.
  * **Tasks:**
    1.  **Get API Key:** Sign up for a free API key from [The Movie Database (TMDB)](https://www.themoviedb.org/signup).
    2.  **Create Fetch Function:** In `App.jsx`, create an `async` function that takes a search query, constructs the TMDB API URL, and fetches the data.
    3.  **Implement `useEffect`:** Use `useEffect` to call your fetch function whenever the search query state changes.
    4.  **Store API Data:** Create a new piece of state using `useState` to store the array of movies returned from the API. Update this state with the data you fetch.
  * **Learning Resources:**
      * [React Docs: `useEffect` Hook](https://www.google.com/search?q=%5Bhttps://react.dev/reference/react/useEffect%5D\(https://react.dev/reference/react/useEffect\))
      * [MDN - Using the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

-----

### **Day 6: Conditional Rendering & Styling**

  * **Today's Goal:** Improve the user experience by handling loading/error states and applying a professional design with Tailwind CSS.
  * **Topics:**
      * **Conditional Rendering:** Show different UI elements based on the application's state (e.g., show a "Loading..." message).
      * **Styling in React:** Apply Tailwind CSS classes to your JSX elements.
  * **Tasks:**
    1.  **Add Loading State:** Create a `loading` state (`useState`). Set it to `true` before you start an API fetch and `false` when it completes. Use this state to conditionally render a loading indicator.
    2.  **Style Components:** Go through each of your components and apply Tailwind classes to make them look like your initial sketch. Use Flexbox or Grid for layouts.
    3.  **Display Movie Data:** Ensure your `MovieCard` component correctly displays the title, release date, and poster image from the API data.
  * **Learning Resources:**
      * [React Docs: Conditional Rendering](https://react.dev/learn/conditional-rendering)
      * [Tailwind CSS Docs](https://tailwindcss.com/docs) (Use this as a reference for classes)

-----

### **Day 7: Refactor, Review, & Deploy**

  * **Today's Goal:** Clean up your code, write documentation, and deploy your new React application.
  * **Topics:**
      * **Component Refactoring:** Breaking down components that have become too large or complex.
      * **Deployment:** Deploying a React application built with Vite.
  * **Tasks:**
    1.  **Code Review:** Read through your entire application. Is the code easy to understand? Are component names clear?
    2.  **Refactor:** If your `App.jsx` is getting crowded, consider moving the API fetching logic into a separate utility file.
    3.  **Update README:** Write a high-quality `README.md` for your project on GitHub.
    4.  **Deploy:** Deploy your site to Netlify or Vercel. The process is very similar to last week, but these platforms will automatically detect it's a Vite project and run the correct build commands.
  * **Learning Resources:**
      * [Vercel Docs: Deploying a Vite Project](https://www.google.com/search?q=https://vercel.com/guides/deploying-vite-with-vercel)

You're making incredible progress\! Finishing this week means you can build and deploy modern, data-driven frontend applications. Let me know when you're ready for **Week 3: Backend Development with Node.js & Express**.

This [React Full Course for free ⚛️ (2024)](https://www.youtube.com/watch?v=CgkZ7MvWUAA) video provides a comprehensive introduction to React, covering many of the core concepts you'll be learning this week.
http://googleusercontent.com/youtube_content/1
