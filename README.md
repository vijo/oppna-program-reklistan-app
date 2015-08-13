# oppna-program-rekapp

Work in progress!

### Installation (for development)

```
# Install Dev dependencies (gulp etc)
npm install

# Cd to the actual app dir
cd rekapp

# Install App Dependencies
npm install

# Add iOS and Android Platforms
tns platform add ios
tns platform add android
```

When developing, run:

```
# To start the emulator the first time
gulp startIOS

# To watch for file changes. When a file is changed
# the source is recomipled (from ES2015 to ES5) and 
# changes pushed to the emulator.
gulp livesyncIOS
```

or run:

```
gulp watchFullIOS
```

Currently, NativeScript does unfortunately not display `console.log` or exception statements in the terminal when running with livesync. Therefor we still have to do full rebuilds with the `watchFullIOS` command to get terminal outputs.


### File structure
```
| - gulpfile.js - Development gulp file (for recompiling, etc)
| - node_modules - Development modules
| - package.json - Development package.json
| - rekapp - The actual app.
  | - app - The actual app
  | - node_modules - App modules
  | - package.json - App package json
| - resources - Resources which are not bundled with the app
| - src - Source of the app. Files gets moved from here to 'rekapp'

```

* Javascript source files (ES2015) gets compiled and moved from `src` to `rekapp`. XML and CSS files gets copied without alternation.
* Javascript files in `src/thirdparty` gets moved from `src` to `rekapp` _without_ compilation.
* To install app dependencies, run `npm install [package] --save` from the `rekapp` folder. The NativeScript build process will copy them  to the correct places in the app. They may be required in the normal way (`let theModules = require('theModule')`)



### Release for production
In `app.js`, remember to set all appSettings to production mode. 

### Note on Babel usage
We're currently not including the Babel polyfill in the App runtime, which means that you cannot use these:

|Feature | Requirements |
|--------|--------------|
|Abstract References | Symbol |
|Array destructuring | Symbol |
|Async functions, Generators | regenerator runtime |
|Comprehensions | Array.from |
|For Of | Symbol, prototype[Symbol.iterator] |
|Spread | Array.from |


