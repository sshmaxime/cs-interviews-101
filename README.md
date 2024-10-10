# Computer Science Interviews 101

## Frontend Software Engineering

#### 1. Explain the differences between SSR, CSR, ISR, and SSG, and how the request process works for each, starting from when a user types a URL, as well as when each approach is most suitable?

---

- **SSR (Server-Side Rendering)**: The HTML is generated on the server for each request, then sent to the client. This provides faster initial page loads, beneficial for SEO and users with slower devices. It's best for content-heavy or dynamic sites where SEO is critical.

<pre>
┌───────────────────────────┬──────────────────────────────────────────────────────────────────────┐
│ Rendering Method          │ Request Handling Process                                             │
├───────────────────────────┼──────────────────────────────────────────────────────────────────────┤
│ 1. Server-Side Rendering  │ 1. User enters a URL and hits Enter                                  │
│    (SSR)                  │ 2. Browser sends an HTTP request to the server                       │
│                           │ 3. Server dynamically generates HTML (fetches data, processes logic) │
│                           │ 4. Server sends back complete HTML to the client                     │
│                           │ 5. Browser renders the HTML, JavaScript hydrates the page for        │
│                           │    interactivity                                                     │
│                           │                                                                      │
└───────────────────────────┴──────────────────────────────────────────────────────────────────────┘
</pre>

Best for dynamic, SEO-driven content.

---

- **CSR (Client-Side Rendering)**: The client (browser) downloads a JavaScript bundle and renders content after execution. It leads to slower initial load times but better subsequent navigations. Best for web apps where SEO isn't the primary focus, such as dashboards.

<pre>
┌───────────────────────────┬──────────────────────────────────────────────────────────────────────┐
│ Rendering Method          │ Request Handling Process                                             │
├───────────────────────────┼──────────────────────────────────────────────────────────────────────┤
│ 2. Client-Side Rendering  │ 1. User enters a URL and hits Enter                                  │
│    (CSR)                  │ 2. Browser sends an HTTP request, server responds with minimal HTML  │
│                           │ 3. Browser downloads JavaScript (JS) bundle, JS fetches data         │
│                           │    asynchronously                                                    │
│                           │ 4. JS dynamically generates HTML on the client side                  │
│                           │ 5. Page becomes interactive after data fetching and rendering        │
│                           │                                                                      │
└───────────────────────────┴──────────────────────────────────────────────────────────────────────┘
</pre>

Best for complex, interactive apps with minimal SEO needs.

---

- **ISR (Incremental Static Regeneration)**: Combines SSG and SSR. Pages are statically generated, but revalidated on the server at intervals to keep data fresh. Best for content that changes occasionally, such as blogs or e-commerce, balancing speed and freshness.

<pre>
┌───────────────────────────┬──────────────────────────────────────────────────────────────────────┐
│ Rendering Method          │ Request Handling Process                                             │
├───────────────────────────┼──────────────────────────────────────────────────────────────────────┤
│ 3. Static Site Generation │ 1. Pre-generation happens at build time (deployment phase)           │
│    (SSG)                  │ 2. User enters a URL and hits Enter                                  │
│                           │ 3. Server (or CDN) serves pre-built static HTML immediately          │
│                           │ 4. Browser renders the static HTML                                   │
│                           │ 5. Optional JavaScript hydration adds interactivity                  │
│                           │                                                                      │
└───────────────────────────┴──────────────────────────────────────────────────────────────────────┘
</pre>

Best for static sites needing periodic data updates.

---

- **SSG (Static Site Generation)**: The site is built entirely at compile time and served as static files. This is the fastest option but lacks dynamic updates. Best for sites with rarely changing content, like documentation or marketing pages.

<pre>
┌───────────────────────────┬──────────────────────────────────────────────────────────────────────┐
│ Rendering Method          │ Request Handling Process                                             │
├───────────────────────────┼──────────────────────────────────────────────────────────────────────┤
│ 4. Incremental Static     │ 1. Pre-generation happens at build time (like SSG)                   │
│    Regeneration (ISR)     │ 2. User enters a URL and hits Enter                                  │
│                           │ 3. Server serves pre-built static HTML                               │
│                           │ 4. Behind-the-scenes: Server regenerates content if the revalidation │
│                           │    period has expired, and serves updated content to future requests │
│                           │ 5. Browser renders the static HTML                                   │
│                           │                                                                      │
└───────────────────────────┴──────────────────────────────────────────────────────────────────────┘
</pre>

Best for fast, static content with little need for updates.