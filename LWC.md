- [Lightning Web Components](#lightning-web-components)
    - [HTML Templates](#html-templates)
      - [Data Binding](#data-binding)
      - [Handle User Input](#handle-user-input)
      - [Use Getters to Compute a Value](#use-getters-to-compute-a-value)
      - [Render Lists](#render-lists)
      - [Render HTML Conditionally](#render-html-conditionally)
      - [Render Multiple Templates](#render-multiple-templates)
      - [Import a Component Dynamically](#import-a-component-dynamically)
    - [Calling Apex Methods From LWC](#calling-apex-methods-from-lwc)
      - [Expose Apex Methods to Lightning Web Components](#expose-apex-methods-to-lightning-web-components)
- [Reference](#reference)

# Lightning Web Components

- Lightning web components are **custom HTML elements** built using HTML and modern JavaScript.
- Lightning Web Components uses core [Web Components](https://github.com/WICG/webcomponents) standards.

### HTML Templates

A component that renders UI has 2 parts.

1. An HTML template file.
2. A JavaScript class file. which is an [ES module](https://lwc.dev/guide/es_modules)

- Lightning Web Components templating system uses the virtual DOM to render components smartly and efficiently.
- Use simple syntax to declaratively **bind a component’s template to data** in the component’s JavaScript class.
- A template is valid HTML with a `<template>` root tag
- You write templates using standard HTML and a few [directives](https://lwc.dev/guide/reference#html-template-directives) that are unique to Lightning Web Components.
- Directives are **special HTML attributes**, like `if:true` and `for:each`, that give you more power to manipulate the DOM in markup.

#### Data Binding

#### Handle User Input

#### Use Getters to Compute a Value

#### Render Lists

#### Render HTML Conditionally

#### Render Multiple Templates

#### Import a Component Dynamically

### [Calling Apex Methods From LWC](https://developer.salesforce.com/docs/component-library/documentation/en/lwc/lwc.apex)

#### [Expose Apex Methods to Lightning Web Components](https://developer.salesforce.com/docs/component-library/documentation/en/lwc/lwc.apex_expose_method)

1. Define a `static` method in the Apex class and annotate it with `@AuraEnabled(cacheable=true)`

```js
public with sharing class ExampleController {

     @AuraEnabled(cacheable=true)
    public static void exampleMethod(string recordId) {
    
    }
}
```

2.Import the static method defined in Apex Class and use it.

```js
import { LightningElement, api } from 'lwc';
import exampleMethod from '@salesforce/apex/ExampleController.exampleMethod';  // Importing Apex Method

export default class ExampleComponent extends LightningElement {

    @api recordId;

    // Calling Apex Method and passing the param
    connectedCallback() {
      exampleMethod({recordId: this.recordId})
      .then(result => {})
      .error(error => {})
    }
}

```


# Reference

- [Lightning Web Components Dev Guide](https://developer.salesforce.com/docs/component-library/documentation/en/lwc)
- [LWC | Dev Guide](https://lwc.dev/guide/introduction)
- [Trailhead LWC Sample Apps](https://github.com/trailheadapps)
- [JavaScript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- [Extend Salesforce with Clicks, Not Code](https://help.salesforce.com/s/articleView?id=sf.extend_click_intro.htm&type=5)
- [SFDCFacts Academy | Lightning Web Component Crash Course | Learn LWC in 100 Minutes with Live Project](https://www.youtube.com/watch?v=bLyAsIeDZtw)
- [Coding Addict | Javascript Fundamentals](https://www.youtube.com/watch?v=2Ji-clqUYnA)
- [SFDCFacts Academy | Modern JS Crash Course | The Ultimate Hands-On JavaScript Tutorial 2021 | Learn JS in 3 hour](https://www.youtube.com/watch?v=dY8li4JnoWQ)
- [Exploring ES6 | Book](https://exploringjs.com/es6.html)
