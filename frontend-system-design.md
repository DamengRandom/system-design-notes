# Frontend System Design (Lite)

This is one of examples about the way to explore how to prepare frontend system design interview. The news feed has been selected as an example.

## Functional requirements: (Example - News feeds)

- Display list of feeds
- Each feed has a title, description, and comments
- Only concern the user post type
- should support infinite scroll


## Non-functional requirements

- Accessability support (`a11y`)
- Should be mobile friendly (responsive display)
- Should support internationalization (`i18n`)
- Should be performant (fast loading)
- Some observability for the system, like metrics, logs, etc, `monitoring`


## Architecture

- Start with a simple UI design (quick demo only, visually show your understanding of the feature/system development)
- Design a component architecture (list the components and how they will work together)
- Discuss design patterns (eg: MVC or MVVM) with interviewer and why you chose those patterns and explain how data flow between the components

Tiny Note: When to use MVC or MVVM?

- MVC: Model-View-Controller
- MVVM: Model-View-ViewModel

- MVC is a pattern that separates the application into three layers: Model, View, and Controller.
- MVVM is a pattern that separates the application into three layers: Model, View, and ViewModel.

If we use Framework like Angular, which is 2 way data binding, we can use MVVM pattern.
If we need to consider to use controller to trigger the view update, we can use MVC pattern.

Complexity comaprision: MVC is less complex than MVVM, because it has less layers.

MVC is good for SSR, simple apps and MVVM is good for SPA, dynamic UIs.


## Data Model

We could have following data model:

```ts
type App = {
  user: User,
  settings: UserSettings,
  feed: Feed,
}

type Feed = {
  items: List[FeedItem],
  page: int,
  size: int,
}

type FeedItem = {
  type: FeedItemType,
  creationDate: string,
  author: User,
  content: FeedItemContent,
  comments: List[FeedItemComments]
}

type User = {
  name: string,
  ...
}

type UserSettings = {
  language: string,
  timezone: string,
  accessibilityPreferences: AccessibilityPreferences,
  etc ...
}

type FeedItemType = {
  type: string,
  ...
}

type FeedItemContent = {
  title: string,
  body: string,
  media: Media,
  ...
}

type FeedItemComments = {
  comments: Array<Comment>,
  ...
}
```

## API Design

- API `protocol` to select to use:
  - HTTP1 vs HTTP2:

  HTTP1:
  - Limited number of connections it can handle at once
  - Synchronous blocking queue
  - Plain text
  - Explicitly need to close the connection
  - Single TCP sends one data at a time
  - Latency is a bit higher compared to HTTP2

  HTTP2: (better use this one) [✅]
  - Multiplexing
  - Multiple connections
  - Rich data format support (JSON, XML, etc)
  - Parallel requests
  - Better compression (`HPACK` algorithm)
  - One TCP sends multiple streams of data at once

- API `options` to select to use: Depending on situation to choose
  - REST vs GraphQL:

  REST:
  - Simple to understand and easy & commonly to be used [✅]
  - Make multiple requests to the server to fetch the data (/users, /users/1/posts ...) [❌]
  - No need to learn a new query language [✅]
  - Need to define a API documentation, eg: `OpenAPI` or `Swagger` [❌]
  - Need to use tools, eg: `Postman` to test the API

  GraphQL:
  - Fetch what you need, customized data shape [✅]
  - Fetch all the data in a single request [✅]
  - Sometimes, deeply nested query could cause expensive query performance [❌]
  - Has built in introspection tools, eg: `Apollo Client` to explore the schema and query the data [✅]
  - Need to use tools, eg: `GraphQL Playground` to test the API



## Optimizations & Performance (More general answers)

- Use `lazy loading` for the images, so the images will be loaded only when the user scrolls to the image
- Use `virtual list` for the list of feeds, so the list will be loaded only when the user scrolls to the list
- Use `debouncing` & `throttling` for the search input, so the search will be performed only when the user stops typing for a certain amount of time
- Use `Batching request` to reduce the number of requests to the server
- Use `Code splitting` to split the code into smaller chunks
- Use `Tree shaking` to remove the unused code
- Use `Pre-rendering` to pre-render the static web page (SSR), which doesn't have multiple data interactions
- Use `Caching` to reduce the number of requests to the server, if the data is not changed frequently
- Use `CDN` (Content Delivery Network) for reducing latency, and improve the performance of the website (user can read the website faster which is from nearest geographic located server)
- Use `loading-state (pre-loading)` mechinsm to show the users the latest state of the page or specific area of the page
- Consider `responsive design` to make the website more friendly to different devices (using `CSS media queries` to adjust the UI based on the device width and tools for testing, eg: `Responsive Design Checker`)
- Use `GraphQL` to fetch the specific shape of data from the server, which is more flexible and sufficient (Soemtimes, can use Apollo Cache to cache the data, more performance improvement)
- Could consider to introduce `Micro-frontend architecture` develop a website, because, for some pages, like home page, maybe more static contents related, which can be server side rendered, for some forms view, more user data interaction UIs, we can build as client side redenring for better state management and interactions handling, which means the different pages can choose to use different rendering techniques, which is more flexible and efficient.
- Use third party tools eg: `lighthouse`, `Chrome DevTools` to analyze the performance of the website, `web vitals`: LCP (largest contentful paint), FCP (first contentful paint), FID (first input delay), etc
- Adding more accessibility features, like `alt text` for the images, `aria-labels` for the buttons, `tabindex` for the focusable elements, etc


## Security

- Use `HTTPS` to encrypt the data between the client and the server
- Use `CSRF` (Cross-Site Request Forgery) to prevent the malicious requests from the client
- Use `XSS` (Cross-Site Scripting) to prevent the malicious scripts from the client
- Use `CSP` (Content Security Policy) to prevent the malicious scripts from the client
- Use `CORS` (Cross-Origin Resource Sharing) to prevent the malicious requests from the client
- Use `HTTPOnly` to prevent the malicious scripts from the client
- Use `Secure` to prevent the malicious scripts from the client


## My own thoughts

The steps of system design interview could be concluded as following:

- Grab & Understand the business `functional requirements` + `non-functional requirements`
- Structure the `components` (Break down UI into smaller components)
- Start with `data models` design based on the components
- Do the `API design` (Choose the right tool based on specific interview question)
- Provide the valid points of `optimizations & performance` (Eg: rendering, bundling, API efficiency, monitoring tools, etc)
- Some `security` considerations (Eg: CSRF, XSS, etc)


To be continued (more new contents will be added later) ...
