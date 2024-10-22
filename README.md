# E_commerce123
<main id="content">
    <!-- Dynamic Content will be inserted here -->
</main>

<footer>
    <p>© 2024 E-commerce Website</p>
</footer>

<script>
    // JavaScript: Product Database
    const products = [
        { id: 1, name: "Product 1", price: 100, image: "https://via.placeholder.com/150" },
        { id: 2, name: "Product 2", price: 150, image: "https://via.placeholder.com/150" },
    ];

    // Function to display the product list
    function showProducts() {
        const content = document.getElementById("content");
        content.innerHTML = `
            <h2>Products</h2>
            <div class="product-list">
                ${products.map(product => `
                    <div class="product-item" data-id="${product.id}">
                        <img src="${product.image}" alt="${product.name}">
                        <h3>${product.name}</h3>
                        <p>Price: $${product.price}</p>
                        <button onclick="viewProduct(${product.id})">View Details</button>
                        <button onclick="addToCart(${product.id})">Add to Cart</button>
                    </div>
                `).join('')}
            </div>
        `;
    }

    // Function to display product details
    function viewProduct(productId) {
        const product = products.find(p => p.id === productId);
        const content = document.getElementById("content");
        content.innerHTML = `
            <div id="product-detail">
                <img src="${product.image}" alt="${product.name}">
                <h2>${product.name}</h2>
                <p>Price: $${product.price}</p>
                <button onclick="addToCart(${product.id})">Add to Cart</button>
                <button onclick="showProducts()">Back to Products</button>
            </div>
        `;
    }

    // Cart functionality
    function addToCart(productId) {
        let cart = JSON.parse(localStorage.getItem("cart")) || [];
        const product = products.find(p => p.id === productId);
        cart.push(product);
        localStorage.setItem("cart", JSON.stringify(cart));
        alert("Product added to cart!");
    }

    // Function to show the cart
    function showCart() {
        const cart = JSON.parse(localStorage.getItem("cart")) || [];
        let total = 0;
        const content = document.getElementById("content");

        if (cart.length === 0) {
            content.innerHTML = <h2>Your Cart is Empty</h2>;
            return;
        }

        content.innerHTML = `
            <h2>Your Cart</h2>
            <div id="cart-items">
                ${cart.map(item => {
                    total += item.price;
                    return <p>${item.name} - $${item.price}</p>;
                }).join('')}
            </div>
            <p>Total: $${total}</p>
            <button onclick="checkout()">Checkout</button>
            <button onclick="clearCart()">Clear Cart</button>
        `;
    }

    // Checkout function
    function checkout() {
        alert("Checkout Successful!");
        clearCart();
    }

    // Function to clear the cart
    function clearCart() {
        localStorage.removeItem("cart");
        showCart();
    }

    // Show products on page load
    window.onload = showProducts;
</script>
