<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sana Özel Bahçe 🌸</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Handlee&display=swap" rel="stylesheet"> 
    <style>
        body {
            margin: 0;
            overflow: hidden;
            font-family: 'Handlee', cursive;
            color: #333;
            cursor: pointer;
            /* Hafif pembe/mor tonlarında zarif arka plan */
            background: linear-gradient(135deg, #FFC0CB 0%, #ADD8E6 100%); 
        }

        /* Hoş Geldin Ekranı */
        #welcome-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            /* Parıltılı Açık Mor Arka Plan */
            background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            z-index: 100;
            transition: opacity 1s ease-out;
            animation: pulseBackground 5s infinite alternate; /* Yeni Arka Plan Animasyonu */
        }
        #welcome-screen.hidden {
            opacity: 0;
            pointer-events: none;
        }
        #welcome-screen h1 {
            /* Yeni Giriş Fontu: Daha Zarif */
            font-family: 'Great Vibes', cursive; 
            font-size: 5em;
            color: #8A2BE2; /* Mor */
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            margin-bottom: 30px;
            animation: slideIn 1.5s ease-out; /* Yeni Başlık Animasyonu */
        }
        #welcome-screen button {
            padding: 15px 30px;
            font-size: 1.2em;
            background-color: #FF69B4; /* Pembe */
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            animation: bounceIn 1.5s ease-out 0.5s both; /* Buton Animasyonu */
        }
        #welcome-screen button:hover {
            background-color: #FF1493;
            transform: scale(1.05);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.4);
        }

        /* Bahçe Alanı */
        #garden {
            position: relative;
            width: 100vw;
            height: 100vh;
            /* Daha Canlı Yeşil ve Mavi Geçiş */
            background: linear-gradient(to bottom, #87CEEB 40%, #A2FF86 100%); 
            overflow: hidden;
            opacity: 0;
            transition: opacity 2s ease-in-out;
        }
        #garden.active {
            opacity: 1;
        }

        .flower {
            position: absolute;
            font-size: 4em; /* Çiçek boyutu biraz büyüdü */
            user-select: none;
            pointer-events: none;
            animation: fadeInRotate 0.7s ease-out forwards; /* Yeni Çiçek Animasyonu */
            transform: scale(0);
        }

        /* Yeni Animasyonlar */
        @keyframes fadeInRotate {
            0% {
                opacity: 0;
                transform: scale(0) rotate(0deg);
            }
            100% {
                opacity: 1;
                /* Çiçeğin rastgele dönmesi için JavaScript kullanılır */
                transform: scale(1) rotate(var(--random-rotation, 0deg)); 
            }
        }

        @keyframes pulseBackground {
            0% { background-color: #e0c3fc; }
            100% { background-color: #8ec5fc; }
        }

        @keyframes slideIn {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @keyframes bounceIn {
            0%, 20%, 40%, 60%, 80%, 100% {
                transition-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
            }
            0% { opacity: 0; transform: scale3d(.3, .3, .3); }
            20% { transform: scale3d(1.1, 1.1, 1.1); }
            40% { transform: scale3d(.9, .9, .9); }
            60% { opacity: 1; transform: scale3d(1.03, 1.03, 1.03); }
            80% { transform: scale3d(.97, .97, .97); }
            100% { opacity: 1; transform: scale3d(1, 1, 1); }
        }
    </style>
</head>
<body>

    <div id="welcome-screen">
        <h1>Hoş Geldin Giz 👋</h1>
        <button id="continue-button">Devam Et ve Bahçeni Gör</button>
    </div>

    <div id="garden">
        </div>

    <script>
        const continueButton = document.getElementById('continue-button');
        const welcomeScreen = document.getElementById('welcome-screen');
        const garden = document.getElementById('garden');
        // Kalp emojisi eklendi
        const flowerEmojis = ['🌸', '🌺', '🌼', '🌷', '🌻', '🌹', '💐', '♥️', '♥️']; 

        continueButton.addEventListener('click', () => {
            // Hoş geldin ekranını gizle
            welcomeScreen.classList.add('hidden');

            // Bahçe ekranını yavaşça görünür yap
            setTimeout(() => {
                garden.classList.add('active');
            }, 1000); 
        });

        garden.addEventListener('click', (event) => {
            const flower = document.createElement('span');
            flower.classList.add('flower');
            
            // Rastgele bir emoji seç
            flower.textContent = flowerEmojis[Math.floor(Math.random() * flowerEmojis.length)];

            // Rastgele bir dönüş açısı belirle (0 ile 360 derece arası)
            const randomRotation = Math.floor(Math.random() * 360); 

            // CSS'teki animasyon için değişkeni ayarla
            flower.style.setProperty('--random-rotation', `${randomRotation}deg`);

            // Tıklanan yerin koordinatlarına göre çiçeği yerleştir
            flower.style.left = `${event.clientX - 30}px`; // Hafifçe merkeze hizalama
            flower.style.top = `${event.clientY - 30}px`;

            garden.appendChild(flower);
        });
    </script>

</body>
</html>
