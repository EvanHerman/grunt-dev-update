# [grunt](http://gruntjs.com/)-dev-update
> Automate the updating of your package.json packages with a grunt task

[![NPM Version](http://img.shields.io/npm/v/grunt-dev-update.svg)](https://npmjs.org/package/grunt-dev-update)
[![Gittip](http://img.shields.io/gittip/pgilad.svg)](https://www.gittip.com/pgilad/)
[![Dependencies](http://img.shields.io/gemnasium/pgilad/grunt-dev-update.svg)](https://gemnasium.com/pgilad/grunt-dev-update)
[![Built with Grunt](https://cdn.gruntjs.com/builtwith.png)](http://gruntjs.com/)


## Getting Started
This plugin requires Grunt.

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-dev-update --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-dev-update');
```

The best way to load tasks is probably using [load-grunt-tasks](https://github.com/sindresorhus/load-grunt-tasks)

```bash
npm install matchdep --save-dev
```

And then add to your grunt file:
```js
require('load-grunt-tasks')(grunt);
```

***

## The "devUpdate" task

#### This plugin allows you to both update your dependencies and devDependencies with an automated task.

1. You control if you want to just be notified of outdated packages, be prompted for updates or always update.
2. Also you can control whether to stay inside your `package.json` semver matching, or alwasy update to latest

*Q: Why not use `npm update` or `npm install`?*

**A: First, npm update doesn't work on dev dependencies. Second, npm update stays inside your semver matching in your package.json,
thirdly - npm isn't automated like your grunt tasks.**

### Overview
In your project's Gruntfile, add a task config named `devUpdate` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
    devUpdate: {
        your_target: {
            options: {
            // Target specific options go here
            }
        }
    }
})
```

### Options

#### options.reportUpdated
Type: `Boolean`
Default value: `false`

Whether to report an already updated package

#### options.updateType
Type: `String`
Default value: `report`

How devUpdate should handle the outdated packages. Valid options:

* `report` - Just report that the package is outdated.
* `prompt` - Prompt user to confirm update of every package
* `force` - Automatically force the update for the outdated packages.

#### options.packages
Type: `Object`
Default value: `{devDependencies: true}`

What kind of packages should be checked. Valid options:

* `dependencies` - Specify true to check **production dependencies**.

    > Outdated **dependencies** are installed using the `--save` option.

* `devDependencies` - Specify true to check **development dependencies**. This is **true** by default.

    > Outdated **devDependencies** are installed using the `--save-dev` option.

#### options.semver
Type: `Boolean`
Default value: `true`

If true or undefined, packages will be updated with `npm update` and will be installed up to your allowed version in
your `package.json`. Your allowed version is determined using [semver](http://semver.org).

If false your packages will be updated to the latest version there is, regardless of your `package.json` specifications.

**Warning** - this could break packages and only use this option if you're sure of what you're doing.

#### options.packageJson
Type: `null|Object|String`
Default value: `null`

This option allow you to manully configure the path of your **package.json**. Valid options:

* `null` - This will use `matchdep` own logic for finding your package.json (using `findup` to find
nearest package.json). This is the recommended and default option.
* `String` - specify a relative path from your **process.cwd()** to find your package.json.
* `Object` - pass in an object representing your package.json

For better understanding the `String` and `Object` option, please see [matchdep config](https://github.com/tkellen/node-matchdep#config).

### Usage Examples

#### Default Options
Example usage with all options specified with defaults:

```js
grunt.initConfig({
    devUpdate: {
        main: {
            options: {
                //just report
                updateType: 'report',
                //don't report ok packages by default
                reportUpdated: false,
                //what packages to check
                packages: {
                    //only devDependencies by default
                    devDependencies: true,
                    dependencies: false
                },
                //by deafult - use matchdep default findup to locate package.json
                packageJson: null
            }
        }
    }
})
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## License
Copyright (c) 2014 Gilad Peleg. Licensed under the MIT license.
