
e-commerce platform
   welocome to our e-commerce website Artisanal's touch where you can buy the handmade products.
 

Our e-commerce platform provides the following objects:

Home page:
 Shopping Cart:
   A virtual cart or basket on an e-commerce website where users can add products they intend to purchase. 
   It's a temporary storage mechanism that allows customers
to review, edit, and finalize their product selections before proceeding to the checkout. The shopping cart also displays the total cost of selected items.


 Price:
   The amount of money assigned to a product or service. In the context of an e-commerce website, prices are displayed for each item available for purchase.
   Prices may include taxes and shipping fees, or these may be calculated separately during the checkout process. Prices are crucial information for customers to make informed decisions about their purchases.

Source code:

   The Html and css code for creating a e-commerce website.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Artisan's Touch</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }


        header {
            background-color: #333;
            color: white;
            padding: 10px;
            text-align: center;
        }


        section {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
            padding: 20px;
        }


        .product {
            background-color: white;
            border: 1px solid #ddd;
            padding: 20px;
            margin: 10px;
            width: 200px;
            text-align: center;
        }


        .product img {
            max-width: 100%;
            height: auto;
            margin-bottom: 10px;
        }


        .product-details {
            background-color: white;
            border: 1px solid #ddd;
            padding: 20px;
            margin: 10px;
            width: 400px;
        }


        .cart {
            background-color: white;
            border: 1px solid #ddd;
            padding: 20px;
            margin: 10px;
            width: 400px;
        }


        footer {
            background-color: #333;
            color: white;
            padding: 10px;
            text-align: center;
            position: fixed;
            bottom: 0;
            width: 100%;
        }
    </style>
</head>
<body>
    <header>
        <h1>Artisan's Touch</h1>
    </header>


    <section>
        <div class="product">
            <img src="pic1.jpg" alt="pic1">
            <h2>Handmade hanging cuckoo</h2>
            <p>Handmade and hand painting wall decorative</p>
            <p>Rs.700</p>
            <button onclick="addToCart('Handmade hanging cuckoo', Rs.700)">Add to Cart</button>
        </div>


        <div class="product">
        
            <img src="pic2.jpg" alt="pic2">
            <h2>Iron Doll</h2>
            <p>Handmade iron doll sitting on a table.</p>
            <p>Rs.800</p>
            <button onclick="addToCart('Iron Doll', Rs.800)">Add to Cart</button>
        </div>
    </section>


    <div class="product-details" id="productDetails" style="display: none;">
        <h2>Product Details</h2>
        <img id="productImage" alt="Product Image">
        <p id="productDescription"></p>
        <p id="productPrice"></p>
        <button onclick="addToCart(currentProduct.name, currentProduct.price)">Add to Cart</button>
    </div>


    <div class="cart" id="shoppingCart">
        <h2>Shopping Cart</h2>
        <ul id="cartList"></ul>
        <p>Total: Rs <span id="cartTotal">0.00</span></p>
    </div>


    <footer>
        <p>&copy; 2023 Artisan's Touch. All rights reserved.</p>
    </footer>


    <script>
        var currentProduct = {};


        function showProductDetails(name, description, price, image) {
            document.getElementById('productDetails').style.display = 'block';
            document.getElementById('productImage').src = image;
            document.getElementById('productDescription').innerText = description;
            document.getElementById('productPrice').innerText = 'Rs' + price.toFixed(2);
            currentProduct = { name, price };
        }


        function addToCart(name, price) {
            var cartList = document.getElementById('cartList');
            var cartTotal = document.getElementById('cartTotal');


            var listItem = document.createElement('li');
            listItem.innerText = name + ' - Rs' + price.toFixed(2);
            cartList.appendChild(listItem);


            var total = parseFloat(cartTotal.innerText) + price;
            cartTotal.innerText = total.toFixed(2);
        }
    </script>
</body>
</html>
