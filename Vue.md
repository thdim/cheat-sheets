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

Event Binding  
`<button v-on:click="addMethod">Add</button>`  
`<button v-on:click="removeMethod(arg)">Remove</button>`
