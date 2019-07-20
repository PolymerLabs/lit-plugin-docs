# Unknown property error

```
Unknown property 'value'

             <fancy-slider .value=${this.value}>
                            ~~~~~
```

## What this error means

When binding to a property in a lit-html template, the property must be known to the TypeScript type system.

This error indicates that your the property isn't present, or that the lit-analyzer can't resolve it.

## How to fix it

If your code is correct, and the property is present on that element, then the best solution is to find the TypeScript definition for the element class and add the property there.

## How it's configured

This error is enabled by default. It can be disabled by setting `skipUnknownProperties` to true.
