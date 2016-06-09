# generate-eslint [![NPM version](https://img.shields.io/npm/v/generate-eslint.svg?style=flat)](https://www.npmjs.com/package/generate-eslint) [![NPM downloads](https://img.shields.io/npm/dm/generate-eslint.svg?style=flat)](https://npmjs.org/package/generate-eslint) [![Build Status](https://img.shields.io/travis/generate/generate-eslint.svg?style=flat)](https://travis-ci.org/generate/generate-eslint)

Generate a `.eslintrc.json` or `.eslintignore` file as part of a larger build workflow. This generator can be used as a sub-generator or plugin inside other generators.

## What is generate?

Generate is a new, open source developer framework for rapidly initializing and scaffolding out new code projects, offering an intuitive CLI, and a powerful and expressive API that makes it easy and enjoyable to use.

Visit the [getting started guide](https://github.com/generate/getting-started-guide) or the [generate](https://github.com/generate/generate) project and documentation to learn more.

## Quickstart

Use as a plugin, to extend your own generator with this generator:

```js
module.exports = function(app) {
  app.use(require('generate-eslint'));
};
```

Register as a sub-generator, to add this generator to a namespace in your generator:

```js
module.exports = function(app) {
  // you can use any arbitrary name to register the generator
  app.register('eslint', require('generate-eslint'));
};
```

See the [API docs](#api) for more detailed examples and descriptions.

***

### CLI

**Installing the CLI**

To run the `eslint` generator from the command line, you'll need to install [generate](https://github.com/generate/generate) globally first. You can do that now with the following command:

```sh
$ npm i -g generate
```

This adds the `gen` command to your system path, allowing it to be run from any directory.

**Help**

Get general help and a menu of available commands:

```sh
$ gen help
```

**Running the `eslint` generator**

Once both [generate](https://github.com/generate/generate) and `generate-eslint` are installed globally, you can run the generator with the following command:

```sh
$ gen eslint
```

If completed successfully, you should see both `starting` and `finished` events in the terminal, like the following:

```sh
[00:44:21] starting ...
...
[00:44:22] finished ✔
```

If you do not see one or both of those events, please [let us know about it](../../issues).

### Tasks

#### [eslint](generator.js#L21)

Generate a `.eslintrc.json` file to the current working directory or specified `--dest` directory.

**Example**

```sh
$ gen eslint
```

#### [eslint:ignore](generator.js#L42)

Generate a `.eslintignore` file to the current working directory or specified `--dest` directory. This task is also aliased as `eslintignore`, in case you want to use this generator as a sub-generator or plugin and want to use the `ignore` task name for something else.

**Example**

```sh
$ gen eslint:ignore
```

#### [eslint:default](generator.js#L61)

Alias for the [eslint](http://eslint.org) task.

**Example**

```sh
$ gen eslint:default
```

***

### API

**Use as a plugin in your generator**

Use as a plugin if you want to extend your own generator with the features, settings and tasks of generate-eslint, as if they were created on your generator.

In your `generator.js`:

```js
module.exports = function(app) {
  app.use(require('generate-eslint'));

  // specify any tasks from generate-eslint. Example:
  app.task('default', ['eslint']);
};
```

**Use as a sub-generator**

Use as a sub-generator if you want expose the features, settings and tasks from generate-eslint on a _namespace_ in your generator.

In your `generator.js`:

```js
module.exports = function(app) {
  // register the generate-eslint generator (as a sub-generator with an arbitrary name)
  app.register('foo', require('generate-eslint'));

  app.task('minify', function(cb) {
    // minify some stuff
    cb();
  });

  // run the "default" task on generate-eslint (aliased as `foo`), 
  // then run the `minify` task defined in our generator
  app.task('default', function(cb) {
    app.generate(['foo:default', 'minify'], cb);
  });
};
```

Tasks from `generate-eslint` will be available on the `foo` namespace from the API and the command line. Continuing with the previous code example, to run the `default` task on `generate-eslint`, you would run `gen foo:default` (or just `gen foo` if `foo` does not conflict with an existing task on your generator).

To learn more about namespaces and sub-generators, and how they work, [visit the getting started guide](https://github.com/generate/getting-started-guide).

## Related projects

You might also be interested in these projects:

* [generate](https://www.npmjs.com/package/generate): Fast, composable, highly pluggable project generator with a user-friendly and expressive API. | [homepage](https://github.com/generate/generate "Fast, composable, highly pluggable project generator with a user-friendly and expressive API.")
* [generate-file](https://www.npmjs.com/package/generate-file): Generator for generating a single file from a template. | [homepage](https://github.com/generate/generate-file "Generator for generating a single file from a template.")
* [generate-mocha](https://www.npmjs.com/package/generate-mocha): Generate mocha test files. | [homepage](https://github.com/generate/generate-mocha "Generate mocha test files.")
* [generate-node](https://www.npmjs.com/package/generate-node): Generate a node.js project, with everything you need to begin writing code and easily publish… [more](https://github.com/generate/generate-node) | [homepage](https://github.com/generate/generate-node "Generate a node.js project, with everything you need to begin writing code and easily publish the project to npm.")

## Contributing

This document was generated by [verb-readme-generator](https://github.com/verbose/verb-readme-generator) (a [verb](https://github.com/verbose/verb) generator), please don't edit directly. Any changes to the readme must be made in [.verb.md](.verb.md). See [Building Docs](#building-docs).

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](../../issues/new). Or visit the [verb-readme-generator](https://github.com/verbose/verb-readme-generator) project to submit bug reports or pull requests for the readme layout template.

## Building docs

Generate readme and API documentation with [verb](https://github.com/verbose/verb):

```sh
$ npm install -g verb verb-readme-generator && verb
```

## Running tests

Install dev dependencies:

```sh
$ npm install -d && npm test
```

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT license](https://github.com/generate/generate-eslint/blob/master/LICENSE).

***

_This file was generated by [verb](https://github.com/verbose/verb), v0.9.0, on June 09, 2016._