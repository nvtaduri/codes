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

```

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

```

# Use eMail class in Controller

```
$this->load->library('email');
		
		//SMTP & mail configuration
		$config = array(
		    'protocol'  => 'smtp',
		    'smtp_host' => 'ssl://smtp.gmail.com',
		    'smtp_port' => 465,
		    'smtp_user' => 'keystroke99@gmail.com',
		    'smtp_pass' => 'tjvhbayegpcpczia',
		    'mailtype'  => 'html',
		    'charset'   => 'utf-8'
		);
		$this->email->initialize($config);
		$this->email->set_mailtype("html");
		$this->email->set_newline("\r\n");

		//Email content
		$htmlContent = '<h1>Test Mail from my APP :)</h1>';
		$htmlContent .= '<p>Reply me if this is working fine :) Thank you.</p>';
		$htmlContent .= '<p><em>Rohini Kumar D</em></p>';

		$this->email->to(array('keystroke99@gmail.com', 'ramsai@proximquestit.com', 'vinod@proximquestit.com', 'vikram@proximquestit.com'));
		$this->email->cc('ramsai@proximquestit.com');
		$this->email->bcc('rohinikumar.d@proximquestit.com');
		$this->email->from('keystroke99@gmail.com','PHPDeveloper');
		$this->email->subject('Testing Email Serivce from CodeIginter');
		$this->email->message($htmlContent);

		//Send email
		$this->email->send();
  
  ```
  
  # Insert Multiple Values (Array of Inputs ) into database Controller Code
  
  ```
  // Add Multiple Contacts

    public function addmultiplecontacts(Request $request) {
        $userInput = $request->all();

        $mobileNo = $request->mobile; // mobile numbers array which is taken as input using name="mobile[]"
        $emails  = $request->email; // emails array which is taken as input using name="email[]"
        $firstNames  = $request->firstname;
        $lastNames  = $request->lastname;

          for($i=0; $i < (count($mobileNo)); $i++) {
            $contact = new Contact;
          $contact->contact_name  = $mobileNo[$i];
          $contact->contact_email  = $emails[$i];
          $contact->contact_mobile  = $firstNames[$i].$lastNames[$i];

          $contact->user_id  = Auth::user()->id;

          $contact->save();
          }
        return back();
  ```
# Laravel Databales Jquery Custom Columns

```
$('#contactsTable').DataTable({
                                    processing: true,
                                    responsive: true,
                                    
                                      "lengthChange": false,
                                    "ajax":{"url":"rendercontacts","dataSrc":""},
                                    // "ajax": "/rendercontacts",
                                    "columns": [
                                      { 
                                          "mData": "Name",
                                                          "mRender": function (data, type, row) {
                                                              return "<input type='checkbox' name='sno' value='{{ $contact->id }}'>";
                                                          }
                                     },
                                      { data: 'contact_name', name: 'contact_name' },
                                      { data: 'contact_email', name: 'contact_email' },
                                      { data: 'contact_mobile', name: 'contact_mobile' },
                                      { data: 'groupname', name: 'groupname' },
                                      { data: 'created_at', name: 'created_at' },
                                      { data: 'status', name: 'status' },
                                      { 
                                          "mData": "Name",
                                                          "mRender": function (data, type, row) {
                                                              return "<select class='editcontact'><option>Select</option><option value='{{$contact->id }}'>Send SMS</option><option value='{{ $contact->id }}'>Edit</option><option value='{{ $contact->id }}'>Delete</option></select>";
                                                          }
                                       }
                                    ]
                                });    // Contacts Page Table
```
