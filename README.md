***
# markdown-it-reddit-spoiler
[![npm](https://img.shields.io/npm/v/markdown-it-reddit-spoiler?color=red)](https://www.npmjs.com/package/markdown-it-reddit-spoiler)

Reddit style spoilers for markdown-it by ${Mr.DJA}.
***

>This is a plugin for [markdown-it](https://github.com/markdown-it/markdown-it) uses [markdown-it-regexp](https://github.com/rlidwka/markdown-it-regexp) to render spoilers like those on Reddit: `>!spoiler!<`. Sounds good huh? \^-^

## Install:
**Node.js**:

To install the plugin simply use this command:
```bash
npm install markdown-it-reddit-spoiler --save
```
Then simply require it:
```js
const markdownitRedditSpoiler = require("markdown-it-reddit-spoiler");
// => object
```
This method will work on Node, but it can also work on browser after compiling it using [Webpack](https://webpack.js.org/guides/getting-started/).

**Browser**:

A pre-compilled version for browser is available on [JsDeliver CDN](https://cdn.jsdelivr.net/gh/iMrDJAi/markdown-it-reddit-spoiler/dist/main.js):
```html
<script src='https://cdn.jsdelivr.net/gh/iMrDJAi/markdown-it-reddit-spoiler/dist/main.js'></script>
```
It will be declared as `window.markdownitRedditSpoiler`:
```js
const markdownitRedditSpoiler = window.markdownitRedditSpoiler;
// => object
```

## Usage:

You will see these methods and properties on the returned object:

| Name | Description |
|:--:|:--:|
| spoiler | This will render spoilers for you <3 |
| blockquote | This is required to stop blockquotes from overriding spoilers |
| nestedRenderer | This is required to render the nested tags inside spoilers | 12 |
| env | This is needed to enable references outside spoilers | 
| openTag | This is used to customize the open tag of spoilers since HTML doesn't have a real spoiler tag | 
| closeTag | This one is for customizing the spoilers close tag | 

This is a simple example:

```js
const markdownit = require('markdown-it'); //Our markdown renderer
const markdownitRedditSpoiler = require('markdown-it-reddit-spoiler'); //Our package

function renderMarkdown(text) { //A function to render markdown from a given string

    //This will deal with references
    let env = {};
    markdownit('zero').enable('reference').parse(text, env);
    markdownitRedditSpoiler.env = env;

    //The main renderer
    var mdRender = markdownit({
        linkify: true,
    }).use(markdownitRedditSpoiler.spoiler) //Spoilers enabled
    .use(markdownitRedditSpoiler.blockquote); //Spoilers friendly block quotes enabled

    return mdRender.render(text); //Render Markdown!
}
```

Then add some css:

```css
.md-spoiler {
  display: inline-block;
  background: #1b1b1b;
  border-radius: 4px;
  padding: 4px;
}

.md-spoiler>* {
  z-index: -1;
  opacity: 0;
  position: relative;
}

.md-unhidenspoiler>* {
  opacity: 1 !important;
  z-index: 1 !important;
}
```

Preview:

![image](https://i.imgur.com/skJEIty.png)

A more advanced example:

```js
const markdownit = require('markdown-it'); //Our markdown renderer
const markdownitIns = require('markdown-it-ins'); //Another optional plugin
const markdownitRedditSpoiler = require('markdown-it-reddit-spoiler'); //Our package

function renderMarkdown(text) { //A function to render markdown from a given string

    //This will deal with references
    let env = {};
    markdownit('zero').enable('reference').parse(text, env);
    markdownitRedditSpoiler.env = env;

    //This one is for customizing the nested tags renderer
    markdownitRedditSpoiler.nestedRenderer = function () {
        let renderer = markdownit({
             linkify: true,
        }).disable('table').disable('list').disable('heading')
        .disable('lheading').disable('fence')
        .disable('blockquote').disable('code').disable('hr')
        .use(markdownitIns); //Now markdownitIns will work inside spoilers
        return renderer;
    }

    //It's very simple to customize the open/close tag of spoilers
    markdownitRedditSpoiler.openTag = '<details><summary>Spoiler ⚠</summary>';
    markdownitRedditSpoiler.closeTag = '</details>';

    //The main renderer
    var mdRender = markdownit({
        linkify: true,
    }).use(markdownitIns)
    .use(markdownitRedditSpoiler.spoiler) //Spoilers enabled
    .use(markdownitRedditSpoiler.blockquote); //Spoilers friendly block quotes enabled

    return mdRender.render(text); //Render Markdown!
}
```

Preview:

![image](https://i.imgur.com/hXtC7OM.png)

**Enjoy <3**.

## Dependents Projects:
Wanna use **markdown-it-reddit-spoiler** on your next big project? Let me now and it will be listed here! :)

- [iMrDJAi-MDE](https://github.com/iMrDJAi/iMrDJAi-MDE): Open source, Simple, Easy to use and fully featured Markdown editor - by me.

## Notes:
- This package has made by [${Mr.DJA}](https://invite.gg/MrDJA).
- Do you like it? Gimme a star ⭐ and I'll smile 😃.
- You are free to suggest anything and I will try to add it soon if I found it useful.
- If you found any mistake (including the README file) feel free to help to fix it.
- Please report any bugs.
- **Made with ❤ in Algeria 🇩🇿**.