# `bower`

[< README](README.md)

If you haven't already read the [`npm`](NPM.md) intro, then now's a good time
to do that. `bower` is similar to `npm` in so many ways, so understanding `npm`
will help you're understanding of `bower`.

To install `bower`, run this command:

```bash
npm install -g bower
```

`bower` components are usually (if not always) client-side modules. They include
javascript, css, fonts, images, polyfills, html, basically anything you can
include in the front-end. Where you would use `npm` to download your 'back-end'
modules, you would use `bower` to download and manage your front-end modules.

## Install components

Basically the same as `npm`. Everything gets downloaded into a
`bower_components` directory:

```bash
bower install angular angular-route angular-animate
```

Dependendencies will also be downloaded. Unlike `npm`, dependencies don't
get nested within their dependents. They also don't really get included
automatically like `npm` modules do. When you get into build process, we'll
talk more about how to deal with that.

You can look up packages using `bower search [search term]` or you can look them
up at [`bower.io`](http://bower.io/).

## How to keep track of installed components

`bower` is a lot like `npm` in this manner. It uses a `bower.json` file instead
of a `package.json`. And to generate the `bower.json`, use

```bash
bower init
```

and follow the prompts.

[< README](README.md)
