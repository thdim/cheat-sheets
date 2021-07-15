# HTTP Response Status Codes:  
__200__ - OK  
__201__ - Created  

__400__ - Bad Request  
_bad supplied data from urls, headers or JSON_  


__401__ - Unauthorized  
__403__ - Forbidden  
__404__ - Not Found    
__405__ - Method Not Allowed  
__409__ - Conflict _(e.g. username exist)_    

__500__ - Internal Server Error  
_database interaction errors_

# HTTP Request Methods:  
__GET__ - Transmit the data identified by the URL to the client  
__POST__ - Create new resource/s (update and merge)  
__PUT__ - If resource exists then update, else create new resource (update and overwrite)  
__PATCH__ - Always for update a resource  
__DELETE__ - Delete a resource identified by a URI  
