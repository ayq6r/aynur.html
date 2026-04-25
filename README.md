<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <title>Moda Tasarım Galerisi</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f8f9fa;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        .gallery-container {
            position: relative;
            width: 400px;
            height: 600px;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            overflow: hidden;
            text-align: center;
        }

        .slide {
            display: none;
            width: 100%;
            height: 100%;
            animation: fade 0.5s ease-in-out;
        }

        .slide img {
            width: 100%;
            height: 80%;
            object-fit: cover;
        }

        .active { display: block; }

        .info {
            padding: 15px;
            background: white;
        }

        .info h2 { margin: 0; font-size: 1.2rem; color: #333; }
        .info p { color: #888; font-size: 0.9rem; }

        /* Ok Butonları */
        .btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(255, 255, 255, 0.8);
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            transition: 0.3s;
        }

        .btn:hover { background: #333; color: white; }
        .prev { left: 10px; }
        .next { right: 10px; }

        @keyframes fade {
            from { opacity: 0.4; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>

<div class="gallery-container">
    <div class="slide active">
        <img src="https://images.unsplash.com/photo-1539008835279-43467450821c?auto=format&fit=crop&w=800&q=80" alt="Elbise 1">
        <div class="info">
            <h2>Zümrüt Yeşili Gece Elbisesi</h2>
            <p>Modern kesim ve ipek doku.</p>
        </div>
    </div>

    <div class="slide">
        <img src="https://images.unsplash.com/photo-1515372039744-b8f02a3ae446?auto=format&fit=crop&w=800&q=80" alt="Elbise 2">
        <div class="info">
            <h2>Minimalist Yaz Esintisi</h2>
            <p>Hafif keten ve pastel tonlar.</p>
        </div>
    </div>

    <div class="slide">
        <img src="https://images.unsplash.com/photo-1566174053879-31528523f8ae?auto=format&fit=crop&w=800&q=80" alt="Elbise 3">
        <div class="info">
            <h2>Klasik Kraliyet Mavisi</h2>
            <p>Zarif dantel detaylı özel tasarım.</p>
        </div>
    </div>

    <button class="btn prev" onclick="changeSlide(-1)">&#10094;</button>
    <button class="btn next" onclick="changeSlide(1)">&#10095;</button>
</div>

<script>
    let currentSlide = 0;
    const slides = document.querySelectorAll(".slide");

    function changeSlide(n) {
        slides[currentSlide].classList.remove("active");
        currentSlide = (currentSlide + n + slides.length) % slides.length;
        slides[currentSlide].classList.add("active");
    }

    // Klavye ok tuşları ile kontrol
    document.addEventListener("keydown", (e) => {
        if (e.key === "ArrowLeft") changeSlide(-1);
        if (e.key === "ArrowRight") changeSlide(1);
    });
</script>

</body>
</html>
