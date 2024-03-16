 # Overview of app
 This is a blog app that allows users to sign up and sign in to create posts. You can either be an author or an admin when you sign up.
 - Posts can be made and edited out of their categories. This means that if you change the category of a particular post, It would not show up in the search of the post like when it was made under the former category.


SIGN UP
- Usernames should not be the same with what is already signed up in the database else sign up will not be possible and forms will indicate why if you try to submit.
- Avatar names that are used during sign up are renamed after sign up to make sure that there are no duplicates
- New users are added as authors that can only add and manage posts

SIGN IN
- Each user has an account
- Users can sign in
- User avatar shows up on nav bar 

### ADMIN VS AUTHOR
- Admin can manage users in the database
- Admin can add and manage categories



HOMEPAGE
## POSTS
- Posts are fetched from the database
- There's going to be only one featured post
- Every post has a category. 
- You can click on the category name to list all posts that are under that category. Some categories do not have posts.

BLOG PAGE
## POSTS
- You can search posts by the title
- You can click on the category name to list all posts that are under that category. Some categories do not have posts.
Pots

## TABLES IN THE DATABASE
users table
post table
categories

- If your iSADMIN = 1 you are an admin
- If your iSADMIN = 0 you are an author