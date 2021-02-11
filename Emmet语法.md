# Emmet语法

## Nesting operators

### Child: `>`

To nest elements inside each other

```html
div>ul>li
```

### Sibling: `+`

To place elements near each other, on the same level

```html
div+p
```

### Climb-up: `^`

With `>` operator you’re descending down the generated tree and positions of all sibling elements will be resolved against the most deepest element

```html
div+div>p>span+em
<div></div>
<div>
    <p><span></span><em></em></p>
</div>
```

you can climb one level up the tree and change context where following elements should appear

```html
div+div>p>span+em^bq
<div></div>
<div>
    <p><span></span><em></em></p>
    <blockquote></blockquote>
</div>
```

You can use as many `^` operators as you like, each operator will move one level up

```html
div+div>p>span+em^^^bq
```

### Multiplication: `*`

Define how many times element should be outputted

```html
ul>li*5
```

### Grouping: `()`

Parenthesises are used by Emmets’ power users for grouping subtrees in complex abbreviations

```html
div>(header>ul>li*2>a)+footer>p
```

## Attribute operators

### ID and CLASS

In CSS, you use `elem#id` and `elem.class` notation to reach the elements with specified `id` or `class` attributes

#### ID: `#`

#### CLASS: '.'

```html
div#header+div.page+div#footer.class1.class2.class3
```

### Custom attributes: `[]`

You can use `[attr]` notation (as in CSS) to add custom attributes to your element

```html
td[title="Hello world!" colspan=3]
```

### Item numbering: `$`

With multiplication `*` operator you can repeat elements, but with `$` you can *number* them. Place `$` operator inside element’s name, attribute’s name or attribute’s value to output current number of repeated element

```html
ul>li.item$*5
```

You can use multiple `$` in a row **to pad number with zeroes**

```html
ul>li.item$$$*5
```

#### Changing numbering base and direction: `@`

With `@` modifier, you can change **numbering direction** (ascending or descending) and **base** (e.g. start value)

For example, to change direction, add `@-` after `$`

```html
ul>li.item$@-*5
```

To change counter base value, add `@N` modifier to `$`

```html
ul>li.item$@3*5
ul>li.item$@-3*5
```

## Text: `{}`

You can use curly braces to add text to element

```html
a{Click me}
```

Note that `{text}` is used and parsed as a separate element (like, `div`, `p` etc.)  but has a special meaning when written right after element

For example, `a{click}` and `a>{click}` will produce the same output, but `a{click}+b{here}` and `a>{click}+b{here}` won’t



*注：don't use spaces between elements and operators, because space is a stop symbol where Emmet stops abbreviation parsing*

## 参考：

<https://docs.emmet.io/abbreviations/syntax/>