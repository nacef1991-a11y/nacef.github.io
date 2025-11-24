# nacef.github.io
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    
    <!-- Méta-données PWA pour l'installation sur mobile -->
    <meta name="theme-color" content="#3b82f6">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="default">
    <meta name="apple-mobile-web-app-title" content="Masterclass AAG">
    <meta name="description" content="Formation interactive sur la prise en charge de l'Asthme Aigu Grave.">

    <!-- Icône Favicon (SVG encodé pour être autonome) -->
    <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🫁</text></svg>">
    
    <!-- Manifeste PWA intégré via Data URI -->
    <link rel="manifest" href="data:application/manifest+json;base64,ewogICJuYW1lIjogIk1hc3RlcmNsYXNzIEFzdGhtZSBBaWd1IEdyYXZlIiwKICAic2hvcnRfbmFtZSI6ICJNQSBhZ3IiLAogICJzdGFydF91cmwiOiAiLiIsCiAgImRpc3BsYXkiOiAic3RhbmRhbG9uZSIsCiAgImJhY2tncm91bmRfY29sb3IiOiAiI2YxZjVmOSIsCiAgInRoZW1lX2NvbG9yIjogIiMzYjgyZjYiLAogICJvcmllbnRhdGlvbiI6ICJwb3J0cmFpdCIsCiAgImljb25zIjogWwogICAgewogICAgICAic3JjIjogImRhdGE6aW1hZ2Uvc3ZnK3htbDtiYXNlNjQsaVZCT1J3MEtHZ29BQUFBTlNVaEVVZ0FBQU1nQUFBRElDQVlBQUFDdGNFSlVBQUFBQ1hCSVdYTUFBQXNUQUFDTHdBR3lscHdBQUFDWlSURVVOQ1F6... (shortened for brevity, browser will handle auto-icon) ...Il0KfQ==">

    <title>Masterclass : Asthme Aigu Grave</title>
    
    <!-- Import de la police Inter pour un look moderne et lisible -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    
    <style>
        :root {
            /* Palette de couleurs médicales modernes */
            --primary: #3b82f6; 
            --primary-dark: #2563eb;
            --primary-light: #eff6ff;
            --secondary: #64748b;
            --success: #10b981;
            --success-bg: #ecfdf5;
            --success-text: #047857;
            --error: #ef4444;
            --error-bg: #fef2f2;
            --error-text: #b91c1c;
            --surface: #ffffff;
            --background: #f8fafc;
            --text-main: #0f172a;
            --radius: 20px;
            --shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
            --shadow-sm: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background-color: var(--background);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: flex-start; /* Better for scrolling on mobile */
        }

        /* Conteneur principal "App Shell" */
        .app-container {
            width: 100%;
            max-width: 550px; /* Format mobile idéal */
            min-height: 100vh;
            background: var(--surface);
            position: relative;
            display: flex;
            flex-direction: column;
            box-shadow: none;
            overflow-x: hidden;
        }

        @media (min-width: 600px) {
            body {
                padding: 20px;
                align-items: center;
                background: linear-gradient(135deg, #e0f2fe 0%, #f1f5f9 100%);
            }
            .app-container {
                min-height: 85vh;
                height: 85vh;
                max-height: 900px;
                border-radius: var(--radius);
                box-shadow: var(--shadow);
                overflow-y: hidden; /* Scroll interne */
                border: 1px solid rgba(255,255,255,0.5);
            }
        }

        /* Gestion du scroll interne pour les écrans desktop/tablette */
        .scrollable-content {
            flex: 1;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            padding: 24px;
            display: flex;
            flex-direction: column;
        }

        /* --- Transitions entre les vues --- */
        .screen {
            flex: 1;
            display: flex;
            flex-direction: column;
            opacity: 0;
            transform: translateX(20px);
            transition: opacity 0.3s ease, transform 0.3s ease;
            display: none; /* Caché par défaut */
            height: 100%;
        }

        .screen.active {
            display: flex;
            opacity: 1;
            transform: translateX(0);
        }

        /* --- Écran d'accueil --- */
        .welcome-hero {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px 0;
        }

        .logo-container {
            width: 120px;
            height: 120px;
            background: var(--primary-light);
            border-radius: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            margin-bottom: 30px;
            box-shadow: var(--shadow-sm);
            transform: rotate(-5deg);
        }

        .app-title {
            font-size: 2rem;
            font-weight: 800;
            color: var(--text-main);
            margin: 0 0 10px 0;
            letter-spacing: -0.03em;
            line-height: 1.1;
        }

        .app-subtitle {
            font-size: 1.1rem;
            color: var(--secondary);
            margin-bottom: 40px;
            line-height: 1.5;
            padding: 0 20px;
        }

        .feature-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
            width: 100%;
            margin-bottom: 20px;
        }

        .feature-item {
            background: var(--background);
            padding: 16px;
            border-radius: 16px;
            display: flex;
            align-items: center;
            font-weight: 500;
            color: var(--text-main);
            border: 1px solid #e2e8f0;
        }

        .feature-icon {
            font-size: 1.5rem;
            margin-right: 15px;
            width: 32px;
            text-align: center;
        }

        /* --- Header du Quiz --- */
        .quiz-header {
            margin-bottom: 24px;
            position: sticky;
            top: 0;
            background: var(--surface);
            z-index: 10;
            padding-bottom: 10px;
        }

        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        .badge-theme {
            background: var(--primary-light);
            color: var(--primary);
            padding: 6px 12px;
            border-radius: 99px;
            font-size: 0.8rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .progress-indicator {
            font-family: monospace; /* Look technique */
            font-weight: 700;
            color: var(--secondary);
            font-size: 1rem;
        }

        .progress-bar-bg {
            width: 100%;
            height: 8px;
            background: #e2e8f0;
            border-radius: 99px;
            overflow: hidden;
        }

        .progress-bar-fill {
            height: 100%;
            background: var(--primary);
            border-radius: 99px;
            width: 0%;
            transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }

        /* --- Carte Question --- */
        .question-text {
            font-size: 1.35rem;
            font-weight: 700;
            line-height: 1.4;
            margin-bottom: 30px;
            color: var(--text-main);
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 14px;
            padding-bottom: 20px; /* Espace pour le scroll */
        }

        .option-card {
            background: var(--surface);
            border: 2px solid #e2e8f0;
            padding: 20px;
            border-radius: 16px;
            text-align: left;
            font-size: 1rem;
            font-family: inherit;
            color: var(--text-main);
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            outline: none;
            font-weight: 500;
            display: flex;
            align-items: flex-start;
        }

        .option-card:hover:not(:disabled) {
            border-color: var(--primary);
            background: var(--primary-light);
            transform: translateY(-2px);
        }

        .option-letter {
            flex-shrink: 0;
            width: 28px;
            height: 28px;
            background: #e2e8f0;
            color: var(--secondary);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.85rem;
            font-weight: 700;
            margin-right: 16px;
            margin-top: 2px;
            transition: all 0.2s;
        }

        /* États de réponse */
        .option-card.correct {
            background: var(--success-bg);
            border-color: var(--success);
            color: var(--success-text);
        }
        .option-card.correct .option-letter {
            background: var(--success);
            color: white;
        }

        .option-card.incorrect {
            background: var(--error-bg);
            border-color: var(--error);
            color: var(--error-text);
        }
        .option-card.incorrect .option-letter {
            background: var(--error);
            color: white;
        }

        .option-card:disabled {
            cursor: default;
            transform: none !important;
        }
        /* Opacité réduite pour les non-sélectionnées lors de la révélation */
        .option-card:disabled:not(.correct):not(.incorrect) {
            opacity: 0.6;
            border-color: #f1f5f9;
        }

        /* --- Zone de Feedback et Indices --- */
        .interaction-area {
            margin-top: 20px;
        }

        .hint-btn {
            background: transparent;
            border: none;
            color: var(--primary);
            font-weight: 600;
            font-size: 0.95rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 10px 0;
            transition: opacity 0.2s;
        }
        
        .hint-btn:hover { opacity: 0.8; }

        .hint-card {
            margin-top: 10px;
            padding: 16px;
            background: #fffbeb;
            border-radius: 12px;
            color: #b45309;
            font-size: 0.95rem;
            display: none;
            border-left: 4px solid #f59e0b;
            line-height: 1.5;
            animation: fadeIn 0.3s ease;
        }

        .feedback-card {
            margin-top: 20px;
            padding: 20px;
            border-radius: 16px;
            background: var(--background);
            display: none;
            animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            border: 1px solid #e2e8f0;
        }

        .feedback-header {
            font-weight: 800;
            font-size: 1.1rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .feedback-body {
            color: var(--secondary);
            line-height: 1.6;
            font-size: 0.95rem;
        }

        /* --- Footer Actions --- */
        .footer-fixed {
            padding: 24px;
            background: var(--surface);
            border-top: 1px solid #f1f5f9;
            width: 100%;
            /* Sticky footer effect inside the container */
            margin-top: auto; 
        }

        .btn-main {
            width: 100%;
            background: var(--primary);
            color: white;
            border: none;
            padding: 18px;
            border-radius: 16px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
            -webkit-appearance: none; /* iOS fix */
        }

        .btn-main:hover {
            background: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(59, 130, 246, 0.4);
        }

        .btn-main:active {
            transform: scale(0.98);
        }
        
        .btn-outline {
            width: 100%;
            background: transparent;
            color: var(--secondary);
            border: 2px solid #e2e8f0;
            padding: 16px;
            border-radius: 16px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            margin-top: 12px;
        }

        /* --- Résultats et Rapport --- */
        .results-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
            padding: 20px 0;
        }

        .score-display {
            position: relative;
            width: 140px;
            height: 140px;
            margin-bottom: 20px;
        }
        
        .score-svg {
            transform: rotate(-90deg);
            width: 100%;
            height: 100%;
        }

        .score-value {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--text-main);
        }

        .result-title {
            font-size: 1.5rem;
            font-weight: 800;
            margin-bottom: 5px;
            color: var(--text-main);
            text-align: center;
        }

        .result-desc {
            color: var(--secondary);
            text-align: center;
            margin-bottom: 30px;
            line-height: 1.5;
            padding: 0 20px;
        }
        
        /* Styles du Rapport */
        .report-container {
            width: 100%;
            text-align: left;
            animation: slideUp 0.5s ease 0.2s backwards;
        }

        .report-card {
            background: var(--surface);
            border: 1px solid #e2e8f0;
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 16px;
            box-shadow: var(--shadow-sm);
        }

        .report-title {
            font-weight: 700;
            color: var(--text-main);
            margin-bottom: 15px;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .success-tags-container {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }

        .success-tag {
            background: var(--success-bg);
            color: var(--success-text);
            padding: 6px 12px;
            border-radius: 8px;
            font-size: 0.85rem;
            font-weight: 600;
            border: 1px solid rgba(16, 185, 129, 0.2);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .summary-section h4 {
            color: var(--primary);
            margin: 15px 0 8px 0;
            font-size: 0.95rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }
        
        .summary-section h4:first-child { margin-top: 0; }

        .summary-section ul {
            padding-left: 0;
            list-style-type: none;
            margin: 0;
        }

        .summary-section li {
            margin-bottom: 8px;
            color: var(--secondary);
            font-size: 0.9rem;
            line-height: 1.5;
            padding-left: 15px;
            position: relative;
        }
        
        .summary-section li::before {
            content: "•";
            color: var(--primary);
            font-weight: bold;
            position: absolute;
            left: 0;
        }

        .disclaimer {
            font-size: 0.75rem;
            color: #94a3b8;
            text-align: center;
            margin-top: 20px;
            padding: 0 20px;
            line-height: 1.4;
        }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

    </style>
</head>
<body>

<div class="app-container">
    
    <!-- Screen 1: Accueil -->
    <div id="screen-welcome" class="screen active">
        <div class="scrollable-content welcome-hero">
            <div class="logo-container">🫁</div>
            <h1 class="app-title">Masterclass<br>Asthme Aigu</h1>
            <p class="app-subtitle">Simulateur clinique interactif pour les urgences et la réanimation.</p>
            
            <div class="feature-grid">
                <div class="feature-item">
                    <span class="feature-icon">⏱️</span> 
                    <span>Mode sans limite de temps</span>
                </div>
                <div class="feature-item">
                    <span class="feature-icon">🩺</span> 
                    <span>20 cas cliniques réels</span>
                </div>
                <div class="feature-item">
                    <span class="feature-icon">🎓</span> 
                    <span>Rationnels détaillés</span>
                </div>
            </div>
            
            <p class="disclaimer">
                ⚠️ <strong>Avertissement :</strong> Cet outil est destiné à l'enseignement médical. Il ne remplace pas les recommandations officielles ni le jugement clinique face à un patient réel.
            </p>
        </div>
        
        <div class="footer-fixed">
            <button class="btn-main" onclick="app.startQuiz()">
                Commencer le Cas
                <svg width="24" height="24" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
                </svg>
            </button>
        </div>
    </div>

    <!-- Screen 2: Quiz -->
    <div id="screen-quiz" class="screen">
        <div class="scrollable-content">
            <div class="quiz-header">
                <div class="header-top">
                    <span class="badge-theme">Cas Clinique</span>
                    <span class="progress-indicator" id="progress-text">1/20</span>
                </div>
                <div class="progress-bar-bg">
                    <div id="progress-fill" class="progress-bar-fill"></div>
                </div>
            </div>

            <h2 id="question-text" class="question-text">...</h2>
            
            <div id="options-list" class="options-container">
                <!-- Options injectées par JS -->
            </div>

            <div class="interaction-area">
                <button id="hint-btn" class="hint-btn" onclick="app.toggleHint()">
                    <span>💡 Indice</span>
                </button>
                <div id="hint-content" class="hint-card"></div>

                <div id="feedback-area" class="feedback-card">
                    <div class="feedback-header" id="feedback-header"></div>
                    <div class="feedback-body" id="feedback-text"></div>
                </div>
            </div>
        </div>

        <div class="footer-fixed">
            <button id="next-btn" class="btn-main" onclick="app.nextQuestion()" style="display: none;">
                Suivant
                <svg width="24" height="24" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
            </button>
        </div>
    </div>

    <!-- Screen 3: Résultats -->
    <div id="screen-results" class="screen">
        <div class="scrollable-content results-container">
            
            <!-- Score Circle -->
            <div class="score-display">
                <svg class="score-svg" viewBox="0 0 100 100">
                    <circle cx="50" cy="50" r="45" fill="none" stroke="#e2e8f0" stroke-width="8" />
                    <circle id="score-circle-fill" cx="50" cy="50" r="45" fill="none" stroke="var(--primary)" stroke-width="8" stroke-dasharray="283" stroke-dashoffset="283" stroke-linecap="round" transition="stroke-dashoffset 1s ease" />
                </svg>
                <div class="score-value" id="final-score">0</div>
            </div>

            <h2 id="final-title" class="result-title">Analyse terminée</h2>
            <p id="final-msg" class="result-desc">Calcul de la performance...</p>
            
            <!-- Rapport détaillé injecté ici -->
            <div id="final-report" class="report-container"></div>

        </div>
        <div class="footer-fixed">
            <button class="btn-main" onclick="app.restart()">
                Recommencer
                <svg width="24" height="24" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                </svg>
            </button>
            <button class="btn-outline" onclick="window.print()">Imprimer la fiche</button>
        </div>
    </div>

</div>

<script>
    // --- Données du Cas Clinique ---
    // Ajout du champ 'concept' pour le rapport
    const quizData = [
        {
            concept: "Gravité Clinique Extrême",
            question: "Julie, 24 ans, arrive aux urgences. Dyspnée, mots hachés. Auscultation : très peu de sibilants, murmure vésiculaire quasi aboli. Quelle est la signification du 'silence auscultatoire' ?",
            options: [
                { text: "La crise commence à céder, le bronchospasme diminue.", correct: false },
                { text: "Obstruction extrême : le débit d'air est insuffisant pour générer du bruit.", correct: true },
                { text: "Il s'agit probablement d'un pneumothorax bilatéral d'emblée.", correct: false },
                { text: "C'est un signe d'atteinte parenchymateuse (pneumonie) associée.", correct: false }
            ],
            rationale: "Le silence auscultatoire est un signe de gravité extrême (pré-arrêt respiratoire). Le flux aérien est si faible qu'il ne fait même plus vibrer les voies aériennes.",
            hint: "Pour entendre un sifflement, il faut de l'air qui passe dans un tuyau. Pas d'air = Pas de bruit."
        },
        {
            concept: "Signes de Faillite Musculaire",
            question: "Quel signe clinique témoigne spécifiquement de la fatigue des muscles respiratoires (épuisement de la pompe) ?",
            options: [
                { text: "Le tirage sus-sternal.", correct: false },
                { text: "La respiration abdominale paradoxale (balancement thoraco-abdominal).", correct: true },
                { text: "La fréquence respiratoire à 30/min.", correct: false },
                { text: "L'expiration active.", correct: false }
            ],
            rationale: "La respiration paradoxale signe la faillite du diaphragme. Fatigué, il est aspiré vers le haut (le ventre rentre) lors de l'inspiration au lieu de descendre.",
            hint: "Regardez le ventre et le thorax : en temps normal, ils se gonflent ensemble."
        },
        {
            concept: "Gazométrie & Gravité",
            question: "Gazométrie : pH 7.35, PaCO2 42 mmHg, PaO2 60 mmHg. Pourquoi cette 'normocapnie' (42 mmHg) est-elle alarmante ?",
            options: [
                { text: "Car elle masque une alcalose métabolique.", correct: false },
                { text: "Un patient hyperventilant à 35/min devrait être hypocapnique (PaCO2 < 35).", correct: true },
                { text: "Elle indique que l'échangeur pulmonaire fonctionne bien.", correct: false },
                { text: "Elle signe un effet shunt intrapulmonaire majeur.", correct: false }
            ],
            rationale: "C'est l'effet 'pseudo-normal'. Si la PaCO2 remonte alors que le patient respire vite, c'est que l'espace mort augmente et que la ventilation alvéolaire s'effondre.",
            hint: "La PaCO2 est inversement proportionnelle à la ventilation alvéolaire. Elle devrait être basse."
        },
        {
            concept: "Cible SpO2",
            question: "Concernant l'oxygénothérapie initiale, quel est votre objectif de SpO2 chez cette patiente ?",
            options: [
                { text: "100% impérativement.", correct: false },
                { text: "Entre 93% et 95%.", correct: true },
                { text: "88-92% comme pour un BPCO.", correct: false },
                { text: "Peu importe tant que la cyanose disparaît.", correct: false }
            ],
            rationale: "C'est la cible recommandée (BTS/GINA) pour assurer une oxygénation suffisante sans risquer l'hyperoxie délétère (effet Haldane, atélectasies de dénitrogénation).",
            hint: "Le mieux est l'ennemi du bien. Viser 100% peut aggraver les échanges gazeux."
        },
        {
            concept: "Délai d'action Corticoïdes",
            question: "Vous débutez Corticoïdes systémiques. Quel est le délai d'action attendu pour l'effet anti-inflammatoire ?",
            options: [
                { text: "Immédiat.", correct: false },
                { text: "Environ 4 à 6 heures.", correct: true },
                { text: "24 heures minimum.", correct: false },
                { text: "1 heure si administrés en IV.", correct: false }
            ],
            rationale: "L'action génomique des corticoïdes prend plusieurs heures. C'est pourquoi on les donne le plus tôt possible aux urgences, en parallèle des bronchodilatateurs.",
            hint: "C'est un traitement de fond de la crise, pas un traitement minute comme la Ventoline."
        },
        {
            concept: "Indication Magnésium IV",
            question: "L'état stagne. Vous envisagez le Sulfate de Magnésium (MgSO4) IV. Quelle est son indication principale ?",
            options: [
                { text: "Corriger une hypomagnésémie.", correct: false },
                { text: "Agir comme bronchodilatateur musculaire lisse.", correct: true },
                { text: "Sédater la patiente pour la calmer.", correct: false },
                { text: "Améliorer la contractilité diaphragmatique.", correct: false }
            ],
            rationale: "Le magnésium bloque l'entrée du calcium dans les cellules musculaires lisses bronchiques, favorisant leur relaxation directe.",
            hint: "Considérez-le comme un 'super-bronchodilatateur' intraveineux."
        },
        {
            concept: "Hémodynamique pré-intubation",
            question: "L'intubation est décidée (troubles de conscience). Pourquoi le remplissage vasculaire pré-induction est-il crucial ?",
            options: [
                { text: "Pour diluer les médicaments d'induction.", correct: false },
                { text: "Pour prévenir le collapsus de reventilation (tamponnade gazeuse).", correct: true },
                { text: "Pour traiter la déshydratation liée à la polypnée.", correct: false },
                { text: "Pour améliorer la diffusion de l'O2.", correct: false }
            ],
            rationale: "La pression positive intrathoracique va écraser le retour veineux. Une hypovolémie relative précipiterait l'arrêt cardiaque par désamorçage de la pompe.",
            hint: "Quand vous soufflez sous pression dans le thorax, le sang a du mal à rentrer dans le cœur."
        },
        {
            concept: "Choix Sonde Intubation",
            question: "Quelle taille de sonde d'intubation choisissez-vous pour cette adulte ?",
            options: [
                { text: "La plus petite possible (6.0) pour ne pas irriter.", correct: false },
                { text: "Un calibre large (7.5 ou 8.0).", correct: true },
                { text: "Une sonde armée obligatoirement.", correct: false },
                { text: "Peu importe.", correct: false }
            ],
            rationale: "Il faut minimiser les résistances du tube (le patient a déjà des résistances bronchiques énormes) et permettre le passage aisé d'une sonde d'aspiration pour les bouchons muqueux.",
            hint: "Petit tube = Énorme résistance (Loi de Poiseuille : rayon puissance 4)."
        },
        {
            concept: "Choix Curare ISR",
            question: "Induction séquence rapide (ISR). Quel curare privilégiez-vous ?",
            options: [
                { text: "Atracurium.", correct: false },
                { text: "Succinylcholine (Célocurine).", correct: true },
                { text: "Rocuronium, à faible dose.", correct: false },
                { text: "Aucun curare pour garder la ventilation spontanée.", correct: false }
            ],
            rationale: "La Succinylcholine ou le Rocuronium (à forte dose 1.2mg/kg) sont les choix pour l'ISR. Le but est d'éviter l'Atracurium qui est histamino-libérateur.",
            hint: "On veut rapide, puissant et sans histamine."
        },
        {
            concept: "Mécanique Ventilatoire",
            question: "Sous ventilation : Pression Crête 50 cmH2O (haute), Pression Plateau 20 cmH2O (normale). Quel est le diagnostic ?",
            options: [
                { text: "Diminution de la compliance (poumon rigide).", correct: false },
                { text: "Augmentation des résistances des voies aériennes.", correct: true },
                { text: "Pneumothorax sous tension.", correct: false },
                { text: "Sonde intubation bouchée.", correct: false }
            ],
            rationale: "L'écart important entre Crête (Pression dynamique) et Plateau (Pression statique) signe l'obstacle résistif pur (bronchospasme). Si le plateau montait aussi, ce serait un problème de compliance (PNO, OAP).",
            hint: "Si seule la crête monte, c'est un problème de 'tuyaux', pas de 'ballons'."
        },
        {
            concept: "Réglage Fréquence Respiratoire",
            question: "Pourquoi choisir une fréquence respiratoire basse (10-12/min) sur le respirateur ?",
            options: [
                { text: "Mettre les muscles au repos.", correct: false },
                { text: "Allonger le temps expiratoire total par minute.", correct: true },
                { text: "Augmenter la ventilation minute.", correct: false },
                { text: "Pour synchroniser le patient.", correct: false }
            ],
            rationale: "Moins de cycles par minute = plus de secondes disponibles entre chaque cycle pour vider les poumons et éviter l'auto-PEEP (air trapping).",
            hint: "Le poumon de l'asthmatique est une bouteille qui se vide très, très lentement."
        },
        {
            concept: "Ratio I:E",
            question: "Réglage I:E à 1:4 avec une FR 10/min. Combien de temps dure l'expiration ?",
            options: [
                { text: "3 secondes.", correct: false },
                { text: "4.8 secondes.", correct: true },
                { text: "4 secondes.", correct: false },
                { text: "5 secondes.", correct: false }
            ],
            rationale: "Un cycle dure 60s / 10 = 6 secondes. Le ratio est 1+4 = 5 parts. 1 part = 1.2s. L'expiration (4 parts) = 4 * 1.2s = 4.8s.",
            hint: "Divisez 6 secondes en 5 parts."
        },
        {
            concept: "Hypercapnie Permissive",
            question: "Quel est l'objectif concernant le pH et la PaCO2 (Hypercapnie Permissive) ?",
            options: [
                { text: "Normaliser la PaCO2 à 40 mmHg.", correct: false },
                { text: "Tolérer l'acidose tant que pH > 7.20 pour protéger le poumon.", correct: true },
                { text: "Maintenir un pH > 7.45.", correct: false },
                { text: "Utiliser du Bicarbonate systématiquement.", correct: false }
            ],
            rationale: "La priorité est la mécanique (éviter l'auto-PEEP et l'éclatement du poumon). On tolère le CO2 élevé tant que le pH n'est pas menaçant pour le cœur.",
            hint: "Mieux vaut un patient un peu acide mais vivant (sans barotraumatisme)."
        },
        {
            concept: "Dépistage Auto-PEEP",
            question: "Comment repérer visuellement l'Auto-PEEP sur le respirateur ?",
            options: [
                { text: "La courbe de pression ne redescend pas.", correct: false },
                { text: "La courbe de débit expiratoire ne revient pas à zéro avant le cycle suivant.", correct: true },
                { text: "Le volume courant est bas.", correct: false },
                { text: "La capnographie est plate.", correct: false }
            ],
            rationale: "Cela signifie qu'il restait encore de l'air à sortir quand la machine a lancé l'inspiration suivante (Air Trapping).",
            hint: "Regardez la courbe de débit (Flow) en fin d'expiration."
        },
        {
            concept: "ACR & Tamponnade Gazeuse",
            question: "Arrêt cardiaque brutal sous respirateur avec alarme 'Pressions élevées'. Première action spécifique ?",
            options: [
                { text: "Adrénaline 1mg IV.", correct: false },
                { text: "Déconnecter le patient du respirateur et comprimer le thorax.", correct: true },
                { text: "Choc électrique externe.", correct: false },
                { text: "Vérifier la position de la sonde.", correct: false }
            ],
            rationale: "Il faut lever la tamponnade gazeuse immédiatement en déconnectant le circuit pour permettre une expiration passive complète.",
            hint: "Il faut 'déboucher' la sortie pour laisser l'air piégé sortir."
        },
        {
            concept: "Pneumothorax Compressif",
            question: "Après déconnexion, le pouls ne repart pas. Suspicion de PNO compressif. Que faire ?",
            options: [
                { text: "Demander une radio thorax au lit.", correct: false },
                { text: "Exsufflation immédiate à l'aiguille (ou thoracostomie).", correct: true },
                { text: "Intubation sélective.", correct: false },
                { text: "Echographie cardiaque complète.", correct: false }
            ],
            rationale: "C'est un geste de sauvetage immédiat sur présomption clinique devant un ACR. On ne perd pas de temps avec l'imagerie.",
            hint: "Pas le temps pour la radio en cas d'arrêt cardiaque."
        },
        {
            concept: "Neuromyopathie de Réa",
            question: "Quelle est la complication neuromusculaire spécifique de l'association Corticoïdes + Curares ?",
            options: [
                { text: "Syndrome de Guillain-Barré.", correct: false },
                { text: "Neuromyopathie de réanimation (Myopathie quadriplégique aiguë).", correct: true },
                { text: "Etat de mal épileptique.", correct: false },
                { text: "Myasthénie auto-immune.", correct: false }
            ],
            rationale: "C'est le facteur de risque majeur de myopathie aiguë sévère et durable chez l'asthmatique ventilé.",
            hint: "Paralysie flasque diffuse au réveil."
        },
        {
            concept: "Test de Fuite",
            question: "Avant l'extubation, quel test pour vérifier l'absence d'oedème laryngé ?",
            options: [
                { text: "Le test de fuite (Cuff Leak Test).", correct: true },
                { text: "Une fibroscopie bronchique.", correct: false },
                { text: "Une épreuve de ventilation spontanée.", correct: false },
                { text: "Un scanner cervical.", correct: false }
            ],
            rationale: "On dégonfle le ballonnet : si l'air fuit autour de la sonde, c'est qu'il y a de la place (pas d'œdème majeur). Si pas de fuite, risque de stridor à l'extubation.",
            hint: "L'air doit pouvoir passer 'à côté' du tube."
        },
        {
            concept: "Antibiothérapie",
            question: "Place des antibiotiques en post-crise immédiate ?",
            options: [
                { text: "Systématiques pour tout asthme grave.", correct: false },
                { text: "Uniquement si signes francs d'infection bactérienne (fièvre, crachats purulents, foyer radio).", correct: true },
                { text: "Toujours un macrolide.", correct: false },
                { text: "Si immunodépression seulement.", correct: false }
            ],
            rationale: "La majorité des crises sont virales ou allergiques. L'antibiothérapie systématique n'est pas recommandée.",
            hint: "L'asthme est rarement d'origine bactérienne."
        },
        {
            concept: "Prévention Récidive",
            question: "À la sortie, quel élément est indispensable pour prévenir la récidive ?",
            options: [
                { text: "Bronchodilatateurs courte durée uniquement.", correct: false },
                { text: "Corticothérapie inhalée (fond) +/- LABA et éducation thérapeutique.", correct: true },
                { text: "Interdire le sport définitivement.", correct: false },
                { text: "Déménagement immédiat.", correct: false }
            ],
            rationale: "Le contrôle de l'inflammation de fond par CSI est la clé pour éviter la prochaine crise grave.",
            hint: "Il faut traiter le 'feu' (l'inflammation) tous les jours, pas juste quand ça brûle."
        }
    ];

    // --- Logique de l'Application ---
    const app = {
        state: {
            currentQuestion: 0,
            score: 0,
            answered: false,
            userAnswers: [] // Stocke l'état de chaque réponse
        },

        init: function() {
            this.showScreen('screen-welcome');
        },

        showScreen: function(screenId) {
            document.querySelectorAll('.screen').forEach(el => {
                el.classList.remove('active');
                setTimeout(() => {
                    if(!el.classList.contains('active')) el.style.display = 'none';
                }, 300);
            });
            
            const target = document.getElementById(screenId);
            target.style.display = 'flex';
            setTimeout(() => target.classList.add('active'), 50);
            
            const content = target.querySelector('.scrollable-content');
            if(content) content.scrollTop = 0;
        },

        startQuiz: function() {
            this.state.currentQuestion = 0;
            this.state.score = 0;
            this.state.answered = false;
            this.state.userAnswers = [];
            this.loadQuestion();
            this.showScreen('screen-quiz');
        },

        loadQuestion: function() {
            const data = quizData[this.state.currentQuestion];
            this.state.answered = false;
            
            document.getElementById('question-text').textContent = data.question;
            document.getElementById('progress-text').textContent = `${this.state.currentQuestion + 1}/${quizData.length}`;
            
            const progressPercent = ((this.state.currentQuestion) / quizData.length) * 100;
            document.getElementById('progress-fill').style.width = `${progressPercent}%`;

            document.getElementById('hint-content').style.display = 'none';
            document.getElementById('feedback-area').style.display = 'none';
            document.getElementById('next-btn').style.display = 'none';
            document.getElementById('hint-btn').style.display = 'flex';
            
            document.getElementById('hint-content').textContent = data.hint;

            const optionsContainer = document.getElementById('options-list');
            optionsContainer.innerHTML = '';
            const letters = ['A', 'B', 'C', 'D'];

            data.options.forEach((opt, index) => {
                const btn = document.createElement('button');
                btn.className = 'option-card';
                btn.innerHTML = `<span class="option-letter">${letters[index]}</span><span>${opt.text}</span>`;
                btn.onclick = () => this.handleAnswer(index, opt.correct, btn);
                optionsContainer.appendChild(btn);
            });
        },

        toggleHint: function() {
            const hintBox = document.getElementById('hint-content');
            hintBox.style.display = hintBox.style.display === 'block' ? 'none' : 'block';
        },

        handleAnswer: function(index, isCorrect, btnElement) {
            if (this.state.answered) return;
            this.state.answered = true;

            // Enregistrer la réponse pour le rapport
            this.state.userAnswers.push({
                questionIndex: this.state.currentQuestion,
                correct: isCorrect,
                concept: quizData[this.state.currentQuestion].concept
            });

            const allBtns = document.querySelectorAll('.option-card');
            allBtns.forEach(btn => btn.disabled = true);

            btnElement.classList.add(isCorrect ? 'correct' : 'incorrect');

            if (!isCorrect) {
                if(navigator.vibrate) navigator.vibrate(200);
                const data = quizData[this.state.currentQuestion];
                data.options.forEach((opt, i) => {
                    if (opt.correct) {
                        allBtns[i].classList.add('correct');
                    }
                });
            } else {
                this.state.score++;
                if(navigator.vibrate) navigator.vibrate([50, 50, 50]);
            }

            const feedbackArea = document.getElementById('feedback-area');
            const feedbackHeader = document.getElementById('feedback-header');
            const feedbackText = document.getElementById('feedback-text');

            feedbackHeader.innerHTML = isCorrect 
                ? '<span style="color:var(--success)">✅ Excellente réponse</span>' 
                : '<span style="color:var(--error)">❌ Réponse incorrecte</span>';
            
            feedbackText.textContent = quizData[this.state.currentQuestion].rationale;
            feedbackArea.style.display = 'block';

            document.getElementById('next-btn').style.display = 'flex';
            document.getElementById('hint-btn').style.display = 'none';
            
            const content = document.querySelector('#screen-quiz .scrollable-content');
            setTimeout(() => {
                content.scrollTo({ top: content.scrollHeight, behavior: 'smooth' });
            }, 100);
        },

        nextQuestion: function() {
            this.state.currentQuestion++;
            if (this.state.currentQuestion < quizData.length) {
                this.loadQuestion();
            } else {
                this.showResults();
            }
        },

        showResults: function() {
            const score = this.state.score;
            document.getElementById('final-score').textContent = score;
            
            // Animation Score
            const radius = 45;
            const circumference = 2 * Math.PI * radius;
            const offset = circumference - ((score / quizData.length) * circumference);
            setTimeout(() => {
                document.getElementById('score-circle-fill').style.strokeDashoffset = offset;
            }, 500);
            
            const percent = (score / quizData.length) * 100;
            let title = "", msg = "";

            if (percent === 100) { title = "Expert 🏆"; msg = "Maîtrise parfaite."; }
            else if (percent >= 80) { title = "Excellent 👏"; msg = "Très solides connaissances."; }
            else if (percent >= 50) { title = "Validé 👍"; msg = "Les bases sont acquises."; }
            else { title = "À revoir 📚"; msg = "Révisez les bases physiopathologiques."; }

            document.getElementById('final-title').textContent = title;
            document.getElementById('final-msg').textContent = msg;

            // --- GÉNÉRATION DU RAPPORT ---
            const reportContainer = document.getElementById('final-report');
            
            // 1. Liste des concepts validés
            const masteredConcepts = this.state.userAnswers
                .filter(a => a.correct)
                .map(a => a.concept);

            let conceptsHtml = '';
            if (masteredConcepts.length > 0) {
                conceptsHtml = `
                    <div class="report-card">
                        <div class="report-title">
                            <span>✅</span> Vos Points Forts
                        </div>
                        <div class="success-tags-container">
                            ${masteredConcepts.map(c => `<span class="success-tag">✓ ${c}</span>`).join('')}
                        </div>
                    </div>
                `;
            }

            // 2. Fiche de Synthèse (Statique)
            const summaryHtml = `
                <div class="report-card summary-section">
                    <div class="report-title">
                        <span>📋</span> Fiche de Synthèse : AAG
                    </div>
                    
                    <h4>1. Reconnaître la Gravité</h4>
                    <ul>
                        <li><strong>Signes :</strong> Silence auscultatoire, dyspnée paradoxale, troubles conscience.</li>
                        <li><strong>Gazométrie :</strong> Une normocapnie (PaCO2 ~40) chez un polypnéique signe l'épuisement.</li>
                    </ul>

                    <h4>2. Traiter sans délai</h4>
                    <ul>
                        <li><strong>Oxygène :</strong> Cible 94-98% (Attention hyperoxie).</li>
                        <li><strong>Bronchodilatateurs :</strong> B2 + Anticholinergiques nébulisés en continu.</li>
                        <li><strong>Systémique :</strong> Corticoïdes IV (délai 4-6h) + Sulfate de Magnésium IV.</li>
                    </ul>

                    <h4>3. Ventiler (si échec)</h4>
                    <ul>
                        <li><strong>Induction :</strong> Pré-remplissage + Kétamine + Suxamethonium/Rocu.</li>
                        <li><strong>Réglages :</strong> FR basse (10-12), I:E long (1:4) pour expirer.</li>
                        <li><strong>Tolérance :</strong> Hypercapnie permissive tant que pH > 7.20.</li>
                    </ul>

                    <h4>4. Sauver (ACR)</h4>
                    <ul>
                        <li><strong>Tamponnade gazeuse :</strong> Déconnexion immédiate du respirateur.</li>
                        <li><strong>PNO :</strong> Exsufflation bilatérale si doute.</li>
                    </ul>
                </div>
            `;

            reportContainer.innerHTML = conceptsHtml + summaryHtml;

            this.showScreen('screen-results');
        },

        restart: function() {
            document.getElementById('score-circle-fill').style.strokeDashoffset = 283; 
            this.startQuiz();
        }
    };

    window.addEventListener('load', () => {
        app.init();
    });

</script>

</body>
</html>
