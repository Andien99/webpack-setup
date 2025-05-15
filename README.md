# webpack-setup
list of general codes and their function to use when building a project with a webpack  bundler

# Installs: webpack: The core bundling tool & webpack-cli: Enables running Webpack from the command line.
npm install --save-dev webpack webpack-cli

# Makes a src directory with index.js to run
mkdir src && touch src/index.js

# Creates a webpack config file
touch webpack.config.js
    Webpack should contain:
    const path = require("path");
    module.exports = {
      mode: "development",
      entry: "./src/index.js",
      output: {
        filename: "main.js",
        path: path.resolve(__dirname, "dist"),
        clean: true,
      },
    };

# Installs HTML Handling plugin
npm install --save-dev html-webpack-plugin
    webpack.config.js should contain:
      plugins: [
    new HtmlWebpackPlugin({
      template: "./src/template.html",
    }),
  ],

#  Installs CSS Loader MODULE
npm install --save-dev style-loader css-loader
    webpack.config.js MODULE should contain:
      module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
    ],

# Installs HTML Loader (detects image file paths in the HTML template)
npm install --save-dev html-loader
    webpack.config.js MODULES should contain:
    {
  test: /\.html$/i,
  loader: "html-loader",
    }
    {
  test: /\.(png|svg|jpg|jpeg|gif)$/i,
  type: "asset/resource",
  }

# Installs webpack live preview
npm install --save-dev webpack-dev-server
  webpack.config.js > module.exports = { should contain
    devtool: "eval-source-map",
  devServer: {
    watchFiles: ["./src/template.html"],
  },

to start, issue command: npx webpack serve
preview URL: http://localhost:8080/

# final config:

// webpack.config.js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  devtool: "eval-source-map",
  devServer: {
    watchFiles: ["./src/template.html"],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/template.html",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.html$/i,
        loader: "html-loader",
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: "asset/resource",
      },
    ],
  },
};

