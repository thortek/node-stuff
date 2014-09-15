# `grunt`

[< README](README.md)

`grunt` is a build process management tool. It leverages the power of community
created tools to process files. For front-end development, it's used to help
concatenate and minify files, process css preprocessors (such as less or sass),
check for syntax errors, auto-reload your web page, and all sorts of other tasks
that you might classify as 'grunt work'.

## Installation

First, you'll need to install the `grunt` CLI.

```bash
npm install grunt-cli -g
```

Next, you'll need to install `grunt` locally.

```bash
npm install grunt --save-dev
```

(Note that the `--save-dev` will only work if you have a `package.json`)

## Setup

Grunt is a configuration-based build system. You put the configuration into a
file called `Gruntfile.js` in the root of your project. Later versions also work
with all-lowercase `gruntfile.js`.

Start out with this template for your `Gruntfile.js`:

```javascript
'use strict';

module.exports = function (grunt) {

  // Project configuration.
  grunt.initConfig({

  });

};
```

Next, let's create a task to concatenate all of the javascript files in our
`src/scripts/` directory. First, we'll need to download a module that
minifies files ([`grunt-contrib-uglify`](https://github.com/gruntjs/grunt-contrib-uglify))
Note that all grunt plugins begin with the `grunt-` prefix. The `contrib-` is in
there because it was created by the grunt core team.

So first we install it: `npm install --save-dev grunt-contrib-uglify`

Then we need to load it in our `Gruntfile.js`:

```javascript
module.exports = function (grunt) {

  // Project configuration.
  grunt.initConfig({

  });

  // This is what we add
  grunt.loadNpmTasks('grunt-contrib-uglify');

};
```

Now we can set up our UglifyJS configuration. In the `grunt.initConfig()`
object, add this property and configuration. We'll walk through it in just a
minute.

```javascript
grunt.initConfig({
  uglify: { // This specifies which plugin we're configuring
    scripts: { // This is the target. We can specify multiple targets for a single plugin
      options: { // This is the target specific options. We can also place an options hash at the plugin level to specify configuration for all targets
        sourceMap: true // This option says that we want a source map printed out
      },
      files: { // This is the configuration for the task that specifies destination and source.
        'public/js/app.min.js': ['src/scripts/**/*.js']
      }
    }
  }
});
```

Now when you run `grunt uglify` in your terminal when you're in your project
directory, it will concatenate all of the `.js` files in your `src/scripts`
folder! Keep in mind that it won't keep them in any sort of order, so if you
want to do that, you'll have to put the paths to the files in the order you want
them in in the `uglify.scripts.files['public/js/app.min.js']` array.

Note that you can also run `grunt uglify:scripts` to achieve the same result.

## Customization

You can also make alias names to run a task to series of tasks at once.

At the end of your grunt configuration function in your `Gruntfile.js`, put this
line in:

```javascript
grunt.registerTask('default', ['uglify']);
```

So you're entire file should look like:

```javascript
'use strict';

module.exports = function (grunt) {

  // Project configuration.
  grunt.initConfig({
    uglify: {
      scripts: {
        options: {
          sourceMap: true
        },
        files: {
          'public/js/app.min.js': ['src/scripts/**/*.js']
        }
      }
    }
  });

  grunt.loadNpmTasks('grunt-contrib-uglify');

  grunt.registerTask('default', ['uglify']);

};
```

When you register a task, it is an alias for `grunt [taskname]`. If you use
`'default'`, then you're defining the default `grunt` task that runs when you
run `grunt` in the terminal without any taskname.

For more on `grunt` see their official [site](http://gruntjs.com/).

[< README](README.md)
