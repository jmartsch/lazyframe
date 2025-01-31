# LazyframeAdvanced

[comment]: <> ([![npm version]&#40;https://badge.fury.io/js/lazyframeAdvanced.svg&#41;]&#40;https://badge.fury.io/js/lazyframeAdvanced&#41;)

Dependency-free library for lazyloading iframes like YouTube, Vimeo, Twitter, Google Maps, Codepen etc.

Watch some examples here: [https://jmartsch.github.io/lazyframeAdvanced](https://jmartsch.github.io/lazyframeAdvanced)

## Why do you need it?

JavaScripts loaded from external providers like YouTube are big and slow down the loading time of your website, even if your visitors don't want to see your beautiful videos.
This also negatively impacts your ranking on Google

For example here are the number of requests and filesizes of some well-known services.

* **YouTube** – 11 requests ≈ 580kb
* **Google maps** – 52 requests ≈ 580kb
* **Vimeo** – 8 requests ≈ 145kb

LazyframeAdvanced creates a responsive placeholder for embedded content and requests it when the user interacts with it or it lazyloads if it is in view. This decreases the page load and idle time.

LazyframeAdvanced comes with brand-like themes for YouTube and other services.

### Why is it advanced?

The original [Lazyframe library](https://github.com/vb/lazyframe) from [Viktor Bergehall](https://github.com/vb) is good as it is.
But there were some features missing, that we needed, so we created our own deviation.

#### What we enhanced

* use IntersectionObserver instead of the old and slow scroll event listener
* lazyload is the default behaviour
* move to a modern and fast build stack with vite
* added codepen as a vendor
* removed vine, as it does not exist anymore
* add aspect ratios for the placeholders


###  New features that we are planning to add:
* make it compatible with a cookie consent tool and only load the frame if consent for a specific vendor cookie is given, else display a placeholder element that you can modify by yourself
* add thumbnail placeholder with image element instead of background element
* overlay thumbnail with play button
* add style for Google Maps placeholder
* automatically add data-vendor based on URL

## Installation Instructions
1. [Install](#install)
2. [Import](#import)
3. [Initialize](#Initialize)
4. [Options](#options)
5. [Changelog](#changelog)
5. [Compile from Source](#compile-from-source)

### Install

NPM

```bash
npm install lazyframe-advanced
```

### Import

JavaScript ES6 import

```js
import lazyframe from 'lazyframe-advanced';
import 'lazyframe-advanced/lazyframe.css'
```

[comment]: <> (Include the library directly. Currently does not work because there is no minified standalone version. )

[comment]: <> (```html)

[comment]: <> (<script src="dist/lazyframe.min.js"></script>)

[comment]: <> (```)

[comment]: <> (Sass import)

[comment]: <> (```sass)

[comment]: <> (@import 'src/scss/lazyframe';)

[comment]: <> (```)

[comment]: <> (Include CSS in HTML)

[comment]: <> (```html)

[comment]: <> (<link rel="stylesheet" href="dist/lazyframe.css">)

[comment]: <> (```)

### Initialize

```js
// Passing a selector
lazyframe('.lazyframe');

// Passing a nodelist
let elements = document.querySelectorAll('.lazyframe');
lazyframe(elements);

// Passing a jQuery object
let elements = $('.lazyframe');
lazyframe(elements);
```

## Options

You can pass general options to lazyframe on initialization. Element-specific options (most options) are set on data attributes on the element itself.

General options and corresponding defaults

```js
lazyframe(elements, {
   // Callbacks
   onLoad: (lazyframe) => console.log(lazyframe),
   onAppend: (iframe) => console.log(iframe),
   onThumbnailLoad: (img) => console.log(img)
})
```
## possible options

| option name | default value | description |
|---|---|---|
| onLoad | function: empty | Callback function for when a element is initialized. 
| onAppend | function: empty | Callback function for when the iframe is appended to DOM. 
| onThumbnailLoad | function: empty | Callback function with the thumbnail URL. 


## Element-specific attributes

Use these attributes on your HTML element like this:

```html
<div
    class="lazyframe"
    data-vendor=""
    data-title=""
    data-thumbnail=""
    data-src=""
    data-ratio="1:1"
    data-initinview="false">
</div>
```

| attribute name | possible values | description |
|---|---|---|
| data-vendor | youtube, vimeo, codepen | Attribute for theming lazyframeAdvanced. Currently supported values are `youtube`, `youtube_nocookie` and `vimeo`
| data-title | string: anything you like | Attribute for custom title. Leave empty to get value from API 
| data-thumbnail | string: url | URL of the thumbnail image you would like to show, before the video is loaded 
| data-src | string: url | The source of what you want to lazyload
| data-ratio | string: url | The ratio of the lazyframe. Possible values: 16:9, 4:3, 1:1
| data-initinview | boolean: true | Set this to true if you want the resource to execute (for example video to play) when the element is in view.

## Changelog
* v2.0.0 much new stuff and optimized demo page
* v1.2.4 fix IntersectionObserver
* v1.2.3 set lazyload to false, as IntersectionObserver is not working yet
* v1.2.0 release on npm, uses vitejs instead of webpack
* v1.1.901 betterify example page
* v1.1.9 remove gulp and rollup and use webpack instead
    * use Babel 7
    * add changelog to README
    * add Compile from source instructions
* v1.1.8 add rel=0 parameter to YouTube videos

## Compile from source
* clone the github repo
* cd into the cloned directory
* run `npm install`
* make your changes in the script or the scss file
  
##Development server with live reload
 
Use `npm run dev` to run a server with HMR. It uses vite https://vitejs.dev/ which includes the script as a JS module in modern browsers.

## License

[MIT](https://opensource.org/licenses/MIT). © 2021 Jens Martsch

[MIT](https://opensource.org/licenses/MIT). © 2016 Viktor Bergehall
