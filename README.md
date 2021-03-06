# traceur-compiler-loader v1.0.6
Up to date [Traceur](https://github.com/google/traceur-compiler) Compiler 0.0.8x loader for [Webpack](https://webpack.github.io/).

## Before using

You should manually install "imports-loader" in your project

`$ npm install imports-loader`

By default traceur-compiler-loader using 0.0.86 version of traceur, but you can manually install any version from 0.0.8x.

*IMPORTANT*
````
  You should install traceur-compiler before traceur-compiler-loader
  if you want use different version on compiler.
````

Add `TRACEUR_RUNTIME` to `module.noParse` in `webpack.config.js`

```javascript
var
  TRACEUR_RUNTIME = require('traceur-compiler-loader').runtime;

module.exports = {

  //....

  module: {
    noParse: [
      new RegExp(TRACEUR_RUNTIME)
    ]
  }

  //...
};
```

## Usage
```javascript
// Simple option (does not include Traceur runtime)
require("traceur!./script-file");

// Include Traceur runtime automatically
require("traceur?runtime!./script-file");

// Specify Traceur options
require("traceur?experimental&symbols!./script-file");

// All together now
require("traceur?runtime&symbols!./script-file");
```

### Recommended configuration (do not process modules)
```javascript
{
  module: {
    loaders: [
      {
        test: /^(?!.*(bower_components|node_modules))+.+\.js$/,
        loader: 'traceur'
      }
    ],
    noParse: [
      new RegExp(TRACEUR_RUNTIME)
    ]
  }
}

// With parameters
{
  module: {
    loaders: [
      {
        test: /^(?!.*(bower_components|node_modules))+.+\.js$/,
        loader: 'traceur?experimental&runtime'
      }
    ],
    noParse: [
      new RegExp(TRACEUR_RUNTIME)
    ]
  }
}
```

### Defaults
```javascript
{
  // Modules set to CommonJS (consistent with Node.js and Webpack)
  modules: 'commonjs',

  // Source maps are built and fed to Webpack (use Webpack options)
  sourceMaps: true,

  // Traceur runtime by default not auto included
  runtime: false
}
```

### Runtime path
Access to the runtime path is available as a direct reference:
`require('traceur-compiler-loader').runtime`.

To view all Traceur options, visit
[here](https://github.com/google/traceur-compiler/blob/master/src/Options.js).
