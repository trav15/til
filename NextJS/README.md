# Next.js

## Pre-rendering

By default, Next.js pre-renders every page. This means that Next.js generates HTML for each page in advance, *instead of having it all done by client-side JavaScript*. Pre-rendering can result in better performance and SEO.

Each generated HTML is associated with minimal JavaScript code necessary for that page. When a page is loaded by the browser, its JavaScript code runs and makes the page fully interactive. (This process is called **hydration**.)

A plain React.js app (without Next.js) has no pre-rendering, so you will not see the app if you disable JavaScript.

Next.js lets you choose which pre-rendering form to use for each page. You can create a "hybrid" Next.js app by using Static Generation for most pages and using Server-side Rendering for others.

*Next.js polyfills fetch() on both the client and server. You don't need to import it.*

`getStaticProps` only **runs on the server-side**. It will never run on the client-side. It won’t even be included in the JS bundle for the browser. That means you can write code such as direct database queries without them being sent to browsers. Because it’s meant to be run at build time, you won’t be able to use data that’s only available during request time, such as query parameters or HTTP headers.

## Client Side Data Fetching

[SWR](https://swr.vercel.app/) is highly recommended if you are fetching data on the client-side. It handles caching, revalidation, focus tracking, refetching on intervals, and more.

Example usage:
```js
import useSWR from 'swr'

const fetcher = (...args) => fetch(...args).then((res) => res.json())

function Profile() {
  const { data, error } = useSWR('/api/profile-data', fetcher)

  if (error) return <div>Failed to load</div>
  if (!data) return <div>Loading...</div>

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.bio}</p>
    </div>
  )
}
```

You have to create the `fetcher` function. It can be asynchronous and can use fetch polyfill (which is built-in to Next.js) or any data-fetching library such as Axios. Example:

```js
import axios from 'axios'

const fetcher = url => axios.get(url).then(res => res.data)
```

You can use `mutate` returned from `useSWR` for updates/revalidation. [Source: SWR docs](https://swr.vercel.app/docs/mutation)

## TypeScript

Next.js provides specific types for use such as `GetStaticProps` and `GetServerSideProps`

```js
import { GetStaticProps, GetStaticPaths, GetServerSideProps } from 'next';

export const getStaticProps: GetStaticProps = async (context) => {
  // ...
};

export const getStaticPaths: GetStaticPaths = async () => {
  // ...
};

export const getServerSideProps: GetServerSideProps = async (context) => {
  // ...
};
```

## *Resources*

- [Next.js Docs](https://nextjs.org/docs/getting-started)
- [SWR (React Hooks for Data Fetching)](https://swr.vercel.app/)
- [Beginners Guide to SWR Fetching in React](https://blog.openreplay.com/beginner-s-guide-to-swr-data-fetching-in-react)
- [Next.js's TypeScript docs](https://nextjs.org/docs/basic-features/typescript)