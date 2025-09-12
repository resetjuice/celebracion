<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¡Descubre tu Premio Mexicano!</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: white;
            min-height: 100vh;
            padding: 15px;
            position: relative;
        }

        /* Patrón sutil mexicano de fondo */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                linear-gradient(45deg, rgba(0, 104, 71, 0.02) 25%, transparent 25%),
                linear-gradient(-45deg, rgba(200, 16, 46, 0.02) 25%, transparent 25%),
                white;
            background-size: 30px 30px;
            z-index: -1;
        }

        /* Banderas decorativas - SIN la de arriba */
        .mexican-flags {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .flag {
            position: absolute;
            width: 20px;
            height: 12px;
            animation: float 4s ease-in-out infinite;
            border-radius: 2px;
            overflow: hidden;
            box-shadow: 0 1px 3px rgba(0,0,0,0.2);
            display: flex;
            flex-direction: column;
        }

        .flag-green { background: #006847; height: 33.33%; }
        .flag-white { 
            background: white; 
            height: 33.33%; 
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .flag-red { background: #C8102E; height: 33.33%; }

        .eagle {
            font-size: 4px;
            color: #8B4513;
        }

        /* Posicionamiento de banderas - SIN la de arriba que tapaba */
        .flag:nth-child(1) { bottom: 20%; left: 8%; animation-delay: 0s; }
        .flag:nth-child(2) { top: 25%; right: 12%; animation-delay: 1s; }
        .flag:nth-child(3) { bottom: 35%; right: 20%; animation-delay: 1.5s; }
        .flag:nth-child(4) { top: 60%; left: 5%; animation-delay: 2s; }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-6px) rotate(2deg); }
        }

        /* Contenedor principal */
        .game-container {
            background: rgba(255, 255, 255, 0.98);
            border: 2px solid transparent;
            border-image: linear-gradient(45deg, #006847 0%, white 50%, #C8102E 100%) 1;
            border-radius: 20px;
            padding: 20px;
            max-width: 380px;
            margin: 0 auto;
            position: relative;
            z-index: 10;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .game-completed {
            background: rgba(255, 255, 255, 0.98);
            border: 2px solid transparent;
            border-image: linear-gradient(45deg, #006847 0%, white 50%, #C8102E 100%) 1;
            border-radius: 20px;
            padding: 20px;
            max-width: 380px;
            margin: 0 auto;
            position: relative;
            z-index: 10;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            display: none;
        }

        /* Títulos */
        .title {
            font-size: 1.8em;
            font-weight: bold;
            margin-bottom: 8px;
            text-align: center;
            background: linear-gradient(45deg, #006847, #C8102E);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1.2;
        }

        .subtitle {
            font-size: 1em;
            color: #006847;
            margin-bottom: 15px;
            text-align: center;
            font-weight: 600;
        }

        .instructions {
            font-size: 0.95em;
            color: #006847;
            margin: 15px 0;
            text-align: center;
            font-weight: 500;
            line-height: 1.4;
        }

        /* Grid de comida */
        .food-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin: 15px 0;
        }

        .food-item {
            background: linear-gradient(135deg, #fff 0%, #f8f9fa 100%);
            border: 2px solid #e9ecef;
            border-radius: 15px;
            padding: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .food-item:hover {
            transform: translateY(-3px);
            border-color: #006847;
            box-shadow: 0 8px 20px rgba(0,104,71,0.15);
        }

        .food-item:active {
            transform: translateY(-1px);
        }

        .food-emoji {
            font-size: 2.5em;
            margin-bottom: 8px;
            display: block;
            animation: bounce 2s ease-in-out infinite;
        }

        .food-item:nth-child(1) .food-emoji { animation-delay: 0s; }
        .food-item:nth-child(2) .food-emoji { animation-delay: 0.3s; }
        .food-item:nth-child(3) .food-emoji { animation-delay: 0.6s; }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-5px); }
            60% { transform: translateY(-2px); }
        }

        .food-name {
            font-size: 1.1em;
            font-weight: bold;
            color: #333;
            margin-bottom: 4px;
        }

        .food-description {
            font-size: 0.8em;
            color: #666;
            line-height: 1.3;
        }

        .footer-msg {
            margin-top: 15px;
            font-size: 0.9em;
            color: #C8102E;
            font-weight: 500;
            text-align: center;
        }

        /* Modales */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            padding: 20px;
        }

        .modal-content {
            background: white;
            border-radius: 20px;
            padding: 25px 20px;
            text-align: center;
            max-width: 350px;
            width: 100%;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            animation: modalAppear 0.5s ease-out;
            border: 2px solid transparent;
            border-image: linear-gradient(45deg, #006847, white, #C8102E) 1;
        }

        .lose-modal .modal-content {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
        }

        @keyframes modalAppear {
            0% { transform: scale(0.8) rotate(3deg); opacity: 0; }
            100% { transform: scale(1) rotate(0deg); opacity: 1; }
        }

        .modal-title {
            font-size: 1.6em;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .modal-title.win {
            background: linear-gradient(45deg, #006847, #C8102E);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .modal-title.lose {
            color: #666;
        }

        .modal-text {
            font-size: 1em;
            margin-bottom: 15px;
            line-height: 1.4;
            color: #333;
        }

        .prize-highlight {
            background: linear-gradient(45deg, #FFD700, #FFA500);
            padding: 15px;
            border-radius: 12px;
            margin: 15px 0;
            font-weight: bold;
            color: #8B4513;
            box-shadow: 0 5px 15px rgba(255,215,0,0.2);
        }

        .lose-highlight {
            background: linear-gradient(45deg, #e9ecef, #f8f9fa);
            padding: 15px;
            border-radius: 12px;
            margin: 15px 0;
            font-weight: bold;
            color: #666;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 20px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 10px 5px;
        }

        .btn-primary {
            background: linear-gradient(45deg, #006847, #2d5a3d);
            color: white;
        }

        .btn-primary:hover {
            background: linear-gradient(45deg, #004d35, #1e3d2a);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,104,71,0.3);
        }

        .btn-secondary {
            background: linear-gradient(45deg, #6c757d, #495057);
            color: white;
        }

        .btn-secondary:hover {
            background: linear-gradient(45deg, #5a6268, #3d434a);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(108,117,125,0.3);
        }

        /* Efectos especiales */
        .confetti {
            position: fixed;
            pointer-events: none;
            z-index: 1500;
        }

        .food-burst {
            position: absolute;
            font-size: 1.2em;
            pointer-events: none;
            animation: burst 2s ease-out forwards;
        }

        @keyframes burst {
            0% { 
                transform: translateY(0) rotate(0deg) scale(1);
                opacity: 1;
            }
            100% { 
                transform: translateY(-120px) rotate(360deg) scale(0.3);
                opacity: 0;
            }
        }

        .selected-food {
            animation: foodExplode 0.8s ease-out forwards;
            border-color: #FFD700 !important;
            background: linear-gradient(135deg, #FFD700, #FFA500) !important;
        }

        @keyframes foodExplode {
            0% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.1) rotate(3deg); }
            100% { transform: scale(1.05) rotate(0deg); }
        }

        .completed-title {
            font-size: 1.8em;
            background: linear-gradient(45deg, #006847, #C8102E);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 15px;
            font-weight: bold;
            text-align: center;
        }

        .completed-text {
            font-size: 1em;
            color: #006847;
            margin-bottom: 20px;
            line-height: 1.5;
            text-align: center;
        }

        .social-section {
            background: linear-gradient(45deg, #006847, #C8102E);
            padding: 20px;
            border-radius: 15px;
            color: white;
            margin: 20px 0;
        }

        .social-section h3 {
            margin-bottom: 10px;
            font-size: 1em;
        }

        .warning-message {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border: 2px solid #006847;
            color: #006847;
            padding: 20px;
            border-radius: 12px;
            font-weight: bold;
        }

        /* Ocultar banderas en pantallas muy pequeñas */
        @media (max-width: 350px) {
            .mexican-flags {
                display: none;
            }
            
            .game-container, .game-completed {
                max-width: 320px;
                padding: 15px;
            }
            
            .title {
                font-size: 1.6em;
            }
        }

        /* Tablet y desktop */
        @media (min-width: 768px) {
            body {
                padding: 30px;
                display: flex;
                justify-content: center;
                align-items: center;
            }
            
            .game-container, .game-completed {
                max-width: 500px;
                padding: 30px;
            }
            
            .food-grid {
                display: grid;
                grid-template-columns: repeat(3, 1fr);
                gap: 20px;
                margin: 25px 0;
            }
            
            .title {
                font-size: 2.2em;
            }
            
            .subtitle {
                font-size: 1.2em;
            }
            
            .food-emoji {
                font-size: 3.5em;
            }
        }
    </style>
</head>
<body>
    <!-- Banderas decorativas SIN la de arriba -->
    <div class="mexican-flags">
        <div class="flag">
            <div class="flag-green"></div>
            <div class="flag-white"><span class="eagle">🦅</span></div>
            <div class="flag-red"></div>
        </div>
        <div class="flag">
            <div class="flag-green"></div>
            <div class="flag-white"><span class="eagle">🦅</span></div>
            <div class="flag-red"></div>
        </div>
        <div class="flag">
            <div class="flag-green"></div>
            <div class="flag-white"><span class="eagle">🦅</span></div>
            <div class="flag-red"></div>
        </div>
        <div class="flag">
            <div class="flag-green"></div>
            <div class="flag-white"><span class="eagle">🦅</span></div>
            <div class="flag-red"></div>
        </div>
    </div>

    <!-- Contenedor principal del juego -->
    <div class="game-container" id="gameContainer">
        <h1 class="title">¡Descubre tu Premio!</h1>
        <p class="subtitle">🇲🇽 Elige tu platillo mexicano favorito 🇲🇽</p>
        
        <p class="instructions">¡Uno de estos deliciosos platillos esconde tu premio!</p>
        
        <div class="food-grid">
            <div class="food-item" onclick="selectFood('pozole', this)">
                <span class="food-emoji">🍲</span>
                <div class="food-name">Pozole</div>
                <div class="food-description">Tradicional sopa con maíz y carne</div>
            </div>
            
            <div class="food-item" onclick="selectFood('enchiladas', this)">
                <span class="food-emoji">🌯</span>
                <div class="food-name">Enchiladas</div>
                <div class="food-description">Tortillas bañadas en salsa picante</div>
            </div>
            
            <div class="food-item" onclick="selectFood('tacos', this)">
                <span class="food-emoji">🌮</span>
                <div class="food-name">Tacos</div>
                <div class="food-description">El platillo más querido de México</div>
            </div>
        </div>
        
        <div class="footer-msg">
            <p>🎉 ¡Celebra con Reste Juice! 🎉</p>
        </div>
    </div>

    <!-- Pantalla de agradecimiento -->
    <div class="game-completed" id="gameCompleted">
        <h2 class="completed-title">¡Gracias por participar! 🎊</h2>
        <p class="completed-text">
            ¡Esperamos que hayas disfrutado de nuestro juego mexicano!<br>
            Este septiembre celebramos contigo las fiestas patrias.
        </p>
        <div class="social-section">
            <h3>📱 ¡Síguenos para más sorpresas!</h3>
            <p>🎁 Más promociones • 🎉 Eventos especiales • 📢 Noticias</p>
        </div>
        <p style="margin-top: 15px; color: #666; font-size: 0.9em;">
            ¡Comparte esta experiencia con tus amigos!
        </p>
    </div>

    <!-- Modal de Premio -->
    <div class="modal" id="prizeModal">
        <div class="modal-content">
            <h2 class="modal-title win">🎉 ¡felicidades! 🎉</h2>
            <p class="modal-text">¡tu platillo favorito tenía el premio escondido!</p>
            <div class="prize-highlight">
                <strong>gratis pack de 2 immune boost 50 ml + 2 gingerlicious 50 ml.</strong><br>
                con valor de $160 mxn en tu próxima compra.
            </div>
            <p class="modal-text">¡contacta con nosotros para reclamar tu premio!</p>
            <button class="btn btn-primary" onclick="closePrize()">¡increíble!</button>
        </div>
    </div>

    <!-- Modal de Pérdida -->
    <div class="modal lose-modal" id="loseModal">
        <div class="modal-content">
            <h2 class="modal-title lose">😅 ¡qué lástima!</h2>
            <p class="modal-text">¡este platillo no tenía premio escondido!</p>
            <div class="lose-highlight">
                <strong>llévate una caja detox one day y la segunda con 10% de descuento.</strong><br>
                pero no te preocupes, siempre hay más oportunidades
            </div>
            <p class="modal-text">¡síguenos en redes para más sorpresas!</p>
            <button class="btn btn-secondary" onclick="closeLose()">¡entendido!</button>
        </div>
    </div>

    <!-- Modal de Ya Jugó -->
    <div class="modal" id="alreadyPlayedModal">
        <div class="modal-content">
            <div class="warning-message">
                <h2>⚠️ ¡oops!</h2>
                <p>ya participaste en este juego anteriormente.</p>
                <p><strong>solo se permite una participación por persona.</strong></p>
                <p style="margin-top: 15px;">¡gracias por tu comprensión! 😊</p>
            </div>
            <button class="btn btn-primary" onclick="closeAlreadyPlayed()">entendido</button>
        </div>
    </div>

    <script>
        // Sistema anti-trampas
        const STORAGE_KEY = 'mexican_food_game_played';
        const WIN_PROBABILITY = 0.3; // 30% de ganar
        let gameActive = false;

        // Verificar si ya jugó al cargar la página
        window.addEventListener('DOMContentLoaded', function() {
            checkIfAlreadyPlayed();
        });

        function checkIfAlreadyPlayed() {
            const hasPlayed = localStorage.getItem(STORAGE_KEY) ||
                             sessionStorage.getItem(STORAGE_KEY) ||
                             getCookie(STORAGE_KEY);
            
            if (hasPlayed) {
                showAlreadyPlayedModal();
                return true;
            }
            return false;
        }

        function markAsPlayed() {
            const timestamp = new Date().getTime();
            localStorage.setItem(STORAGE_KEY, timestamp);
            sessionStorage.setItem(STORAGE_KEY, timestamp);
            setCookie(STORAGE_KEY, timestamp, 30);
        }

        function setCookie(name, value, days) {
            const expires = new Date();
            expires.setTime(expires.getTime() + (days * 24 * 60 * 60 * 1000));
            document.cookie = name + '=' + value + ';expires=' + expires.toUTCString() + ';path=/';
        }

        function getCookie(name) {
            const nameEQ = name + "=";
            const ca = document.cookie.split(';');
            for (let i = 0; i < ca.length; i++) {
                let c = ca[i];
                while (c.charAt(0) == ' ') c = c.substring(1, c.length);
                if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length, c.length);
            }
            return null;
        }

        function selectFood(foodType, element) {
            if (checkIfAlreadyPlayed()) {
                return;
            }

            if (gameActive) return;
            gameActive = true;

            markAsPlayed();

            // Animar el elemento seleccionado
            element.classList.add('selected-food');
            
            // Deshabilitar otros elementos
            const allFoodItems = document.querySelectorAll('.food-item');
            allFoodItems.forEach(item => {
                if (item !== element) {
                    item.style.opacity = '0.5';
                    item.style.pointerEvents = 'none';
                }
            });

            // Crear explosión de comida
            createFoodBurst(element, foodType);
            
            // Reproducir sonido
            playSelectionSound();
            
            // Determinar resultado
            const playerWins = Math.random() < WIN_PROBABILITY;
            
            if (playerWins) {
                createConfetti();
                setTimeout(() => {
                    document.getElementById('prizeModal').style.display = 'flex';
                }, 1200);
            } else {
                setTimeout(() => {
                    document.getElementById('loseModal').style.display = 'flex';
                }, 1200);
            }
        }

        function createFoodBurst(element, foodType) {
            const foodEmojis = {
                'pozole': ['🌽', '🥄', '🍲', '🌶️'],
                'enchiladas': ['🌯', '🧄', '🧅', '🌶️'],
                'tacos': ['🌮', '🥩', '🧅', '🌿']
            };
            
            const emojis = foodEmojis[foodType] || ['🎉', '⭐', '✨'];
            const rect = element.getBoundingClientRect();
            
            for (let i = 0; i < 6; i++) {
                setTimeout(() => {
                    const burst = document.createElement('div');
                    burst.className = 'food-burst';
                    burst.textContent = emojis[Math.floor(Math.random() * emojis.length)];
                    burst.style.position = 'fixed';
                    burst.style.left = (rect.left + rect.width/2) + 'px';
                    burst.style.top = (rect.top + rect.height/2) + 'px';
                    burst.style.transform = `translate(${(Math.random() - 0.5) * 80}px, ${(Math.random() - 0.5) * 80}px)`;
                    burst.style.zIndex = '1500';
                    
                    document.body.appendChild(burst);
                    
                    setTimeout(() => {
                        if (burst.parentNode) {
                            burst.parentNode.removeChild(burst);
                        }
                    }, 2500);
                }, i * 100);
            }
        }

        function createConfetti() {
            const colors = ['#006847', '#C8102E', '#FFD700', '#FFA500', '#58D68D'];
            
            for (let i = 0; i < 40; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.position = 'fixed';
                    confetti.style.left = Math.random() * 100 + 'vw';
                    confetti.style.top = '-10px';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.width = Math.random() * 8 + 4 + 'px';
                    confetti.style.height = confetti.style.width;
                    confetti.style.pointerEvents = 'none';
                    confetti.style.zIndex = '1500';
                    confetti.style.animation = `burst ${Math.random() * 2 + 1.5}s linear forwards`;
                    
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        if (confetti.parentNode) {
                            confetti.parentNode.removeChild(confetti);
                        }
                    }, 4000);
                }, i * 50);
            }
        }

        function playSelectionSound() {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                oscillator.frequency.setValueAtTime(500, audioContext.currentTime);
                oscillator.frequency.exponentialRampToValueAtTime(700, audioContext.currentTime + 0.2);
                
                gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.3);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + 0.3);
            } catch (e) {
                // Silenciar errores de audio
            }
        }

        function closePrize() {
            document.getElementById('prizeModal').style.display = 'none';
            showCompletedScreen();
        }

        function closeLose() {
            document.getElementById('loseModal').style.display = 'none';
            showCompletedScreen();
        }

        function showAlreadyPlayedModal() {
            document.getElementById('alreadyPlayedModal').style.display = 'flex';
        }

        function closeAlreadyPlayed() {
            document.getElementById('alreadyPlayedModal').style.display = 'none';
            showCompletedScreen();
        }

        function showCompletedScreen() {
            document.getElementById('gameContainer').style.display = 'none';
            document.getElementById('gameCompleted').style.display = 'block';
        }

        // Prevenir trucos adicionales
        window.addEventListener('beforeunload', function() {
            if (gameActive) {
                markAsPlayed();
            }
        });

        // Detectar herramientas de desarrollador
        let devtools = false;
        setInterval(function() {
            if (window.outerHeight - window.innerHeight > 200 || window.outerWidth - window.innerWidth > 200) {
                if (!devtools) {
                    devtools = true;
                    console.log("🌮 ¡Juega limpio, compadre! 😊");
                }
            }
        }, 1000);
    </script>
</body>
</html>
