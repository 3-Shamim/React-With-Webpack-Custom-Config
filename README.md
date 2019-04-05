## Make directory {Project Name}

mkdir {folder-name} && cd {folder-name}/

## Git ignore file if you want to git it

## Initialize npm and Config

npm init -y

npm config list

npm set init.author.name <Your Name>
npm set init.author.email you@example.com
npm set init.author.url example.com
npm set init.license DEMO

## Install React and ReactDom

npm install --s react react-dom

## Need to create all neccessary file

mkdir src
cd src/
touch index.js App.js index.html index.css

## index.js

```
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import "./index.css";

ReactDOM.render(<App />, document.getElementById("app"));
```

## App.js

```
import React, { Component } from "react";

class App extends Component {
  state = {};
  render() {
    return (
      <div>
        <h2>Hello World!</h2>
      </div>
    );
  }
}

export default App;
```

## index.html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>React With Webpack</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

## Install webpack and need to config webpack.config.js

npm install --save-dev webpack webpack-cli webpack-dev-server

## Install babel and need to config on package.json and webpack.config.js

npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react
npm install --save-d @babel/plugin-proposal-class-properties

## Install css and html-loader and need to webpack.config.js

npm install --save-dev css-loader style-loader html-webpack-plugin html-loader

## Install babel and need to config on package.json and webpack.config.js

npm install --save-dev file-loader

## webpack.config.js

```
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "index_bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: ["babel-loader"]
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      },
      {
        test: /\.(png|jpg|svg|gif)$/,
        use: ["file-loader"]
      }
    ]
  },
  resolve: {
    extensions: ["*", ".js", ".jsx"]
  },
  mode: "development",
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    })
  ]
};
```

## package.json

```
{
  "name": "react-with-webpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "babel": {
    "presets": [
      "@babel/preset-env",
      "@babel/preset-react"
    ],
    "plugins": [
      "@babel/plugin-proposal-class-properties"
    ]
  },
  "scripts": {
    "create": "webpack",
    "start": "webpack-dev-server --mode development --open",
    "build": "webpack --mode production",
    "start-server": "webpack-dev-server --config ./webpack.config.js --mode development"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6"
  },
  "devDependencies": {
    "@babel/core": "^7.4.3",
    "@babel/plugin-proposal-class-properties": "^7.4.0",
    "@babel/preset-env": "^7.4.3",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.5",
    "css-loader": "^2.1.1",
    "file-loader": "^3.0.1",
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "react-hot-loader": "^4.8.2",
    "style-loader": "^0.23.1",
    "webpack": "^4.29.6",
    "webpack-cli": "^3.3.0",
    "webpack-dev-server": "^3.2.1"
  }
}
```
