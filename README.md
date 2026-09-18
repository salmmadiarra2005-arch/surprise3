<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Joyeux Anniversaire Kaka Nini ! 🎁</title>
  
  <!-- Polices Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Great+Vibes&family=Montserrat:wght@400;500;600;700&family=Playfair+Display:ital,wght@0,600;1,400&display=swap" rel="stylesheet">
  
  <!-- Canvas-Confetti via CDN -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <style>
    :root {
      /* Thème 1 par défaut : Doré & Warm Beige */
      --bg-gradient: linear-gradient(135deg, #f5efe6 0%, #e8dad1 50%, #d4c3b3 100%);
      --env-bg: #e6cca0;
      --env-inner: #d1b280;
      --flap-bg: #deb887;
      --letter-bg: #fffcf7;
      --text-main: #3d2b1f;
      --accent-color: #c0392b;
      --accent-light: #e74c3c;
      --gold-detail: #d4af37;
      --shadow-color: rgba(61, 43, 31, 0.15);
      --font-heading: 'Great Vibes', cursive;
      --font-body: 'Playfair Display', serif;
    }

    /* Thème 2 : Lavande & Violet */
    [data-theme="lavender"] {
      --bg-gradient: linear-gradient(135deg, #f3e8ff 0%, #e9d5ff 50%, #d8b4fe 100%);
      --env-bg: #c084fc;
      --env-inner: #a855f7;
      --flap-bg: #d8b4fe;
      --letter-bg: #faf5ff;
      --text-main: #3b0764;
      --accent-color: #7e22ce;
      --accent-light: #a855f7;
      --gold-detail: #9333ea;
      --shadow-color: rgba(59, 7, 100, 0.15);
    }

    /* Thème 3 : Rose Poudré & Blush */
    [data-theme="rose"] {
      --bg-gradient: linear-gradient(135deg, #fff1f2 0%, #ffe4e6 50%, #fecdd3 100%);
      --env-bg: #f43f5e;
      --env-inner: #e11d48;
      --flap-bg: #fda4af;
      --letter-bg: #fff5f5;
      --text-main: #4c0519;
      --accent-color: #be123c;
      --accent-light: #fb7185;
      --gold-detail: #e11d48;
      --shadow-color: rgba(76, 5, 25, 0.15);
    }

    /* Thème 4 : Vert Sauge */
    [data-theme="sage"] {
      --bg-gradient: linear-gradient(135deg, #f0fdf4 0%, #dcfce7 50%, #bbf7d0 100%);
      --env-bg: #4ade80;
      --env-inner: #22c55e;
      --flap-bg: #86efac;
      --letter-bg: #f6fbf7;
      --text-main: #052e16;
      --accent-color: #15803d;
      --accent-light: #4ade80;
      --gold-detail: #16a34a;
      --shadow-color: rgba(5, 46, 22, 0.15);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background: var(--bg-gradient);
      font-family: var(--font-body);
      color: var(--text-main);
      overflow-x: hidden;
      transition: background 0.5s ease;
      position: relative;
    }

    /* Header & Theme Switcher */
    header {
      position: fixed;
      top: 20px;
      display: flex;
      gap: 12px;
      background: rgba(255, 255, 255, 0.4);
      backdrop-filter: blur(10px);
      padding: 8px 16px;
      border-radius: 30px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.05);
      z-index: 10;
    }

    .theme-dot {
      width: 22px;
      height: 22px;
      border-radius: 50%;
      cursor: pointer;
      border: 2px solid #fff;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .theme-dot:hover {
      transform: scale(1.2);
    }

    .dot-gold { background: linear-gradient(45deg, #e6cca0, #c0392b); }
    .dot-lavender { background: linear-gradient(45deg, #c084fc, #7e22ce); }
    .dot-rose { background: linear-gradient(45deg, #f43f5e, #be123c); }
    .dot-sage { background: linear-gradient(45deg, #4ade80, #15803d); }

    .instruction {
      margin-bottom: 25px;
      font-family: 'Montserrat', sans-serif;
      font-size: 0.95rem;
      text-transform: uppercase;
      letter-spacing: 2px;
      color: var(--text-main);
      opacity: 0.8;
      animation: pulse 2s infinite;
      text-align: center;
      padding: 0 15px;
    }

    @keyframes pulse {
      0%, 100% { opacity: 0.5; transform: translateY(0); }
      50% { opacity: 1; transform: translateY(-3px); }
    }

    /* Scène 3D & Enveloppe */
    .scene {
      width: 320px;
      height: 220px;
      perspective: 1000px;
      cursor: pointer;
      position: relative;
    }

    @media (min-width: 480px) {
      .scene {
        width: 420px;
        height: 280px;
      }
    }

    .envelope {
      width: 100%;
      height: 100%;
      position: relative;
      transform-style: preserve-3d;
      transition: transform 0.6s ease;
    }

    /* Parties de l'enveloppe */
    .env-back {
      position: absolute;
      width: 100%;
      height: 100%;
      background: var(--env-inner);
      border-radius: 8px;
      box-shadow: 0 15px 35px var(--shadow-color);
    }

    /* La Lettre */
    .letter {
      position: absolute;
      bottom: 5px;
      left: 5%;
      width: 90%;
      height: 90%;
      background: var(--letter-bg);
      border-radius: 6px;
      padding: 20px 25px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.08);
      transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1), z-index 0.8s;
      z-index: 2;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border: 1px solid rgba(0,0,0,0.05);
    }

    .letter-preview {
      text-align: center;
    }

    .letter-preview h2 {
      font-family: var(--font-heading);
      font-size: 2rem;
      color: var(--accent-color);
      margin-bottom: 5px;
    }

    .letter-preview p {
      font-size: 0.85rem;
      line-height: 1.4;
      color: var(--text-main);
      display: -webkit-box;
      -webkit-line-clamp: 4;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }

    .letter-date {
      font-family: 'Montserrat', sans-serif;
      font-size: 0.75rem;
      font-weight: 600;
      color: var(--gold-detail);
      text-transform: uppercase;
      letter-spacing: 1px;
      text-align: right;
    }

    /* Rabats de l'enveloppe */
    .env-flaps {
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 3;
    }

    .flap-left {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-top: 110px solid transparent;
      border-bottom: 110px solid transparent;
      border-left: 175px solid var(--env-bg);
      border-radius: 8px 0 0 8px;
    }

    .flap-right {
      position: absolute;
      top: 0;
      right: 0;
      width: 0;
      height: 0;
      border-top: 110px solid transparent;
      border-bottom: 110px solid transparent;
      border-right: 175px solid var(--env-bg);
      border-radius: 0 8px 8px 0;
    }

    .flap-bottom {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid transparent;
      border-right: 160px solid transparent;
      border-bottom: 130px solid var(--env-bg);
      border-radius: 0 0 8px 8px;
    }

    @media (min-width: 480px) {
      .flap-left { border-top-width: 140px; border-bottom-width: 140px; border-left-width: 230px; }
      .flap-right { border-top-width: 140px; border-bottom-width: 140px; border-right-width: 230px; }
      .flap-bottom { border-left-width: 210px; border-right-width: 210px; border-bottom-width: 160px; }
    }

    .flap-top {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid transparent;
      border-right: 160px solid transparent;
      border-top: 130px solid var(--flap-bg);
      transform-origin: top center;
      transition: transform 0.6s ease, z-index 0.6s;
      z-index: 4;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.1));
    }

    @media (min-width: 480px) {
      .flap-top { border-left-width: 210px; border-right-width: 210px; border-top-width: 160px; }
    }

    /* Sceau de cire */
    .wax-seal {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 48px;
      height: 48px;
      background: radial-gradient(circle, var(--accent-light) 0%, var(--accent-color) 100%);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      font-size: 20px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.25);
      z-index: 5;
      transition: opacity 0.4s, transform 0.4s;
    }

    /* Animation quand l'enveloppe est ouverte */
    .open .flap-top {
      transform: rotateX(180deg);
      z-index: 1;
    }

    .open .wax-seal {
      opacity: 0;
      transform: translate(-50%, -50%) scale(0.5);
    }

    .open .letter {
      transform: translateY(-110px);
      z-index: 5;
    }

    @media (min-width: 480px) {
      .open .letter {
        transform: translateY(-140px);
      }
    }

    /* Bouton sous l'enveloppe */
    .controls {
      margin-top: 40px;
      display: flex;
      justify-content: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.5s ease 0.6s;
    }

    .show-controls .controls {
      opacity: 1;
      pointer-events: auto;
    }

    .btn {
      padding: 12px 28px;
      border: none;
      border-radius: 25px;
      font-family: 'Montserrat', sans-serif;
      font-size: 0.9rem;
      font-weight: 600;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.08);
      transition: all 0.2s;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .btn-primary {
      background: var(--accent-color);
      color: #fff;
    }

    .btn-primary:hover {
      background: var(--accent-light);
      transform: translateY(-2px);
      box-shadow: 0 6px 18px rgba(0,0,0,0.12);
    }

    /* Modal Plein Écran */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(0, 0, 0, 0.4);
      backdrop-filter: blur(8px);
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.4s ease;
      z-index: 100;
      padding: 20px;
    }

    .modal-overlay.active {
      opacity: 1;
      pointer-events: auto;
    }

    .modal-card {
      background: var(--letter-bg);
      width: 100%;
      max-width: 550px;
      max-height: 80vh;
      border-radius: 12px;
      padding: 35px 30px;
      box-shadow: 0 20px 50px rgba(0,0,0,0.2);
      overflow-y: auto;
      scroll-behavior: smooth;
      position: relative;
      transform: translateY(20px) scale(0.95);
      transition: transform 0.4s ease;
      border: 1px solid rgba(0,0,0,0.05);
      -webkit-overflow-scrolling: touch;
    }

    .modal-overlay.active .modal-card {
      transform: translateY(0) scale(1);
    }

    .close-modal {
      position: fixed;
      top: 20px;
      right: 25px;
      background: rgba(255, 255, 255, 0.8);
      border: none;
      font-size: 28px;
      color: var(--text-main);
      cursor: pointer;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      z-index: 110;
      transition: transform 0.2s;
    }

    .close-modal:hover {
      transform: scale(1.1);
    }

    .modal-body {
      text-align: center;
    }

    .modal-body h2 {
      font-family: var(--font-heading);
      font-size: 3rem;
      color: var(--accent-color);
      margin-bottom: 10px;
    }

    .modal-body .subtitle {
      font-family: 'Dancing Script', cursive;
      font-size: 1.4rem;
      color: var(--gold-detail);
      margin-bottom: 25px;
    }

    .modal-body p {
      font-size: 1.05rem;
      line-height: 1.8;
      color: var(--text-main);
      margin-bottom: 20px;
      text-align: justify;
      white-space: pre-line;
    }

    .signature {
      margin-top: 30px;
      text-align: right;
      font-family: var(--font-heading);
      font-size: 2rem;
      color: var(--accent-color);
    }

    /* Bouton pour remonter en haut */
    .scroll-top-btn {
      display: block;
      margin: 25px auto 0 auto;
      padding: 8px 18px;
      background: transparent;
      border: 1px solid var(--accent-color);
      color: var(--accent-color);
      border-radius: 20px;
      font-family: 'Montserrat', sans-serif;
      font-size: 0.8rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
    }

    .scroll-top-btn:hover {
      background: var(--accent-color);
      color: #fff;
    }
  </style>
</head>
<body>

  <!-- Sélecteur de Thème -->
  <header>
    <div class="theme-dot dot-gold" onclick="setTheme('')" title="Thème Doré"></div>
    <div class="theme-dot dot-lavender" onclick="setTheme('lavender')" title="Thème Lavande"></div>
    <div class="theme-dot dot-rose" onclick="setTheme('rose')" title="Thème Rose Poudré"></div>
    <div class="theme-dot dot-sage" onclick="setTheme('sage')" title="Thème Vert Sauge"></div>
  </header>

  <div class="instruction" id="instruction">Ouvre mon cœur 💌</div>

  <!-- Scène 3D Enveloppe -->
  <div class="scene" id="scene" onclick="toggleEnvelope()">
    <div class="envelope" id="envelope">
      <div class="env-back"></div>
      
      <!-- La Lettre -->
      <div class="letter">
        <div class="letter-date">29 Septembre</div>
        <div class="letter-preview">
          <h2>Joyeux Anniversaire !</h2>
          <p>À mon précieux Kaka Nini, qu'en ce 29 septembre ton cœur soit rempli de bonheur...</p>
        </div>
        <div style="text-align: center; font-size: 0.75rem; opacity: 0.6; font-family: 'Montserrat', sans-serif;">
          Clique pour agrandir
        </div>
      </div>

      <!-- Rabats -->
      <div class="env-flaps">
        <div class="flap-left"></div>
        <div class="flap-right"></div>
        <div class="flap-bottom"></div>
        <div class="flap-top"></div>
      </div>

      <!-- Sceau de cire -->
      <div class="wax-seal">❤️</div>
    </div>
  </div>

  <!-- Bouton sous l'enveloppe -->
  <div class="controls" id="controls">
    <button class="btn btn-primary" onclick="openModal()">
      <span>📖</span> Lire en grand
    </button>
  </div>

  <!-- Modal Affichage Plein Écran -->
  <div class="modal-overlay" id="modalOverlay" onclick="closeModalOnOverlay(event)">
    <button class="close-modal" onclick="closeModal()">&times;</button>
    <div class="modal-card" id="modalCard">
      <div class="modal-body">
        <h2>Joyeux Anniversaire !</h2>
        <div class="subtitle">Joyeux anniversaire mon Kaka Nini ❤️</div>
        <p>
          Mon chéri,

          En ce jour si spécial du 29 septembre, je tiens à te rappeler à quel point tu comptes pour moi. 
          
          Merci d'apporter tant de lumière, de rires et de douceur dans ma vie au quotidien. Tu es une personne formidable et je suis tellement chanceuse de t'avoir à mes côtés.

          Que cette nouvelle année t'apporte tout le bonheur, la santé, la réussite et l'amour que tu mérites amplement.

          Je t'aime très fort ! 🎉🎂✨
        </p>
        <div class="signature">Ta Salmma ❤️</div>
        
        <!-- Bouton pour remonter en haut -->
        <button class="scroll-top-btn" onclick="scrollToTop()">⬆️ Remonter en haut</button>
      </div>
    </div>
  </div>

  <script>
    let isOpen = false;

    // Changement de thème
    function setTheme(theme) {
      if (theme) {
        document.documentElement.setAttribute('data-theme', theme);
      } else {
        document.documentElement.removeAttribute('data-theme');
      }
    }

    // Ouvrir / Fermer l'enveloppe
    function toggleEnvelope() {
      const scene = document.getElementById('scene');
      const envelope = document.getElementById('envelope');
      const instruction = document.getElementById('instruction');

      isOpen = !isOpen;

      if (isOpen) {
        envelope.classList.add('open');
        scene.classList.add('show-controls');
        document.body.classList.add('show-controls');
        instruction.textContent = "Clique sur la lettre ou le bouton ci-dessous pour lire 📜";
        
        // Lancer les confettis
        launchConfetti();
      } else {
        envelope.classList.remove('open');
        document.body.classList.remove('show-controls');
        instruction.textContent = "Ouvre mon cœur 💌";
      }
    }

    // Lancement de confettis
    function launchConfetti() {
      if (typeof confetti === 'function') {
        confetti({
          particleCount: 70,
          spread: 60,
          origin: { y: 0.7 },
          colors: ['#f43f5e', '#e6cca0', '#7e22ce', '#ffffff']
        });
      }
    }

    // Modal
    function openModal() {
      document.getElementById('modalOverlay').classList.add('active');
      document.getElementById('modalCard').scrollTop = 0;
    }

    function closeModal() {
      document.getElementById('modalOverlay').classList.remove('active');
    }

    function closeModalOnOverlay(e) {
      if (e.target.id === 'modalOverlay') {
        closeModal();
      }
    }

    // Fonction pour remonter tout en haut de la carte
    function scrollToTop() {
      document.getElementById('modalCard').scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    }
  </script>
</body>
</html>
