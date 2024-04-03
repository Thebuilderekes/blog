# blog
## Functions used in this project (study them)
filter_var()
htmlspecialchars()
move_uploaded_file()
isset()
password_hash()
die()
in_array()
mysqli_fetch_assoc()
mysqli_query()
unlink()

## Key structure
- All forms page has a corresponding logic page for the logic that controls the form

- On the edit user page, the data of the user is gotten according to the user id from the database

- Logged in admin will not  be able to see themselves in the list of registerd users therefore will not be able to select and delete own account from the frontend.



### Common patterns to used in project and the meaning

- Whenever you are checking ``if (isset($_SESSION['name_of_data']))`` you are checking if there is an error when getting the ``name_of_data`` in your session so you can conditionally set your alert message in PHP web page file according to value of the string that you set for the message for that ``$_SESSION`` in your logic php file 
