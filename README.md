# CSS notes with Jupyter notebooks

This is a Proof of Concept repository for taking CSS notes using [Jupyter Notebook](https://jupyter.org/).

I created it because:
- I'm experimenting with CSS a lot and I'd like to have an accessible and readable step-by-step record of it
- when I write blog posts about CSS, I have to juggle a lot of phases of the code and rename CSS classes so
    that they're being properly applied to elements I'm working with - abstracting it away in a Jupyter notebook
    helps me focus on the CSS code
- Jupyter notebooks are easily shareable and can be used as explorable explanations without much effort
- it allows for building the CSS programatically, which helps with creating complex patterns

## Prerequisites

You need to install [Jupyter notebook](https://jupyter.org/install) and run it in this directory.

## How to use this code

If you want to create a new notebook with this setup, you just need to copy the first cell of the `Example.ipynb`
file. All the other cells in that notebook are examples.

Core functions in this code are:
- `render_html()` - using the iPython `display` module, it renders a single `div` with provided HTMl and class name
- `render()` - using the iPython `display` module, it outputs the provided CSS as a Markdown code block and calls
    `render_html()`

1. Writing CSS
Write the CSS as a multiline string without curly brackets or class name, and assign it to a variable.

```Python
css = '''
    background-color: red;
    height: 100px;
    width: 200px;
'''
```

2. Displaying elements
To display an element with the CSS applied, call `render_html()` and provide it the CSS, class name and element number (n).
Element number is added to the CSS class, so that the notebook can display multiple different divs with similar class
names and different CSS at the same time. If no element number is provided, none will be appended.

Examples:
```
render_html(css, 'box', 1)
render_html(css, 'zigzag')
```

3. Exporting to Markdown
For the purpose of writing blog posts, for each element I want to export:
- the CSS applied to the element as a code block
- the `<style>` tag for the element
- the `<div>` element with appropriate CSS class applied

This is achieved through `render()`, e.g.:
```
render(css, 'box', 1)
```

Following [this answer](https://stackoverflow.com/questions/34818723/export-notebook-to-pdf-without-code/45029786#45029786)
on StackOverflow, I created a stripped-down template for exporting the notebook (`./hidecode.tpl`), so I can directly use 
the Markdown file on my blog (I use a Jekyll setup for the blog posts).

Place the template file and your notebook in the same directory and run:
```
jupyter nbconvert --to markdown --template hidecode <notebook_name>.ipynb
```

This will create a Markdown file `<notebook_name>.md`. Any code cells in the notebook will be omitted, but all the other cell
types (e.g. Markdown, SVG, PNG, HTML) will be preserved in the output.

## Potential improvements

1. Working with more DOM elements - it's currently not my use-case, as I mostly work with CSS in a single `div`, but it might
    be useful in the future
2. Passing custom HTML to the `render()` and `render_html()` functions