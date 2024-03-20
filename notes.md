# Overview of app

This is a blog app that allows users to sign up and sign in to create posts. You can either be an author or an admin when you sign up.

## Features

- Users can sign up and create their account and their details are stored in a database.
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

define ('ROOT_URL', 'http://localhost/blog');

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

<li> <a href="<?=ROOT_URL ?>blog.php">LOGO</a></li>
<li> <a href="<?=ROOT_URL ?>blog.php">blog</a></li>
<li> <a href="<?=ROOT_URL ?>logout.php">LOGOUT</a></li>
<li> <a href="<?=ROOT_URL ?>admin/index.php">dashboard</a></li>

<script src="<?=ROOT_URL ?>js/main.js"></script>
<link href="<?=ROOT_URL ?>css/styles.css" type="text/css></link>

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

session_start()
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
    die(msqli_error($connection))
}

```

## SIGNUP FUNCTIONALITY IN DATATBASE

After creating the devHangout database, Create a table in the devHangout database on phpmyadmin and name name it `users` having 8 ROWS to match the number of input fields in on the signup form
set the fields in the database as follows, from first row to 8th row:

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

use ROOT_URL signup-logic.php for the form action as with other links
on opening form element in the sign up, use `enctype="multipart/form-data"` and `method="POST"` as attributes

on the signup.php page `require 'config/constants.php'` at the top of the file

### Sign up logic page

Create ``signup-logic.php` file in the root that the submit button on the `signup.php` page leads to and `require 'config/database.php'` in the file.

When you click on the submit button on the sign up page, it will take you to the signup logic page.
also include the following code in the sign up logic file:

```php
// get signup form data if signup button was clicked
if (isset($_POST['submit'])) {
$firstname = filter_var($_POST['firstname'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$lastname = filter_var($_POST['lastname'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$username = filter_var($_POST['username'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
$createpassword = filter_var($_POST['createpassword'], FILTER_SANITIZE_FULL_SPECIAL_CHARS); $confirmpassword = filter_var($_POST['confirmpassword'], FILTER_SANITIZE_FULL_SPECIAL_CHARS);
$avatar = $_FILES['avatar'];


//You are checking for every input field so you have to have everything filled be trying to submit when all fields are filled for you to know if there is any error.

//check opening and closing curly braces for every if statement

//You can use echo command to debug and to check if things are working.

if(!$firstname){
    $_SESSION['signup'] = 'Please enter your firstname';
}elseif (!$lastname){
    $_SESSION['signup'] = 'Please enter your lastname';

    }
    elseif (!$email){
    $_SESSION['signup'] = 'Please enter your email';

    }
    elseif (!$username){
    $_SESSION['signup'] = 'Please enter your usernamename';

    }
    elseif (strlen($createpassword) < 8 || ($confirmpassword) < 8){
    $_SESSION['signup'] = 'Password should be 8+ characters long';

    }
    elseif (!$avatar['name']){
    $_SESSION['signup'] = 'Please add an avatar';
    } else{
      //check if passwords match
    if ($createpassword !== $confirmpassword) {
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
        $time = time(); // uniquie time value to be appended to a
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

          }else{
               $_SESSION['signup'] = "file size too big, should be less than 1MB "

            }
         }else{
               $_SESSION['signup'] = "file should be in png, jpg or jpeg format"
         }

      }
    }

//if button wasn't clicked, and there isn't a successful sign up, and user tries to access any other page that exists after the signup page through browser URL search, redirect back to signup page

if($_SESSION['signup']){
 //pass data back to signup page so that data persists after trying to submit an incomplete form
$_SESSION['signup-data'] = $_POST;

    header('location: ' . ROOT_URL . 'signup.php');
    die();
}else {
   $insert_user_query = "INSERT INTO users (firstname, lastname, username, email, password, avatar) VALUES ('$firstname', '$lastname', '$username', '$email', '$hashed_password', '$avatar_name', 0)";

   if(!mysqli_query($connection)){
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

In the top of the sign-up.php page, write this to keep track of the input fields and get the values whenever there is a submitting on an incomplete form and you want the data to persist on the form: 

```php
<?php
 $firstname = $_SESSION['signup-data']['firstname'] ?? null ;
 $lastname = $_SESSION['signup-data']['lastname'] ?? null ;
 $firstname = $_SESSION['signup-data']['username'] ?? null ;
 $email = $_SESSION['signup-data']['email'] ?? null ;
 $createpassword = $_SESSION['signup-data']['createpassword'] ?? null ;
$confirmpassword= $_SESSION['signup-data']['confirmpassword'] ?? null ;

//delete session

?>
```
Then as attributes on the form inputs write
 `value ="<?= $firstname ?>"` and so on with all other fields




















### Alternative code below to be tested later, use AI to find out what is valid PHP 8 code 


```php
<?php

if (isset($_POST['submit'])) {
  $firstname = filter_var(trim($_POST['firstname']), FILTER_SANITIZE_FULL_SPECIAL_CHARS);
  $lastname = filter_var(trim($_POST['lastname']), FILTER_SANITIZE_FULL_SPECIAL_CHARS);
  $username = filter_var(trim($_POST['username']), FILTER_SANITIZE_FULL_SPECIAL_CHARS);
  $email = filter_var(trim($_POST['email']), FILTER_VALIDATE_EMAIL);

  // Validate username format (example using regular expressions)
  if (!preg_match('/^[a-zA-Z0-9._]+$/', $username)) {
    $_SESSION['signup'] = 'Username should only contain letters, numbers, periods, and underscores.';
    goto no_submit; // Use goto to avoid nested ifs unnecessarily
  }

  // Basic email format check
  if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    $_SESSION['signup'] = 'Please enter a valid email address.';
    goto no_submit;
  }

  $createpassword = filter_var(trim($_POST['createpassword']), FILTER_SANITIZE_FULL_SPECIAL_CHARS);
  $confirmpassword = filter_var(trim($_POST['confirmpassword']), FILTER_SANITIZE_FULL_SPECIAL_CHARS);

  // Check for empty password fields before strlen
  if (empty($createpassword) || empty($confirmpassword)) {
    $_SESSION['signup'] = 'Please enter and confirm your password.';
    goto no_submit;
  }

  if (strlen($createpassword) < 8) {
    $_SESSION['signup'] = 'Password should be at least 8 characters long.';
    goto no_submit;
  }

  // More robust password validation (consider using password_strength libraries)
  // ...

  if ($createpassword !== $confirmpassword) {
    $_SESSION['signup'] = 'Passwords do not match!';
    goto no_submit;
  }

  // File upload validation (example using allowed MIME types)
  $avatar = $_FILES['avatar'];
  $allowed_mime_types = array("image/jpeg", "image/png", "image/gif");
  if (!in_array($avatar['type'], $allowed_mime_types)) {
    $_SESSION['signup'] = 'Invalid avatar file type. Only images (jpeg, png, gif) are allowed.';
    goto no_submit;
  }

  // Hash password securely
  $hashed_password = password_hash($createpassword, PASSWORD_DEFAULT);

  // Use prepared statements to prevent SQL injection
  $stmt = $connection->prepare("INSERT INTO users (firstname, lastname, username, email, password) VALUES (?, ?, ?, ?, ?)");
  $stmt->bind_param("sssss", $firstname, $lastname, $username, $email, $hashed_password);
  $stmt->execute();

  // Check for insertion errors (example using mysqli_error)
  if ($stmt->error) {
    // Log the error or display a generic error message to the user
    $_SESSION['signup'] = 'Registration failed. Please try again later.';
    goto no_submit;
  }

  // Handle successful registration (redirect, etc.)
  // ...

  $stmt->close(); // Close the prepared statement

  no_submit: // Label to jump to instead of nested ifs
} else {
  header('location: ' . ROOT_URL . 'signup.php');
  die();
}
```
