# Next.js

**This** cheat sheet **is missing:** Next.js advanced features, Next.js configuration and next/amp

## Usage

```bash
npx next [build | start | export | dev | telemetry]

npx create-next-app
```

## FileSystem Structure

- `.` - root
- `[src/]pages` - pages source (if `pages` does not exist, `src/pages` is used)
- `[src/]pages` - a page, `**/*.[js | jsx | ts | tsx]` - a React component
- `[src]/pages/_app.[js | jsx | ts | tsx]` - custom `App`
  - imports `import 'path/to/styles.css'` allowed only here
- `[src]/pages/[_[document | error] | 404].[js | jsx | ts | tsx]` - custom `Document`, `Error` or 404 page
- `**/[name].module.[css | scss | sass | less | styl]` - CSS module, Sass module _(with configuration)_, Less and Stylus _(with plugin)_
- `[src]/pages/api/*` - an API handler `(req, res) => {...}`
- `public` - mapped to `/`, static assets
- `.env.local` - environment variables, loaded into `process.env`, to expose a variable to the browser use prefix `NEXT_PUBLIC_`
  - `.env.development`, `.env.production` - development and production environment variables default, overriden by `.env.local`

## Routes

- `pages/index.js` - directory root
- `pages/static.js` - static route `/static`
- `pages/dynamic/[param].js` - dynamic route `/dynamic/param`, multiple params allowed
- `pages/[...param]` - catch-all route, e.g. `/foo/bar` = `{ 'param': ['foo', 'bar'] }`
- `pages/[[...param]]` - optional catch-all route, e.g. `/foo/bar` = `{ 'param': ['foo', 'bar'] }` _experimental (with configuration)_
- use `Router` from `next/router`
  - imperative client-side routes: `Router.push('/page')`
  - shallow routing without running data fetching methods, works only for the same page URL changes - `Router.push('/path/...', undefined, { shallow: true })` or with `useRouter` like `const router = useRouter(); ... router.push('/path/...', undefined, { shallow: true })`, useful with React `useEffect` or `componentDidUpdate`
- `pages/api/endpoint.js` - API endpoint, index, dynamic and catch-all routes supported as well

## Router Object

```javascript
const router = useRouter(); // React router hook, OR
function Page({ router }) { ... // Component router prop
```

- `router`
  - `pathname: String` - current route
  - `query: Object` - query string parsed
  - `asPath: String` - actual path including the query
  - `push(url: string | { pathname: string, query?: { param: string, ... } }, as?: string, options?: { shallow: boolean })` - client-side transition
  - `replace( ... the same as router.push )` - client-side transition without a new entry in the history
  - `prefetch(url: string, as?: string)` - client-side prefetch, only for navigation without `next/link`
  - `back()`, `reload()` - navigate back, reload
  - `events.on(name: string, f: function)` and `events.off(name: string)`: `routeChangeStart`, `routeChangeComplete`, `routeChangeError`, `beforeHistoryChange`, `hashChangeStart`, `hashChangeComplete`

## Links

- use `Link` from `next/link`
  - `href` - URL string or `router` URL object
  - `as?` - url for dynamic path segments
  - `passHref = false` - sends `href` prop to the child
  - other: `prefetch = true`, `replace = false`, `scroll = true`, `shallow = false`

## Head

```javascript
<Head><title>Title</title><Head> // Multiple Heads allowed, avoid to duplicate elements using `name` and `key` props
```

## Rendering

- Static Generation - at build time (pages without fetching data)
  - `async getStaticProps: GetStaticProps(context: { params: { param: ... }, preview: boolean, previewData: { #TODO } })` - called at build time, passes returned `{ props: { data } }` data to page's `props`
    - page component type `InferGetStaticPropsType<typeof getStaticProps>`
  - `async getStaticPaths: GetStaticPaths` - called at build time, specifies returned paths `{ paths: { params: { param: string } }[], fallback: boolean }` to prerender
    - `fallback` - `false` generates **404 page** for paths not returned by `getStaticPaths`, `true` tries to generate static HTML and sends JSON to browser
- Server-side Rendering - on each request
  - `async getServerSideProps: GetServerSideProps(context { params: { param: ... }, req, res, query: string, preview: boolean, previewData })` - called on each request, passes returned `{ props: { data } }` data to page's `props`
    - page component type `InferGetServerSidePropsType<typeof getServerSideProps>`
- **all functions** are eliminated from server output to client, see [Next.js - Code Elimination](https://next-code-elimination.now.sh/)
- Client-side Rendering - **custom**, **SWR**: `const { data, error } = useSWR('/api/user', fetch)`

## API

- types `NextApiRequest`, `NextApiResponse<Type>` #TODO
- **built in** middlewares `req.cookies`, `req.query` and `req.body`
- **per-route** `config` object
- **response helpers** `res.status(code)`, `res.json(json)` and `res.send(body: string | object | Buffer)`

## CSS

### CSS Module

```javascript
import styles from './Component.module.css'

<element className={styles.class}> // Inside the Component
```

### JSS

```javascript
return <p style={{ color: "red" }}>...</p>;
```

### Styled JSX

```javascript
return (<><style jsx>element { color: red }</style><style global jsx>body { color: blue }</style></>)
```

## See Also

### Stack

- [Node.js - Documentation](https://nodejs.org/en/docs/)
- [TypeScript - Documentation](https://www.typescriptlang.org/docs/home.html)
- [React - Documentation](https://reactjs.org/docs/getting-started.html)
- [Babel - Documentation](https://babeljs.io/docs/en/)
- [Webpack - Documentation](https://webpack.js.org/concepts/)
- [Browserslist](https://github.com/browserslist/browserslist)
- [PostCSS - Documentation](https://github.com/postcss/postcss/tree/master/docs)
- [CSS Modules](https://github.com/css-modules/css-modules)
- [Sass - Documentation](https://sass-lang.com/documentation)
- [JSS](https://cssinjs.org/)
- [Styled JSX](https://github.com/vercel/styled-jsx)
- [SWR - Documentation](https://swr.vercel.app/)

### Tools

- [Next.js - Code Elimination](https://next-code-elimination.now.sh/)

## Sources

- [Next.js - Documentation](https://nextjs.org/docs/getting-started)
