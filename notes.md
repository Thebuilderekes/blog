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
|-- constants.php
|-- database.php
|--partials
|-header.php
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

Make sure you get the paths right ../ or ../../
Don't forget to end each statement with ;

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

Create ```signup-logic.php`` file that the submit button on the signup page leads to and `require 'config/database.php'` in the file.

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


//You are checking for everythingso you have to be trying to submit when all fields are filled for you to know if there is any error. You echo to check things.

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

      $hashed_passwaord = password_hash($createpassword, PASSWORD_DEFAULT);

      //check if user or email already exists in the database
      $user_check_query = "SELECT * FROM users WHERE username= $username OR email=$email";
      $user_check_result = mysqli_query($connection, $user_check_query);

      if(mysqli_num_rows(user_ceheck_result) > 0){

        $_SESSION['signup'] = 'Username or passowrd already exists!';


      }else {

      }
    }
    }


//if button wasn't clicked, bounce back to signup page
} else { 
    header('Iocation: ' . ROOT_URL . 'signup.php'); 
    die(); 
}
```


