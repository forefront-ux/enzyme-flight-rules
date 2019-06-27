# Flight rules for Enzyme

❤️ Inspired by [Git Flight Rules](https://github.com/k88hudson/git-flight-rules)

🌍
*[English](README.md) ∙ [简体中文](README_zh-CN.md)*

#### What are "flight rules"?

A guide for astronauts (now, programmers using Git) about what to do when things go wrong.

>  *Flight Rules* are the hard-earned body of knowledge recorded in manuals that list, step-by-step, what to do if X occurs, and why. Essentially, they are extremely detailed, scenario-specific standard operating procedures. [...]

> NASA has been capturing our missteps, disasters and solutions since the early 1960s, when Mercury-era ground teams first started gathering "lessons learned" into a compendium that now lists thousands of problematic situations, from engine failure to busted hatch handles to computer glitches, and their solutions.

&mdash; Chris Hadfield, *An Astronaut's Guide to Life*.

#### Conventions for this document

This Document should work for Enzyme version ^3.10.0. See the [enzyme website](https://airbnb.io/enzyme/) to check your enzyme version.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [SubComponent](#subcomponent)
- [Render Component](#render-component)
  - [I want to only render the top level component, or I don't want to render child component](#i-want-to-only-render-the-top-level-component-or-i-dont-want-to-render-child-component)
  - [I want to render the component with all child components.](#i-want-to-render-the-component-with-all-child-components)
  - [I want to get shallowWrapper of a child component in a shallow render component](#i-want-to-get-shallowwrapper-of-a-child-component-in-a-shallow-render-component)
  - [I want to get a CheerioWrapper around the rendered HTML of the single node's subtree in a shallow/mount render component.](#i-want-to-get-a-cheeriowrapper-around-the-rendered-html-of-the-single-nodes-subtree-in-a-shallowmount-render-component)
  - [I want to get a string of the rendered HTML markup of the entire component (not just the shallow-rendered part)](#i-want-to-get-a-string-of-the-rendered-html-markup-of-the-entire-component-not-just-the-shallow-rendered-part)
  - [I want to get an HTML-like string of the wrapper for debugging purposes of the component](#i-want-to-get-an-html-like-string-of-the-wrapper-for-debugging-purposes-of-the-component)
  - [I want to get an react component instance of the component](#i-want-to-get-an-react-component-instance-of-the-component)
- [Other Resources](#other-resources)
  - [Vidoes](#vidoes)
  - [Articles](#articles)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## SubComponent
*this component will be used in all these sample code below*
```
const SubComponent = props => (
    <a href="https://airbnb.io/enzyme/docs/api">{props.children}</a>
);
```

## Render Component

### I want to only render the top level component, or I don't want to render child component
**`shallow`**
```js
const wrapper = shallow(
    <h1>
        Hello Enzyme!
        <SubComponent />
    </h1>
);

// console.log(wrapper.debug());
// <h1>
//   Hello Enzyme!
//   <SubComponent />
// </h1>
```

[Visit Shallow API](https://airbnb.io/enzyme/docs/api/shallow.html)

---

### I want to render the component with all child components.
**`mount`**
```js
const wrapper = mount(
    <h1>
        Hello Enzyme!
        <SubComponent>Vist Enzyme Website</SubComponent>
    </h1>
);

// console.log(wrapper.debug());
// <h1>
//   Hello Enzyme!
//   <SubComponent>
//     <a href="https://airbnb.io/enzyme/docs/api">
//       Vist Enzyme Website
//     <a/>
//   <SubComponent>
// </h1>
```

[Visit Mount API](https://airbnb.io/enzyme/docs/api/mount.html)

---

### I want to get shallowWrapper of a child component in a shallow render component 
**`ShallowWrapper.dive`**
```js
const wrapper = shallow(
    <h1>
        Hello Enzyme!
        <SubComponent>Vist Enzyme Website</SubComponent>
    </h1>
);
const shallowWrapper = wrapper.find(SubComponent).dive();

// console.log(wrapper.debug());
// <SubComponent>
//   <a href="https://airbnb.io/enzyme/docs/api">
//     Vist Enzyme Website
//   <a/>
// <SubComponent>
```

[Visit ShallowWrapper/dive API](https://airbnb.io/enzyme/docs/api/ShallowWrapper/dive.html)

---

### I want to get a CheerioWrapper around the rendered HTML of the single node's subtree in a shallow/mount render component.
**`ShallowWrapper.render`**

**`ReactWrapper.render`**
```js
const wrapper = shallow(
// const wrapper = mount(
    <h1>
        Hello Enzyme!
        <SubComponent>Vist Enzyme Website</SubComponent>
    </h1>
);
const cheerioWrapper = wrapper.find(SubComponent).render();

// output:
// <a href="https://airbnb.io/enzyme/docs/api">
//   Vist Enzyme Website
// <a/>
```

[Visit ShallowWrapper/render API](https://airbnb.io/enzyme/docs/api/ShallowWrapper/render.html)

[Visit ReactWrapper/render API](https://airbnb.io/enzyme/docs/api/ReactWrapper/render.html)

---


### I want to get a string of the rendered HTML markup of the entire component (not just the shallow-rendered part)
**`ShallowWrapper.html`**

**`ReactWrapper.html`**
```js
const wrapper = shallow(
// const wrapper = mount(
    <h1>
        Hello Enzyme!
        <SubComponent>Vist Enzyme Website</SubComponent>
    </h1>
);

const output = wrapper.html();
// output:
// <h1>Hello Enzyme!<a href="https://airbnb.io/enzyme/docs/api">Vist Enzyme Website<a/></h1>
```

[Visit ShallowWrapper/html API](https://airbnb.io/enzyme/docs/api/ShallowWrapper/html.html)

[Visit ReactWrapper/html API](https://airbnb.io/enzyme/docs/api/ReactWrapper/html.html)

---

### I want to get an HTML-like string of the wrapper for debugging purposes of the component
**`ShallowWrapper.debug`**

**`ReactWrapper.debug`**
```js
const wrapper = mount(
// const wrapper = shallow(
    <h1>
        Hello Enzyme!
        <SubComponent>Vist Enzyme Website</SubComponent>
    </h1>
);

// console.log(wrapper.debug());
// <h1>
//   Hello Enzyme!
//   <a href="https://airbnb.io/enzyme/docs/api">
//     Vist Enzyme Website
//   <a/>
// </h1>
```

[Visit ShallowWrapper/debug API](https://airbnb.io/enzyme/docs/api/ShallowWrapper/debug.html)

[Visit ReactWrapper/debug API](https://airbnb.io/enzyme/docs/api/ReactWrapper/debug.html)

---

### I want to get an react component instance of the component
*NOTE: can only be called on a wrapper instance that is also the root instance. With React 16 and above, instance() returns null for stateless functional components.*

**`ShallowWrapper.instance`**

**`ReactWrapper.instance`**
```js
const wrapper = mount(
// const wrapper = shallow(
    <h1>
        Hello Enzyme!
        <SubComponent>Vist Enzyme Website</SubComponent>
    </h1>
);

wrapper.instance();
```

[Visit ShallowWrapper/debug API](https://airbnb.io/enzyme/docs/api/ShallowWrapper/debug.html)

[Visit ReactWrapper/debug API](https://airbnb.io/enzyme/docs/api/ReactWrapper/debug.html)

---

## Other Resources

### Vidoes

* [React Redux Unit & Integration Testing with Jest and Enzyme](https://www.youtube.com/watch?v=EgJZv9Iyj-E&list=PL-Db3tEF6pB8Am-IhCRgyGSxTalkDpUV_) - The purpose of this tutorial series is to demonstrate how to properly implement a test first approach (TDD) to coding with react and redux.

### Articles

* [Testing React With Jest and Enzyme
](https://medium.com/codeclan/testing-react-with-jest-and-enzyme-20505fec4675) - Look at how to setup and use Jest and Enzyme to test a React application
* [Test your redux container with enzyme](https://medium.com/@visualskyrim/test-your-redux-container-with-enzyme-a0e10c0574ec)
