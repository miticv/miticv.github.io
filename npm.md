

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

##NPM removing packages

```
npm uninstall PACKAGE        # removes package from your machine (not from your "dependencies" package.json file)
npm uninstall PACKAGE --save # removes package from your "dependencies" package.json file (cannot use -S here!)
npm uninstall PACKAGE -g     # removes package from your global space
```

##NPM installing specific versions of packages

Major.Minor.Patch
Patch = bug fixes
Minor = new features (existing functionality not broken)
Major = signatures change

```bash
npm i PACKAGE                   # will install the latest version
npm i PACKAGE@1.8.2             # will install the specific version 
npm i PACKAGE@1.8               # will install the latest 1.8 version
npm i PACKAGE@1                 # will install the latest 1 version
npm i PACKAGE@">1.1.0"          # will install any version bigger than 1.1.0 version (not inclusive)
npm i PACKAGE@">=1.1.0"         # will install any version bigger or equal 1.1.0 version
npm i PACKAGE@">=1.1.0 <1.4.0"  # will install any version bigger or equal 1.1.0 version and less than 1.4.0
npm i PACKAGE@">=1.1.0 <1.4.0 || .."  # you can add || (or) statement as well but this is rarelly needed
```
common scenarios:
* latest `npm i PACKAGE` will add to dependencies `"PACKAGE": "^1.8.3"`      
  package will be upgraded if author of the libraries upgrade the patch or minor version 
* specific `npm i PACKAGE@1.8.2 --save --save-exact` will add to dependencies `"PACKAGE": "1.8.2"`      
  package will not be upgraded. Used for mission critical apps that need testing and large teams.    
  this work for both --save and --save-dev


##NPM installing existing packages

```bash
npm install   # will install all packages from your package.json file
```

* tilda ~ means we want the latest version of the **minor** release:    
  `"PACKAGE": "~1.8.2"` would install 1.8.**2**, 1.8.**3**, 1.8.**4** ...
* carrot ^ means we want the latest version of the **major** release:    
  `"PACKAGE": "^1.8.2"` would install 1.8.**2**, 1.8.**3**, 1.**9.1**, 1.**9.2** ...
* star * means we want the latest version of the library:    
  `"PACKAGE": "*"`
* no prefix: means we want the exact varsion of the library:    
  `"PACKAGE": "1.8.2"`


##NPM updating existing packages

```bash
npm update   # will update all packages according to your package.json file
```
usually not done but you can update only your prod or dev dependencies:
```bash
npm update --dev   # will update "devDependencies" in your package.json file
npm update --prod  # will update "dependencies" in your package.json file
```
update one dependency at the time:
```bash
npm update PACKAGE   # will update only package PACKAGE according to your package.json file
```
update one dependency at the time:
```bash
npm update -g           # will update ALL global dependencies
npm update -g PACKAGE   # will update global dependency PACKAGE 
```


#Advanced NPM

##Installing from url

If you dont know npm name like: `npm install express`, you can install from git hib directly:
```bash
npm install https://github.com/strongloop/express
```
that would work from any url that contains the package.

## installing gist as package
every gist has HASH in the url
```bash
npm install gist:HASH        # it might say 'extraneous' when listed as npm list --depth 0
npm install gist:HASH --save #to include it in our package.json as "gist:HASH" as version.
```

## installing from folder

```bash
npm install ../hello-mars
```

## npm registry

Search registry on [npmjs.com](http://www.npmjs.com)      
Or look directly package for example: [underscore](http://registry.npmjs.org/underscore)     
Or look at npm.im: [underscore](http://npm.im/underscore)     

## npm search

```bash
npm search TEMPLATE
```
but not usefull better use: [npmjs.com](http://www.npmjs.com) and search there

## npm prune

```bash
npm list --depth 0
```
will list all packages as `extrenious` - if they are not being used in any of your package.json files.

```bash
npm prune
```
will remove all packages not being used in any of your package.json files

```bash
npm prune --production
```
will remove all dev dependencies

## npm repo
`npm repo PACKAGE` will open browser for this repository

## upgrade npm
MAKE SURE your command prompt is administrator!
```
npm install npm@latest -g
```

##npm simple scripts

most common to have:
`npm test`, `npm start`
full list are in [documentation](https://docs.npmjs.com/misc/scripts) but most not ones you will be used.      

Good practice to put your commong scripts so that user of your package doesnt have to read your code to figure out how to do what.
This way everything they need to know is inside package.json
To run the script you run
```
npm run SCRIPT_NAME
```

## npm publishing

In order to publish you need to do this first:
* [Sign up](https://www.npmjs.com/signup) to create user account in npmjs
* run `npm adduser` will add authentication token to your npmrc file and then you can publish
 
To publish you need 2 things:
* Set up your project in Git      
  `git init`, `git remote add origin https://github.com/vmitic/some-project`    
  `git add .`, `git commit -m "first commit"`, `git push`
* Set up your package.json file     
  `npm init` and pay attention to all questions

to publish you do
```bash
npm publish
#to check it:
npm info YOUR_PKG_NAME
npm repo YOUR_PKG_NAME
```

NPM is containing your package name and your version, but GIT is holding your code.
After you commited and published files do:
```
git tag 1.0.2
git push --tags
```
where 1.0.2 is your npm version that shows when you do `npm info YOUR_PKG_NAME`
That way you have release that matches NPM.

## npm publish updates

3 steps:
* make changes to your code
  `git add .`, `git commit -m "second commit"`    

* updating your version   
 `npm version patch` - for bug fixes   
 `npm version minor` - for bug fixes   
 `npm version major` - for bug fixes     
 it will update package.json. Also commit it to git! Also created a tag! :)    

* walk through same publish proces
 `git push --tags`    
 `git push`   
 `npm publish`   

## npm publish BETA (and ALPHA) version

use convention version format in package.json:    
 `"version": "1.1.0-beta.0"`    
npm does not support changeing beta versions so we have to do it manually
```
git add.
git commit -m "beta version 0"
git tag 1.1.0-beta.0
git push
git push --tags
npm publish --tag beta 
```
now we can use :
```
npm install PACKAGE@beta
```

your package has following info (check with `npm info YOUR_PKG_NAME`):  
```json
'dist-tags': { latest: '1.0.3', beta: '1.1.0-beta.0' },
versions: ['1.0.1','1.0.2','1.0.3']
```







