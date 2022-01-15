# Netlify

- Build failed, Treating warnings as errors because process.env.CI = true

```
  CI= yarn build
  CI= npm run build
```

- Netlify renders 404 on page refresh (using React and react-router)

add \_redirects file inside the /public folder.

```
/*  /index.html  200
```
