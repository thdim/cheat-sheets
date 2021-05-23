## Filestructure

MVC - Model (/app/Models) View (/resources/views) Controller (/app/Http/Controllers)  

/app _contains all the bussiness logic (requests, database interaction)_  
/config _configuration files_  
/database _modifing and working with the database schema_  
/public _entrypoint of the app_  
/resources _styles, scripts, views_  
/routes _configure routes_  
/tests  
/vendor _3rd party software, including Laravel_  

## Routes

__Set route name__  
`Route::get('/contact', function () {`  
&nbsp;&nbsp;`return view('contact');`  
`})->name('home.contact');`  

__Set route with parameters__  
`Route::get('/posts/{id}', function($id) {`  
&nbsp;&nbsp;`return 'Blog post '.$id;`  
`});`  

