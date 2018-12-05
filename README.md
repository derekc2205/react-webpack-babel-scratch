# Build [React](https://reactjs.org/) Project Using [Webpack 4](https://webpack.js.org/) and [Babel](https://babeljs.io/)

## Description

Following the guide [How to build a React project from scratch using Webpack 4 and Babel](https://hackernoon.com/how-to-build-a-react-project-from-scratch-using-webpack-4-and-babel-56d4a26afd32)

By [Sukhjinder Arora](https://hackernoon.com/@Sukhjinder) on [HackerNoon](https://hackernoon.com/)

---

## Packages

- [`@babel/core`](https://babeljs.io/docs/en/babel-core) : transform ES6 to ES5
- [`@babel/preset-env`](https://babeljs.io/docs/en/babel-preset-env) : preset to convert ES6/ES7/ES8 to ES5
- [`@babel/preset-react`](https://babeljs.io/docs/en/babel-preset-react) : preset to transform JSX to Javascript
- [`babel-loader`](https://github.com/babel/babel-loader) : webpack helper to transpile code given presets
- [`css-loader`](https://github.com/webpack-contrib/css-loader) : load and bundle CSS files
- [`html-webpack-plugin`](https://webpack.js.org/plugins/html-webpack-plugin/) : injecting scripts inside the HTML file and writes to dist/index.html
- [`react`](https://github.com/facebook/react) : JS library for building user interface
- [`react-dom`](https://github.com/facebook/react/tree/master/packages/react-dom) : react package for working with DOM
- [`style-loader`](https://github.com/webpack-contrib/style-loader) : add all styles nside the style tag of the document
- [`webpack`](https://github.com/webpack/webpack) : module bundler; bundle project files into single file
- [`webpack-cli`](https://github.com/webpack/webpack-cli) : command line interface for webpack
- [`webpack-dev-server`](https://github.com/webpack/webpack-dev-server) : serves webpack app; updates browser on changes

---

## Steps

1. create `src/components` and `src/styles` folders

   `mkdir -p src/components src/styles`

2. initialize `npm`. To **_skip all_** configs setting insert flag `-y`

   `npm init -y`

3. install **_Webpack_**, the module bundler that **_bundle project files_** into a **_single file_** for production

   `npm install webpack webpack-cli --save-dev`

4. install **_react_** and **_react-dom_**

   `npm install react react-dom`

5. install **_babel_**, the transpiler to **_transpile ES6 and JSX_** to **_ES5_**

   `npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev`

   - `babel-core`: **_transform_** ES6 to ES5
   - `babel-loader`: **_webpack helper_** to **_transpile code_**, given the preset
   - `babel-preset-env`: **_preset_** to help babel convert **_ES6, ES7 and ES8 code to ES5_**
   - `babel-preset-react`: **_preset_** to transform **_JSX_** to **_Javascript_**

6. add `index.js` in `./src` folder with code below

   `console.log('hello')`

7. add `index.html` in `./src` folder with a `<div id="root">` in the html structure

8. add `webpack.config.js` at `root` with the **_code_** below

   this file is used for **_defining rules_** for our **_loaders_** by defining the `entry` point and `output` directory

   in the code below, webpack will bundle **_all `_.js` files\*** into `index-bundle.js`

```javascript
 const path = require("path");

 module.exports = {
     entry: "./src/index.js",
     output: {
     path: path.join(\_\_dirname, "/dist"),
     filename: "index_bundle.js"
     }
 };
```

9. add **_webpack loaders_**, append in `webpack.config.js`, after `output: ...`

   loaders are responsible for **_loading and bundling_** the **_source files_**

   - `babel-loader`: to **_load_** `JSX/Javascript` files
   - `css-loader`: to **_load and bundle_** `CSS` files
   - `style-loader`: **_add_** all styles inside the **_style tag_** of the document

```javascript
module.exports = {
    ...,
    module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  }
}
```

10. install `css-loader` and `style-loader`

    `npm install css-loader style-loader --save-dev`

11. create file `.babelrc` in `root`

    this file is **_config for babel_** to **_use which presets_** for **_transpiling code_**

    - `preset-env`: to transpile **_ES6/ES7/ES8_** code to **_ES5_**
    - `preset-react`: to transpile **_JSX_** code to **_ES5_**

    ```javascript
    {
        "presets": [
            "@babel/preset-env",
            "@babel/preset-react"
        ]
    }
    ```

12. add `scripts` in `package.json` for **_compiling files using webpack_**

    - in `start` script, `--watch` flag is used to **_automatically compile_** all source files **_when changes is made_**
    - in `start` script, `--mode development` flag is used to **_produce easy to read codes_**
    - in `build`, `--mode production` flag is used to **_produce optimized files_** ready for production

    after running the `script`, webpack will transpile codes in `index.js`, `~/dist/index_bundle.js` will be created containing **_ES5 code_** from `index.js`

    ```javascript
    {
        scripts: {
            "start": "webpack --mode development --watch",
            "build": "webpack --mode production"
        }
    }
    ```

13. create `App.js` file in `~/src/components` with code below

    ```javascript
    import React, { Component } from "react";

    import "../style/App.css";

    class App extends Component {
      render() {
        return (
          <div>
            <h1>My React App!</h1>
          </div>
        );
      }
    }

    export default App;
    ```

14. create `App.css` file in `~/src/styles` with code below

    this file is to make sure `css-loader` and `style-loader` is working correctly

    ```css
    h1 {
      color: #27aedb;
      text-align: center;
    }
    ```

15. update `~/src/index.js` with the code below

    ```javascript
    import React from "react";
    import ReactDOM from "react-dom";
    import App from "./components/App";

    ReactDOM.render(<App />, document.getElementById("root"));
    ```

16. install `HTML-webpack-plugin` to generate an HTML file

    this is used for **_injecting scripts_** inside the HTML file and writes to `~/dist/index.html`

    `npm install html-webpack-plugin --save-dev`

17. update `webpack.config.js` for `html-webpack-plugin`

    - **_template key_** is the `./src/index.html` file as a template and generates new file named `index.html` in `~/dist` folder with `script` **_injected_**

    ```javascript
    const path = require("path");
    const HtmlWebpackPlugin = require("html-webpack-plugin");

    module.exports = {
        ...,
        plugins: [
            new HtmlWebpackPlugin({
                template: "./src/index.html"
            })
        ]
    }
    ```

> ## Intermission
>
> Running `npm start` **_here_** will generate `index_bundle.js` and `index.html` in `~/dist` folder.
> Opening `index.html` will now allow you to see the static webpage with the text **_My React App!_**.
> This approach **_has no hot reload_**, **_manual refresh_** is required as code changes.

18. install `webpack-dev-server` to enable **_hot reload_**

    `npm install webpack-dev-server --save-dev`

    and update `package.json` `start` script

    `"start": "webpack-dev-server --mode development --open --hot`

    - `open`: **_automatically opens_** webpage as the script runs
    - `hot`: **_automatically refreshes_** webpage as the code changes
