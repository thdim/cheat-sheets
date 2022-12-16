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

### routes

Route in a static blade template (no params)  
`Route::view('/', 'index');`  

Set named route  
```
Route::get('/contact', function () {    
  return view('contact');    
})->name('home.contact');
```  

Set route with parameters  
```
Route::get('/posts/{id}', function($id) {  
  return 'Blog post '.$id;  
});
```  

Set route with optional parameter  
```
Route::get('/recent-posts/{days_ago?}', function($daysAgo = 20) {  
  return 'Posts from '.$daysAgo.' days ago';  
});
```  

### Helpers

#### URL's with Params  

in blade  
```
<a href="{{ route('page_name') }}?param_id={{ $paramId }}">link with param</a>
```

in controller use the request() helper  
```
$posts = Post::where('category_id', request('category_id'))->latest()->get();
```  

#### compact()  

```
return view('index', [
  'categories' => $categories,
  'posts' => $posts
]);
```  

the same with compact()   

`return view('index', compact('categories', 'posts'));`  

### Blade

#### Helper functions and commands

asset()  
`{{ asset('css/styles.css') }}`  

yield()  
`@yield('content')`  
```
@section('content')
...
@endsection
```





