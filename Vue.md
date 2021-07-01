# The basics

_Data option: return an object with variables_  
`data() { return { varName: 'Name' } }`  

_Interpolation_  
`{{ varName }}`  

_Data binding_  
`v-bind:href="varLink"` _or_ `:href="varLink"`  
`v-bind:class="varClass"` _or_ `:class="varClass"`  

_Methods option (pass a JS object with functions)_  
`methods: { functionName() { return this.varName } }`  

_Call method_  
`{{ functionName() }}`  

_Output raw HTML_  
`<p v-html="varParagraph"></p>`  

_Event binding_  
`<button v-on:click="counter++">Add</button>`
