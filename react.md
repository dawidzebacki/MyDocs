# React

- [Storybook](https://dev.to/estheragbaje/learn-to-use-storybookjs-in-your-react-project-4nf2)
- [GraphQL Diving deep](https://dev.to/timecampus/graphql-diving-deep-4hnm)
- [React Router Hooks](https://dev.to/dauntless/react-routers-useroutes-hook-38fc)
- [React Testing](https://dev.to/ohdylan/react-component-testing-54ie)
#### Private Route in react-router

```js
const PrivateRoute = ({
  component,
  isAuthenticated,
  isRouteEnabled = true,
  ...rest
}: any) => {
  const routeComponent = (props: any) =>
    isAuthenticated ? (
      isRouteEnabled ? (
        React.createElement(component, props)
      ) : (
        <>
          {dashboardMessage(
            DashboardMessageTypes.warning,
            "You don't have access to this resources.",
            5
          )}
          <Redirect to={{ pathname: "/welcome" }} />
        </>
      )
    ) : !isAuthenticated ? (
      <Redirect to={{ pathname: "/login" }} />
    ) : (
      <Redirect to={{ pathname: "/welcome" }} />
    );
  return <Route {...rest} render={routeComponent} />;
};
```

#### How I'm structuring directories

```
└── /src
    ├── /assets
    ├── /components
    ├── /context
    ├── /hooks
    ├── /pages
    ├── /services
    ├── /utils
    ├── App.js
    └── index.js
```

```
└── /src
    ├── /components
    |   ├── /Button
    |   |   ├── Button.js
    |   |   ├── Button.styles.js
    |   |   ├── Button.test.js
    |   |   ├── Button.stories.js
    |   ├──index.js
```

- `Button.js` file that contains the actual React component
- `Button.styles.js` file that contains corresponding styles
- `Button.test.js` file that contains tests
- `Button.stories.js` storybook file

```js
// /src/components/index.js
import { Button } from "./Button/Button";
export { Button };
```

- `index.js` acts as an index of all components that are part of the namesake directory.
