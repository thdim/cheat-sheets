##### Table of Contents  
[Refs](#refs)  
[Methods](#methods)

[Conditional Content & Lists](#conditional-content--lists)  
[Vue Route](#vue-route)  
[Vuex](#vuex)  


# The Basics

### Data configuration option  
Create a Vue App  
`const app = Vue.createApp({ data(), methods: {}, computed: {}, watch: {} });`  
`app.mount('#id');`  

The data() properties  
```
data() {   
  return {   
    name: 'Name',  
    fullname: '',  
    link: '',  
    class: '',  
  }  
}  
```

Interpolation  
`{{ name }}`  

Data Binding  
`v-bind:href="link"` _or_ `:href="link"`  
`v-bind:class="class"` _or_ `:class="class"`  

Output raw HTML  
`<p v-html="paragraph"></p>`  

Show the first value and preserve it  
`<p v-once>{{ name }}</p>`  

## Refs  
`<input type="text" ref="userInput">`  _set a ref with key 'userInput'_  
`this.$refs.userInput.value` _use it in vue_  

Notes:  
_Use refs when you don't need to update in each keystroke as with v-model (e.g. when you have a save button)_  

### Methods vs Computed vs Watch  
#### Methods
Use with event binding or data binding  
Data binding: Method is executed for every "re-render" cyrcle of the component  
Use for events of data that really needs to be re-evaluated all the time  

```
methods: {  
  methodName() {  
    return this.name  
  }  
}
```

Call method  
`{{ functionName() }}`  

#### Computed  
Use with data binding  
Computed properties are only re-evaluated if one of their "used values" changed  
Use for data that depends on other data  

```
computed: {  
  method() {  
    return this.varName  
  }  
}
```

Notes:   
_Name your computed methods as you would name a data property_  
_To use it `{{ method }}`, NOT `{{ method() }}` (Vue will call it automatically)_   
_In most scenarios we use computed, except in events since only methods allowed_  

#### Watch  
Not used directly in template  
Allows you to run and code in reaction to some changed data (e.g. send Http requests etc.)  
Use for any non-data update you want to make  

```
watch: {  
  counter(value) {  
    if (value > 50) { this.counter = 0 }  
  }  
}
```

Notes:  
_Methods should be named with the same name as a data property_  
_This naming will create a connection and the watcher will executed each time the data property changes_  
_Watchers don't return and the value is the latest value of the data propetry_  
_Can also accept `name(newValue, oldValue)`_  


### Event Binding  
`<button v-on:click="addMethod">Add</button>` _or_ `<button @click="addMethod">Add</button>`  
`<button v-on:click="removeMethod(arg)">Remove</button>` _or_ `<button @click="removeMethod(arg)">Remove</button>`   

### Native Event Object  
_when you point to a method_  
`<input type="text" v-on:input="setName">`   
`setName(event) { return event.target.value }`  

_when you need to send an argument use $event_  
`<input type="text" v-on:input="setName($event, 'varchar')">`   
`setName(event, lastname) { return event.target.value + ' ' + lastname }`  

### Event Modifiers (with dot)  
_prevent default form submit_  
`<form v-on:submit.prevent="submitForm"></form>`  

_react to a behaviour with middle click (default left)_  
`<button v-on:click.middle="addMethod">Add</button>`  

_listen to a key with modifier_  
`v-on:keyup.enter` _or_ `v-on:keydown.cntr`  

_.stop will stop a parent @click in the selected element_  
`@click.stop` 

### Two-way Binding  
`<input type="text" v-model="varName">`  

### Dynamic Styling  

#### Inline Styling  

_bind style border-color (borderColor) to red if dataPropetry is true and to #ccc is not_  
`<div class="demo" :style="{borderColor: dataProperty ? 'red' : '#ccc'}">`  

#### CSS Classes  

_Ternary oparation in class binding_  
`<div :class="dataProperty ? 'demo active' : 'demo'">`  

Always bind demo class and bind active if dataPropetry is true  
`<div :class="{demo: true, active: dataProperty}">` _or_  
`<div class="demo" :class="{active: dataProperty}">` _or_  
`<div :class="['demo', {active: dataPropetry}]">`  

For more complex cases, use computed  
`<div :class="boxClass">`  
`computed: { boxClass() { return { active: this.boxSelected }; } }`

# Conditional Content & Lists

### v-if, v-else, v-else-if

#### v-if
`<p v-if="dataPropetry.lenght === 0"></p>`  

Notes:  
_inside the "" can be any expression that can be interpreted as a true/false_  
_conditions can be compined with && or ||_  
_can point to a method or a computed propetry_  
_v-if adds and removes from the DOM_  
_v-show works in the same way but shows hides with CSS_  

#### v-else
`<p v-if="_condition_"></p>`  
`<p v-else></p>`  

Notes:  
_v-else needs to be used in an html element that it's next to the v-if element_  

### v-for  
`<li v-for="row in array">{{ row }}</li>` _loop in arrays_  
`<li v-for="(row, index) in array">{{ index }}: {{ row }}</li>` _get index_    
`<li v-for="(value, key) in {name: 'Themis', age: 38}">{{ key }}: {{ value }}</li>` _loop in objects_  
`<li v-for="num in 10">{{ num }}</li>`  _loop from 1 to 10_  
`<li v-for="(row, index) in array" :key="row['id']">{{ index }}: {{ row['name'] }}</li>` _bind key (:key)_    

# Vue Instance Lifecyrcle

_createApp({})_  
`beforeCreate()`  
`created()`  
`beforeMount()`  
`mounted()`  
_data change_  
`berofeUpdate()`  
`updated()`  
_instance unmounted_  
`beforeUnmount()`  
`unmounted`  

# Components

In a new .vue file have a `<template></template>` and `<script>export default { data() { ... } }`  

#### Global component
`import TheComponent from './relative/path'`  
`app.component('the-component', TheComponent)`  

#### Local component
`import TheComponent from './relative/path'`  
`components: { TheComponent }, data() { ... }`    

### Props  

Parent --> Child Communication  
In the parent template
`<the-component prop1="..."></the-component>` 

In the component  
_basic config_  
`props: ['prop1'],`  _access prop template_    

_only type congig_  
`props: { prop1: String|Number|Boolean|Array|Object|Date }`  

_full config_  
`props: { prop1: { type: String, required: false, default: 0 } }` (also validator: function() {} is possible, check documentation)  

Bind props  
`<the-component :prop2="true"></the-component>` _if you want any other value than string you need to bind the value (or if they are dynamic anyway)_  

### Emits  
Emit from inside the component  
`this.$emit('custom-event-name', argument)`  

Listen it in the parent  
`<the-component @custom-event-name="callMethod"></the-component>`  
`callMethod(argument) { ... }`  

To define emits (optionally)  
`emits: ['custom-event-name']`  

### Provide & Inject  
_used when you want to communicate between components that are having a pass-thew component_  

__WATCH 100/102 AND ADD NOTES__  


### Scoped Styles
_when using scoped the css will apply only in the template of the same component_  
`<style scoped>`  

### Slotes  
In the child component  
`<slot>`  

In the parent component  
`<custom-component> ... HTML and Vue code ...</custom-component>`  

Notes  
_slotes are like props but for HTML and Vue code_  
_they are used when we want to use a component as a wrapper of HTML and dynamic content_  

Named slots  
`<slot name="my-slot-name"></slot>`  _declare them in the child_  
`<template v-slot:tbody> ... </template>` _target them in the parent (use v-slot:default to target the not named)_  

__ADD NOTES__  

### Dynamic Components  

__ADD NOTES__  


# Vue Route

Redirect from a component  
`this.$route.push('/coaches')` _we can go back to the page we came_  
`this.$route.replace('/coaches')` _we cannot go back, good for forms_  


# Vuex  
`npm install --save vuex`  

### Create store

`import { createStore } from 'vuex'`  

_init store and create a statewide variable named counter_  
```
const store = createStore({  
  state() {  
    return { counter: 0 }  
  }  
})  
app.use(store)
```  

_use this state in any component_  
`{{ $store.state.counter }}` _or_ `this.$store.state.counter`  

### Mutations  
_update the vuex store data_  

#### mutations should be occured in actions  
```
state() { ... }  
mutations: {  
  addOne(state) { state.counter++ }  
}
```
  
`this.$store.commit('addOne')`  

mutation with a payload _can be a num, string, bool or object_  
`increase(state, payload) { state.counter = state.counter + payload.value }`   
`this.$store.commit('increase', { value: 10 })`  

### Actions
they are used in components to commit mutations   

#### they commit mutations and can be unsynchronous  
_you can use the same name as with the mutation_  

```
state() { ... }   
mutations: { ... }  
actions: {  
  increment(context) { context.commit('increment', { value: 10 } ) }  
}
```

_use_ in the component
`this.$store.dispatch( { 'increment', { value: 10 } } )`  

### Getters  
get values from the vuex store data  

```
state() { ... }   
mutations: { ... }  
actions: { ... }  
getters: {  
  finalCounter(state) { return state.counter *2 }  
}
```

use getters  
`this.$store.getters.finalCounter`  















