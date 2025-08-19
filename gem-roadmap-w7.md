Excellent, let's move on to Week 7.

So far, you've managed application state with `useState`, `useContext`, and `useEffect`. This works, but as apps grow, managing data fetching, caching, and loading states can become messy and repetitive. This week, you'll learn the modern, professional way to handle data from your server and distinguish it from data that just lives in your UI.

Here is the detailed, day-by-day plan for **Week 7**.

-----

## Week 7: Advanced State Management & Data Fetching

**Project of the Week:** A "Project Management Tool" (a Trello clone). You'll build a board with lists and draggable cards. This project will heavily feature a clean separation between server state (the board data) and client state (UI interactions).

**Key Concepts:** Client-side vs. Server-side State, Caching, Server State Management, Global State Management.

-----

### **Day 1: The Two Types of State & Intro to React Query**

  * **Today's Goal:** Understand the fundamental difference between client and server state and why they need different management tools.
  * **Topics:**
      * **Client State:** Data that your application owns and controls directly. Examples: Is a modal open? The current value of a form input. The current theme (dark/light mode).
      * **Server State:** Data that lives on a server and you don't directly own. It's fetched asynchronously, can be updated by others, and can become "stale." Examples: User profiles, blog posts, recipe data.
      * **Why `useEffect` for Data Fetching Falls Short:** It doesn't handle caching, background updates, or de-duplicating requests. This leads to a lot of boilerplate code.
      * **Introduction to TanStack Query (React Query):** Learn what it is—a library that excels at managing server state. It's not a global state manager; it's a server state and cache manager.
  * **Tasks:**
    1.  **Project Setup:** Create a new `trello-clone` project with `backend` and `frontend` folders.
    2.  **Backend Data Modeling:** In your backend, set up a new project. In `schema.prisma`, model your data. You'll likely need three models: `Board`, `List` (which has a relation to a Board), and `Card` (which has a relation to a List).
    3.  **Read and Conceptualize:** Read the first few pages of the TanStack Query documentation to solidify your understanding of its philosophy.
  * **Learning Resources:**
      * [TanStack Query Docs - Overview & Motivation](https://tanstack.com/query/latest/docs/react/overview)
      * [Client-Side State vs Server-Side State](https://www.google.com/search?q=Client-Side+State+vs+Server-Side+State)

-----

### **Day 2: Fetching Data with `useQuery`**

  * **Today's Goal:** Replace your manual `fetch` logic with React Query's `useQuery` hook and experience its benefits immediately.
  * **Topics:**
      * **`QueryClientProvider`:** Setting up the provider at the top level of your application.
      * **The `useQuery` hook:** Its core components: a unique `queryKey` and a `queryFn` (your fetcher function).
      * **Query Statuses:** The handy boolean values `useQuery` returns: `isLoading`, `isError`, `isSuccess`.
  * **Tasks:**
    1.  **Build Backend API:** Create the backend endpoints to `GET` all lists and all cards for a specific board.
    2.  **Install React Query:** In your frontend, run `npm install @tanstack/react-query`.
    3.  **Set Up Provider:** Wrap your `<App />` component with `<QueryClientProvider>`.
    4.  **Refactor a Fetch:** Create a component for your main board view. Instead of `useEffect` and `useState`, use the `useQuery` hook to fetch your lists and cards.
    5.  **Render the UI:** Use the `isLoading` and `isError` states to show loading/error messages, and map over the `data` to render your lists and cards.
    6.  **Install & Use Devtools:** Install `@tanstack/react-query-devtools` and add them to your app. Open them and watch how React Query caches your data.
  * **Learning Resources:**
      * [TanStack Query Docs - Important Defaults](https://www.google.com/search?q=https://tanstack.com/query/latest/docs/react/important-defaults)
      * [TanStack Query Docs - Devtools](https://tanstack.com/query/latest/docs/react/devtools)

-----

### **Day 3: Changing Data with `useMutation`**

  * **Today's Goal:** Learn how to create, update, and delete server data using the `useMutation` hook.
  * **Topics:**
      * **What is a Mutation?** Any action that changes data on the server.
      * **The `useMutation` hook:** How it provides functions and status variables (`isPending`, `isError`) for performing these actions.
      * **Invalidating Queries:** The magic of React Query. Learn how to tell React Query that certain data is now stale after a mutation, causing it to automatically refetch and keep the UI in sync.
  * **Tasks:**
    1.  **Build Backend Endpoints:** Create the `POST` endpoints on your server for creating a new list and creating a new card.
    2.  **Implement "Add List":** Create a form for adding a new list. Wire it up to a `useMutation` hook.
    3.  **Invalidate on Success:** In the `onSuccess` callback of your mutation, use the `queryClient` to invalidate the query for "all lists." Watch your UI magically update with the new list without any manual state management.
    4.  **Implement "Add Card":** Do the same for adding a new card to a specific list.
  * **Learning Resources:**
      * [TanStack Query Docs - Mutations](https://tanstack.com/query/latest/docs/react/guides/mutations)
      * [TanStack Query Docs - Query Invalidation](https://tanstack.com/query/latest/docs/react/guides/query-invalidation)

-----

### **Day 4: Global Client State with Zustand**

  * **Today's Goal:** Learn to manage simple global *client* state without the complexity of Redux or the performance issues of Context for high-frequency updates.
  * **Topics:**
      * **When to Use a Global Store:** When you need to share client state between components that are far apart in the component tree (e.g., theme, user settings, UI state).
      * **Zustand:** A minimalist, fast, and unopinionated state management library.
      * **Creating a Store:** How to define a simple "store" with state and actions to modify that state.
  * **Tasks:**
    1.  **Install Zustand:** In your frontend, run `npm install zustand`.
    2.  **Create a UI Store:** Create a new store (e.g., `store/uiStore.js`). Define a piece of state in it, for example, `isAddCardFormOpenForListId: null`.
    3.  **Define Actions:** Create actions in the store to `openAddCardForm(listId)` and `closeAddCardForm()`.
    4.  **Use the Store:** In your `List` component, use the store to determine whether to show the "Add Card" form. The "Add Card" button will call the `open` action, and the form's cancel button will call the `close` action. Notice how you don't need any providers.
  * **Learning Resources:**
      * [Zustand GitHub Repository (Read the README)](https://github.com/pmndrs/zustand)

-----

### **Day 5 & 6: Implementing Drag-and-Drop**

  * **Today's Goal:** Implement the core interactive feature of the Trello clone: dragging and dropping cards.
  * **Topics:**
      * **Drag-and-Drop Libraries:** Introduction to a modern library like `@dnd-kit/core`.
      * **Core Concepts:** Draggables, Droppables, and Sensors.
      * **Handling the `onDragEnd` event:** This is where you'll get the information about what was dragged and where it was dropped.
      * **Updating the Backend:** Firing off a mutation to the backend to persist the new position or list of the card.
  * **Tasks for Day 5 (Setup & Within-List Drag):**
    1.  **Install `@dnd-kit`:** Run `npm install @dnd-kit/core @dnd-kit/sortable`.
    2.  **Build Backend Endpoint:** Create a `PUT /api/cards/:id/move` endpoint that can update a card's `listId` and/or its position.
    3.  **Wrap Your App:** Set up the `<DndContext>` provider.
    4.  **Make Cards Draggable:** Wrap your `Card` component with the `useSortable` hook.
    5.  **Make Lists Droppable:** Wrap your `List` component to create a droppable area.
    6.  **Implement Drag Within a List:** Write the `onDragEnd` handler to reorder cards within the same list. For now, just log the result to the console.
  * **Tasks for Day 6 (Cross-List Drag & Backend Update):**
    1.  **Implement Cross-List Drag:** Update your `onDragEnd` handler to detect when a card moves from one list to another.
    2.  **Create a Mutation:** Set up a `useMutation` hook to call your `PUT /api/cards/:id/move` endpoint.
    3.  **Trigger Mutation:** Call your mutation from the `onDragEnd` handler, passing the card ID and its new list ID.
    4.  **Optimistic Updates (Challenge):** Try implementing an optimistic update for the move. Reorder the cards in the UI state *immediately* in the `onDragEnd` handler, before the mutation even starts. Use the `onMutate` and `onError` callbacks from `useMutation` to handle rollbacks if the server call fails.
  * **Learning Resources:**
      * [`@dnd-kit` Documentation](https://www.google.com/search?q=%5Bhttps://docs.dndkit.com/%5D\(https://docs.dndkit.com/\))
      * [TanStack Query Docs - Optimistic Updates](https://tanstack.com/query/latest/docs/react/guides/optimistic-updates)

-----

### **Day 7: Review and Final Polish**

  * **Today's Goal:** Solidify your understanding of the week's concepts and clean up your feature-rich application.
  * **Tasks:**
    1.  **Explore Devtools:** Open the React Query Devtools and watch what happens as you perform mutations. See how queries are marked as stale and then refetched.
    2.  **Refactor:** Look at your data fetching logic. Is it clean? Can you abstract any fetcher functions into a separate `api.js` file?
    3.  **Add Loading States:** Your mutations also have loading states (`isPending`). Use this to provide visual feedback, for example, by slightly graying out a card while its move is being saved to the server.
    4.  **Update README:** This is your most complex frontend project yet. Document the state management strategy. Explain the separation of server state (React Query) and client state (Zustand) and why that's a powerful pattern.

Incredible work. You've now gone beyond basic data fetching and learned the modern, scalable patterns for state management that are used in top-tier tech companies. This knowledge separates you from junior developers who only know `useEffect`.

You are now prepared to build truly complex and performant applications. Let me know when you're ready to tackle **Week 8: WebSockets & Testing**.
