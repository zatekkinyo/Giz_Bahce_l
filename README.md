<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sana Özel Bahçe 🌸</title>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Handlee&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            overflow: hidden; /* Çiçeklerin taşmasını engeller */
            font-family: 'Handlee', cursive;
            color: #333;
            cursor: pointer;
            background: linear-gradient(to bottom, #87CEEB, #B0E0E6); /* Gökyüzü tonları */
        }

        /* Hoş Geldin Ekranı */
        #welcome-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #f0f8ff; /* Açık mavi */
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            z-index: 100;
            transition: opacity 1s ease-out;
        }
        #welcome-screen.hidden {
            opacity: 0;
            pointer-events: none; /* Gizlendiğinde tıklamayı engelle */
        }
        #welcome-screen h1 {
            font-family: 'Pacifico', cursive;
            font-size: 4em;
            color: #FF69B4; /* Pembe */
            margin-bottom: 20px;
        }
        #welcome-screen button {
            padding: 15px 30px;
            font-size: 1.2em;
            background-color: #4CAF50; /* Yeşil */
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        #welcome-screen button:hover {
            background-color: #45a049;
            transform: translateY(-2px);
        }

        /* Bahçe Alanı */
        #garden {
            position: relative;
            width: 100vw;
            height: 100vh;
            background: linear-gradient(to bottom, #87CEEB 50%, #7CFC00 100%); /* Gökyüzü ve çimen */
            overflow: hidden;
            opacity: 0; /* Başlangıçta gizli */
            transition: opacity 2s ease-in-out;
        }
        #garden.active {
            opacity: 1;
        }

        .flower {
            position: absolute;
            font-size: 3em; /* Çiçek boyutu */
            user-select: none;
            pointer-events: none; /* Çiçeklerin tıklanabilirliği engellenir */
            animation: fadeInScale 0.5s ease-out forwards; /* Animasyon */
            transform: scale(0); /* Başlangıçta küçük */
        }

        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: scale(0);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }
    </style>
</head>
<body>

    <div id="welcome-screen">
        <h1>Hoş Geldin Giz 👋</h1>
        <button id="continue-button">Devam</button>
    </div>

    <div id="garden">
        </div>

    <script>
        const continueButton = document.getElementById('continue-button');
        const welcomeScreen = document.getElementById('welcome-screen');
        const garden = document.getElementById('garden');
        const flowerEmojis = ['🌸', '🌺', '🌼', '🌷', '🌻', '🌹', '💐'];

        continueButton.addEventListener('click', () => {
            // Hoş geldin ekranını gizle
            welcomeScreen.classList.add('hidden');

            // Bahçe ekranını yavaşça görünür yap
            setTimeout(() => {
                garden.classList.add('active');
            }, 1000); // 1 saniye sonra bahçe görünmeye başlar, animasyon süresine göre ayarlanabilir
        });

        garden.addEventListener('click', (event) => {
            const flower = document.createElement('span');
            flower.classList.add('flower');
            flower.textContent = flowerEmojis[Math.floor(Math.random() * flowerEmojis.length)];

            // Tıklanan yerin koordinatlarına göre çiçeği yerleştir
            flower.style.left = `${event.clientX - (flower.offsetWidth / 2)}px`;
            flower.style.top = `${event.clientY - (flower.offsetHeight / 2)}px`;

            garden.appendChild(flower);

            // Belirli bir süre sonra çiçeği sil (isteğe bağlı, bahçeyi temiz tutmak için)
            // setTimeout(() => {
            //     flower.remove();
            // }, 5000); // 5 saniye sonra siler
        });
    </script>

</body>
</html>
