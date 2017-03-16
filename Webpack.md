#Webpack
https://github.com/joeeames/WebpackFundamentalsCourse

## Why Build Client side apps
* Multiple web request (combine fles)
* Code size (minify files)
* Order dependencies (use module system)
* Transpilations (compatibility to use Ecma Script 6 in browser that do not support it)
* Linting


## Other tools to around builds
* Server side tools
* Grunt or Gulp (task runners)
ES6 => js => min.js => combined
scss => css => min.css => combined
## Webpack
do everything tak runners do
plus can combine js and css together also

* Webpack uses NPM not bower
* Webpack uses all 3 module systems (AMD, CommonJs and EcmaScript) 

## CLI basics

(node has to be installed)
```
npm install webpack -g
npm ./app.js bundle.js   // this creates (outputs) bundle.js
```
now can run index:
app.js
```
document.write("some text inside html");
console.log('text in comand prompt');
```
index.html
```
<html>
    <body>
      <script src=="bundle.js"></script>
    </body>
</html>
```
we can run it also by just `webpack` if we have config file:
```
module.exports = {
  entry: "./app.js",
  output: {
    filename: ""
  },
  watch: true   //this will watch for file changes :)
}
```
runing dev server (with http url: http://localhost:8080/webpack-dev-server/):
* app is runing on http://localhost:8080
* inside IFrame that is on: http://localhost:8080/webpack-dev-server/ (that helps with auto refreshing)

```
npm install webpack-dev-server -g  //to install
webpack-dev-server                 // to run
```
we can run without iframe and with automatic reloading:
```
webpack-dev-server --inline
```

### Multiple files
app.js add `require("./login");`
or add config file as array:
```
entry: ["./login", "./app.js"],
```

### using loaders
that is how webpack learns new tricks
* add CS6 (babble) and hinting (jshint)
package.json added:
```
  "devDependencies": {
    "babel-core": "^6.24.0",
    "babel-loader": "^6.4.0",
    "babel-preset-es2015": "^6.24.0",
    "jshint": "^2.9.4",
    "jshint-loader": "^0.8.4",
    "node-libs-browser": "^2.0.0",
    "webpack": "^2.2.1"

  }
```



