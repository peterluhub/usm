 ![XSM](/docs/xsmlogo.png)
<p>
  <a href="https://bundlephobia.com/result?p=xsm">
    <img src="https://flat.badgen.net/bundlephobia/minzip/xsm" alt="Minified + gzip package size for xsm in KB">
  </a>
  <a href="https://travis-ci.com/peterluhub/xsm">
    <img src="https://travis-ci.com/peterluhub/xsm.svg?branch=master" alt="Build Status">
  </a>
  <a href="https://www.npmjs.com/package/xsm">
    <img src="https://img.shields.io/npm/v/xsm.svg" alt="npm version">
  </a>
  <a href="https://packagephobia.now.sh/result?p=xsm">
    <img src="https://packagephobia.now.sh/badge?p=xsm" alt="install size">
  </a>
  <a href="https://github.com/peterluhub/usm/blob/master/LICENSE">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" target="_blank" />
  </a>
</p>

> XSM - State Management made eXtraordinarily simple and effective for Angular, React, Vue, and Svelte.

### 🏠 [Homepage](https://github.com/peterluhub/usm)

### Demos
[Angular](https://codesandbox.io/s/angular-xsm-demo-1j9j0)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [React](https://codesandbox.io/s/xsm-react-3v3fg)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Svelte](https://codesandbox.io/s/svelte-xsm-x4o6r)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Vue](https://codesandbox.io/s/vuexsmdemo-2152h)

[Realworld Example App with react-xsm](https://codesandbox.io/s/realworld-example-app-with-react-xsm-xelx1)
### Highlights

  -   Incredibly easy to use, developer friendly and minimum learning curve
  -   Reactive, unintrusive
  -   Automatic re-rendering and state data removal, efficient memory management
  -   Super simple async handling
  -   Same API for Angular, React, Vue, and Svelte, code reuse, framework agnostic
  -   Small size for fast download, no framework specific plugins needed.

<table border="0">
    <thead>
        <tr>
            <th>Library</th>
            <th>Minzipped Size</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>XSM</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/xsm" alt="Minified + gzip package size for xsm in KB">
            </td>
        </tr>
        <tr>
            <td>Redux</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/redux" alt="Minified + gzip package size for redux in KB" class="badge--in-table">
            </td>
        </tr>
        <tr>
            <td>react-Redux</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/react-redux" alt="Minified + gzip package size for react-redux in KB" class="badge--in-table">
            </td>
        </tr>
        <tr>
            <td>mobx</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/mobx" alt="Minified + gzip package size for mobx in KB" class="badge--in-table">
            </td>
        </tr>
        <tr>
            <td>mobx-react</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/mobx-react" alt="Minified + gzip package size for mobx-react in KB" class="badge--in-table">
            </td>
        </tr>
        <tr>
            <td>Vuex</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/vuex" alt="Minified + gzip package size for vuex in KB" class="badge--in-table">
            </td>
        </tr>
        <tr>
            <td>RXJS</td>
            <td>
                <img src="https://flat.badgen.net/bundlephobia/minzip/rxjs" alt="Minified + gzip package size for rxjs in KB" class="badge--in-table">
            </td>
        </tr>
    <tbody>
</table>

### Benchmark Results
XSM is performant according to Stefan Krause's [js-framework-benchmark](https://github.com/krausest/js-framework-benchmark).  As shown below,
 ![Benchmarks](/docs/jfb-benchmarks.png).

The code for the benchmarks is in [this repo](https://github.com/peterluhub/jfb).

### How-to's

##### Install
```sh
npm install xsm
```

##### Usage in Brief

-   Tell XSM which framework to use

  ```javascript
    setup({'framework': 'React'})
  ```

-   Bind the component state to XSM

  ```javascript
    bindState(this, {key: val, key2: val2, ...})
  ```

-   When you are ready to update the state(sync or async)

  ```javascript
    set('key', val)
  ```

Component will be re-rendered automatically.

##### Debug and Trace

Both debug and trace can be selectively turn on and off at any point

  ```javascript
  setup({debug: true})  //debug on
  setup({debug: false}) //debug off
  setup({trace: true})  //trace on
  setup({trace: false}) //trace off
  ```

### Why XSM

To answer why, let's start by answering another question, what is XSM?  It consists of a global store and the machinary to re-render the component when the state is updated.  The store is just a javascript object with key and value pairs.  By binding the instance reference, *this*, to the store, each component can react to the changes of the store whether it is re-render or unmount.  It is really *this* simple, no need to use HOC, provider, reducer, decorator, observer, action, dispatcher, etc.  Hence, all the three most popular frameworks work the same way in XSM and that's why we can keep the code size very small and support the three frameworks without framework specific modules.  Svelte is very different from other frameworks.  It is *this* less.  The state object becomes *this*. 

### API

**bindState** - binds a component's *this* and optionally state to the store.  The state is an object with key and value pairs. For Svelte, the value is a fuction that wraps the assignment of the value.
```javascript
 bindState(this, state) //Angular, React, Vue
 bindState(state) //Svelte is this less, state is {key: val => stateVariable = val}
```

**unbindState** - If a component is mounted and unmounted repeatedly, you need to unbind the component state from the store when the component unmounts to prevent memory leak.  This is needed for Svelte only.  The unbinding is done aotumatically with the other frameworks by XSM.
```javascript
 unbindState(state) //Svelte only
```

**get** - gets the value of a given key from the store.
```javascript
 get(key)
```

**set** - updates the store with the value for a given key and re-renders the component(s).
```javascript
 set(key, value)
```

**setMany** - updates the store for the given key and value pairs and re-renders the component(s).
```javascript
 setMany({key1: value1, key2: value2, ...})
```

**setup** - It takes an object as an argument and is used for telling XSM which framework you app uses and optionally for binding the state of all components of the app to the store as well as turning the debug and trace on and off.
```javascript
 setup(
    {framework: frameworkValue, 
     bindings: {ComponentName: {key1: value1, ...},
             ComponentName1: {key1: value1, ...},
            ...},
     debug: true/false,
     trace: true/false
    }
 )
```
-   frameworkValue: Angular, React, Vue, or Svelte
-   ComponentName: It is the class name for React and Angular.  It is the registered component name for Vue.  Does not apply to Svelte.
-   bindings: It serves two purposes.  One is to bind the state of each component to the store and you don't need to binState in this case.  Another is to tell XSM that which piece of data is shared by more than one components and the shared data will not be deleted even if the the components are unmounted.  Does not apply to Svelte.

**setcfg** - It is an alias of *setup*.



## User Guide

To use XSM to manage you app state, here are the steps to follow:

- Use *setup* to bind XSM to a framework.  Currently, XSM supports Angular, Reatc, Vue, and Svelte.
- Bind the component state to the store with *bindState* to enble the auto re-rendering when the state is updated.  The value of each bound key can be accessed in the component with *this.keyname*.  For example, you want to bind a key and value pair of {title: 'XSM'} to a component,
- For Angular and React, it is done in the constructor.
  ```javascript
  constructor() {
      super()
      bindState(this, {title: 'XSM'})
  }
  ```
- For Vue, it can be done in the *created* life cycle hook.
  ```javascript
  created() {
      bindState(this, {title: 'XSM'})
  }
  ```
- For Svelte, it can be done inside the script tag of a component.
  ```javascript
  let title;
  let bindings = {title: val => title = val};
  bindState(bindings);
  //if needed
  onDestroy(() => unbindState(bindings));
  ```

- When it's time to update the state, use *set* when and where your state data is available whether it's in the await function, promise.then callback, plain old callback, or anywhere in your code path. XSM does not get in the way.

- Besides the demos, you can find more code examples in [this repository](https://github.com/peterluhub/xsm-code-examples).  A realworld example(implementing the [Realworld Example Specs](https://github.com/gothinkster/realworld) using XSM with React is in [this repo](https://github.com/peterluhub/realworld-example).  Angular and Vue verions will be implemented soon.

## Author

👤 **Peter Lu**

* Github: [@peterluhub](https://github.com/peterluhub)

### Show your support

Give a ⭐️ if this project helped you !

### 📝 License

This project is [MIT](https://github.com/peterluhub/usm/blob/master/LICENSE) licensed.

***
_This README was originally generated with [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
