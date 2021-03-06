# <%= name %>
[![Published on npm](https://img.shields.io/npm/v/<%= orgNpm %>/<%= name %>.svg?style=flat)](https://www.npmjs.com/package/<%= orgNpm %>/<%= name %>)
[![Build Status](https://travis-ci.org/<%= orgGit %>/<%= name %>.svg?branch=master)](https://travis-ci.org/<%= orgGit %>/<%= name %>)
[![Dependency Status](https://img.shields.io/david/<%= orgGit %>/<%= name %>.svg?style=flat)](https://david-dm.org/<%= orgGit %>/<%= name %>)
[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/author/<%= orgGit %>)
Welcome to the <%= name %> project! Let's work with web components!
## Quick-start

*Notice: You will need to use [Node](https://nodejs.org/en/) v.6 or higher. These web components are written in [ES6](http://es6-features.org/) and build routines compile to es5 to encompass more browsers.*

```bash
$ git clone <%= gitRepo %>
$ cd <%= name %>
$ yarn install # this will take a while due to lerna bootstrap
$ yarn rebuild node-sass  # this may be necessary
$ yarn start
```

## Scripts

- `$ yarn start`
    - Launch a demo server. This should be continuously running as you develop.
- `$ yarn run new`
    -  Create a new component.
- `$ yarn test`
    -  Run tests on ALL <%= name %>.
- `$ yarn run build`
    -  Run build on ALL <%= name %>.
- `$ yarn run bootstrap`
    - Update ALL <%= name %>' dependencies and interlink them with [lerna bootstrap][lerna-bs].
- `$ yarn run storybook`
    - Run storybook
- `$ yarn run build-storybook`
    - Build storybook for deployment

[lerna]: https://github.com/lerna/lerna
[lerna-bs]: https://github.com/lerna/lerna#bootstrap

## Web Component development

Because this is a monorepo, each web component will need to be independently built in order to actively work on and preview the changes. Every web component has its own Gulp file and Yarn/NPM script.

While still running `yarn start` in one terminal window (which runs the local server), you will need to open another terminal window, drill into the directory of the web component you'd like to work on, and execute the `yarn run dev` command. This command will use gulp tasks to watch the files within that web component directory and will automatically re-run the build command and refresh the browser when you make changes to the web component.

### Example development on a web component

```bash
$ cd /Sites/<%= name %>
$ yarn start

# SHIFT + CTRL + T to open a new tab in Terminal

$ cd elements your-card  # or any other web component
$ yarn run dev
```

Make a change to the web component and save. The gulpfile will handle transpiling the element down to ES5 and will bring in the HTML and Sass into the template in the web component.

## Test

To test all <%= name %>, run `yarn test` from the root of the repo. If you only want to test the web component you're working on:

```bash
$ cd elements/your-card
$ yarn test
```

Also, if your tests are failing and you want access to a live browser to investigate why, the following flag will keep the browser open.

```bash
$ yarn test -- -p
```

Then open the URL that will be printed in the terminal. It looks something like this: `http://localhost:8081/components/@<%= orgNpm %>/<%= name %>/generated-index.html?cli_browser_id=0`.

## Storybook

We've added [Storybook](https://storybook.js.org/) to <%= name %> as a way to preview our web components as they are being developed. We'll also use Storybook to export a static site that will be the demo site for <%= name %>.

To run storybook

```bash
$ yarn run storybook
```

This will start a web server on port 9001. Navigate in your browser to `http://localhost:9001` to see Storybook in action. Storybook will watch for file changes and reload the browser automatically for you. This is a little slow at the moment, but we'll look into speeding this up.

To export the storybook static site

```bash
$ yarn run build-storybook
```

This places a build of the storybook site in the .storybook_out directory.

### Known Issues with Storybook

For any web component that has a third-party dependency you will need to update the `/.storybook/webpack.config.js` file. You will need to create an alias for your depedency.

For example:

```js
"../../whatwg-fetch/fetch.js": path.join( // this is the third-party dependency in the <%= name %>
  __dirname,
  "../node_modules/whatwg-fetch/fetch.js" // this is where it lives in node_modules
)
```
