
### Disclaimer  
**THIS SYSTEM WRITES TO YOUR FILESYSTEM!   
IT IS A CODING EXPERIMENT AND HAS NOT BEEN TESTED EXTENSIVELY!**  
This project not intended for beginners
### imagesTreeCopyNResize project
- This setup is a git-bash/bash commmand line utility, not a web app.   
It recursively copies a folder containing jpeg files into another, and modifies the EXIF information (like Title, gps info).
- Run it using git-bash script ```./imagesTreeCopyNResize.sh```  
  This script runs javascript, supplying command line options to the javascript which you edit.  
- **After you download or clone**, run npm i. Creates a node_modules folder and fills it with downloaded node.js packages specified by package.json.  
  - **package.json** was setup to specify all packages needed by this system.
### How typescript gets run  
- The 'tsc' (typescript compiler) converts the typescript *.ts files into javascript *.js files which then gets run by ```node```. 
- Compiled javascript files go into ```code/typescriptCompiled```.  These are the files which get run.    
- Script ```./imagesTreeCopyNResize.sh``` does this:  
  - runs the typescript compiler and produces .js file. Compilation errors show up now.  
  - It runs javascript to do the actual work, supplying command line options to the app.
### Where to modify source code  
- File ```code/imagesTreeCopyNResize.ts``` does the work; edit this to modify. The other source files are more static.  
### package.json package dependency entry notes    
  - A ^ carat in front of an entry in package.json allows auto-upgrading of the package when a new (minor) version is released, and **this caused me lots of trouble**.  
    A package was re-published with an update, my app broke and could not figure out why!   
    Even restoring it from backups was broken because of this!  
      - That is why I removed the carat ^ from some entries in **package.json**  
      - Use of some EXIF packages is shaky in this app, so that's another reason to lock the version.  
### Notes about ```npm i packageName -D```
  - The -D means it's a dev-dependency, so it won't go into a bundle for export. It goes to **devDependencies** section. 
  - Use of '@' in packageName ie ```npm i sharp@0.28.0 -D``` installs specific version, not the latest. You need to manually remove the "^" it inserts into package.json to prevent possible upgrade.  

If this folder is inside of another project, it can use the parent's node_modules.  
### Warning about React and nodejs (not applicable to this project but copied here anyway) 
- When running a node/React app directly or from webpack **there must be only one node_modules in the run folder hierarchy**. If more than one node_modules is present ie: run folder and 2 levels up and React exists in both, React fails with ambiguous error message, typically something about ***useEffect not allowed***. 
- Wrong bracket placment in imports produces ambiguous error messages:   
  ```
  /* WARNING: OMITTING BRACKETS GIVES THIS MISLEADING ERROR:
    "Warning: React.createElement: type is invalid -- expected a string (for built-in components) or a class/function..." */
  import { Mypackage } from './Mypackage.tsx'
  ```
- Proper bracket placement for React import.   
  ***Wrong placement also leads to ambiguous error message!***  
  Following works ok:  
```import React, { ReactDOM, useEffect, useState } from 'react';```
  
