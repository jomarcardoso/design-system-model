# A proposal of a design system model

At my last years I have been working with design systems. I was getting knowledge and following with the minimum of questions. I saw many things that I doubt and want to make better. I consider myself ready to make a proposal of a design system model and structure.

## Stacks and layers

I have splitted in different stacks to facilitate the governance and the organize the the subjects by knowledge of the teams.

| definitions | tokens     | CSS        | React       | SwiftUI     |
|------------ | ---------- | ---------- | ----------- | ----------- |
| language    | base       | reboot     |             |             |
| patterns    | foundation | helpers    |             |             |
| components  | components | components | components  | components  |
| templates   |            |            | composition | composition |

The tokens brings all chacacterists of the design system, since the base unique values, the patterns of foundation values and the layer of the components with all values that any technology needs to make a component following the defined characteristics. The team that manage the tokens are responsible to set the values that will change all the components without the necessity to change anywhere else. The CSS stack is an example of full use of the layers of the tokens.

## Definition stack

Here is where the design system starts, and if you or the company wish can keep only in this stack.

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

I am going to show my web point of view how to organize tokens by themes.

ˋˋˋcss
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
ˋˋˋ










