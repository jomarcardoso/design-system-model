# A proposal of a design system model

At my last years I have been working with design systems. I was getting knowledge and following with the minimum of questions. I saw many things that I doubt and want to make better. I consider myself ready to make a proposal of a design system model and structure.

## Stacks and layers

I have splitted in different stacks to facilitate the governance and the organize the the subjects by knowledge of the teams.

| definitions | tokens     | CSS                 | React       | SwiftUI     |
| ----------- | ---------- | ------------------- | ----------- | ----------- |
| language    | variables  | variables (private) |             |             |
| patterns    | foundation | reboot / helpers    |             |             |
| components  | components | components          | components  | components  |
| templates   |            |                     | composition | composition |

The tokens brings all chacacterists of the design system, since the base unique values, the patterns of foundation values and the layer of the components with all values that any technology needs to make a component following the defined characteristics. The team that manage the tokens are responsible to set the values that will change all the components without the necessity to change anywhere else. The CSS stack is an example of full use of the layers of the tokens.

## Definition stack

Here is where the design system starts, and if you or the company wish can keep only in this stack, working only like a guideline, mainly if the it is a small company, small project or the or the development is done by an outsourced company. As well this stack can work together the tokens stack, whether exists, and the same staff that keep the definition put this in code by the tokens.

### Language

Here is defined all about the brand. This is the minimum of a design system. There is not much control and no patterns to follow, but a start of a visual identity.

- palette colors
- fonts
- text sizes
- writing style
- borders
- corner radius

### Patterns

Patterns are the values of the language with a semantic load and even composition of language values. In the language level is defined the yellow color, but here this color can be used with the meaning of an alert color.

- primary color
- secondary color
- main title font (size + family + weight)

## Tokens stack

The tokens stacks is necessary for cross technologies work with the same values. Libraries like Amazon Style Dictionary will help to make it easy. In this project is defined the variables in JSON files or something similar and the key values of this settings will be parsed to respective configured destination formats like SASS, Kotlin, iOS...

### Variables

All basic definitions will be in variables. It could be many predefined variables that not exacly will be used in the components yet. Here can have a palette of gray tons that will be defined for a possbile use.

I am going to show my web point of view how to organize tokens by themes.

```css
.theme {
  /* base */
  --yellow: gold;
  --blue: darkSlateBlue;

  &.-dark {
    /* base */
    --yellow: khaki;
    --blue: lightBlue;
  }
}

.theme {
  /* foundation */
  --color-primary: var(--blue);
}
```

## CSS stack

The CSS stack is very useful for companies that uses more than one framework or way to render the HTML. For example, if part of the pages of the company are in Vue.js and part as server side rendering with Mustache, you will need common styles and a compiled prefixed CSS is the best way to share this styles. CSS is also good to make simples things like put a class in an element, make a reset of styles or to make available for external projects.

### Variables layer

The layer of variables is optional if the design system already have the tokens stack. The variables layer keeps the unique values, like in tokens and do not show or export this variables to the users, therefore is necessary to use a CSS preprocessor to save this values in private valiables, for example `$blue: #00f` in SASS. The names of the variables are not semantic just because the function is only to hold the values to not repeat in code.

### Foundation layer

...

### components layer

One more layer may be seen like an overkill, but to your product is one more layer of patterns.

> You will never attend 100% well of your user, so allow them to self attend.
