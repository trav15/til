# Next.js

## Pre-rendering

By default, Next.js pre-renders every page. This means that Next.js generates HTML for each page in advance, *instead of having it all done by client-side JavaScript*. Pre-rendering can result in better performance and SEO.

Each generated HTML is associated with minimal JavaScript code necessary for that page. When a page is loaded by the browser, its JavaScript code runs and makes the page fully interactive. (This process is called **hydration**.)

A plain React.js app (without Next.js) has no pre-rendering, so you will not see the app if you disable JavaScript.

Next.js lets you choose which pre-rendering form to use for each page. You can create a "hybrid" Next.js app by using Static Generation for most pages and using Server-side Rendering for others.

