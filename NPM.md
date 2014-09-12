# `npm`

[< README](README.md)

`npm` stands for Node Package Manager. It itself is a Node module which allows
you to download and keep track of versioned packages for your projects. As of
Node version 0.6.3, it has been bundled and installed automatically with Node.

`npm` is essentially a repository of published packages. You can search npm
packages online at [npmjs.org](https://www.npmjs.org/). Not all of them are Node
modules, but a good majority are. At the time of writing this, `npm` is an API
wrapped around a series of 'CouchDB' servers, which keep track of every `npm`
module, it's contents, and each published version.

## How to install packages

```bash
npm install [package name]
```

Replace `[package name]` with the name of the package you wish to install. This
will create a folder in the current working directory called `node_modules` and
place the module within that folder. Any Node file (`.js` and so forth) can then
use `require('[package name]')` to bring it into your project.

You can `npm install` as many packages as you want in a single command. Just
separate out the package names with a space.

```bash
npm install gulp gulp-less gulp-ng-annotate gulp uglify
```

You can also install packages globally using the `-g` flag. Rather than install
a module into your `node_modules` folder, it will install it in your
`/usr/local/bin` directory to use as a CLI.

## How keep track of installed packages

So you can use `npm install` to a package, but what if your `node_modules`
directory gets hosed? You have to go through your project files and and find
which node modules you installed. That's where a `package.json` file comes in
handy.

If you don't already have a package.json in the directory, you can generate one
through `npm`!

```bash
npm init
```

This will ask you a series of questions to fill out a default package.json. If
you're not publishing a node module, none of it really matters, so you can just
skip through all of the prompts until it creates it. You can always go back and
edit it later.

Now that the `package.json` is there, you can add dependencies to it.

```bash
npm install [package_name] --save
```

This command installs the package and saves it to your `package.json`. After you
install a package with the `--save` flag, take a look at your `package.json` to
see what it added.

You can also save development dependencies.

```bash
npm install [package_name] --save-dev
```

This saves the packages to a `'devDependencies'` property in your
`package.json`. The difference between this list of dependencies and the normal
`'dependencies'` is that if you run `npm install`, it will install all of the
dependencies and devDependencies, but if you run `npm install --production`, it
won't install the devDependencies.

Once you have your `package.json` set up with all of your dependencies, you can
delete your `node_modules` directory, and run `npm install` or `npm i` to
reinstall all of your dependencies again.

## Versioning

`npm` and `npm` modules use a standard of versioning called
[Semantic Versioning](http://semver.org/). It uses 3 different numbers to
declare a version (e.g. 1.4.12). Basically, it sets a standard for version
numbers.

* The first number is a MAJOR version number. It's incremented when you make
breaking API changes.
* The second is a MINOR version number. It's incremented with added
functionality that is backwards compatible. No breaking changes.
* The third is a PATCH version number. It's incremented with small backwards
compatible bug fixes.

Another addendum to that is that anything in MAJOR version 0 should be
considered unstable, and breaking changes may happen in MINOR and PATCH
versions.

This standard is not always followed, but it gives you an idea as to the method
behind deciding on version.

`npm` lets you install specific version, and even define valid version ranges
for packages. You can read all about it [here](https://www.npmjs.org/doc/).

## Publishing

You can publish you're own `npm` modules! It's not too difficult. Before you
start, you'll need to create an `npm` account
[here](https://www.npmjs.org/signup). Next, in the terminal, type:

```bash
npm adduser
```

You'll go through some prompts to authenticate your `npm` user.

Before you start work, you'll probably want to decide on a name for the project.
Each `npm` package must be unique, so you have to choose something new. Also,
don't just create an `npm` package just for the sake of creating one. It's good
practice, but we don't want to dirty up the `npm` registry with useless
packages. The other thing is that maybe there's already a module for what you
want to do. Consider using their module, or submitting a pull request to add the
functionality you want to.

Next, you'll create repository on GitHub (Note, that you don't actually need to
set up your code in a repository, but if you want to be seriously considered, it
would be a good idea).

Once you clone it to your machine, you can begin work! Start with that
`npm init` command so that you can create your `package.json` (this is required
for `npm` modules). When it asks you for your 'main' file, that's the file that
will be used when someone `require()`s your module.

A good folder structure could be something like this:

```
my-module
├─ package.json
├─ .npmignore
├─ .gitignore
├─ LICENSE
├─ README.md
├─ index.js
├─ lib/
│  ├─ sub-module.js
│  └─ another-sub-module.js
└─ test/
   └─ your-test.js
```

The `.npmignore` file is a file (like the `.gitignore`) which tells npm which
files not to publish. These would be files like: `node_modules` (because `npm`
will download them for whomever downloads your package) and `.gitignore`
(because we don't want to mess with what other people want to ignore with git
whatnot). For more on this, see [this](https://www.npmjs.org/doc/misc/npm-developers.html).

After you've finished developing, you can run,

```bash
npm publish
```

There's a lot more you need to know as you begin development, and the above link
will help you with that.

[< README](README.md)
