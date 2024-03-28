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
