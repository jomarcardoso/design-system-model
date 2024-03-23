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

Here is defined all about the brand definitions and usually is the first page of a design system documentation. This languange is the minimum of a design system, there is not much control and no patterns to follow, but a start of a visual identity. The names in this level are not semantic because the role of this step is bring the basic information of the brand to be or not used afterward. There are some basic values that is in this layer:

- Palette colors: orange, blue, green.
- Fonts: Tahoma, Arial, Verdana.
- Text sizes: 42px, 22px, 14px.
- Corner radius: 5px, 2px.

The list can go on with all brand definitions such as writing style, borders, shapes... 

It is primordial the Language layer be well documented with all this patterns and what is expect for the brand. In the Material Design I see this step with their definition of what they call "material", and how it looks like and how the "materials" respond to users interactions.

### Patterns

Patterns are the values of the language with a semantic load and even composition of language values. In the language level is defined the yellow color, but here this color can be used with the meaning of an alert color.

- primary color
- secondary color
- main title font (size + family + weight)

## Tokens stack

The tokens stacks is necessary for cross technologies work with the same values. Libraries like Amazon Style Dictionary will help to make it easy. In this project is defined the variables in JSON files or something similar and the key values of this settings will be parsed to respective configured destination formats like SASS, Kotlin, iOS...

### Variables

All basic definitions will be in variables. It could be many predefined variables that not exacly will be used in the components yet. Here can have a palette of gray tons that will be defined for a possbile use. This layer represent in code what has in the Language of the Definition Stack.

Being raw values to possible use, it is not recommend that this variables comes up to the final users. It has to be used only to fill up the next level of tokens. 

```json
{
  "orange": "#FF8C00",
  "red": "#DC143C"
}
```

```scss
$orange: #FF8C00;
$red: #DC143C;
```

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

## New Features

The planning of a new feature does not necessarily have to consider the limitations of the technologies that will be implemented. Material Design provides a good example of unconventional shapes that cannot be easily achieved with CSS alone. For Material Design, ideas such as motion, shapes, and everything else are limited only by creativity and are implemented if possible. This approach is called "Graceful Degradation," where the initial planning aims for perfection but acknowledges technological limitations that may require certain features to be omitted.

![Material Design Shapes](https://m2.material.io/design/shape/about-shape.html#shaping-material)

The other approach is more closely related to the technologies.

### Graceful Degradation

Graceful degradation is a great approach that allows the design system to scale without barriers of technology. User clients like Outlook, smart devices, and old smartphone software would not influence the conception of the feature The planning flow is independent of further implementations. Libraries like Material UI and Angular Material are examples of development of Material Design, and both of them do not bring impossible features for the web, such as negative corner radius. Every stack of technology has to adapt that ideal feature to its technology, and both stacks, definition and technology, run separately.

> When an updated version of a browser or operating system is released, new features are often included to keep pace with the latest enhancements to internet standards and other technologies.

The necessity of this approach arises when some of these arguments show up:

- All stacks have to come together to identify all limitations.
- The stack of definition is not happy cutting features off.
- There will be more technologies implementing that feature further.
- The aim technologies are evolving fast, and frequent revisits to the feature planning are needed.
- When the team of definition and technology are not of the same company structure and do not communicate with each other.

For robust and growing design systems, the graceful degradation methodology is highly recommended since the product can evolve, and the technology will follow as possible and get better when possible, whether by an update or the decision to cut off this limitation. Internet Explorer is a recent example (considering this was written in 2024).

Below is an idea of the development flow for new features:

1. The graceful degradation approach starts by designing the application to deliver the functionality necessary to meet the needs of users on modern. [TechTarget](https://www.techtarget.com/searchnetworking/definition/graceful-degradation#:~:text=Graceful%20degradation%20is%20the%20ability,is%20to%20prevent%20catastrophic%20failure.)
2. All specialists come together to bring information about concerns, not limitations, but accessibility, user experience, SEO ideals, and so on.
3. Developers build with the technology limitation.

Since the releases of technology stacks are not tied to design, it can be splited in smaller features. The development can use other method like Progressive Enhancement  

### Progressive Enhancement

Progressive Enhancement is a simple approach that focuses on technology as a product. We can see this method in libraries like Bootstrap, where the design and code are in the same place. The limitations of the technology will sometimes make it necessary to change the structure and, in some cases, the visual. For example, Bootstrap has used `float` CSS for its grid for many years because some browsers did not implement the flexbox features.

Another way to use Progressive Enhancement is combined with Graceful Degradation. When it is necessary to support a very limited technology, the project can start with common features, but at the breakpoint, split the methods, and the limited technology has its own planning of features based on its limitations and can be improved if there is a new technology update or if the team finds a workaround to get closer to the main project. 

> Instead of starting with the advanced features supported on modern browsers, progressive enhancement starts with the most basic features supported on all browsers. The developer than adds the more advanced features, which are automatically available when the user accesses the application through a modern browser.

Below is an example of how YouTube was on Internet Explorer, showing exactly how Progressive Enhancement works. There is a common base of backend data, URL, but the rendered pages are not the same. They decided not to create all features and remove what does not work on IE. For other browsers, pages with more updated features could be made and then apply Graceful Degradation.

![Youtube on Internet Explorer](https://github.com/jomarcardoso/design-system-model/assets/27368585/82d5ddfe-0aea-4939-8ab0-d2c9a9674865 "source: https://news.softpedia.com/news/YouTube-No-Longer-Working-for-Some-Internet-Explorer-11-Users-401553.shtml")

The steps of planning and development with progressive enhancement are:

1. All stacks come together and plan the minimum of the component.
2. Develop as planned.
3. Revisit this component to improve it when the technology limitation is overcome.
