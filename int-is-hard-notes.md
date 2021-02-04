---
title: Interneting is Hard
author: Daniel W. Kennedy
output:
  html_document:
    css: web-devel-notes.css
    self_contained: no
    theme: null
    highlight: null
---

<div class='container'>
<div class='page'>
<div class='sidebar'>
<h3>Sections</h3>
<p class='sidebar-list'>
<a class='sidebar-link' href="#introduction">Introduction</a>
<a class='sidebar-link' href="#basic-web-pages">Basic Web Pages</a>
<a class='sidebar-link' href="#linking-and-images">Linking and Images</a>
<a class='sidebar-link' href="#css">CSS</a>
<a class='sidebar-link' href="#the-box-model">The Box Model</a>
<a class='sidebar-link' href="#floats">Floats</a>
<a class='sidebar-link' href="#flexbox">Flexbox</a>
</p>
</div>
<div class='content'>


### Notes on compilation

To correctly render in HTML with CSS, run pandoc with standalone (`-s`) option:
y
```shell
pandoc -s int-is-hard-notes.md -o iis-notes.html --css web-devel-notes.css
```

# Introduction

HTML stands for ***H**yper**T**ext **M**arkup **L**anguage*. Hypertext means text with links, and markup means taking the raw content and "marking it up" to have a structure.

CSS stands for ***C****ascading* ***S****tyle* ***S**heets*. It takes the structured content and formats it.

JavaScript allows content and formatting to be interactive.

The explanation given is that the HTML is the abstract text and images which are used to make the webpage, the CSS is the actual webpage itself, and the JavaScript is the behaviours which manipulate the HTML and CSS.

As an example, one might have this for HTML:

```html
<p id='some-paragraph'>This is a paragraph.</p>
```

which says to create a `p`aragraph (referenced in code with the ID `'some-paragraph'`), where the content is "This is a paragraph". This is some raw content, but what do paragraphs look like? What font, size, colour, spacing etc. does the text have? These questions are answered with CSS:

```css
p {
  font-size: 20px;
  color: blue;
}
```

So the colour and font size will be <span style="color:blue;font-size: 20px">blue and 20 pixels</span>.

To make the content interactive, we need to use JavaScript:

```js
var p = document.getElementById('some-paragraph');
p.addEventListener('click', function(event) {
  p.innerHTML = 'You clicked it!';
});
```

<p id='some-paragraph'>This is a paragraph. (Try clicking me)</p>

<script>var p = document.getElementById('some-paragraph');
p.addEventListener('click', function(event) {
  p.innerHTML = 'You clicked it!';
});</script>

There is no need to understand exactly how it is working, but you can probably deduce that on a click from the user, the content of the paragraph changes to "You clicked it!".

### Web Development versus HTML+CSS+JS

Knowing the holy trinity is a *prerequisite* to being a web developer, but there are many other skills that a successful web developer needs other than how to code in each of them. Some of these skills are creating reusable templates to maximise efficiency, standing up a web server, version control for code in local computersand remote servers, and pointing a domain name at a server so people can actually go to your website.

*Interneting is Hard* does not teach these skills, only the HTML+CSS to create websites. 

### Web Publishing

What is it to publish to the web? We generally arrange content into webpages, and then connect a few webpages into a *website*. These connections are called links, so we can get from one webpage in the website to another.

An analogy is to the printing press, which used block printing to create pages (webpages), and then those pages were bound into books (websites). HTML+CSS can be thought of as the printing blocks: the tools used to create the create the content of the pages.

### Frameworks

Writing huge, complicated websites is hard, and much of it is doing simple things over and over again. To make this more straightforward,  developers have created frameworks like *bootstrap*, *ZURB foundation*, and *Pure CSS* to "abstract away" the actual HTML+CSS. Any good web developer will use these frameworks, but it is foolish to use them without understanding the fundamentals of HTML and CSS.

### Atom Editor

The atom editor is lightweight and simple. Use Ctrl+Shift+H to render the html after installing the `atom-html-preview` package via

```shell
apm install atom-html-preview
```

# Basic Web Pages

The language of HTML can be thought of as the structural aspects of the webpage, such as paragraphs, headings, sections and boxes (called floats). The code below is the basic structure for a webpage.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Metadata goes here -->
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>
```

The top line: `<!DOCTYPE html>` is read by browsers to mean that this is a HTML5 webpage and is absolutely necessary and doesn't need to be changed. The next line has a `<html>` *tag*, and there is an accompanying *closing tag* `</html>` on the last line. These opening and closing tags need to *wrap* the entire webpage. HTML is made up of opening and closing tags, similar to opening and closing brackets, and the content inside of the tags is called an *element*. 

Inside of the `<html>` element is the `<head>` element and the `<body>` element. The `<head>` element provides all of the metadata of the webpage, such as what the title of the page is (think what goes on the tab in the browser), and what CSS stylesheets (more on this later) are associated with the webpage. The `<body>` element contains the actual content which is seen when the page opens.

The text inside of the `<head>` and `<body>` elements are surrounded by `<!--` and `-->` strings, which symbolise a *comment*: some characters which are not code and are not rendered into any part of the visible webpage, and do not affect the webpage in any way. They are used by programmers to communicate how the code works or other information useful to the back end but not to the end-user.

There is currently no metadata or visible content on the webpage.

### Common tags

The `<title>` element contains the title of the webpage, which for most browsers shows up in the tab. HTML elements are *nested*, meaning that elements have elements themselves by containing the tags and content of "subelements". This means that in order to write neat HTML, you should always ensure the subelements have been closed before closing an element. Here is an example of what not to do:

```html
 <head>
   <title>Interneting is somewhat difficult
 </head>
```

Incidently, HTML will still render a webpage with this kind of error, and it may even be "correct", in the sense that it behaves as intended, but it could also have unexpected behaviour, and will be difficult to understand from a programming point-of-view.

The following tags will go instead in the `<body>` element, because they concern visible elements of the page itself.

The `<p>` element denotes paragraphs of text as we have seen previously. The subelements should always be indented to ensure it is easy to read the webpage.

Basic HTML provides six levels of headings from `<h1>` to `<h6>` with `<h1>` being the highest. Typically the first element in the body will be a title `<h1>` which matches or is similar to the content in the `<title>` element. 


### Lists

Bullet points and enumerated lists are created using the `<ul>` and `<ol>` tags respectively. Each list item is given by `<li>` tags. For example:

```html
<ol>
  <li>Bananas</li>
  <li>Oranges</li>
  <li>Apples</li>
</ol>
```

creates an ordered list:

<ol>
  <li>Bananas</li>
  <li>Oranges</li>
  <li>Apples</li>
</ol>

The best reference for HTML is the [Mozilla Developer Network (MDN)](https://developer.mozilla.org/en-US/).

Notice that in the above list we get 1.,2.,3.. This can be altered using CSS, which will be detailed later.

The `<p>`, `<ol>`, `<h1>` and other elements we've learnt so far in the `<body` section are called 'block-level elements', and generally take up their own line, or lines. These are contrasted with 'inline elements', which affect portions of text within a single line. One example is the `<em>` tag, which is most often associated with an italicised section. The `<strong>` type is generally associated with bold type. Note that this is the default behaviour and can be altered (as we will see later) in the CSS of the webpage to be expressed differently, so a more general association is that `<em>` is for a weak emphasis, and `<strong>` is for a strong emphasis.

Note that these aren't style markings per se; they are markings for where a particular style is to be used. There are default behaviours, however they can all be changed in CSS, and new styles can be defined in addition to the base HTML elements. HTML provides the structure, and CSS tells the browser how to display the structure.

### Line Breaks

A small number of tags are 'self-closing' (also called empty elements), in that they only have a single tag rather than an opening and closing tag. One example is the line break: `</br>`. For example:

```html
<p>One line
  Second Line</p>
```

displays as:

<p>One line
  Second Line</p>

So to get the required line break we need to use the `<br/>` tag:

```html
<p>One line<br/>
  Second Line</p>
```

which displays as:

<p>One line<br/>
  Second Line</p>
  
However, note that like other tags the <br/> tag should always convey meaning. For example, never use six `<br/>` tags in a row in order to achieve a desired spacing. This will be handled, as we shall see, in the CSS file.

### Horizontal rule

Another self-closing tag is the horizontal rule `<hr/>`. This should represent a thematic break in the content. For example it may represent the start of the appendix or footer information, or a new post in a blog. As with all previous tags, the `<hr/>` tag is less an actual horizontal line, and more of a meaningful peice of structural information. For example, it doesn't make sense to insert a `<hr/>` after every `<p>`, because such a line would be more indicative of the `<p>` structure than an actual thematic break. We will see that we can alter the behaviour of `<p>` in the CSS to accomplish this much more sensibly.

For both `<hr/>` and `<br/>`, the trailing slash `/` can actually be left out and the expected behaviour will still occur. It is ultimately a matter of personal coding style, but a possible benefit for leaving the slash in is that you will immediately see that it is a self-closing tag and not an opening tag.

## More Elements

For more information on elements, see [MDN's HTML Element Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

# Linking and Images

The previous sections have shown how to structure a single webpage using HTML elements, which is similar to a Word document. In this section the webpage will move on from the Word document to include images in the page, and link to other webpages. To achieve this, we'll also cover attributes, a fundamental part of HTML.

## Setting up

The following section requires setting up a directory with three HTML files and an images directory. Consult the relevent [section](https://www.internetingishard.com/html-and-css/links-and-image/) on *Interneting is hard* to set up correctly.)

## Links

Links are constructed using the `<a>` tag, which stands for "anchor". If you try to use an `<a>` element on its own:

```html
<p>I think <a>this</a> is a link?</p>
```

then you will get:

I think <a>this</a> is a link?

Nothing out of the ordinary! This is because the `<a>` tag doesn't have any functionality without specifying attributes. Attributes add meaning to the elements they are associated with. Recall that elements are just structural information for the raw content, so attributes provide more specific structural information on how the content is to be structured. For a reference on what attributes are available for each element type, consult the [MDN HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

To make the <a> element work, we need to give it something to link to, which we do via the `href` attribute:

```html
<p>I know that <a href='links-and-images/images.html'>this</a> is definitely a link.</p>
```

<p>I know that <a href='links-and-images/images.html'>this</a> is definitely a link.</p>

The value supplied of `href` supplied to `<a>` is a file path to the HTML file `images.html`, so it shows `<a>` what to link to. In HTML, the equals (`=`) sign is used to assign the value to the attribute. Either single (`'`) or double (`"`) quotation marks can be used when specifying the character string value. When `href` is supplied, `<a>` knows that it is infact a link, and so the default formatting (blue underlined) is used.

## Types of Links

The values of `href` in the previous section are given in a specific form called a ***U**niform **R**esource **L**ocator (URL)*. There are three ways of linking from one webpage to another using URLs:

- *relative*: Specify a path from the original webpage location to the linked page location.
- *root relative*: Specify a path relative to the domain root location.
- *absolute*: Specify a location in a universal way.
	
### Absolute links

Absolute links are the most detailed and the most universal method of specifying a location. They have three parts to them:

1. The *scheme*: The protocol in which the information is to be read (usually `http` or `https`), which is followed by the well-known `://` delimiter.
2. The *domain*: The web domain in which the webpage is located. E.g. `www.google.com.au`
3. The *path*: a file path to the requested page from the domain.
	
As an example, we can link to the MDN HTML elements reference with:

```html
<p><a href='https://developer.mozilla.org/en-US/docs/Web/HTML'>MDN HTML reference<a></p>
```

### Relative Links

When the other webpage is in the same domain/file as the current page, then you can opt not to specify the scheme and domain, and just specify the path from one page to the other. This called a *relative link*, because the link is relative to the current webpage's location. For example, we have already used a relative link from this notes webpage to `links-an-images/images.html`. Forward-slashes (`/`) are used for navigating directories. To link to a webpage in a parent folder, you can use the standard `..` notation.

### Root-Relative Links

Similar to relative links, it is possible to link to a webpage in the same domain by specifying it from the root, or base of the domain. Because all the HTML files in the tutorial are local, rather than hosted at a domain on a webserver, root-relative links will not work here. To specify a root-relative link, you begin the path with a forward slash (`/`).

### Targets

A second attribute for `<a>` is `target`, which tells `<a>` how to open the link. The default behaviour for a link is to replace the current webpage with the linked webpage once opened, but it is also possible for the browser to open a new window or tab by specifying `target='_blank'`:

```html
<li>Absolute links, like to
    <a href='https://developer.mozilla.org/en-US/docs/Web/HTML'
       target='_blank'>Mozilla Developer Network</a>, which is a very good
       resource for web developers.</li>
```

There are other possible values for `target` which allow for different behaviours (see [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a) on MDN for details). 

### Spacing in Links

URLs do not allow spacing, and it is good practice to avoid them, but it happens sometimes. When spaces occur, the special coding for spaces is `%20`, which needs to be substituted in place of a space.

## Images

Images are defined outside of the webpage, unlike the previous elements. Like links, we will need to point to them in the webpage in order for the browser to render them. To refer to an image in the webpage, we use the element `<img/>`. The attribute `src` provides a URL to the image file:

```html
<img src='links-and-images/images/mochi.jpg'/>
```

<img src='links-and-images/images/mochi.jpg'/>

The story becomes a bit more complex because of the many screen sizes in which webpages are now viewed, and this will be explained in later sections.

### Image formats

There are many formats in which images can be rendered, with different benefits and limitations.

**JPG**: This format allows for large colour palettes such as photos without having a huge file size. They don't allow for transparent pixels, which can sometimes result in seams on the borders of the picture.

**GIF**: This format allows for very simple animations but only simple colour palettes and are inappropriate for photos.

**PNG**: This format has a slightly larger file size that JPG, but allows for different levels of opacity. This is ideal for diagrams, logos, and icons. They are suboptimal for photos (against JPG) and can't do animation.

**SVG**: This format is vector-based rather than pixel based, meaning that the building blocks of the image are lines and shapes as opposed to a grid of colour-coded pixels. This means that they can be blown up as much as desired and won't lose quality. They are ideal for the same situations as PNGs and are preferable where possible.

When the image has many geometric objects (lines, shapes), SVG can be suboptimal and can be a very large file size. This can occur in diagrams which contain text, since characters tend to be complex shapes. In these cases, a high quality PNG is preferable.

### Image dimensions

The default behaviour for `img` is to use the inherent dimensions of the image when rendering it on the webpage. The `width` attribute of `img` allows this to be modified:

```html
<img src='links-and-images/images/mochi.jpg' width='75'/>
```

<img src='links-and-images/images/mochi.jpg' width='75'/>


The `width` is specified in pixels, so the above image is 75 pixels in width. Note that it is usually better to set dimensions with CSS, however there are occasions where it's useful.

### Text alternatives

The `alt` attribute of `img` allows you to set some text as "alternative text" to the image. This text is useful for:

- search engines: image and webpage search engines can find the content more easily.
- vision impaired people: text-to-speech programs can read out the alternative text.
- errors: If for some reason the image cannot be found the alternative text will be displayied instead.
	
### Document Language

The `<html>` element (recall that this is the element which surrounds the entire webpage) has a `lang` attribute which specifies what languate the webpage is written in. Instead of writing the language name in English, each language has an alphabetical code of a few characters. To look up the code for a language see [here](http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry). The code for English is `'en'`:

```html
<html lang='en'>
```

### Character Sets

Each character you see is coded in a set of binary values (0s and 1s), but there are few different ways of converting the binary information into a visible character. The result is that the wrong character might be displayed if the browser is using the wrong encoding. This encoding is called a character set.

To specify the character set you use the `<meta>` tag in the `<head>` element:

```html
<meta charset='UTF-8'/>
```

UTF-8 is a very common character set and should be directly specified for all your webpages.

## HTML Entities

Some characters which are rendered in a webpage are actually represented as a special sequence of characters in the HTML of a webpage. Reasons for this might be:

- the character is reserved: this means that the character is used in the HTML language itself, so to avoid confusion, rendering this character on the webpage requires an entity. Examples are &lt; and &gt;.
- the character is represented on the keyboard. An example would be &mu;.

To write a HTML entity you begin with an ampersand (`&`), and end with a semicolon (`;`). There are a huge number of HTML entities, and you can find a good reference [here](https://dev.w3.org/html5/html-author/charref). Four very common HTML entities are double quotes (&ldquo; and &rdquo;) and single quotes (&lsquo; and &rsquo;).

With the uptake of UTF-8 the need for entities is reduced, but they are useful for writing reserved characters and writing straight HTML.

## Template for all websites

The below code provides a basic starting template for any website, ensuring that a language (English) is specified and a character set (UTF-8) is explicitly specified.

```html
<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='UTF-8'/>
    <title>Some Web Page</title>
  </head>
  <body>
    <h1>Some Web Page</h1>
    <!-- Rest of the page content -->
  </body>
</html>
```

# CSS

**C**ascading **S**tyle **S**heets (CSS) is the way of controlling (and therefore improving) the way the webpage looks, by specifying how each of the (visible) elements should be rendered. HTML takes the content of the website and structures it in a systematic way, and CSS takes that structured content and gives it a visual design.

HTML says "this content is a heading, or this content is a paragraph", and CSS says "this is what a heading looks like, or this is what a paragraph looks like". CSS and HTML files are typically separate text files which interact with each other to make the webpage.

The associated example files in this chapter are in the directory `hello-css`.

## Structure of CSS

CSS is made up of "rules": sections of code which define a particular aspect of design. A rule is made up of three types of thing:

- *selector*: This part defines what HTML elements this CSS rule applies to.
- *property*: Inside curly brackets (called a *declarations block*), the names of properties to be changed are given.
- *value*: For each property, a value is given.

```css
body {
  color: #FF0000;
}
```

The above example changes the colour of the body (basically the entire visible webpage) to red. 

## Linking a stylesheet

To get a CSS file to actually alter the design of a webpage, the HTML and CSS files need to be *linked*:

```html
<head>
  <meta charset='UTF-8'/>
  <title>Hello, CSS</title>
  <link rel='stylesheet' href='styles.css'/>
</head>
```

The `<link/>` element in `<head>` allows us to do that. The `rel` attribute of `<link/>` defines what the relationship between HTML and CSS, and `href` works in the same way as with anchors.

### Comments in CSS

To make a 
comment in CSS, you need to use `/*` and `*/`.

## More complex CSS

A rule does not have to be for a single element or property. See the below example for for multiple selectors and properties:

```css
h1, h2 {
  color: #414141;               /* Dark gray */
  background-color: #EEEEEE;    /* Light gray */
}
```

The semicolons are **necessary** for the CSS to function properly; the code will break if they are not present. 

**ASIDE** Shades of grey

Black-text on white background is difficult to read, and so the above colours for dark and light grey are better.

The rule for `<body>` will apply to all subelements, but you can put specific rules for subelements, which will override the rules for the higher element if they clash.

```css
h1 {
  font-size: 36px;
}
```

## Units of Measurements

CSS has many units of measure available, but the most common are pixels (`px`), and `em`. `px` is an absolute measure, and `em` is a relative measure. `em` is relative to the base font size. The base font size is the size given for the higher element, so for example:

```css
body {
  color: #414141;               /* Dark gray */
  background-color: #EEEEEE;    /* Light gray */
  font-size: 18px;
}

h1 {
  font-size: 2em;
}

h2 {
  font-size: 1.6em;
}
```

`<h1>` and `<h2>` take the `font-size` value in `<body>` as a base.

### Fonts

The attribute `font-family` tells the browser what font to use for the specified element. It accepts multiple values, which will be used in order of most to least preferred. This is because different users will have different font-sets.

```css
h1, h2, h3, h4, h5, h6 {
  font-family: "Helvetica", "Arial", sans-serif;
}
```

## Lists

The `list-style-type` attribute allows the bullet icons (`ul`) and enumerations (`ol`) to be altered:

```css
ul {
  list-style-type: circle;
}

ol {
  list-style-type: lower-roman;
}
```

The `none` option is useful for `<ul>`, because lists give the appearance of buttons. As an example, we can think of the HTML as being what the search engine sees: an unordered list, and the CSS is what the human sees: a set of buttons. The [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-image) gives a set of possible options.

## Text styles

There are several options for "decorating" text using the `text-decoration` property, including `underline`, `line-through`. Line-throughs traditionally represents deleted text, but it would be more appropriate to use a HTML tag such as `<del>` to indicate this, since HTML is for structure, rather than CSS.

You can also define the text alignment:

```css
p {
  text-align: left;
}
```

You can also set the `font-weight` (`bold` or `bold`) and `font-style` (`normal` or `italic`).

## Cascading

CSS files provide the design of the webpage, and because they are a separate file, they can be used for multiple webpages. In fact, you might have an overarching CSS file for your entire website. This practice helps to ensure a consistent design accross all webpages.

The reason CSS files are called cascading is because webpages have a heirarchy of CSS files used for formatting in a special preference. The order of preference from least to most prefered is:

- The browser’s default stylesheet
- User-defined stylesheets
- External stylesheets (that’s us)
- Page-specific styles (that’s also us)
- Inline styles (that could be us, but it never should be)

Inline styles, which should be avoided if possible, take highest precedence, so default styles and other stylesheets will be ignored in favour of them.

## Page-specific styles

For styles which are specific to a webpage, the `<style>` element is used in the `<head>` section of the HTML file.

```css
<head>
  <meta charset='UTF-8'/>
  <title>Dummy</title>
  <link rel='stylesheet' href='styles.css'/>
  <style>
    body {
      color: #0000FF;    /* Blue */
    }
  </style>
</head>
```

This will take precedence over external stylesheets, and will only affect the webpage itself. This however is not a prefered method for applying styles from a web development perspective, because it requires copy-pasting to recreate it on other webpages. Additionally, if updates to the style are required, then the number of changes to be made is very large compared to if all style was given by a single, external `.css` file.

### Inline styles

The highest preference for styles is inline styles, meaning that the style is applied in the code of the element itself. See the below example:

```html
<p>Want to try crossing out an <a href='nowhere.html'
   style='color: #990000; text-decoration: line-through;'>obsolete link</a>?
   This is your chance!</p>
```

The styles are applied as attributes to the anchor `<a>` element, and these style values will take precedence over all browser defaults, external stylesheets, and page-specific styles.

Even more so than page-specific styles, inline styles should be avoided if at all possible.

## Multiple stylesheets

A webpage can have multiple stylesheets defined for it. In the example below, there are two `.css` files linked to via `<link>` elements:

```html
<head>
  <link rel='stylesheet' href='styles.css'/>
  <link rel='stylesheet' href='product.css'/>
</head>
```

The order of the `<link>` elements is important, as later stylesheets will override earlier ones.

## Summary

The Mozilla Developer Network (MDS) has very useful [CSS reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference) for finding information on different properties.

# The Box Model

HTML and and the CSS learned so far are only part of the story of how a webpage looks. HTML provides a structure for the raw content, and CSS rules tell the browser how to format the structure, but what is missing is the visual structure or *layout* of the website itself. The framework in which the structured content is layed out on the webpage is called the "CSS Box Model". 

CSS treats each HTML element as a box, or rectangle. In the default formating, each element is laid out in the order it is given, but this does not have to be the case.

## Setup

The example for the following section is given in the directory `css-box-model`.

## Block and Inline Elements

As mentioned previously, all HTML elements are defined as either *block* elements, or *inline* elements. `<h1>` and `<p>` are examples of b
lock elements. Block elements defined the flow of the webpage, while inline elements do not.

To see the "boxes" the each element defines, you can use CSS to change the `background-color` attribute/property:

```css
h1, p {
  background-color: #DDE0E3;    /* Light gray */
}

em, strong {
  background-color: #B2D6FF;    /* Light blue */
}
```

Blocks have several behavioural rules to understand:

1. Block boxes always appear *below* previous block element boxes.
2. Block box widths are always set by the width of its container.
3. The height of the box is defined by the content it contains.
4. Inline boxes *do not* affect vertical spacing. They are for styling inside of a box, not for deciding layout.
5. The width of inline boxes is determined by the containing content rather than the width of the content.

To show how this works, we can override the default display behaviour of `<em>` and `<strong>` to be `block` rather than `inline`:

```css
em, strong {
  background-color: #B2D6FF;
  display: block;
}
```

The result is that the `<em>` and `<strong>` elements start on a new line, since block elements have to be below previous block elements.

## Box model properties

There are four properties which define the box dimensions for an element.

### Padding

```css
h1 {
  padding: 50px;
}
```

The *padding* defines the amount of internal space between the edge of the box and the content.

You can also provide separate values for all four directions:

```css
p {
  padding-top: 20px;
  padding-bottom: 20px;
  padding-left: 10px;
  padding-right: 10px;
}
```

An alternative method of specifying padding is by using a particular CSS shorthand for this action:

```css
p {
  padding: 20px 10px;  /* Vertical  Horizontal */
}
```

The vertical (top and bottom) padding is specified, followed by the horizontal (left and right). There is also a shorthand for all four directions:

```css
p {
  padding: 20px 0 20px 10px;  /* Top  Right  Bottom  Left */
}
```

It is a matter of style whether you want to use shorthand or not.

## Border

The border is a line drawn around the edges of the box.

```css
h1 {
  padding: 50px;
  border: 1px solid #5D6063;
}
```

The above syntax for `border` is line-width/line-style/line colour. You can also specify the particular edge for the border:

```css
h1 {
	border-bottom: 1px solid #5D6063;
}	
```

Borders are useful for debugging, since if you can't actually see how an element is being rendered, drawing a red box around it would certainly help to narrow it down!

### Margins

Margins define the space between a given box and the boxes around it. It is similar to padding, but it acts outside of the border, whereas padding acts within. It is often difficult to determine which is the correct attribute to use to separate element content, but here are a few considerations to help determine:

- The padding of a box has a background, whereas the larger box defined by the margins is always transparent.
- For a clickable element (i.e using JavaScript), clicking on the area in the padding will work, but the margins will not.
- Margins collapse vertically, but boxes do not.

Inline elements completely ignore any vertical margin instructions. They will however respect horizontal margins. Altering the padding of an inline shows that the box increases and may obscure a previous line, but the box will be centered at the same location regardless of the value of the padding.

### Vertical Margin Collapse

Margins don't add together in the vertical space. This means that for two consecutive block elements, if the higher one has a bottom margin of 20px, and the lower has an upper margin of 10px, the space between the boxes will be rendered as 20px, the higher value.

To prevent margin collapse, you can add an invisible element between the two elements:

```html
<p>Paragraphs are blocks, too. <em>However</em>, &lt;em&gt; and &lt;strong&gt;
elements are not. They are <strong>inline</strong> elements.</p>

<div style='padding-top: 1px'></div>  <!-- Add this -->

<p>Block elements define the flow of the HTML document, while inline elements
do not.</p>
```

The invisible element must have non-zero height in order for this to work.

There are also some other strategies for getting around margin collapse:

- Use `padding` instead of `margin`: Since padding doesn't collapse, you can use it instead to space out the values how you want. This will work, but it is only useful if you aren't using the padding for any other reason.
- Use a bottom-only or top-only convention: Only set the top or bottom margins for boxes. This means there is no smaller margin to cancel out and it is easy to define the spacings.
- Use the [flexbox](https://www.internetingishard.com/html-and-css/flexbox/) layout scheme.

## Generic Boxes

All the HTML elements we've looked at so far carry additional meaning other than a "box", but there are many situations where you might just want a generic box in styling the webpage. For example, you might be:

- preventing margin collapse as above
- grouping a particular set of paragraphs with a different styling.

The `<div>` and `<span>` elements serve this purpose. For example if you need to create a button, this can be done very effectively with a styled `<div>` box. For a `<div>` element we put:

```html
<div>Button</div>
```
and then style using CSS to get:

```css
div {
  color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
}
```
we get:

<div style='color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;'>Button</div>

This will of course affect all `<div>` elements, so we will need a way of selecting particular `<div>` elements if we want to use them for more than one purpose on a webpage. More on this later.

### Explicit Dimensions

So far the actual width of the elements have been decided by the padding and margin properties, but it is possible to explicitly set these values via the `width` and `height` attributes. We can modify the above button to be smaller as an example:

```css
div {
  color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
  width: 200px;
}
```
<div style='color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
  width:200px'>Button</div>

### Content Boxes versus Border Boxes

The `width` and `height` properties define the size of the box's *content* only, and the padding and and border are added on top of these alues. This means that the actual size of a box is going to be a combination of the content width, padding, and border width.

This can be a little complicated, so there are actually two options for using `width` and `height`, specified by the attribute `box-sizing`. The default value for `box-sizing` is `content-box`, which means `width` and `height` are defining the size of the content. The `border-box` option means that `width` and `height` determine the size of the entire box, including content, padding, and border, so if this option is used, the content box width and height are determined automatically using the box's dimensions minus padding and border width. The `border-box` option is considered as the prefered option for most modern web developers.

### Text alignment

Text can be aligned using the `text-align` property.

## Aligning Boxes

The flexbox and float methods will ultimately give complete control over alignment of boxes, but the auto-align method is within our grasp at this point. By specifying `auto` in our margin it automatically centers the button:

```css
div {
  color: #FFF;
  background-color: #4A90E2;
  font-weight: bold;
  padding: 20px;
  text-align: center;

  width: 200px;
  box-sizing: border-box;
  margin: 20px auto; /* Vertical  Horizontal */
}
```

<div style='color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
  width:200px;
  margin: 20px auto;'>Button</div>

This will only work for boxes where the width is explicitly defined for them.

## Resetting styles

Different browsers have different default properties, so it is a good idea to overwrite these properties using a universal selector (`*`). Adding

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

to the top of the CSS file controlling the style of the webpage will allow us to be confident that our webpage will style the way we expect it to.

## Summary


- Everything is a box.
- Boxes can be inline or block-level.
- Boxes have content, padding, borders, and margins.
- They also have seemingly arbitrary rules about how they interact.
- Mastering the CSS box model means you can lay out most web pages.

# CSS Selectors

In the previous section we could set rules for an entire class of elements to define the formating for all examples in the HTML. While this is a good thing, because it means there is consistency in the formatting within the webpage, it means were are constrained in the things we can do. For example, the generic box elements `<div>` are useful for a variety of purposes, so we'd like to have different behaviours for different examples of `<div>`.

*CSS selectors* allows us to map CSS rules to specific elements, and ignore others. In fact, we have already used a particular CSS selector called a *type selector*, which as you imagine, selects all examples of a type.

### Setup

The relavent files for this section are in the directory `css-selectors`.

## Class Selectors

*Class selectors* allow you to make different CSS rules for different elements of the same type. Each HTML element has a `class` attribute, which can be used to specify that some elements are of the same class, and thus need to have the same formatting. For example, we can create a paragraph element with the class `'synopsis'`:

```html
<p class='synopsis'>CSS selectors let you <em>select</em> individual HTML
   elements in an HTML document. This is <strong>super</strong> useful.</p>
```

These elements can be selected with a class selector in the CSS using a full-stop to indicate a class:

```css
.synopsis {
  color: #7E8184;        /* Light gray */
  font-style: italic;
}
```

**Naming conventions**: class names can be almost anything, but to ensure that the HTML and CSS is simple to read, it is best to stick to lower case letters and hyphens for spaces. Additionally, it is better to use meaningful names rather than descriptions of what the element should look like. For instance, in the above example the class is called `synopsis`, rather than something like `italics`.

Note that the `class` attribute does not change anything about the way the HTML works like other attributes. It is solely there to allow for more flexibility in applying CSS rules.

## Using classes with `<div>`

Now that we have classes we can use the `<div>` element for multiple purposes within out HTML page. Previously, we created a button using a `<div>` and some CSS, but the CSS applied to all `<div>` elements on the page. Here we will create a specific `button` class:

```css
.button {
  color: #FFF;
  background-color: #5995DA;    /* Blue */
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;    /* Dark gray */
  border-radius: 5px;

  width: 200px;
  margin: 20px auto;
}
```

And the HTML is given as:

```html
<div class='button'>Button One</div>
```

The result is:
<div class='button'>Button One</div>

## Container DIVs

Generic elements `<div>` do not chane the semantic structure of the HTML; they don't provide any additional meaning to the text. They are all about *presentation*, and are often used to wrap other HTML elements without altering how search engines see the the content. We can use a `<div>` and the *auto-margin* method to create a layout with a fixed width on the page.

```html
<body>
  <div class='page'>
	<!-- content -->
  </div>
</body>
```

We then assign the CSS rule to `page`:

```css
.page {
  width: 600px;
  margin: 0 auto;
}
```

The result is that the browser will always render the webpage as 600 pixels wide, regardless of the size of the window.

It is using this technique that complex webpage layouts are created. For example, we might create a `<div>` class called `.sidebar` to hold a set of links to form a sidebar on the left hand margin of the page.

Classes don't have to be for a single HTML element of course; they can apply a CSS rule to multiple elements in a webpage. For example, we can create another button:

```html
<div class='button'>Button Two</div>
```

<div class='button'>Button Two</div>

## Multiple Class Styles

Not only can we apply a single class rule to a number of elements, we can also apply a number of class rules to a single element!

```html
<div class='button call-to-action'>Button Two</div>
```

In the above code we are assigning both the `.button` and `.call-to-action` classes to the above `<div>` type element. We create a CSS rule for `.call-to-action`:

```css
.call-to-action {
  font-style: italic;
  background-color: #EEB75A;    /* Yellow */
}
```

The result is:

<div class='button call-to-action'>Button Two</div>

The button is yellow, because `.call-to-action` is overriding the colour property value for `.button`. Order is important in the CSS file, as classes specified after will override previous ones. The order of specifying in the `class` attribute in the HTML file is not important.

## Descendent Selectors

You can define CSS rules for subelements, or *descendents* of classes. This is useful, for example, when a class specifies an italic font-type, resulting in `<em>` inline elements looking the same as the surrounding text.

```css
.synopsis em {
  font-style: normal;
}
```

The above CSS causes `<em>` elements within `.synopsis` class elements to have a normal font-style, while still being (the default) italic in the rest of the webpage.

Descendent selectors are not limitted to classes. You could, for some reason make a CSS role for all `<strong>` elements within <h2> elements:

```css
h2 em {
	color:#FF0000;
}
```

## Pseudoclasses

Have you noticed how on some webpages, when you hover over a link it changes colour or some other formatting? This is accomplished by CSS pseudoclasses. They allow an element to have multiple different styles for different "states", such as a mouse click or hover.

### Link pseudoclasses

Pseudoclasses are defined using a colon. There are four common pseudoclasses for links.

- `:link`: a link that the user has not visited before.
- `:visited`: a link the user has visited before.
- `:hover`: a link with a users mouse hovering over it.
- `:active`: a link that is being pressed.

An example set of CSS rules for these four pseudoclasses is:

```css
a:link {
  color: blue;
  text-decoration: none;
}
a:visited {
  color: purple;
}
a:hover {
  color: aqua;
  text-decoration: underline;
}
a:active {
  color: red;
}
```

You can also apply formatting for a case where two pseudoclasses apply, such as when you are hovering over a link that has been visited.

```css
a:visited:hover {
  color: orange;
}
```

This is nice, because it means that the user can still see if they have visited the link before, even if they are hovering over it.

This does however mean, for internal CSS reasons, that we need to define the `:action` pseudoclass for it to show up read as expected.

```css
a:visited:active {
  color: red;
}
```

### Pseudoclasses for our buttons

We can also create pseudoclasses for the `.button` classes that we previously created. We first need to use the `<a>` anchor class instead of `<div>` for our buttons:

```html
<a class='button' href='nowhere.html'>Button One</a>
<a class='button call-to-action' href='nowhere.html'>Button Two</a>
```

These are inline elements, but we want our buttons to be block elements, so we need to change their `display` value, and set the properties for the pseudoclasses:

```css
.button:link,                 /* Change this */
.button:visited {             /* Change this */
  display: block;             /* Add this */
  text-decoration: none;      /* Add this */

  color: #FFF;                /* The rest is the same */
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;

  width: 200px;
  margin: 20px auto;
}

.button:hover,
.button:visited:hover {
  color: #FFF;
  background-color: #76AEED;  /* Light blue */
}

.button:active,
.button:visited:active {
  color: #FFF;
  background-color: #5995DA;  /* Blue */
}
```

Note that this replaces the previous `.button` CSS rule. The result is:

<a class='button2' href='nowhere.html'>Button One</a>
<a class='button2 call-to-action' href='nowhere.html'>Button Two</a>

Notice that the `.call-to-action` button styling has been overwritten. This is because the pseudoclass `.button:link` is **more specific** than `.call-to-action`, and so it takes precedence. This is an exception to the rule given earlier, where even though `.call-to-action` is defined later, the `.button` styling overrides due to the specificity of the pseudoclass `:link`.

To fix this we need to create pseudoclass rules for `.call-to-action` as well, which will then take precedence:

```css
.call-to-action:link,
.call-to-action:visited {
  font-style: italic;
  background-color: #EEB75A;     /* Yellow */
}

.call-to-action:hover,
.call-to-action:visited:hover {
  background-color: #F5CF8E;     /* Light yellow */
}

.call-to-action:active,
.call-to-action:visited:active {
  background-color: #EEB75A;     /* Yellow */
}
```

The buttons now have the desired formatting:

<a class='button2' href='nowhere.html'>Button One</a>
<a class='button2 call-to-action2' href='nowhere.html'>Button Two</a>

### Structural pseudoclasses

There are many other pseudoclasses other than link states. One useful one is the "last of type" which selects the final element of a given type in each container element:

```css
p:last-of-type {
  margin-bottom: 50px;
}
```

The above code creates a nice margin between the final paragraph and the next block element. There is also a `:first-of-type` pseudoclass which works in the expected way. Note that this does not only mean the final element on the webpage, but also every previous element which is the last of its type in its *container element*. Therefore, if there was a single `<p>` within a `<div>` element, then this will be formatted according to the above rule, regardless of whether there are later `<p>` elements in the HTML file.

It is possible to select only the very last `<p>`, but it requires using a **child selector**:

```css
.body > p:first-of-type {
  color: #7E8184;
  font-style: italic;
}
```

This `>` symbol indicates we want to look at all of the children of `.body`.


# Floats

With the CSS box model alone we can only really create single columns of content. This is because we force block elements to appear after each other, so we cannot get them to appear next to each other. With floats we will be able to use horizontal flow as well as verticle flow, allowing for a much more versitile range of layouts.

Note that floats have now been replaced with (Flexbox)[https://www.internetingishard.com/html-and-css/flexbox/] as the choice for formatting modern websites, but they are useful for understanding how older websites work. Additionally, because they are more limited than Flexbox, floats make for a kinder introduction to horizontal flow and creating sophisticated web pages.

## Set-Up

The files for this chapter are located in `floats`.

## Default HTML Layout

Floats work by changing the behaviour of the layout from the default. We know from previous sections that the default behaviour depends on whether an element is *box* or *inline*, and that box elements will not be rendered above a previous box element. Additionally, we know that a box element will horizontally fill its container element, unless it is given an explicit `width` property value.

## Floating an element

In its basic sense, all that float gives us the ability to do is determine the *horizontal* position of the element in the page. For example, we can start to create something that looks like a sidebar by changing the `float` property for the `.sidebar` class:

```css
.sidebar {
  float: left;                  /* Add this */
  width: 200px;
  height: 300px;
  background-color: #F09A9D;
}
```

The result is that the side bar box now sits inside the content box. It isn't just telling HTML to align the box to the left; it is also telling it that other elements can flow around the sidebar instead of being strictly underneath it. Notably it still sits below the menu box. You can also set `float` to be equal to `right`, or `none` if the goal is to override previous CSS rules. The float will remain inside the containers, and so using nested container div's can be used to create sophisticated layouts. 

If we let the `.content` class have a `float` value aswell, then it will sit beside the side bar rather than around it:

```css
.content {
  float: left;                  /* Add this */
  width: 650px;
  height: 500px;
  background-color: #F5CF8E;
}
```

However, this also affects the `footer` element, resulting in it being stacked horizontally as well! The reason is that once elements `sidebar` and `content` are floated, they are removed from the normal flow of the page. As a result, `footer` looks to `menu` as the last non-floated element, and puts itself below that.

## Clearing floats

Putting a red border on the `.page` class shows how the float elements don't follow the page border at all, where as the `menu` and `footer` elements stay within the border. Clearing a float is one way to deal with this issue.

```css
.footer {
  clear: both;            /* Add this */
  height: 200px;
  background-color: #D6E9FE;
}
```

In the above code, the `footer` element is given the `clear` property value of `both`, which means that `footer` will ignore the `float` properties of the other elements, and revert to default behaviour. This means that, as in line with the CSS box model, the `footer` element will go below the `sidebar` and `content` elements. The value `both` means it will "clear" both left and right floats, but you can select `left` or `right` only if desired, although this is rare if ever.

Another option is to contain the floats within a `<div>` element, and then the `footer` element will appear below the containing element. If however there are no elements in the `<div>` other than floats, then the height of the `<div>` will be 0. This causes a problem, because we might want that containing element to have a background or some style associated, but if it's height is 0, we won't be able to see it!

## Hiding Overflow

Because floats don't contribute to the height of their containing element, the containing element can be 0. To fix this, we can use the `overflow` property:

```css
.page {
  width: 900px;
  margin: 0 auto;
  overflow: hidden;             /* Add this */
  background-color: #EAEDF0;    /* Add this */
}
```

This means that the containing element `page` recognises any containing floats when determining its height.

## Full Bleed Layouts

Most websites will carry on with a background to the edge of the page, and have some content in the center. In our example, the `<page>` element is doing the job of centering the floats, so allowing it to blead out to the edge of the webpage would result in the `sidebar` and `content` elements moving to the side. We therefore need to add a container `<div>` around the `page` element to achieve this layout.

```html
  <div class='container'>                 <!-- Add this -->
    <div class='page'>
      <div class='sidebar'>Sidebar</div>
      <div class='content'>Content</div>
    </div>
  </div>
```

We then move the `background-color` property to the container rather than the page.

```css
.page {
  width: 900px;
  margin: 0 auto;
}

.container {
  overflow: hidden;
  background-color: #EAEDF0;
}
```

We need to give `.container` the `overflow: hidden` property, otherwise its height will be 0 and we won't see the background colour. Notice that the `.page` class no longer has an `overflow` property. This is because the purpose of the `page` is now solely to centre the content of the webpage, and the `container` element does the background. The `sidebar` and `content` elements provide the content of the page.

<div class='menu_ex_float'>Menu</div>
<div class='container_ex_float'>
<div class='page_ex_float'>
<div class='sidebar_ex_float'>Sidebar</div>
<div class='content_ex_float'>Content</div>
</div>
</div>
<div class='footer_ex_float'>Footer</div>

## Equal Width Columns

Floats allow us to create columns in a similar way to the `sidebar` and `content` floats above:

```html
<div class='footer'>
  <div class='column'></div>
  <div class='column'></div>
  <div class='column'></div>
</div>
```

and then style these `column`s:

```css
.column {
  float: left;
  width: 31%;
  margin: 20px 1.15%;
  height: 160px;
  background-color: #B2D6FF;    /* Medium blue */
}
```

The result is three well separated columns in the footer. The percentage sign `%` is a relative width to the parent element, meaning that the width of `column` will be 31% of the width of `footer`. Therefore, when the webpage is resized, the width of the columns will grow and shrink responsively in order to be be 31% of the footer. The `margin` for the left-right directions is also set using a percentage.

<div class='footer_ex_float'>
<div class='footer-item_ex_float'></div>
<div class='footer-item_ex_float'></div>
<div class='footer-item_ex_float'></div>
</div>

## Grid Layouts

The grid layout is a simple extension of the column layout. If you add more `<div class='column'></div>` elements, then they will eventually spill below the footer, because the footer is too short to contain them. Fortunately, all we have to do is make the `footer` aware of the heights of the containing floats by adding an `overflow: hidden` property and drop the explicit `height` property.

Note that we have re-used the `column` class here, and exposed a bit of a flaw in the names of our classes. If a web developer wants to change the footer from column based to grid-based, then they have to either use the name "column" for something that isn't a column anymore, or change the class name and risk breaking the site! In fact, the original web developer shouldn't have really called them columns in the first place, because that refers to their appearance, not their intrinsic function. Instead, the class should be called `footer-item` or something similar to show that they are in fact just elements of the footer.

```html
   <div class='footer'>
      <div class='footer-item'>
	<div class='avatar'></div>
	<h3 class='username'>Bob Smith</h3>
	<p class='comment'>Aptent vel egestas vestibulum aliquam ullamcorper volutpat
	  ullamcorper pharetra hac posuere a rhoncus purus molestie torquent. Scelerisque
	  purus cursus dictum ornare a phasellus. A augue venenatis adipiscing.</p>
      </div>
      <div class='footer-item'></div>
      <div class='footer-item'></div>
      <div class='footer-item'></div>
      <div class='footer-item'></div>
      <div class='footer-item'></div>
    </div>
```

<div class='footer_ex_float'>
<div class='footer-item_ex_float'>
<div class='avatar'></div>
<h3 class='username'>Bob Smith</h3>
<p class='comment'>Aptent vel egestas vestibulum aliquam ullamcorper volutpat ullamcorper pharetra hac posuere a rhoncus purus molestie torquent. Scelerisque purus cursus dictum ornare a phasellus. A augue venenatis adipiscing.</p>
</div>
<div class='footer-item_ex_float'></div>
<div class='footer-item_ex_float'></div>
<div class='footer-item_ex_float'></div>
<div class='footer-item_ex_float'></div>
<div class='footer-item_ex_float'></div>
</div>	

## Floats for Content

So far we've worked on the overall page structure to get it looking nice and pretty, but we also need to think about how the actual content of the page looks, such as images and text. We can draw on what we've done previously to structure the content. For example, we can elect to have the text flow around the image by making the image a float:

```css
.content {
  padding: 20px;
}

.article-image {
  float: left;
  width: 300px;
  height: 200px;
  margin-right: 20px;
  margin-bottom: 20px;
}

p {
  margin-bottom: 20px;
}
```

We've also given the `content` some padding so that the text and images don't go right up to the borders, and added some spacing to the paragraphs so there is more space between them. 

We now have a float (an image) inside of a float (the `content` element), and it is still functioning fine. Building a webpage is a recursive process; first you build the highest level structure, and then move inside that to add in the content. More complex layouts just mean more layers of nesting.

# Flexbox

Floats gave us horizontal and some vertical positioning control, but it was somewhat limited. Floats for many years were the industry standard for creating webpage layouts, and they have been used to build many millions of webpages on the internet. However, floats were only designed for "magazine-style" layouts, and are actually pretty limited in what can be accomplished with them. The *Flexbox* (named for "Flexible Box") method provides complete control over the alignment (left, right, centre), direction (vertical or horizontal) positioning, order of box positioning, and the size of the boxes. All modern browsers now support flexbox, whilst also having legacy support for float layouts. Generally, flexbox is always a better choice for constructing a layout, with floats only coming in handy when you want text to "flow" around a box, and legacy cases.

### Setup

The files for this chapter are contained in the `flexbox` directory.


## Overview

There are two types of box in the flexbox system: *flex containers*, and *flex items*. A flexbox container's job is to group items together and define how they should be positioned. Every element contained in a flex container is a flex item; its job is to tell the container how many elements need to be positioned. As with floats, defining a webpage's layout is a recursive, heirarchical process where boxes are nested within boxes within boxes. That is it!

## Flex Containers

To turn an element into a flexbox container, we need to use the `display` property in the CSS rule defining the class. This enables the flexbox layout mode, allowing us to use the flexbox properties. It is good practice to explicitly set it rather than rely too much on inheritance, so you can mix and match with other layout models such as floats.

Our current menu looks as below:

```html
<div class='menu-container'>
  <div class='menu'>
    <div class='date'>Aug 14, 2016</div>
    <div class='signup'>Sign Up</div>
    <div class='login'>Login</div>
  </div>
</div>
```

With nothing:

<div class='menu-container_fb_ex_1'>
<div class='menu_fb_ex0'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>

Now adding `display: flex;` for the `menu-container` class results in:

<div class='menu-container_fb_ex_2'>
<div class='menu_fb_ex0'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>


In some browsers this causes the content to be horizontal, and in others there is no difference at all. We haven't given any instructions for how to display the content, so we need to give it some more properties. Setting `justify-content: center;` in the `menu-container` class gives us:


<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex0'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>

It is now centered. We can now do this for the `menu` class, adding `display: flex;` and `justify-content: space-around;` to its CSS rule:

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex1'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>

And then we change our item `menu` rule to `justify-content: space-around;`

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex2'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>

which results in an automatic distribution of the items horizontally. Another option is to use the `justify-content: space-between;`{.css} value:

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex3'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>

### Grouping Flex Items

Flex containers only use their immediate child elements in spacing, which means you can use groupings to great advantage:

```html
<div class='menu'>
  <div class='date'>Aug 14, 2016</div>
  <div class='links'>
    <div class='signup'>Sign Up</div>      <!-- This is nested now -->
    <div class='login'>Login</div>         <!-- This one too! -->
  </div>
</div>
```

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex3'>
<div class='date'>Aug 14, 2016</div>
<div class='links_fb_ex1'>
<div class='signup'>Sign Up</div>
<div class='login_fb_ex1'>Login</div>
</div>
</div>
</div>

We can then make `links` a flex container as well to get a horizontal layout:

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex3'>
<div class='date'>Aug 14, 2016</div>
<div class='links_fb_ex2'>
<div class='signup'>Sign Up</div>
<div class='login_fb_ex1'>Login</div>
</div>
</div>
</div>

## Vertical alignment

Flex containers can define vertical alighnments as well as horizontal ones, which is the first bit of functionality that we can do with flexbox that we could never have done with floats. Adding the below code to our menu code will allow us to explore vertically aligning content:

```html}
<div class='header-container'>
  <div class='header'>
    <div class='subscribe'>Subscribe &#9662;</div>
    <div class='logo'><img src='images/awesome-logo.svg'/></div>
    <div class='social'><img src='images/social-icons.svg'/></div>
  </div>
</div>
```

We also give the `header-container` and `header` classes some properties:

```css
.header-container {
  color: #5995DA;
  background-color: #D6E9FE;
  display: flex;
  justify-content: center;
}

.header {
  width: 900px;
  height: 300px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

The `.header-container` has the `flex` display property and is justified in the center, which ensures all its child elements are centered on the page. The `header` is also a flexbox, but its content is justified `space-between` meaning it is roughly spread out over the width of `header`. It also has the property `align-items` as `center`, which means it vertically aligns its items in the center.

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex2'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>
<div class='header-container_fb_ex'>
<div class='header_fb_ex'>
<div class='subscribe'>Subscribe &#9662;</div>
<div class='logo'><img src='flexbox/images/awesome-logo.svg'/></div>
<div class='social'><img src='flexbox/images/social-icons.svg'/></div>
</div>
</div>

The `align-items` property has very similar options to `justify-content`, but also includes `stretch` and `baseline`. The `stretch` option allows the creation of columns of equal height, which can be quite difficult with floats. 

## Wrapping Flex Items

Items can be wrapped to stay within the horizontal limits of the page using flexbox with the `flex-wrap` property. For example, we can create a row of images, and set the container `flex-wrap: wrap;`:

```css
.photo-grid-container {
  display: flex;
  justify-content: center;
}

.photo-grid {
  width: 900px;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}

.photo-grid-item {
  border: 1px solid #fff;
  width: 300px;
  height: 300px;
}
```

```html
<div class='menu-container'>
  <div class='menu'>
    <div class='date'>Aug 14, 2016</div>
    <div class='signup'>Sign Up</div>
    <div class='login'>Login</div>
  </div>
</div>
<div class='header-container'>
  <div class='header'>
    <div class='subscribe'>Subscribe &#9662;</div>
    <div class='logo'><img src='images/awesome-logo.svg'/></div>
    <div class='social'><img src='images/social-icons.svg'/></div>
  </div>
</div>
<div class='photo-grid-container'>
  <div class='photo-grid'>
    <div class='photo-grid-item first-item'>
      <img src='images/one.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/two.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/three.svg'/>
    </div>
    <div class='photo-grid-item'>
      <img src='images/four.svg'/>
    </div>
    <div class='photo-grid-item last-item'>
      <img src='images/five.svg'/>
    </div>
  </div>
</div>
```

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex2'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>
<div class='header-container_fb_ex'>
<div class='header_fb_ex'>
<div class='subscribe'>Subscribe &#9662;</div>
<div class='logo'><img src='flexbox/images/awesome-logo.svg'/></div>
<div class='social'><img src='flexbox/images/social-icons.svg'/></div>
</div>
</div>
<div class='photo-grid-container_fb_ex1'>
<div class='photo-grid_fb_ex1'>
<div class='photo-grid-item first-item_fb_ex1'>
<img src='flexbox/images/one.svg'/>
</div>
<div class='photo-grid-item_fb_ex1'>
<img src='flexbox/images/two.svg'/>
</div>
<div class='photo-grid-item_fb_ex1'>
<img src='flexbox/images/three.svg'/>
</div>
<div class='photo-grid-item_fb_ex1'>
<img src='flexbox/images/four.svg'/>
</div>
<div class='photo-grid-item_fb_ex1 last-item_fb_ex1'>
<img src='flexbox/images/five.svg'/>
</div>
</div>
</div>

## Flex Direction

Flex containers can render their items horizontally or vertically. To render items vertically, we can set the container's `flex-direction` to `column`:

```css
.photo-grid {
  width: 900px;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  justify-content: center;
  flex-direction: column;
}
```

<div class='menu-container_fb_ex_3'>
<div class='menu_fb_ex2'>
<div class='date'>Aug 14, 2016</div>
<div class='signup'>Sign Up</div>
<div class='login'>Login</div>
</div>
</div>
<div class='header-container_fb_ex'>
<div class='header_fb_ex'>
<div class='subscribe'>Subscribe &#9662;</div>
<div class='logo'><img src='flexbox/images/awesome-logo.svg'/></div>
<div class='social'><img src='flexbox/images/social-icons.svg'/></div>
</div>
</div>
<div class='photo-grid-container_fb_ex1'>
<div class='photo-grid_fb_ex2'>
<div class='photo-grid-item first-item_fb_ex1'>
<img src='flexbox/images/one.svg'/>
</div>
<div class='photo-grid-item_fb_ex1'>
<img src='flexbox/images/two.svg'/>
</div>
<div class='photo-grid-item_fb_ex1'>
<img src='flexbox/images/three.svg'/>
</div>
<div class='photo-grid-item_fb_ex1'>
<img src='flexbox/images/four.svg'/>
</div>
<div class='photo-grid-item_fb_ex1 last-item_fb_ex1'>
<img src='flexbox/images/five.svg'/>
</div>
</div>
</div>


This ability to change the direction comes in very handy when we need to have *responsive design*, which is when the page displays differently depending on the device that it is being viewed on. Mobile phones tend to view pages in a single column, whereas on larger screens webpages are in a stacked horizontal layout.

Changing the `flex-direction` also affects the way that the `justify-content` property is read by the browser. When `flex-direction=column` then `justify-content` specifies the vertical alignment rather than the horizontal alignment. Instead we use the `align-items` property. So `justify-content` specifies the alignment in the flex-direction, and `align-items` specifies the alignment in the other direction.

## Flex Container Order

So far it is the HTML code order alone which decides the direction and order in which elements are displayed on a page. With Flexbox, you can specify the items in a flex container to be displayed in reverse order by using `flex-direction=row-reverse` or `flex-direction=column-reverse`. When using the row-reverse direction, the order is only changed on a by-row basis, so if there are multiple rows then the items will be displayed on the same way as if it was simple row direction, but each row's order of items would change.

This is great! It gives us alot of power to display items in a logical and aesthetic way. However, we should remember that content and presentation should always be separated, and the HTML should still make sense without having to actually apply the CSS.

## Flex Item Order

You can add an `order` value to flex items in order to control the order in which they appear. Items with a higher order appear after those with a lower order value. The default value is `0`. For example, you can force the first item to appear last:

```css
.first-item {
  order: 1;
}
```

This order works accross rows and columns, unlike the flex-direction options.

## Item Alignment

We can use flex to align single items as well as entire containers. For example, we can move the "Subscribe" and social media buttons to the bottom of the header:

```css
.social,
.subscribe {
  align-self: flex-end;
  margin-bottom: 20px;
}
```

<div class='header-container_fb_ex'>
<div class='header_fb_ex'>
<div class='subscribe_fb_ex3'>Subscribe &#9662;</div>
<div class='logo'><img src='flexbox/images/awesome-logo.svg'/></div>
<div class='social_fb_ex3'><img src='flexbox/images/social-icons.svg'/></div>
</div>
</div>

Notice we are using the `align-self` rather than `align-items` property. These properties take the same values, but act on items and containers respectively.

## Flexible Items

So far we have seen how to position boxes, and their dimensions have largely been determined by their contents and their containers. However, we can finetune this easily. Items have a `flex` property, which takes a numerical value with a default of 1. The `flex` value tells the browser how much the item should grow as the container size increases. So if an items flex value is 2, then it will grow twice as large as an item with `flex` value 1. For example we can add some footer items:

```html
<div class='footer'>
  <div class='footer-item footer-one'></div>
  <div class='footer-item footer-two'></div>
  <div class='footer-item footer-three'></div>
</div>
```

with CSS:

```css
.footer {
  display: flex;
  justify-content: space-between;
}

.footer-item {
  border: 1px solid #fff;
  background-color: #D6E9FE;
  height: 200px;
  flex: 1;
}
```

<div class='footer_fb_ex4'>
<div class='footer-item_fb_ex4'></div>
<div class='footer-item_fb_ex4y'></div>
<div class='footer-item_fb_ex4'></div>
</div>

and then set the `flex` for the third item to be 2:

```css
.footer-three {
  flex: 2;
}
```

<div class='footer_fb_ex4'>
<div class='footer-item_fb_ex4'></div>
<div class='footer-item_fb_ex4'></div>
<div class='footer-item_fb_ex4 footer-three_fb_ex4'></div>
</div>

We can also combine flexible width items with static width ones. For example, we can set the first and last footer items to be a particular with, and the middle one will fill up the space flexibly:

```css
.footer-one,
.footer-three {
  background-color: #5995DA;
  flex: initial;
  width: 300px;
}
```

Note that the `flex` property is given the value "`initial`", which resets the `flex` value. This is required because otherwise the items would inherit the `flex` value of 1 from the class rule for `footer-item`. When `flex` is set, the `width` value is ignored, hence the need to reset it.

<div class='footer_fb_ex4'>
<div class='footer-item_fb_ex4 footer-one_fb_ex4'></div>
<div class='footer-item_fb_ex4 footer-two_fb_ex4'></div>
<div class='footer-item_fb_ex4 footer-three_fb_ex5'></div>
</div>

## Summary

Flexbox gives you so much more flexibility than the old, janky floats of the previous era in web design. However, it is actually the easy part of web design. The harder part is writting the HTML CSS to get the desired layout. The first step should always be to get a pen and paper, and sketch out the boxes, then work out the behaviour of the boxes. Once you have worked out those details, flexbox makes that translation from concept to CSS easily.

# Advanced Positioning

So far we have been working on "Static Positioning", however there are three other types: relative, absolute, and fixed. Each of these allow you to position objects specifically using coordinates, rather than semantically, as with flexbox. The majority of elements on a webpage should still be laid out according to a static flow, but advanced positioning schemes allow us to tweak positions of particular components and allow for more complex scenarios such as animation or menus.

### Setup

The examples for this section are given in the directory `advanced-positioning`.

## Positioned elements

A CSS property we have not seen until now is the `position` property for an element. The default value for this is `static`, and when it is *not* static the element is called a "positioned element". We start with three basic elements:

```html
<div class='container'>
  <div class='example relative'>
    <div class='item'><img src='images/static.svg' /></div>
    <div class='item'><img src='images/static.svg' /></div>
    <div class='item'><img src='images/static.svg' /></div>
  </div>
</div>
```

with CSS:

```css
.container {
  display: flex;
  justify-content: center;
}

.example {
  display: flex;
  justify-content: space-around;
  width: 800px;
  margin: 50px 0;
  background-color: #D6E9FE;
}

.item img {
  display: block;
}
```

<div class='container_ap_ex1'>
<div class='example_ap_ex1'>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
</div>
</div>


### Relative Positioning

A relative positioning means that an element is positioned relative to where they would normally appear if they were a static element. We convert the middle element into a relative element:

```html
<div class='item item-relative'><img src='images/relative.svg' /></div>
```

```css
.item-relative {
  position: relative;
  top: 30px;
  left: 30px;
}
```

<div class='container_ap_ex1'>
<div class='example_ap_ex1'>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1 item-relative_ap_ex1'><img src='advanced-positioning/images/relative.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
</div>
</div>

The `top` and `left` property values allow us to offset the position down and to the right (counter-intuitive I know!). There are also `bottom` and `right` properties which behave in a similar way.

### Absolute Positioning

Absolute positioning is similar to relative positioning, but it is relative to the entire browser window instead of the original static position of the element. We won't demonstrate this here, but instead show how absolute can be used to place an element relative to its container. In order to do this, we need to change the `example` container element to have `position: relative;`.

```html
<div class='container'>
  <div class='example absolute'>
    <div class='item'><img src='advanced-positioning/images/static.svg' /></div>
    <div class='item item-absolute'><img src='advanced-positioning/images/absolute.svg' /></div>
    <div class='item'><img src='advanced-positioning/images/static.svg' /></div>
  </div>
</div>
```

```css
.absolute {
  position: relative;
}

.item-absolute {
  position: absolute;
  top: 10px;
  left: 10px;
}
```

<div class='container_ap_ex1'>
<div class='example_ap_ex1 absolute_ap_ex1'>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1 item-absolute_ap_ex1'><img src='advanced-positioning/images/absolute.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
</div>
</div>

The reason we need to give the containing element a `position` value is that an absolute item will position itself relative to the closest ancestor that is positioned (i.e. not static). If all of its ancestors are static, then the element is positioned relative to the entire webpage (not very useful!).

Another thing to note is that whether a position is relative or absolute affects the flow of the page. If, for example, the `justify-content` property is changed to `flex-start` for the `example` class, then there is still space left for the relative element: 

<div class='container_ap_ex1'>
<div class='example_ap_ex2'>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1 item-relative_ap_ex1'><img src='advanced-positioning/images/relative.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
</div>
</div>

On the other hand, for the absolute element, it is completely removed from the flow of the page:

<div class='container_ap_ex1'>
<div class='example_ap_ex2 absolute_ap_ex1'>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1 item-absolute_ap_ex1'><img src='advanced-positioning/images/absolute.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
</div>
</div>

### Fixed Positioning

Fixed positioning means that the element is positioned relative to the browser window, not the page, meaning that it doesn't disappear or move when scrolling. An example below shows an item that would be fixed at the bottom right of the page:

```css
.item-fixed {
  position: fixed;
  bottom: 0;
  right: 0;
}
```

## Positioning Elements in Animation

The following is slightly out of scope for the section, but animation is a very common use of relative and absolute positioning. The following JavaScript code makes the element jump around:

```js
    <script>
  var left = 0;

  function frame() {
    var element = document.querySelector('.item-relative');
    if(left == 0){
      left = left + 1;
    }
    left = 200 * (3.2 * left/200 * (1-left/200));
    element.style.left = left + 'px';
    if (left >= 300) {
      clearInterval(id)
    }
  }

  var id = setInterval(frame, 1000)
  </script>
```

<div class='container_ap_ex1'>
<div class='example_ap_ex1'>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
<div class='item_ap_ex1 item-relative_ap_ex2'><img src='advanced-positioning/images/relative.svg' /></div>
<div class='item_ap_ex1'><img src='advanced-positioning/images/static.svg' /></div>
</div>
</div>


<script>
var left = 0;

function frame() {
var element = document.querySelector('.item-relative_ap_ex2');
if(left == 0){
left = left + 1;
}
left = 200 * (3.2 * left/200 * (1-left/200));
element.style.left = left + 'px';
if (left >= 300) {
clearInterval(id)
}
}

var id = setInterval(frame, 1000)
</script>

<!---End Document--->

</div>
</div>
</div>
</div>
