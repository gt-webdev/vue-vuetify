install `webpack`

```sh
npm i -D webpack webpack-cli webpack-dev-server
```

- webpack is in charge of compiling your application

---

add `webpack.config.js`
- when webpack runs, it will use this config

---

we'll also add the bare-bones of our app: `src/main.js` and `src/index.html`

add some scripts to your `package.json`, which allow you to run webpack
- for development: 
  ```sh
	npm start`
	```
- for production build:
  ```sh
	npm run build`
	```

---

run your development script: `npm start` and...errors:

![](2018-09-18-15-41-09.png)

:+1:


