<?php
// task_manager.php

// Start session to store tasks
session_start();

if (!isset($_SESSION['tasks'])) {
    $_SESSION['tasks'] = [];
}

// Add a new task
if (isset($_POST['new_task']) && !empty($_POST['new_task'])) {
    $task = htmlspecialchars($_POST['new_task']);
    $_SESSION['tasks'][] = $task;
}

// Clear all tasks
if (isset($_POST['clear'])) {
    $_SESSION['tasks'] = [];
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>PHP Task Manager</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 400px;
            margin: 80px auto;
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        input[type="text"] {
            width: 70%;
            padding: 8px;
        }
        input[type="submit"] {
            padding: 8px 12px;
            margin-left: 5px;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            background: #eee;
            margin: 5px 0;
            padding: 8px;
            border-radius: 5px;
        }
        .clear-btn {
            margin-top: 10px;
            background: red;
            color: #fff;
            border: none;
            padding: 8px;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
<div class="container">
    <h2>PHP Task Manager</h2>
    <form method="post">
        <input type="text" name="new_task" placeholder="Enter a new task...">
        <input type="submit" value="Add">
    </form>
    <ul>
        <?php foreach ($_SESSION['tasks'] as $task): ?>
            <li><?php echo $task; ?></li>
        <?php endforeach; ?>
    </ul>
    <form method="post">
        <input type="submit" class="clear-btn" name="clear" value="Clear All">
    </form>
</div>
</body>
</html>
