Of course. Let's get into Week 10.

You've learned how to build and deploy a functional application. Now, you need to learn how to make it scale. This week, you'll be introduced to the principles of **System Design**—the art of architecting complex, high-performance systems. You'll learn how to handle thousands of users by incorporating essential components like caching.

Here is the detailed, day-by-day plan for **Week 10**.

-----

## Week 10: System Design & Caching

**Project of the Week:** You will design and build the backend for a high-performance "Link Shortener" service (like bit.ly). The core challenge is to make the redirection lightning-fast using a caching layer with Redis.

**Key Concepts:** System Design, Scalability, Latency, Availability, Load Balancing, Database Replication, Caching, Redis.

-----

### **Day 1: Introduction to System Design**

  * **Today's Goal:** Understand the "big picture" of how large-scale web applications are structured.
  * **Topics:**
      * **What is System Design?** The process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements.
      * **Key Principles:**
          * **Scalability:** The ability of a system to handle a growing amount of work.
          * **Availability:** The measure of a system's uptime. Often discussed in "nines" (e.g., 99.99% available).
          * **Latency:** The delay between a user's action and the web application's response.
      * **Core Building Blocks:** A high-level overview of Clients, Servers, Databases, Load Balancers, and Caches.
  * **Tasks:**
    1.  **Watch System Design Primers:** Watch introductory videos on YouTube about system design interviews and basic concepts. Search for "System Design Fundamentals."
    2.  **Whiteboard Exercise:** On paper or with a diagramming tool (like Excalidraw), draw the architecture of the blog application you built the API for in Week 3. Start with a single user, a single server, and a single database. Think about where the bottlenecks would be if you suddenly had a million users.
  * **Learning Resources:**
      * [System Design Primer on GitHub](https://github.com/donnemartin/system-design-primer) (Read the "System Design Topics" section)

-----

### **Day 2: Core Scalability Patterns**

  * **Today's Goal:** Learn two fundamental techniques for scaling an application.
  * **Topics:**
      * **Horizontal vs. Vertical Scaling:** **Vertical scaling** means adding more power (CPU, RAM) to an existing server. **Horizontal scaling** means adding more servers to your pool of resources. Horizontal is generally preferred for web apps.
      * **Load Balancing:** A component that acts as a "traffic cop," distributing incoming network traffic across multiple servers. This improves responsiveness and availability.
      * **Database Replication:** The process of creating and maintaining multiple copies of a database. A common pattern is **Primary-Replica**, where all writes go to the primary database, and reads are distributed across the replicas, reducing the load on the primary.
  * **Tasks:**
    1.  **Redraw Your Diagram:** Take your blog architecture diagram from yesterday and add a load balancer and multiple application servers.
    2.  **Add Database Replicas:** Modify the diagram again to show a primary database and several read replicas. Draw arrows to show the flow of write traffic vs. read traffic.
  * **Learning Resources:**
      * [What is a Load Balancer?](https://www.google.com/search?q=https://www.cloudflare.com/learning/cdn/what-is-a-load-balancer/)
      * [Understanding Database Replication](https://www.google.com/search?q=https://www.digitalocean.com/community/tutorials/understanding-database-replication-in-mysql) (Concepts apply to PostgreSQL too)

-----

### **Day 3: Caching with Redis**

  * **Today's Goal:** Understand caching as a primary tool for improving performance and get hands-on with Redis.
  * **Topics:**
      * **The Principle of Caching:** Storing the results of expensive operations (like database queries) in a faster, temporary data store (memory) to serve future requests more quickly.
      * **Redis:** An extremely fast, open-source, in-memory key-value data store. Perfect for caching.
      * **Cache-Aside Strategy:** A common caching pattern. Your application logic is:
        1.  Look for data in the cache.
        2.  If it's there (a **cache hit**), return it.
        3.  If it's not (a **cache miss**), fetch it from the database, store it in the cache, and then return it.
  * **Tasks:**
    1.  **Install Redis:** The easiest way is with Docker: `docker run -p 6379:6379 --name my-redis -d redis`.
    2.  **Use `redis-cli`:** Connect to your Redis instance using the command-line interface.
    3.  **Practice Commands:** Use basic Redis commands:
          * `SET user:1 '{"name": "Alice"}'`
          * `GET user:1`
          * `EXPIRE user:1 10` (set a 10-second expiration)
          * `TTL user:1` (check the time to live)
  * **Learning Resources:**
      * [Redis Docs - Introduction to Redis](https://redis.io/docs/about/)
      * [Try Redis in your browser](https://www.google.com/search?q=https://try.redis.io/)

-----

### **Day 4: Designing the Link Shortener Service**

  * **Today's Goal:** Apply system design principles to plan out the week's project before writing any code.
  * **Topics:**
      * **Clarifying Requirements:** Defining what the service must do (functional) and how it must perform (non-functional).
      * **API Design (Endpoints):** `POST /api/url` to create a short link and `GET /:shortCode` to handle the redirect.
      * **Data Modeling:** How to store the links in PostgreSQL (`id`, `shortCode`, `originalUrl`).
      * **Hashing Algorithm:** How to generate a unique, short, and non-predictable code for each URL. A simple approach is to use a library that generates short, unique IDs (like `nanoid`) or to encode the database row ID into a Base62 string.
  * **Tasks:**
    1.  **Write Down Requirements:** List the functional and non-functional requirements for your service. The key non-functional requirement is **low-latency redirects**.
    2.  **Design the Schema:** Define the Prisma schema for your `Link` model.
    3.  **Draw the Architecture:** Create a complete system design diagram for the link shortener. It should include the client, the API, the Redis cache, and the PostgreSQL database. Show the data flow for a redirect, indicating the cache-aside logic.

-----

### **Day 5: Building the Core Backend Service**

  * **Today's Goal:** Implement the basic functionality of the link shortener without the caching layer.
  * **Tasks:**
    1.  **Project Setup:** Create a new Node.js, Express, and Prisma backend project.
    2.  **Install `nanoid`:** Run `npm install nanoid` to help generate short, unique strings.
    3.  **Implement `POST /api/url`:**
          * Take a long URL from the request body.
          * Generate a unique `shortCode` using `nanoid`.
          * Save the `shortCode` and `originalUrl` to your PostgreSQL database using Prisma.
          * Return the full short URL to the user (e.g., `http://localhost:3001/your-code`).
    4.  **Implement `GET /:shortCode`:**
          * Take the `shortCode` from the URL parameters.
          * Look up the entry in the PostgreSQL database.
          * If found, use `res.redirect(302, link.originalUrl)` to redirect the user.
          * If not found, return a 404 error.
    5.  **Test with Postman:** Ensure both endpoints are working correctly.

-----

### **Day 6: Integrating the Redis Cache Layer**

  * **Today's Goal:** Implement the cache-aside strategy to dramatically speed up the redirect endpoint.
  * **Tasks:**
    1.  **Install Redis Client:** In your backend project, run `npm install ioredis`.
    2.  **Connect to Redis:** In your application, create a new Redis client instance.
    3.  **Refactor the Redirect Logic:** Modify your `GET /:shortCode` controller to implement the cache-aside pattern:
          * First, try to `redis.get(shortCode)`.
          * **If a URL is returned (cache hit):** Log "Cache Hit" and redirect immediately.
          * **If `null` is returned (cache miss):**
              * Log "Cache Miss."
              * Query the PostgreSQL database as before.
              * If a link is found in the DB, use `redis.set(shortCode, link.originalUrl, 'EX', 86400)` to save it in the cache for 24 hours.
              * Perform the redirect.
  * **Learning Resources:**
      * [`ioredis` npm package](https://www.google.com/search?q=%5Bhttps://www.npmjs.com/package/ioredis%5D\(https://www.npmjs.com/package/ioredis\))

-----

### **Day 7: Performance Benchmarking & Review**

  * **Today's Goal:** Prove that your caching implementation works by measuring the performance improvement.
  * **Topics:**
      * **Load Testing:** The process of simulating high traffic to your application to see how it performs under stress.
      * **Benchmarking Tools:** Using a simple command-line tool like `autocannon`.
  * **Tasks:**
    1.  **Install `autocannon`:** Run `npm install -g autocannon`.
    2.  **Benchmark Without Cache:** Temporarily comment out your Redis logic. Create a short link and then run a benchmark against it: `autocannon http://localhost:3001/your-code`. Note the requests/sec.
    3.  **Benchmark With Cache:** Re-enable your Redis logic. Run the benchmark command again. The first run will warm up the cache. Run it a second time.
    4.  **Compare Results:** Observe the dramatic increase in requests per second and the decrease in latency. This is the tangible result of your system design choice.
    5.  **Document Your Design:** In your project's `README.md`, embed your system design diagram. Explain your architectural choices and include the results of your performance benchmarks.

You've now moved beyond just being a coder to thinking like an architect. You understand how to design systems that are not only functional but also fast and scalable. This is a critical skill that sets senior developers apart.

Next, you'll learn how to build with one of the most popular and powerful full-stack frameworks in the world. Let me know when you're ready for **Week 11**.
