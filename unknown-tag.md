# Unknown tag error

```
Unknown tag <unknown-element>
  Check that you've imported the element, and that it's declared on the HTMLElementTagNameMap.

19             <unknown-element></unknown-element>
                ~~~~~~~~~~~~~~~
```

### What this error means

A lit-html template may contain HTML tags. These tags may be built into the browser, like `<div>`, `<input>`, or `<video>`. Or they may be custom elements declared by your code, or code that you depend on.

This error indicates that your lit-html template references a tag that the lit-analyzer can't resolve.

There must be a declaration of the element to TypeScript in order for the analyzer to find it. For example:

```typescript
export class FancySlider extends HTMLElement {
  value: number;
  // etc...
}
customElements.define('fancy-slider', FancySlider);

declare global {
  interface HTMLElementTagNameMap {
    'fancy-slider': FancySlider,
  }
}
```

### How to fix it

Three conditions must hold:

1. There must be a type for the element in TypeScript, either because the code for the element is written in TpeScript, or because there are TypeScript typings for the element.
2. The type must be associated with the element's tagname in the HTMLElementTagNameMap. 
3. The the file where you're using the element must depend on the declaration of the element, generally by importing it.

Most commonly, you're just missing an import for the element. If you're importing the element, and your code works at runtime, then you need to define an interface for the element, and add it to the HTMLElementTagNameMap.

### How it's configured

This error is enabled by default. It can be disabled by setting `skipUnknownTags` to true.

To ignore errors about tags without declaring them to the TypeScript type system, you can add them to `globalTags`, however it is almost always a better idea to declare a type instead.
