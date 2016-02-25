#Learning Babel 6 with ES6 

([ECMAScript 6](http://es6-features.org/) aka es2015)    
[babel compatibility table](http://kangax.github.io/compat-table/es6/#babel)     
[babel playground](http://babeljs.io/repl/)    



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

##Using babel to transcode js
install babel preset. Otherwise would not know which version to transocde to: 
```
npm install babel-preset-es2015 --save-dev 
```

using babel preset to transcode: 
```bash
babel src --presets es2015 # this will transcode to the console all js files in this directory

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
We see there that commonjs is default for this preset.    
```json
{ 
"presets" : ["es2015"], 
"sourceMaps": true 
} 
```
now we can transcode using shorther string (ommitting: `--presets es2015 -s`): 
```bash
babel src -o build/bundle.js 
```


##Different specifications and formatters
Module formatters plugins can utilize multiple module or most popular specifications    
- CommonJS (generally followed for node js)   
- AMD (ansynchronous module definition) popular for ansynchronously loading of modules    

Following 2 try to unify above 2 specifications in their own way.     
- UMD   
- SystemJS   

Above are only specifications, and need implementations to be used in practice.   
Implementations of above modules can be used with babel by including these [modules](http://babeljs.io/docs/plugins/#modules).   
That way es2015 can be turn into any specification format we like.   

For AMD environment most common is RequireJS that is included in your html and configurations and your js will be loaded by ajax when needed. Other ones are dojo toolkit and ScriptManJS.   
For CommonJS environment on the server you just need to run it on Node.js since it supports this specification.   
For CommonJS environment on the browser you just need to include browerify.   

To use AMD specification instead of default one commonJS, we would remove preset (that uses commonjs) and use all plugins manually that we need:  
```json
{ 
"plugins" : ["transform-es2015-block-scoping", 
             "transform-es2015-block-literlas",
             "transform-es2015-modules-amd"], 
"sourceMaps": true 
} 
```
Now when we run babel, it would use AMD specification.


