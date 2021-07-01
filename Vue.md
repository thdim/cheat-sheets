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

### Event Modifiers  
_prevent default form submit_  
`<form v-on:submit.prevent="submitForm"></form>`  

_react to a behaviour with right click (default left)_  
`<button v-on:click.right="addMethod">Add</button>`  


