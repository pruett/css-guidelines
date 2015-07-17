# CSS Styleguide
Exploring CSS techniques and best practices in hopes of landing on a styleguide.

## Some loose rules during exploration

- Avoid nested rules unless defining a modifier; try to keep your stylesheets as flat as possible as to avoid cascading issues. There may be certain circumstances where nesting may prove useful (we'll explore this)
- Do not use IDs to style elements, only classes. Following this combats specificity issues.
- Do not style naked element tags (i.e. `p`, `ul`) unless used for styling baseline layout setup. If not, use classes.


### Universal Selectors

Universal selectors are those that can be applied to any element and produce expected results. These can be thought of as 'helper classes' that are there at your disposal. **All universal selector classes begin with a `u_`**.

```css
/* format */
.u_universal-name {}

/* example */
.u_centered { text-align: center; }
.u_headline { font-size: 3rem; font-weight: 600; }
```

### Modifiers

Modifiers provide additional styling to an already-defined class. They cannot stand alone and are dependent on the styling that they are attached to. To denote this relationship, **all modifier classes begin with a `-` (hypen)**.

```css
/* format */
.-modifier-name {}

/* example */
.u_headline { font-size: 3rem; font-weight: 600; }
/* define a modifier on the universal headline property */
.u_headline.-showtime { text-transform: uppercase; }
```

**Note:** Since `.-showtime` is defined as a modifier of `.u_headline`, we can still define another `.-showtime` modifier on another class if the situation should arise down the road.


### Components

A component is a cohesive group of markup that combines to create a functional piece of the UI. **Components are denoted with a `c_` and a Pascal-cased name**. Preferably this name is comprised of more than one word. For example, instead of `.c_Searchbar`, try `.c_SearchBar`. This name is then used to namespace its descendents.   

```css
/* format */
.c_ComponentName

/* example */
.c_GlobalFooter { padding: 2rem 5%; }
/* we use the prefix 'gf' from GlobalFooter to namespace its descendents */
.gf-title { text-transform: uppercase; }
.gf-logo { float: left; }
```

An example HTML snippet could look like the following:

```html
<html>
  <head><title>Title</title></head>
  <body>
    <h1>Hello World!</h1>
    <footer class="c_GlobalFooter">
      <h6 class="gf-title.u_centered">Footer</h6>
      <img src="/path/to/logo" class="gf-logo">
    </footer>
  </body>
</html>
```
