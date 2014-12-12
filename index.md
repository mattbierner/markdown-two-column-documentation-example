---
layout: base
---

# Responsive, Two Column Documentation Layout With Markdown and CSS

Markdown makes it easy to write and maintain documentation, but is normally limited to single column layouts. For documenting code, and on larger screens particularly, single column layouts do not utilize space well and separate explanatory text too much from code samples:

This page documents how to use plain old Markdown and CSS to achieve a responsive, two column layout, with code examples their explanations appear next to each other. It targets code documentation, but can easily be adapted to other contexts as well.

For maximum metaness, the page itself uses the two column layout it documents. More complete examples are demonstrated on the [Bennu][bennu] and [Nu][nu] project sites.

Checkout the complete code on [github][src]. It uses [Jekyll](http://jekyllrb.com). Simply run: `$ jekyll build` to build it.

<div class="begin-examples"></div>

## The Markdown
We'll abuse some Markdown elements to get the layout we want. You can choose to style your page differently, but here we'll have code examples on the right, and code explanations on the left.

### First, we need to tell Markdown where the two column layout begins.
Anything before this element will be rendered normally.

```
<div class="begin-examples"></div>
```

And we should also tell it where the two column layout ends.

```
<div class="end-examples"></div>
```

### `h2` will be an example section header.

```
## Section title
```

And any text directly after the section title will not be split into two columns.

```
## Section title
This text, along with the title, remains in a single column
```

### Each point in a section starts with an `h3`.

```
### Main you want to make point here
```

### Normal text elements (`p`) are used for more detailed explanations. 
You can put them after the main point.

``` 
### Main point
Some explanatory text.
```

### Code is interleaved with explanatory text.

The main point or explanation for a piece of code should come directly before it.

    ### Main point about code block 1

    ```
    code block 1
    ```

    More text explaining code block 2

    ```
    code block 2
    ```

## Styling
We can use CSS to style the Markdown output to create a two column layout when readers view our page on a larger screen.

### The main section and subsection headings both take up the entire width of the page.

```
article .begin-examples ~ h2,
article .begin-examples ~ h2 + p {
    width: 100%;
    clear: both;
}
```

### Each column element is 50% width

```
article .begin-examples ~ h3,
article .begin-examples ~ p,
article .begin-examples ~ .highlight {
    width: 50%;
}
```

### The left column has the main point and explanation text (`h3` and `p`).
We'll add some padding here too for good measure.

```
article .begin-examples ~ h3,
article .begin-examples ~ p {
    float: left;
    box-sizing: border-box;
    padding-right: 1rem;
    clear: both;
}
```

### While the right column has only the code examples `.highlight`.
And some spacing between the sections.

```
article .begin-examples ~ .highlight {
    float: right;
    clear: right;
    margin-bottom: 1rem;
}
```

### That's it!
But we have to ensure that nothing goes past the end of content.

```
.end-examples {
    clear: both;
}
```

### But we should clean up after ourselves.
Reset the styles to stop the two column layout. This must come after all the other styles in the CSS file.

```
article .end-examples ~ p,
article .end-examples ~ h3,
article .end-examples ~ .highlight {
    width: auto;
    float: none;
    clear: none;
}
```


## Style For Small Screens
Using a media query on screens less that 580px in width, we'll create a single column layout again. 

### All you have to do is reset the styling on the main elements of the two column layout

```
article .begin-examples ~ h3,
article .begin-examples ~ p,
article .begin-examples ~ .highlight {
    width: 100%;
    float: none;
    clear: none;
}
```

<div class="end-examples"></div>

# Conclusion
This example and the [source][src] intentionally keep any other fancy styling to a minimum, but it is very easy to style the two column layout. For styles that only apply inside the layout, add styles for `.begin-examples ~ * { }` and then reset them with `.end-examples ~ * { }`.



[Nu]: http://mattbierner.github.io/nu/
[bennu]: http://bennu-js.com

[src]: https://github.com/mattbierner/markdown-two-column-documentation-example
