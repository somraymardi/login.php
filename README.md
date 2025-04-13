# login.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login and Registration App</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css">
    <style>
        body {
            background-color: #f2f2f2;
        }
        .container {
            max-width: 400px;
            margin-top: 50px;
            padding: 20px;
            background-color: #fff;
            border: 1px solid #ddd;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .tab-content {
            padding: 20px;
        }
    </style>
</head>
<body>
    <div id="login-container" class="container">
        <ul class="nav nav-tabs" id="myTab" role="tablist">
            <li class="nav-item" role="presentation">
                <button class="nav-link active" id="login-tab" data-bs-toggle="tab" data-bs-target="#login" type="button" role="tab" aria-controls="login" aria-selected="true">Login</button>
            </li>
            <li class="nav-item" role="presentation">
                <button class="nav-link" id="register-tab" data-bs-toggle="tab" data-bs-target="#register" type="button" role="tab" aria-controls="register" aria-selected="false">Register</button>
            </li>
        </ul>
        <div class="tab-content" id="myTabContent">
            <div class="tab-pane fade show active" id="login" role="tabpanel" aria-labelledby="login-tab">
                <h2>Login</h2>
                <form id="login-form">
                    <div class="form-group">
                        <label for="username">Username:</label>
                        <input type="text" class="form-control" id="username" placeholder="Enter username">
                    </div>
                    <div class="form-group">
                        <label for="password">Password:</label>
                        <input type="password" class="form-control" id="password" placeholder="Enter password">
                    </div>
                    <button type="button" class="btn btn-primary" onclick="loginUser()">Login</button>
                </form>
            </div>
            <div class="tab-pane fade" id="register" role="tabpanel" aria-labelledby="register-tab">
                <h2>Register</h2>
                <form id="register-form">
                    <div class="form-group">
                        <label for="reg-username">Username:</label>
                        <input type="text" class="form-control" id="reg-username" placeholder="Enter username">
                    </div>
                    <div class="form-group">
                        <label for="reg-password">Password:</label>
                        <input type="password" class="form-control" id="reg-password" placeholder="Enter password">
                    </div>
                    <div class="form-group">
                        <label for="reg-confirm-password">Confirm Password:</label>
                        <input type="password" class="form-control" id="reg-confirm-password" placeholder="Confirm password">
                    </div>
                    <button type="button" class="btn btn-primary" onclick="registerUser()">Register</button>
                </form>
            </div>
        </div>
        <div class="modal fade" id="messageModal" tabindex="-1" role="dialog" aria-labelledby="messageModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="messageModalLabel">Message</h5>
                        <button type="button" class="close" data-bs-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <p id="message"></p>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div id="home-container" style="display: none;" class="container">
        <h2>Welcome, <span id="username-display"></span>!</h2>
        <p>You are now logged in.</p>
        <button class="btn btn-primary" onclick="logoutUser()">Logout</button>
    </div>

    <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
    <script>
        var users = JSON.parse(localStorage.getItem("users")) || [];

        function registerUser() {
            var username = document.getElementById("reg-username").value;
            var password = document.getElementById("reg-password").value;
            var confirmPassword = document.getElementById("reg-confirm-password").value;

            if (username && password && confirmPassword) {
                if (password === confirmPassword) {
                    var existingUser = users.find(user => user.username === username);
                    if (!existingUser) {
                        users.push({ username: username, password: password });
                        localStorage.setItem("users", JSON.stringify(users));
                        document.getElementById("message").innerHTML = "Registration successful!";
                        $('#messageModal').modal('show');
                        document.getElementById("reg-username").value = "";
                        document.getElementById("reg-password").value = "";
                        document.getElementById("reg-confirm-password").value = "";
                    } else {
                        document.getElementById("message").innerHTML = "Username already exists!";
                        $('#messageModal').modal('show');
                    }
                } else {
                    document.getElementById("message").innerHTML = "Passwords do not match!";
                    $('#messageModal').modal('show');
                }
            } else {
                document.getElementById("message").innerHTML = "Please fill in all fields!";
                $('#messageModal').modal('show');
            }
        }

        function loginUser() {
            var username = document.getElementById("username").value;
            var password = document.getElementById("password").value;

            if (username && password) {
                var user = users.find(user => user.username === username && user.password === password);
                if (user) {
                    document.getElementById("username-display").innerHTML = username;
                    document.getElementById("login-container").style.display = "none";
                    document.getElementById("home-container").style.display = "block";
                } else {
                    document.getElementById("message").innerHTML = "Invalid username or password!";
                    $('#messageModal').modal('show');
                }
            } else {
                document.getElementById("message").innerHTML = "Please fill in all fields!";
                $('#messageModal').modal('show');
            }
        }

        function logoutUser() {
            document.getElementById("login-container").style.display = "block";
            document.getElementById("home-container").style.display = "none";
        }
    </script>
</body>
</html>
