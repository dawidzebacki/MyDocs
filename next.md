# Next

- [Next.js combined plugins](https://github.com/hashicorp/next-mdx-enhanced/issues/18#issuecomment-859167393)

```js
/**
 * @type {import('next').NextConfig}
 */

const nextConfig = {
  reactStrictMode: true,
  serverRuntimeConfig: {
    // Will only be available on the server side
    graphqlEndpoint:
      process.env.GRAPHQL_ENDPOINT || "http://api-gateway:4000/graphql",
  },
  publicRuntimeConfig: {
    // Will be available on both server and client
    graphqlClientEndpoint:
      process.env.GRAPHQL_CLIENT_ENDPOINT ||
      process.env.GRAPHQL_ENDPOINT ||
      "http://localhost:4000/graphql",
  },
};

const withImages = require("next-images");
// const withPlugins = require('next-compose-plugins');

// module.exports = withPlugins([withImages], nextConfig);

// module.exports = (phase, { defaultConfig }) => {
//   const plugins = [
//     withImages({
//       /* Plugin config here ... */
//     }),
//   ];
//   return plugins.reduce((acc, next) => next(acc), nextConfig);
// };

// next.config.js
module.exports = () => {
  const plugins = [withImages];
  return plugins.reduce((acc, next) => next(acc), nextConfig);
};
```
