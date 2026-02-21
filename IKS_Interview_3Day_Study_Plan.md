# IKS Health – Product Engineer Interview Prep
## 3-Day Intensive Study Plan
**Role:** Product Engineer | **Exp:** 3–5 Years | **Location:** Mumbai

---

# DAY 1 – FRONTEND FOCUS
## React.js | JavaScript/TypeScript | Redux | UI Performance

---

## KEY CONCEPTS TO REVISE

### 1. React Hooks
- **useState** – manage local component state
- **useEffect** – handle side effects (API calls, subscriptions, timers). Runs after render. Cleanup with return function.
- **useContext** – share data without prop drilling
- **useRef** – access DOM elements or keep mutable values that don't cause re-render
- **useCallback** – memoize a function so it doesn't re-create on every render
- **useMemo** – memoize a computed value (expensive calculation)
- **useReducer** – like Redux but local to component; good for complex state logic
- **Custom Hooks** – extract reusable logic into a function starting with "use"

> **Quick Note:** `useCallback` is for functions, `useMemo` is for values. Both help with performance by avoiding unnecessary re-renders.

---

### 2. Redux
- **Store** – single source of truth for app state
- **Action** – plain object describing what happened (`{ type: 'INCREMENT', payload: 1 }`)
- **Reducer** – pure function that takes state + action, returns new state
- **Dispatch** – send an action to the store
- **Selector** – read data from the store
- **Redux Toolkit (RTK)** – modern way; use `createSlice`, `createAsyncThunk`
- **RTK Query** – built-in data fetching + caching in Redux Toolkit

> **Flow:** UI dispatches Action → Reducer updates Store → Component re-renders with new state

---

### 3. React Performance Optimization
- **React.memo** – prevent re-render of a component if props haven't changed
- **Code Splitting** – `React.lazy` + `Suspense` to load components on demand
- **Virtualization** – render only visible items in long lists (react-window / react-virtualized)
- **Avoid anonymous functions in JSX** – they create new references on every render
- **Key prop in lists** – always use stable unique keys, never use array index
- **Debounce/Throttle** – for search inputs or scroll events
- **Bundle size** – tree shaking, analyze with webpack-bundle-analyzer

---

### 4. JavaScript Essentials
- **Closures** – function remembers its outer scope even after outer function returns
- **Promises & Async/Await** – handle asynchronous code cleanly
- **Event loop** – JS is single-threaded; async tasks go to the task queue
- **Prototypal inheritance** – objects inherit from other objects via prototype chain
- **ES6+ features** – destructuring, spread/rest, arrow functions, template literals, optional chaining (`?.`), nullish coalescing (`??`)
- **this keyword** – depends on how function is called; arrow functions don't have their own `this`
- **Array methods** – `map`, `filter`, `reduce`, `find`, `some`, `every`

---

### 5. TypeScript Basics
- **Type annotations** – `let name: string = "John"`
- **Interfaces vs Types** – interfaces are extendable, types are more flexible (can use unions)
- **Generics** – reusable code with type parameters: `function identity<T>(arg: T): T`
- **Enums** – named constants
- **Type narrowing** – using `typeof`, `instanceof`, or custom type guards
- **Utility types** – `Partial<T>`, `Required<T>`, `Pick<T, K>`, `Omit<T, K>`

---

### 6. Responsive Design & Cross-platform
- **CSS Flexbox & Grid** – layout systems
- **Media queries** – adjust styles based on screen size
- **Mobile-first approach** – design for small screens first, then scale up
- **CSS-in-JS** – styled-components or Emotion for component-level styles
- **Accessibility (a11y)** – semantic HTML, ARIA attributes, keyboard navigation

---

## INTERVIEW QUESTIONS – DAY 1

### Q1. Can you explain the difference between `useCallback` and `useMemo`?

"Sure. Both are hooks for performance optimization, but they serve different purposes. `useMemo` is used to memoize a computed value — so if you have a heavy calculation, it won't re-run unless its dependencies change. `useCallback` on the other hand is used to memoize a function itself — so the function reference stays the same across renders. This is useful when you're passing a callback to a child component wrapped in `React.memo`, because if the function reference changes every render, the child will re-render unnecessarily. I've used `useCallback` in list components where I was passing an `onDelete` handler to multiple child items."

---

### Q2. How does Redux work? Can you walk me through the data flow?

"Redux follows a one-directional data flow. When a user does something — say clicks a button — the component dispatches an action, which is just a plain JavaScript object with a `type` field and optional `payload`. This action goes to the reducer, which is a pure function that takes the current state and the action, and returns a new state. The store gets updated with this new state, and any components that are subscribed to that part of the store will automatically re-render with the new data. In modern projects, I use Redux Toolkit, which makes this cleaner with `createSlice` and `createAsyncThunk` for async operations."

---

### Q3. What is the difference between `useEffect` with an empty dependency array vs no dependency array?

"Good question. If you pass an empty array `[]`, `useEffect` runs only once — after the first render. It's basically like `componentDidMount` in class components. If you don't pass any array at all, `useEffect` runs after every render — which can cause issues if you're not careful about infinite loops. If you pass specific values in the array, the effect runs whenever those values change. I always make sure to include the correct dependencies and also return a cleanup function when I'm setting up subscriptions or timers."

---

### Q4. How do you optimize a React application that is feeling slow?

"I usually start by profiling with React DevTools to find which components are re-rendering unnecessarily. The most common fix I've used is wrapping components with `React.memo` so they don't re-render unless props change. I also use `useCallback` and `useMemo` to stabilize function references and heavy calculations. For large lists, I use virtualization libraries like `react-window` so only visible items are in the DOM. For initial load time, I do code splitting with `React.lazy` and `Suspense`. I also look at bundle size using `webpack-bundle-analyzer` and remove unused packages."

---

### Q5. What is the difference between controlled and uncontrolled components?

"In a controlled component, the form element's value is managed by React state. Every keystroke updates the state, and the input always reflects that state. In an uncontrolled component, the form element manages its own state internally in the DOM, and you use `useRef` to read the value when needed. I generally prefer controlled components because they give me more control — I can do validation on every change, and the state is the single source of truth."

---

### Q6. How does JavaScript's event loop work?

"JavaScript is single-threaded, meaning it can only do one thing at a time. The event loop is what allows JavaScript to handle async operations without blocking. When you call something like `setTimeout` or a `fetch` request, that gets offloaded to the browser's Web APIs. Meanwhile, the main thread continues executing. When the async operation finishes, its callback is placed in the task queue. The event loop continuously checks — when the call stack is empty, it picks up the next task from the queue and runs it. This is why `setTimeout(fn, 0)` doesn't run immediately — it waits for the call stack to clear."

---

### Q7. What is a closure in JavaScript? Give an example.

"A closure is when a function has access to its outer function's variables even after the outer function has finished executing. A classic example is a counter function — you have an outer function that initializes a count variable, and it returns an inner function that increments and returns that count. Each time you call the inner function, it still has access to that count variable. I've used closures for things like creating private state, or in event handlers where I need to capture a variable at the time the handler is created."

---

### Q8. Explain the virtual DOM and how React uses it.

"The virtual DOM is a lightweight in-memory representation of the actual DOM. When state or props change, React creates a new virtual DOM tree and compares it with the previous one — this process is called reconciliation or diffing. React figures out the minimal set of changes needed and then applies only those changes to the real DOM. This is much faster than directly manipulating the DOM for every change. The key prop in lists is important here because it helps React identify which items changed, were added, or removed during reconciliation."

---

### Q9. How do you handle API calls in React?

"I typically use `useEffect` to trigger API calls, with proper cleanup to avoid state updates on unmounted components. For the actual HTTP calls, I use Axios or the Fetch API. If the project uses Redux, I use `createAsyncThunk` from Redux Toolkit, which handles the pending, fulfilled, and rejected states automatically. For more complex data fetching with caching and background updates, I've used React Query, which is really powerful — it handles loading states, error states, and refetching automatically."

---

### Q10. What is the difference between `==` and `===` in JavaScript?

"Double equals does type coercion — so `'5' == 5` is true because JavaScript converts the string to a number before comparing. Triple equals is strict equality — it checks both value and type, so `'5' === 5` is false. I always use triple equals in my code to avoid unexpected behavior from type coercion. It's a common source of bugs if you're not careful."

---

### Q11. How do you implement lazy loading in React?

"React provides `React.lazy()` for this. You wrap your import in it — like `const MyComponent = React.lazy(() => import('./MyComponent'))` — and then wrap it in a `Suspense` component with a fallback UI like a spinner. This way, the component code is only downloaded when it's actually needed, reducing the initial bundle size and making the app load faster. I've used this for route-level code splitting — each page component loads only when the user navigates to it."

---

### Q12. What are React Hooks rules?

"There are two main rules. First, only call hooks at the top level — don't call them inside loops, conditions, or nested functions. This ensures hooks are always called in the same order on every render, which React relies on. Second, only call hooks from React function components or custom hooks — not from regular JavaScript functions. If I need to share stateful logic between components, I extract it into a custom hook."

---

## SCENARIO-BASED QUESTIONS – DAY 1

### S1. You have a dashboard with 10 widgets, each making its own API call. The page is loading slowly. How do you fix this?

"First, I'd look at whether all 10 API calls need to happen simultaneously on page load. Maybe some widgets can load data lazily — only when the user scrolls to them or interacts with them. For the ones that must load immediately, I'd use `Promise.all` to run them in parallel instead of sequentially. I'd also add loading skeletons so the UI feels responsive even while data is loading. On the backend side, I might talk to the team about creating a dashboard-specific aggregation endpoint that returns all widget data in one call. And I'd use caching — either React Query or a service worker — so repeated visits don't re-fetch everything."

---

### S2. A user reports that clicking a button multiple times causes duplicate API submissions. How do you handle this?

"This is a common issue with async operations. I'd disable the button as soon as the first click fires and re-enable it only after the API call resolves or rejects. I'd manage a loading state in React — `const [isSubmitting, setIsSubmitting] = useState(false)` — and set it to true on click, then false in the finally block. I'd also add debouncing to the click handler for extra safety. On the backend side, I'd recommend implementing idempotency keys — so even if a duplicate request somehow gets through, the server recognizes it and doesn't process it twice."

---

### S3. You need to build a real-time search feature that calls an API on every keystroke. What approach do you take?

"I'd definitely use debouncing here. Instead of calling the API on every keystroke, I'd wait until the user stops typing for, say, 300ms, and then make the call. I'd implement this with `useCallback` and a debounce utility. I'd also cancel the previous API call if a new one is triggered — with Axios, you can use a cancel token for this. This prevents a situation called race conditions where an older, slower response arrives after a newer one and overwrites the correct result. React Query also handles this really well with its built-in request deduplication."

---

### S4. You're asked to migrate a class-based React component to functional components with hooks. Walk me through your approach.

"I'd start by mapping each lifecycle method to its hook equivalent. `componentDidMount` becomes `useEffect` with an empty dependency array. `componentDidUpdate` becomes `useEffect` with specific dependencies. `componentWillUnmount` becomes the cleanup function returned inside `useEffect`. State declarations move from `this.state` to multiple `useState` calls or a `useReducer` if the state is complex. `this.setState` calls become the setter from `useState`. I'd make sure to extract any reusable logic into custom hooks. I'd also run all existing tests after the migration to make sure behavior is unchanged."

---

### S5. Your React app bundle size has grown to 5MB. The manager wants it under 1MB. How do you approach this?

"I'd start by analyzing the bundle with `webpack-bundle-analyzer` to see exactly what's taking up space. The most common culprits are large libraries like moment.js, lodash, or chart libraries. I'd replace moment.js with date-fns or dayjs, which are much smaller. For lodash, I'd import only the specific functions I need instead of the whole library. I'd implement route-level code splitting with `React.lazy`. I'd also enable gzip or Brotli compression on the server, which can reduce bundle size by 70%. Finally, I'd check if there are any unused dependencies and remove them."

---

## SYSTEM DESIGN QUESTIONS – DAY 1

### SD1. Design the frontend architecture for a healthcare dashboard that shows patient data from multiple sources.

"I'd start with a component hierarchy that separates concerns clearly. At the top level, I'd have a Dashboard layout component. Below that, independent widget components — vitals, appointments, medications — each managing their own data fetching state. For global state, I'd use Redux Toolkit — patient context, user authentication, and shared filters would live in the Redux store. Widget-specific data would use React Query, which gives us caching, background refresh, and error handling out of the box. I'd implement role-based rendering — doctors see different widgets than billing staff. For performance, lazy load widgets that are below the fold. I'd also think about WebSocket connections for real-time vitals data. The component library would be built on something like Ant Design or Material UI with a custom theme to match the brand."

---

### SD2. How would you structure a large React application for maintainability?

"I'd use a feature-based folder structure — instead of grouping by type (components, services, utils), group by feature. So you'd have a `patients` folder with its own components, hooks, API calls, and Redux slice. This makes it easier to navigate and delete features cleanly. I'd have a `shared` folder for truly reusable components and utilities. I'd enforce consistent patterns through ESLint rules and a PR checklist. For styling, I'd pick one approach — either CSS modules or styled-components — and stick with it. I'd also set up absolute imports so we don't have deeply nested relative paths like `../../../../utils`. Documentation via Storybook for the component library is also something I'd recommend."

---

### SD3. How would you implement state management for a multi-step form with complex validation?

"For a multi-step form, I'd use a combination of approaches. The form state — values, errors, touched fields — would be managed with React Hook Form, which is highly performant because it uses uncontrolled inputs under the hood. For the step navigation and overall form submission state, I'd use a local `useReducer` to model the state machine — which step are we on, is it submitting, did it succeed or fail. I wouldn't use global Redux for form state unless the data needs to persist when navigating away and coming back. I'd implement Yup for schema-based validation and connect it to React Hook Form. Each step would only validate its own fields before allowing the user to proceed."

---

## BEHAVIORAL QUESTIONS – DAY 1

### B1. Tell me about a time you improved the performance of a frontend application.

"In my previous project, our customer-facing portal was taking about 6 seconds to load. I profiled it and found that we were loading the entire application code upfront, including admin-only pages that regular users never see. I implemented route-based code splitting using React.lazy, which reduced the initial bundle by about 40%. I also found that a heavily used table component was re-rendering completely every time any data changed — I wrapped it with React.memo and memoized the data transformation logic with useMemo. Combined, these changes brought load time down to under 2 seconds, which the product team was really happy about."

---

### B2. Describe a time you had to push back on a design or product requirement.

"Our product manager once asked us to add 12 widgets to the main dashboard that would all load simultaneously. I raised a concern in sprint planning that this would significantly impact load time and user experience. I suggested an alternative — show the 4 most important widgets immediately, and let users customize which other widgets they want visible. I backed this with some research on dashboard usability. The PM appreciated the input, we aligned on a phased approach, and users actually rated the customizable dashboard higher in feedback surveys."

---

### B3. How do you handle code reviews? Have you ever had a major disagreement with a peer about code?

"I actually enjoy code reviews — they're one of the best ways to learn and maintain quality. I try to be specific in my feedback and always explain the 'why' behind suggestions rather than just saying 'change this.' I've had disagreements, yes. Once, a colleague wanted to store a large dataset directly in Redux global state, and I felt it belonged in local component state with React Query since it was only used in one feature. We had a good discussion, I explained the performance implications, and we ended up doing a small proof of concept. We went with my approach, but I made sure to document the reasoning so others would understand the decision later."

---

### B4. How do you stay updated with React and frontend ecosystem changes?

"I follow the React blog and the RFC discussions on GitHub, which gives me early visibility into upcoming features. I also follow a few engineers on Twitter who work on React and related tools. When I see something interesting — like when React 18 came out with concurrent features — I build a small demo project to understand it hands-on rather than just reading about it. I share what I learn with my team in our weekly tech sync. I also try to contribute small PRs to open source libraries when I find bugs or documentation gaps."

---

### B5. Tell me about a time you collaborated with a QA engineer to fix a tricky bug.

"We had a bug that only appeared in production and not in our staging environment. The QA engineer and I sat together and went through the reproduction steps carefully. He helped me narrow down the exact sequence of actions that triggered it. I added detailed logging and deployed it to a production-like environment. We eventually found it was a race condition — two API calls were resolving in a different order in production due to network latency. I fixed it using proper state management with useEffect cleanup functions. After that, I worked with the QA engineer to write an integration test that would catch similar race conditions in future."

---

## DAY 1 QUICK REVISION SUMMARY

| Topic | Remember This |
|-------|---------------|
| useEffect | `[]` = once, no array = every render, `[dep]` = when dep changes |
| useMemo vs useCallback | useMemo = cache value, useCallback = cache function |
| Redux flow | Dispatch → Action → Reducer → Store → Component |
| Performance | memo, lazy, virtualization, debounce |
| Closures | Inner function remembers outer scope |
| Event Loop | Call stack → Web API → Task Queue → Stack |
| `===` vs `==` | Always use `===` (no type coercion) |
| Controlled component | React state drives input value |
| Code splitting | React.lazy + Suspense for route-level |

---

---

# DAY 2 – BACKEND + DATABASE FOCUS
## Python (FastAPI) | REST APIs | SQL | Microservices | .NET Basics

---

## KEY CONCEPTS TO REVISE

### 1. FastAPI Fundamentals
- **Path parameters** – `@app.get("/users/{user_id}")`
- **Query parameters** – `@app.get("/users?active=true")`
- **Request body** – Use Pydantic models for validation
- **Pydantic** – Data validation and serialization; define models as Python classes with type hints
- **Dependency Injection** – `Depends()` for shared logic (auth, DB sessions)
- **Async support** – Native `async def` endpoints for non-blocking I/O
- **Background tasks** – Run code after returning response
- **Middleware** – CORS, logging, authentication middleware
- **OpenAPI docs** – Auto-generated at `/docs` (Swagger UI)
- **Status codes** – 200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 422 Unprocessable Entity, 500 Internal Server Error

```python
# Example FastAPI endpoint
from fastapi import FastAPI, Depends, HTTPException
from pydantic import BaseModel

app = FastAPI()

class UserCreate(BaseModel):
    name: str
    email: str

@app.post("/users", status_code=201)
async def create_user(user: UserCreate, db=Depends(get_db)):
    # user data is already validated by Pydantic
    return await db.create(user)
```

---

### 2. REST API Design Principles
- **Resources as nouns** – `/users`, `/patients`, not `/getUsers`
- **HTTP verbs** – GET (read), POST (create), PUT (full update), PATCH (partial update), DELETE
- **Status codes matter** – Return correct HTTP status
- **Versioning** – `/api/v1/users` in URL, or via header
- **Pagination** – `?page=1&limit=20` or cursor-based for large datasets
- **Filtering & Sorting** – `?status=active&sort=created_at`
- **HATEOAS** – include links to related actions in response (not always needed)
- **Idempotency** – GET, PUT, DELETE are idempotent; POST is not
- **Authentication** – JWT Bearer tokens in Authorization header
- **Rate limiting** – protect against abuse
- **Error response format** – consistent structure: `{ "error": "message", "code": "ERROR_CODE" }`

---

### 3. Authentication & Authorization
- **JWT (JSON Web Token)** – Header.Payload.Signature; stateless; store in memory or httpOnly cookie
- **OAuth 2.0** – Authorization framework; used with third-party providers
- **Refresh tokens** – Short-lived access token + long-lived refresh token
- **RBAC (Role-Based Access Control)** – roles like admin, doctor, nurse control what they can access
- **FastAPI security** – `OAuth2PasswordBearer`, `HTTPBearer`, dependency injection for auth

---

### 4. SQL – Complex Queries & Optimization

**Essential SQL:**
```sql
-- Window functions
SELECT name, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees;

-- CTE (Common Table Expression)
WITH high_earners AS (
    SELECT * FROM employees WHERE salary > 100000
)
SELECT department, COUNT(*) FROM high_earners GROUP BY department;

-- Subquery vs JOIN - prefer JOIN for performance
SELECT p.*, COUNT(a.id) as appointment_count
FROM patients p
LEFT JOIN appointments a ON a.patient_id = p.id
GROUP BY p.id;

-- CASE WHEN
SELECT name,
       CASE WHEN status = 'A' THEN 'Active'
            WHEN status = 'I' THEN 'Inactive'
            ELSE 'Unknown' END as status_label
FROM users;
```

**SQL Optimization Techniques:**
- **Indexes** – Create on columns used in WHERE, JOIN, ORDER BY. Trade-off: faster reads, slower writes.
- **EXPLAIN / EXPLAIN ANALYZE** – See query execution plan; look for sequential scans on large tables
- **Avoid SELECT \*** – Fetch only columns you need
- **Avoid N+1 queries** – Use JOINs instead of querying in a loop
- **Connection pooling** – Don't create a new DB connection on every request
- **Partitioning** – Split large tables by date or range for faster queries
- **Query caching** – Cache frequently run, expensive queries
- **Proper data types** – Don't use VARCHAR(MAX) when VARCHAR(50) is enough

---

### 5. ORM – SQLAlchemy (Python)
- **Models** – Python classes that map to DB tables
- **Sessions** – Unit of work; use context manager to auto-commit/rollback
- **Relationships** – `relationship()` for foreign key associations
- **Eager vs Lazy loading** – Lazy loads related data on access (can cause N+1); eager loads with JOIN
- **Migrations** – Use Alembic for schema changes

---

### 6. Microservices Basics
- **Service decomposition** – Break app by business domain (patient service, billing service, auth service)
- **Communication** – Synchronous (REST, gRPC) or Asynchronous (message queues like RabbitMQ, Pub/Sub)
- **API Gateway** – Single entry point for all client requests; handles routing, auth, rate limiting
- **Service Discovery** – Services register themselves (Consul, Kubernetes DNS)
- **Circuit breaker pattern** – Stop calling a failing service temporarily to prevent cascading failures
- **Event-driven architecture** – Services communicate via events published to a message broker
- **Challenges** – Distributed tracing, eventual consistency, harder debugging than monolith

---

### 7. .NET Basics (Secondary Skill)
- **C# syntax** – Statically typed, object-oriented
- **ASP.NET Core** – Web framework similar to FastAPI; uses controllers and routing
- **Entity Framework Core** – ORM for .NET, similar to SQLAlchemy
- **Middleware pipeline** – Request goes through a series of middleware functions
- **Dependency injection** – Built into ASP.NET Core via `IServiceCollection`
- **LINQ** – Language-Integrated Query; SQL-like queries in C# code
- **Async/Await** – Same concept as Python; `Task<T>` is equivalent to Python's coroutine

---

## INTERVIEW QUESTIONS – DAY 2

### Q1. What makes FastAPI different from Django? Why would you choose one over the other?

"FastAPI and Django solve slightly different problems. Django is a full-featured framework — it comes with its own ORM, admin panel, authentication system, and templating engine out of the box. It's great for content-heavy applications where you want everything included. FastAPI is a more lightweight, modern framework built specifically for building APIs. Its big advantages are speed — it's one of the fastest Python frameworks — native support for async/await, and automatic API documentation with OpenAPI. It also uses type hints throughout, which makes the code cleaner and allows Pydantic to automatically validate request data. I'd choose FastAPI when building microservices or pure API backends where performance and developer experience matter. I'd choose Django for a project that needs a CMS-style admin, or where the team is already familiar with Django's conventions."

---

### Q2. How does FastAPI handle data validation?

"FastAPI uses Pydantic for data validation. You define your request body as a Pydantic model — a Python class that inherits from `BaseModel` — and specify field types using Python type hints. When a request comes in, FastAPI automatically validates the request body against the Pydantic model. If something is wrong — like a required field is missing, or a value doesn't match the expected type — FastAPI automatically returns a 422 status code with a detailed error message. You can also add custom validators, set field constraints like min/max length, and mark fields as optional with default values. This means you spend almost no time writing manual validation code."

---

### Q3. What is dependency injection in FastAPI, and why is it useful?

"Dependency injection in FastAPI is done through the `Depends()` function. You create a function that provides some shared resource — like a database session or the currently authenticated user — and then declare it as a dependency in your endpoint by adding it as a parameter with `Depends(your_function)`. FastAPI handles calling that function and injecting the result. It's useful because it keeps your endpoints clean and focused on business logic. For example, instead of writing database connection code in every endpoint, I declare a `get_db` dependency once and reuse it everywhere. It also makes testing easier — in tests, I can override dependencies to inject mock objects instead of real database connections."

---

### Q4. What is the N+1 problem in databases, and how do you fix it?

"The N+1 problem happens when you fetch a list of records and then run a separate query for each record to get related data. For example, if you fetch 100 patients and then in a loop fetch each patient's appointments, you're making 101 queries total — 1 for patients plus 100 for appointments. This gets very slow at scale. The fix is to use a JOIN to fetch everything in a single query. In SQL directly, that's a `JOIN` between patients and appointments tables. In an ORM like SQLAlchemy, you use eager loading — either `joinedload` or `selectinload` — to tell the ORM to fetch related data in one go instead of lazily loading it on access. I've caught N+1 issues in production by enabling query logging and seeing an unexpected number of queries being made."

---

### Q5. Explain the difference between `INNER JOIN`, `LEFT JOIN`, and `FULL OUTER JOIN`.

"An INNER JOIN returns only rows where there's a match in both tables. If a patient has no appointments, they won't appear in the result. A LEFT JOIN returns all rows from the left table and matching rows from the right table — if there's no match on the right, those columns will be NULL. So all patients appear, even those with no appointments. A FULL OUTER JOIN returns all rows from both tables, with NULLs where there's no match on either side. I use LEFT JOIN most commonly when I want to include records even when the related data doesn't exist yet — like showing all patients whether or not they have appointments."

---

### Q6. How do you secure a REST API?

"There are several layers to API security. For authentication, I use JWT tokens — the client sends a Bearer token in the Authorization header, and the server validates it on every request. For authorization, I implement RBAC — different roles have different permissions, and I check them in middleware or in the dependency layer. I always use HTTPS so data is encrypted in transit. I add rate limiting to prevent brute force attacks and DDoS. I validate all input rigorously — Pydantic handles most of this in FastAPI. I avoid exposing internal error details in responses, since those can give attackers useful information. I also set proper CORS headers so the API only accepts requests from trusted origins. For sensitive endpoints, I add additional logging and alerting."

---

### Q7. What are database indexes? When should you use them, and what are the downsides?

"An index is a data structure — usually a B-tree — that speeds up data retrieval on a table. When you query with a WHERE clause on an indexed column, the database can jump directly to the matching rows instead of scanning every row in the table. I add indexes on columns I frequently filter on, join on, or sort by. The downside is that indexes slow down write operations — every INSERT, UPDATE, or DELETE on an indexed column requires updating the index as well. They also take up storage space. So you don't want to over-index. I generally avoid indexing columns with very low cardinality — like a boolean column — because the index wouldn't help much. I also use composite indexes when I frequently query on multiple columns together."

---

### Q8. How do you design a microservices architecture? What challenges have you faced?

"I design microservices by splitting the application along business domain boundaries — a concept from Domain-Driven Design. Each service owns its own database and is independently deployable. Communication between services can be synchronous — using REST or gRPC — or asynchronous using a message broker like Pub/Sub or RabbitMQ. I put an API Gateway in front to handle routing, authentication, and rate limiting for all client requests. The challenges I've faced are mainly around data consistency — since each service has its own database, you can't use database transactions across services. You have to use patterns like the Saga pattern for distributed transactions. Debugging is also harder because a single user action might span multiple services, so distributed tracing with something like Jaeger or Cloud Trace is essential."

---

### Q9. What is a window function in SQL? Give an example.

"A window function performs calculations across a set of rows that are related to the current row, without collapsing the result into a single row like GROUP BY does. A classic example is `RANK()` — if I want to rank employees by salary within each department, I use `RANK() OVER (PARTITION BY department ORDER BY salary DESC)`. Each row keeps its identity, and the rank is added as an extra column. Other useful window functions are `ROW_NUMBER()`, `LAG()` and `LEAD()` — which let you access values from previous or next rows — and `SUM() OVER()` for running totals. I find them very useful for reporting queries where you need both detail and aggregated context."

---

### Q10. How do you handle errors in FastAPI?

"FastAPI has a built-in `HTTPException` that you can raise anywhere to return an error response with a specific status code and detail message. For more complex scenarios, I define custom exception classes and register exception handlers using `@app.exception_handler()`. This way, when a custom exception is raised anywhere in the application, the handler formats it consistently before returning it to the client. For unexpected errors, I add global middleware that catches unhandled exceptions, logs them with full stack trace, and returns a generic 500 response — without leaking implementation details to the client. I also use Pydantic's validation errors, which FastAPI automatically converts to 422 responses."

---

### Q11. What is connection pooling and why is it important?

"Every time you open a database connection, there's overhead — establishing the connection, authentication, allocating resources. If you create a new connection for every API request, that overhead adds up quickly and can overwhelm the database. Connection pooling keeps a pool of pre-established connections open and reuses them. When a request needs a database connection, it borrows one from the pool and returns it when done. This significantly improves performance. In Python, SQLAlchemy has built-in connection pooling. I configure the pool size based on expected concurrency and the database's connection limit. It's especially important in production where you might have thousands of requests per minute."

---

### Q12. What is eventual consistency in microservices?

"Eventual consistency is the idea that in a distributed system, after a data change, not all services will immediately reflect that change — but they will all eventually converge to the same state. For example, if a patient updates their address, the patient service immediately has the new address, but the billing service might still have the old one for a short time until an event is processed. This is acceptable for many use cases, but not for all — financial transactions, for instance, need strong consistency. I handle eventual consistency by designing the system to be tolerant of stale data where acceptable, and using compensating transactions or the Saga pattern for multi-step operations that must stay consistent."

---

## SCENARIO-BASED QUESTIONS – DAY 2

### S1. Your API endpoint is responding in 8 seconds. Users are complaining. How do you debug and fix this?

"First, I'd look at the application logs and distributed tracing to identify where the time is being spent. Is it the database? The business logic? A call to an external service? If it's the database, I'd enable query logging and run EXPLAIN ANALYZE on the slow queries. Often it's a missing index or an N+1 problem. I'd add an index or rewrite the query to use JOINs. If it's business logic, I'd profile the Python code with cProfile or a similar tool. If it's an external API call, I'd consider adding a cache so we don't call it on every request. I'd also check if the endpoint is doing unnecessary work — like fetching 1000 records when only 10 are needed. Adding pagination often fixes these kinds of problems. Finally, I'd consider making the endpoint async if it's doing I/O-bound work."

---

### S2. You need to design an API for a healthcare app where doctors can view patient records but billing staff cannot access clinical notes. How do you implement this?

"I'd implement role-based access control. Each user has one or more roles — `doctor`, `billing`, `admin`, etc. In FastAPI, I'd create a dependency function that checks the current user's role against the required role for the endpoint. For the clinical notes endpoint, I'd require the `doctor` role. The dependency would raise a 403 Forbidden exception if the user doesn't have that role. For more fine-grained control — like a doctor can only see their own patients — I'd add an additional check in the endpoint logic itself. All access attempts, successful or not, would be logged for audit purposes, which is especially important in healthcare applications for HIPAA compliance."

---

### S3. You are migrating a monolith to microservices. How do you approach it without downtime?

"I'd use the Strangler Fig pattern — gradually replace parts of the monolith with microservices instead of doing a big bang rewrite. I'd start by identifying the most independently deployable and highest-value parts of the system — usually something like authentication or notifications. I'd extract that into a microservice first, put an API Gateway in front, and route just that traffic to the new service while everything else still goes to the monolith. I'd run the old and new code in parallel initially to validate correctness. Then I'd gradually migrate more and more functionality, shrinking the monolith over time. Throughout this process, I'd make sure to keep comprehensive integration tests so I can catch any regressions."

---

### S4. A critical SQL query that reports on patient appointments is timing out in production. It works fine in development. What do you do?

"The fact that it works in development but times out in production usually means it's a data volume problem. First, I'd run EXPLAIN ANALYZE on the query in production to see the execution plan. I'd look for full sequential scans on large tables — that's usually the culprit. I'd check if the relevant columns are indexed. In production, if the data has grown significantly since the query was written, an index may have been missed or may need to be added for a new filter column. I'd also check for table statistics being stale — the query planner makes decisions based on statistics, so running ANALYZE to update them sometimes helps. If the query is inherently complex, I might rewrite it to use CTEs or break it into steps. For a reporting query, I'd also consider running it on a read replica to take load off the primary database."

---

### S5. Your team is adopting microservices, and you need to ensure services can communicate reliably even when one service is temporarily down. How do you handle this?

"I'd implement a combination of patterns. First, I'd use a message queue like Pub/Sub or RabbitMQ for async communication where possible — the publishing service sends a message and doesn't wait; the consumer processes it when it's available. For synchronous communication that can't be avoided, I'd implement the Circuit Breaker pattern — if service B starts failing, the circuit breaker trips and service A stops calling it for a period, returning a fallback response instead. I'd also add retries with exponential backoff — automatically retry failed requests with increasing delays. For critical operations, I'd use the Outbox pattern — write events to a local database table and a separate process publishes them to the message queue, ensuring no events are lost even if the service crashes."

---

## SYSTEM DESIGN QUESTIONS – DAY 2

### SD1. Design a REST API for a patient management system with multiple user roles.

"I'd start by identifying the core resources: patients, appointments, doctors, notes, billing records. I'd design clean REST endpoints for each. For authentication, I'd use JWT tokens issued on login, with refresh token rotation. Authorization would be RBAC — each endpoint checks if the caller's role allows the operation. I'd use FastAPI with SQLAlchemy for the ORM layer and PostgreSQL as the database. For the patient data, I'd think carefully about what goes in one record vs. related tables — appointments are a separate table linked to patients and doctors with foreign keys. I'd add pagination to all list endpoints to avoid returning thousands of records. For audit compliance in healthcare, every data access and modification would be logged to an audit trail table. I'd version the API from day one — `/api/v1/` — so future breaking changes don't affect existing clients."

---

### SD2. How would you design a scalable backend for a system that processes 10,000 API requests per minute?

"At 10,000 requests per minute, I'd think about horizontal scaling first — run multiple instances of the FastAPI application behind a load balancer. For the database, I'd use connection pooling and potentially read replicas for read-heavy workloads. I'd add a caching layer with Redis — frequently accessed data that doesn't change often gets cached, reducing database load significantly. For computationally expensive or non-urgent operations, I'd use background task queues — Celery with Redis — so the API can return immediately and the work happens asynchronously. I'd put a rate limiter at the API Gateway level to prevent any single client from overwhelming the system. I'd also ensure all expensive endpoints are async so the server doesn't block while waiting for I/O."

---

### SD3. How do you ensure data integrity when multiple services write to related data?

"In a microservices setup where each service has its own database, traditional ACID transactions spanning multiple services aren't possible. I'd use the Saga pattern. A saga is a sequence of local transactions, where each step publishes an event that triggers the next step in another service. If a step fails, compensating transactions undo the previous steps. For example, creating an appointment might involve the scheduling service and the notification service. I'd implement this as a choreography saga using events on Pub/Sub, or an orchestration saga where a coordinator service tells each service what to do. I'd also design each step to be idempotent — if an event is processed twice, it produces the same result as once. This handles message delivery guarantees."

---

## BEHAVIORAL QUESTIONS – DAY 2

### B1. Describe a time you optimized a slow API endpoint.

"We had a patient search endpoint that was timing out for large customer accounts with tens of thousands of patients. I profiled it and found we were doing a full table scan because the search was using a LIKE query with a wildcard at the start — `LIKE '%john%'` — which can't use a regular B-tree index. I replaced this with PostgreSQL's full-text search using `tsvector` and `tsquery`, and added a GIN index on the search column. Search time dropped from 8 seconds to under 200ms. I documented the pattern so the team could apply it to other search endpoints."

---

## DAY 2 QUICK REVISION SUMMARY

| Topic | Remember This |
|-------|---------------|
| FastAPI | Pydantic validation, Depends() for DI, async endpoints, auto docs |
| REST verbs | GET=read, POST=create, PUT=replace, PATCH=partial, DELETE=remove |
| SQL N+1 | Use JOINs, not loops; use eager loading in ORM |
| Indexes | Faster reads, slower writes; use on WHERE/JOIN/ORDER columns |
| Microservices | Own database, API Gateway, Circuit breaker, Saga pattern |
| JWT | Stateless auth; Header.Payload.Signature; short-lived + refresh token |
| Window functions | RANK(), ROW_NUMBER(), LAG(), LEAD() — no GROUP BY collapse |
| Connection pool | Reuse DB connections; configure pool size per concurrency |
| Eventual consistency | OK for non-critical; Saga for distributed transactions |

---

---

# DAY 3 – DEVOPS, CLOUD, TESTING & AI INTEGRATION
## Docker | CI/CD | GCP | Testing | Agile/Scrum | AI

---

## KEY CONCEPTS TO REVISE

### 1. Docker
- **Image** – read-only template for creating containers (defined by Dockerfile)
- **Container** – running instance of an image; isolated process
- **Dockerfile** – instructions to build an image
- **docker-compose** – define and run multi-container apps with a YAML file
- **Volumes** – persist data outside the container lifecycle
- **Networks** – containers on the same network can communicate by service name
- **Multi-stage builds** – use multiple FROM statements to keep final image small
- **Layer caching** – Docker caches each instruction layer; put infrequently changed layers first for faster builds
- **Health checks** – Docker checks if container is running correctly

```dockerfile
# Example Dockerfile
FROM python:3.11-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

FROM python:3.11-slim
WORKDIR /app
COPY --from=builder /app .
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

### 2. CI/CD Pipelines
- **CI (Continuous Integration)** – automatically build and test code on every commit/PR
- **CD (Continuous Deployment/Delivery)** – automatically deploy to staging/production after CI passes
- **Jenkins** – open-source CI/CD; uses Jenkinsfile (Groovy DSL); can run on-premise or cloud
- **Cloud Build** – GCP's managed CI/CD service; triggered by Git pushes; uses cloudbuild.yaml
- **Pipeline stages** – Checkout → Install dependencies → Lint → Unit tests → Build → Integration tests → Deploy
- **Artifacts** – build outputs (Docker images, binaries); stored in Artifact Registry or Container Registry
- **Branch strategies** – feature branches → develop → staging → main; each merge triggers a pipeline stage

**Cloud Build example config:**
```yaml
steps:
  - name: 'python:3.11'
    entrypoint: 'pip'
    args: ['install', '-r', 'requirements.txt']
  - name: 'python:3.11'
    entrypoint: 'pytest'
    args: ['tests/']
  - name: 'gcr.io/cloud-builders/docker'
    args: ['build', '-t', 'gcr.io/$PROJECT_ID/myapp', '.']
images: ['gcr.io/$PROJECT_ID/myapp']
```

---

### 3. GCP Basics
- **Cloud Run** – serverless container platform; auto-scales, pay per request; great for APIs
- **GKE (Google Kubernetes Engine)** – managed Kubernetes; for complex, long-running workloads
- **Cloud SQL** – managed relational database (PostgreSQL, MySQL)
- **Pub/Sub** – managed message queue for async communication between services
- **Cloud Storage** – object storage (like S3); for files, backups, assets
- **Cloud Build** – CI/CD service
- **Artifact Registry** – store Docker images and other build artifacts
- **Secret Manager** – securely store API keys, DB passwords, secrets
- **IAM (Identity and Access Management)** – control who can access what; principle of least privilege
- **VPC (Virtual Private Cloud)** – private network for your resources
- **Cloud Monitoring & Cloud Logging** – observability; set up alerts on error rates, latency
- **Load Balancing** – distribute traffic across multiple instances

---

### 4. Testing

**Types of tests:**
- **Unit tests** – test a single function/class in isolation; mock external dependencies; fast
- **Integration tests** – test multiple components together (e.g., API endpoint + database); slower
- **End-to-end (E2E) tests** – test the full user journey from UI to backend; slowest, most realistic
- **Test pyramid** – many unit tests, fewer integration tests, very few E2E tests

**Python testing (pytest):**
```python
# Unit test example
def test_calculate_bmi():
    result = calculate_bmi(weight=70, height=1.75)
    assert round(result, 1) == 22.9

# FastAPI integration test
from fastapi.testclient import TestClient
def test_create_user():
    response = client.post("/users", json={"name": "John", "email": "john@test.com"})
    assert response.status_code == 201
    assert response.json()["name"] == "John"
```

**React testing (Jest + React Testing Library):**
```javascript
// Component test
test('shows patient name', () => {
  render(<PatientCard name="John Doe" />);
  expect(screen.getByText('John Doe')).toBeInTheDocument();
});

// User interaction test
test('submits form on button click', async () => {
  render(<LoginForm onSubmit={mockSubmit} />);
  fireEvent.change(screen.getByLabelText('Email'), { target: { value: 'test@test.com' } });
  fireEvent.click(screen.getByRole('button', { name: 'Login' }));
  expect(mockSubmit).toHaveBeenCalled();
});
```

**E2E testing (Playwright / Cypress):**
- Simulate real browser interactions
- Test critical user flows: login → create patient → schedule appointment

---

### 5. Agile / Scrum
- **Sprint** – fixed time period (usually 2 weeks) to complete a set of planned work
- **Sprint Planning** – team selects items from backlog and commits to completing them
- **Daily Standup** – 15-min sync: what did I do yesterday, what am I doing today, any blockers
- **Sprint Review** – demo completed work to stakeholders
- **Sprint Retrospective** – team reflects on process; what went well, what to improve
- **Product Backlog** – prioritized list of all features and bug fixes
- **User Stories** – features from the user's perspective: "As a doctor, I want to view my patients so that I can manage their care"
- **Acceptance Criteria** – conditions that must be met for a story to be considered done
- **Definition of Done** – team's shared definition (coded, tested, reviewed, deployed to staging)
- **Story Points** – relative effort estimation; not hours
- **Velocity** – average story points completed per sprint; used for planning
- **Jira** – most common tool for backlog management, sprint tracking
- **Epic** – large body of work that spans multiple sprints, broken into user stories

---

### 6. AI Integration
- **LLM APIs** – OpenAI, Anthropic, Gemini; call via REST API in backend
- **Prompt engineering** – crafting prompts to get consistent, accurate output from LLMs
- **RAG (Retrieval Augmented Generation)** – add your own data context to LLM responses; prevents hallucinations
- **Vector databases** – store embeddings for semantic search (Pinecone, Weaviate, pgvector)
- **Streaming responses** – stream LLM output token-by-token for better UX (Server-Sent Events)
- **Function calling / Tool use** – let the LLM call predefined functions to fetch data
- **Fine-tuning** – train a model on your own data for domain-specific tasks
- **Guardrails** – validate and filter AI output; prevent harmful or off-topic responses

---

## INTERVIEW QUESTIONS – DAY 3

### Q1. What is Docker and why do we use it?

"Docker is a containerization platform that packages an application along with all its dependencies — libraries, runtime, config files — into a single unit called a container. The main benefit is consistency — the container runs the same way everywhere, whether on a developer's laptop, a staging server, or production. Before Docker, you'd often hear 'it works on my machine' — Docker eliminates that problem. Containers are also lightweight because they share the host OS kernel, unlike virtual machines which have their own full OS. I use Docker in development for local environments — everyone on the team runs the same database and service versions. In production, containers make deployment and scaling much more predictable and reliable."

---

### Q2. What is the difference between Docker image and Docker container?

"An image is like a blueprint — it's a read-only template that contains your application code, runtime, and dependencies. It's built from a Dockerfile and stored in a registry like Docker Hub or GCP Artifact Registry. A container is a running instance of that image — it's the actual live process. You can run multiple containers from the same image simultaneously. If a container crashes, you just start a new one from the same image. I think of it like a class and an object in programming — the image is the class (the template) and the container is an instance (the running copy)."

---

### Q3. What is CI/CD and why is it important?

"CI stands for Continuous Integration — every time a developer pushes code, an automated pipeline runs to build the code and run tests. This catches bugs early, before they reach production. CD stands for Continuous Deployment or Delivery — after CI passes, the code is automatically deployed to staging or production. The importance is speed and quality. Without CI/CD, deployments are manual, infrequent, and error-prone — developers are nervous about big releases. With CI/CD, you can deploy multiple times a day with confidence because every change goes through the same automated validation process. It also promotes smaller, incremental changes which are easier to debug when something goes wrong."

---

### Q4. What GCP services have you worked with or are familiar with?

"I've worked with Cloud Run for deploying containerized FastAPI services — it's really convenient because it auto-scales to zero and you only pay when the service is running. I've used Cloud SQL for managed PostgreSQL databases. For messaging between services, I've used Pub/Sub. Cloud Storage for storing uploaded files and exports. I'm familiar with Cloud Build for CI/CD pipelines triggered by pushes to Cloud Source Repositories or GitHub. I've also used Secret Manager for storing database credentials and API keys securely — you never put secrets in environment files in source code. For observability, Cloud Monitoring and Cloud Logging are really useful for setting up alerts and debugging production issues."

---

### Q5. How do you write a good unit test?

"A good unit test follows the AAA pattern — Arrange, Act, Assert. First you set up the conditions — create your test data and any mocks. Then you call the function you're testing. Then you assert on the result. A good unit test should be isolated — it shouldn't depend on a database or external service; those get mocked. It should be fast — ideally milliseconds. It should test one thing at a time — if a test fails, you should immediately know what broke. I also test edge cases — empty inputs, boundary values, error conditions — not just the happy path. Test names should describe what the test is checking: `test_calculate_bmi_returns_correct_value` is better than `test_bmi`."

---

### Q6. What is the difference between unit tests, integration tests, and E2E tests?

"Unit tests are the smallest — they test a single function or class in isolation, with all external dependencies mocked. They run very fast and should be numerous. Integration tests check how multiple components work together — for example, an API endpoint talking to a real database. They're slower and you need a test database. E2E tests simulate real user behavior in a browser — clicking through the UI just like a user would. They're the slowest but most realistic. I follow the test pyramid principle — write lots of unit tests, some integration tests, and a small number of E2E tests for critical user flows. Too many E2E tests make the pipeline slow and flaky."

---

### Q7. How do you handle environment-specific configuration (dev, staging, prod)?

"I never hardcode configuration values or put secrets in source code. I use environment variables for all config — database URLs, API keys, feature flags. In Python, I use pydantic's `BaseSettings` in FastAPI, which reads from environment variables and supports default values. For secrets like passwords and API keys, I use a secrets manager — GCP Secret Manager in our case. I have separate configuration for each environment — dev, staging, prod — with the staging environment closely mirroring production. For local development, I use a `.env` file that's listed in `.gitignore` so it's never committed. The CI/CD pipeline injects the right environment variables during deployment."

---

### Q8. What is a Dockerfile multi-stage build and why is it useful?

"A multi-stage build uses multiple `FROM` instructions in the Dockerfile. The idea is to have a build stage that compiles your code or installs dependencies, and then a final stage that copies only the necessary output without the build tools. For a Python application, I might have a stage that installs all dependencies including dev tools like pytest, and then a final slim stage that only has the production dependencies. This keeps the final Docker image much smaller — sometimes the difference between 1GB and 100MB. Smaller images mean faster deployments, lower storage costs, and a smaller attack surface for security."

---

### Q9. How do you handle secrets and sensitive configuration in a CI/CD pipeline?

"Secrets should never be committed to source code or stored in plaintext. In a GCP environment, I store secrets in Secret Manager and configure the CI/CD pipeline's service account to have read-only access to only the specific secrets it needs — principle of least privilege. In Cloud Build or Jenkins, I inject secrets as environment variables at pipeline runtime. The application also reads from Secret Manager directly using the GCP SDK, so secrets are fetched at startup rather than baked into the container image. I also set up alerting for any accidental commits of credentials — tools like git-secrets or GitHub's secret scanning can catch this automatically."

---

### Q10. What is a sprint retrospective and how do you make it valuable?

"A retrospective happens at the end of each sprint and is a dedicated time for the team to reflect on how they worked — not what they built, but how they worked together. I find it valuable when it's structured. I use the 'Start, Stop, Continue' format — what should we start doing, what should we stop doing, what's working well and should continue. The key is to make it a safe space where people can raise real concerns without blame. The most important part, though, is the action items — retrospectives are worthless if the same problems come up every sprint with no change. I always make sure we pick one or two concrete action items per retro and assign owners to them."

---

### Q11. How do you contribute to a sprint as a developer?

"Before the sprint starts, I participate in sprint planning — I ask questions to clarify requirements, flag technical risks, and give story point estimates. During the sprint, I attend standups and keep my updates focused — what I did, what I'm doing today, and if there are any blockers. I flag blockers early rather than waiting for the standup. I try to finish my stories a couple of days before the sprint ends so there's time for QA. I also participate in peer code reviews, which I treat as a way to help the team, not just gate code. At the sprint review, I demo my work and gather feedback from stakeholders. And in retros, I give honest, constructive feedback."

---

### Q12. What does observability mean in production systems?

"Observability is your ability to understand what's happening inside your system from its outputs. It has three pillars — logs, metrics, and traces. Logs tell you what happened — error messages, request details. Metrics tell you the health of your system — request rate, error rate, latency, CPU usage. Traces show you the journey of a single request across multiple services, which is essential in microservices. In GCP, I use Cloud Logging for logs, Cloud Monitoring for metrics and setting up alerts, and Cloud Trace for distributed tracing. Good observability means that when something goes wrong in production, I can find the root cause quickly instead of guessing."

---

## SCENARIO-BASED QUESTIONS – DAY 3

### S1. Your CI/CD pipeline is taking 45 minutes to run. The team is frustrated. How do you speed it up?

"45 minutes is definitely too long. I'd start by visualizing where the time is going — most CI systems have stage timing. Usually the slow parts are dependency installation, long-running tests, or slow Docker builds. For dependency installation, I'd add caching — cache the node_modules or pip virtual environment and only reinstall if the lock file changes. For tests, I'd run unit tests first since they're fastest, and fail fast if they fail rather than running everything. I'd also parallelize test suites across multiple runners. For Docker builds, I'd optimize the Dockerfile to maximize layer caching — copy requirements.txt and install dependencies before copying application code, so the dependency layer doesn't rebuild unless requirements change. If E2E tests are slow, I'd run them only on PRs to main, not on every commit to feature branches."

---

### S2. A new team member accidentally commits an API key to the Git repository. What do you do?

"This needs to be treated as a security incident immediately. First, I'd revoke the API key right away — even before cleaning up the repository. An exposed key is a security risk from the moment it's committed. Then I'd generate a new key and store it in Secret Manager. To remove it from Git history, I'd use `git filter-branch` or the BFG Repo Cleaner tool to rewrite history and remove the commit. Then force-push to the remote repository. I'd also notify the security team so they can check if the key was used maliciously during the window it was exposed. Going forward, I'd set up pre-commit hooks using git-secrets or similar tools that scan for credentials before every commit."

---

### S3. You need to deploy a new feature without any downtime. How do you approach this?

"I'd use a rolling deployment or blue-green deployment strategy. In a rolling deployment, new containers replace old ones gradually — at any point some users hit the old version and some hit the new one. This works well when the new version is backward compatible with the old API contract. For bigger changes, I'd use blue-green deployment — bring up the new version in a separate 'green' environment, run smoke tests against it, then switch the load balancer to point all traffic to green. The 'blue' old version stays running for a bit so you can instantly roll back if something goes wrong. I'd also use feature flags for risky features — deploy the code to production but keep the feature disabled until we're ready to turn it on for users."

---

### S4. You're asked to add AI-powered clinical note summarization to the product. How would you build it?

"I'd start by scoping the requirements carefully — what should be summarized, how long should summaries be, what tone? For the AI backend, I'd use an LLM API — something like Gemini on GCP or OpenAI. I'd design a FastAPI endpoint that receives the clinical note, builds a well-crafted prompt with clear instructions, and calls the LLM API. For latency, I'd use streaming — the frontend would display the summary as tokens come in rather than waiting for the full response. Since this is clinical data, I'd think carefully about privacy — whether we can send patient data to a third-party API or if we need an on-premise model. I'd implement guardrails — validate that the output looks like a summary and not something unexpected. I'd also add a review step — the doctor sees the AI summary and can edit or reject it before it's saved."

---

### S5. Your Docker container in production is using too much memory and getting OOM killed. How do you debug this?

"First, I'd check the Cloud Monitoring metrics for memory usage over time — is it a sudden spike or a gradual increase? A gradual increase suggests a memory leak. I'd add memory limits to the Docker container and set up alerts so I'm notified before it gets OOM killed. For debugging a leak in Python, I'd use `tracemalloc` or `memory-profiler` to track what's allocating memory over time. Common causes of memory leaks are keeping large objects in global state, not closing database connections or files, or accumulating data in a cache without expiry. In FastAPI, I'd check if there are any background tasks holding references to large data. I'd also look at database connection pooling — connection pools that are too large hold memory unnecessarily."

---

## SYSTEM DESIGN QUESTIONS – DAY 3

### SD1. Design a CI/CD pipeline for a full-stack application with React frontend and FastAPI backend on GCP.

"I'd structure the pipeline in Cloud Build with separate steps. For the backend: install Python dependencies, run linting with flake8, run unit tests with pytest, build the Docker image, push it to Artifact Registry, and deploy to Cloud Run. For the frontend: install npm dependencies, run ESLint, run Jest tests, build the production bundle, and deploy to Cloud CDN or Firebase Hosting. I'd have separate pipelines triggered by branches — PRs run tests only; merges to develop deploy to staging; merges to main deploy to production. Environment-specific configs come from Secret Manager. I'd add a manual approval gate before production deployments. Smoke tests run automatically after each deployment to verify the service is healthy."

---

### SD2. How would you set up monitoring and alerting for a production API on GCP?

"I'd use Cloud Monitoring as the primary platform. For metrics, I'd set up dashboards tracking request latency (p50, p95, p99), error rate (4xx and 5xx), throughput, and database query latency. I'd configure alerts — if error rate exceeds 1% for 5 minutes, or if p95 latency goes above 2 seconds, notify the on-call engineer via PagerDuty or Slack. For logs, I'd structure them as JSON in Cloud Logging with correlation IDs so I can trace a specific request across services. I'd set up log-based metrics for specific error patterns. For distributed tracing, Cloud Trace gives you flame graphs of request durations across services. I'd also add health check endpoints that Cloud Run uses to route traffic — only send traffic to healthy instances."

---

### SD3. How do you ensure your tests don't slow down the development team while still providing confidence?

"I'd implement the test pyramid strictly — lots of fast unit tests, fewer integration tests, minimal E2E tests. In the CI pipeline, I'd run tests in stages with fail-fast: unit tests first (seconds), then integration tests (minutes), then E2E only on the main branch (many minutes). I'd use test parallelization — split tests across multiple workers so a large test suite runs faster. For integration tests that need a database, I'd use a test database with Docker Compose in the pipeline, and write tests that each create and clean up their own data so tests can run in any order. I'd track test execution times and flag any test that takes more than a few seconds — those get refactored or moved to a slower suite. I'd also encourage developers to run only relevant tests locally before pushing, and let CI run the full suite."

---

## BEHAVIORAL QUESTIONS – DAY 3

### B1. Tell me about a time you had to quickly learn a new technology for a project.

"When we decided to migrate to GCP, I had no hands-on experience with it. I allocated two weeks alongside my regular work to learn. I went through the core GCP labs on Qwiklabs, focusing on the services we'd actually use — Cloud Run, Cloud SQL, Pub/Sub. I built a small proof-of-concept by deploying one of our existing FastAPI services to Cloud Run. When I ran into issues, I asked in the team Slack and looked at the official documentation rather than just Stack Overflow. Within a month I was leading the migration for our service. I think the key was being focused — learning only what I needed for the specific task rather than trying to learn everything."

---

### B2. Describe a situation where you caught a critical bug before it reached production.

"During code review, I noticed a teammate's PR was building a SQL query by string concatenation using user input — a classic SQL injection vulnerability. I flagged it immediately and suggested using parameterized queries or the ORM's query builder instead. I also asked if we had any tests covering that endpoint with unusual inputs. We didn't, so I added some. We also ran a quick security scan with bandit on the codebase and found two other similar patterns. It was a good example of how thorough code review prevents issues — this could have been a serious security breach for our healthcare application."

---

### B3. Have you ever disagreed with a technical decision made by a senior engineer? How did you handle it?

"Yes, once a senior engineer proposed using a NoSQL database for all data in a new service, including highly relational data like appointments and billing records. I felt this would cause problems down the line — complex queries that are natural in SQL become very difficult in NoSQL. I prepared a short document comparing the two approaches for our specific use case, showing the query complexity difference. I brought it up in a tech design meeting and presented my concerns respectfully. We had a good discussion, the senior engineer raised some valid points about scalability, and we ended up on a hybrid approach — PostgreSQL for relational data, with Redis for caching. I learned that backing up concerns with data and specific examples is more effective than just saying 'I think we should do it differently.'"

---

### B4. How do you handle it when your sprint velocity drops due to unexpected complexity?

"First, I flag it early — as soon as I realize a story is much bigger than estimated, I bring it up in the standup or ping the product manager directly. I don't wait until the last day of the sprint. I explain what the complexity is and give a revised estimate. We then decide together whether to carry over the story to the next sprint, scope it down to deliver part of it this sprint, or get another team member to help. I also do a mini-retro on why the estimation was off — was it missing requirements, technical dependencies we didn't know about, or just optimistic estimating? This helps improve future estimates. I've found that transparency and early communication prevents most of the frustration that comes from missed sprint commitments."

---

### B5. How do you balance technical debt with feature delivery in an Agile team?

"This is a real tension in every team. My approach is to make technical debt visible — I create Jira tickets for tech debt items and add them to the backlog, just like features. This way the product manager can see the debt and make informed trade-off decisions rather than being surprised later. I advocate for a 20% rule — roughly one day per sprint dedicated to tech debt, testing improvements, or refactoring. I also apply the Boy Scout Rule — whenever I'm working in an area of code, I leave it slightly better than I found it, without gold-plating. For critical debt that's actively causing bugs or slowing down feature delivery, I make a business case — fixing this debt will save us X hours per sprint going forward. That framing helps product managers prioritize tech debt more readily."

---

## DAY 3 QUICK REVISION SUMMARY

| Topic | Remember This |
|-------|---------------|
| Docker | Image = blueprint (immutable), Container = running instance |
| Multi-stage build | Smaller final image; copy only what's needed |
| CI/CD | CI = build + test on commit; CD = auto deploy after CI |
| GCP Cloud Run | Serverless containers; auto-scale to zero; pay per request |
| Testing pyramid | Many unit → some integration → few E2E |
| pytest | Arrange-Act-Assert; mock external deps; test edge cases |
| Agile | Sprint = 2 weeks; standup = blockers; retro = process improvement |
| Secret Manager | Never put secrets in code or env files; use secrets manager |
| Observability | Logs + Metrics + Traces; set up alerts |
| AI integration | LLM API + Prompt engineering + RAG + Streaming |

---

---

# FINAL RAPID REVISION SECTION
## "Last Night Before Interview" Cheat Sheet

---

## KEY BUZZWORDS TO DROP IN INTERVIEWS

**Frontend:** React Hooks, Virtual DOM, Reconciliation, Code Splitting, Lazy Loading, Tree Shaking, React.memo, Redux Toolkit, RTK Query, Controlled Components, Custom Hooks, Accessibility

**Backend:** FastAPI, Pydantic, Dependency Injection, Async/Await, RESTful API, Idempotency, Pagination, JWT, OAuth2, RBAC, Connection Pooling, N+1 Problem, Eager Loading

**Database:** Window Functions, CTE, Query Execution Plan, EXPLAIN ANALYZE, Index Cardinality, Composite Index, Partitioning, Full-Text Search, ACID Properties, Normalization

**Microservices:** Service Decomposition, API Gateway, Circuit Breaker, Saga Pattern, Event-Driven, Pub/Sub, Eventual Consistency, Strangler Fig Pattern, Domain-Driven Design

**DevOps/Cloud:** CI/CD Pipeline, Docker Multi-stage Build, Layer Caching, Blue-Green Deployment, Rolling Deployment, Feature Flags, Secret Manager, Principle of Least Privilege, Cloud Run, GKE

**Testing:** Test Pyramid, AAA Pattern, Mocking, Test Coverage, Flaky Tests, Integration Test Database, E2E with Playwright

**Agile:** Sprint Velocity, User Story, Acceptance Criteria, Definition of Done, Story Points, Retrospective Action Items, Sprint Burndown

**AI:** LLM, Prompt Engineering, RAG, Vector Embeddings, Streaming Response, Guardrails, Function Calling

---

## QUICK CHEAT SHEET NOTES

### React
- `useState` → local state | `useEffect` → side effects | `useRef` → DOM/mutable value
- `useMemo` → cache value | `useCallback` → cache function
- Redux flow: Action → Reducer → Store → Component
- Performance: memo, lazy, virtualization, debounce, code splitting

### Python/FastAPI
- Pydantic = validation | `Depends()` = dependency injection
- `async def` for I/O bound | background tasks for post-response work
- Always return proper HTTP status codes
- Use parameterized queries / ORM — never string concat SQL

### SQL
- `EXPLAIN ANALYZE` to find slow queries
- Index on: WHERE / JOIN / ORDER BY columns
- Window fn: `RANK() OVER (PARTITION BY x ORDER BY y)`
- CTE: `WITH name AS (SELECT ...)` — readable complex queries
- N+1 fix: JOINs + eager loading

### Docker
- `CMD` runs at container start | `RUN` runs during build
- Multi-stage: small prod image | Layer cache: COPY requirements first
- `docker-compose` for local multi-service setup

### GCP
- Cloud Run: serverless containers | Cloud SQL: managed DB
- Pub/Sub: async messaging | Secret Manager: secrets
- IAM: least privilege | Cloud Monitoring: alerts + dashboards

### Testing
- Unit: mock everything external, test one thing
- Integration: real DB, test component interaction
- E2E: real browser, test user flow
- Pyramid: many unit → some integration → few E2E

### Agile
- Standup: yesterday / today / blockers (max 15 min)
- Retro: Start / Stop / Continue + action items
- Velocity: points completed per sprint (average, not target)
- Story: "As a [user], I want [feature] so that [reason]"

---

## PHRASES TO USE IN INTERVIEWS

- "I've used this in production and found that..."
- "A common pitfall here is... and I avoid it by..."
- "The trade-off I considered was..."
- "I typically start by profiling/analyzing before optimizing"
- "I flagged this early in standup to unblock the team"
- "I backed up my suggestion with data / a small PoC"
- "The reason I prefer X over Y in this context is..."
- "From a security perspective, I always..."

---

## LAST-MINUTE REMINDERS

1. **Always mention trade-offs** — interviewers love when you think about pros and cons
2. **Give concrete examples** — "in my project" beats abstract theory
3. **Ask clarifying questions** in system design — don't assume
4. **Think out loud** — say what you're considering, even if you're not sure
5. **It's okay to say "I haven't used that specifically, but I understand the concept and would..."**
6. **Connect technical answers to business impact** — latency improvements = better user retention
7. **Show Agile maturity** — mention standups, code reviews, sprint planning naturally
8. **Healthcare context** — mention security, HIPAA-style compliance, audit trails where relevant

---

*Study Plan created for IKS Health – Product Engineer Interview*
*Aligned with JD: Python (FastAPI), React, JavaScript, SQL, Docker, CI/CD, GCP, Microservices, Testing, Agile*
