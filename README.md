<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¡Rompe la Piñata Septiembre!</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
        }

        .mexican-flags {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .flag {
            position: absolute;
            width: 25px;
            height: 15px;
            animation: float 4s ease-in-out infinite;
            border-radius: 2px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        .flag-green { background: #006847; height: 33.33%; }
        .flag-white { background: white; height: 33.33%; position: relative; }
        .flag-red { background: #C8102E; height: 33.33%; }

        .eagle {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 6px;
            color: #8B4513;
        }

        .flag:nth-child(1) { 
            top: 10%; 
            left: 10%; 
            animation-delay: 0s; 
        }
        .flag:nth-child(2) { 
            top: 20%; 
            right: 15%; 
            animation-delay: 1s; 
        }
        .flag:nth-child(3) { 
            bottom: 30%; 
            left: 20%; 
            animation-delay: 2s; 
        }
        .flag:nth-child(4) { 
            bottom: 20%; 
            right: 25%; 
            animation-delay: 0.5s; 
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(3deg); }
        }

        .game-container {
            background: rgba(255, 255, 255, 0.95);
            padding: 30px 20px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            text-align: center;
            max-width: 450px;
            width: 90%;
            position: relative;
            z-index: 10;
        }

        .game-completed {
            background: rgba(255, 255, 255, 0.95);
            padding: 30px 20px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
            text-align: center;
            max-width: 450px;
            width: 90%;
            position: relative;
            z-index: 10;
            display: none;
        }

        .title {
            font-size: 2.2em;
            color: #C8102E;
            margin-bottom: 10px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .subtitle {
            font-size: 1.1em;
            color: #006847;
            margin-bottom: 25px;
            font-weight: 600;
        }

        .pinata-area {
            height: 250px;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 25px 0;
        }

        .pinata {
            width: 120px;
            height: 120px;
            background: linear-gradient(45deg, #C8102E 0%, #FCE300 50%, #006847 100%);
            border-radius: 50%;
            position: relative;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: bounce 2s ease-in-out infinite;
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
            border: 4px solid #FFD700;
        }

        .pinata:hover {
            transform: scale(1.1);
            box-shadow: 0 12px 30px rgba(0,0,0,0.4);
        }

        .pinata::before {
            content: "⭐";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2.5em;
            animation: sparkle 1.5s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
        }

        @keyframes sparkle {
            0%, 100% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            50% { opacity: 0.6; transform: translate(-50%, -50%) scale(1.2); }
        }

        .instructions {
            font-size: 1.1em;
            color: #333;
            margin: 20px 0;
            font-weight: 500;
        }

        .footer-msg {
            margin-top: 20px;
            font-size: 0.9em;
            color: #666;
        }

        /* Modales */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }

        .modal-content {
            background: white;
            padding: 35px 25px;
            border-radius: 20px;
            text-align: center;
            max-width: 380px;
            width: 90%;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
            animation: modalAppear 0.5s ease-out;
        }

        .lose-modal .modal-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        @keyframes modalAppear {
            0% { transform: scale(0.7) rotate(5deg); opacity: 0; }
            100% { transform: scale(1) rotate(0deg); opacity: 1; }
        }

        .modal-title {
            font-size: 1.8em;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .modal-text {
            font-size: 1.1em;
            margin-bottom: 15px;
            line-height: 1.4;
        }

        .prize-highlight {
            background: linear-gradient(45deg, #FFD700, #FFA500);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            font-weight: bold;
            color: #8B4513;
            box-shadow: 0 5px 15px rgba(255,215,0,0.3);
        }

        .lose-highlight {
            background: rgba(255,255,255,0.2);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            font-weight: bold;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 10px 5px;
        }

        .btn-primary {
            background: #C8102E;
            color: white;
        }

        .btn-primary:hover {
            background: #A00E2A;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .btn-secondary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }

        .btn-secondary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        /* Animaciones de confeti y dulces */
        .confetti {
            position: fixed;
            pointer-events: none;
            z-index: 1500;
        }

        .candy {
            position: absolute;
            font-size: 1.5em;
            pointer-events: none;
            animation: fall 2.5s ease-in forwards;
        }

        @keyframes fall {
            0% { 
                transform: translateY(-30px) rotate(0deg);
                opacity: 1;
            }
            100% { 
                transform: translateY(200px) rotate(360deg);
                opacity: 0;
            }
        }

        .broken-pinata {
            animation: explode 0.6s ease-out forwards;
        }

        @keyframes explode {
            0% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.4) rotate(15deg); }
            100% { transform: scale(0) rotate(180deg); opacity: 0; }
        }

        .completed-title {
            font-size: 2em;
            color: #C8102E;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .completed-text {
            font-size: 1.2em;
            color: #006847;
            margin-bottom: 20px;
            line-height: 1.5;
        }

        .social-section {
            background: linear-gradient(45deg, #C8102E, #006847);
            padding: 20px;
            border-radius: 15px;
            color: white;
            margin: 20px 0;
        }

        .social-section h3 {
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .warning-message {
            background: #ffebee;
            border: 2px solid #f44336;
            color: #c62828;
            padding: 20px;
            border-radius: 10px;
            font-weight: bold;
        }

        /* Responsive */
        @media (max-width: 480px) {
            .title { font-size: 1.8em; }
            .subtitle { font-size: 1em; }
            .pinata { width: 100px; height: 100px; }
            .pinata::before { font-size: 2em; }
            .game-container, .game-completed { padding: 20px 15px; }
        }
    </style>
</head>
<body>
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

    <div class="game-container" id="gameContainer">
        <h1 class="title">¡Rompe la Piñata!</h1>
        <p class="subtitle">🇲🇽 Celebra Septiembre con nosotros 🇲🇽</p>
        
        <div class="pinata-area">
            <div class="pinata" id="pinata" onclick="breakPinata()"></div>
        </div>
        
        <p class="instructions">¡Haz clic en la piñata para descubrir tu premio!</p>
        
        <div class="footer-msg">
            <p>🎉 ¡Que viva México! 🎉</p>
        </div>
    </div>

    <div class="game-completed" id="gameCompleted">
        <h2 class="completed-title">¡Gracias por participar! 🎊</h2>
        <p class="completed-text">
            ¡Esperamos que hayas disfrutado de nuestra piñata virtual!<br>
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
            <h2 class="modal-title">🎉 ¡FELICIDADES! 🎉</h2>
            <p class="modal-text">¡Has ganado nuestro premio especial!</p>
            <div class="prize-highlight">
                <strong>Pack de 4 shots para tu siguiente compra:</strong><br>
                • Immune Boost 50 ml<br>
                • Gingerlicious 50 ml
            </div>
            <p class="modal-text">¡Contacta con nosotros para reclamar tu premio!</p>
            <button class="btn btn-primary" onclick="closePrize()">¡Increíble!</button>
        </div>
    </div>

    <!-- Modal de Pérdida -->
    <div class="modal lose-modal" id="loseModal">
        <div class="modal-content">
            <h2 class="modal-title">😅 ¡Uffff!</h2>
            <p class="modal-text">¡Esta vez la piñata se resistió!</p>
            <div class="lose-highlight">
                <strong>¡Suerte para la próxima! 🍀</strong><br>
                Pero no te preocupes, siempre hay más oportunidades
            </div>
            <p class="modal-text">¡Síguenos en redes para más sorpresas!</p>
            <button class="btn btn-secondary" onclick="closeLose()">¡Entendido!</button>
        </div>
    </div>

    <!-- Modal de Ya Jugó -->
    <div class="modal" id="alreadyPlayedModal">
        <div class="modal-content">
            <div class="warning-message">
                <h2>⚠️ ¡Oops!</h2>
                <p>Ya participaste en este juego anteriormente.</p>
                <p><strong>Solo se permite una participación por persona.</strong></p>
                <p style="margin-top: 15px;">¡Gracias por tu comprensión! 😊</p>
            </div>
            <button class="btn btn-primary" onclick="closeAlreadyPlayed()">Entendido</button>
        </div>
    </div>

    <script>
        // Sistema anti-trampas
        const STORAGE_KEY = 'pinata_game_played';
        const WIN_PROBABILITY = 0.3; // 30% de ganar
        let gameActive = false;

        // Verificar si ya jugó al cargar la página
        window.addEventListener('DOMContentLoaded', function() {
            checkIfAlreadyPlayed();
        });

        function checkIfAlreadyPlayed() {
            // Verificar múltiples métodos de detección
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
            // Guardar en múltiples lugares para prevenir trampas
            const timestamp = new Date().getTime();
            localStorage.setItem(STORAGE_KEY, timestamp);
            sessionStorage.setItem(STORAGE_KEY, timestamp);
            setCookie(STORAGE_KEY, timestamp, 30); // 30 días
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

        function breakPinata() {
            // Verificar si ya jugó antes de permitir jugar
            if (checkIfAlreadyPlayed()) {
                return;
            }

            if (gameActive) return;
            gameActive = true;

            // Marcar como jugado inmediatamente
            markAsPlayed();

            const pinata = document.getElementById('pinata');
            pinata.classList.add('broken-pinata');
            
            // Crear dulces cayendo
            createFallingCandy();
            
            // Reproducir sonido
            playBreakSound();
            
            // Determinar resultado
            const playerWins = Math.random() < WIN_PROBABILITY;
            
            if (playerWins) {
                createConfetti();
                setTimeout(() => {
                    document.getElementById('prizeModal').style.display = 'flex';
                }, 800);
            } else {
                setTimeout(() => {
                    document.getElementById('loseModal').style.display = 'flex';
                }, 800);
            }
        }

        function createFallingCandy() {
            const candies = ['🍬', '🍭', '🍫', '🧁', '🍯', '🍪'];
            const container = document.querySelector('.pinata-area');
            
            for (let i = 0; i < 12; i++) {
                setTimeout(() => {
                    const candy = document.createElement('div');
                    candy.className = 'candy';
                    candy.textContent = candies[Math.floor(Math.random() * candies.length)];
                    candy.style.left = Math.random() * 80 + 10 + '%';
                    candy.style.animationDelay = Math.random() * 0.3 + 's';
                    container.appendChild(candy);
                    
                    setTimeout(() => {
                        if (candy.parentNode) {
                            candy.parentNode.removeChild(candy);
                        }
                    }, 3000);
                }, i * 80);
            }
        }

        function createConfetti() {
            const colors = ['#FFD700', '#FF6B6B', '#4ECDC4', '#45B7D1', '#C8102E', '#006847'];
            
        function createConfetti() {
            const colors = ['#2d5a3d', '#4a8b5c', '#6bb77b', '#FFD700', '#FF6B35', '#58D68D'];
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * 100 + 'vw';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.width = Math.random() * 8 + 4 + 'px';
                    confetti.style.height = confetti.style.width;
                    confetti.style.animation = `fall ${Math.random() * 2 + 1.5}s linear forwards`;
                    confetti.style.position = 'fixed';
                    confetti.style.top = '-10px';
                    confetti.style.pointerEvents = 'none';
                    confetti.style.zIndex = '1500';
                    
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        if (confetti.parentNode) {
                            confetti.parentNode.removeChild(confetti);
                        }
                    }, 4000);
                }, i * 40);
            }
        }

        function playBreakSound() {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                oscillator.frequency.setValueAtTime(600, audioContext.currentTime);
                oscillator.frequency.exponentialRampToValueAtTime(200, audioContext.currentTime + 0.4);
                
                gainNode.gain.setValueAtTime(0.2, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.4);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + 0.4);
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

        // Detectar si intentan abrir herramientas de desarrollador
        let devtools = false;
        setInterval(function() {
            if (window.outerHeight - window.innerHeight > 200 || window.outerWidth - window.innerWidth > 200) {
                if (!devtools) {
                    devtools = true;
                    console.log("🎮 ¡Juega limpio! 😊");
                }
            }
        }, 500);
    </script>
</body>
</html>
