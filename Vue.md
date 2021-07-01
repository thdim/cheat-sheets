# The basics

Data option: return an object with variables  
`data() { return { varName: 'Name' } }`  

Interpolation  
`{{ varName }}`  

Data binding  
`v-bind:href="varLink"` _or_ `:href="varLink"`  
`v-bind:class="varClass"` _or_ `:class="varClass"`  

Methods option (pass a JS object with functions)  
`methods: { functionName() { return this.varName } }`  

Call method  
`{{ functionName() }}`  

Output raw HTML  
`<p v-html="varParagraph"></p>`  

Event binding  
`<button v-on:click="addMethod">Add</button>`
