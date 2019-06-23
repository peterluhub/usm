<h1 align="center">Welcome to XSM 👋</h1>
<p>
  <img src="https://img.shields.io/badge/version-1.0.0-blue.svg?cacheSeconds=2592000" />
  <a href="https://github.com/peterluhub/usm/blob/master/LICENSE">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" target="_blank" />
  </a>
</p>

> XSM - State Management made eXtraordinarily simple for React, Vue, and Angular

### 🏠 [Homepage](https://github.com/peterluhub/usm)

### Highlights

  - Incrediblly easy to use, developer friedly and minimum learning curve
  - Reactive, nonintrusive
  - Automatic state data removal, efficient memory management
  - Small size for fast download
  - Super simple async handling
  - Same API for React, Vue, and Angular

### How-to's

##### Install

```sh
npm install usm
```

##### Usage in Brief

1. Tell XSM which framework to use

```javascript
setcfg({'framework': 'React'})
```

2. Bind the component state to XSM

```javascript
bindState(this, {key: val, key2: val2, ...})
```

3. When you are ready to update the state(sync or async)

```javascript
set('key', val)
```

Component will be re-rendered automatically.

##### Debug and Trace

Both debug and trace can be selectively turn on and off at any point

```javascript
setcfg({debug: true})  //debug on
setcfg({debug: false}) //debug off
setcfg({trace: true})  //trace on
setcfg({trace: false}) //trace off
```

### Why XSM?

To answer why, let's start by answering another question, what is XSM?.  It consists a global store and the machinary to re-render the component when the state is updated.  The store is just a javascript object with key and value pairs.  By binding the instance reference, *this*, to the store, each component can react to the changes of the store whether it is re-render or unmount.  It is really *this* simple, no need to use HOC, provider, reducer, decorator, observer, action, dispatcher, etc.  Hence, all the three most popular framewokrs work the same way in XSM and that's why we can keep the code size very small and support the three frameworks without framework specific modules.  On top of that, XSM is performant according to Stefan Krause's [js-framework-benchmark](https://github.com/krausest/js-framework-benchmark).  It outperforms Redux and MobX with React and Vuex with Vue.

### API

**bindState** - binds a component's *this* and optionally state to the store.  The state is an object with key and value pairs.
```javascript
 bindState(this, state)
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
 setMany({key1: value1, key2, value2, ...})
```

**setcfg** - It takes an object as an argument and is used for telling XSM which framework you app uses and optionally for binding the state of all components of the app to the store as well as turning the debug and trace on and off.
```javascript
 setcfg(
    {framework: frameworkValue, 
     bindings: {ComponetName: {key1: value1,...},
             ComponetName1: {key1: value1,...},
            ...},
     debug: true/false,
     trace: true/false
    }
 )
```
- frameworkValue: React, Vue, or Angular
- ComponetName: It is the classe name for React and Angular.  It is the registered component name for Vue
  bindings: It serves two purposes.  One is to bind the state of each component to the store and you don't need to binState in this case.  Another is to tell XSM that which piece of data is shared by more than one components and the shared data will not be deleted even if the the components are unmounted.

## User Guide

To use XSM to manage you app state, here are the steps to follow:

1. Use *setcfg* to bind XSM to a framework.  Currently, XSM supports Angular, Reatc, and Vue.
2. Bind the component state to the store with *bindState* to enble the auto re-rendering when the state is updated.  The value of each bound key can be accessed in the component with *this.keyname*.  For example, you want to bind a key and value pair of {title: 'XSM'} to a component,
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

3. When it's time to update the state, use *set* where your state data is available whether it's in the await function, promise.then callback, or just plain old callback. XSM does not get in the way.


## Author

👤 **Peter Lu**

* Github: [@peterluhub](https://github.com/peterluhub)

### Show your support

Give a ⭐️ if this project helped you !

### 📝 License

Copyright © 2019 [Peter Lu](https://github.com/peterluhub).<br />
This project is [MIT](https://github.com/peterluhub/usm/blob/master/LICENSE) licensed.

***
_This README was originally generated by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
