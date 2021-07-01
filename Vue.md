# The basics

#### Data configuration option  
`data() {`   
  `return { `  
    `name: 'Name',`  
    `fullname: ''`  
  `}`  
`}`  

Interpolation  
`{{ name }}`  

Data Binding  
`v-bind:href="varLink"` _or_ `:href="varLink"`  
`v-bind:class="varClass"` _or_ `:class="varClass"`  

#### Methods configuration option
`methods: {`  
  `methodName() {`  
    `return this.name`  
  `}`  
`}`  

Call method  
`{{ functionName() }}`  

Output raw HTML  
`<p v-html="varParagraph"></p>`  

Show the first value and preserve it  
`<p v-once>{{ name }}</p>`  

#### Computed configuration option  

`computed: {`  
  `method() {`  
    `return this.varName`  
  `}`  
`}`  

Notes:   
_Name your computed methods as you would name a data property_  
_To use it `{{ method }}`, NOT `{{ method() }}` (Vue will call it automatically)_  
_Computed will check the code and update the DOM only when something is used_  
_In most scenarios we use computed, except in events since only methods allowed_  

#### Watch configuration option

`watch: {`  
  `name(value) {`  
    `this.fullname = value + ' ' + 'Dimitriou'`  
  `}`  
`}`  

Notes:  
_Methods should be named with the same name as a data property_  
_This naming will create a connection and the watcher will executed each time the data property changes_  
_Watchers don't return anything, the value is the latest value of the data propetry_  

### Event Binding  
`<button v-on:click="addMethod">Add</button>`  
`<button v-on:click="removeMethod(arg)">Remove</button>`  

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

