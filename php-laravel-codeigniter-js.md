# Codes
Code Blocks for Laravel

# Excel File Load to Database:

https://github.com/Maatwebsite/Laravel-Excel

```
 public function excelupload(Request $request)
    {

        if($request->hasFile('excelfile')){
            $path = $request->file('excelfile')->getRealPath();
            $data = Excel::load($path, function($reader) {})->get();
            
            if(!empty($data) && $data->count()){

                foreach ($data->toArray() as $key => $value) {
                    if(!empty($value)){
                        foreach ($value as $v) {
                            $insert[] = ['title' => $v['title'], 'description' => $v['description']];
                        }
                    }
                }
                if(!empty($insert)){
                    Item::insert($insert);
                    return back()->with('success','Insert Record successfully.');
                }
            }
        }
        return back()->with('error','Please Check your file, Something is wrong there.');
    }
```

# Enter only number in Text Field using Javascript
```
<input type="text" value="" name="mobileNo" onkeypress="return isNumber(event)" />
```
```
<script>
    function isNumber(evt) {
    evt = (evt) ? evt : window.event;
    var charCode = (evt.which) ? evt.which : evt.keyCode;
    if (charCode > 31 && (charCode < 48 || charCode > 57)) {
        return false;
    }
    return true;
}
</script>
```
# Get values of Checkbox group on click event

```
function checkboxclicked(){
             var IDs = $('input:checked').map(function(){
                         
                       return $(this).val();
                         console.log(IDs.get());
                     });
             var names = $('input:checked').map(function(){
                         
                       return $(this).attr("name");
                         console.log(names.get());
                     });
```
# Ajax Call in Laravel 5.4
```
$('#enrolcol3').on('click', function() {
                    
                    $.ajax({
                        // headers: {
                        //               'X-CSRF-Token': $('input[name="_token"]').val()
                        //           },
                        url: "/submituserdetails",
                        type: "POST",
                        data: {firstname: $("#firstname").val(), lastname: $("#lastname").val(), email: $("#email").val(), mobileNo: $("#phone").val(), country: $("#country").val(), city: $("#city").val(), address: $("#address").val(), courselanguage: $("#courselanguage").val(), genpwd: $("#pwd").val(), flag: $("#enrolflag").val(), _token:'{{ csrf_token() }}'  },
                        success: function (response) {
                          // you will get response from your php page (what you echo or print) 
                          // rohini = "you are attending the event";
                          // u = document.getElementById('msg');
                          // u.innerHTML = rohini;
                        },
                        error: function(jqXHR, textStatus, errorThrown) {
                           console.log(textStatus, errorThrown);
                        }
                    });
                
                }); 
  ```
                
  # Remove Index.php from URL's in Laravel
  add this code in .htaccess file
```
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ /index.php?/$1 [L]
```
 # CodeIgniter .htaccess file to override index.php from URL's
 
 ```
  RewriteEngine On
  RewriteCond $1 !^(index\.php|assets|images|js|css|uploads|favicon.png)
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule ^(.*)$ index.php/$1 [L]
  
 ```
 
 # Ajax Call in CodeIgniter
 POST REQUEST
 ```
 $('#like').click(function () {
  	    $.ajax({
  	      url: "<?php echo base_url();?>index.php/welcome/savelike",
  	      type: "POST",
  	      data: {
  	      		jbskr_id : 1,
  	      		rctr_id	 : 2},
  	      dataType: "json",
  	      success: function(data) {
  	        
  	      }
  	    });
  	  });
 ```
GET REQUEST
```
 function countlikes(){
    		var id=1;
    		$.ajax({
    		  url: "<?php echo base_url();?>index.php/welcome/getlikes?id="+id,
    		  type: "GET",
    		  dataType: "json",
    		  success: function(data) {
    		    console.log(data.id);
    		    $("#likescount").append(data.rctr_id + " &nbsp; Liked your profile");
    		  }
    		});
    	}
    	
```
<<<<<<< patch-3
# CodeIgniter - Checking to see if a value already exists in the database

```
There is not a built-in form validation check for whether or not a value is in the database, but you can create your own validation checks.

In your controller, create a method similar to this:

function rolekey_exists($key)
{
    $this->roles_model->role_exists($key);
}
And in your model that handles roles, add something like this:

function role_exists($key)
{
    $this->db->where('rolekey',$key);
    $query = $this->db->get('roles');
    if ($query->num_rows() > 0){
        return true;
    }
    else{
        return false;
    }
}
And then you can write a form validation check like this:

$this->form_validation->set_rules('username', 'Username', 'callback_rolekey_exists');
See this page for more information:

http://ellislab.com/codeigniter/user_guide/libraries/form_validation.html#callbacks
=======
# Routes in Laravel not working after downloaded from CPANEL

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ /index.php?/$1 [L]
>>>>>>> master
```
