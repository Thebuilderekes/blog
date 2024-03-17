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


In ```constants.php```

```php
<?PHP

define ('ROOT_URL', 'http://localhost/blog');

```

In between php open and close PHP tags, using require statement,
require  ``'config/constants.php'`` in the ``config/database.php``
require  ``'config/database.php`` in the ``'partials/header.php'`` and close the php tag. after the require statement in ``'partials/header.php'``.
Then right under it, in the ``'partials/header.php'``, paste the repeating header code that contains the nav,  since we have the nav repeating for all the pages

Then on each page in-between opening and closing php tags,
include ``'partials/header.php'``

Do the same for the footer in the ``'partials/footer.php'`` by copying and pasting the footer code into the file. and including it in all the pages.

### For nav the links, script and css link tags
<li> <a href="<?=ROOT_URL ?>blog.php">LOGO</a></li>
<li> <a href="<?=ROOT_URL ?>blog.php">blog</a></li>
<li> <a href="<?=ROOT_URL ?>logout.php">LOGOUT</a></li>
<li> <a href="<?=ROOT_URL ?>admin/index.php">dashboard</a></li> 

<script src="<?=ROOT_URL ?>js/main.js"></script>
<link href="<?=ROOT_URL ?>css/styles.css" type="text/css></link> 

 and so on for all the links that leads to its own page. Do the same for the script tags and css link tags


 LOGGING FUNCTIONALITY
``header.php`` in ``admin/partials`` is where we check who is logged in.

we are going to require ``'config/database.php'`` in the  ``admin/partials/header.php`` in between opening and closing php tags and it will also include the common pasted header code that includes the 
just after, just like the last time with other pages.


### DATABASE SETUP

- Create a database in phpmyadmin named devHangout
- 



In the ```admin/config/constants.php``` and the main ```config/constants.php``` file put this:

OR YOU COULD JUST HAVE ONLY ONE CONFIG FOLDER AND HAVE THIS IN HERE AND LINK TO OTHER FILES EFFECTIVELY

```php

<?php
define('ROOT_URL', 'http://localhost/blog/');
define('DB_HOST', 'localhost');
define('DB_USER', 'Ekeopre');
define('DB_PASS', 'dev91$$'); //password of database
define('DB_NAME', 'devHangout'); // name of the database

```

In the ```admin/config/database.php``` write

```php

<?php
require 'constants.php';

//connect to the database
$connection = new mysqli(DB_HOST, DB_USER, DB_PASS, DB_NAME);

if (mysqli_errno($connection)){
    die(msqli_error($connection))
}

``


## SIGNUP FUNCTIONALITY IN DATATBASE
Create a table in the devHangout database with name "users" having 8 columns to match the number of sign up input requirement





