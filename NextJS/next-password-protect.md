# next-password-protect

Define your password in .env file. For development use .env.local and add YOUR_SECRET_PASSWORD there. 

In [Step 2](https://github.com/instantcommerce/next-password-protect#step-2) of the setup docs be sure to name the api files `login.js` and `passwordCheck.js` if you want to use the default routes of `/login` and `/passwordCheck`. 

in [Step 3](https://github.com/instantcommerce/next-password-protect#step-3) be sure App is declared before the export default. Below is the [example code](https://github.com/instantcommerce/next-password-protect/blob/master/example/src/pages/_app.tsx) from the live demo:

```js
class MyApp extends App {
  componentDidMount() {
    objectFitImages();
  }

  render() {
    const { Component, pageProps } = this.props;
    return (
        ...
    );
  }
}

export default process.env.PASSWORD_PROTECT
  ? withPasswordProtect(MyApp, {
      loginComponentProps: {
        backUrl: 'https://github.com/instantcommerce/next-password-protect',
        logo: 'https://avatars.githubusercontent.com/u/93975473',
      },
    })
  : App;
```

## *Resources*

- [Github repo](https://github.com/instantcommerce/next-password-protect)