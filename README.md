# Webpage-to-control-the-direction-of-the-robot-movement
## Step 1 : install software
- XAMPP : https://www.apachefriends.org
- VS code : https://code.visualstudio.com/download

## Step 2 : Go to xampp controll panel and start both of apache and MySQL

<img width="664" alt="Screen Shot 2024-07-25 at 3 19 32 AM" src="https://github.com/user-attachments/assets/cc632531-14a0-4028-8084-8ad054105a11">


- go to >xampp>htdocs ، create a folder inside (htdocs) and give it a name.
- open that file in VS code.


## Step 3 : create a database and table and some columns

<img width="1440" alt="Screen Shot 2024-07-25 at 3 26 02 AM" src="https://github.com/user-attachments/assets/69618b32-7306-44a5-a265-e387d2885bb3">


## Step 4 : writing code

- php
````
<?php
// Connect to the database
$servername = "robot";
$username = "your_username";
$password = "your_password";
$dbname = "robott";

$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Get the direction from the request
$direction = $_POST['direction'];

// Update the robot's direction in the database
$sql = "UPDATE robot_positions SET direction = '$direction' WHERE id = 1";

if ($conn->query($sql) === TRUE) {
    echo "Robot direction updated to: " . $direction;
} else {
    echo "Error updating robot direction: " . $conn->error;
}

$conn->close();
?>
````

- html 
````
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Robot Control</title>
  <link rel="stylesheet" href="robot.css">
</head>
<body>
  <h1>Robot Control</h1>
  <div class="button-container">
    <button class="button" id="up">Move Up</button>
    <button class="button" id="down">Move Down</button>
    <button class="button" id="left">Move Left</button>
    <button class="button" id="right">Move Right</button>
  </div>
  <script src="robot.js"></script>
</body>
</html>
````
- css
````
.button {
    padding: 10px 20px;
    font-size: 16px;
    margin: 10px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
````

- js
````
// Function to update the robot's direction in the database
function updateRobotDirection(direction) {
    // Create an XMLHttpRequest object
    const xhr = new XMLHttpRequest();
  
    // Set up the request
    xhr.open('POST', 'update_robot_direction.php', true);
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
  
    // Define the callback function for the request
    xhr.onreadystatechange = function() {
      if (xhr.readyState === XMLHttpRequest.DONE && xhr.status === 200) {
        console.log('Robot direction updated:', direction);
      }
    };
  
    // Send the request with the direction as the payload
    xhr.send('direction=' + direction);
  }
  
  // Add event listeners to the buttons
  document.getElementById('up').addEventListener('click', () => updateRobotDirection('up'));
  document.getElementById('down').addEventListener('click', () => updateRobotDirection('down'));
  document.getElementById('left').addEventListener('click', () => updateRobotDirection('left'));
  document.getElementById('right').addEventListener('click', () => updateRobotDirection('right'));
````

## The result

- <img width="1440" alt="Screen Shot 2024-07-25 at 4 06 49 AM" src="https://github.com/user-attachments/assets/53e06f51-0efd-4198-b699-403b8910ef60">






- <img width="947" alt="Screen Shot 2024-07-25 at 4 15 49 AM" src="https://github.com/user-attachments/assets/fc55e107-fa91-4b42-9adf-a792df6eda66">



