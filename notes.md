 # Overview of app
 This is a blog app that allows users to sign up and sign in to create posts. You can either be an author or an admin when you sign up.

## Features
 - Users can sign up and create their account and their details are stored in a database.
 - Users are either admins or author. Users are authors by default.
 - Users can login using either their username or email.
 - Users passwords are being hashed in the database.
 - Posts can be made and edited out of their categories. This means that if you change the category of a particular post, It would not show up in the search under it's former category.
 - Posts can be opened by clicking on title to open the entire post on its own page. 
 - If you logout, and try to access your dashboard throught the URL it redirects you back to the sign in page.
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
- Users are expecpected to have at least 8 characters as password.




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
