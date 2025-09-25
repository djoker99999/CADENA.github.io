<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🎰 Jeu du Cadenas - Récompenses Spéciales</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Arial', sans-serif;
      background: url('https://images.unsplash.com/photo-1589829545856-d10d557cf95f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2070&q=80') no-repeat center center fixed;
      background-size: cover;
      color: #fff;
      text-align: center;
      min-height: 100vh;
      padding: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    body::before {
      content: '';
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.6);
      z-index: -1;
    }

    .game-container {
      max-width: 900px;
      width: 100%;
      background: rgba(0, 0, 0, 0.8);
      border-radius: 20px;
      padding: 30px;
      backdrop-filter: blur(10px);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.7);
      border: 3px solid rgba(255, 215, 0, 0.5);
      position: relative;
      overflow: hidden;
    }

    .game-container::before {
      content: '';
      position: absolute;
      top: -5px;
      left: -5px;
      right: -5px;
      bottom: -5px;
      background: linear-gradient(45deg, #ffd700, #ff6b9d, #c44569, #ffd700);
      border-radius: 25px;
      z-index: -1;
      animation: borderGlow 3s linear infinite;
    }

    @keyframes borderGlow {
      0% { filter: hue-rotate(0deg); }
      100% { filter: hue-rotate(360deg); }
    }

    h1 {
      font-size: 2.8em;
      margin-bottom: 15px;
      text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
      background: linear-gradient(45deg, #ff6b9d, #feca57);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .jackpot {
      font-size: 1.5em;
      color: #feca57;
      margin-bottom: 20px;
      font-weight: bold;
      text-shadow: 0 0 10px rgba(254, 202, 87, 0.8);
    }

    .difficulty-selector {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin: 20px 0;
      flex-wrap: wrap;
    }

    .difficulty-btn {
      padding: 12px 20px;
      font-size: 16px;
      cursor: pointer;
      border: 2px solid rgba(255, 255, 255, 0.3);
      border-radius: 20px;
      background: rgba(255, 255, 255, 0.1);
      color: #fff;
      transition: all 0.3s ease;
      backdrop-filter: blur(5px);
      min-width: 120px;
      font-weight: bold;
    }

    .difficulty-btn:hover {
      background: rgba(255, 255, 255, 0.2);
      transform: translateY(-2px);
    }

    .difficulty-btn.active {
      background: linear-gradient(45deg, #ff6b9d, #feca57);
      border-color: #fff;
      box-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
    }

    .difficulty-btn.easy {
      border-color: #2ecc71;
    }

    .difficulty-btn.medium {
      border-color: #feca57;
    }

    .difficulty-btn.hard {
      border-color: #ff6b9d;
    }

    .difficulty-btn.expert {
      border-color: #c44569;
    }

    .lock-container {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin: 30px 0;
      perspective: 1000px;
      flex-wrap: wrap;
    }

    .digit-wheel {
      width: 70px;
      height: 110px;
      background: linear-gradient(145deg, #2c3e50, #34495e);
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 3em;
      font-weight: bold;
      color: #feca57;
      box-shadow: 
        inset 0 0 10px rgba(0, 0, 0, 0.5),
        0 5px 15px rgba(0, 0, 0, 0.3);
      border: 3px solid #feca57;
      position: relative;
      overflow: hidden;
      transition: transform 0.3s;
    }

    .digit-wheel:hover {
      transform: translateY(-5px);
    }

    .digit-wheel::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 50%;
      background: linear-gradient(to bottom, rgba(255,255,255,0.1), transparent);
      pointer-events: none;
    }

    .digit-wheel::after {
      content: '';
      position: absolute;
      top: 50%;
      left: 0;
      right: 0;
      height: 2px;
      background: #feca57;
      box-shadow: 0 0 10px #feca57;
    }

    .digit-wheel.winning {
      animation: winPulse 0.5s ease-in-out 3;
      background: linear-gradient(145deg, #27ae60, #2ecc71);
      color: white;
    }

    @keyframes winPulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.1); }
    }

    .digit-wheel.spinning {
      animation: spinDigit 0.1s linear infinite;
    }

    @keyframes spinDigit {
      0% { transform: translateY(0); }
      50% { transform: translateY(-5px); }
      100% { transform: translateY(0); }
    }

    .attack-modes {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin: 20px 0;
      flex-wrap: wrap;
    }

    .attack-mode-btn {
      padding: 10px 15px;
      font-size: 14px;
      cursor: pointer;
      border: 2px solid rgba(255, 255, 255, 0.3);
      border-radius: 20px;
      background: rgba(255, 255, 255, 0.1);
      color: #fff;
      transition: all 0.3s ease;
      backdrop-filter: blur(5px);
      min-width: 60px;
      font-weight: bold;
    }

    .attack-mode-btn:hover {
      background: rgba(255, 255, 255, 0.2);
      transform: translateY(-2px);
    }

    .attack-mode-btn.active {
      background: linear-gradient(45deg, #ff6b9d, #feca57);
      border-color: #fff;
      box-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
    }

    .controls {
      margin: 25px 0;
    }

    button {
      padding: 15px 30px;
      margin: 10px;
      font-size: 18px;
      cursor: pointer;
      border: none;
      border-radius: 50px;
      background: linear-gradient(45deg, #ff6b9d, #c44569);
      color: #fff;
      transition: all 0.3s ease;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
      text-transform: uppercase;
      font-weight: bold;
      letter-spacing: 1px;
      position: relative;
      overflow: hidden;
    }

    button::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
      transition: 0.5s;
    }

    button:hover::before {
      left: 100%;
    }

    button:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
      background: linear-gradient(45deg, #feca57, #ff6b9d);
    }

    button:active {
      transform: translateY(0);
    }

    button:disabled {
      background: #555;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }

    button:disabled:hover::before {
      left: -100%;
    }

    #spinBtn {
      background: linear-gradient(45deg, #27ae60, #2ecc71);
      font-size: 20px;
      padding: 18px 40px;
    }

    #spinBtn:hover {
      background: linear-gradient(45deg, #2ecc71, #27ae60);
    }

    #message {
      margin: 20px 0;
      font-size: 1.3em;
      font-weight: bold;
      text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
      min-height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .result-box {
      background: linear-gradient(135deg, rgba(39, 174, 96, 0.9), rgba(46, 204, 113, 0.9));
      padding: 20px;
      border-radius: 15px;
      margin: 20px 0;
      border: 2px solid rgba(255, 255, 255, 0.5);
      backdrop-filter: blur(10px);
      animation: fadeInUp 0.5s ease;
    }

    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(30px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .hidden {
      display: none;
    }

    .stats {
      display: flex;
      justify-content: space-around;
      margin: 20px 0;
      background: rgba(255, 255, 255, 0.1);
      padding: 15px;
      border-radius: 10px;
      flex-wrap: wrap;
    }

    .stat-item {
      display: flex;
      flex-direction: column;
      margin: 5px 10px;
    }

    .stat-value {
      font-size: 1.8em;
      font-weight: bold;
      color: #feca57;
    }

    .win-animation {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1000;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      background: #feca57;
      opacity: 0;
    }

    @keyframes confettiFall {
      0% {
        transform: translateY(-100px) rotate(0deg);
        opacity: 1;
      }
      100% {
        transform: translateY(1000px) rotate(360deg);
        opacity: 0;
      }
    }

    .win-text {
      font-size: 5em;
      font-weight: bold;
      color: #feca57;
      text-shadow: 0 0 20px rgba(254, 202, 87, 0.8);
      animation: textPulse 1s ease-in-out infinite;
    }

    @keyframes textPulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.1); }
    }

    .lock-body {
      width: 100%;
      max-width: 600px;
      height: 150px;
      background: linear-gradient(145deg, #8B4513, #A0522D);
      margin: 0 auto 20px;
      border-radius: 10px;
      position: relative;
      box-shadow: 0 10px 20px rgba(0,0,0,0.5);
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .lock-shackle {
      position: absolute;
      top: -60px;
      left: 50%;
      transform: translateX(-50%);
      width: 120px;
      height: 80px;
      border: 15px solid #D2691E;
      border-bottom: none;
      border-radius: 60px 60px 0 0;
      z-index: 1;
    }

    .difficulty-info {
      margin: 10px 0;
      font-size: 1.1em;
      color: #feca57;
    }

    .reward-info {
      margin: 5px 0;
      font-size: 1em;
      color: #ffd700;
      font-weight: bold;
    }

    .reward-animation {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 2000;
      background: rgba(0, 0, 0, 0.8);
      animation: fadeIn 0.5s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .reward-content {
      background: linear-gradient(135deg, #ff6b9d, #feca57);
      padding: 30px;
      border-radius: 20px;
      text-align: center;
      max-width: 500px;
      animation: scaleIn 0.5s ease;
    }

    @keyframes scaleIn {
      from { transform: scale(0.5); }
      to { transform: scale(1); }
    }

    .reward-icon {
      font-size: 5em;
      margin-bottom: 20px;
      animation: bounce 1s infinite;
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-20px); }
    }

    .reward-title {
      font-size: 2.5em;
      margin-bottom: 10px;
      color: white;
      text-shadow: 0 0 10px rgba(0,0,0,0.5);
    }

    .reward-description {
      font-size: 1.2em;
      margin-bottom: 20px;
      color: white;
    }

    .reward-close {
      padding: 10px 20px;
      background: #2ecc71;
      border: none;
      border-radius: 10px;
      color: white;
      font-size: 1.1em;
      cursor: pointer;
      transition: all 0.3s;
    }

    .reward-close:hover {
      background: #27ae60;
      transform: scale(1.05);
    }

    @media (max-width: 768px) {
      .game-container {
        padding: 20px;
        margin: 10px;
      }
      
      h1 {
        font-size: 2.2em;
      }
      
      .digit-wheel {
        width: 55px;
        height: 90px;
        font-size: 2.5em;
      }
      
      button {
        padding: 12px 25px;
        font-size: 16px;
      }
      
      #spinBtn {
        font-size: 18px;
        padding: 15px 30px;
      }

      .attack-mode-btn {
        padding: 8px 12px;
        font-size: 12px;
        min-width: 50px;
      }

      .difficulty-btn {
        padding: 10px 15px;
        font-size: 14px;
        min-width: 100px;
      }
    }

    @media (max-width: 480px) {
      .digit-wheel {
        width: 45px;
        height: 75px;
        font-size: 2em;
      }
      
      .lock-container {
        gap: 8px;
      }

      .attack-modes {
        gap: 5px;
      }

      .attack-mode-btn {
        padding: 6px 10px;
        font-size: 11px;
        min-width: 45px;
      }

      .difficulty-btn {
        padding: 8px 12px;
        font-size: 12px;
        min-width: 80px;
      }
    }
  </style>
</head>
<body>
  <div class="game-container">
    <h1>🎰 Jeu du Cadenas - Récompenses Spéciales</h1>
    
    <div class="difficulty-selector">
      <button id="difficulty4" class="difficulty-btn easy active">4 Chiffres (Facile)</button>
      <button id="difficulty5" class="difficulty-btn medium">5 Chiffres (Moyen)</button>
      <button id="difficulty6" class="difficulty-btn hard">6 Chiffres (Difficile)</button>
      <button id="difficulty7" class="difficulty-btn expert">7 Chiffres (Expert)</button>
    </div>

    <div class="difficulty-info" id="difficultyInfo">Objectif : Obtenir 7777 !</div>
    <div class="reward-info" id="rewardInfo">Récompense : 🐋 Une Baleine</div>
    
    <div class="lock-body">
      <div class="lock-shackle"></div>
      <div class="lock-container" id="lockContainer">
        <!-- Les roues de chiffres seront générées ici -->
      </div>
    </div>

    <div class="attack-modes">
      <button id="mode1" class="attack-mode-btn active">1 coup</button>
      <button id="mode5" class="attack-mode-btn">5 coups</button>
      <button id="mode10" class="attack-mode-btn">10 coups</button>
      <button id="mode30" class="attack-mode-btn">30 coups</button>
      <button id="mode100" class="attack-mode-btn">100 coups</button>
      <button id="mode1000" class="attack-mode-btn">1000 coups</button>
    </div>

    <div class="stats">
      <div class="stat-item">
        <div>Coups joués</div>
        <div class="stat-value" id="attemptsCount">0</div>
      </div>
      <div class="stat-item">
        <div>Meilleur score</div>
        <div class="stat-value" id="bestScore">0</div>
      </div>
      <div class="stat-item">
        <div>Difficulté</div>
        <div class="stat-value" id="currentDifficulty">4</div>
      </div>
    </div>

    <div class="controls">
      <button id="spinBtn">Tourner le cadenas</button>
      <button id="resetBtn">Nouvelle partie</button>
    </div>

    <div id="message">Prêt à jouer ? Choisissez une difficulté et cliquez sur "Tourner le cadenas" !</div>

    <div id="resultContainer" class="hidden result-box">
      <h3>🎉 Félicitations ! 🎉</h3>
      <p id="winMessage">Vous avez trouvé la combinaison gagnante !</p>
      <p id="attemptsResult">Nombre de tentatives : 0</p>
    </div>
  </div>

  <script>
    // Variables du jeu
    let digits = [];
    let attempts = 0;
    let bestScores = {
      4: localStorage.getItem('bestScore4') ? parseInt(localStorage.getItem('bestScore4')) : 0,
      5: localStorage.getItem('bestScore5') ? parseInt(localStorage.getItem('bestScore5')) : 0,
      6: localStorage.getItem('bestScore6') ? parseInt(localStorage.getItem('bestScore6')) : 0,
      7: localStorage.getItem('bestScore7') ? parseInt(localStorage.getItem('bestScore7')) : 0
    };
    let isSpinning = false;
    let winAnimationActive = false;
    let attackMode = 1;
    let audioContext = null;
    let currentDifficulty = 4;
    let targetCombination = "7777";

    // Récompenses par difficulté
    const rewards = {
      4: {
        icon: "🐋",
        title: "UNE BALEINE !",
        description: "Félicitations ! Vous avez gagné une magnifique baleine !"
      },
      5: {
        icon: "🌍",
        title: "LA PLANÈTE MERVEILLE !",
        description: "Incroyable ! Vous avez découvert la planète merveilleuse !"
      },
      6: {
        icon: "🌌",
        title: "L'UNIVERS !",
        description: "Extraordinaire ! Vous avez conquis l'univers tout entier !"
      },
      7: {
        icon: "💰",
        title: "100 000 PIÈCES !",
        description: "Fantastique ! Vous avez gagné 100 000 pièces d'or !"
      }
    };

    // Éléments DOM
    const lockContainer = document.getElementById('lockContainer');
    const spinBtn = document.getElementById('spinBtn');
    const resetBtn = document.getElementById('resetBtn');
    const message = document.getElementById('message');
    const resultContainer = document.getElementById('resultContainer');
    const attemptsCount = document.getElementById('attemptsCount');
    const bestScoreElement = document.getElementById('bestScore');
    const currentDifficultyElement = document.getElementById('currentDifficulty');
    const attemptsResult = document.getElementById('attemptsResult');
    const winMessage = document.getElementById('winMessage');
    const difficultyInfo = document.getElementById('difficultyInfo');
    const rewardInfo = document.getElementById('rewardInfo');

    // Système audio
    function initAudioContext() {
      try {
        if (!audioContext) {
          audioContext = new (window.AudioContext || window.webkitAudioContext)();
        }
        if (audioContext.state === 'suspended') {
          audioContext.resume();
        }
        return audioContext;
      } catch (e) {
        return null;
      }
    }

    function createSound(frequency, duration, type = 'sine', volume = 0.15) {
      const context = initAudioContext();
      if (!context) return;

      try {
        const oscillator = context.createOscillator();
        const gainNode = context.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(context.destination);
        
        oscillator.frequency.value = frequency;
        oscillator.type = type;
        
        gainNode.gain.setValueAtTime(volume, context.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, context.currentTime + duration);
        
        oscillator.start(context.currentTime);
        oscillator.stop(context.currentTime + duration);
      } catch (e) {
        // Silence en cas d'erreur
      }
    }

    function playSpinSound() {
      createSound(600, 0.1, 'square');
    }

    function playClickSound() {
      createSound(300, 0.05, 'square');
    }

    function playWinSound() {
      createSound(800, 0.3, 'sine');
      setTimeout(() => createSound(1000, 0.3, 'sine'), 300);
      setTimeout(() => createSound(1200, 0.5, 'sine'), 600);
    }

    function playLoseSound() {
      createSound(200, 0.5, 'sawtooth');
    }

    function playDifficultyChangeSound() {
      createSound(500, 0.2, 'sine');
    }

    function playRewardSound() {
      createSound(1000, 0.5, 'sine');
      setTimeout(() => createSound(1200, 0.5, 'sine'), 200);
      setTimeout(() => createSound(1400, 0.5, 'sine'), 400);
    }

    // Initialisation du jeu
    function initGame() {
      attempts = 0;
      digits = Array(currentDifficulty).fill(0);
      updateDisplay();
      attemptsCount.textContent = attempts;
      bestScoreElement.textContent = bestScores[currentDifficulty];
      currentDifficultyElement.textContent = currentDifficulty;
      resultContainer.classList.add('hidden');
      updateDifficultyInfo();
      message.textContent = `Prêt à jouer ? Objectif : ${targetCombination} !`;
      spinBtn.disabled = false;
      removeWinClasses();
      playClickSound();
    }

    // Mise à jour de l'affichage des chiffres
    function updateDisplay() {
      lockContainer.innerHTML = '';
      
      digits.forEach((digit, index) => {
        const digitElement = document.createElement('div');
        digitElement.className = 'digit-wheel';
        digitElement.id = `digit${index + 1}`;
        digitElement.textContent = digit;
        lockContainer.appendChild(digitElement);
      });
    }

    // Mise à jour des informations de difficulté
    function updateDifficultyInfo() {
      const targets = {
        4: "7777",
        5: "77777", 
        6: "777777",
        7: "7777777"
      };
      
      targetCombination = targets[currentDifficulty];
      difficultyInfo.textContent = `Objectif : Obtenir ${targetCombination} !`;
      rewardInfo.textContent = `Récompense : ${rewards[currentDifficulty].icon} ${rewards[currentDifficulty].title}`;
    }

    // Supprimer les classes de victoire
    function removeWinClasses() {
      document.querySelectorAll('.digit-wheel').forEach(digit => {
        digit.classList.remove('winning');
        digit.classList.remove('spinning');
      });
    }

    // Animation de rotation d'un chiffre
    function spinDigit(index) {
      return new Promise(resolve => {
        const digitElement = document.getElementById(`digit${index + 1}`);
        if (!digitElement) return resolve();
        
        digitElement.classList.add('spinning');
        
        let spins = 0;
        const maxSpins = 10 + Math.floor(Math.random() * 10);
        
        const spinInterval = setInterval(() => {
          digits[index] = Math.floor(Math.random() * 10);
          digitElement.textContent = digits[index];
          playSpinSound();
          spins++;
          
          if (spins >= maxSpins) {
            clearInterval(spinInterval);
            digitElement.classList.remove('spinning');
            setTimeout(resolve, 100);
          }
        }, 100);
      });
    }

    // Afficher la récompense
    function showReward() {
      const reward = rewards[currentDifficulty];
      const rewardAnimation = document.createElement('div');
      rewardAnimation.className = 'reward-animation';
      
      rewardAnimation.innerHTML = `
        <div class="reward-content">
          <div class="reward-icon">${reward.icon}</div>
          <div class="reward-title">${reward.title}</div>
          <div class="reward-description">${reward.description}</div>
          <button class="reward-close">Continuer</button>
        </div>
      `;
      
      document.body.appendChild(rewardAnimation);
      playRewardSound();
      
      // Fermer l'animation
      const closeButton = rewardAnimation.querySelector('.reward-close');
      closeButton.addEventListener('click', () => {
        document.body.removeChild(rewardAnimation);
      });
      
      // Fermer automatiquement après 5 secondes
      setTimeout(() => {
        if (document.body.contains(rewardAnimation)) {
          document.body.removeChild(rewardAnimation);
        }
      }, 5000);
    }

    // Tourner tous les chiffres
    async function spinAllDigits() {
      if (isSpinning) return;
      
      isSpinning = true;
      spinBtn.disabled = true;
      message.textContent = "Le cadenas tourne...";
      
      // Effectuer le nombre de coups sélectionné
      for (let coup = 0; coup < attackMode; coup++) {
        // Animation séquentielle des chiffres
        for (let i = 0; i < currentDifficulty; i++) {
          await spinDigit(i);
        }
        
        attempts++;
        attemptsCount.textContent = attempts;
        
        // Vérifier si c'est une victoire
        const currentCombination = digits.join('');
        if (currentCombination === targetCombination) {
          await winGame();
          break;
        } else if (coup < attackMode - 1) {
          // Pause entre les coups (sauf le dernier)
          await new Promise(resolve => setTimeout(resolve, 300));
        }
      }
      
      const currentCombination = digits.join('');
      if (currentCombination !== targetCombination) {
        message.textContent = `Combinaison: ${currentCombination} - Essayez encore !`;
        playLoseSound();
      }
      
      isSpinning = false;
      spinBtn.disabled = false;
    }

    // Gestion de la victoire
    async function winGame() {
      winAnimationActive = true;
      message.textContent = "🎉 FÉLICITATIONS ! Vous avez gagné ! 🎉";
      playWinSound();
      
      // Animation de victoire pour chaque chiffre
      for (let i = 0; i < currentDifficulty; i++) {
        setTimeout(() => {
          const digitElement = document.getElementById(`digit${i + 1}`);
          if (digitElement) digitElement.classList.add('winning');
        }, i * 200);
      }
      
      // Mise à jour du meilleur score
      if (bestScores[currentDifficulty] === 0 || attempts < bestScores[currentDifficulty]) {
        bestScores[currentDifficulty] = attempts;
        localStorage.setItem(`bestScore${currentDifficulty}`, bestScores[currentDifficulty]);
        bestScoreElement.textContent = bestScores[currentDifficulty];
      }
      
      // Affichage du résultat
      winMessage.textContent = `Vous avez trouvé la combinaison gagnante ${targetCombination} !`;
      attemptsResult.textContent = `Nombre de tentatives : ${attempts}`;
      await new Promise(resolve => setTimeout(resolve, 1500));
      resultContainer.classList.remove('hidden');
      
      // Afficher la récompense
      showReward();
      
      // Animation de confettis
      createConfetti();
      
      // Réinitialiser après un délai
      setTimeout(() => {
        winAnimationActive = false;
      }, 5000);
    }

    // Création d'animation de confettis
    function createConfetti() {
      const confettiContainer = document.createElement('div');
      confettiContainer.className = 'win-animation';
      document.body.appendChild(confettiContainer);
      
      // Créer des confettis
      for (let i = 0; i < 150; i++) {
        const confetti = document.createElement('div');
        confetti.className = 'confetti';
        confetti.style.left = Math.random() * 100 + 'vw';
        confetti.style.backgroundColor = getRandomColor();
        confetti.style.animation = `confettiFall ${2 + Math.random() * 3}s linear forwards`;
        confetti.style.animationDelay = Math.random() * 2 + 's';
        confettiContainer.appendChild(confetti);
      }
      
      // Texte de victoire
      const winText = document.createElement('div');
      winText.className = 'win-text';
      winText.textContent = `${targetCombination}!`;
      confettiContainer.appendChild(winText);
      
      // Supprimer l'animation après un délai
      setTimeout(() => {
        document.body.removeChild(confettiContainer);
      }, 5000);
    }

    // Générer une couleur aléatoire
    function getRandomColor() {
      const colors = ['#feca57', '#ff6b9d', '#48dbfb', '#1dd1a1', '#f368e0', '#ff9ff3'];
      return colors[Math.floor(Math.random() * colors.length)];
    }

    // Définir le mode d'attaque
    function setAttackMode(mode) {
      attackMode = mode;
      
      document.querySelectorAll('.attack-mode-btn').forEach(btn => {
        btn.classList.remove('active');
      });
      
      document.getElementById(`mode${mode}`).classList.add('active');
      
      spinBtn.textContent = `Tourner (${mode} coup${mode > 1 ? 's' : ''})`;
      playClickSound();
    }

    // Changer la difficulté
    function setDifficulty(difficulty) {
      currentDifficulty = difficulty;
      
      document.querySelectorAll('.difficulty-btn').forEach(btn => {
        btn.classList.remove('active');
      });
      
      document.getElementById(`difficulty${difficulty}`).classList.add('active');
      
      playDifficultyChangeSound();
      initGame();
    }

    // Événements
    spinBtn.addEventListener('click', spinAllDigits);
    resetBtn.addEventListener('click', initGame);

    document.getElementById("mode1").addEventListener("click", () => setAttackMode(1));
    document.getElementById("mode5").addEventListener("click", () => setAttackMode(5));
    document.getElementById("mode10").addEventListener("click", () => setAttackMode(10));
    document.getElementById("mode30").addEventListener("click", () => setAttackMode(30));
    document.getElementById("mode100").addEventListener("click", () => setAttackMode(100));
    document.getElementById("mode1000").addEventListener("click", () => setAttackMode(1000));

    document.getElementById("difficulty4").addEventListener("click", () => setDifficulty(4));
    document.getElementById("difficulty5").addEventListener("click", () => setDifficulty(5));
    document.getElementById("difficulty6").addEventListener("click", () => setDifficulty(6));
    document.getElementById("difficulty7").addEventListener("click", () => setDifficulty(7));

    // Raccourcis clavier
    document.addEventListener('keydown', (e) => {
      if (e.key === ' ' || e.key === 'Enter') {
        e.preventDefault();
        if (!isSpinning && !winAnimationActive) {
          spinAllDigits();
        }
      }
      
      if (e.key === 'r' || e.key === 'R') {
        initGame();
      }
      
      // Raccourcis numériques pour les modes
      if (e.key >= '1' && e.key <= '6') {
        const modes = [1, 5, 10, 30, 100, 1000];
        const index = parseInt(e.key) - 1;
        if (index < modes.length) {
          setAttackMode(modes[index]);
        }
      }
      
      // Raccourcis pour les difficultés (F1-F4)
      if (e.key === 'F1' || e.key === '1' && e.altKey) setDifficulty(4);
      if (e.key === 'F2' || e.key === '2' && e.altKey) setDifficulty(5);
      if (e.key === 'F3' || e.key === '3' && e.altKey) setDifficulty(6);
      if (e.key === 'F4' || e.key === '4' && e.altKey) setDifficulty(7);
    });

    // Initialisation au chargement
    window.addEventListener('load', initGame);
  </script>
</body>
</html>
