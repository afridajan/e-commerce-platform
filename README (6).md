
 e-commerce website(Developement)

 System Architecture:
Backend: For backend  part we have used NodeJS a JavaScript runtime environment with Express framework and python flask.
Frontend : For the Frontend we have used Html and CSS     
a. HTML: HTML stands for Hyper Text Markup Language. It is used to create webpages.Html has elements which tells the browser how to display the content.
b. CSS: CSS is the language we use to style an HTML document.CSS describes how the html elements should be displayed
          c. JavaScript:  Is used to program the behavior of web pages.
Implementing user login,registration,user authentication,and checkout functionality.
Source code:
User login,registration:
Front end :(login.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Login - Artisan Marketplace</title>
</head>
<body>
    <div class="login-container">
        <h2>Login</h2>
        <form id="loginForm">
            <label for="username">Username:</label>
            <input type="text" id="username" name="username" required>


            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>


            <button type="button" onclick="login()">Login</button>
        </form>
    </div>


    <script src="login.js"></script>
</body>
</html>

Back end:(login.js)
function login() {
    var username = document.getElementById("username").value;
    var password = document.getElementById("password").value;


    // Send a POST request to the server
    fetch("/login", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({ username: username, password: password })
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            // Redirect to dashboard or another authenticated page
            window.location.href = "/dashboard";
        } else {
            alert("Invalid username or password");
        }
    })
    .catch(error => console.error("Error:", error));
}


python:(app.py)
from flask import Flask, render_template, request, jsonify


app = Flask(__name__)


# Replace these values with your actual database connection details
users = {
    "john": {"password": "johnhere"},
    "jane": {"password": "janehere"}
}


@app.route('/')
def index():
    return render_template('login.html')


@app.route('/login', methods=['POST'])
def login():
    data = request.get_json()
    username = data.get('username')
    password = data.get('password')


    if username in users and check_password(users[username]['password'], password):
        return jsonify({'success': True})
    else:
        return jsonify({'success': False})


def check_password(hashed_password, user_password):
    # Implement your password hashing and verification logic here
    # For simplicity, we'll compare plain text passwords in this example
    return hashed_password == user_password
if __name__ == '__main__':
app.run(debug=True)
Checkout functionality:
Front end:(checkout.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Checkout - Artisan Marketplace</title>
</head>
<body>
    <div class="checkout-container">
        <h2>Checkout</h2>
        <form id="checkoutForm">
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required>


            <label for="address">Address:</label>
            <textarea id="address" name="address" required></textarea>


            <button type="button" onclick="completeCheckout()">Complete Checkout</button>
        </form>
    </div>


    <script src="checkout.js"></script>
</body>
</html>


Back end:(checkout.js)
function completeCheckout() {
    var name = document.getElementById("name").value;
    var address = document.getElementById("address").value;


    // Dummy product details for demonstration purposes
    var products = [
        { id: 1, name: "Handcrafted Mug", price: 15.99 },
        { id: 2, name: "Artisan Soap Set", price: 24.99 }
    ];


    // Calculate the total price
    var totalPrice = products.reduce((total, product) => total + product.price, 0);


    // Send a POST request to the server for processing
    fetch("/checkout", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({ name: name, address: address, products: products, totalPrice: totalPrice })
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            // Display success message or redirect to a thank you page
            alert("Checkout successful!");
        } else {
            // Display error message
            alert("Checkout failed. Please try again.");
        }
    })
    .catch(error => console.error("Error:", error));
}


python:(app1.py)
from flask import Flask, render_template, request, jsonify


app = Flask(__name__)


@app.route('/')
def index():
    return render_template('checkout.html')


@app.route('/checkout', methods=['POST'])
def checkout():
    data = request.get_json()
    name = data.get('name')
    address = data.get('address')
    products = data.get('products')
    totalPrice = data.get('totalPrice')


    # Implement actual checkout logic here (e.g., update database, process payment, etc.)
    # For simplicity, we'll just return a success response
    return jsonify({'success': True})


if __name__ == '__main__':
    app.run(debug=True)


