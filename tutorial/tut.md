# Vuejs + Vuetify

***For a more detailed explanation about this boilerplate, see the from scratch instructions below**

## Setup

- clone this repo, and open it in VsCode

- You'll want to install the `Vueter` extension in VsCode
  - syntax highlighting, snippets

- run `npm install` to install dependencies

## Running the app

- run `npm start` to start the development server

:+1:

---

## Add some stuff

- Go to https://vuetifyjs.com/en/ and browse the components

- We'll pick a couple of components, and paste them straight in the `<template>` tag

For example, you can take this `Jumbotron` component

![](2018-09-18-18-02-18.png)

and view its source by clicking here:

![](2018-09-18-18-03-34.png)
...and paste it directly in your source:

![](2018-09-18-18-05-01.png)

>note:  we must have a `<v-app>` tag wrapping your app at the root level, like this:

```html
<template>
<v-app>
  ...
</v-app>
</template>
```


### Using `Vue` single-file-components:

create another `.vue` file named `src/component.vue`, and paste the contents between `<v-app>` into its `<template>`

For example for a Jumbotron:
```html
<template>
  <v-jumbotron>
    <v-container fill-height>
      <v-layout align-center>
        <v-flex>
          <h3 class="display-3">Welcome to the site</h3>

          <span class="subheading">Lorem ipsum dolor sit amet, pri veniam forensibus id. Vis maluisset molestiae id, ad semper lobortis cum. At impetus detraxit incorrupte usu, repudiare assueverit ex eum, ne nam essent vocent admodum.</span>

          <v-divider class="my-3"></v-divider>

          <div class="title mb-3">Check out our newest features!</div>

          <v-btn
            class="mx-0"
            color="primary"
            large
          >
            See more
          </v-btn>
        </v-flex>
      </v-layout>
    </v-container>
  </v-jumbotron>
</template>

<script>
export default {
}
</script>

<style scoped>

</style>

```

now modify your `App.vue` to look like this:
```html
<template>
<v-app>
	<Component/>
</v-app>
</template>

<script>
import Component from './component.vue'


export default {
	components: {
		Component
	}
}
</script>

<style scoped>

</style>

```


You're now making composable applications with `Vue`+`Vuetify` !

:wave:




<details>
  <summary>From scratch instructions</summary>


---
Initialize a git repo (version contorl is good)
```sh
git init
```
---

Initialize a npm project

```sh
npm init -y # accept all the defaults
```

---

install `webpack`

```sh
npm install --save-dev webpack webpack-cli webpack-dev-server
```

- webpack is in charge of compiling your application
- magic

---

you don't want `node_modules` in your `git` history

We'll create a `.gitignore` file with this line:

```js
// .gitignore
node_modules
```


---

add `webpack.config.js`
- when webpack runs, it will use this config

```js
const path = require('path')
const webpack = require('webpack')
const VueLoaderPlugin = require('vue-loader/lib/plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')


module.exports = {
	entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'build.js',
  },
  resolve: {
    modules: ['src', 'node_modules'],
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: /node_modules/,
      },
      {
        test: /\.(png|jpg|gif|svg|json)$/,
        loader: 'file-loader',
        query: {
          name: '[name].[ext]?[hash]',
        },
      },
      {
        test: /\.html$/,
        loader: 'raw-loader',
      },
      {
        test: /\.css$/,
        loader: ['style-loader', 'css-loader'],
      }
    ],
  },
  devServer: {
    historyApiFallback: true,
    noInfo: false,
    open: true,
  },
  devtool: '#eval-source-map',

  plugins: [
    new VueLoaderPlugin(),
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],

  mode: process.env.NODE_ENV,
}

if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"',
      },
    }),
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      }
    })
  ])
}
```

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

scroll up to see the real error:

![](2018-09-18-15-57-00.png)


---

bring in the `webpack loaders` 
- these are in charge of interpreting the different types of files you're compiling (ex. `.vue .js .html`)

- we'll be installing the followling loaders:
  - `vue-loader` : .vue files
	- `babel-loader` : js files
	- `style-loader css-loader` : .css files
	- `file-loader` : any file as a filepath
	- `raw-loader` : any file as a raw string

```sh
npm install --save-dev vue-loader babel-loader style-loader css-loader file-loader raw-loader
```

---

We also need `webpack plugins`
- these do other things to your files (ex. copying files, minification)

- we'll be using the following `webpack plugins`:
  - `html-webpack-plugin` : automatically creates a `index.html` entry file for you

```sh
npm i -D html-webpack-plugin
```
---

But wait, `babel-loader` needs some more stuff

`babel` requires a whole host of dependencies in itself

```
npm i -D @babel/core @babel/preset-env
```


Now run `npm start` again

</details>