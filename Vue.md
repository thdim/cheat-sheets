# The basics

### Data configuration option  
`data() {`   
  `return { `  
    `name: 'Name',`  
    `fullname: '',`  
    `link: '',`  
    `class: '',`  
  `}`  
`}`  

Interpolation  
`{{ name }}`  

Data Binding  
`v-bind:href="link"` _or_ `:href="link"`  
`v-bind:class="class"` _or_ `:class="class"`  

Output raw HTML  
`<p v-html="paragraph"></p>`  

Show the first value and preserve it  
`<p v-once>{{ name }}</p>`  

### Methods vs Computed vs Watch  
#### Methods
Use with event binding or data binding  
Data binding: Method is executed for every "re-render" cyrcle of the component  
Use for events of data that really needs to be re-evaluated all the time  

`methods: {`  
  `methodName() {`  
    `return this.name`  
  `}`  
`}`  

Call method  
`{{ functionName() }}`  

#### Computed  
Use with data binding  
Computed properties are only re-evaluated if one of their "used values" changed  
Use for data that depends on other data  

`computed: {`  
  `method() {`  
    `return this.varName`  
  `}`  
`}`  

Notes:   
_Name your computed methods as you would name a data property_  
_To use it `{{ method }}`, NOT `{{ method() }}` (Vue will call it automatically)_   
_In most scenarios we use computed, except in events since only methods allowed_  

#### Watch  
Not used directly in template  
Allows you to run and ccode in reaction to some changed data (e.g. send Http requests etc.)  
Use for any non-data update you want to make  

`watch: {`  
  `counter(value) {`  
    `if (value > 50) { this.counter = 0 }`  
  `}`  
`}`  

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

### Two-way Binding  
`<input type="text" v-model="varName">`  

### Dynamic Styling  

#### Inline Styling  

bind style border-color (borderColor) to red if dataPropetry is true and to #ccc is not  
`<div class="demo" :style="{borderColor: dataProperty ? 'red' : '#ccc'}">`  

#### CSS Classes  

Ternary oparation in class binding  
`<div :class="dataProperty ? 'demo active' : 'demo'">`  

_or_    

always bind demo class and bind active if dataPropetry is true  
`<div :class="{demo: true, active: dataProperty}">`  
`<div class="demo" :class="{active: dataProperty}">`


