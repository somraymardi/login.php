# login.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration Form</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h2>Create Your Account</h2>
        <form id="registration-form">
            <div class="input-group">
                <label for="name">Full Name</label>
                <input type="text" id="name" name="name" required placeholder="Enter your full name">
            </div>
            <div class="input-group">
                <label for="email">Email</label>
                <input type="email" id="email" name="email" required placeholder="Enter your email">
            </div>
            <div class="input-group">
                <label for="password">Password</label>
                <input type="password" id="password" name="password" required placeholder="Enter your password">
            </div>
            <div class="input-group">
                <button type="submit" id="submit-btn">Register</button>
            </div>
        </form>
        <p id="Form submitted successfully"></p>
    </div>

    <script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ration Card Registration</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h2>Ration Card Registration Form</h2>
        <form id="registration-form">
            <div class="input-group">
                <label for="full-name">Full Name</label>
                <input type="text" id="full-name" name="full-name" required placeholder="Enter your full name">
            </div>
            <div class="input-group">
                <label for="address">Address</label>
                <input type="text" id="address" name="address" required placeholder="Enter your address">
            </div>
            <div class="input-group">
                <label for="aadhaar-number">Aadhaar Number</label>
                <input type="text" id="aadhaar-number" name="aadhaar-number" required placeholder="Enter your Aadhaar number">
            </div>
            <div class="input-group">
                <label for="phone-number">Phone Number</label>
                <input type="text" id="phone-number" name="phone-number" required placeholder="Enter your phone number">
            </div>
            <div class="input-group">
                <button type="submit" id="submit-btn">Submit</button>
            </div>
        </form>
        
        <!-- Success message will appear here --> 
        <p id="form-message"></p>
    </div>
    <script src="script.js"></script>
</body>
</html>
