# Next.js

**This** cheat sheet **is missing:** Next.js advanced features, Next.js configuration and next/amp

## Usage

```bash
npx next [build | start | export | dev | telemetry]

npx create-next-app
```

## FileSystem Structure

- `.` - root
- `next.config.js` - Next.js configuration
- `[src/]pages` - pages source (if `pages` does not exist, `src/pages` is used)
- `[src/]pages` - a page, `**/*.[js | jsx | ts | tsx]` - a React component
- `[src/]pages/_app.[js | jsx | ts | tsx]` - custom `App`
  - imports `import 'path/to/styles.css'` allowed only here
- `[src/]pages/[_[document | error] | 404].[js | jsx | ts | tsx]` - custom `Document`, `Error` or 404 page
- `**/[name].module.[css | scss | sass | less | styl]` - CSS module, Sass module _(with configuration)_, Less and Stylus _(with plugin)_
- `[src/]pages/api/*` - an API handler `(req, res) => {...}`
- `public` - mapped to `/`, static assets
- `.env.local` - environment variables, loaded into `process.env`, to expose a variable to the browser use prefix `NEXT_PUBLIC_`
  - `.env.development`, `.env.production` - development and production environment variables default, overriden by `.env.local`
- `jsconfig.json` or `tsconfig.json`, `.babelrc`, `postcss.config.json` - JavaScript or TypeScript configuration, Babel, PostCSS configuration

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

## Advanced Features

- **[Preview Mode](https://nextjs.org/docs/advanced-features/preview-mode)**, **[Dynamic Import](https://nextjs.org/docs/advanced-features/dynamic-import)**, **[AMP Support](https://nextjs.org/docs/advanced-features/amp-support/introduction)**, **[Custom Server](https://nextjs.org/docs/advanced-features/custom-server)**, **[Multi Zones](https://nextjs.org/docs/advanced-features/multi-zones)**
- **Automatic Static Optimization** - in the absence of `getServerSideProps` or `getInitialProps`
- **Static HTML Export** - use `next export`
- **Customizing Target Browsers** - `package.json` `{ "browserslist": [ ... browserslist array ... ]}`
- **Measuring performance** - add to `[src/]pages/_app.js`: `export function reportWebVitals(metric: { id, name, startTime, value, label }) { ... }`
- **Debug mode** - add Next.js inspect flag `NODE_OPTIONS='--inspect' next dev`, go to go to `chrome://inspect` or use Visual Studio Code _attach mode_,

## Configuration

- `next.config.js` - regular Noe.js module

```javascript
module.exports = (phase /* see next/constants */, { defaultConfig }) => {
  return {
    env: { var1: val1, ... }, // Environment variables object
    pageExtensions: [ 'js', 'jsx', ... ], // Page extensions array
    assetPrefix: 'https://cdn...', // CDN asset prefix string
    serverRuntimeConfig: { var1: val1, ... }, // Server runtime configuration, to access config use next/config
    publicRuntimeConfig: { var1: val1, ... }, // Server and client runtime configuration, to access config use next/config
    target: 'server' | 'serverless', // Build target
    distDir: 'build', // Custom build directory
    generateBuildId: async () => { ... }, // Custom build ID
    typescript: { ignoreBuildErrors: true }, // Ignore build TypeScript errors
    exportPathMap: async (defaultPathMap, { dev, dir, outDir, distDir, buildId }) => { return { '/path/to/page': { page: '/path', query?: { param1: val1, ... } }, ... } }, // Eport pages as HTML files
    exportTrailingSlash: true, // Export pages as HTML files with trailing slash
    webpack: (config, { buildId, dev, isServer, defaultLoaders, webpack }) => { return config }, // Custom webpack configuration
    webpackDevMiddleware: (config) => { return config }, // Custom webpack development middleware configuration
    compress: false, // Turn off gzip compression, only for target: 'server'
    poweredByHeader: false, // Turn off x-powered-by HTTP header
    generateEtags: false, // Turn off etags HTTP header
    devIndicators: { autoPrerender: boolean } // Development indicators
    onDemandEntries: { maxInactiveAge: integer, pagesBufferLength: integer } // Development buffer fine tuning, see https://nextjs.org/docs/api-reference/next.config.js/configuring-onDemandEntries
  };
};
```

## See Also

### Next.js Stack

- [Node.js - Documentation](https://nodejs.org/en/docs/)
- [TypeScript - Documentation](https://www.typescriptlang.org/docs/home.html)
- [React - Documentation](https://reactjs.org/docs/getting-started.html)
- [Babel - Documentation](https://babeljs.io/docs/en/)
- [Webpack - Documentation](https://webpack.js.org/concepts/)
- [Browserslist](https://github.com/browserslist/browserslist)
- [PostCSS - Documentation](https://github.com/postcss/postcss/tree/master/docs)
- [PostCSS Autoprefixer](https://github.com/postcss/autoprefixer)
- [CSS Modules](https://github.com/css-modules/css-modules)
- [Sass - Documentation](https://sass-lang.com/documentation)
- [JSS](https://cssinjs.org/)
- [Styled JSX](https://github.com/vercel/styled-jsx)
- [SWR - Documentation](https://swr.vercel.app/)
- [Web Vitals](https://web.dev/vitals/)

### Tools

- [Next.js - Code Elimination](https://next-code-elimination.now.sh/)
- [browserl.ist](https://browserl.ist/)

## Sources

- [Next.js - Documentation](https://nextjs.org/docs/getting-started)
