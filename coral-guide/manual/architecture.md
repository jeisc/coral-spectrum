# Architecture

## Web Components

Coral Spectrum hides implementation detail from consumers by leveraging the [Custom Elements v1](https://html.spec.whatwg.org/multipage/custom-elements.html) 
specification, which is part of the emerging [Web Components](https://www.webcomponents.org/introduction) standard.

**Therefore any Coral CSS classes and attributes not explicitly mentioned in the public documentation are private and subject to change. 
Their direct use is not recommended and at high risk of breaking after subsequent updates of Coral Spectrum library.**

Custom elements allow Coral Spectrum to define new types of DOM elements to be used in an HTML document. As a result, Coral Spectrum 
can extend native elements like a button or text input to provide additional functionality or it can provide completely 
new elements like a progress indicator. Consumers can then use these elements using their custom tags (e.g., `<coral-progress>`) 
and directly interact with their custom properties.

A strong advantage Coral Spectrum derives from Custom Elements is the ability to hide many implementation details from the consumer. 
While a progress indicator may be composed of a variety of spans, divs, or images, these are underlying details that shouldn't
concern consumers. Rather than consumers copying and maintaining large swaths of code containing all these elements with their 
various attributes, they are typically able to use a simple Custom Element tag and the underlying elements are seamlessly 
produced by Coral Spectrum on their behalf. By keeping implementation details internal to components, the exposed public API is 
minimized and more explicit resulting in a lower risk of introducing breaking changes. 

For now, we have not implemented Shadow DOM or other aspects of the Web Components specification due to lack of browser 
native support but also polyfill performance issues. 

Custom Elements can be used before their definition is registered. Progressive enhancement is a feature of Custom Elements.
To know when an element or a set of elements becomes defined, you can use `Coral.commons.ready(el, callback)`;

## Content Zones

Without shadow DOM, we need some way to mix user-provided content with presentational elements. Our answer to this is content zones. 
Essentially, we have simple, brainless HTML tags that serve as wrappers for content. 
Users provide these tags when creating elements from markup, and after we render the template, we simply move these content zones into place.

This `Coral.Alert` markup shows content zones for header and content areas of the component:

```
<coral-alert>
  <coral-alert-header>INFO</coral-alert-header>
  <coral-alert-content>This is is an alert.</coral-alert-content>
</coral-alert>
```

Additionally, in the same way you can access the body of the HTML document with document.body, we create references for 
each content zone on the JavaScript object that corresponds to the component. You can access the header content zone with 
`alert.header` and change its content e.g append elements or do whatever else you need to do.

## Dependencies

Coral Spectrum has a few dependencies and polyfills. Some are actually written and maintained by the Coral Spectrum team, and are included 
without being considered an external dependency.

These dependencies are:
* [Spectrum CSS](https://github.com/adobe/spectrum-css) for the Spectrum theme and icons
* [Custom Elements v1 polyfill](https://github.com/webcomponents/custom-elements/) with built-in components support
* [Promise polyfill](https://www.npmjs.com/package/promise-polyfill) for IE11 support
* [CustomEvent polyfill](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/CustomEvent#Polyfill) for IE11 support
* [ResizeObserver polyfill](https://github.com/que-etc/resize-observer-polyfill) to detect element size changes
* Element `closest(), matches(), remove() and classList` polyfills for IE11 support
* [DOMly](https://github.com/lazd/domly) to render HTML templates
* [Vent](https://github.com/adobe/vent) for DOM event delegation
* [PopperJS](https://popper.js.org/) to manage poppers
* [Typekit](https://typekit.com/) to load Adobe Clean fonts

**Note:** Calendar, Clock and Datepicker components will leverage [moment.js](http://momentjs.com/) if loaded on the page. 
 
 
 
