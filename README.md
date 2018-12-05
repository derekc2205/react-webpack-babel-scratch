# react-webpack-babel-scratch

1. create src/components and src/styles folders

   `mkdir -p src/components src/styles`

2. initialize NPM. To skip all configs insert flag `-y`

   `npm init -y`

3. install **Webpack**, the module bundler that **bundle project files** into a **single file** for production

   `npm install webpack webpack-cli --save-dev`

4. install **react** and **react-dom**

   `npm install react react-dom`

5. install **babel**, the transpiler to **transpile ES6 and JSX** to **ES5**

   `npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev`

   - `babel-core`: **transform** ES6 to ES5
   - `babel-loader`: webpack **helper to transpile code**, given the preset
   - `babel-preset-env`: **preset** to help babel convert **ES6, ES7 and ES8 code to ES5**
   - `babel-preset-react`: **preset** to transform **JSX** to **Javascript**

6. add `index.js` in `./src` folder with code below

   `console.log('hello')`

7. add `index.html` in `./src` folder with a `<div id="root">` in the html structure

8. add `webpack.config.js` at `root` with the **code** below

   this file is used for **defining rules** for our **loaders** by defining the `entry` point and `output` directory

   in the code below, webpack will bundle **all `*.js` files** into `index-bundle.js`

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

9. add **webpack loaders**, append in `webpack.config.js`, after `output: ...`

   loaders are responsible for **loading and bundling** the **source files**

   - `babel-loader`: to **load** `JSX/Javascript` files
   - `css-loader`: to **load and bundle** `CSS` files
   - `style-loader`: **add** all styles inside the **style tag** of the document

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

    this file is **config for babel** to **use which presets** for **transpiling code**

    - `preset-env`: to transpile **ES6/ES7/ES8** code to **ES5**
    - `preset-react`: to transpile **JSX** code to **ES5**

    ```javascript
    {
        "presets": [
            "@babel/preset-env",
            "@babel/preset-react"
        ]
    }
    ```

12. add `scripts` in `package.json` for **compiling files using webpack**

    - in `start` script, `--watch` flag is used to **automatically compile** all source files **when changes is made**
    - in `start` script, `--mode development` flag is used to **produce easy to read codes**
    - in `build`, `--mode production` flag is used to **produce optimized files** ready for production

    after running the `script`, webpack will transpile codes in `index.js`, `~/dist/index_bundle.js` will be created containing **ES5 code** from `index.js`

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

    this is used for **injecting scripts** inside the HTML file and writes to `~/dist/index.html`

    `npm install html-webpack-plugin --save-dev`

17. update `webpack.config.js` for `html-webpack-plugin`

    - **template key** is the `./src/index.html` file as a template and generates new file named `index.html` in `~/dist` folder with `script` **injected**

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

### Intermission

Running `npm start` will generate `index_bundle.js` and `index.html` in `~/dist` folder

Opening `index.html` will now allow you to see the static webpage with the text **My React App!**

This approach **has no hot reload**, **manual refresh** is required as code changes

18. install `webpack-dev-server` to enable **hot reload**

    `npm install webpack-dev-server --save-dev`

    and update `package.json` `start` script

    `"start": "webpack-dev-server --mode development --open --hot`

    - `open`: **automatically opens** webpage as the script runs
    - `hot`: **automatically refreshes** webpage as the code changes
