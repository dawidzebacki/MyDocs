# Next

- [Next.js combined plugins](https://github.com/hashicorp/next-mdx-enhanced/issues/18#issuecomment-859167393)

#### Next.js private routes

- [Article setup](https://medium.com/@eslamifard.ali/how-to-simply-create-a-private-route-in-next-js-38cab204a99c)
<details>
  <summary>TS file</summary>

```js
//@components/templates/PrivateRoute file
import React from "react";
import Router from "next/router";
import { NextPageContext } from "next";
import { NextPageWithLayout } from "pages/_app";

// Pointing to 403.tsx page (access denied)
const accessDenied = "/403";

interface Context extends NextPageContext {
  auth: {
    isAdmin: boolean,
  };
}

const checkUserAuthentication = () => {
  //TODO: create user/admin proper authentication
  return { auth: null }; // no access
  //   return { auth: { isAdmin: true } }; // access
};

const withPrivateRoute = (WrappedComponent: NextPageWithLayout) => {
  const higherOrderComponent = ({ ...props }) => (
    <WrappedComponent {...props} />
  );

  higherOrderComponent.getInitialProps = async (context: Context) => {
    const userAuth = await checkUserAuthentication();

    if (!userAuth?.auth) {
      // Handle server-side and client-side rendering.
      if (context.res) {
        context.res?.writeHead(302, {
          Location: accessDenied,
        });
        context.res?.end();
      } else {
        Router.push(accessDenied);
      }
    } else if (WrappedComponent.getInitialProps) {
      const wrappedProps = (WrappedComponent.getInitialProps = async (
        context: Context
      ) => {
        return {
          ...context,
          auth: userAuth,
        };
      });

      return { ...wrappedProps, userAuth };
    }

    return { userAuth };
  };

  higherOrderComponent.getLayout = WrappedComponent.getLayout;

  return higherOrderComponent;
};

export default withPrivateRoute;

//Private Route page
import type { ReactElement } from 'react';
import { Layout } from '@components/templates/Layout';
import { withPrivateRoute } from '@components/templates/PrivateRoute';

const PrivateRoute = () => {
  return <div>If you can see me, you have access to private routes!</div>;
};

PrivateRoute.getLayout = function getLayout(page: ReactElement) {
  return <Layout title="Private route">{page}</Layout>;
};

export default withPrivateRoute(PrivateRoute);
```

</details>

#### Next.js static images

- declare proper extensions in your `types/global.d.ts` file.

```jsx
declare module '*.png';
declare module '*.jpg';
```

- add disablingStaticImages to your `next.config.js` file.

```jsx
images: {
    // disablingStaticImages resolves error with passing a reference of static image to component
    disableStaticImages: true,
},
```

- import static image files and set them as src.

```jsx
import background from "./background.png";

export const Container = styled.div`
  background-image: url(${background});
`;
```

#### Next.js with styled components

- [Example app with styled-components](https://github.com/vercel/next.js/tree/canary/examples/with-styled-components)

or you can install it yourself.

```
yarn add styled-components
yarn add babel-plugin-styled-components
```

Then add 2 files. .babelrc to the root folder. and \_document.js to pages

<details>
<summary>.babelrc</summary>
</details>

```
{
  "presets": ["next/babel"],
  "plugins": ["styled-components"]
}
```

<details>
<summary>_document.js</summary></details>

```js
import Document from "next/document";
import { ServerStyleSheet } from "styled-components";

export default class MyDocument extends Document {
  static async getInitialProps(ctx) {
    const sheet = new ServerStyleSheet();
    const originalRenderPage = ctx.renderPage;

    try {
      ctx.renderPage = () =>
        originalRenderPage({
          enhanceApp: (App) => (props) =>
            sheet.collectStyles(<App {...props} />),
        });

      const initialProps = await Document.getInitialProps(ctx);
      return {
        ...initialProps,
        styles: (
          <>
            {initialProps.styles}
            {sheet.getStyleElement()}
          </>
        ),
      };
    } finally {
      sheet.seal();
    }
  }
}
```
