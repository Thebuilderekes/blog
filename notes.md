# Overview of app

This is a blog app that allows users to sign up and sign in to create posts. You can either be an author or an admin when you sign up.

## Features


- Users are either admins or author. Users are authors by default.
- Users can login using either their username or email.
- Users passwords are being hashed in the database.

- Posts can be made and edited out of their categories.
  This means that if you change the category of a particular post, It would not show up in the search under it's
  former category.
- Posts can be opened by clicking on title to open the entire post on its own page.
- If you logout, and try to access your dashboard throught the URL it redirects you back to the sign in page.

- You can delete a category and the post under the deleted category is going to be set to the uncategorized catego:
- Theres is a file size limit for uploading an avatar.
- There is a file type Check for uploads. Only images are allowed.

### Admin VS Author

#### Admin

- Admin can manage users in the database. They can create featured posts.
- Admin can add and manage users and categories, choose who is an author or an admin

## SIGN UP PAGE

- Usernames must be unique , that is they should not be the same with what is already signed up
  in the database else sign up will not be possible and forms will indicate why if you try to submit.
- Avatar names that are used during sign up are renamed after sign up to make sure that there are no duplicates
  and are uploaded into image folder in the application.
- New users are added as authors by default that can only add and manage posts.
- Users are expected to have at least 8 characters as password.

## SIGN IN PAGE

- Each user has an account
- Users can sign in
- User avatar shows up on nav bar

## HOMEPAGE

### POSTS

- Posts are fetched from the database
- There's going to be only one featured post
- Every post has a category.
- You can click on the category name to list all posts that are under that category.
  Some categories do not have posts.

## BLOG PAGE

### POSTS

- You can search posts by the title
- You can click on the category name to list all posts that are under that category.
- Some categories do not have posts.

## TABLES IN THE DATABASE

users table
post table
categories

- If your iSADMIN = 1 you are an admin
- If your iSADMIN = 0 you are an author

## Folder layout to be made inside htdocs folder in the lammp folder

admin
|--config
|--constants.php
|--database.php
|--manage-users.php
|--manage-category.php  
|--add-users.php
|--add-category.php
|--add-post.php
|--edit-user.php
|--edit-post.php
|--edit-category.php
|--dashboard.php
config
|-- constants.php
|-- database.php
css
|-- styles.css
images
js
|-- main.js
partials
|--header.php
|-footer.php
about.php
blog.php  
category-posts.php  
contact.php  
index.php  
post.php  
services.php  
signin.php
signup.php

OR YOU COULD JUST HAVE ONLY ONE CONFIG FOLDER AND LINK TO OTHER FILES EFFECTIVELY

## Steps to making the files and everything play nicely

- Make sure you get the paths right ../ or ../../
- Don't forget to end each statement with ;
- make sure the links are used with the php tags when linking the files

In `constants.php`

```php
<?PHP

define ('ROOT_URL', 'http://localhost/blog/');

```

In between php open and close PHP tags, using require statement,
require `'config/constants.php'` in the `config/database.php`
require `'config/database.php` in the `'partials/header.php'` and close the php tag. after the require statement in `'partials/header.php'`.
Then right under it, in the `'partials/header.php'`, paste the repeating header code that contains the nav, since we have the nav repeating for all the pages

Then on each page in-between opening and closing php tags,
include `'partials/header.php'`

Do the same for the footer in the `'partials/footer.php'` by copying and pasting the footer code into the file. and including it in all the pages.

INCLUDE THE HEADER.PHP AND FOOTER.PHP PARTIALS IN ALL PAGES USING THE `include` KEYWORD

### For nav the links, script and css link tags

#### nav links

<li> <a href="<?=ROOT_URL ?>blog.php">LOGO</a></li>
<li> <a href="<?=ROOT_URL ?>blog.php">blog</a></li>
<li> <a href="<?=ROOT_URL ?>logout.php">LOGOUT</a></li>
<li> <a href="<?=ROOT_URL ?>admin/index.php">dashboard</a></li>

#### js script tag

<script src="<?=ROOT_URL ?>js/main.js"></script>

#### css link

<link href="<?=ROOT_URL ?>css/styles.css" type="text/css>

and so on for all the links that leads to its own page. Do the same for the script tags and css link tags

LOGGING FUNCTIONALITY
`header.php` in `admin/partials` is where we check who is logged in.

we are going to require `'config/database.php'` in the `admin/partials/header.php` in between opening and closing php tags and it will also include the common pasted header code that includes the
just after, just like the last time with other pages.

### DATABASE SETUP

- Create a database in phpmyadmin named devHangout
-

In the `admin/config/constants.php` and the main `config/constants.php` file put this:

OR YOU COULD JUST HAVE ONLY ONE CONFIG FOLDER AND HAVE THIS IN HERE AND LINK TO OTHER FILES EFFECTIVELY

```php

<?php

session_start();
define('ROOT_URL', 'http://localhost/blog/');
define('DB_HOST', 'localhost');
define('DB_USER', 'Ekeopre');
define('DB_PASS', 'dev91$$'); //password of database
define('DB_NAME', 'devHangout'); // name of the database

```

In the `admin/config/database.php` write

```php

<?php
require 'constants.php';

//connect to the database
$connection = new mysqli(DB_HOST, DB_USER, DB_PASS, DB_NAME);

if (mysqli_errno($connection)){
    //alternate way to write the if statement
  //if ($connection-> connect_errno)
    die(msqli_error($connection));
}

```

## SIGNUP FUNCTIONALITY IN DATABASE

After creating the devHangout database, Create a table in the devHangout database on phpmyadmin and name name it `users` having 8 ROWS to match the number of input fields in on the signup form
set the fields in the database as follows, from first row to 8th row:

         1col, 2col, 3col, 4col, 5col, 6col

1 row -> id, type - INT, length - 11, default-none, attributes- unsigned, index- primary
2 row -> firstname, type - VARCHAR, length - 50
3 row -> lastname, type - VARCHAR, length - 50
4 row -> username, type - VARCHAR, length - 50
5 row -> email, type - VARCHAR, length - 100
6 row -> password, type - VARCHAR, length - 255 (because of hashing)
7 row -> avatar, type - VARCHAR, length - 255 (because of hashing)
8 row -> is_admin, type - TINYINT, length - 1 (because of hashing)
THEN SAVE.

## SIGNUP FORM LOGIC

## SIGN UP PHP PAGE ALERT MESSAGE

Check image file in assets folder to see require code and code placement for alert message

use ROOT_URL signup-logic.php for the form action as with other links
on opening form element in the sign up, use `enctype="multipart/form-data"` and `method="POST"` as attributes

on the signup.php page `require 'config/constants.php'` at the top of the file

## SIGN UP LOGIC PHP PAGE

Create ``signup-logic.php` file in the root that the submit button on the `signup.php` page leads to and `require 'config/database.php'` in the file.

When you click on the submit button on the sign up page, it will take you to the signup logic page.
also include the following code in the sign up logic file:

```php
<?php
// get signup form data method is POST
if($_SERVER['REQUEST_METHOD'] === 'POST') {
$firstname =  htmlspecialchars(
filter_var($_POST['firstname'], FILTER_SANITIZE_FULL_SPECIAL_CHARS));
$lastname = htmlspecialchars(
filter_var($_POST['lastname'], FILTER_SANITIZE_FULL_SPECIAL_CHARS));
$username = filter_var($_POST['username'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
$createpassword = filter_var($_POST['createpassword'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$confirmpassword = filter_var($_POST['confirmpassword'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$avatar = $_FILES['avatar'];


//You are checking for every input field so you have to have everything filled be trying to submit when all fields are filled for you to know if there is any error.

//check opening and closing curly braces for every if statement

//You can use echo command to debug and to check if things are working.

if(!$firstname){
    $_SESSION['signup'] = 'Please enter your first name';
}elseif (!$lastname){
    $_SESSION['signup'] = 'Please enter your last name';

    }
    elseif (!$email){
    $_SESSION['signup'] = 'Please enter your email';

    }
    elseif (!$username){
    $_SESSION['signup'] = 'Please enter your username';

    }
    elseif (strlen($createpassword) < 8 || ($confirmpassword) < 8){
    $_SESSION['signup'] = 'Password should be 8+ characters long';

    }
    elseif (!$avatar['name']){
    $_SESSION['signup'] = 'Please add an avatar';
    } else{
      //check if passwords match
    if ($createpassword !== $confirmpassword) {
      //alternative if($_POST['createpassword'] !== $_POST['confirmpassword'])
        $_SESSION['signup'] = 'Passwords do not match!';
    }else {

      $hashed_password = password_hash($createpassword, PASSWORD_DEFAULT);

      //check if user or email already exists in the database
      $user_check_query = "SELECT * FROM users WHERE username= $username OR email=$email";
      $user_check_result = mysqli_query($connection, $user_check_query);

      if(mysqli_num_rows(user_check_result) > 0){

        $_SESSION['signup'] = 'Username or password already exists!';


      }else {

        // work on avatar by using time function to create a unique identifier for the name of each image getting uploaded
        $time = time(); // unique time value to be appended to a
        $avatar_name = $time . $avatar['name'];
        $avatar_tmp_name = $avatar['tmp_name']; //temporary name of file
         $avatar_destination_path = 'image/'. $avatar_name;

         // make sure that file is an image
         $allowed_file_format = ['png', 'jpg', 'jpeg'];
         $file_extension = explode('.', $avatar_name);
         $file_extension = end($file_extension);

         if(in_array($file_extension, $allowed_file_format)){

          //check for image size
          if($avatar['size'] < 1000000){
                 //upload avatar
                        move_uploaded_file($avatar_tmp_name, $avatar_destination_patih)

          }else{
               $_SESSION['signup'] = "file size too big, should be less than 1MB "

            }
         }else{
               $_SESSION['signup'] = "file should be in png, jpg or jpeg format"
         }

      }
    }

//if button wasn't clicked, and there isn't a successful sign up, and user tries to access any other page that exists after the signup page through browser URL search, redirect back to signup page

if(isset($_SESSION['signup'])){
 //pass data back to signup page so that data persists after trying to submit an incomplete form
$_SESSION['signup-data'] = $_POST;

    header('location: ' . ROOT_URL . 'signup.php');
    die();
}else {
     // if evertything went well and sign up was successful insert user into the users table with below code
  //watch the video and edit this section if it doesn't work
   $insert_user_query = "INSERT INTO users (firstname, lastname, username, email, password, avatar, is_admin) VALUES ('$firstname', '$lastname', '$username', '$email', '$hashed_password', '$avatar_name', 0)";
   //leave comment content saying thank you and point that the issue at 2:44:41 to say that the issue was at line 76 for the closing bracket for VALUES
 //watch the video and edit this section if it doesn't work

   $insert_user_result = mysqli_query($connection, $insert_user_query);
   if(!mysqli_errno($connection)){
      // alternative way of writing this if statement
    //if(!$connection -> connect_errno  )
     // redirect to login page with success message
     $_SESSION['signup-success'] = "User created successfully";
     header('location: ' . ROOT_URL . 'signin.php');
     die();
   }else {
     $_SESSION['signup'] = "Couldn't create user";
     header('location: ' . ROOT_URL . 'signup.php');
     die();
   }
   }

}
} else {
    header('location: ' . ROOT_URL . 'signup.php');
    die();
}
```

In the top of the sign-up.php page, write this code below to keep track of the input fields and get the values whenever the user is a submitting on an incomplete form and you want the data to persist on the form while showing the alert messages:

```php
<?php
 $firstname = $_SESSION['signup-data']['firstname'] ?? null ;
 $lastname = $_SESSION['signup-data']['lastname'] ?? null ;
 $username = $_SESSION['signup-data']['username'] ?? null ;
 $email = $_SESSION['signup-data']['email'] ?? null ;
 $createpassword = $_SESSION['signup-data']['createpassword'] ?? null ;
 $confirmpassword= $_SESSION['signup-data']['confirmpassword'] ?? null ;

//delete session
unset($_SESSION['signup-data'])

?>
```

Then as attributes on the form inputs write
`value ="<?= $firstname ?>"` and so on with all other fields

## SIGN IN PHP PAGE

At the top of the sign-in.php page, write this code below to keep track of the input fields and get the values whenever the user is a submitting on an incomplete form or experiencing any problem and you want the data to persist on the form while showing the alert messages:

```php
<?php
 $username_email = $_SESSION['signin-data']['username_email'] ?? null ;
 $password = $_SESSION['signin-data']['password'] ?? null ;



//delete session
unset($_SESSION['signin-data'])

?>
```

Then as attributes on the sign in htmlk form inputs write
`value ="<?= $username_email ?>"` and same with the password input

### ALERT MESSAGE PLACEMENT

Check image file in assets folder to see require code and code placement for alert message.
instead OF 'signup' use 'signin'

## SIGN IN LOGIC PHP PAGE

create a sign in logic.php file and write in it the following:

```php
<?php
require 'config/database.php';

if($_SERVER['REQUEST_METHOD'] === 'POST'){
  //get form data
   $username_email = htmlspecialchars($_POST['username_email']) //check this later to see if it needs to be changed for security purposes
   $password = htmlspecialchars($_POST['password'])

   if(empty($_POST['username_email'])){
    $_SESSION['signin'] = "username or Email required";

   }elseif(empty($_POST['password'])){
    $_SESSION['signin'] = "Password required";
   } else {

    //fetch user from database
    $fetch_user_query = "SELECT * FROM users WHERE username='$username_email' OR email= '$username_email'";
    $fetch_user_result = mysqli_query($connection, $fetch_user_query);

    if(mysqli_num_rows($fetch_user_result) == 1){
           // user found, so convert the user's record into assoc array
           $user_record = mysqli_fetch_assoc($fetch_user_result);

           // get user's password
           $db_password = $user_record['password']

           //check if the user's form password matches the user password in the database. ``password_verify()`` decrypts the hased password in thedatabase
            if(password_verify($password, $db_password)){

                // set session for access control. This is where user id comes in
                  $_SESSION['user-id'] = $user_record['id'];

                  //set session if user is an admin i.e if is_admin has a value of 1
                  if($user_record['is_admin'] == 1){
                    $SESSION['user_is_admin'] = true;
                  }
                  header('location:' . ROOT_URL . 'admin/');
           }else {

             $_SESSION['signin'] = "Please check your input and try again";

           }

           }else {

             $_SESSION['signin'] = "User not found";

           }

   }

   //if there is a problem redirect user to signin page
   if(isset[$SESSION['signin']]){
        $_SESSION['signin-data'] = $_POST;
        header('location:' . ROOT_URL . 'signin.php');
        die();
   }

} else {
    header('location: ' . ROOT_URL . 'signin.php');
    die();
}

```

## Manage-categories, manage-users and index.php files to conditionally render list options

In manage-categories.php file, condionally render some of the options according to the value of `user-id`,
check image file in assets folder to see how it is done.

write

```
<?php endif?>
```

after the last list item just before closing ul tag in `manage-categories.php`

To check if the user is logged in we use the `user-id` to conditionally render the logged in and sign in links on the navigation menu bar

Check logged-in-rendering.jpg image to see how to set it in all `header.php` files fou8nd in `./partials` and `/admin/header.php`

### in the ./partials/header.php file

```php
<?php
if(isset($_SESSION['user-id'])){
    // working on displaying the avatar that matches the user based on the user-id
    $id = filter_var($_SESSION['user-id'], FILTER_SANITIZE_NUMBER_INT);
    $query = "SELECT avatar FROM users WHERE id=$id ";
    $result = mysqli_query($connection, $query);
    $avatar = mysqli_fetch_assoc($result);
}
```

then on the `header.php` page that has the image avatar in the navigation bar, set:

``<img src="<?= ROOT_URL . 'images/' . $avatar['avatar']" >` this will display the user's avatar according too the matching user who is logged in

### admin/partials/header.php

```php
<?php
require '/partials/header.php file'

if(isset($_SESSION['user-id'])){

    header('location: ' . ROOT_URL . 'signin.php');
    die();

}
```

### in the logout.php file

```php
<?php
require 'config/constants.php';
//destroy all sessions and redirect to home page
session_destroy();

    header('location: ' . 'ROOT_URL');
   die()

```

## Add user logic

### create add-user-logic.php file

write this code in there, which is basically same code as in sign-up logic page. Note that all the repetition of code would be different if all of this was being done with OOP style.

```php
<?php
// if form data method is POST
if($_SERVER['REQUEST_METHOD'] === 'POST') {
$firstname =  htmlspecialchars(
filter_var($_POST['firstname'], FILTER_SANITIZE_FULL_SPECIAL_CHARS));
$lastname = htmlspecialchars(
filter_var($_POST['lastname'], FILTER_SANITIZE_FULL_SPECIAL_CHARS));
$username = filter_var($_POST['username'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
$createpassword = filter_var($_POST['createpassword'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$confirmpassword = filter_var($_POST['confirmpassword'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$is_admin = filter_var($_POST['userrole'], FILTER_SANITIZE_NUMBER_INT);
$avatar = $_FILES['avatar'];


//You are checking for every input field so you have to have everything filled be trying to submit when all fields are filled for you to know if there is any error.

//check opening and closing curly braces for every if statement

//You can use echo command to debug and to check if things are working.

//validate input values
if(!$firstname){
    $_SESSION['add-user'] = 'Please enter your first name';
}elseif (!$lastname){
    $_SESSION['add-user'] = 'Please enter your last name';

    }
    elseif (!$email){
    $_SESSION['add-user'] = 'Please enter your email';

    }
    // you can omit this check if it causes issues but first experiment with it
    //    elseif (!$is_admin === 0 || !$is_admin === 1 ){
    // $_SESSION['add-user'] = 'Please select a user role';
    // }

    elseif (!$username){
    $_SESSION['add-user'] = 'Please enter your username';

    }
    elseif (strlen($createpassword) < 8 || ($confirmpassword) < 8){
    $_SESSION['add-user'] = 'Password should be 8+ characters long';

    }
    elseif (!$avatar['name']){
    $_SESSION['add-user'] = 'Please add an avatar';
    } else{
      //check if passwords match
    if ($createpassword !== $confirmpassword) {
        $_SESSION['add-user'] = 'Passwords do not match!';
    }else {

      $hashed_password = password_hash($createpassword, PASSWORD_DEFAULT);

      //check if user or email already exists in the database
      $user_check_query = "SELECT * FROM users WHERE username= $username OR email=$email";
      $user_check_result = mysqli_query($connection, $user_check_query);

      if(mysqli_num_rows(user_check_result) > 0){

        $_SESSION['add-user'] = 'Username or password already exists!';


      }else {

        // work on avatar by using time function to create a unique identifier for the name of each image getting uploaded
        $time = time(); // unique time value to be appended to a
        $avatar_name = $time . $avatar['name'];
        $avatar_tmp_name = $avatar['tmp_name']; //temporary name of file
         $avatar_destination_path = '../images/'. $avatar_name;

         // make sure that file is an image
         $allowed_file_format = ['png', 'jpg', 'jpeg'];
         $file_extension = explode('.', $avatar_name);
         $file_extension = end($file_extension);

         if(in_array($file_extension, $allowed_file_format)){

          //check for image size
          if($avatar['size'] < 1000000){

          //upload avatar
           move_uploaded_file($avatar_tmp_name, $avatar_destination_patih)

          }else{
               $_SESSION['add-user'] = "file size too big, should be less than 1MB "

            }
         }else{
               $_SESSION['add-user'] = "file should be in png, jpg or jpeg format"
         }

      }


//if button wasn't clicked, and there isn't a successful sign up, and user tries to access any other page that exists after the add-user page through browser URL search, redirect back to add-user page

if(isset($_SESSION['add-user'])){
 //pass data back to add-user page so that data persists after trying to submit an incomplete form
$_SESSION['add-user-data'] = $_POST;

    header('location: ' . ROOT_URL . 'admin/add-user.php');
    die();
}else {
     // if everything went well and sign up was successful insert user into the users table with below code
  //watch the video and edit this section if it doesn't work 3:44:00
   $insert_user_query = "INSERT INTO users (firstname, lastname, username, email, password, avatar, is_admin) VALUES ('$firstname', '$lastname', '$username', '$email', '$hashed_password', '$avatar_name', $is_admin)";
   //leave comment content saying thank you and point that the issue at 2:44:41 to say that the issue was at line 76 for the closing bracket for VALUES
 //watch the video and edit this section if it doesn't work

   $insert_user_result = mysqli_query($connection, $insert_user_query);
   if(!mysqli_errno($connection)){
      // alternative way of writing this if statement
    //if(!$connection -> connect_errno  )
     // redirect to login page with success message
     $_SESSION['add-user-success'] = "New user $firstname $lastname added successfully";
     header('location: ' . ROOT_URL . 'admin/manage-users.php');
     die();
   }else {
     $_SESSION['signup'] = "Couldn't create user";
     header('location: ' . ROOT_URL . 'admin/add-user.php');
     die();
   }
   }

}

} else {
      header('location: ' . ROOT_URL . 'admin/add-user.php');
    die();

}

```

### in the add-user.php page

use the following code to persist the form data if there was an error

```php
<?php
 $firstname = $_SESSION['add-user-data']['firstname'] ?? null ;
 $lastname = $_SESSION['add-user-data']['lastname'] ?? null ;
 $username = $_SESSION['add-user-data']['username'] ?? null ;
 $email = $_SESSION['add-user-data']['email'] ?? null ;
 $createpassword = $_SESSION['add-user-data']['createpassword'] ?? null ;
 $confirmpassword= $_SESSION['add-user-data']['confirmpassword'] ?? null ;
//  $is_admin= $_SESSION['add-user-data']['userrole'] ?? null ; dont use this


//delete session
unset($_SESSION['add-user-data'])

?>
```

set the following in the add user form:
`<form action = "<?= ROOT_URL ?> admin/add-user-logic.php" enctype="multipart/form-data" method = "POST">`  
 give names to all the inputs in the form,
Then as attributes on the form inputs write
`value ="<?= $firstname ?>"` and so on with all other fields

```
<select name ="user-role">
<input name="avatar">

```

Check add-user-php-alert image for message alert format
`unset($_SESSION['add-user'])` is the complete code in the image
 

## in the manage-users php page

// fetch user from databhase that is not the current logged in user to prevent us from being able to delete ourselves from the database when we are logged in

```php 
<?php
include 'partials/header.php'

$current_admin_id = $_SESSION['user-id']; // get the id of the current user

$query = "SLECT * FROM users WHERE NOT id=$current_admin_id" //search the user table and gety the id og the user that is not the current user id
```





