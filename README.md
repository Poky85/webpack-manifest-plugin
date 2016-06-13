# Webpack Manifest Plugin

Webpack plugin for generating an asset manifest.

[![Circle CI](https://circleci.com/gh/danethurber/webpack-manifest-plugin.svg?style=shield)](https://circleci.com/gh/danethurber/webpack-manifest-plugin)


## Usage

In your `webpack.config.js`

```javascript
var ManifestPlugin = require('webpack-manifest-plugin');

module.exports = {
    // ...
    plugins: [
      new ManifestPlugin()
    ]
};
```

This will generate a `manifest.json` file in your root output directory with a mapping of all source file names to their corresponding output file, for example:

```json
{
  "mods/alpha.js": "mods/alpha.1234567890.js",
  "mods/omega.js": "mods/omega.0987654321.js"
}
```


## Configuration

A manifest is configurable using constructor options:

```javascript
new ManifestPlugin({
  fileName: 'my-manifest.json',
  format: 'json',
  basePath: '/app/'
})
```

**Options:**

* `fileName`: The manifest filename in your output directory (`manifest.json` by default).
* `format`: The manifest file type (`json` or `yml`, `json` is default).
* `basePath`: A path prefix for all file references. Useful for including your output path in the manifest.
* `stripSrc`: removes unwanted strings from source filenames
* `cache`: In [multi-compiler mode](https://github.com/webpack/webpack/tree/master/examples/multi-compiler) webpack will overwrite the manifest on each compilation. Passing a shared `{}` as the `cache` option into each compilation's ManifestPlugin will combine the manifest between compilations.
* `process`: Function to transform output JSON before it is stringified to JSON or YML string
* `postProcess`: Function to transform JSON or YML string before it is emitted to file
