

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
to make sure package has a start script you can look into package.json `cat package.json`
```json
"scripts": {
    "init":"npm install",
    "install":"bower install",
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
```bash
npm init
npm init -y #with all defaults created
```
also can save defalt values to your user directory: 
* To set it: `npm set init-license 'MIT'`
* To get it: `npm get init-license`
* To delete it: `npm config delete init-license`
* Location of the file: `ls ~/.npmrc`
 
##NPM installing packages (aka libraries)

Install to "dependancies" section that you need in PRODUCTION: (like angular)
```bash
npm install PACKAGE --save # or
npm install PACKAGE -S     # or
npm i PACKAGE -S
```

Install to "devDependancies" section that you need in DEV: (like karma)
```bash
npm install PACKAGE --save-dev # or
npm install PACKAGE -D         # or
npm i PACKAGE -D
```

Show all libraries installed:
```bash
npm list                          #all packages installed
npm list --debth 1                #all packages installed with 1 level of dependancies
npm list --debth 0                #all packages you install 
npm list --global true            #all global packages installed
npm list --global true --depth 0  #all global packages that you installed
npm list --depth 0 --long true    #more info about each package
npm list --depth 0 --json true    #more info about each package in json format

npm list --depth 0 --dev true     #more info about each package in json format
npm list --depth 0 --prod true    #more info about each package in json format

```
(also shorthands for list are ls la ll)

Some packages you need globaly otherwise they would not run on command line.
* gulp
* grunt
* karma
* ...
```
npm i PACKAGE -g
```
to view global packages you installed: `npm list -g --depth 0`




