#Learning Babel 6 with ES6 

([ECMAScript 6](http://es6-features.org/) aka es2015)    
[babel compatibility table](http://kangax.github.io/compat-table/es6/#babel)     
[babel playground](http://babeljs.io/repl/)    
[browserstack](https://www.browserstack.com)

##Installing babel
Installing globaly 
```bash
npm install -global babel-cli 
babel --version
npm ls -g --depth 0
```

##installing locally is better practice
- installing localy so that project can be shared with other users (saved in package.json)   
- also allows to have different versions of babel per project   
- npm install would install anything as per packages.json file   
```bash
npm init # creates package.json file
npm install babel-cli --save-dev 
node_modules/.bin/babel --version 
```

##Using babel to transpile js
install babel preset. Otherwise would not know which version to transocde to: 
```
npm install babel-preset-es2015 --save-dev 
```

using babel preset to transpile: 
```bash
babel src --presets es2015 # this will transpile to the console all js files in this directory

babel src --presets es2015 --out-dir build   #same as below: (save to output directory)
babel src --presets es2015 -d build 

babel src --presets es2015 --out-file build/bundle.js   #same as below: 
babel src --presets es2015 -o build/bundle.js 

babel src --presets es2015 -o build/bundle.js -s    #(to add source map file - good for debugging) 
babel src --presets es2015 -o build/bundle.js -s -w #(to watch file for changes ) 
```

##.babelrc
using .babelrc for configuration and therefore minify our command line from being too long.        
When in doubt what libraries preset include we can check from babel website: [here](http://babeljs.io/docs/plugins/preset-es2015/)    
We see there that **commonjs** is default for this preset.    
```json
{ 
"presets" : ["es2015"], 
"sourceMaps": true 
} 
```
now we can transpile using shorther string (ommitting: `--presets es2015 -s`): 
```bash
babel src -o build/bundle.js 
```


##Different specifications and formatters
Module formatters plugins can utilize multiple module or most popular specifications    
- CommonJS   
  * Node.js (server)    
  * Browserify (browser)    
- AMD (Ansynchronous Module Definition) popular for ansynchronously loading of modules    
  * RequireJS   
  * Dojo Toolkit   
  * ScriptMainJS    

Following 2 try to unify above 2 specifications in their own way.     
- UMD   
- SystemJS   

Above are only specifications, and need implementations to be used in practice.   
Implementations of above modules can be used with babel by including these [modules](http://babeljs.io/docs/plugins/#modules).   
That way es2015 can be turn into any specification format we like.   

For **AMD** environment most common is RequireJS that is included in your html and configurations and your js will be loaded by ajax when needed. Other ones are dojo toolkit and ScriptManJS.   
For **CommonJS** environment on the **server** you just need to run it on Node.js since it supports this specification.   
For **CommonJS** environment on the **browser** you just need to include **browerify**.   

To use AMD specification instead of default one CommonJS, we would remove preset (that uses commonjs) and use all plugins manually that we need:  
```json
{ 
"plugins" : ["transform-es2015-block-scoping", 
             "transform-es2015-block-literlas",
             "transform-es2015-modules-amd"], 
"sourceMaps": true 
} 
```
Now when we run babel, it would use AMD specification.

##Browser support

**Shim** refers to any piece of code that performs interception of an API call and provides a layer of abstraction.    
**Polyfill** is a type of shim that retrofits legacy browsers with moredn HTML/CSS/js features (browser APIs) usually usging js.    

```
npm install babel-polyfill --save
```
babel polyfill uses:  
* core-js
* Regenerator runtime

###core-js
* core-js    
  * Scope is all of the ES5, ES6, ES7 and the future
  * Modular   
  * does not polute global namespace
alternative is:
ES Shims   
* Scope is specific ES5 or ES6 ...  
* not modular   
* polute global namespace   

###Regenerator runtime
It is facebook open source. It has 2 parts:    
* transform (babel already has that)
* runtime (babel needs this part to run it on the browser)

### Make features work on browser

There are 2 options. We can **Polyfill** them or we can **Transpile** them.  
When look at babel [docs](http://babeljs.io/docs/learn-es2015/), we can see for each feature weather is supported by polyfill or transpiling.



#### Polyfill
Include libs:
```
npm install babel-polyfill --save
```
include it to the html page:
```html
<script type="text/javascript" src="../node_modules/bable-polyfill/dist/polyfill.js"></script>
```

If some feature is not supported via polyfill we have to use transpile

#### Transpile

```
babel src --o dist
```
with .babelrc:
```json
{ 
"presets" : ["es2015"],
"plugins": []
} 
```
can also run it on node to test script. Node supports commonJS:
```
node sometest_module.js
```

#### Older browser ES3

| ES3  | ES5      |
| ----:|:--------:|
| IE8+ | IE9+     |
| CH5+ | CH6-19+  |
| FF3+ | FF4+     |
| SF4+ | SF5-6+   |


In case of older browsers or that still have some features not working after polyfill and transpile:   
Go to babel plugins, and for ES3 you might need plugin for example [this one](http://babeljs.io/docs/plugins/transform-es3-member-expression-literals/):
```
npm install babel-plugin-transform-es3-member-expression-literals --save-dev
npm install babel-plugin-transform-es3-property-literals --save-dev
```
use that plugin:
```json
{ 
"presets" : ["es2015"],
"plugins": ["transform-es3-member-expression-literals",
            "transform-es3-property-literals"]
} 
```
run transpile and then it will work for IE9


##Integrating babel in your build

###npm
npm looks at the package.json for existing scripts:
```
"scripts": {
    "demo": "babel --version",
    "build.js": "babel src -o dist"
  }
```

###gulp
```
npm install gulp -g  
npm install gulp --save-dev
npm install gulp-babel --save-dev
```
create gulpfile.js:
```js
var gulp = require('gulp');
var gulp = require('gulp-babel');

gulp.task('default', function(){
 return gulp.src('src/*.js')
            .pipe(babel())
            .pipe(gulp.dest('dist'))
});
```
and run the task:
```
gulp
```
#### gulpfile.js with new version of es6
For node verion 4 or later below updated script will just work:
```js
const gulp = require('gulp');
const gulp = require('gulp-babel');

gulp.task('default', ()=>{
 return gulp.src('src/*.js')
            .pipe(babel())
            .pipe(gulp.dest('dist'))
});
```

but if you run older version of node `node -v` then:
* rename your `gulpfile.js` to `gulpfile.babel.js`   
* run `npm install babel-core --save-dev`

