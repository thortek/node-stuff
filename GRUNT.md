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

[< README](README.md)
