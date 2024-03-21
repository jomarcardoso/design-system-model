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

One more layer may be seen like an overkill, but to your product is one more layer of patterns. One of the great benefits is when your stacks of components fail but your design system has this tokens to equalize the implementations of component patterns anywhere.

> You will never attend 100% well of your user, so allow them to self attend.

I am going to give you some examples of ways to render HTML that I had to work with:

- email with Apache Velocity
- Google AMP
- VTEX
- SSR with Pug

your component can partially attend and your client still need patterns to continue and do not need to ask you featured 

I would not assume that my components will serve everyone every time.

If your project has several stacks of components, and it is necessary to change an aspect of one of them, without the layer of component tokens, it will be necessary to create a task to each team to change to the value, and having this layer is only necessary edit in there. The maintenance is centered and follows the Single Responsibility Principle of the SOLID, that says, "There should never be more than one reason for a class to change", in other words, your component has its aspects of the technology and not the responsibility of the common characteristics of the design system. This centered information becomes greater if you consider that users not attended by the componets of the design system but still have this values to make themselves and following the same patterns.

## New features

The plannning of a new feature do not necessaraly have to consider the limitation of the technologies that the will be impelmented. Material Design brings a good example of non conventional shapes que could not be make with CSS or it will need to bust a gut to do it. For Material Design the ideas of motion, shapes and everthing else is limited by creativity and it will be implementeded if possible, this approach is called "Gracefull Degradation", the planning aim the perfect but the limitation of technology, will cut some features off if necessary.  

![https://m2.material.io/design/shape/about-shape.html#shaping-material](https://github.com/jomarcardoso/design-system-model/assets/27368585/d2edf425-cedc-4b25-b00f-7df0fbb64f3c)

The other approach is more close to the technologies, 

### Graceful degradation

Graceful degradation is a great approach that allow the design system to scale with no barriers of the technology. Some user clients like Outlook, smart devices and old smartphones softwares would not influence the conception of the feature. The flow of planning is independent of further implemenetations. Libraries like Material UI and Angular Material are examples of developmenet of the the Material Design and both of them does not brings that impossible features for web like negative corner radius. Every stack of technology has to adapt that ideal feature to its technology and both stacks, definition and technology, run separately.

The necessity of this approach comes when some of these arguments show up:

- All stack have to get together to identify all limitations
- The stack of definition is not happy cutting features off
- The design will have other technologies furthuer
- The aim techonologies are evolving fast and frequently is needed to revisit the feature planning
- When the team of definition and technology are not of the same company structure and do not talk each other

For robust and growing Design Systems the Graceful degradation methodology is very recommended since the product can evolve and the technology will follow now what is possible and get better when possible, whether by an update or the decision to cut this limitation off, the Internet Explorer is a great recent example (consider was wrote in 2024).

Bellow as idea of flux of development of a new features:

1. Designers plan the ideal feature
2. All specialists get together to bring information about cares, not the limitations, but the accessibility, user experience, SEO ideal and so on
3. Developers build with the technology limitation

## Progressive enchancement

The Progressive Enchancement is a way simple approach that is focused to the technology like a product. We can see this method in libraries like Bootstrap, that the design and code are in the same place. The limitation of the technology will sometimes makes necessary to change the structure and in some cases the visual. Botstrap, for instance for many years have been made its grid with `float` CSS, because some browsers have not implemented the flexbox features.

Another way to use the Progressive Enchacement is combined with Graceful Degradation. When it is necessary to have support for a very limited technology the project can start with common features, but at the breakpoint split the methods and the limited technology has his own planning of features based in their limitations and can be improved if has a new techology update or the team find a workaround to get closer to the main Project. Below how was the Youtube on Internet Explorer that show exactly how the Progressive Enchancement works; There is a common base of backend data, url, but the rendered pages are not the same. They decided to not create with all features and remove what does not works on IE. For other browsers, pages with more updated features could be made and then apply Graceful Degradation.

![Youtube on Internet Explorer](https://github.com/jomarcardoso/design-system-model/assets/27368585/82d5ddfe-0aea-4939-8ab0-d2c9a9674865 "source: https://news.softpedia.com/news/YouTube-No-Longer-Working-for-Some-Internet-Explorer-11-Users-401553.shtml")

The steps of planning and developement with progressive enchancement are:

1. All stacks get together and plan the minimum of the component
2. Developers build as planned
3. Revisit this component to improve it
