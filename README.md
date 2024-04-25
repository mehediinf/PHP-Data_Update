# PHP-Data_Update

#First Page ............>


<head>
    <link rel="stylesheet" href="style.css">
</head>

<body>

<?php 
    $con = mysqli_connect('localhost','root','','student');
    $query = "SELECT *FROM std_info";
    $result = mysqli_query($con,$query);

    $count = mysqli_num_rows($result);

    if($count>0){

        if(isset($_REQUEST['updated'])){
            echo "<font color='green'>Data Updated </font>";
        }

    ?>
    <table class="table">
        <thead class="thead-dark">

        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
            <th>Password</th>
            <th>Action</th>
        </tr>

        </thead>
    <?php
    
        while($row = mysqli_fetch_assoc($result)){

            $id = $row['id'];
            $username = $row['username'];
            $email = $row['email'];
            $password = $row['password'];

    ?>
            <tbody>           
                <tr>
                    <td><?php echo $id;  ?></td>
                    <td><?php echo $username;  ?></td>
                    <td><?php echo $email;  ?></td>
                    <td><?php echo $password;  ?></td>
                    <td><a href="single_data_update.php?id=<?php echo $id;?>">Edit</a> || <a href="delete.php?id=<?php echo $id;?>">Delete</a></td>
                </tr>
             </tbody>
                     
<?php

        }

    }
    ?>
    </table>
    <?php
    


?>


    
</body>






#Second Page ............>


<head>
    <link rel="stylesheet" href="style.css">
</head>

<body>



<?php 


    $con = mysqli_connect('localhost','root','','student');


    if(isset($_REQUEST['id'])){
        $Rcvd_id = $_REQUEST['id'];
        $query = "SELECT *FROM std_info WHERE id = $Rcvd_id";
        $result = mysqli_query($con,$query);


        while($row=mysqli_fetch_assoc($result)){
           


?>

        <form action="update_data.php" method="post">

            <input type="text" name="username" value="<?php echo $row['username']; ?>" placeholder="username">
            <input type="email" name="email" value="<?php echo $row['email']; ?>" placeholder="email">
            <input type="password" name="password" value="<?php echo $row['password']; ?>" placeholder="password">
            <input type="submit" name="submit" value="Update">
            <input type="hidden" name="updating_hidden_id" value="<?php echo $Rcvd_id; ?>">

        </form>

<?php        

        }


    }

    
    ?>
    


    
</body>






#Third Page ............>





<head>
    <link rel="stylesheet" href="style.css">
</head>

<body>


<?php 
    $con = mysqli_connect('localhost','root','','student');


    if(isset($_REQUEST['submit'])){

            $username = $_REQUEST['username'];
            $email = $_REQUEST['email'];
            $password = $_REQUEST['password'];
            $hidden_id = $_REQUEST['updating_hidden_id'];
        
            
            $update_query = "UPDATE std_info SET username='$username',email='$email',password='$password' WHERE id=$hidden_id";

            $final_update_query = mysqli_query($con,$update_query);

            if($final_update_query){
                header("location: home.php?updated");
            }

    }
  

?>

    
</body>




