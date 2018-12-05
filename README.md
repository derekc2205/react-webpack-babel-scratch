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

    * `babel-core`: **transform** ES6 to ES5
    * `babel-loader`: webpack **helper to transpile code**, given the preset
    * `babel-preset-env`: **preset** to help babel convert **ES6, ES7 and ES8 code to ES5**
    * `babel-preset-react`: **preset** to transform **JSX** to **Javascript**