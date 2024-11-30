# Breaking Up with Next.js

**source**: https://www.youtube.com/watch?v=Jw8sXzaZUDQ

## What is Next.js?

- it is a framework for React, and there are lots of things we can do in it, which can't by default in
  React, like: - Server Side Rendering - Static Site Generation - Incremental Site Generation - Server Components - Server Actions, etc.

- Plus there is a team called `vercel` which provides you the various feature Out-of-the-box like CI/CD
  Pipelines, Deployments, Environment Variable Management, etc. So that you can focus on the Development
  only and the rest about deployment will be taken care by them. Vercel is the team which owns Next.js.

## Problem in React.js:

- Whenever you write code in React.js everything is client-rendered, so whenever user tried to load the
  page the page at the client-side will call an API and fetched the data from it and then display it on
  the Page. There is no data already available on the HTML at the client-side.

- That's Ok with the case of Humans, In the case of Bots, crawlers, which used to visit the website, they
  only see the blank HTML page, which contains no data. That's the case when your SEO will get degraded.

- Because we are doing most of the client-rendering the performance of the website very low and the
  website becomes eventually heavier.

## f
