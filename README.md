[Link to LinkedIn Post by Lee Rob](https://www.linkedin.com/posts/leeerob_how-should-you-search-filter-and-paginate-activity-7228525688062889984-JBph?utm_source=share&utm_medium=member_desktop)

### How should you search, filter, and paginate data with Next.js? This demo has 50,000 books in a Postgres database.

- Page Load: When the page loads, we see the React Suspense fallback. This loading skeleton is displayed until the first page of books is retrieved from the database.
- Searching: The search input has a 200ms debounce. After 200ms of inactivity, the form submits, updating the URL state with `?q={search}`. The Server Component reads `searchParams` and queries the database. On form submission, a React transition starts, allowing us to read the pending status with `useFormStatus` to display an inline loading state.
- State Preservation: Navigating to an individual book page retains the search input state. Reloading the page or sharing the link preserves the search results.
- Client-side Filtering: Filtering authors in the left sidebar is done client-side. Authors are fetched by a Server Component and passed as props to the sidebar. Changing the input value updates React state and re-renders the sidebar.
- Optimistic Updates: The sidebar’s selected authors are optimistically updated with `useOptimistic`. Checkbox selections update instantly without waiting for the URL to change.
- State Preservation: Navigating to an individual book page retains the sidebar filter input and selected author state across navigations, giving it an app-like feel.
- Pagination: Navigating between pages updates the URL state, triggering the Server Component to query the database for the specific page of books. We also fetch the total book count to show the total number of pages.

This demo isn't perfect yet (still working on it) but it's been a fun playground for some of these patterns. You can imagine a similar experience for thousands of movies, cars, products, or any other very large dataset.

----
# Next.js Book Inventory

Demo: https://next-books-search.vercel.app

This is a simple book inventory app built with Next.js, Drizzle, and PostgreSQL. The database contains over 50,000 books from the included `books.csv` file.

## Deploy on Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fvercel-labs%2Fbook-inventory&stores=%5B%7B"type"%3A"postgres"%7D%5D)
