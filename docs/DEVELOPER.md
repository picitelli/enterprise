# Developer Guide

## Installing IDS into your project

Before installing IDS for usage in your project, make sure to install its dependencies:

- [jQuery](https://jquery.com/)
- [D3](https://d3js.org/)

### Download IDS

#### NPM

You can use NPM (or Yarn) to install from the global NPM registry:

```sh
npm install --save ids-enterprise@latest
```

You can also use `ids-enterprise@dev` for a nightly (and potentially unstable) development build.

After installation, the pre-built files are accessible in `./node_modules/ids-enterprise/dist`

#### CDN

We now offer the IDS library via CDN. For example, the paths for the 4.10.0 releases would be:

```html
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/js/sohoxi.js
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/js/sohoxi.min.js
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/css/dark-theme.css
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/css/dark-theme.min.css
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/css/dark-theme.css
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/css/dark-theme.min.css
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/css/light-theme.css
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/css/light-theme.min.css
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/svg/svg.html
https://cdn.hookandloop.infor.com/sohoxi/4.10.0/svg/svg-extended.html
```

Versions available on CDN are: 4.3.2, 4.3.3, 4.3.4, 4.3.5, 4.7.0, 4.8.0, 4.9.0, and 4.10.0.

**Note:** There may be a cost involved to using this with Infor's Amazon S3 account.  Please keep this in mind when using the library this way.

### Adding the library to a project

Include the IDS dependencies and the library itself in your page's `<head>` tag:

```html
<head>
  <link rel="stylesheeet" href="css/light-theme.min.css" />
  <script src="js/jquery.min.js"></script>
  <script src="js/d3.min.js"></script>
  <script src="js/sohoxi.js"></script>
</head>
```

Next, establish some IDS components using the appropriate HTML markup and CSS styles.  For a full list of available components, see our [component documentation](https://design.infor.com/code/ids-enterprise/latest).  Below is an example of what's necessary to create a simple IDS Button component inside of a twelve column layout:

```html
<div class="row">
  <div class="twelve columns">

    <button id="my-button" class="btn-primary">
      <span>This is My Button</span>
    </button>

  </div>
</div>
```

Finally, in a footer section below the markup on your page, add a `<script>` tag with some Javascript code that will invoke the Javascript interactions available for each IDS component.  One way to do this is to call the generic Initializer on the `<body>` tag (or whatever block element in which you want to scope IDS):

```html
<script type="text/javascript">
  $('body').initialize();
</script>
```

It's also possible to manually initialize each individual component:

```js
  $('#my-button').button();
```

If you've got some specific Javascript code you'd like to run after IDS completely initializes, simply add an event listener for IDS's generic `initialized` event on the `<body>` tag:

```html
<script type="text/javascript">
  $('body').on('initialized', function () {
    // extra code runs here
  });
</script>
```

At this point, IDS should be completely setup in your project!

## Running the development server

### Install pre-requisites

#### Node.js

![Node.js Version](https://img.shields.io/badge/node-%3E%3D%2010.9.0-green.svg);

All of our build tools run in [Node.JS](https://nodejs.org/en/). We are currently pinned to version 10 of node, **so be sure to use that version**. We have a script that tests for this during `npm install`. You'll also need all the requirements [node-gyp](https://github.com/nodejs/node-gyp#installation) suggests installing for your operating system.

#### Git

Our project uses [Git](https://git-scm.com/) for version control.  Any pull requests made to IDS Enterprise will need to be done in a new branch cut from our latest `master` branch.  See the [Git Workflow documentation](./GIT-WORKFLOW.md) for more information.

### Getting started

If using windows the default for linebreaks is CRLF. This project uses LF. In order to configure this for windows you can run the following command before cloning.

```sh
git config core.autocrlf false
```

Use the following to clone our repo and install dependencies:

```sh
git clone https://github.com/infor-design/enterprise.git
cd enterprise
npm i
```

#### Basic commands

- `npm start` : builds the IDS library and runs the demo server.  After running this, open a browser to [`localhost:4000`](http://localhost:4000).
- `npm run documentation` : builds a local copy of the documentation for the IDS components based on the source code in this package.  You can also view [the most current stable release's documentation](https://design.infor.com/code/ids-enterprise/latest).
- `npm run test` : runs [eslint](https://eslint.org/), and IDS's functional and e2e test suites.  Before running this command, make sure to [read our testing documentation](./TESTING.md).

See the `scripts` object in [package.json](../package.json) for a full list of commands.

#### Editor Plugins

This project uses `eslint` and `editorconfig`. You may want to add linting plugins to your editor to help comply with our coding standards:

_For Atom:_

- [ESLint](https://github.com/AtomLinter/linter-eslint)
- [EditorConfig](https://github.com/sindresorhus/atom-editorconfig#readme)

_For VSCode:_

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [EditorConfig](https://github.com/editorconfig/editorconfig-vscode)

Additionally, check out our [Coding Standards documentation](./CODING-STANDARDS.md) for the code standards that will be enforced by these plugins.

## Guidelines for creating a new IDS Component

- See if it can be done with only css.
- Add `_*.scss` file to sass/controls folder similar to current examples
- Add new entry for new file in `_controls.scss`
- Add any variables in `_config.scss`
- Add a view like current examples to `views/controls/`
- Add link to view to `index.html` page
- if Javascript is needed, copy the `template.js` in the `js/controls` folder.
- modify the `gruntfie.js` to add the new script.
- add initializer code to `initialize.js` (should be able to bootstrap the page).
- write the code for the component
- write functional/e2e tests. See [Testing.md](./TESTING.md) for guidelines/instructions.
- make sure all tests pass
- add a `readme.md` file with some basic information about the component.
- run eslint on all the new JS code.
- verify html is valid: <https://addons.mozilla.org/en-US/firefox/addon/html-validator/>
- verify no automated accessibility errors <http://squizlabs.github.io/HTML_CodeSniffer/>
- test your page(s) with Apple VoiceOver <https://www.apple.com/voiceover/info/guide/>
- test your page(s) with Jaws (download <http://www.freedomscientific.com/Downloads/ProductDemos>) <http://www.washington.edu/itconnect/learn/accessible/atc/quickstarts/jaws-2/>
- commit (including issue number) and pull request

## QA Documentation

See [the QA Documentation Checklist](./QA.md).

## Contributing

See our [Contribution Guidelines](./CONTRIBUTING.md).
