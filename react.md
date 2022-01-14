# React

- [Storybook](https://dev.to/estheragbaje/learn-to-use-storybookjs-in-your-react-project-4nf2)
- [GraphQL Diving deep](https://dev.to/timecampus/graphql-diving-deep-4hnm)

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
