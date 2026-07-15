<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MRN Clothing Shop - Premium Online Store</title>
    <!-- FontAwesome icon ব্যবহারের জন্য -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* ১. গ্লোবাল এবং রিসেট স্টাইল */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #f8f9fa;
            color: #333;
            overflow-x: hidden;
        }
        a {
            text-decoration: none;
            color: inherit;
        }

        /* ২. হেডার এবং নেভিগেশন বার (Menu Bar) */
        header {
            background-color: #ffffff;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 5%;
            max-width: 1200px;
            margin: 0 auto;
        }
        .logo {
            font-size: 24px;
            font-weight: 800;
            color: #e74c3c;
            letter-spacing: 1px;
        }
        .logo span {
            color: #2c3e50;
            font-weight: 400;
            font-size: 16px;
            margin-left: 5px;
            text-transform: uppercase;
        }
        
        /* ডেস্কটপ মেন্যু */
        .nav-menu {
            display: flex;
            list-style: none;
            gap: 20px;
        }
        .nav-menu li a {
            font-weight: 600;
            transition: 0.3s;
        }
        .nav-menu li a:hover {
            color: #e74c3c;
        }
        
        /* আইকন সেকশন */
        .nav-icons {
            display: flex;
            align-items: center;
            gap: 20px;
            font-size: 20px;
            cursor: pointer;
        }
        .cart-icon {
            position: relative;
        }
        .cart-count {
            position: absolute;
            top: -10px;
            right: -10px;
            background-color: #e74c3c;
            color: white;
            font-size: 12px;
            padding: 2px 6px;
            border-radius: 50%;
        }

        /* ৩ লাইনের মোবাইল মেন্যু টগল বাটন */
        .menu-toggle {
            display: none;
            font-size: 24px;
            cursor: pointer;
            color: #2c3e50;
        }

        /* ৩. সাইড ড্রয়ার মেন্যু (Mobile Sidebar Menu) */
        .mobile-menu-overlay {
            position: fixed;
            top: 0;
            left: -100%;
            width: 280px;
            height: 100%;
            background-color: #ffffff;
            z-index: 2000;
            box-shadow: 5px 0 15px rgba(0,0,0,0.2);
            transition: 0.4s ease-in-out;
            padding: 30px 20px;
            display: flex;
            flex-direction: column;
            gap: 25px;
        }
        .mobile-menu-overlay.active {
            left: 0;
        }
        .close-menu {
            align-self: flex-end;
            font-size: 28px;
            cursor: pointer;
            color: #2c3e50;
        }
        .mobile-logo {
            font-size: 24px;
            font-weight: 800;
            color: #e74c3c;
            border-bottom: 2px solid #f1f1f1;
            padding-bottom: 15px;
        }
        .mobile-nav-links {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .mobile-nav-links li a {
            font-size: 18px;
            font-weight: 600;
            color: #2c3e50;
            display: block;
            padding: 10px 0;
            border-bottom: 1px solid #f9f9f9;
        }
        /* ব্যাকগ্রাউন্ড ঝাপসা করার ব্ল্যাক স্ক্রিন */
        .overlay-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1500;
            display: none;
        }
        .overlay-bg.active {
            display: block;
        }

        /* ৪. হিরো ব্যানার (Hero Banner) */
        .hero {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('https://images.unsplash.com/photo-1483985988355-763728e1935b?q=80&w=1200&auto=format&fit=crop') no-repeat center center/cover;
            height: 400px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            color: white;
            padding: 20px;
        }
        .hero h1 {
            font-size: 36px;
            margin-bottom: 15px;
            text-transform: uppercase;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        .hero p {
            font-size: 16px;
            margin-bottom: 25px;
            max-width: 600px;
        }
        .hero-btn {
            background-color: #e74c3c;
            color: white;
            padding: 12px 30px;
            font-size: 16px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: 0.3s;
        }
        .hero-btn:hover {
            background-color: #c0392b;
        }

        /* ৫. ক্যাটাগরি সেকশন (Categories) */
        .section-title {
            text-align: center;
            margin: 40px 0 20px;
            font-size: 24px;
            position: relative;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 50px;
            height: 3px;
            background-color: #e74c3c;
            margin: 10px auto 0;
        }
        .categories {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 15px;
            max-width: 1200px;
            margin: 0 auto 40px;
            padding: 0 5%;
        }
        .category-card {
            background: #fff;
            border-radius: 10px;
            overflow: hidden;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            transition: 0.3s;
            cursor: pointer;
        }
        .category-card:hover {
            transform: translateY(-3px);
        }
        .category-card img {
            width: 100%;
            height: 140px;
            object-fit: cover;
        }
        .category-card h3 {
            padding: 10px;
            font-size: 14px;
        }

        /* ৬. প্রোডাক্ট সেকশন (Product Grid) */
        .products {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
            max-width: 1200px;
            margin: 0 auto 50px;
            padding: 0 5%;
        }
        .product-card {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            transition: 0.3s;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        .product-card:hover {
            box-shadow: 0 10px 20px rgba(0,0,0,0.15);
        }
        .product-img {
            width: 100%;
            height: 300px;
            object-fit: cover;
        }
        .product-info {
            padding: 15px;
            text-align: center;
        }
        .product-title {
            font-size: 15px;
            font-weight: 600;
            margin-bottom: 8px;
            color: #2c3e50;
        }
        .product-price {
            color: #e74c3c;
            font-size: 17px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .add-to-cart {
            background-color: #2c3e50;
            color: white;
            border: none;
            width: 100%;
            padding: 12px;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
        }
        .add-to-cart:hover {
            background-color: #e74c3c;
        }

        /* === নতুন কোড: অর্ডার ফর্ম ডিজাইন (যা আপনার আগের ডিজাইনে কোনো এফেক্ট করবে না) === */
        .checkout-container {
            max-width: 600px;
            margin: 50px auto;
            background: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            border-top: 5px solid #e74c3c;
            display: none; /* প্রথমে লুকানো থাকবে, Add To Cart চাপলে শো করবে */
        }
        .checkout-container.active {
            display: block;
        }
        .selected-product-summary {
            background-color: #fcf3f2;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            border-left: 4px solid #e74c3c;
        }
        .selected-product-summary p {
            font-size: 15px;
            margin: 5px 0;
        }
        .form-group {
            margin-bottom: 18px;
            text-align: left; /* যাতে টেক্সটগুলো বাম পাশে থাকে */
        }
        .form-group label {
            display: block;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 6px;
            color: #2c3e50;
        }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 14px;
            outline: none;
            transition: 0.3s;
        }
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            border-color: #e74c3c;
        }
        .submit-order-btn {
            background-color: #27ae60;
            color: white;
            border: none;
            width: 100%;
            padding: 15px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            transition: 0.3s;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
        }
        .submit-order-btn:hover {
            background-color: #219150;
        }

        /* ৭. ওয়েবসাইটের সুবিধাসমূহ (Features/Facilities) */
        .features {
            background-color: #fff;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            padding: 40px 5%;
            margin-bottom: 50px;
        }
        .feature-box {
            text-align: center;
            padding: 10px;
        }
        .feature-box i {
            font-size: 35px;
            color: #e74c3c;
            margin-bottom: 12px;
        }
        .feature-box h4 {
            font-size: 16px;
            margin-bottom: 8px;
        }
        .feature-box p {
            font-size: 13px;
            color: #7f8c8d;
        }

        /* ৮. ফুটার */
        footer {
            background-color: #2c3e50;
            color: #bdc3c7;
            padding: 40px 5% 20px;
        }
        .footer-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            max-width: 1200px;
            margin: 0 auto;
        }
        .footer-col h3 {
            color: white;
            margin-bottom: 15px;
            position: relative;
        }
        .footer-col h3::after {
            content: '';
            display: block;
            width: 30px;
            height: 2px;
            background-color: #e74c3c;
            margin-top: 5px;
        }
        .footer-col ul {
            list-style: none;
        }
        .footer-col ul li {
            margin-bottom: 8px;
        }
        .footer-col ul li a {
            font-size: 14px;
        }
        .newsletter input {
            padding: 10px;
            width: 65%;
            border: none;
            border-radius: 5px 0 0 5px;
            outline: none;
        }
        .newsletter button {
            padding: 10px 15px;
            background-color: #e74c3c;
            border: none;
            color: white;
            border-radius: 0 5px 5px 0;
            cursor: pointer;
        }
        .footer-bottom {
            text-align: center;
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #34495e;
            font-size: 12px;
        }

        /* ৯. রেসপনসিভ মিডিয়া কোয়েরি */
        @media (max-width: 768px) {
            .nav-menu {
                display: none;
            }
            .menu-toggle {
                display: block;
                order: -1;
            }
            .nav-container {
                padding: 10px 4%;
            }
            .logo {
                font-size: 20px;
            }
            .logo span {
                font-size: 12px;
            }
            .hero h1 {
                font-size: 28px;
            }
            .hero p {
                font-size: 14px;
            }
            /* মোবাইলে প্রোডাক্ট কার্ড এবং ক্যাটাগরিগুলো সুন্দর দেখানোর জন্য গ্রিড পরিবর্তন */
            .products {
                grid-template-columns: repeat(2, 1fr);
                gap: 12px;
                padding: 0 3%;
            }
            .product-img {
                height: 180px;
            }
            .product-title {
                font-size: 13px;
                height: 36px;
                overflow: hidden;
            }
            .product-price {
                font-size: 14px;
            }
            .add-to-cart {
                padding: 10px;
                font-size: 12px;
            }
            .categories {
                grid-template-columns: repeat(3, 1fr);
                gap: 8px;
                padding: 0 3%;
            }
            .category-card img {
                height: 90px;
            }
            .category-card h3 {
                font-size: 11px;
                padding: 5px;
            }
            .checkout-container {
                margin: 30px 4%;
                padding: 20px 15px;
            }
        }
    </style>
</head>
<body>

    <!-- ব্যাকগ্রাউন্ড ঝাপসা করার লেয়ার -->
    <div class="overlay-bg" id="overlayBg" onclick="toggleMenu()"></div>

    <!-- সাইড ড্রয়ার মেন্যু (মোবাইলের জন্য) -->
    <div class="mobile-menu-overlay" id="mobileMenu">
        <div class="close-menu" onclick="toggleMenu()">&times;</div>
        <div class="mobile-logo">MRN <span>Clothing</span></div>
        <ul class="mobile-nav-links">
            <li><a href="#" onclick="toggleMenu()">Home</a></li>
            <li><a href="#categories" onclick="toggleMenu()">Categories</a></li>
            <li><a href="#products" onclick="toggleMenu()">New Products</a></li>
            <li><a href="#features" onclick="toggleMenu()">Our Services</a></li>
            <li><a href="#" onclick="toggleMenu()">Contact</a></li>
        </ul>
    </div>

    <!-- হেডার এবং মেন্যু বার -->
    <header>
        <div class="nav-container">
            <div class="menu-toggle" onclick="toggleMenu()">
                <i class="fas fa-bars"></i>
            </div>

            <div class="logo">MRN<span>Clothing Shop</span></div>
            
            <!-- ডেস্কটপ মেন্যু -->
            <ul class="nav-menu">
                <li><a href="#">Home</a></li>
                <li><a href="#categories">Categories</a></li>
                <li><a href="#products">New Products</a></li>
                <li><a href="#features">Our Services</a></li>
                <li><a href="#">Contact</a></li>
            </ul>

            <div class="nav-icons">
                <i class="fas fa-search" onclick="alert('Search Bar Opening...')"></i>
                <i class="fas fa-user" onclick="alert('Profile Loading...')"></i>
                <div class="cart-icon" onclick="scrollToCheckout()">
                    <i class="fas fa-shopping-cart"></i>
                    <span class="cart-count" id="cartCount">0</span>
                </div>
            </div>
        </div>
    </header>

    <!-- হিরো সেকশন (ব্যানার) -->
    <section class="hero">
        <h1>Eid Collection 2026</h1>
        <p>Discover modern traditional & trending outfit designs on MRN Clothing</p>
        <button class="hero-btn" onclick="scrollToProducts()">Shop Now</button>
    </section>

    <!-- ক্যাটাগরি সেকশন -->
    <h2 class="section-title" id="categories">Shop By Category</h2>
    <section class="categories">
        <div class="category-card" onclick="alert('Loading Men\'s Collection...')">
            <img src="https://images.unsplash.com/photo-1617137968427-85924c800a22?q=80&w=250&auto=format&fit=crop" alt="Men">
            <h3>Men's Collection</h3>
        </div>
        <div class="category-card" onclick="alert('Loading Women\'s Collection...')">
            <img src="https://images.unsplash.com/photo-1595777457583-95e059d581b8?q=80&w=250&auto=format&fit=crop" alt="Women">
            <h3>Women's Collection</h3>
        </div>
        <div class="category-card" onclick="alert('Loading Kids\' Collection...')">
            <img src="https://images.unsplash.com/photo-1622290291468-a28f7a7dc6a8?q=80&w=250&auto=format&fit=crop" alt="Kids">
            <h3>Kids' Collection</h3>
        </div>
    </section>

    <!-- প্রোডাক্ট গ্রিড সেকশন -->
    <h2 class="section-title" id="products">New & Trending Arrivals</h2>
    <section class="products">
        
        <!-- ১. পাঞ্জাবি (Panjabi) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=350&auto=format&fit=crop" alt="Designer Panjabi">
            <div class="product-info">
                <div class="product-title">Premium Silk Designer Panjabi</div>
                <div class="product-price">৳ ২,৪৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Premium Silk Designer Panjabi', '৳ ২,৪৫০')">Add To Cart</button>
        </div>

        <!-- ২. থ্রি পিস (Three Piece) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1610030469668-93535c17b6b3?q=80&w=350&auto=format&fit=crop" alt="Women Three Piece">
            <div class="product-info">
                <div class="product-title">Georgette Exclusive Three Piece</div>
                <div class="product-price">৳ ৩,৮০০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Georgette Exclusive Three Piece', '৳ ৩,৮০০')">Add To Cart</button>
        </div>

        <!-- ৩. শার্ট (Shirt) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1596755094514-f87e34085b2c?q=80&w=350&auto=format&fit=crop" alt="Casual Shirt">
            <div class="product-info">
                <div class="product-title">Premium Cotton Casual Shirt</div>
                <div class="product-price">৳ ১,২০০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Premium Cotton Casual Shirt', '৳ ১,২০০')">Add To Cart</button>
        </div>

        <!-- ৪. টি শার্ট (T-Shirt) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1521572267360-ee0c2909d518?q=80&w=350&auto=format&fit=crop" alt="T Shirt">
            <div class="product-info">
                <div class="product-title">Solid Slim-Fit Cotton T-Shirt</div>
                <div class="product-price">৳ ৫৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Solid Slim-Fit Cotton T-Shirt', '৳ ৫৫০')">Add To Cart</button>
        </div>

        <!-- ৫. জিন্স প্যান্ট (Jeans Pant) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1542272604-787c3835535d?q=80&w=350&auto=format&fit=crop" alt="Jeans Pant">
            <div class="product-info">
                <div class="product-title">Regular Fit Stretchable Jeans</div>
                <div class="product-price">৳ ১,৬৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Regular Fit Stretchable Jeans', '৳ ১,৬৫০')">Add To Cart</button>
        </div>

        <!-- ৬. ট্রাউজার (Trouser) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1624378439575-d8705ad7ae80?q=80&w=350&auto=format&fit=crop" alt="Trouser">
            <div class="product-info">
                <div class="product-title">Comfy Athletic Track Trouser</div>
                <div class="product-price">৳ ৭৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Comfy Athletic Track Trouser', '৳ ৭৫০')">Add To Cart</button>
        </div>

        <!-- ৭. জুব্বা (Jubba) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1609357605129-26f69add5d6e?q=80&w=350&auto=format&fit=crop" alt="Jubba">
            <div class="product-info">
                <div class="product-title">Traditional Arabic Slim Fit Jubba</div>
                <div class="product-price">৳ ২,৯৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Traditional Arabic Slim Fit Jubba', '৳ ২,৯৫০')">Add To Cart</button>
        </div>

        <!-- ৮. বোরকা (Burka) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1585487000160-6ebcfceb0d03?q=80&w=350&auto=format&fit=crop" alt="Burka">
            <div class="product-info">
                <div class="product-title">Dubai Cherry Fabric Designer Borka</div>
                <div class="product-price">৳ ৩,২০০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Dubai Cherry Fabric Designer Borka', '৳ ৩,২০০')">Add To Cart</button>
        </div>

        <!-- ৯. মেয়েদের টপস (Women Tops) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1515886657613-9f3515b0c78f?q=80&w=350&auto=format&fit=crop" alt="Women Tops">
            <div class="product-info">
                <div class="product-title">Stylish Western Tops for Girls</div>
                <div class="product-price">৳ ৯৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Stylish Western Tops for Girls', '৳ ৯৫০')">Add To Cart</button>
        </div>

        <!-- ১০. বাচ্চাদের পোশাক (Child Outfit) -->
        <div class="product-card">
            <img class="product-img" src="https://images.unsplash.com/photo-1519457431-44ccd64a579b?q=80&w=350&auto=format&fit=crop" alt="Child Dress">
            <div class="product-info">
                <div class="product-title">Premium Comfort Kids Outfit Set</div>
                <div class="product-price">৳ ১,১৫০</div>
            </div>
            <button class="add-to-cart" onclick="addToCart('Premium Comfort Kids Outfit Set', '৳ ১,১৫০')">Add To Cart</button>
        </div>

    </section>

    <!-- === নতুন কোড: নতুন ডেডিকেটেড ক্যাশ অন ডেলিভারি অর্ডার ফরম সেকশন === -->
    <section class="checkout-container" id="checkoutSection">
        <h2 style="text-align: center; margin-bottom: 15px; color: #2c3e50;">Confirm Your Order</h2>
        <p style="text-align: center; font-size: 13px; color: #7f8c8d; margin-bottom: 20px;">অর্ডারটি সম্পন্ন করতে নিচের তথ্যগুলো সঠিক উপায়ে পূরণ করুন।</p>
        
        <!-- কোন প্রোডাক্ট সিলেক্ট হলো তার বিবরণ -->
        <div class="selected-product-summary">
            <strong>Selected Product:</strong>
            <p id="selectedTitle" style="font-weight: 600; color: #e74c3c;"></p>
            <p>Price: <span id="selectedPrice" style="font-weight: bold;"></span></p>
            <p>Delivery Fee: <span id="deliveryCost">৳ ৮০</span> (ঢাকার বাইরে ১৫০ টাকা)</p>
        </div>

        <form id="orderForm" onsubmit="sendOrderToWhatsApp(event)">
            <div class="form-group">
                <label for="fullName">আপনার নাম (Full Name) *</label>
                <input type="text" id="fullName" placeholder="যেমন: মোহাম্মদ রহিম" required>
            </div>

            <div class="form-group">
                <label for="mobileNo">মোবাইল নাম্বার (Mobile Number) *</label>
                <input type="tel" id="mobileNo" placeholder="যেমন: 017XXXXXXXX" required pattern="[0-9]{11}">
            </div>

            <div class="form-group">
                <label for="division">বিভাগ (Division) *</label>
                <select id="division" required onchange="updateDeliveryCharge()">
                    <option value="" disabled selected>আপনার বিভাগ সিলেক্ট করুন</option>
                    <option value="Dhaka">Dhaka (ঢাকা)</option>
                    <option value="Chattogram">Chattogram (চট্টগ্রাম)</option>
                    <option value="Rajshahi">Rajshahi (রাজশাহী)</option>
                    <option value="Khulna">Khulna (খুলনা)</option>
                    <option value="Barishal">Barishal (বরিশাল)</option>
                    <option value="Sylhet">Sylhet (সিলেট)</option>
                    <option value="Rangpur">Rangpur (রংপুর)</option>
                    <option value="Mymensingh">Mymensingh (ময়মনসিংহ)</option>
                </select>
            </div>

            <div class="form-group">
                <label for="fullAddress">গ্রাম / থানা / জেলা এবং পূর্ণ ঠিকানা *</label>
                <textarea id="fullAddress" rows="3" placeholder="যেমন: গ্রাম: উত্তর পাড়া, ডাকঘর: সদর, থানা: মিরপুর, ঢাকা।" required></textarea>
            </div>

            <button type="submit" class="submit-order-btn">
                <i class="fab fa-whatsapp"></i> WhatsApp-এ অর্ডার কনফার্ম করুন
            </button>
        </form>
    </section>

    <!-- ওয়েবসাইটের সুবিধাসমূহ (Features/Facilities) -->
    <section class="features" id="features">
        <div class="feature-box">
            <i class="fas fa-truck"></i>
            <h4>Fast Delivery</h4>
            <p>Home delivery inside Dhaka in 24 hours & outside Dhaka in 48 hours.</p>
        </div>
        <div class="feature-box">
            <i class="fas fa-undo-alt"></i>
            <h4>7-Day Return Policy</h4>
            <p>Easy size exchange or refund within 7 days if you are not satisfied.</p>
        </div>
        <div class="feature-box">
            <i class="fas fa-headset"></i>
            <h4>24/7 Support</h4>
            <p>Always active customer support system via phone or messenger.</p>
        </div>
        <div class="feature-box">
            <i class="fas fa-shield-alt"></i>
            <h4>100% Secure Payment</h4>
            <p>Cash on delivery, bKash, Nagad or Visa/MasterCard accepted.</p>
        </div>
    </section>

    <!-- ফুটার সেকশন -->
    <footer>
        <div class="footer-container">
            <div class="footer-col">
                <h3>About MRN</h3>
                <p>We provide the best quality premium fabrics and design at an affordable price in Bangladesh. Our target is your ultimate satisfaction.</p>
            </div>
            <div class="footer-col">
                <h3>Quick Links</h3>
                <ul>
                    <li><a href="#">Size Guide</a></li>
                    <li><a href="#">Return Policy</a></li>
                    <li><a href="#">Privacy Policy</a></li>
                    <li><a href="#">Terms & Conditions</a></li>
                </ul>
            </div>
            <div class="footer-col">
                <h3>Newsletter</h3>
                <p>Subscribe to get updates on new arrivals and flash sales.</p><br>
                <div class="newsletter">
                    <input type="email" placeholder="Enter email...">
                    <button onclick="alert('Thanks for subscribing!')">Send</button>
                </div>
            </div>
        </div>
        <div class="footer-bottom">
            <p>&copy; 2026 MRN Clothing Shop. Created with determination on a modest laptop.</p>
        </div>
    </footer>

    <!-- জাভাস্ক্রিপ্ট লজিক -->
    <script>
        // কাস্টমার যে নাম্বার থেকে অর্ডার রিসিভ করবেন সেটি এখানে দিন (যেমন: 88017xxxxxxxx)
        // অবশ্যই প্রথমে 88 কান্ট্রি কোড দিয়ে শুরু করতে হবে।
        const WHATSAPP_NUMBER = "8801700000000"; 

        let count = 0;
        
        function toggleMenu() {
            const mobileMenu = document.getElementById("mobileMenu");
            const overlayBg = document.getElementById("overlayBg");
            
            mobileMenu.classList.toggle("active");
            overlayBg.classList.toggle("active");
        }

        // আগের addToCart ফাংশনটি আপডেট করা হয়েছে যাতে কাস্টমার ক্লিক করলে কার্ট কাউন্ট বাড়ার সাথে সাথে অর্ডার ফর্মটি ওপেন হয়ে স্ক্রল হয়।
        function addToCart(title, price) {
            count++;
            document.getElementById("cartCount").innerHTML = count;
            
            // অর্ডার ফরমে প্রোডাক্টের নাম এবং প্রাইস অটোমেটিক সেট হবে
            document.getElementById("selectedTitle").innerText = title;
            document.getElementById("selectedPrice").innerText = price;
            
            // অর্ডার ফর্মটি শো করবে
            const checkoutSection = document.getElementById("checkoutSection");
            checkoutSection.classList.add("active");
            
            alert("অভিনন্দন! আপনার পছন্দের প্রোডাক্টটি সিলেক্ট হয়েছে। নিচের ফর্মে আপনার নাম-ঠিকানা দিন।");
            
            // স্ক্রল করে সরাসরি অর্ডারের ফর্মে নিয়ে যাবে
            checkoutSection.scrollIntoView({ behavior: 'smooth' });
        }

        function showCart() {
            if (count === 0) {
                alert("Your cart is empty! Add some products first.");
            } else {
                scrollToCheckout();
            }
        }

        function scrollToProducts() {
            document.getElementById("products").scrollIntoView({ behavior: 'smooth' });
        }

        // যদি কাস্টমার উপরে ডান পাশে কার্ট আইকনে ক্লিক করে সরাসরি ফর্মে যেতে চায়
        function scrollToCheckout() {
            const checkoutSection = document.getElementById("checkoutSection");
            if(checkoutSection.classList.contains("active")) {
                checkoutSection.scrollIntoView({ behavior: 'smooth' });
            } else {
                alert("দয়া করে প্রথমে যেকোনো একটি প্রোডাক্টের 'Add To Cart' বাটনে ক্লিক করুন!");
            }
        }

        // ঢাকা বিভাগের জন্য ডেলিভারি চার্জ ৮০ টাকা, ঢাকার বাইরের জন্য ১৫০ টাকা অটোমেটিক সেট হবে
        function updateDeliveryCharge() {
            const division = document.getElementById("division").value;
            const deliveryCostSpan = document.getElementById("deliveryCost");
            
            if (division === "Dhaka") {
                deliveryCostSpan.innerText = "৳ ৮০";
            } else {
                deliveryCostSpan.innerText = "৳ ১৫০";
            }
        }

        // কাস্টমার অর্ডার সাবমিট করলে সম্পূর্ণ তথ্য হোয়াটসঅ্যাপে চলে যাবে
        function sendOrderToWhatsApp(event) {
            event.preventDefault(); 

            const product = document.getElementById("selectedTitle").innerText;
            const price = document.getElementById("selectedPrice").innerText;
            const delivery = document.getElementById("deliveryCost").innerText;
            
            const name = document.getElementById("fullName").value;
            const phone = document.getElementById("mobileNo").value;
            const division = document.getElementById("division").value;
            const address = document.getElementById("fullAddress").value;

            // সুন্দর মেসেজ টেমপ্লেট
            const message = `*নতুন অর্ডারের তথ্য (MRN Shop)*\n\n` +
                            `📦 *প্রোডাক্ট:* ${product}\n` +
                            `💵 *দাম:* ${price}\n` +
                            `🚚 *ডেলিভারি চার্জ:* ${delivery}\n\n` +
                            `👤 *কাস্টমারের নাম:* ${name}\n` +
                            `📞 *মোবাইল নাম্বার:* ${phone}\n` +
                            `🗺️ *বিভাগ:* ${division}\n` +
                            `📍 *বিস্তারিত ঠিকানা:* ${address}`;

            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://api.whatsapp.com/send?phone=${WHATSAPP_NUMBER}&text=${encodedMessage}`;
            
            window.open(whatsappUrl, '_blank');
        }
    </script>

</body>
</html>
