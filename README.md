# load-flit-plugins

[![Greenkeeper badge](https://badges.greenkeeper.io/taoyuan/load-flit-plugins.svg)](https://greenkeeper.io/)

> Load multiple flit plugins using globbing patterns

Usually you would have to load each task one by one, which is unnecessarily cumbersome.

This module will read the `dependencies`/`devDependencies`/`peerDependencies` in your package.json and load flit plugins that match the provided patterns.


#### Before

```js
flit.loadNpmPlugins('flit-plugin-flightplan');
flit.loadNpmPlugins('flit-xxx');
```

#### After

```js
require('load-flit-plugins')(flit);
```


## Install

```bash
$ npm install --save-dev load-flit-plugins
```


## Example config

```js
// flitfile.js
module.exports = function (flit) {
	// load all flit plugins matching the `flit-*` pattern
	require('load-flit-plugins')(flit);

	flit.init({});
	flit.task('default', []);
}
```


## Usage examples

### Load all flit plugins

```js
require('load-flit-plugins')(flit);
```

Equivalent to:

```js
require('load-flit-plugins')(flit, {pattern: 'flit-*'});
```

### Load all flit-contrib plugins

```js
require('load-flit-plugins')(flit, {pattern: 'flit-contrib-*'});
```

### Load all flit-contrib plugins and another non-contrib task

```js
require('load-flit-plugins')(flit, {pattern: ['flit-contrib-*', 'flit-xxx']});
```

### Load all flit-contrib plugins excluding one

You can exclude plugins using the negate `!` globbing pattern:

```js
require('load-flit-plugins')(flit, {pattern: ['flit-contrib-*', '!flit-contrib-xxx']});
```

### Set custom path to package.json

```js
require('load-flit-plugins')(flit, {config: '../package'});
```

### Only load from `devDependencies`

```js
require('load-flit-plugins')(flit, {scope: 'devDependencies'});
```

### Only load from `devDependencies` and `dependencies`

```js
require('load-flit-plugins')(flit, {scope: ['devDependencies', 'dependencies']});
```

### All options in use

```js
require('load-flit-plugins')(flit, {
	pattern: 'flit-contrib-*',
	config: '../package.json',
	scope: 'devDependencies'
});
```


## Options

### pattern

Type: `String`, `Array`  
Default: `'flit-*'` ([globbing pattern](https://github.com/isaacs/minimatch))

### config

Type: `String`, `Object`  
Default: Path to nearest package.json

### scope

Type: `String`, `Array`  
Default: `['dependencies', 'devDependencies', 'peerDependencies']`


## License

[MIT](http://opensource.org/licenses/MIT)
