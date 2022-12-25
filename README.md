# Gulp - by Jack Iakovenko

> version: Gulp 4.0.2

## Getting Started

To work with this build in a new project, clone all the contents of the repository <br>
`git clone <this repo>`
Then, from the root of the project, run the `npm i` command, which will install all the dependencies in package.json .
After that, you can use any of the proposed build commands (the final files go to the __app__ folder of the root directory): <br>
`gulp` - is a basic command that runs a development build using browser-sync

`gulp build` - team for the production build of the project. All assets are compressed and optimized for hosting.

`gulp chache` - a command to run after `gulp build` if you need to upload new files to your host without caching.

`gulp backend` - command for the backend build of the project. It is devoid of unnecessary things from the dev build, but not compressed, for the convenience of the backender.

`gulp zip` - command compiles your finished code into a zip archive.

## Folders and files structure

```
├── src/                          # Sources
│   ├── assets                    # folder for storing other assets - php, video files, favicon, etc.
│   │   ├── fonts                 # Folder for storing fonts in woff2 format
│   ├── img                       # Images / SVG folder
│   │   ├── svg                   # A special folder for converting svg to sprite
│   ├── js                        # Scripts
│   │   └── main.js               # Main script
│   │   ├── _vars.js              # File with project variables
│   │   ├── _vendor.js            # File with library connections
│   │   ├── _functions.js         # A file with ready-made js functions
│   │   ├── _components.js        # File with component connections
│   │   ├── components            # js components
│   │   ├── vendor                # Folder to load local versions of libraries
│   ├── partials                  # Folder for storing html-parts of the page
│   ├── scss                      # Website Styles (sass preprocessor in scss syntax)
│   │   └── main.scss             # Main style file
│   │   └── vendor.scss           # File for including library styles from vendor folder
│   │   └── _fonts.scss           # Font connection file (you can use a mixin)
│   │   └── _mixins.scss          # File for including mixins from the mixins folder
│   │   └── _vars.scss            # File for writing css or scss variables
│   │   └── _settings.scss        # File for writing global styles
│   │   ├── components            # SCSS components
│   │   ├── mixins                # Folder for saving ready-made scss components
│   │   ├── vendor                # Folder for storing local css-style libraries
│   └── index.html                # Main html file
└── .ecrc                         # Editorconfig-checker package settings file (excludes unnecessary folders)
└── .editorconfig                 # File with code formatting settings
└── .stylelintrc                  # File with stylelint settings
└── gulpfile.js                   # Gulp configuration file
└── package.json                  # Build configuration file with installed packages
└── README.md   
```

## Contents
1. [npm-scripts](#npm-scripts)
2. [Working with html](#Working-with-html)
3. [Working with CSS](#Working-with-CSS)
4. [Working with JavaScript](#Working-with-JavaScript)
5. [Working with fonts](#Working-with-fonts)
6. [Working with images](#Working-with-images)
7. [Working with other resources](#Working-with-other-resources)
8. [Recommended VS Code plugins](#Recommended-VS-Code-plugins)
9. [Local snippets](#Local-snippets)
10. [Ready modules](#Ready-modules)
11. [Conclusion](#Conclusion)

## npm-scripts

You can call gulp scripts via npm.
Also in the assembly it is possible to check the code for compliance with the config (editorconfig) and validate html.

`npm run html` - runs the html validator, you need to run it if there are html files in the __app__ folder.

`npm run code` - runs editorconfig-checker to check if it matches the config file.

## Working with html

Thanks to the __gulp-file-include__ plugin, you can split the html file into different templates, which should be stored in the __partials__ folder. It is convenient to divide the html page into sections.

> To insert html parts into the main file use `@include('partials/filename.html')`

If you want to create a multi-page site - copy __index.html__, rename as you need, and use.

When you use the `gulp build` command, you will get minified html code in one line for all html files.

## Working with CSS

The build uses the __sass__ preprocessor in __scss__ syntax.

Styles written in __components__ must be included in __main.scss__.
__IMPORTANT:__ Be sure to remove the styles that are written in __main.scss__ for `.page__body`.

To include third-party css files (libraries) - put them in the __vendor__ folder and include them in the ___vendor.scss__ file

If you want to create your own mixin, do it in the __mixins__ folder, and then include it in the ___mixins.scss__ file.

If you want to use scss variables, include ___vars.scss__ also in main.scss or wherever you need it, but be sure to remove __:root__.

> To include css files, use the `@import` directive

Two files are created in the resulting __app/css__ folder: <br> __main.css__ - for page styles, <br> __vendor.css__ - for styles of all libraries used in the project.

When you use the `gulp build` command, you will get minified css code in one line for all css files.

## Working with JavaScript

Webpack is used to build the JS code.

JS code is better divided into components - small js files that contain their own implementation isolated from each other. Place these files in the __components__ folder, and then import them into the ___components.js__ file

The __vars.js__ file should store basic project variables, like finding elements, etc.

There is no need to change anything in the __main.js__ file, it is made simply as a result.

You can connect third-party libraries through npm, for this there is a ___vendor.js__ file. Import connections there.

If some library is not in npm or you just need to connect something with a local file, put it in the __vendor__ folder and import it in the same way, but with the path to the file.

When using the `gulp build` command, you will get minified js code in one line for all js files.


## Working with fonts

Because the author does not support IE11, only the __woff2__ format is supported in the assembly (this means that only this format is used in the font connection mixin).

Put the __woff2__ files into the __assets/fonts__ folder and then call the `@font-face` mixin in the ___fonts.scss__ file.

Also, don't forget to write the same fonts in `<link preload>` in html.


## Working with images

Any images other than __favicon__ should be placed in the __img__ folder.

If you need to make an svg sprite, put the svg files you need for the sprite in the __img/svg__ folder. At the same time, such attributes as fill, stroke, style will be automatically deleted. Other svg files just leave in the __img__ folder.

When using the `gulp build` command, you will get minified images in the resulting __img__ folder.

Support for __webp__ and __avif__ formats is available in the build. You can connect them through the `picture` tag. For background, you can use regular __jpg__ or __png__ , or use `image-set` where possible.


## Working with other resources

Any resources (assets) of the project, for which the appropriate folder is not allocated, should be stored in the __assets__ folder. These can be video files, php files (such as a form submission file), favicons, and others.


## Recommended VS Code plugins

I recommend using VS Code, and the assembly implements interaction with this editor. So, when you open a folder with an assembly in VS Code, the editor will offer you previously uninstalled plugins that are suitable for the assembly to work correctly.

The most important one is __projects snippets__, this plugin "turns on" locally written snippets for building.

## Local snippets

For convenience and speed of development, local snippets (located in the .vscode/snippets folder) were added, which work thanks to the plugin described above. All snippets start with the __g-__ prefix. So far, the snippets contain only html (quick creation of navigation, social networks, the correct picture tag with webp and avif, and so on).

Some snippets are closely related to scss mixins, such as the burger button. The __g-burger__ snippet will create a burger HTML markup for you, and including the __@include burger__ mixin will add styles for it, which is extremely convenient.

A full list of snippets with mixin support will be published later.

## Ready modules

Ready-made, frequently used modules for various tasks are gradually added to the assembly. The already added functionality will be listed below.

__Attention!__ The _functions.js_ file describes only the connection of all the necessary modules. It is recommended to use all this in separate files. For example, if you need to create a modal window, create the _modal.js_ file in the components folder, include it in the components.js file, and use the connection code in the _modal.js_ file.


### Burger menu

You can very quickly add a working burger to your page, for this you need:

1. Use `g-burger` snippet in html
2. Add the `data-menu` attribute to your potential menu in html
3. Call the `burger` mixin in scss

```
.burger { @include burger }
```
4. Go to the js/_functions.js file and uncomment the line with the connection of the burger js file
5. Customize menu display styles for yourself using the `menu--active` class

### Modal 

You can very quickly add a working modal window to your page, for this you need:

1. Use the `g-graph-btn` snippet in html. It will create a button for the modal window, your task is only to fill in the `data-graph-path` attribute
2. Next, call the `g-graph-modal` snippet. It will create the basic layout of the window. Your task is to make the window according to the layout, fill in the content and be sure to designate the `data-graph-target` attribute with the same value as the `data-graph-path`
3. Go to the vendor.scss file and uncomment the line with the connection of the graph-modal.min.css file
4. Go to the js/_functions.js file and uncomment the line with the import and connection of the `GraphModal` library

### Scroll control

You can disable\enable scrolling on the page (works even on iPhone). For this you need:

1. Go to the js/_functions.js file and uncomment the line with import functions `disableScroll`, `enableScroll`.
__Important!__. If the page contains blocks with fixed positioning (for example, a header), add the class `fixed-block` to it so that this block does not jump when scrolling is disabled.

It is not necessary to use functions in the __functions__ file, do as you like.

### Tabs

You can very quickly add working tabs to your page, for this you need:

1. In html, call the `g-tabs` snippet. It will create the markup for the tabs, your only task is to fill in the `data-tabs` attribute
2. For the `.tabs` class, call the `tabs` mixin in scss (or use the library script connection from npm in the vendor.scss file)
4. Go to the js/_functions.js file and uncomment the line with the import and connection of the `GraphTabs` library

### Validation and sending data to the mail

You can quickly set up validation and sending data to the mail (while working in test mode). How to use it:

1. Create a form, specifying a unique class for it. Also specify unique classes for input fields.
2. Create an array containing the plugin rules <a href="https://github.com/horprogs/Just-validate" target="_blank">just-validate</a>, for example:
```
const rules1 = [
  {
    ruleSelector: '.input-name',
    rules: [
      {
        rule: 'minLength',
        value: 3
      },
      {
        rule: 'required',
        value: true,
        errorMessage: 'Заполните имя!'
      }
    ]
  },
  {
    ruleSelector: '.input-tel',
    tel: true,
    telError: 'Введите корректный телефон',
    rules: [
      {
        rule: 'required',
        value: true,
        errorMessage: 'Заполните телефон!'
      }
    ]
  },
];
```
__IMPORTANT__. If your form has a field with a phone number, be sure to add new fields to the rules array: `tel: true, telError: 'Error entering phone number'`.
3. Connect the `validateForms` function, it is located in _functions.js_, passing three parameters there:
3.1. String with form class
3.2. Array of rules
3.3. If necessary, you can create your own function that will be executed after submission, then it will also need to be passed as an argument to the `validateForms` function.

Code example:
```
import { validateForms } from './functions/validate-forms';
const rules1 = [
  {
    ruleSelector: '.input-name',
    rules: [
      {
        rule: 'minLength',
        value: 3
      },
      {
        rule: 'required',
        value: true,
        errorMessage: 'Заполните имя!'
      }
    ]
  },
  {
    ruleSelector: '.input-tel',
    tel: true,
    telError: 'Введите корректный телефон',
    rules: [
      {
        rule: 'required',
        value: true,
        errorMessage: 'Заполните телефон!'
      }
    ]
  },
];

const afterForm = () => {
  console.log('Произошла отправка, тут можно писать любые действия');
};

validateForms('.form-1', rules1, afterForm);
```

### Throttle function

To smooth the handling of commonly used events, you can use the ready-made __throttle__ function. For this you need:

1. In the right place, import the __throttle()__ function
2. Write the function you need, for example, __func()__
3. Create a variable in which to place your function call inside throttle, for example: `let f = throttle(func)`
4. Use this variable as a function in the call, for example: `window.addEventListener('resize', f)`

### Fix fullscreen blocks

It is not uncommon for blocks with a height of 100vh to cause problems in mobile browsers. The ready-made fix-fullheight module will help solve this:

1. Uncomment the line importing the __fix-fullheight.js__ file
2. Assign height to the block you need not 100vh, but `var(--vh)`

This function uses the previously mentioned throttle. You can remove it, or change the time inside the __fix-fullheight.js__ file.

### Getting the header height

Sometimes it is required to get the exact height of the header if it is made absolute or fixed positioned, and there is a `getHeaderHeght` function for this. How to use it:

1. Uncomment the line importing the __header-height.js__ file
2. Use the css variable `--header-height` where you want

It is not necessary to use functions in the __functions__ file, do as you like.

### Custom scroll

To implement a custom scroll, the __simplebar.js__ plugin is installed in the assembly. How to use it:

1. Uncomment the line with plugin import __simplebar__
2. Add the maximum height to the desired block and the `data-simplebar` attribute

### Viewport definition functions

You can run scripts at a certain width (resize support is not yet implemented) using the ready-made functions `isMobile()`, `isTablet()`, `isDesktop()`. To do this, you just need to include the one you need from the file, and then use the `if` conditions inside.

### Tooltips

You can quickly create a working, accessible tooltip, which will also calculate the indentation itself using js. How to use it:

1. Use the `g-tooltip` snippet in html. It will create a button for the modal, your job is to fill in the `aria-describedby` and `id` attributes.
2. Next, you need to connect tooltips (code in the _functions.js_ file), and instead of el, pass the id or class of the tooltip button, and instead of tooltip, pass the id or class of the tooltip itself.
3. After that, you can style the tooltip however you like.

### Slider

You can quickly create a working swiper slider. How to use it:

1. Use the `g-swiper` snippet in html. It will create the basic structure of the swiper slider, you need to add your class for the swiper container.
2. Uncomment the line with styles connection in the _vendor.scss_ file
3. Connect the swiper itself (code in the _functions.js_ file) and use it following the documentation.

### Scroll animations

You can quickly sketch out scroll animations using the plugin. How to use it:

1. Include the AOS.js library code (code in the _functions.js_ file) and initialize it.
2. Using the attributes from the plugin documentation, call certain animations, or write your own.

### Parallax Effect on scroll

You can quickly sketch parallax elements on scroll using the plugin. How to use it:

1. Include the rellax.js library code (code in the _functions.js_ file) and initialize it by passing the class of the element(s).
2. Set this class to the required elements, and use the attributes from the documentation to customize animations.

### Smooth scrolling to anchors

You can make smooth scrolling to anchors, which even works in Safari, with a plugin. How to use it:

1. Include the smooth-scroll.js library code (code in the _functions.js_ file) and initialize it by passing the selector of all anchor links.
2. Give all anchor links the `data-scroll` attribute.

### Swipe on mobile devices

You can implement various interactions with the page through swipes on mobile devices using the plugin. How to use it:

1. Include the swiped-events.js library code (code in the _functions.js_ file).
2. Use various events from the plugin library.

### Mixin for Flex-layout (test version)

In the latest version of the build, I added a flex-layout mixin (can be found in the mixins folder), which implements a typical grid for cards. You can choose the settings you need to make the grid fast and hassle-free. For example:

```

<div class="cards">
  <div class="cards__item">Текст</div>
  <div class="cards__item">Текст</div>
  <div class="cards__item">Текст</div>
  <div class="cards__item">Текст</div>
  <div class="cards__item">Текст</div>
  <div class="cards__item">Текст</div>
</div>

$options: (
  parentClass: "cards",
  itemsClass: "cards__item",
  desktopGap: 30px,
  desktopElems: 3,
  tablet: "1024px",
  tabletElems: 2,
  tabletGap:  30px,
  mobile: "600px",
  mobileElems: 1,
  mobileGap: 20px
);

@include flex-layout($options);

```
In the options, you can select the parent class (or the flex container, the class for descendants, what indentation they will have, at what resolutions the number of elements will change).
So far, the mixin is in a test form, I will see how it shows itself. Offer your options on how to improve it, make it more flexible, etc.

## Conclusion

Thank you to everyone who uses the build! If you notice any error, please send an issue with a detailed description of the problem, I'll look at everything and try to solve it. Thank you!