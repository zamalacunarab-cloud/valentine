<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feliz San Valentín Señora</title>
    <style>
        :root {
            --color-sobre: #ff1744;
            --color-sobre-oscuro: #c2185b;
            --color-carta: #fff;
            --color-fondo: #ffdee9;
            --color-acento: #ff6b9d;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, 
                #ff0844 0%, 
                #ffb199 12%, 
                #ff0844 24%, 
                #d81b60 36%, 
                #8e24aa 48%, 
                #d81b60 60%, 
                #ff0844 72%, 
                #ff6090 84%, 
                #ff0844 100%);
            background-size: 400% 400%;
            animation: gradientShift 18s ease infinite;
            font-family: 'Georgia', 'Times New Roman', serif;
            overflow: hidden;
            position: relative;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            25% { background-position: 50% 100%; }
            50% { background-position: 100% 50%; }
            75% { background-position: 50% 0%; }
            100% { background-position: 0% 50%; }
        }

        /* Corazones y ositos flotantes de fondo */
        .floating-hearts {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
            z-index: 0;
        }

        .floating-heart {
            position: absolute;
            font-size: 30px;
            opacity: 0;
            animation: float 10s infinite;
        }

        .floating-bear {
            position: absolute;
            font-size: 35px;
            opacity: 0;
            animation: floatBear 12s infinite;
        }

        .floating-violet {
            position: absolute;
            font-size: 32px;
            opacity: 0;
            animation: floatViolet 14s infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.7;
            }
            90% {
                opacity: 0.7;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }

        @keyframes floatBear {
            0% {
                transform: translateY(100vh) rotate(-10deg);
                opacity: 0;
            }
            10% {
                opacity: 0.8;
            }
            50% {
                transform: translateY(50vh) rotate(10deg);
            }
            90% {
                opacity: 0.8;
            }
            100% {
                transform: translateY(-100px) rotate(-10deg);
                opacity: 0;
            }
        }

        @keyframes floatViolet {
            0% {
                transform: translateY(100vh) rotate(0deg) scale(1);
                opacity: 0;
            }
            10% {
                opacity: 0.85;
            }
            30% {
                transform: translateY(70vh) rotate(15deg) scale(1.1);
            }
            60% {
                transform: translateY(40vh) rotate(-15deg) scale(0.9);
            }
            90% {
                opacity: 0.85;
            }
            100% {
                transform: translateY(-100px) rotate(0deg) scale(1);
                opacity: 0;
            }
        }

        /* Contenedor del sobre */
        .envelope-wrapper {
            position: relative;
            cursor: pointer;
            transition: transform 0.3s;
            z-index: 10;
        }

        .envelope-wrapper:hover:not(.open) {
            transform: scale(1.05);
        }

        .envelope {
            position: relative;
            width: 340px;
            height: 230px;
            background-color: var(--color-sobre);
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
            box-shadow: 0 15px 50px rgba(255, 0, 128, 0.5),
                        0 5px 30px rgba(255, 23, 68, 0.6),
                        0 0 40px rgba(255, 107, 157, 0.3);
        }

        /* Solapa del sobre */
        .envelope::before {
            content: "";
            position: absolute;
            top: 0;
            z-index: 4;
            border-top: 125px solid var(--color-sobre-oscuro);
            border-left: 170px solid transparent;
            border-right: 170px solid transparent;
            transform-origin: top;
            transition: transform 0.6s 0.3s ease-in-out;
        }

        /* Lados del sobre */
        .envelope::after {
            content: "";
            position: absolute;
            z-index: 3;
            width: 0;
            height: 0;
            border-top: 115px solid transparent;
            border-right: 170px solid var(--color-sobre);
            border-bottom: 115px solid var(--color-sobre);
            border-left: 170px solid var(--color-sobre-oscuro);
            border-radius: 0 0 10px 10px;
        }

        /* La Carta */
        .letter {
            position: absolute;
            bottom: 0;
            left: 10px;
            width: 340px;
            height: 220px;
            background: linear-gradient(135deg, #ffffff 0%, #ffe0f0 50%, #ffd5e5 100%);
            z-index: 2;
            padding: 32px;
            box-sizing: border-box;
            transition: transform 0.8s ease, bottom 0.8s ease;
            box-shadow: 0 10px 40px rgba(255, 23, 68, 0.6),
                        0 0 30px rgba(255, 107, 157, 0.5),
                        0 5px 15px rgba(216, 27, 96, 0.4);
            text-align: center;
            border-radius: 8px;
            border: 4px solid rgba(255, 23, 68, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .letter-content {
            opacity: 0;
            transform: scale(0.8);
            transition: opacity 0.6s 0.8s, transform 0.6s 0.8s;
        }

        .letter p {
            font-size: 17px;
            color: #c2185b;
            line-height: 1.7;
            margin: 10px 0;
            text-shadow: 0 1px 3px rgba(255, 255, 255, 0.9);
            font-weight: 500;
        }

        .letter .firma {
            margin-top: 16px;
            font-size: 17px;
            color: #c2185b;
            font-weight: bold;
            background: linear-gradient(45deg, #ff1744, #c2185b, #ff6b9d);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1.7;
        }

        .letter .titulo {
            font-size: 24px;
            background: linear-gradient(45deg, #ff0080, #ff1744, #ff6b9d, #c2185b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-weight: bold;
            margin-bottom: 16px;
            text-transform: uppercase;
            letter-spacing: 1px;
            filter: drop-shadow(0 2px 4px rgba(255, 23, 68, 0.3));
        }

        /* Corazón/Sello */
        .heart {
            position: absolute;
            top: 100px;
            left: 50%;
            width: 35px;
            height: 35px;
            background: linear-gradient(135deg, #ff0080 0%, #ff1744 50%, #ff6b9d 100%);
            z-index: 5;
            transform: translate(-50%, -50%) rotate(45deg);
            transition: opacity 0.5s, transform 0.5s;
            animation: heartbeat 1.5s infinite;
            filter: drop-shadow(0 0 10px rgba(255, 0, 128, 0.8))
                    drop-shadow(0 0 20px rgba(255, 23, 68, 0.6));
        }
        
        @keyframes heartbeat {
            0%, 100% { 
                transform: translate(-50%, -50%) rotate(45deg) scale(1); 
            }
            25% { 
                transform: translate(-50%, -50%) rotate(45deg) scale(1.15); 
                filter: drop-shadow(0 0 15px rgba(255, 0, 128, 1))
                        drop-shadow(0 0 25px rgba(255, 23, 68, 0.8));
            }
            50% { 
                transform: translate(-50%, -50%) rotate(45deg) scale(1); 
            }
        }

        .heart:before, .heart:after {
            content: "";
            position: absolute;
            width: 35px;
            height: 35px;
            background: linear-gradient(135deg, #ff0080 0%, #ff1744 50%, #ff6b9d 100%);
            border-radius: 50%;
        }
        .heart:before { left: -17px; }
        .heart:after { top: -17px; }

        /* Animación al Abrir */
        .envelope-wrapper.open .envelope::before {
            transform: rotateX(180deg);
            z-index: 0;
        }

        .envelope-wrapper.open .letter {
            transform: translateY(-30px);
            z-index: 10;
            height: auto;
            min-height: 400px;
            padding: 32px;
        }

        .envelope-wrapper.open .letter-content {
            opacity: 1;
            transform: scale(1);
        }

        .envelope-wrapper.open .heart {
            opacity: 0;
            transform: translate(-50%, -50%) rotate(45deg) scale(0);
        }

        .instruccion {
            position: absolute;
            bottom: 40px;
            color: rgba(255, 255, 255, 0.9);
            text-transform: uppercase;
            letter-spacing: 3px;
            font-size: 13px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            animation: pulse 2s infinite;
            z-index: 1;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        /* Control de música */
        .music-control {
            position: absolute;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, rgba(255, 0, 128, 0.9), rgba(255, 23, 68, 0.9));
            border: 3px solid rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s;
            backdrop-filter: blur(10px);
            z-index: 100;
            box-shadow: 0 5px 25px rgba(255, 0, 128, 0.6),
                        0 0 20px rgba(255, 23, 68, 0.4),
                        inset 0 -2px 10px rgba(0, 0, 0, 0.2);
            animation: musicPulse 2s ease-in-out infinite;
        }

        @keyframes musicPulse {
            0%, 100% {
                box-shadow: 0 5px 25px rgba(255, 0, 128, 0.6),
                            0 0 20px rgba(255, 23, 68, 0.4),
                            inset 0 -2px 10px rgba(0, 0, 0, 0.2);
            }
            50% {
                box-shadow: 0 5px 30px rgba(255, 0, 128, 0.8),
                            0 0 30px rgba(255, 23, 68, 0.6),
                            inset 0 -2px 10px rgba(0, 0, 0, 0.2);
            }
        }

        .music-control:hover {
            background: linear-gradient(135deg, rgba(255, 0, 128, 1), rgba(255, 23, 68, 1));
            transform: scale(1.15) rotate(5deg);
            box-shadow: 0 8px 35px rgba(255, 0, 128, 0.8),
                        0 0 40px rgba(255, 23, 68, 0.6);
        }

        .music-control:active {
            transform: scale(0.95);
        }

        .music-control svg {
            width: 28px;
            height: 28px;
            fill: white;
            filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
        }

        .music-control.playing {
            animation: musicPulse 1s ease-in-out infinite, rotate 3s linear infinite;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        /* Partículas brillantes */
        .sparkle {
            position: absolute;
            pointer-events: none;
            animation: sparkleFloat 3s ease-out forwards;
            filter: drop-shadow(0 0 5px currentColor);
        }

        @keyframes sparkleFloat {
            0% {
                transform: translateY(0) scale(1) rotate(0deg);
                opacity: 1;
            }
            50% {
                transform: translateY(-50px) scale(1.2) rotate(180deg);
                opacity: 0.8;
            }
            100% {
                transform: translateY(-100px) scale(0) rotate(360deg);
                opacity: 0;
            }
        }

        /* Estilos para dispositivos móviles */
        @media (max-width: 768px) {
            body {
                padding: 10px;
            }

            .envelope {
                width: 280px;
                height: 190px;
            }

            .envelope::before {
                border-top: 105px solid var(--color-sobre-oscuro);
                border-left: 140px solid transparent;
                border-right: 140px solid transparent;
            }

            .envelope::after {
                border-top: 95px solid transparent;
                border-right: 140px solid var(--color-sobre);
                border-bottom: 95px solid var(--color-sobre);
                border-left: 140px solid var(--color-sobre-oscuro);
            }

            .letter {
                left: 10px;
                width: 280px;
                height: 180px;
                padding: 25px;
            }

            .letter .titulo {
                font-size: 20px;
                margin-bottom: 16px;
            }

            .letter p {
                font-size: 15px;
                line-height: 1.7;
                margin: 10px 0;
            }

            .letter .firma {
                margin-top: 16px;
                font-size: 15px;
            }

            .envelope-wrapper.open .letter {
                transform: translateY(-30px);
                min-height: 320px;
                padding: 22px;
                z-index: 10;
            }

            .heart {
                top: 85px;
                width: 30px;
                height: 30px;
            }

            .heart:before, .heart:after {
                width: 30px;
                height: 30px;
            }

            .heart:before { left: -15px; }
            .heart:after { top: -15px; }

            .instruccion {
                font-size: 11px;
                bottom: 30px;
                letter-spacing: 2px;
            }

            .music-control {
                width: 55px;
                height: 55px;
                top: 15px;
                right: 15px;
            }

            .music-control svg {
                width: 26px;
                height: 26px;
            }

            .floating-heart {
                font-size: 25px;
            }

            .floating-bear {
                font-size: 28px;
            }

            .floating-violet {
                font-size: 27px;
            }

            .titulo-superior {
                font-size: 32px;
                top: 20px;
                letter-spacing: 2px;
            }
        }

        @media (max-width: 480px) {
            .envelope {
                width: 260px;
                height: 180px;
            }

            .envelope::before {
                border-top: 100px solid var(--color-sobre-oscuro);
                border-left: 130px solid transparent;
                border-right: 130px solid transparent;
            }

            .envelope::after {
                border-top: 90px solid transparent;
                border-right: 130px solid var(--color-sobre);
                border-bottom: 90px solid var(--color-sobre);
                border-left: 130px solid var(--color-sobre-oscuro);
            }

            .letter {
                left: 8px;
                width: 244px;
                padding: 22px;
            }

            .letter .titulo {
                font-size: 18px;
                margin-bottom: 14px;
            }

            .letter p {
                font-size: 14px;
                line-height: 1.7;
                margin: 9px 0;
            }

            .letter .firma {
                font-size: 14px;
                margin-top: 14px;
            }

            .envelope-wrapper.open .letter {
                transform: translateY(-30px);
                min-height: 300px;
                padding: 20px;
                z-index: 10;
            }

            .floating-heart {
                font-size: 22px;
            }

            .floating-bear {
                font-size: 25px;
            }

            .floating-violet {
                font-size: 24px;
            }

            .titulo-superior {
                font-size: 28px;
                top: 20px;
                letter-spacing: 2px;
            }
        }
    </style>
</head>
<body>
    <!-- Corazones flotantes de fondo -->
    <div class="floating-hearts" id="floatingHearts"></div>

    <!-- Control de música -->
    <div class="music-control" id="musicControl" title="Música">
        <svg id="musicIcon" viewBox="0 0 24 24">
            <path d="M12 3v10.55c-.59-.34-1.27-.55-2-.55-2.21 0-4 1.79-4 4s1.79 4 4 4 4-1.79 4-4V7h4V3h-6z"/>
        </svg>
    </div>

    <div class="envelope-wrapper" id="envelopeWrapper">
        <div class="envelope">
            <div class="heart"></div>
        </div>
        <div class="letter">
            <div class="letter-content">
                <p class="titulo">¡Feliz San Valentín Señora!</p>
                <p>
                    En este día especial quiero que sepas que cada momento a tu lado es un regalo. 
                    Tu sonrisa ilumina mis días y tu amor hace que todo tenga sentido.
                </p>
                <p>
                    Gracias por ser mi compañera, mi amor y mi todo. ❤️
                </p>
                <p class="firma">
                    Con todo mi amor,<br>
                    De: <strong>Ángel</strong><br>
                    Para: <strong>Laura</strong> 💕
                </p>
            </div>
        </div>
    </div>

    <div class="instruccion">Haz clic en el sobre</div>

    <!-- Audio de fondo -->
    <audio id="backgroundMusic" loop>
        <!-- Música romántica suave de fondo -->
        <source src="https://assets.mixkit.co/music/preview/mixkit-tender-love-116.mp3" type="audio/mpeg">
    </audio>

    <!-- Efecto de sonido al abrir -->
    <audio id="openSound">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-fairy-arcade-sparkle-866.mp3" type="audio/mpeg">
    </audio>

    <!-- Efecto de sonido mágico -->
    <audio id="magicSound">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-magic-sweep-game-trophy-257.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Crear corazones y ositos flotantes
        function createFloatingHearts() {
            const heartsContainer = document.getElementById('floatingHearts');
            const heartSymbols = ['❤️', '💕', '💖', '💗', '💝', '💘'];
            const bearSymbols = ['🧸', '🐻', '🐨'];
            const violetSymbols = ['🌸', '🌺', '🌷', '🪻', '💐'];
            
            setInterval(() => {
                const heart = document.createElement('div');
                heart.className = 'floating-heart';
                heart.textContent = heartSymbols[Math.floor(Math.random() * heartSymbols.length)];
                heart.style.left = Math.random() * 100 + '%';
                heart.style.animationDuration = (Math.random() * 5 + 8) + 's';
                heart.style.animationDelay = Math.random() * 2 + 's';
                heartsContainer.appendChild(heart);
                
                setTimeout(() => {
                    heart.remove();
                }, 13000);
            }, 1500);

            // Crear ositos con menos frecuencia
            setInterval(() => {
                const bear = document.createElement('div');
                bear.className = 'floating-bear';
                bear.textContent = bearSymbols[Math.floor(Math.random() * bearSymbols.length)];
                bear.style.left = Math.random() * 100 + '%';
                bear.style.animationDuration = (Math.random() * 4 + 10) + 's';
                bear.style.animationDelay = Math.random() * 3 + 's';
                heartsContainer.appendChild(bear);
                
                setTimeout(() => {
                    bear.remove();
                }, 15000);
            }, 2500);

            // Crear violetas
            setInterval(() => {
                const violet = document.createElement('div');
                violet.className = 'floating-violet';
                violet.textContent = violetSymbols[Math.floor(Math.random() * violetSymbols.length)];
                violet.style.left = Math.random() * 100 + '%';
                violet.style.animationDuration = (Math.random() * 5 + 12) + 's';
                violet.style.animationDelay = Math.random() * 2 + 's';
                heartsContainer.appendChild(violet);
                
                setTimeout(() => {
                    violet.remove();
                }, 17000);
            }, 2000);
        }

        createFloatingHearts();

        // Control del sobre
        const envelopeWrapper = document.getElementById('envelopeWrapper');
        const music = document.getElementById('backgroundMusic');
        const openSound = document.getElementById('openSound');
        const magicSound = document.getElementById('magicSound');
        const musicControl = document.getElementById('musicControl');
        const musicIcon = document.getElementById('musicIcon');
        let musicPlaying = false;

        // Configurar volúmenes
        music.volume = 0.7; // Música de fondo más alta
        openSound.volume = 0.8;
        magicSound.volume = 0.7;

        // Abrir sobre y crear partículas
        envelopeWrapper.addEventListener('click', function() {
            const wasOpen = this.classList.contains('open');
            this.classList.toggle('open');
            
            if (this.classList.contains('open') && !wasOpen) {
                // Reproducir sonido de apertura
                openSound.currentTime = 0;
                openSound.play().catch(e => console.log('Sonido bloqueado'));
                
                // Reproducir sonido mágico después de un momento
                setTimeout(() => {
                    magicSound.currentTime = 0;
                    magicSound.play().catch(e => console.log('Sonido bloqueado'));
                }, 300);
                
                createSparkles(this);
                
                // Iniciar música si no está reproduciendo
                if (!musicPlaying) {
                    setTimeout(() => {
                        music.play().catch(e => console.log('Autoplay bloqueado'));
                        musicPlaying = true;
                        musicControl.classList.add('playing');
                    }, 800);
                }
            }
        });

        // Control de música
        musicControl.addEventListener('click', function(e) {
            e.stopPropagation();
            if (musicPlaying) {
                music.pause();
                musicPlaying = false;
                this.classList.remove('playing');
                musicIcon.innerHTML = '<path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 14.5v-9l6 4.5-6 4.5z"/>';
            } else {
                music.play();
                musicPlaying = true;
                this.classList.add('playing');
                musicIcon.innerHTML = '<path d="M12 3v10.55c-.59-.34-1.27-.55-2-.55-2.21 0-4 1.79-4 4s1.79 4 4 4 4-1.79 4-4V7h4V3h-6z"/>';
            }
        });

        // Crear partículas brillantes
        function createSparkles(element) {
            const rect = element.getBoundingClientRect();
            const sparkleCount = 30;
            const sparkleSymbols = ['✨', '💫', '⭐', '🌟', '💖', '💗', '💝', '💕', '❤️'];
            const colors = ['#ff0080', '#ff1744', '#ff6b9d', '#c2185b', '#ffd700'];
            
            for (let i = 0; i < sparkleCount; i++) {
                setTimeout(() => {
                    const sparkle = document.createElement('div');
                    sparkle.className = 'sparkle';
                    sparkle.textContent = sparkleSymbols[Math.floor(Math.random() * sparkleSymbols.length)];
                    sparkle.style.left = (rect.left + Math.random() * rect.width) + 'px';
                    sparkle.style.top = (rect.top + Math.random() * rect.height) + 'px';
                    sparkle.style.fontSize = (Math.random() * 25 + 20) + 'px';
                    sparkle.style.color = colors[Math.floor(Math.random() * colors.length)];
                    document.body.appendChild(sparkle);
                    
                    setTimeout(() => sparkle.remove(), 3000);
                }, i * 40);
            }
        }

        // Intentar reproducir música después de interacción
        document.addEventListener('click', function playMusic() {
            if (!musicPlaying) {
                music.play().then(() => {
                    musicPlaying = true;
                    document.removeEventListener('click', playMusic);
                }).catch(e => {});
            }
        }, { once: true });
    </script>

</body>
</html>
