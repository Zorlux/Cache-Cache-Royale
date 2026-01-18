<!--Cache-Cache Royale-->
<!--6851-->
<!--28947361-->
<!--73916428-->
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cache-Cache Royale</title>
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
            color: white;
        }

        .container {
            text-align: center;
            padding: 20px;
            max-width: 1200px;
            width: 100%;
        }

        h1 {
            font-size: 3em;
            margin-bottom: 30px;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.5);
        }

        .menu-buttons {
            display: flex;
            flex-direction: column;
            gap: 20px;
            align-items: center;
        }

        .btn {
            padding: 20px 50px;
            font-size: 1.5em;
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            border: none;
            border-radius: 15px;
            color: white;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            transition: transform 0.2s;
            font-weight: bold;
        }

        .btn:hover {
            transform: scale(1.05);
        }

        .difficulty-buttons {
        display: flex;
        flex-direction: column;
        gap: 15px;
        align-items: center;
        }


        .game-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            font-size: 1.5em;
            font-weight: bold;
        }

        .timer {
            font-size: 3em;
            font-weight: bold;
            color: #ff6b6b;
            text-shadow: 3px 3px 10px rgba(0,0,0,0.5);
            text-align: center;
            margin-bottom: 20px;
        }

        .difficulty-selected {
            transform: scale(1.1);
            border: 4px solid #ffd93d;
            box-shadow: 0 0 25px rgba(255, 217, 61, 0.6);
        }

        .cards-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 10px;
            padding: 20px;
        }

        .card {
            padding: 15px;
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            border: 3px solid #fff;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.9em;
            transition: all 0.2s;
            box-shadow: 0 3px 10px rgba(0,0,0,0.3);
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.4);
        }

        .message-box {
            font-size: 2em;
            line-height: 1.6;
            margin: 50px 0;
        }

        .countdown {
            font-size: 3em;
            color: #ffd93d;
            font-weight: bold;
        }

        .hidden {
            display: none;
        }

        .final-score {
            font-size: 2.5em;
            margin: 30px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <div id="menuScreen">
            <h1>🏆 CACHE-CACHE ROYALE 🏆</h1>
            <div id="playerTitle" style="font-size: 1.8em; margin-bottom: 15px; color: #ffd93d; text-shadow: 2px 2px 5px rgba(0,0,0,0.5); line-height: 1.8;"></div>
            <div style="font-size: 1.5em; margin-bottom: 10px; color: #ffd93d;">SCORES:</div>
            <div style="font-size: 1.3em; margin-bottom: 20px; line-height: 2;">
                <div style="color: #84fab0;">😊 Facile: <span id="bestScoreEasy">-</span>/10</div>
                <div style="color: #ffd89b;">😐 Normal: <span id="bestScoreNormal">-</span>/10</div>
                <div style="color: #ff6b6b;">😈 Difficile: <span id="bestScoreHard">-</span>/10</div>
                <div id="expertMode" style="color: #a855f7; display: none;">👑 Expert: <span id="bestScoreExpert">-</span>/10</div>
            </div>
            <div class="menu-buttons">
                <button class="btn" onclick="showOptions()">JOUER</button>
                <button class="btn" onclick="showRules()">RÈGLES</button>
                <button class="btn" onclick="showCredits()">CRÉDITS</button>
                <button class="btn" onclick="showCodeScreen()">CODES</button>
            </div>
        </div>

        <div id="creditsScreen" class="hidden">
            <h1>CRÉDITS</h1>
            <div class="credits">
                <p><strong>Conception • Programmation • Design</strong></p>
                <p style="font-size: 1.5em; margin-top: 20px;"><strong>Zorlux</strong></p>
            </div>
            <button class="btn" onclick="backToMenu()" style="margin-top: 30px;">RETOUR</button>
        </div>

        <div id="codeScreen" class="hidden">
            <h1>CODES SECRETS</h1>
            <div class="credits">
                <p style="font-size: 1.2em; margin-bottom: 30px;">Trouve les codes secrets pour avoir des badges exclusifs !</p>
                <input type="text" id="codeInput" placeholder="Entrez un code à 4 chiffres" maxlength="8" 
                    style="padding: 15px; font-size: 1.5em; border-radius: 10px; border: 3px solid #fff; text-align: center; width: 300px; background: rgba(255,255,255,0.2); color: white; font-weight: bold;">
                <br>
                <button class="btn" onclick="validateCode()" style="margin-top: 15px; width: 150px; padding: 10px 20px; font-size: 1.2em;">VALIDER</button>
                <div id="codeMessage" style="font-size: 1.3em; margin-top: 20px; min-height: 30px;"></div>
            </div>
            <button class="btn" onclick="backToMenu()" style="margin-top: 30px;">RETOUR</button>
        </div>

        <div id="rulesScreen" class="hidden">
            <h1>RÈGLES DU JEU</h1>
            <div class="credits" style="text-align: left; max-width: 600px; margin: 0 auto; line-height: 1.8;">
            <p>🎯 <strong>Objectif :</strong> Trouve le bon bouton parmi les cartes Clash Royale</p>
            <p>⏱️ Tu as un temps limité pour trouver le bon bouton</p>
            <p>🏆 Complète 10 rounds et obtiens le meilleur score possible</p>
            <p>⚡ Un seul bouton fonctionne par round, les autres ne font rien</p>
            <p>📊 Ton score est enregistré à la fin de la partie</p>
            
            <p style="margin-top:20px; color:#ffd93d; font-size: 1.2em;">
            🏅 <strong>Système de titres :</strong>
            </p>
            <p style="margin-left: 20px;">✨ <strong>Apprenti Maître</strong> : Score parfait (10/10) en Facile</p>
            <p style="margin-left: 20px;">🌟 <strong>Champion</strong> : Score parfait (10/10) en Normal</p>
            <p style="margin-left: 20px;">⚡ <strong>Maître Expert</strong> : Score parfait (10/10) en Difficile</p>
            <p style="margin-left: 20px;">👑 <strong>Légende Absolue</strong> : Score parfait (15/15) en Expert</p>
            <p style="margin-left: 20px;">🔑 <strong>???</strong> : trouve les codes</p>
            
            <p style="margin-top:20px; color:#ff6b6b; font-size: 1.1em;">
            🎁 <strong>Badges Secrets :</strong>  
            Explore le jeu et cherche des <strong>codes secrets</strong> pour débloquer des <strong>badges exclusifs</strong> ! Les badges débloqués restent à vie dans ton profil.
            </p>
            
            <p style="margin-top:20px; color:#ecf009; font-size: 1.1em;">
            🔒 <strong>Niveau Expert :</strong>  
            Réalise un <strong>score parfait (10/10)</strong> en mode <strong>Difficile</strong> pour débloquer le <strong>niveau Expert</strong> avec 15 rounds et seulement 3 secondes par round !
            </p>
        </div>

            <button class="btn" onclick="backToMenu()" style="margin-top: 30px;">RETOUR</button>
        </div>

        <div id="optionsScreen" class="hidden">
            <h1>CHOISIS TA DIFFICULTÉ</h1>
            <div class="difficulty-buttons">
            <button class="btn" id="btnEasy" onclick="selectDifficulty(15)" style="background: linear-gradient(135deg, #84fab0 0%, #8fd3f4 100%);">
                😊 FACILE (15 secondes)
            </button>
            <button class="btn difficulty-selected" id="btnNormal" onclick="selectDifficulty(10)" style="background: linear-gradient(135deg, #ffd89b 0%, #19547b 100%); margin-top: 15px;">
                😐 NORMAL (10 secondes)
            </button>
                <button class="btn" id="btnHard" onclick="selectDifficulty(5)" style="background: linear-gradient(135deg, #ff6b6b 0%, #c92a2a 100%); margin-top: 15px;">
                😈 DIFFICILE (5 secondes)
            </button>
    <button class="btn" id="btnExpert" onclick="selectDifficulty(3)" style="background: linear-gradient(135deg, #a855f7 0%, #6366f1 100%); margin-top: 15px; display: none;">
        👑 EXPERT (3 secondes - 15 round)
    </button>
</div>

            <div style="display: flex; gap: 20px; justify-content: center; margin-top: 30px;">
                <button class="btn" onclick="backToMenu()">RETOUR</button>
                <button class="btn" onclick="launchGame()" style="background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);">LANCER</button>
            </div>
        </div>

        <div id="gameScreen" class="hidden">
            <div class="game-info">
                <div>Round: <span id="roundDisplay">1/10</span></div>
                <div>Points: <span id="scoreDisplay">0/10</span></div>
            </div>
            <div id="timerDisplay" class="timer hidden">7</div>
            <div id="cardsContainer" class="cards-container"></div>
            <div id="messageBox" class="message-box hidden"></div>
        </div>

        <div id="endScreen" class="hidden">
            <h1>FIN DU JEU</h1>
            <div id="rewardContainer"></div>
            <div class="final-score">
                Vous avez trouvé <span id="finalScore"></span> bon(s) bouton(s) !
            </div>
            <button class="btn" onclick="backToMenu()">MENU</button>
        </div>
    </div>

    <script>
        // Système de langue
        let currentLanguage = localStorage.getItem('gameLanguage') || navigator.language.startsWith('fr') ? 'fr' : 'en';
        
        const translations = {
            fr: {
                title: "CACHE-CACHE ROYALE",
                play: "JOUER",
                rules: "RÈGLES",
                credits: "CRÉDITS",
                codes: "CODES",
                back: "RETOUR",
                scores: "SCORES:",
                easy: "Facile",
                normal: "Normal",
                hard: "Difficile",
                expert: "Expert",
                creditsTitle: "CRÉDITS",
                creditsRole: "Conception • Programmation • Design",
                codesTitle: "CODES SECRETS",
                codesDesc: "Trouve les codes secrets pour avoir des badges exclusifs !",
                codesPlaceholder: "Entrez un code à 4 chiffres",
                validate: "VALIDER",
                codeInvalid: "❌ CODE INVALIDE",
                codeValid: "✅ CODE VALIDE !<br>Vous avez désormais le badge",
                codeAlready: "⚠️ Vous possédez déjà ce badge !",
                codeLength: "❌ Le code doit contenir 4 chiffres !",
                badgesUnlocked: "BADGES DÉBLOQUÉS :",
                noBadges: "Aucun badge débloqué pour le moment...",
                rulesTitle: "RÈGLES DU JEU",
                objective: "🎯 <strong>Objectif :</strong> Trouve le bon bouton parmi les cartes Clash Royale",
                timeLimit: "⏱️ Tu as un temps limité pour trouver le bon bouton",
                rounds: "🏆 Complète 10 rounds et obtiens le meilleur score possible",
                oneButton: "⚡ Un seul bouton fonctionne par round, les autres ne font rien",
                scoreRecord: "📊 Ton score est enregistré à la fin de la partie",
                chooseDifficulty: "CHOISIS TA DIFFICULTÉ",
                easyBtn: "😊 FACILE (15 secondes)",
                normalBtn: "😐 NORMAL (10 secondes)",
                hardBtn: "😈 DIFFICILE (5 secondes)",
                expertBtn: "👑 EXPERT (3 secondes - 15 rounds)",
                launch: "LANCER",
                round: "Round:",
                points: "Points:",
                prepare: "PRÉPAREZ-VOUS<br>Le jeu va commencer",
                bravo: "BRAVO<br>Tu as trouvé le bon bouton !<br>Prépare-toi pour le prochain round :",
                dommage: "DOMMAGE<br>Tu n'as pas eu assez de temps pour trouver le bon bouton<br>Prépare-toi pour le prochain round :",
                gameOver: "FIN DU JEU",
                finalScore: "Vous avez trouvé",
                finalScoreEnd: "bon(s) bouton(s) !",
                menu: "MENU",
                cards: [
                    "Chevalier", "Archers", "Gobelins", "Géant", "P.E.K.K.A", 
                    "Mini P.E.K.K.A", "Mousquetaire", "Bébé Dragon", "Prince", "Sorcière",
                    "Squelettes", "Valkyrie", "Bombardier", "Géant Royal", "Garde",
                    "Barbares d'Élite", "Golem", "Ballon", "Chevaucheur de Cochon", "Bûcheron",
                    "Princesse", "Méga Chevalier", "Électrocuteur", "Mineur", "Bandit",
                    "Chevalier Noir", "Bourreau", "Sorcier", "Bowler", "Tornade",
                    "Boule de Feu", "Foudre", "Flèches", "Zap", "Bûche", 
                    "Barbare", "Lancier", "Chevalier de Glace", "Mère Sorcière", "Électro-Géant",
                    "Pêcheur", "Chevalier Squelette", "Dragon Infernal", "Gargouilles", "Chien de Lave",
                    "Golem de Glace", "Clone", "Rage"
                ]
            },
            en: {
                title: "HIDE AND SEEK ROYALE",
                play: "PLAY",
                rules: "RULES",
                credits: "CREDITS",
                codes: "CODES",
                back: "BACK",
                scores: "SCORES:",
                easy: "Easy",
                normal: "Normal",
                hard: "Hard",
                expert: "Expert",
                creditsTitle: "CREDITS",
                creditsRole: "Design • Programming • Concept",
                codesTitle: "SECRET CODES",
                codesDesc: "Find secret codes to unlock exclusive badges!",
                codesPlaceholder: "Enter a 4-digit code",
                validate: "VALIDATE",
                codeInvalid: "❌ INVALID CODE",
                codeValid: "✅ VALID CODE!<br>You now have the badge",
                codeAlready: "⚠️ You already have this badge!",
                codeLength: "❌ Code must be 4 digits!",
                badgesUnlocked: "UNLOCKED BADGES:",
                noBadges: "No badges unlocked yet...",
                rulesTitle: "GAME RULES",
                objective: "🎯 <strong>Objective:</strong> Find the right button among Clash Royale cards",
                timeLimit: "⏱️ You have limited time to find the right button",
                rounds: "🏆 Complete 10 rounds and get the best score possible",
                oneButton: "⚡ Only one button works per round, others do nothing",
                scoreRecord: "📊 Your score is recorded at the end of the game",
                chooseDifficulty: "CHOOSE YOUR DIFFICULTY",
                easyBtn: "😊 EASY (15 seconds)",
                normalBtn: "😐 NORMAL (10 seconds)",
                hardBtn: "😈 HARD (5 seconds)",
                expertBtn: "👑 EXPERT (3 seconds - 15 rounds)",
                launch: "START",
                round: "Round:",
                points: "Points:",
                prepare: "GET READY<br>The game will start",
                bravo: "GREAT<br>You found the right button!<br>Get ready for the next round:",
                dommage: "TOO BAD<br>You didn't have enough time to find the right button<br>Get ready for the next round:",
                gameOver: "GAME OVER",
                finalScore: "You found",
                finalScoreEnd: "correct button(s)!",
                menu: "MENU",
                cards: [
                    "Knight", "Archers", "Goblins", "Giant", "P.E.K.K.A", 
                    "Mini P.E.K.K.A", "Musketeer", "Baby Dragon", "Prince", "Witch",
                    "Skeletons", "Valkyrie", "Bomber", "Royal Giant", "Guards",
                    "Elite Barbarians", "Golem", "Balloon", "Hog Rider", "Lumberjack",
                    "Princess", "Mega Knight", "Electro Wizard", "Miner", "Bandit",
                    "Dark Prince", "Executioner", "Wizard", "Bowler", "Tornado",
                    "Fireball", "Lightning", "Arrows", "Zap", "The Log", 
                    "Barbarian", "Spear Goblin", "Ice Wizard", "Night Witch", "Electro Giant",
                    "Fisherman", "Skeleton King", "Inferno Dragon", "Minions", "Lava Hound",
                    "Ice Golem", "Clone", "Rage"
                ]
            }
        };

        const cardsNames = translations[currentLanguage].cards;

        let currentRound = 1;
        let score = 0;
        let correctButton = 0;
        let gameTimer = null;
        let countdownTimer = null;
        let timeLimit = 10;
        let currentDifficulty = 'normal';
        let maxRounds = 10;
        let expertUnlocked = false;

        // Codes secrets et badges
        const secretCodes = {
            '6851': 'Expert du Code',
            '28947361': 'Admin',
            '73916428': 'Créateur'
        };

        // Charger les badges débloqués
        function loadUnlockedBadges() {
            const badges = JSON.parse(localStorage.getItem('unlockedBadges') || '[]');
            return badges;
        }

        function saveUnlockedBadge(badgeName) {
            const badges = loadUnlockedBadges();
            if (!badges.includes(badgeName)) {
                badges.push(badgeName);
                localStorage.setItem('unlockedBadges', JSON.stringify(badges));
            }
        }

        function displayUnlockedBadges() {
            const badges = loadUnlockedBadges();
            const container = document.getElementById('unlockedBadges');
            
            if (badges.length === 0) {
                container.innerHTML = '<p style="color: #aaa;">Aucun badge débloqué pour le moment...</p>';
            } else {
                let html = '';
                badges.forEach(badge => {
                    let icon = '';
                    let color = '#84fab0';
                    if (badge === 'Expert du Code') {
                        icon = '🔍';
                        color = '#ffd93d';
                    } else if (badge === 'Admin') {
                        icon = '⚙️';
                        color = '#a855f7';
                    } else if (badge === 'Créateur') {
                        icon = '🎨';
                        color = '#ff6b6b';
                    }
                    
                    html += `<div style="color: ${color}; margin: 10px 0; padding: 10px; background: rgba(0,0,0,0.2); border-radius: 8px;">${icon} ${badge}</div>`;
                });
                container.innerHTML = html;
            }
        }

        function validateCode() {
            const input = document.getElementById('codeInput');
            const code = input.value.trim();
            const messageBox = document.getElementById('codeMessage');
            
            if (code.length !== 4 && code.length !== 8) {
                messageBox.innerHTML = '<span style="color: #ff6b6b;">❌ Le code doit contenir 4 chiffres !</span>';
                return;
            }
            
            if (secretCodes[code]) {
                const badgeName = secretCodes[code];
                const badges = loadUnlockedBadges();
                
                if (badges.includes(badgeName)) {
                    messageBox.innerHTML = '<span style="color: #ffd93d;">⚠️ Vous possédez déjà ce badge !</span>';
                } else {
                    saveUnlockedBadge(badgeName);
                    messageBox.innerHTML = `<span style="color: #84fab0;">✅ CODE VALIDE !<br>Vous avez désormais le badge "${badgeName}" débloqué !</span>`;
                    displayUnlockedBadges();
                    updatePlayerTitle();
                }
            } else {
                messageBox.innerHTML = '<span style="color: #ff6b6b;">❌ CODE INVALIDE</span>';
            }
            
            input.value = '';
        }

        function showCodeScreen() {
            document.getElementById('menuScreen').classList.add('hidden');
            document.getElementById('codeScreen').classList.remove('hidden');
            displayUnlockedBadges();
        }

        // Charger les meilleurs scores
        function loadBestScores() {
            const easy = localStorage.getItem('clashRoyaleBestScoreEasy');
            const normal = localStorage.getItem('clashRoyaleBestScoreNormal');
            const hard = localStorage.getItem('clashRoyaleBestScoreHard');
            const expert = localStorage.getItem('clashRoyaleBestScoreExpert');
            expertUnlocked = localStorage.getItem('expertUnlocked') === 'true';
            
            if (easy) document.getElementById('bestScoreEasy').textContent = easy;
            if (normal) document.getElementById('bestScoreNormal').textContent = normal;
            if (hard) document.getElementById('bestScoreHard').textContent = hard;
            if (expert) document.getElementById('bestScoreExpert').textContent = expert;
            
            if (expertUnlocked) {
                document.getElementById('expertMode').style.display = 'block';
                document.getElementById('btnExpert').style.display = 'block';
            }
            
            updatePlayerTitle();
        }

        function updatePlayerTitle() {
            const easy = parseInt(localStorage.getItem('clashRoyaleBestScoreEasy') || 0);
            const normal = parseInt(localStorage.getItem('clashRoyaleBestScoreNormal') || 0);
            const hard = parseInt(localStorage.getItem('clashRoyaleBestScoreHard') || 0);
            const expert = parseInt(localStorage.getItem('clashRoyaleBestScoreExpert') || 0);
            const badges = loadUnlockedBadges();
            
            let titles = [];
            
            // Titres de score
            if (expert === 15) titles.push('👑 LÉGENDE ABSOLUE');
            if (hard === 10) titles.push('⚡ MAÎTRE EXPERT');
            if (normal === 10) titles.push('🌟 CHAMPION');
            if (easy === 10) titles.push('✨ APPRENTI MAÎTRE');
            
            // Badges secrets
            badges.forEach(badge => {
                if (badge === 'Expert du Code') titles.push('🔍 EXPERT DU CODE');
                else if (badge === 'Admin') titles.push('⚙️ ADMIN');
                else if (badge === 'Créateur') titles.push('🎨 CRÉATEUR');
            });
            
            const title = titles.length > 0 ? titles.join('<br>') : '';
            document.getElementById('playerTitle').innerHTML = title;
        }

        function saveBestScore() {
            let key = 'clashRoyaleBestScore' + currentDifficulty.charAt(0).toUpperCase() + currentDifficulty.slice(1);
            const current = parseInt(localStorage.getItem(key) || 0);
            if (score > current) {
                localStorage.setItem(key, score);
                loadBestScores();

        // Fonction pour obtenir la traduction
        function t(key) {
            return translations[currentLanguage][key] || key;
        }

        // Mettre à jour les textes de l'interface
        function updateLanguage() {
            document.querySelector('#menuScreen h1').textContent = `🏆 ${t('title')} 🏆`;
            document.querySelector('#menuScreen .menu-buttons button:nth-child(1)').textContent = t('play');
            document.querySelector('#menuScreen .menu-buttons button:nth-child(2)').textContent = t('rules');
            document.querySelector('#menuScreen .menu-buttons button:nth-child(3)').textContent = t('credits');
            document.querySelector('#menuScreen .menu-buttons button:nth-child(4)').textContent = t('codes');
            
            const scoresDiv = document.querySelector('#menuScreen > div:nth-child(3)');
            if (scoresDiv) scoresDiv.textContent = t('scores');
        }

        updateLanguage();
            }
        }

        loadBestScores();

        function startGame() {
            document.getElementById('menuScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.remove('hidden');
            currentRound = 1;
            score = 0;
            maxRounds = (currentDifficulty === 'expert') ? 15 : 10;
            updateDisplay();
            showStartMessage();
        }

        function showStartMessage() {
            const messageBox = document.getElementById('messageBox');
            messageBox.innerHTML = 'PRÉPAREZ-VOUS<br>Le jeu va commencer<br><span class="countdown" id="startCountdown">3</span>';
            messageBox.classList.remove('hidden');

            let countdown = 3;
            countdownTimer = setInterval(() => {
                countdown--;
                document.getElementById('startCountdown').textContent = countdown;

                if (countdown <= 0) {
                    clearInterval(countdownTimer);
                    startRound();
                }
            }, 1000);
        }

        function showCredits() {
            document.getElementById('menuScreen').classList.add('hidden');
            document.getElementById('creditsScreen').classList.remove('hidden');
        }

        function showRules() {
            document.getElementById('menuScreen').classList.add('hidden');
            document.getElementById('rulesScreen').classList.remove('hidden');
        }

        function showOptions() {
            document.getElementById('menuScreen').classList.add('hidden');
            document.getElementById('optionsScreen').classList.remove('hidden');
        }

        function setDifficulty(seconds) {
            timeLimit = seconds;
        }

        function selectDifficulty(seconds) {
            timeLimit = seconds;
            if (seconds === 15) currentDifficulty = 'easy';
            else if (seconds === 10) currentDifficulty = 'normal';
            else if (seconds === 5) currentDifficulty = 'hard';
            else if (seconds === 3) currentDifficulty = 'expert';
            
            // Enlever la sélection de tous les boutons
            document.getElementById('btnEasy').classList.remove('difficulty-selected');
            document.getElementById('btnNormal').classList.remove('difficulty-selected');
            document.getElementById('btnHard').classList.remove('difficulty-selected');
            if (expertUnlocked) document.getElementById('btnExpert').classList.remove('difficulty-selected');
            
            // Ajouter la sélection au bouton cliqué
            if (seconds === 15) document.getElementById('btnEasy').classList.add('difficulty-selected');
            else if (seconds === 10) document.getElementById('btnNormal').classList.add('difficulty-selected');
            else if (seconds === 5) document.getElementById('btnHard').classList.add('difficulty-selected');
            else if (seconds === 3) document.getElementById('btnExpert').classList.add('difficulty-selected');
        }

        function launchGame() {
            document.getElementById('optionsScreen').classList.add('hidden');
            startGame();
        }

        function backToMenu() {
            document.getElementById('creditsScreen').classList.add('hidden');
            document.getElementById('rulesScreen').classList.add('hidden');
            document.getElementById('optionsScreen').classList.add('hidden');
            document.getElementById('endScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.add('hidden');
            document.getElementById('codeScreen').classList.add('hidden');
            document.getElementById('menuScreen').classList.remove('hidden');
        }

        function updateDisplay() {
            const maxRoundsDisplay = (currentDifficulty === 'expert') ? 15 : 10;
            document.getElementById('roundDisplay').textContent = currentRound + '/' + maxRoundsDisplay;
            document.getElementById('scoreDisplay').textContent = score + '/' + maxRoundsDisplay;
        }

        function startRound() {
            document.getElementById('messageBox').classList.add('hidden');
            createCards();
            startTimer();
        }

        function createCards() {
            const container = document.getElementById('cardsContainer');
            container.innerHTML = '';
            
            // Mélanger les cartes aléatoirement
            const shuffledCards = [...cardsNames].sort(() => Math.random() - 0.5);
            correctButton = Math.floor(Math.random() * 48);

            for (let i = 0; i < 48; i++) {
                const card = document.createElement('button');
                card.className = 'card';
                card.textContent = shuffledCards[i];
                
                if (i === correctButton) {
                    card.onclick = () => correctAnswer();
                } else {
                    card.onclick = () => {};
                }
                
                container.appendChild(card);
            }
        }

        function startTimer() {
            let timeLeft = timeLimit;
            const timerDisplay = document.getElementById('timerDisplay');
            timerDisplay.classList.remove('hidden');
            timerDisplay.textContent = timeLeft;

            gameTimer = setInterval(() => {
                timeLeft--;
                timerDisplay.textContent = timeLeft;

                if (timeLeft <= 0) {
                    clearInterval(gameTimer);
                    timerDisplay.classList.add('hidden');
                    wrongAnswer();
                }
            }, 1000);
        }

        function correctAnswer() {
            clearInterval(gameTimer);
            document.getElementById('timerDisplay').classList.add('hidden');
            score++;
            updateDisplay();
            
            if (currentRound >= maxRounds) {
                endGame();
            } else {
                showMessage("BRAVO<br>Tu as trouvé le bon bouton !<br>Prépare-toi pour le prochain round :");
            }
        }

        function wrongAnswer() {
            if (currentRound >= maxRounds) {
                endGame();
            } else {
                showMessage("DOMMAGE<br>Tu n'as pas eu assez de temps pour trouver le bon bouton<br>Prépare-toi pour le prochain round :");
            }
        }

        function showMessage(message) {
            document.getElementById('cardsContainer').innerHTML = '';
            const messageBox = document.getElementById('messageBox');
            messageBox.innerHTML = message + '<br><span class="countdown" id="countdown">5</span>';
            messageBox.classList.remove('hidden');

            let countdown = 5;
            countdownTimer = setInterval(() => {
                countdown--;
                document.getElementById('countdown').textContent = countdown;

                if (countdown <= 0) {
                    clearInterval(countdownTimer);
                    currentRound++;
                    
                    if (currentRound > maxRounds) {
                        endGame();
                    } else {
                        updateDisplay();
                        startRound();
                    }
                }
            }, 1000);
        }

        function endGame() {
            saveBestScore();
            
            // Vérifier si on débloque le mode Expert
            const hard = parseInt(localStorage.getItem('clashRoyaleBestScoreHard') || 0);
            if (hard === 10 && !expertUnlocked) {
                localStorage.setItem('expertUnlocked', 'true');
                expertUnlocked = true;
            }
            
            document.getElementById('gameScreen').classList.add('hidden');
            document.getElementById('endScreen').classList.remove('hidden');
            document.getElementById('finalScore').textContent = score;
            
            showRewards();
        }

        function showRewards() {
            const container = document.getElementById('rewardContainer');
            container.innerHTML = '';
            
            const isPerfect = (currentDifficulty === 'expert' && score === 15) || (currentDifficulty !== 'expert' && score === 10);
            
            if (isPerfect) {
                let title = '';
                
                if (currentDifficulty === 'expert') {
                    title = '👑 LÉGENDE ABSOLUE 👑';
                } else if (currentDifficulty === 'hard') {
                    title = '⚡ MAÎTRE EXPERT ⚡';
                } else if (currentDifficulty === 'normal') {
                    title = '🌟 CHAMPION 🌟';
                } else if (currentDifficulty === 'easy') {
                    title = '✨ APPRENTI MAÎTRE ✨';
                }
                
                container.innerHTML = `
                    <div style="font-size: 2.5em; margin: 30px 0; color: #ffd93d; text-shadow: 2px 2px 5px rgba(0,0,0,0.5);">${title}</div>
                `;
                
                if (currentDifficulty === 'hard' && !localStorage.getItem('expertModeAnnounced')) {
                    container.innerHTML += '<div style="font-size: 1.5em; margin-top: 20px; color: #a855f7;">🔓 MODE EXPERT DÉBLOQUÉ ! 🔓</div>';
                    localStorage.setItem('expertModeAnnounced', 'true');
                }
            }
        }
    </script>
</body>
</html>
