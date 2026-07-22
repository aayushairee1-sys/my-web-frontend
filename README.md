<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Store Catalog | GSD Suppliers</title>
    <!-- Icons & High-Tech Fonts -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800;900&family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg: #040508;
            --primary: #ffb800;
            --card-bg: rgba(15, 17, 23, 0.85);
            --accent-green: #00e676;
        }

        * {
            margin: 0; padding: 0; box-sizing: border-box;
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        body {
            background-color: var(--bg);
            color: #fff;
            min-height: 100vh;
            padding-bottom: 80px;
        }

        /* Particle Canvas */
        #particleCanvas {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: 1;
            pointer-events: none;
        }

        header {
            position: relative;
            z-index: 10;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 25px 8%;
            background: rgba(8, 10, 15, 0.85);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
            position: sticky;
            top: 0;
        }

        .logo {
            font-family: 'Orbitron', sans-serif;
            font-size: 24px;
            font-weight: 900;
            letter-spacing: 1.5px;
        }

        .logo span {
            color: var(--primary);
            text-shadow: 0 0 12px rgba(255, 184, 0, 0.8);
        }

        nav a {
            color: #8a92a6;
            text-decoration: none;
            margin-left: 30px;
            font-weight: 600;
            transition: 0.3s;
        }

        nav a:hover, nav a.active {
            color: var(--primary);
            text-shadow: 0 0 8px rgba(255, 184, 0, 0.6);
        }

        .container {
            position: relative;
            z-index: 5;
            max-width: 1200px;
            margin: 50px auto;
            padding: 0 20px;
        }

        .page-title {
            text-align: center;
            font-family: 'Orbitron', sans-serif;
            font-size: 38px;
            margin-bottom: 45px;
            letter-spacing: 1px;
        }

        .page-title span { color: var(--primary); }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(270px, 1fr));
            gap: 30px;
        }

        /* Cyber Neon Product Card */
        .card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 25px;
            border: 1px solid rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(10px);
            position: relative;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: all 0.4s ease;
            overflow: hidden;
        }

        .card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--primary);
            box-shadow: 0 15px 35px rgba(255, 184, 0, 0.25);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            font-size: 12px;
            font-weight: 700;
        }

        .tag {
            background: rgba(255, 255, 255, 0.05);
            padding: 4px 10px;
            border-radius: 6px;
            color: #8a92a6;
        }

        .status { color: var(--accent-green); }

        .image-box {
            height: 130px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 14px;
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 20px;
            border: 1px solid rgba(255, 255, 255, 0.04);
        }

        .image-box i {
            font-size: 55px;
            transition: transform 0.3s;
        }

        .card:hover .image-box i {
            transform: scale(1.15) rotate(5deg);
        }

        .icon-ff { color: #ff4757; filter: drop-shadow(0 0 15px rgba(255, 71, 87, 0.6)); }
        .icon-pubg { color: #ffa502; filter: drop-shadow(0 0 15px rgba(255, 165, 0, 0.6)); }
        .icon-ml { color: #2ed573; filter: drop-shadow(0 0 15px rgba(46, 213, 115, 0.6)); }
        .icon-netflix { color: #e50914; filter: drop-shadow(0 0 15px rgba(229, 9, 20, 0.6)); }

        .card-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 18px;
            margin-bottom: 15px;
        }

        select {
            width: 100%;
            padding: 12px;
            background: #0d0f17;
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 10px;
            color: #fff;
            font-weight: 600;
            outline: none;
            margin-bottom: 20px;
            cursor: pointer;
            transition: border-color 0.3s;
        }

        select:focus { border-color: var(--primary); }

        .card-footer {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .price-label { font-size: 11px; color: #8a92a6; }
        .price {
            font-family: 'Orbitron', sans-serif;
            font-size: 20px;
            font-weight: 800;
            color: var(--primary);
        }

        .buy-btn {
            background: var(--primary);
            color: #000;
            padding: 12px 20px;
            border-radius: 10px;
            text-decoration: none;
            font-weight: 800;
            font-size: 13px;
            display: flex;
            align-items: center;
            gap: 6px;
            box-shadow: 0 0 15px rgba(255, 184, 0, 0.3);
            transition: all 0.2s;
        }

        .buy-btn:hover {
            background: #fff;
            transform: scale(1.05);
            box-shadow: 0 0 25px rgba(255, 255, 255, 0.6);
        }
    </style>
</head>
<body>

    <canvas id="particleCanvas"></canvas>

    <header>
        <div class="logo">GSD <span>Suppliers</span></div>
        <nav>
            <a href="index.html">Home</a>
            <a href="products.html" class="active">Store Catalog</a>
        </nav>
    </header>

    <div class="container">
        <h1 class="page-title">SELECT YOUR <span>PACKAGE</span></h1>

        <div class="products-grid">

            <!-- FREE FIRE CARD -->
            <div class="card">
                <div>
                    <div class="card-header">
                        <span class="tag">TOPUP</span>
                        <span class="status"><i class="fa-solid fa-circle"></i> ONLINE</span>
                    </div>
                    <div class="image-box">
                        <i class="fa-solid fa-fire icon-ff"></i>
                    </div>
                    <div class="card-title">Free Fire Diamond</div>
                    <select id="ff-select" onchange="updatePrice('ff')">
                        <option value="30">25 Diamonds</option>
                        <option value="50">50 Diamonds</option>
                        <option value="100">100 Diamonds</option>
                        <option value="105">115 Diamonds</option>
                        <option value="210">240 Diamonds</option>
                        <option value="315">355 Diamonds</option>
                        <option value="420">480 Diamonds</option>
                        <option value="525">610 Diamonds</option>
                        <option value="630">725 Diamonds</option>
                        <option value="735">850 Diamonds</option>
                        <option value="840">965 Diamonds</option>
                        <option value="945">1090 Diamonds</option>
                        <option value="1050">1240 Diamonds</option>
                        <option value="1290">1505 Diamonds</option>
                        <option value="1780">2090 Diamonds</option>
                        <option value="2100">2530 Diamonds</option>
                        <option value="2520">3010 Diamonds</option>
                        <option value="4200">5060 Diamonds</option>
                        <option value="5200">6300 Diamonds</option>
                        <option value="8350">10120 Diamonds</option>
                        <option value="60">Weekly Lite (90💎)</option>
                        <option value="210">Weekly Pass (445💎)</option>
                        <option value="1040">Monthly Pass (2500💎)</option>
                        <option value="540">Level - Pass (1270💎)</option>
                    </select>
                </div>
                <div class="card-footer">
                    <div>
                        <div class="price-label">PRICE</div>
                        <div class="price" id="ff-price">Rs. 30</div>
                    </div>
                    <a href="https://wa.me/9743712703" target="_blank" class="buy-btn">
                        <i class="fa-solid fa-cart-shopping"></i> BUY NOW
                    </a>
                </div>
            </div>

            <!-- PUBG UC CARD -->
            <div class="card">
                <div>
                    <div class="card-header">
                        <span class="tag">TOPUP</span>
                        <span class="status"><i class="fa-solid fa-circle"></i> ONLINE</span>
                    </div>
                    <div class="image-box">
                        <i class="fa-solid fa-gun icon-pubg"></i>
                    </div>
                    <div class="card-title">PUBG Mobile UC</div>
                    <select id="pubg-select" onchange="updatePrice('pubg')">
                        <option value="150">60 UC</option>
                        <option value="300">120 UC</option>
                        <option value="600">240 UC</option>
                        <option value="750">325 UC</option>
                        <option value="1500">660 UC</option>
                        <option value="1650">720 UC</option>
                        <option value="3750">1800 UC</option>
                        <option value="7500">3850 UC</option>
                        <option value="14500">8100 UC</option>
                        <option value="29000">16200 UC</option>
                    </select>
                </div>
                <div class="card-footer">
                    <div>
                        <div class="price-label">PRICE</div>
                        <div class="price" id="pubg-price">Rs. 150</div>
                    </div>
                    <a href="https://wa.me/9743712703" target="_blank" class="buy-btn">
                        <i class="fa-solid fa-cart-shopping"></i> BUY NOW
                    </a>
                </div>
            </div>

            <!-- MOBILE LEGENDS CARD -->
            <div class="card">
                <div>
                    <div class="card-header">
                        <span class="tag">TOPUP</span>
                        <span class="status"><i class="fa-solid fa-circle"></i> ONLINE</span>
                    </div>
                    <div class="image-box">
                        <i class="fa-solid fa-shield-halved icon-ml"></i>
                    </div>
                    <div class="card-title">Mobile Legends</div>
                    <select id="ml-select" onchange="updatePrice('ml')">
                        <option value="135">50 + 5 Diamonds (2X)</option>
                        <option value="400">150 + 15 Diamonds (2X)</option>
                        <option value="650">250 + 25 Diamonds (2X)</option>
                        <option value="1340">500 + 65 Diamonds (2X)</option>
                        <option value="220">86 Diamonds</option>
                        <option value="440">172 Diamonds</option>
                        <option value="600">257 Diamonds</option>
                        <option value="1650">706 Diamonds</option>
                        <option value="5080">2195 Diamonds</option>
                        <option value="260">Weekly Pass</option>
                        <option value="1400">Twilight Pass</option>
                    </select>
                </div>
                <div class="card-footer">
                    <div>
                        <div class="price-label">PRICE</div>
                        <div class="price" id="ml-price">Rs. 135</div>
                    </div>
                    <a href="https://wa.me/9743712703" target="_blank" class="buy-btn">
                        <i class="fa-solid fa-cart-shopping"></i> BUY NOW
                    </a>
                </div>
            </div>

            <!-- NETFLIX CARD -->
            <div class="card">
                <div>
                    <div class="card-header">
                        <span class="tag">PASS</span>
                        <span class="status"><i class="fa-solid fa-circle"></i> ONLINE</span>
                    </div>
                    <div class="image-box">
                        <i class="fa-solid fa-tv icon-netflix"></i>
                    </div>
                    <div class="card-title">Netflix Premium</div>
                    <select id="netflix-select" onchange="updatePrice('netflix')">
                        <option value="350">1 Month Premium (4K)</option>
                        <option value="950">3 Months Premium (4K)</option>
                    </select>
                </div>
                <div class="card-footer">
                    <div>
                        <div class="price-label">PRICE</div>
                        <div class="price" id="netflix-price">Rs. 350</div>
                    </div>
                    <a href="https://wa.me/9743712703" target="_blank" class="buy-btn">
                        <i class="fa-solid fa-cart-shopping"></i> BUY NOW
                    </a>
                </div>
            </div>

        </div>
    </div>

    <!-- Interactive Price Update Script -->
    <script>
        function updatePrice(id) {
            var select = document.getElementById(id + '-select');
            var price = document.getElementById(id + '-price');
            price.innerText = "Rs. " + select.value;
        }

        // Particle Canvas Animation
        const canvas = document.getElementById('particleCanvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 1;
                this.speedX = Math.random() * 1 - 0.5;
                this.speedY = Math.random() * 1 - 0.5;
                this.color = 'rgba(255, 184, 0, ' + (Math.random() * 0.5 + 0.2) + ')';
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.x > canvas.width) this.x = 0;
                if (this.x < 0) this.x = canvas.width;
                if (this.y > canvas.height) this.y = 0;
                if (this.y < 0) this.y = canvas.height;
            }
            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        for (let i = 0; i < 70; i++) {
            particles.push(new Particle());
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animate);
        }
        animate();
    </script>
</body>
</html>
