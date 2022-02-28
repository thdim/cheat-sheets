## Project files structure

MVC   
- Model /app/Models  
- View /resources/views  
- Controller /app/Http/Controllers  

__/app__ _contains all the bussiness logic (requests, database interaction)_  
__/config__ _configuration files_  
__/database__ _modifing and working with the database schema_  
__/public__ _entrypoint of the app_  
__/resources__ _styles, scripts, views_  
__/routes__ _configure routes_  
__/tests__  
__/vendor__ _3rd party software, including Laravel_  

## Routes

__Set named route__  
```
Route::get('/contact', function () {    
  return view('contact');    
})->name('home.contact');
```

__Set route with parameters__  
```
Route::get('/posts/{id}', function($id) {  
  return 'Blog post '.$id;  
});
```

__Set route with optional parameter__  
```
Route::get('/recent-posts/{days_ago?}', function($daysAgo = 20) {  
  return 'Posts from '.$daysAgo.' days ago';  
});
```  

