# Sisu Static Site Starter

Use this repo as a starting point for your next static site build.

## Tech Stack

### Client

- [jQuery](https://jquery.com/) - Get off my lawn!
- [Lodash](https://lodash.com/) - Little utilities like throttle/debounce
- [Postal](https://github.com/postaljs/postal.js) - pub/sub library to allow decoupled communication between components
- [Modernizr](https://modernizr.com) - Browser feature detection (touch-events)

### Development

- [Gulp](http://gulpjs.com/) - Efficient, configurable, streaming task runner
- [Gulp File Include](https://github.com/coderhaoxin/gulp-file-include) - Basic HTML templating/includes.
- [BrowserSync](https://www.browsersync.io/) - Live reload changes
- [Webpack 2.6](https://webpack.github.io) - Automatic common module chunk bundling and tree shaking
- [Babel](https://babeljs.io/) - Use the latest ECMAScript features like all the cool kids
- [Sass](http://sass-lang.com/) - Easier CSS dev with variables, nesting, partials, import, mixins, inheritance, and operators
- [PostCSS](http://postcss.org/) - Autoprefix CSS
- [ESLint](http://eslint.org/) - Catch syntax and style issues

## To Do
- [ ] Progressive web app with offline support?
- [ ] Adjust Gulp to only update changed files
- [ ] Improve Readme documentation
- [ ] Add better example site starting point

## Get Started

1. Install [Node v6.9+](https://nodejs.org/en/) globally if you don't have it already
1. Install [Yarn](https://yarnpkg.com/) globally if you don't have it already
1. Clone or download this repo
1. Using terminal change directories to the project root `cd /path/to/sisu-static-site-starter`
1. Install dependencies by running `yarn`
1. Run any of the available commands found below

## Commands

| Command | Description |
|---------|-------------|
| `yarn` | Install dependencies |
| `yarn dev` | - Transpile CSS and Javascript - View at [http://localhost:3000/](http://localhost:3000/) - BrowserSync will automatically reload CSS or refresh the page when JS, SCSS, or content changes. |
| `yarn build` | Use Gulp to build static output to the `/dist` folder |
| `yarn lint` | Lint code using ESLint |

## Project Structure

- **dist** - Files compiled by the Gulp build pipeline
- **src** - Development files to be transpiled/copied into `dist`
	- **data** - Custom data in JSON files to be used in templates and javascript. Copied to `dist`
	- **docs** - PDFs and other static files that can be linked to. Copied to `dist`
	- **fonts** - Copied to `dist`
	- **images** - Copied to `dist`
	- **markup** - HTML partials to be combined by Gulp. Not copied to `dist`
		- **svgs** - SVGs that will inlined by including them as partials
	- **scripts** - Scripts will be transpiled with Webpack to `dist/js`. See `webpack.config.js` for more details
		- **components** - javascript class files grouped by the areas of the application that they are used
		- **constants** - Constants groups into files by type (ActionTypes.js, NotificationTypes.js, etc..)
		- **services** - Stand-alone JavaScript modules (non-class components)
		- `scripts.js` - File is the entrypoint for webpack and will be built to `/dist/scripts.js`
	- **styles** - Sass files transpiled to `dist/css`
	- `index.html` - Root HTML files will have partials combined and output to root of `dist`
- `dotfiles` - Various configs for the different parts of the stack


## Development Workflow

### Static files

For files and folders that are completely static and don't need to go through the asset pipeline, put them in
the `src` directory and they will be directly copied over to the `dist` directory.

### Javascript

You can use ES6 and use both relative imports or import libraries from npm.

### Modernizr

```javascript
if (Modernizr.touchevents) {
	console.log('touch events');
} else {
	console.log('no touch events');
}
```

### Postal

```javascript
import postal from 'postal';
import { HOME } from '../constants/Channels';

const channel = postal.channel(HOME);

channel.subscribe('some.event', (args) => {
	console.log('some.event called');
	console.log('args', args);
});

channel.publish('some.event', {
	foo: true,
	bar: false
});

```

### CSS

Any SCSS file directly under the `src/styles/` folder will get compiled with [PostCSS Next](http://cssnext.io/)
to `/dist/css/{filename}.css`.


### HTML

To create a new HTML page in the root of the `src` directory.

HTML files can use [Gulp File Include](https://github.com/coderhaoxin/gulp-file-include) to include other partials.

#### To include a partial

```
@@include('./markup/common/_head.html')
```

#### To include a partial with variables

```
@@include('./markup/common/_head.html', {
	"title": "Sisu Static Site",
})
```

Then use inside the partial

```
<title>@@title</title>
```

## Production Workflow

Run `yarn build` then do what you want with the code in `dist`.






