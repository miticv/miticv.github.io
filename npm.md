

#NPM
[Node Package Manager](https://www.npmjs.com/)          
[NPM PlayBook](https://github.com/joeeames/NPMPlaybookCourse)             

* Module  - is js file 
* Package - is directory with js files in it, with `package.json` file that contain info about that package.

##Typical usage
```bash
git clone https://github.com/joeeames/trip-to-mars-typical
cd trip-to-mars-typical
npm install #it will install any dependencies
npm start # to see it in action
```
to make sure package has a start script you can look into package.json
```json
"scripts": {
    "start":"node server.js",
    "test": "node test.js"
  }
```

##NPM help
```bash
npm -h # general help for npm 
npm install -h # command promp help for install command
npm help install # opens up browser to help you with install command
npm help-search remove #search for remove key word
```
Shorthands commands can be found on [npm configuration help](https://docs.npmjs.com/misc/config)

##Creating package.json file
```
npm init
```




