# `gulp`

[< README](README.md)

Gulp is a build tool used to do basically same thing that Grunt does, but with
a few major differences in their philosophies.

Grunt is configuration based. To make changes, you change the configuration or
add in new plugins with their configuration. There are a lot of grunt plugins
that do a lot of things, but you're limited to what those plugins are configured
to do.

Gulp is code based. You write code to build out your tasks. Plugins act as
middleware in a pipeline that modify your files to complete tasks.

Grunt uses the file system to process files. This means that if you have a
series of tasks that need to run on a set of files, each task needs to read,
modify, and save the file before the next task can run.

Gulp uses file streams. This means that for any given set of files, it reads
them, passes the file streams through each of the plugins, then saves the files
once. This makes for a very fast build process, but causes issues when it comes
to things like source maps and includes.

To install `gulp`, run this command:

```bash
npm install -g gulp
```

You'll also need to install `gulp` locally.

```bash
npm install --save-dev gulp
```

## Setup

Gulp is a code-based build system. You put the code into a file called
`gulpfile.js` in the root of your project.

Start out with this template for your `gulpfile.js`.

```javascript
'use strict';

var gulp = require('gulp');

gulp.task('default', []);
```

Next, let's create a task to concatenate and minify all of our javascript files.
First we'll need a couple of plugins to accomplish this task. `gulp-concat` and
`gulp-uglify`.

```bash
npm install --save-dev gulp-concat gulp-uglify
```

Then we modify our `gulpfile.js` to look like this:

```javascript
var gulp   = require('gulp');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');

gulp.task('default', []);

gulp.task('scripts', function () {
  return gulp.src('src/scripts/**/*.js') // Get all of the files in the src/scripts/ directory
    .pipe(concat('app.min.js')) // concatenate them and name the new file app.min.js
    .pipe(uglify()) // minify the files
    .pipe(gulp.dest('public/js')); // save the files to the public/js/ directory
});
```

Now when we run `gulp scripts`, and it minifies our scripts. Now if we want it
to watch our files for changes and run the scripts, we add this task to our
`gulpfile.js`:

```javascript
gulp.task('scripts.watch', ['scripts'], function () {
  gulp.watch('src/scripts/**/*.js', ['scripts']);
});
```

The array passed into the `.task()` function is an array of tasks to run before
the real task is run. So in this task, the `scripts` task runs, then it begins
to watch the files for changes. Then when it sees a change in
`'src/scripts/**/*.js'`, it runs the `scripts` task.

Now you can run `gulp scripts.watch` and it will watch your files for changes.

Grunt and gulp both have their utilities and both are evolving. For more on
gulp, visit see their [documentation](https://github.com/gulpjs/gulp/blob/master/docs/README.md).

[< README](README.md)
