# CSS Styleguide
Exploring CSS techniques and best practices in hopes of landing on a styleguide.

## Inspirations

This styleguide has been inspired by the following:

- [SUITCSS](https://suitcss.github.io/)
- [RSCSS](https://github.com/rstacruz/rscss)

## The Future

I would like to explore the area of js powered css, particularly [css-modules](https://github.com/css-modules/css-modules) in which css is finally modular and composable! The following rules are likely to evolve as this becomes a more stable part of the workflow, eliminating the need for namespaceing etc. In the meatime, these are a set of rules that I have latched on to. 

## Some loose rules during exploration

- Avoid nested rules unless defining a modifier; try to keep your stylesheets as flat as possible as to avoid cascading issues. There may be certain circumstances where nesting may prove useful (we'll explore this)
- Do not use IDs to style elements, only classes. Following this combats specificity issues.
- Do not style naked element tags (i.e. `p`, `ul`) unless used for styling baseline layout setup. If not, use classes.

### Utilities

Utilities are those that can be applied to any element and produce expected results. These can be thought of as 'helper classes' that are there at your disposal. **All utility classes begin with a `u-` and named with a camel-cased descriptor**.

**Note**: Utilities should be thought of as idempodent css "functions". Often, an `!important` declaration is perfectly reasonable.

```css
/* format */
.u-utilityName {}

/* example */
.u-centered { text-align: center !important }
.u-headline { font-size: 3rem !important; text-align: center !important; }
.u-unstyledList { list-style: none !important; }
```

### Modifiers

Modifiers provide additional styling to an already-defined class. **They cannot stand alone** and are dependent on the styling that they are attached to. To denote this relationship, **all modifier classes begin with a `-` (hypen)**.

```css
/* format */
.-modifier-name {}

/* example */
.u-headline { font-size: 3rem !important; text-align: center !important; }
/* define a 'showtime' modifier for this utility class */
.u-headline.-showtime { text-transform: uppercase; }
```

Example HTML snippet:

```html
<h2 class"title -showtime">It&rsquo;s showtime!</h2>
```

**Note:** Since `.-showtime` is defined as a modifier of `.title`, we can still define another `.-showtime` modifier on another class without clobbering styles. This reinforces the notion that modifiers are dependent, relying on some preceding style declarations.

**Caveat/Edge Case:** There does exist an unfortunate edge case in which multiple classes could each define their own modifier of the same name. **AND**, for some unlikely reason, both the classes are used together on the same element, the modifier will be applied to both classes, when perhaps the author intended it to be applied to a single class.

### Components

A component is a cohesive group of markup that combines to create a functional piece of the UI. **Components are denoted with a Pascal-cased name**. This name is comprised of more than one word. For example, instead of `Searchbar`, try `SearchBar`. This name is used to namespace its descendants. **Descendant class names are prefixed with the capital letters of the component. (i.e. component: SearchBar -- descendants: sb-classname)**

```css
/* format */
.ComponentName {}

/* example */
.GlobalFooter { padding: 2rem 5%; }
/* we use the prefix 'gf' from GlobalFooter to namespace descendants */
.gf-title { color: red; }
.gf-logo { float: left; }
```

An example HTML snippet could look like the following:

```html
<footer class="GlobalFooter">
  <h6 class="gf-title u-headline -showtime">footer</h6>
  <img src="/path/to/logo" class="gf-logo">
</footer>
```

**Question:** What happens when there's multiple `gf` namespaces?
