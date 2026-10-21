<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Portal Educacional DEE - Circuitos de Temporização (Constante de Tempo RC)">
  <title>DEE Portal | Circuitos de Temporização (Constante de Tempo RC)</title>
  
  <!-- Fontes Google Inter -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">

  <style>
    /* ==========================================================================
       DESIGN SYSTEM & VARIÁVEIS CSS
       ========================================================================== */
    :root {
      --bg-main: #0F172A;        /* Azul Escuro Noturno */
      --bg-card: #1E293B;        /* Painel/Card */
      --bg-card-hover: #26334D;  /* Card Hover */
      --border: #334155;         /* Bordas Sutis */
      --verde-neon: #00E676;    /* Cor Primária / Eletricidade */
      --verde-dark: #00A852;     /* Verde Interativo Dark */
      --amarelo: #FACC15;        /* Destaques / Avisos */
      --azul-accent: #38BDF8;    /* Acento Secundário */
      --roxo-accent: #A855F7;   /* Acento de Fluxo */
      --texto-main: #F8FAFC;     /* Texto Principal */
      --texto-sub: #94A3B8;      /* Texto Secundário */
      --texto-muted: #64748B;    /* Texto Apagado */
      --danger: #EF4444;         /* Erros/Alertas */
      --radius: 12px;            /* Bordas Arredondadas */
      --shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.4), 0 8px 10px -6px rgba(0, 0, 0, 0.3);
      --font-mono: 'JetBrains Mono', monospace;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      scroll-behavior: smooth;
    }

    body {
      background-color: var(--bg-main);
      color: var(--texto-main);
      font-family: 'Inter', system-ui, -apple-system, sans-serif;
      line-height: 1.6;
      overflow-x: hidden;
    }

    /* ==========================================================================
       BARRA DE ROLAGEM CUSTOMIZADA
       ========================================================================== */
    ::-webkit-scrollbar {
      width: 10px;
    }
    ::-webkit-scrollbar-track {
      background: var(--bg-main);
    }
    ::-webkit-scrollbar-thumb {
      background: var(--border);
      border-radius: 5px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: var(--verde-neon);
    }

    /* ==========================================================================
       HEADER / TOP BAR
       ========================================================================== */
    .header {
      position: sticky;
      top: 0;
      z-index: 1000;
      background-color: rgba(30, 41, 59, 0.92);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      padding: 0.8rem 2rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1.5rem;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      text-decoration: none;
      color: var(--texto-main);
      font-weight: 800;
      font-size: 1.35rem;
      letter-spacing: -0.5px;
    }

    .logo-icon {
      width: 40px;
      height: 40px;
      background: linear-gradient(135deg, var(--verde-neon), #00B0FF);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 0 15px rgba(0, 230, 118, 0.4);
    }

    .logo-icon svg {
      width: 22px;
      height: 22px;
      fill: #0F172A;
    }

    .logo-text span {
      color: var(--verde-neon);
    }

    /* BARRA DE PESQUISA */
    .search-container {
      position: relative;
      flex: 1;
      max-width: 420px;
    }

    .search-input {
      width: 100%;
      background-color: var(--bg-main);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 0.55rem 1rem 0.55rem 2.6rem;
      color: var(--texto-main);
      font-size: 0.9rem;
      transition: all 0.3s ease;
    }

    .search-input:focus {
      outline: none;
      border-color: var(--verde-neon);
      box-shadow: 0 0 0 3px rgba(0, 230, 118, 0.15);
    }

    .search-icon {
      position: absolute;
      left: 0.9rem;
      top: 50%;
      transform: translateY(-50%);
      color: var(--texto-sub);
      width: 16px;
      height: 16px;
    }

    /* MENU NAVEGAÇÃO SUPERIOR */
    .nav-links {
      display: flex;
      align-items: center;
      gap: 1.2rem;
      list-style: none;
    }

    .nav-links a {
      color: var(--texto-sub);
      text-decoration: none;
      font-weight: 500;
      font-size: 0.9rem;
      transition: color 0.2s ease;
    }

    .nav-links a:hover {
      color: var(--verde-neon);
    }

    .btn-cta {
      background: linear-gradient(135deg, var(--verde-neon), #00C853);
      color: #0F172A;
      font-weight: 700;
      padding: 0.55rem 1.2rem;
      border-radius: 8px;
      border: none;
      cursor: pointer;
      font-size: 0.88rem;
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      box-shadow: 0 4px 12px rgba(0, 230, 118, 0.25);
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .btn-cta:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 18px rgba(0, 230, 118, 0.4);
    }

    /* ==========================================================================
       LAYOUT PRINCIPAL (GRID SIDEBAR + CONTENT)
       ========================================================================== */
    .app-layout {
      display: grid;
      grid-template-columns: 280px 1fr;
      min-height: calc(100vh - 65px);
    }

    /* ==========================================================================
       SIDEBAR / LEFT MENU
       ========================================================================== */
    .sidebar {
      background-color: var(--bg-card);
      border-right: 1px solid var(--border);
      padding: 1.8rem 1.2rem;
      position: sticky;
      top: 65px;
      height: calc(100vh - 65px);
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .sidebar-title {
      font-size: 0.75rem;
      text-transform: uppercase;
      letter-spacing: 1.2px;
      color: var(--texto-muted);
      font-weight: 700;
      padding-left: 0.5rem;
    }

    .sidebar-menu {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 0.35rem;
    }

    .sidebar-menu a {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      padding: 0.65rem 0.85rem;
      color: var(--texto-sub);
      text-decoration: none;
      font-size: 0.9rem;
      font-weight: 500;
      border-radius: 8px;
      transition: all 0.2s ease;
    }

    .sidebar-menu a:hover {
      background-color: rgba(255, 255, 255, 0.05);
      color: var(--texto-main);
    }

    .sidebar-menu a.active {
      background-color: rgba(0, 230, 118, 0.12);
      color: var(--verde-neon);
      font-weight: 600;
      border-left: 3px solid var(--verde-neon);
    }

    .sidebar-menu svg {
      width: 18px;
      height: 18px;
      flex-shrink: 0;
    }

    /* ==========================================================================
       CONTEÚDO PRINCIPAL (PAINEL CENTRAL)
       ========================================================================== */
    .content-area {
      padding: 2.5rem 3rem;
      max-width: 1200px;
      margin: 0 auto;
      width: 100%;
    }

    /* HERO BANNER DO TEMA */
    .hero-banner {
      background: linear-gradient(135deg, rgba(30, 41, 59, 0.9), rgba(15, 23, 42, 0.95)), 
                  radial-gradient(circle at top right, rgba(0, 230, 118, 0.15), transparent 50%);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 2.5rem;
      margin-bottom: 2.5rem;
      position: relative;
      overflow: hidden;
      box-shadow: var(--shadow);
    }

    .hero-banner::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 4px;
      height: 100%;
      background: var(--verde-neon);
    }

    .badge-category {
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
      background-color: rgba(0, 230, 118, 0.12);
      color: var(--verde-neon);
      border: 1px solid rgba(0, 230, 118, 0.3);
      padding: 0.25rem 0.75rem;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 1rem;
    }

    .hero-banner h1 {
      font-size: 2.3rem;
      font-weight: 800;
      letter-spacing: -0.8px;
      line-height: 1.25;
      margin-bottom: 0.8rem;
      color: var(--texto-main);
    }

    .hero-banner p {
      color: var(--texto-sub);
      font-size: 1.05rem;
      max-width: 800px;
    }

    /* CARDS DE SEÇÃO DE CONTEÚDO */
    .section-card {
      background-color: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 2rem;
      margin-bottom: 2rem;
      box-shadow: var(--shadow);
      transition: border-color 0.3s ease;
    }

    .section-card:hover {
      border-color: rgba(0, 230, 118, 0.3);
    }

    .section-header {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      margin-bottom: 1.5rem;
      padding-bottom: 0.8rem;
      border-bottom: 1px solid var(--border);
    }

    .section-icon {
      width: 36px;
      height: 36px;
      background-color: rgba(0, 230, 118, 0.1);
      color: var(--verde-neon);
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .section-icon svg {
      width: 20px;
      height: 20px;
    }

    .section-title {
      font-size: 1.4rem;
      font-weight: 700;
      color: var(--texto-main);
    }

    /* GRID DE DUAS COLUNAS */
    .grid-2col {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.5rem;
      margin-top: 1rem;
    }

    /* DESTAQUES E CAIXAS FÓRMULA */
    .formula-box {
      background-color: #0F172A;
      border: 1px solid var(--border);
      border-left: 4px solid var(--verde-neon);
      border-radius: 8px;
      padding: 1.25rem 1.5rem;
      margin: 1.2rem 0;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .formula-main {
      font-family: var(--font-mono);
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--verde-neon);
      letter-spacing: 0.5px;
    }

    .formula-desc {
      font-size: 0.88rem;
      color: var(--texto-sub);
    }

    /* TABELA DOS TAUS */
    .tau-table {
      width: 100%;
      border-collapse: collapse;
      margin: 1rem 0;
      font-size: 0.9rem;
    }

    .tau-table th, .tau-table td {
      padding: 0.75rem 1rem;
      text-align: left;
      border-bottom: 1px solid var(--border);
    }

    .tau-table th {
      background-color: rgba(15, 23, 42, 0.6);
      color: var(--verde-neon);
      font-weight: 600;
    }

    .tau-table tr:hover {
      background-color: rgba(255, 255, 255, 0.02);
    }

    .tau-badge {
      display: inline-block;
      padding: 0.15rem 0.5rem;
      background-color: rgba(56, 189, 248, 0.15);
      color: var(--azul-accent);
      border-radius: 4px;
      font-family: var(--font-mono);
      font-weight: 600;
      font-size: 0.85rem;
    }

    /* ==========================================================================
       MAPA MENTAL INTERATIVO (FLUXOGRAMA ESTILIZADO)
       ========================================================================== */
    .mindmap-container {
      background-color: #0F172A;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 2rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1.5rem;
      position: relative;
      overflow-x: auto;
    }

    .mindmap-root {
      background: linear-gradient(135deg, var(--verde-neon), #00C853);
      color: #0F172A;
      font-weight: 800;
      font-size: 1.1rem;
      padding: 0.8rem 1.8rem;
      border-radius: 30px;
      box-shadow: 0 0 20px rgba(0, 230, 118, 0.3);
      text-align: center;
    }

    .mindmap-branches {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
      width: 100%;
      position: relative;
    }

    .mindmap-node {
      background-color: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 1.2rem;
      display: flex;
      flex-direction: column;
      gap: 0.6rem;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
      transition: transform 0.2s;
    }

    .mindmap-node:hover {
      transform: translateY(-3px);
      border-color: var(--verde-neon);
    }

    .mindmap-node h4 {
      color: var(--azul-accent);
      font-size: 1rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .mindmap-node ul {
      list-style: none;
      padding-left: 0;
      font-size: 0.85rem;
      color: var(--texto-sub);
    }

    .mindmap-node li {
      margin-bottom: 0.4rem;
      position: relative;
      padding-left: 1.2rem;
    }

    .mindmap-node li::before {
      content: '▸';
      position: absolute;
      left: 0;
      color: var(--verde-neon);
    }

    /* ==========================================================================
       SIMULADOR INTERATIVO RC (CANVAS + CONTROLES)
       ========================================================================== */
    .simulator-container {
      background-color: #0F172A;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 1.5rem;
      display: grid;
      grid-template-columns: 320px 1fr;
      gap: 1.5rem;
    }

    .controls-panel {
      display: flex;
      flex-direction: column;
      gap: 1.2rem;
      background-color: var(--bg-card);
      padding: 1.25rem;
      border-radius: 8px;
      border: 1px solid var(--border);
    }

    .control-group {
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }

    .control-group label {
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--texto-sub);
      display: flex;
      justify-content: space-between;
    }

    .control-group label span {
      color: var(--verde-neon);
      font-family: var(--font-mono);
    }

    .control-group input[type="range"] {
      width: 100%;
      accent-color: var(--verde-neon);
      cursor: pointer;
    }

    .btn-sim-group {
      display: flex;
      gap: 0.5rem;
      margin-top: 0.5rem;
    }

    .btn-sim {
      flex: 1;
      padding: 0.6rem;
      border: none;
      border-radius: 6px;
      font-weight: 700;
      font-size: 0.85rem;
      cursor: pointer;
      transition: all 0.2s;
    }

    .btn-sim-charge {
      background-color: var(--verde-neon);
      color: #0F172A;
    }

    .btn-sim-discharge {
      background-color: #38BDF8;
      color: #0F172A;
    }

    .btn-sim-reset {
      background-color: var(--border);
      color: var(--texto-main);
    }

    .btn-sim:hover {
      filter: brightness(1.1);
    }

    .canvas-display-wrapper {
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
    }

    .canvas-container {
      background-color: #050B14;
      border: 1px solid var(--border);
      border-radius: 8px;
      position: relative;
      height: 280px;
      width: 100%;
      overflow: hidden;
    }

    canvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .sim-stats {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 0.8rem;
    }

    .stat-card {
      background-color: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 0.6rem 0.8rem;
      text-align: center;
    }

    .stat-title {
      font-size: 0.72rem;
      color: var(--texto-muted);
      text-transform: uppercase;
      font-weight: 700;
    }

    .stat-value {
      font-family: var(--font-mono);
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--verde-neon);
    }

    /* DIAGRAMAS SVG */
    .svg-diagram-wrapper {
      background-color: #0F172A;
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1rem;
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 1rem;
    }

    /* ==========================================================================
       RESUMO PARA CADERNO (CAIXA DESTACADA)
       ========================================================================== */
    .notebook-summary {
      background: repeating-linear-gradient(
        #1E293B,
        #1E293B 28px,
        #26334D 28px,
        #26334D 29px
      );
      border-left: 5px solid var(--amarelo);
      border-radius: 8px;
      padding: 1.5rem 1.8rem;
      color: var(--texto-main);
      box-shadow: var(--shadow);
    }

    .notebook-summary h3 {
      color: var(--amarelo);
      font-size: 1.2rem;
      margin-bottom: 1rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .notebook-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 0.6rem;
    }

    .notebook-list li {
      position: relative;
      padding-left: 1.5rem;
      font-size: 0.95rem;
      line-height: 1.5;
    }

    .notebook-list li::before {
      content: '📌';
      position: absolute;
      left: 0;
      font-size: 0.85rem;
    }

    /* ==========================================================================
       QUIZ INTERATIVO
       ========================================================================== */
    .quiz-container {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .quiz-question-card {
      background-color: #0F172A;
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 1.25rem;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .quiz-question-text {
      font-weight: 600;
      font-size: 0.98rem;
      color: var(--texto-main);
    }

    .quiz-options {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .quiz-option {
      background-color: var(--bg-card);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 0.65rem 1rem;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 0.75rem;
      font-size: 0.9rem;
      transition: all 0.2s;
    }

    .quiz-option:hover {
      border-color: var(--verde-neon);
      background-color: rgba(0, 230, 118, 0.05);
    }

    .quiz-option input[type="radio"] {
      accent-color: var(--verde-neon);
    }

    .quiz-option.correct {
      background-color: rgba(0, 230, 118, 0.15) !important;
      border-color: var(--verde-neon) !important;
      color: var(--verde-neon) !important;
      font-weight: 600;
    }

    .quiz-option.incorrect {
      background-color: rgba(239, 68, 68, 0.15) !important;
      border-color: var(--danger) !important;
      color: #FCA5A5 !important;
    }

    .quiz-feedback {
      font-size: 0.85rem;
      padding: 0.6rem 0.8rem;
      border-radius: 6px;
      display: none;
    }

    .quiz-feedback.show-correct {
      display: block;
      background-color: rgba(0, 230, 118, 0.1);
      color: var(--verde-neon);
      border: 1px solid rgba(0, 230, 118, 0.2);
    }

    .quiz-feedback.show-incorrect {
      display: block;
      background-color: rgba(239, 68, 68, 0.1);
      color: #FCA5A5;
      border: 1px solid rgba(239, 68, 68, 0.2);
    }

    .quiz-actions {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 1rem;
    }

    .quiz-score-display {
      font-family: var(--font-mono);
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--verde-neon);
    }

    /* ==========================================================================
       RODAPÉ / FOOTER
       ========================================================================== */
    .footer {
      background-color: var(--bg-card);
      border-top: 1px solid var(--border);
      padding: 3rem 2rem 1.5rem 2rem;
      color: var(--texto-sub);
      font-size: 0.88rem;
    }

    .footer-grid {
      max-width: 1200px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: 2fr 1fr 1fr 1fr;
      gap: 2rem;
      margin-bottom: 2.5rem;
    }

    .footer-brand h3 {
      color: var(--texto-main);
      font-size: 1.2rem;
      margin-bottom: 0.8rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .footer-brand p {
      color: var(--texto-sub);
      font-size: 0.85rem;
      line-height: 1.6;
    }

    .footer-col h4 {
      color: var(--texto-main);
      font-size: 0.95rem;
      margin-bottom: 1rem;
      font-weight: 600;
    }

    .footer-col ul {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .footer-col a {
      color: var(--texto-sub);
      text-decoration: none;
      transition: color 0.2s;
    }

    .footer-col a:hover {
      color: var(--verde-neon);
    }

    .footer-bottom {
      max-width: 1200px;
      margin: 0 auto;
      padding-top: 1.5rem;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
      font-size: 0.8rem;
      color: var(--texto-muted);
    }

    /* ==========================================================================
       RESPONSIVIDADE (MEDIA QUERIES)
       ========================================================================== */
    @media (max-width: 992px) {
      .app-layout {
        grid-template-columns: 1fr;
      }

      .sidebar {
        display: none; /* Em telas menores esconde sidebar estática */
      }

      .simulator-container {
        grid-template-columns: 1fr;
      }

      .mindmap-branches {
        grid-template-columns: 1fr;
      }

      .footer-grid {
        grid-template-columns: 1fr 1fr;
      }

      .content-area {
        padding: 1.5rem;
      }
    }

    @media (max-width: 600px) {
      .header {
        padding: 0.8rem 1rem;
      }

      .search-container {
        display: none;
      }

      .grid-2col {
        grid-template-columns: 1fr;
      }

      .footer-grid {
        grid-template-columns: 1fr;
      }

      .hero-banner h1 {
        font-size: 1.6rem;
      }
    }
  </style>
</head>
<body>

  <!-- ==========================================================================
       HEADER / TOP BAR
       ========================================================================== -->
  <header class="header">
    <a href="#" class="logo">
      <div class="logo-icon">
        <svg viewBox="0 0 24 24"><path d="M11 15H6l7-14v8h5l-7 14v-8z"/></svg>
      </div>
      <div class="logo-text">DEE<span>Portal</span></div>
    </a>

    <!-- BARRA DE PESQUISA RÁPIDA -->
    <div class="search-container">
      <svg class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
      <input type="text" class="search-input" id="global-search" placeholder="Pesquisar conceito, fórmula ou aplicação...">
    </div>

    <!-- NAVEGAÇÃO RÁPIDA SUPERIOR -->
    <ul class="nav-links">
      <li><a href="#introducao">Início</a></li>
      <li><a href="#teoria">Teoria</a></li>
      <li><a href="#simulador">Simulador</a></li>
      <li><a href="#quiz">Quiz</a></li>
    </ul>

    <a href="#contato" class="btn-cta">
      <span>Contato / Suporte</span>
    </a>
  </header>

  <!-- ==========================================================================
       LAYOUT PRINCIPAL (SIDEBAR + CONTENT)
       ========================================================================== -->
  <div class="app-layout">

    <!-- MENU LATERAL / SIDEBAR -->
    <aside class="sidebar">
      <span class="sidebar-title">Navegação do Assunto</span>
      <ul class="sidebar-menu">
        <li>
          <a href="#introducao" class="active">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="16" x2="12" y2="12"/><line x1="12" y1="8" x2="12.01" y2="8"/></svg>
            Introdução
          </a>
        </li>
        <li>
          <a href="#teoria">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>
            Teoria & Fórmulas
          </a>
        </li>
        <li>
          <a href="#mapa-mental">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><path d="M10 6h4m0 11h-4m-3 0V10"/></svg>
            Mapa Mental
          </a>
        </li>
        <li>
          <a href="#simulador">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 12h-4l-3 9L9 3l-3 9H2"/></svg>
            Simulador Interativo RC
          </a>
        </li>
        <li>
          <a href="#exemplos">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg>
            Exemplos Práticos
          </a>
        </li>
        <li>
          <a href="#resumo">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/></svg>
            Resumo para Caderno
          </a>
        </li>
        <li>
          <a href="#quiz">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 11l3 3L22 4"/><path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11"/></svg>
            Quiz de Fixação
          </a>
        </li>
        <li>
          <a href="#referencias">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/></svg>
            Referências
          </a>
        </li>
      </ul>
    </aside>

    <!-- PAINEL CENTRAL DE CONTEÚDO -->
    <main class="content-area">

      <!-- HERO BANNER DO ASSUNTO -->
      <section class="hero-banner" id="introducao">
        <div class="badge-category">Aplicações Práticas dos Componentes</div>
        <h1>Circuitos de Temporização<br><span style="color:var(--verde-neon)">Constante de Tempo RC</span></h1>
        <p>Aprenda como a combinação de resistores e capacitores permite criar atrasos precisos, temporizadores analógicos e filtros de ruído sem a necessidade de microcontroladores complexos.</p>
      </section>

      <!-- SEÇÃO 1: INTRODUÇÃO E IMPORTÂNCIA -->
      <article class="section-card">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
          </div>
          <h2 class="section-title">1. Introdução à Temporização Analógica</h2>
        </div>

        <p>Na eletrônica moderna e industrial, o controle de tempo é fundamental. Desde a temporização da luz interna de um veículo até a filtragem de ruídos em botões mecânicos (*debounce*), os circuitos de **Constante de Tempo RC** fornecem a base mais simples e confiável para criar intervalos de tempo temporizados.</p>

        <div class="grid-2col">
          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--verde-neon); margin-bottom: 0.5rem;">O Papel do Resistor (R)</h4>
            <p style="font-size: 0.9rem; color: var(--texto-sub);">O resistor atua como um "gargalo" que limita o fluxo de corrente elétrica (elétrons). Quanto maior a resistência, mais lento é o fluxo de carga para dentro do capacitor.</p>
          </div>
          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--azul-accent); margin-bottom: 0.5rem;">O Papel do Capacitor (C)</h4>
            <p style="font-size: 0.9rem; color: var(--texto-sub);">O capacitor atua como um reservatório de energia elétrica. Ele armazena carga em seu campo elétrico até atingir a tensão máxima da fonte de alimentação.</p>
          </div>
        </div>
      </article>

      <!-- SEÇÃO 2: TEORIA TÉCNICA E FÓRMULAS -->
      <article class="section-card" id="teoria">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>
          </div>
          <h2 class="section-title">2. Conteúdo Técnico & Fórmulas Matemáticas</h2>
        </div>

        <p>Quando uma tensão contínua ($V_{in}$) é aplicada a um circuito RC em série, a tensão no capacitor não sobe instantaneamente. A taxa de carga é governada pela equação exponencial da **Constante de Tempo ($\tau$, Tau)**.</p>

        <!-- CAIXA DE FÓRMULA PRINCIPAL -->
        <div class="formula-box">
          <div class="formula-main">&tau; = R &times; C</div>
          <div class="formula-desc">Onde <strong>&tau; (Tau)</strong> está em Segundos (s), <strong>R (Resistência)</strong> em Ohms (&Omega;), e <strong>C (Capacitância)</strong> em Farads (F).</div>
        </div>

        <h3 style="color: var(--texto-main); font-size: 1.1rem; margin: 1.5rem 0 0.8rem 0;">Equações Exponenciais de Carga e Descarga</h3>

        <div class="grid-2col">
          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--verde-neon); margin-bottom: 0.4rem;">Carga do Capacitor</h4>
            <div style="font-family: var(--font-mono); color: var(--verde-neon); font-size: 1.1rem; margin-bottom: 0.5rem;">V_c(t) = V_in &times; (1 - e^(-t / &tau;))</div>
            <p style="font-size: 0.85rem; color: var(--texto-sub);">A tensão cresce de forma rápida no início e vai desacelerando à medida que o capacitor fica cheio.</p>
          </div>

          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--azul-accent); margin-bottom: 0.4rem;">Descarga do Capacitor</h4>
            <div style="font-family: var(--font-mono); color: var(--azul-accent); font-size: 1.1rem; margin-bottom: 0.5rem;">V_c(t) = V_0 &times; e^(-t / &tau;)</div>
            <p style="font-size: 0.85rem; color: var(--texto-sub);">A energia cai rapidamente no início até se esgotar por completo após 5 Taus.</p>
          </div>
        </div>

        <h3 style="color: var(--texto-main); font-size: 1.1rem; margin: 1.5rem 0 0.8rem 0;">Tabela da Regra dos Taus (&tau;)</h3>

        <table class="tau-table">
          <thead>
            <tr>
              <th>Intervalo de Tempo</th>
              <th>Tensão de Carga (% do Vin)</th>
              <th>Tensão de Descarga (% do V0)</th>
              <th>Estado do Circuito</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><span class="tau-badge">1 &tau;</span></td>
              <td>63,2%</td>
              <td>36,8%</td>
              <td>Início rápido do processo</td>
            </tr>
            <tr>
              <td><span class="tau-badge">2 &tau;</span></td>
              <td>86,5%</td>
              <td>13,5%</td>
              <td>Carga intermediária</td>
            </tr>
            <tr>
              <td><span class="tau-badge">3 &tau;</span></td>
              <td>95,0%</td>
              <td>5,0%</td>
              <td>Aproximação da estabilização</td>
            </tr>
            <tr>
              <td><span class="tau-badge">4 &tau;</span></td>
              <td>98,2%</td>
              <td>1,8%</td>
              <td>Quase totalmente carregado</td>
            </tr>
            <tr>
              <td><span class="tau-badge">5 &tau;</span></td>
              <td><strong>99,3% (~100%)</strong></td>
              <td><strong>0,7% (~0%)</strong></td>
              <td><strong>Regime Permanente / Estável</strong></td>
            </tr>
          </tbody>
        </table>

        <!-- DIAGRAMA ESQUEMÁTICO SVG DO CIRCUITO -->
        <h3 style="color: var(--texto-main); font-size: 1.1rem; margin: 1.5rem 0 0.8rem 0;">Esquemático Elétrico do Circuito RC</h3>
        <div class="svg-diagram-wrapper">
          <svg width="480" height="200" viewBox="0 0 480 200" fill="none">
            <!-- Fonte de Tensão DC -->
            <circle cx="60" cy="100" r="22" stroke="#00E676" stroke-width="2.5" fill="#1E293B"/>
            <text x="60" y="95" fill="#00E676" font-family="sans-serif" font-weight="bold" font-size="14" text-anchor="middle">+</text>
            <text x="60" y="115" fill="#00E676" font-family="sans-serif" font-weight="bold" font-size="14" text-anchor="middle">-</text>
            <text x="60" y="145" fill="#94A3B8" font-family="sans-serif" font-size="12" text-anchor="middle">Vin (DC)</text>

            <!-- Fios e conexões -->
            <path d="M 60 78 L 60 40 L 140 40" stroke="#F8FAFC" stroke-width="2.5" fill="none"/>
            <path d="M 60 122 L 60 160 L 420 160 L 420 130" stroke="#F8FAFC" stroke-width="2.5" fill="none"/>

            <!-- Resistor R -->
            <path d="M 140 40 L 155 40 L 162 28 L 176 52 L 190 28 L 204 52 L 218 28 L 225 40 L 260 40" stroke="#38BDF8" stroke-width="2.5" fill="none"/>
            <text x="190" y="20" fill="#38BDF8" font-family="sans-serif" font-weight="bold" font-size="13" text-anchor="middle">Resistor (R)</text>

            <!-- Capacitor C -->
            <path d="M 260 40 L 420 40 L 420 70" stroke="#F8FAFC" stroke-width="2.5" fill="none"/>
            <line x1="400" y1="70" x2="440" y2="70" stroke="#00E676" stroke-width="3"/>
            <line x1="400" y1="82" x2="440" y2="82" stroke="#00E676" stroke-width="3"/>
            <text x="450" y="80" fill="#00E676" font-family="sans-serif" font-weight="bold" font-size="13">C</text>

            <!-- Tensão Vc -->
            <path d="M 380 40 L 380 160" stroke="#FACC15" stroke-width="1.5" stroke-dasharray="4" fill="none"/>
            <text x="365" y="105" fill="#FACC15" font-family="sans-serif" font-weight="bold" font-size="12" text-anchor="end">Vc(t)</text>
          </svg>
        </div>
      </article>

      <!-- SEÇÃO 3: MAPA MENTAL INTERATIVO -->
      <article class="section-card" id="mapa-mental">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><path d="M10 6h4m0 11h-4m-3 0V10"/></svg>
          </div>
          <h2 class="section-title">3. Mapa Mental Interativo</h2>
        </div>

        <p style="margin-bottom: 1.5rem;">Sintetize a relação completa do circuito RC com componentes, fórmulas e aplicações reais através deste mapa do ecossistema:</p>

        <div class="mindmap-container">
          <div class="mindmap-root">Circuitos de Temporização RC</div>

          <div class="mindmap-branches">
            <div class="mindmap-node">
              <h4>⚡ Componentes Básicos</h4>
              <ul>
                <li><strong>Resistor (R):</strong> Limita a corrente elétrica de carga (&Omega;).</li>
                <li><strong>Capacitor (C):</strong> Armazena energia em campo elétrico (Farads).</li>
                <li><strong>Fonte DC:</strong> Fornece a diferença de potencial elétrico.</li>
              </ul>
            </div>

            <div class="mindmap-node">
              <h4>📐 Fórmulas & Regras</h4>
              <ul>
                <li><strong>&tau; = R &times; C:</strong> Tempo em segundos para atingir 63,2%.</li>
                <li><strong>5 &tau;:</strong> Estabilização e carga completa (~100%).</li>
                <li><strong>Curva Exponencial:</strong> Carga desacelera com o tempo.</li>
              </ul>
            </div>

            <div class="mindmap-node">
              <h4>🚀 Aplicações Reais</h4>
              <ul>
                <li><strong>Debounce:</strong> Filtro de ruído mecânico em botões.</li>
                <li><strong>Luz Automotiva:</strong> Esmaecimento suave após fechar a porta.</li>
                <li><strong>Temporizador 555:</strong> Geração de pulsos e clocks.</li>
              </ul>
            </div>
          </div>
        </div>
      </article>

      <!-- SEÇÃO 4: SIMULADOR INTERATIVO COM CANVAS -->
      <article class="section-card" id="simulador">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 12h-4l-3 9L9 3l-3 9H2"/></svg>
          </div>
          <h2 class="section-title">4. Simulador Interativo em Tempo Real</h2>
        </div>

        <p style="margin-bottom: 1.2rem;">Ajuste a resistência, capacitância e tensão da fonte para ver a curva exponencial de carga ou descarga sendo desenhada ao vivo no gráfico Canvas:</p>

        <div class="simulator-container">
          <!-- PAINEL DE CONTROLES -->
          <div class="controls-panel">
            <div class="control-group">
              <label for="range-r">Resistência (R): <span id="val-r">10 k&Omega;</span></label>
              <input type="range" id="range-r" min="1" max="100" value="10">
            </div>

            <div class="control-group">
              <label for="range-c">Capacitância (C): <span id="val-c">100 &mu;F</span></label>
              <input type="range" id="range-c" min="10" max="1000" step="10" value="100">
            </div>

            <div class="control-group">
              <label for="range-v">Tensão de Entrada (Vin): <span id="val-v">12 V</span></label>
              <input type="range" id="range-v" min="1" max="24" value="12">
            </div>

            <div class="btn-sim-group">
              <button class="btn-sim btn-sim-charge" id="btn-charge">▶ Carregar</button>
              <button class="btn-sim btn-sim-discharge" id="btn-discharge">▼ Descarregar</button>
              <button class="btn-sim btn-sim-reset" id="btn-reset">↺ Reset</button>
            </div>
          </div>

          <!-- ÁREA DO CANVAS E ESTATÍSTICAS -->
          <div class="canvas-display-wrapper">
            <div class="canvas-container">
              <canvas id="rc-canvas"></canvas>
            </div>

            <div class="sim-stats">
              <div class="stat-card">
                <div class="stat-title">Constante (&tau;)</div>
                <div class="stat-value" id="stat-tau">1.00 s</div>
              </div>
              <div class="stat-card">
                <div class="stat-title">Tempo Total (5&tau;)</div>
                <div class="stat-value" id="stat-5tau">5.00 s</div>
              </div>
              <div class="stat-card">
                <div class="stat-title">Tensão no Cap (Vc)</div>
                <div class="stat-value" id="stat-vc" style="color: var(--amarelo);">0.00 V</div>
              </div>
            </div>
          </div>
        </div>
      </article>

      <!-- SEÇÃO 5: EXEMPLOS PRÁTICOS -->
      <article class="section-card" id="exemplos">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg>
          </div>
          <h2 class="section-title">5. Exemplos Práticos & Aplicações no Mundo Real</h2>
        </div>

        <div class="grid-2col">
          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--verde-neon); margin-bottom: 0.5rem;">🚗 Luz de Cortesia Automotiva</h4>
            <p style="font-size: 0.88rem; color: var(--texto-sub);">Ao fechar a porta do carro, a lâmpada do teto não apaga abruptamente. Um circuito RC descarrega a tensão armazenada lentamente através do transistor acionador, criando um suave efeito *fade-out* (esmaecimento).</p>
          </div>

          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--azul-accent); margin-bottom: 0.5rem;">🔘 Filtro Anti-Repique (Debounce)</h4>
            <p style="font-size: 0.88rem; color: var(--texto-sub);">Botoeiras mecânicas geram centenas de faíscas e ruídos rápidos ao serem pressionadas. Um pequeno filtro RC absorve esses picos de tensão, garantindo que o microcontrolador leia um único pulso limpo.</p>
          </div>

          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--amarelo); margin-bottom: 0.5rem;">⏱️ Temporizador com CI NE555</h4>
            <p style="font-size: 0.88rem; color: var(--texto-sub);">O lendário Circuito Integrado 555 utiliza a carga e descarga do resistor e capacitor conectados aos seus pinos de disparo e limiar para gerar pulsos de clock e temporizações de precisão.</p>
          </div>

          <div style="background-color: #0F172A; padding: 1.25rem; border-radius: 8px; border: 1px solid var(--border);">
            <h4 style="color: var(--roxo-accent); margin-bottom: 0.5rem;">📻 Filtros Passivos de Áudio</h4>
            <p style="font-size: 0.88rem; color: var(--texto-sub);">A combinação de R e C também atua como filtro passa-baixas ou passa-altas, atenuando frequências indesejadas e ruídos de alta frequência em equipamentos de som.</p>
          </div>
        </div>
      </article>

      <!-- SEÇÃO 6: RESUMO PARA O CADERNO -->
      <article class="section-card" id="resumo">
        <div class="notebook-summary">
          <h3>📝 Resumo para Copiar no Caderno</h3>
          <ul class="notebook-list">
            <li><strong>Circuito RC de Temporização:</strong> Formado pela associação de um Resistor (R) e um Capacitor (C) para controlar o tempo de resposta do circuito.</li>
            <li><strong>Fórmula Fundamental:</strong> &tau; = R &times; C (Tau em Segundos, Resistance em &Omega;, Capacitance em Farads).</li>
            <li><strong>Valor de 1 Tau (1&tau;):</strong> Tempo para atingir 63,2% da tensão de carga (ou cair para 36,8% na descarga).</li>
            <li><strong>Regime Permanente (5&tau;):</strong> O capacitor é considerado 100% carregado ou totalmente descarregado após 5 Taus.</li>
            <li><strong>Aplicações Chave:</strong> Filtros anti-ruído (Debounce), esmaecimento de LEDs, circuitos de reset e bases de tempo com CI NE555.</li>
          </ul>
        </div>
      </article>

      <!-- SEÇÃO 7: QUIZ DE FIXAÇÃO INTERATIVO -->
      <article class="section-card" id="quiz">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 11l3 3L22 4"/><path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11"/></svg>
          </div>
          <h2 class="section-title">7. Quiz de Fixação</h2>
        </div>

        <div class="quiz-container">

          <!-- PERGUNTA 1 -->
          <div class="quiz-question-card" data-q="1">
            <div class="quiz-question-text">1. Qual é a porcentagem aproximada de carga que um capacitor atinge no intervalo exato de 1 Tau (&tau;)?</div>
            <div class="quiz-options">
              <label class="quiz-option"><input type="radio" name="q1" value="a"> A) 50,0%</label>
              <label class="quiz-option"><input type="radio" name="q1" value="b"> B) 63,2%</label>
              <label class="quiz-option"><input type="radio" name="q1" value="c"> C) 99,3%</label>
              <label class="quiz-option"><input type="radio" name="q1" value="d"> D) 100%</label>
            </div>
            <div class="quiz-feedback" id="fb-q1"></div>
          </div>

          <!-- PERGUNTA 2 -->
          <div class="quiz-question-card" data-q="2">
            <div class="quiz-question-text">2. Se um resistor de 10 k&Omega; (10.000 &Omega;) está em série com um capacitor de 100 &mu;F (0,0001 F), qual é o tempo de 1 &tau;?</div>
            <div class="quiz-options">
              <label class="quiz-option"><input type="radio" name="q2" value="a"> A) 0,1 segundos</label>
              <label class="quiz-option"><input type="radio" name="q2" value="b"> B) 1,0 segundo</label>
              <label class="quiz-option"><input type="radio" name="q2" value="c"> C) 10 segundos</label>
              <label class="quiz-option"><input type="radio" name="q2" value="d"> D) 5,0 segundos</label>
            </div>
            <div class="quiz-feedback" id="fb-q2"></div>
          </div>

          <!-- PERGUNTA 3 -->
          <div class="quiz-question-card" data-q="3">
            <div class="quiz-question-text">3. Quantos Taus (&tau;) são necessários para que o circuito estabilize completamente (alcançar ~100% da tensão)?</div>
            <div class="quiz-options">
              <label class="quiz-option"><input type="radio" name="q3" value="a"> A) 1 Tau</label>
              <label class="quiz-option"><input type="radio" name="q3" value="b"> B) 3 Taus</label>
              <label class="quiz-option"><input type="radio" name="q3" value="c"> C) 5 Taus</label>
              <label class="quiz-option"><input type="radio" name="q3" value="d"> D) 10 Taus</label>
            </div>
            <div class="quiz-feedback" id="fb-q3"></div>
          </div>

          <!-- PERGUNTA 4 -->
          <div class="quiz-question-card" data-q="4">
            <div class="quiz-question-text">4. Qual é a principal função de um circuito RC em uma chave mecânica (botão push-button)?</div>
            <div class="quiz-options">
              <label class="quiz-option"><input type="radio" name="q4" value="a"> A) Aumentar a tensão para o dobro</label>
              <label class="quiz-option"><input type="radio" name="q4" value="b"> B) Eliminar ruídos e faíscas de contato (Filtro Debounce)</label>
              <label class="quiz-option"><input type="radio" name="q4" value="c"> C) Transformar corrente contínua em alternada</label>
              <label class="quiz-option"><input type="radio" name="q4" value="d"> D) Servir como fusível contra curto-circuito</label>
            </div>
            <div class="quiz-feedback" id="fb-q4"></div>
          </div>

          <!-- BOTÕES E PONTUAÇÃO -->
          <div class="quiz-actions">
            <button class="btn-cta" id="btn-submit-quiz">Validar Respostas</button>
            <div class="quiz-score-display" id="quiz-score">Pontuação: - / 4</div>
          </div>

        </div>
      </article>

      <!-- SEÇÃO 8: REFERÊNCIAS BIBLIOGRÁFICAS -->
      <article class="section-card" id="referencias">
        <div class="section-header">
          <div class="section-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/></svg>
          </div>
          <h2 class="section-title">8. Referências Bibliográficas & Recursos</h2>
        </div>

        <ul style="list-style: none; display: flex; flex-direction: column; gap: 0.8rem; font-size: 0.9rem; color: var(--texto-sub);">
          <li style="padding-left: 1.2rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--verde-neon);">📚</span>
            <strong>BOYLESTAD, Robert L.</strong> <em>Introdução à Análise de Circuitos</em>. 13ª ed. São Paulo: Pearson, 2019.
          </li>
          <li style="padding-left: 1.2rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--verde-neon);">📚</span>
            <strong>SEDRA, Adel S.; SMITH, Kenneth C.</strong> <em>Microeletrônica</em>. 5ª ed. São Paulo: Pearson, 2007.
          </li>
          <li style="padding-left: 1.2rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--verde-neon);">📚</span>
            <strong>MALVINO, Albert; BATES, David J.</strong> <em>Eletrônica: Volume 1</em>. 8ª ed. Porto Alegre: AMGH, 2016.
          </li>
          <li style="padding-left: 1.2rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--verde-neon);">🎨</span>
            <strong>Ilustrações & Diagramas:</strong> SVG e gráficos Canvas produzidos digitalmente pela dupla do projeto.
          </li>
        </ul>
      </article>

    </main>
  </div>

  <!-- ==========================================================================
       RODAPÉ / FOOTER COMPLETO
       ========================================================================== -->
  <footer class="footer" id="contato">
    <div class="footer-grid">
      <div class="footer-brand">
        <h3>⚡ DEE Portal Educacional</h3>
        <p>Desenvolvido como projeto prático para abrigar conteúdos didáticos interativos do curso de Elétrica e Eletrônica do Departamento de Elétrica e Eletrônica.</p>
      </div>

      <div class="footer-col">
        <h4>Navegação</h4>
        <ul>
          <li><a href="#introducao">Introdução</a></li>
          <li><a href="#teoria">Teoria</a></li>
          <li><a href="#simulador">Simulador RC</a></li>
          <li><a href="#quiz">Quiz</a></li>
        </ul>
      </div>

      <div class="footer-col">
        <h4>Institucional</h4>
        <ul>
          <li><a href="#">Quem Somos</a></li>
          <li><a href="#">Políticas de Privacidade</a></li>
          <li><a href="#">Termos de Uso</a></li>
          <li><a href="#">Mapa do Site</a></li>
        </ul>
      </div>

      <div class="footer-col">
        <h4>Contato & Dados</h4>
        <ul>
          <li>📧 suporte@deeportal.edu.br</li>
          <li>📞 (51) 3714-7000</li>
          <li>🏢 Lajeado - RS, Brasil</li>
          <li>📄 CNPJ: 00.000.000/0001-00</li>
        </ul>
      </div>
    </div>

    <div class="footer-bottom">
      <div>&copy; 2026 DEE Portal Educacional. Todos os direitos reservados.</div>
      <div>Autores: <strong>Arthur Ruschel & Júlio César</strong> | Professor: <strong>Edson Funke</strong></div>
    </div>
  </footer>

  <!-- ==========================================================================
       JAVASCRIPT / LÓGICA E INTERATIVIDADE COMPLETA
       ========================================================================== -->
  <script>
    document.addEventListener('DOMContentLoaded', () => {

      /* ==========================================================================
         1. LÓGICA DO SIMULADOR CANAVAS DE CARGA/DESCARGA RC
         ========================================================================== */
      const rangeR = document.getElementById('range-r');
      const rangeC = document.getElementById('range-c');
      const rangeV = document.getElementById('range-v');

      const valR = document.getElementById('val-r');
      const valC = document.getElementById('val-c');
      const valV = document.getElementById('val-v');

      const statTau = document.getElementById('stat-tau');
      const stat5Tau = document.getElementById('stat-5tau');
      const statVc = document.getElementById('stat-vc');

      const btnCharge = document.getElementById('btn-charge');
      const btnDischarge = document.getElementById('btn-discharge');
      const btnReset = document.getElementById('btn-reset');

      const canvas = document.getElementById('rc-canvas');
      const ctx = canvas.getContext('2d');

      let R = parseFloat(rangeR.value) * 1000; // em Ohms
      let C = parseFloat(rangeC.value) * 1e-6; // em Farads
      let Vin = parseFloat(rangeV.value);       // em Volts

      let tau = (R * C);
      let time = 0;
      let isSimulating = false;
      let simMode = 'charge'; // 'charge' ou 'discharge'
      let historyPoints = [];
      let animationFrameId = null;

      // Ajusta resolução do canvas para alta definição
      function resizeCanvas() {
        const rect = canvas.parentElement.getBoundingClientRect();
        canvas.width = rect.width;
        canvas.height = rect.height;
        drawGraph();
      }

      window.addEventListener('resize', resizeCanvas);

      function updateParameters() {
        R = parseFloat(rangeR.value) * 1000;
        C = parseFloat(rangeC.value) * 1e-6;
        Vin = parseFloat(rangeV.value);

        valR.innerHTML = `${rangeR.value} k&Omega;`;
        valC.innerHTML = `${rangeC.value} &mu;F`;
        valV.innerHTML = `${rangeV.value} V`;

        tau = R * C;
        statTau.textContent = `${tau.toFixed(2)} s`;
        stat5Tau.textContent = `${(tau * 5).toFixed(2)} s`;

        if (!isSimulating) {
          drawGraph();
        }
      }

      rangeR.addEventListener('input', updateParameters);
      rangeC.addEventListener('input', updateParameters);
      rangeV.addEventListener('input', updateParameters);

      function calculateVc(t) {
        if (simMode === 'charge') {
          return Vin * (1 - Math.exp(-t / tau));
        } else {
          return Vin * Math.exp(-t / tau);
        }
      }

      function drawGraph() {
        const w = canvas.width;
        const h = canvas.height;
        const padding = 40;

        ctx.clearRect(0, 0, w, h);

        // Grade de Fundo
        ctx.strokeStyle = '#1E293B';
        ctx.lineWidth = 1;

        for (let x = padding; x < w; x += 40) {
          ctx.beginPath();
          ctx.moveTo(x, 0);
          ctx.lineTo(x, h - padding);
          ctx.stroke();
        }

        for (let y = 0; y < h - padding; y += 30) {
          ctx.beginPath();
          ctx.moveTo(padding, y);
          ctx.lineTo(w, y);
          ctx.stroke();
        }

        // Eixos
        ctx.strokeStyle = '#334155';
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.moveTo(padding, 10);
        ctx.lineTo(padding, h - padding);
        ctx.lineTo(w - 10, h - padding);
        ctx.stroke();

        // Rótulos do Eixo
        ctx.fillStyle = '#64748B';
        ctx.font = '10px monospace';
        ctx.fillText('0V', 15, h - padding);
        ctx.fillText(`${Vin}V`, 15, 20);
        ctx.fillText('Tempo (s)', w - 60, h - 15);

        // Curva
        if (historyPoints.length > 1) {
          ctx.strokeStyle = simMode === 'charge' ? '#00E676' : '#38BDF8';
          ctx.lineWidth = 3;
          ctx.beginPath();

          const maxTime = Math.max(tau * 5, 0.1);

          for (let i = 0; i < historyPoints.length; i++) {
            const pt = historyPoints[i];
            const px = padding + (pt.t / maxTime) * (w - padding - 20);
            const py = (h - padding) - (pt.v / Vin) * (h - padding - 30);

            if (i === 0) ctx.moveTo(px, py);
            else ctx.lineTo(px, py);
          }
          ctx.stroke();

          // Ponto Atual
          const lastPt = historyPoints[historyPoints.length - 1];
          const curX = padding + (lastPt.t / maxTime) * (w - padding - 20);
          const curY = (h - padding) - (lastPt.v / Vin) * (h - padding - 30);

          ctx.fillStyle = '#FACC15';
          ctx.beginPath();
          ctx.arc(curX, curY, 6, 0, Math.PI * 2);
          ctx.fill();

          statVc.textContent = `${lastPt.v.toFixed(2)} V`;
        }
      }

      function stepSimulation() {
        if (!isSimulating) return;

        time += tau / 30; // Incremento de tempo suave
        const currentVc = calculateVc(time);

        historyPoints.push({ t: time, v: currentVc });

        drawGraph();

        if (time >= tau * 5) {
          isSimulating = false;
          return;
        }

        animationFrameId = requestAnimationFrame(stepSimulation);
      }

      btnCharge.addEventListener('click', () => {
        cancelAnimationFrame(animationFrameId);
        simMode = 'charge';
        time = 0;
        historyPoints = [{ t: 0, v: 0 }];
        isSimulating = true;
        stepSimulation();
      });

      btnDischarge.addEventListener('click', () => {
        cancelAnimationFrame(animationFrameId);
        simMode = 'discharge';
        time = 0;
        historyPoints = [{ t: 0, v: Vin }];
        isSimulating = true;
        stepSimulation();
      });

      btnReset.addEventListener('click', () => {
        cancelAnimationFrame(animationFrameId);
        isSimulating = false;
        time = 0;
        historyPoints = [];
        statVc.textContent = '0.00 V';
        drawGraph();
      });

      resizeCanvas();
      updateParameters();

      /* ==========================================================================
         2. LÓGICA DO QUIZ DE FIXAÇÃO
         ========================================================================== */
      const btnSubmitQuiz = document.getElementById('btn-submit-quiz');
      const quizScoreDisplay = document.getElementById('quiz-score');

      const correctAnswers = {
        q1: { ans: 'b', exp: 'Correto! Em 1 Tau, a tensão no capacitor atinge exatos 63,2% da tensão da fonte.' },
        q2: { ans: 'b', exp: 'Exato! Tau = 10.000 Ohms * 0,0001 Farads = 1,0 segundo.' },
        q3: { ans: 'c', exp: 'Correto! Após 5 Taus o capacitor atinge 99,3% da carga, sendo considerado totalmente carregado.' },
        q4: { ans: 'b', exp: 'Perfeito! O filtro Debounce absorve os repiques elétricos mecânicos da chave.' }
      };

      btnSubmitQuiz.addEventListener('click', () => {
        let score = 0;

        for (let qNum = 1; qNum <= 4; qNum++) {
          const selected = document.querySelector(`input[name="q${qNum}"]:checked`);
          const feedbackDiv = document.getElementById(`fb-q${qNum}`);
          const qData = correctAnswers[`q${qNum}`];

          // Reseta classes nos labels
          const options = document.querySelectorAll(`input[name="q${qNum}"]`);
          options.forEach(opt => {
            opt.parentElement.classList.remove('correct', 'incorrect');
          });

          if (selected) {
            if (selected.value === qData.ans) {
              score++;
              selected.parentElement.classList.add('correct');
              feedbackDiv.className = 'quiz-feedback show-correct';
              feedbackDiv.textContent = qData.exp;
            } else {
              selected.parentElement.classList.add('incorrect');
              feedbackDiv.className = 'quiz-feedback show-incorrect';
              feedbackDiv.textContent = `Incorreto. A resposta certa é a opção ${qData.ans.toUpperCase()}.`;
            }
          } else {
            feedbackDiv.className = 'quiz-feedback show-incorrect';
            feedbackDiv.textContent = 'Por favor, selecione uma alternativa.';
          }
        }

        quizScoreDisplay.textContent = `Pontuação: ${score} / 4`;
      });

      /* ==========================================================================
         3. DESTAQUE DINÂMICO NO MENU LATERAL CONFORME A ROLAGEM (SCROLL)
         ========================================================================== */
      const sections = document.querySelectorAll('article.section-card, section.hero-banner');
      const navLinks = document.querySelectorAll('.sidebar-menu a');

      window.addEventListener('scroll', () => {
        let currentSectionId = '';

        sections.forEach(section => {
          const sectionTop = section.offsetTop - 120;
          if (window.scrollY >= sectionTop) {
            currentSectionId = section.getAttribute('id');
          }
        });

        navLinks.forEach(link => {
          link.classList.remove('active');
          if (link.getAttribute('href') === `#${currentSectionId}`) {
            link.classList.add('active');
          }
        });
      });

    });
  </script>
</body>
</html>
