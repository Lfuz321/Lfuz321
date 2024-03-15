<?php
    $conn = new mysqli('localhost', 'root', '', 'toolhireshops');
    if(!$conn){
        die( 'Error with database ' . mysqli_connect_error() );
    }

    if(isset($_POST['save'])){

        if( isset( $_POST['name'] ) &&
            isset( $_POST['phone'] ) &&
            isset( $_POST['email'] ) &&
            isset( $_POST['address1'] ) &&
            isset( $_POST['address2'] ) &&  
            isset( $_POST['city'] ) &&
            isset( $_POST['postcode'] ) &&
            isset( $_POST['terms'] ) 
        ){

            if( $_POST['name'] &&
                $_POST['phone'] &&
                $_POST['email'] &&
                $_POST['address1'] &&
                $_POST['address2'] &&  
                $_POST['city'] &&
                $_POST['postcode'] &&
                $_POST['terms'] 
            ){
                if($_POST['terms'] == 'on'){

                    $stmt = $conn->prepare( "INSERT INTO `orders`(`name`, `telephone`, `email`, `adress1`, `adress2`, `city`, `postcode`) VALUES (?,?,?,?,?,?,?)" );
                    $stmt->bind_param('sssssss', $_POST['name'], $_POST['phone'], $_POST['email'], $_POST['address1'], $_POST['address2'], $_POST['city'], $_POST['postcode']);
                    $stmt->execute();
                    echo "<p class='success'>Added!</p>";
                }else{
                    echo "<p class='error'>You need to agree with terms!</p>";
                }
            }else{
                echo "<p class='error'>Incomlete data!</p>";
            }
            
        }else{
            echo "<p class='error'>Incomlete data!</p>";
        }

    }

?>

<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Shop</title>
        <link rel="stylesheet" href="style.css">
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
    </head>
    <body>
        
        <div class="header">

            <div class="logo">
                <p>national</p>
                <h3>TOOL HIRE SHOPS</h3>
            </div>

            <div class="info">
                <h3>CALL*0800 808 9600</h3>
            </div>

            <div class="menu">
                <div class="menubutton">
                    <i class="bi bi-house"></i>
                    <p>Home</p>
                </div>
                <div class="menubutton">
                    <i class="bi bi-cart"></i>
                    <p>My Basket</p>
                </div>
            </div>

        </div>

        <div class="main">

            <div class="content">
                <h2>DELIVERY</h2>
                <form method="post">
                    <div class="logo">
                        <p>national</p>
                        <h3>TOOL HIRE SHOPS</h3>
                    </div>
                    <table>
                        <tr>
                            <td><p>Contact name</p></td>
                            <td><input type="text" name="name"></td>
                        </tr>
                        <tr>
                            <td><p>Telephone</p></td>
                            <td><input type="phone" name="phone"></td>
                        </tr>
                        <tr>
                            <td><p>Email</p></td>
                            <td><input type="email" name="email"></td>
                        </tr>
                        <tr>
                            <td><p>Adress 1</p></td>
                            <td><input type="text" name="address1"></td>
                        </tr>
                        <tr>
                            <td><p>Adress 2</p></td>
                            <td><input type="text" name="address2"></td>
                        </tr>
                        <tr>
                            <td><p>City</p></td>
                            <td><input type="text" name="city"></td>
                        </tr>
                        <tr>
                            <td><p>Postcode</p></td>
                            <td><input type="text" name="postcode"></td>
                        </tr>
                        <tr>
                            <td colspan="2"><input type="checkbox" name="terms" id="terms"><label for="terms">I agree to the terms conditions</label></td>
                        </tr>
                        <tr>
                            <td colspan="2"><input type="checkbox" name="register" id="register"><label for="register">Register using these details</label></td>
                        </tr>
                    </table>
                    <div class="control">
                        <button class="cancel">Cancel</button>
                        <input type="submit" name="save" value="Complete">
                    </div>
                </form>
            </div>

            <div class="orderstatus">
                <p>CHECKOUT PROGRESS</p>
                <div class="progresswrap">
                    <div class="progresspoint">
                        <input type="checkbox" checked onclick="return false;">
                        <label>Add items</label>
                    </div>

                    <div class="progresspoint">
                        <input type="checkbox" checked onclick="return false;">
                        <label>Choose your start date</label>
                        <br>
                        <br>
                        <input type="checkbox" checked onclick="return false;">
                        <label>Choose your end date</label>
                    </div>

                    <div class="progressmenu">
                        <div class="purp">Contact Details</div>
                        <div class="black">Next</div>
                        <div class="grey">Order Confirmation</div>
                    </div>

                </div>
            </div>

        </div>

    </body>
</html>
