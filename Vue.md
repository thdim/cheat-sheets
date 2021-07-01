# The basics

Data (return an object with variables)  
`data() { return { varName: 'Name' } }`  

Interpolation  
`{{ varName }}`  

Data Binding  
`v-bind:href="varLink"` _or_ `:href="varLink"`  
`v-bind:class="varClass"` _or_ `:class="varClass"`  

Methods (pass a JS object with functions)  
`methods: { functionName() { return this.varName } }`  

Call method  
`{{ functionName() }}`  

Output raw HTML  
`<p v-html="varParagraph"></p>`  

Show the first value and preserve it  
`<p v-once>{{ varName }}</p>`  

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