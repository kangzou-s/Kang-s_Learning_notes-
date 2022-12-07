[Main Reference](https://medium.com/@richdayandnight/simple-tutorial-on-hosting-your-gitbook-documentation-on-github-pages-bonus-with-gitbook-editor-f27f60d5d408)

# Main library

## Node.js

- Node.js is an open source server environment
- Node.js is free
- Node.js runs on various platforms (Windows, Linux, Unix, Mac OS X, etc.)
- Node.js uses JavaScript on the server

### What Can Node.js Do?

- Node.js can generate dynamic page content
- Node.js can create, open, read, write, delete, and close files on the server
- Node.js can collect form data
- Node.js can add, delete, modify data in your database

### Node.js used here

`npm`  (Node package manager)

`npm install -g gitbook-cli`(use npm to install gitbook command line)

`npm init` initialize project (add package.json that will contain our dependencies)

## Gitbook

`gitbook init` 

`gitbook build`

`gitbook serve`

`gitbook help`

The menu is determined by SUMMARY.md

## Deploy

**Deploy our static site to github pages**

`npm install -g gulp-cli ` 

`yarn add gulp gulp-gh-pages gulp-load-plugins --save-dev` install dependencies

```javascript
# gulpfile.js
const gulp = require('gulp');
const gulpLoadPlugins = require('gulp-load-plugins');

const $ = gulpLoadPlugins();

gulp.task('publish', () => {
  console.log('Publish Gitbook (_book) to Github Pages');
  return gulp.src('./_book/**/*')
    .pipe($.ghPages({
      origin: 'origin',
      branch: 'gh-pages'
    }));
});
```

`gulp publish` deploy  static web pages to github pages.
