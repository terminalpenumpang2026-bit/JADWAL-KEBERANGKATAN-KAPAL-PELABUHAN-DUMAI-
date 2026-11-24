<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Jadwal Keberangkatan Kapal - Pelabuhan Dumai</title>
  <style>
    :root {
      --primary: #0f4c81;
      --primary-dark: #093256;
      --accent: #00a8cc;
      --bg: #f1f5f9;
      --card-bg: #ffffff;
      --text-main: #0f172a;
      --text-muted: #64748b;
      --border: #e2e8f0;
      --row-hover: #f8fafc;
      --badge-ok-bg: #dcfce7;
      --badge-ok-text: #15803d;
      --badge-warn-bg: #fee2e2;
      --badge-warn-text: #b91c1c;
      --badge-info-bg: #e0f2fe;
      --badge-info-text: #0369a1;
      --badge-neutral-bg: #f1f5f9;
      --badge-neutral-text: #475569;
    }

    body.dark-mode {
      --primary: #38bdf8;
      --primary-dark: #0284c7;
      --accent: #22d3ee;
      --bg: #070d19;
      --card-bg: #111b2e;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --border: #24344d;
      --row-hover: #18253d;
      --badge-ok-bg: rgba(74, 222, 128, 0.16);
      --badge-ok-text: #4ade80;
      --badge-warn-bg: rgba(248, 113, 113, 0.16);
      --badge-warn-text: #f87171;
      --badge-info-bg: rgba(56, 189, 248, 0.16);
      --badge-info-text: #38bdf8;
      --badge-neutral-bg: rgba(148, 163, 184, 0.16);
      --badge-neutral-text: #cbd5e1;
    }

    body.dark-mode .ticker-wrap {
      background: #040811;
      border-bottom-color: rgba(148, 163, 184, 0.16);
    }

    body.dark-mode .header-banner-box {
      background: linear-gradient(135deg, #061326, #0f294a);
      border: 1px solid rgba(148, 163, 184, 0.22);
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.35);
    }

    body.dark-mode .summary-card,
    body.dark-mode .controls-bar,
    body.dark-mode .table-card,
    body.dark-mode .note-box {
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.35);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text-main);
      line-height: 1.4;
      transition: background-color 0.25s, color 0.25s;
      overflow-x: hidden;
      min-height: 100dvh;
      width: 100vw;
      max-width: 100vw;
      display: flex;
      flex-direction: column;
    }

    /* Mode layar penuh penuh-lebar & penuh-tinggi tanpa ruang kosong samping/bawah */
    :fullscreen,
    ::backdrop {
      background-color: var(--bg);
      width: 100vw;
      height: 100dvh;
      overflow-x: hidden;
      overflow-y: auto;
    }

    body.pseudo-fullscreen {
      position: fixed;
      inset: 0;
      width: 100vw;
      height: 100dvh;
      z-index: 99990;
      overflow-y: auto;
    }

    body.fit-screen-active {
      height: 100dvh;
      overflow-y: auto;
    }

    body.is-fullscreen .header-wrap,
    body.is-fullscreen .main-container,
    .header-wrap,
    .main-container {
      max-width: 100vw;
      width: 100%;
    }

    @media (min-width: 1536px) {
      .header-wrap,
      .main-container {
        max-width: 100vw;
      }
      .header-center h1 {
        font-size: clamp(1.5rem, 2.1vw, 2.2rem);
      }
      .summary-value {
        font-size: clamp(1.35rem, 1.75vw, 1.8rem);
      }
    }

    /* Running Text Ticker */
    .ticker-wrap {
      background: #072540;
      color: #f8fafc;
      font-size: clamp(0.75rem, 0.9vw, 0.88rem);
      padding: 0.35rem 0;
      overflow: hidden;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      display: flex;
      align-items: center;
      flex-shrink: 0;
    }

    .ticker-label {
      background: #eab308;
      color: #0f172a;
      font-weight: 700;
      font-size: 0.75rem;
      padding: 0.2rem 0.75rem;
      margin-left: 0.75rem;
      border-radius: 4px;
      white-space: nowrap;
      z-index: 2;
    }

    .ticker-marquee {
      flex: 1;
      overflow: hidden;
      white-space: nowrap;
      margin-left: 0.75rem;
    }

    .ticker-text {
      display: inline-block;
      padding-left: 100%;
      animation: marquee 48s linear infinite;
    }

    .ticker-wrap:hover .ticker-text {
      animation-play-state: paused;
    }

    @keyframes marquee {
      0% { transform: translateX(0); }
      100% { transform: translateX(-100%); }
    }

    .inline-ticker-wrap {
      flex: 1;
      min-width: 260px;
      width: 100%;
      max-width: none;
      background: rgba(15, 76, 129, 0.18);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: clamp(0.45rem, 0.9vh, 0.78rem) clamp(0.9rem, 1.4vw, 1.4rem) clamp(0.45rem, 0.9vh, 0.78rem) clamp(0.55rem, 0.95vw, 0.85rem);
      display: flex;
      align-items: center;
      gap: clamp(0.65rem, 1.1vw, 1rem);
      overflow: hidden;
    }

    body.dark-mode .inline-ticker-wrap {
      background: rgba(56, 189, 248, 0.14);
    }

    .inline-ticker-badge {
      background: #eab308;
      color: #0f172a;
      font-weight: 800;
      font-size: clamp(0.9rem, 1.2vw, 1.2rem);
      padding: clamp(0.28rem, 0.5vh, 0.45rem) clamp(0.7rem, 1.1vw, 1rem);
      border-radius: 9px;
      white-space: nowrap;
      flex-shrink: 0;
      letter-spacing: 0.5px;
    }

    .inline-ticker-marquee {
      flex: 1;
      overflow: hidden;
      white-space: nowrap;
      text-align: center;
      font-size: clamp(1.12rem, 1.65vw, 1.7rem);
      font-weight: 700;
      line-height: 1.3;
      color: var(--text-main);
      position: relative;
    }

    .inline-ticker-text {
      display: inline-block;
      padding-left: 0;
      text-align: center;
      transition: opacity 0.35s ease, transform 0.35s ease;
    }

    .inline-ticker-text.is-fading {
      opacity: 0;
      transform: translateY(-6px);
    }

    .ticker-edit-input {
      width: clamp(160px, 22vw, 310px);
      padding: 0.26rem 0.6rem;
      border-radius: 8px;
      border: 1px solid var(--border);
      background: var(--card-bg);
      color: var(--text-main);
      font-size: 0.76rem;
      outline: none;
      transition: border-color 0.2s;
    }

    .ticker-edit-input:focus {
      border-color: var(--primary);
    }

    /* Header Penuh Lebar Layar */
    header {
      background: transparent;
      padding: clamp(0.45rem, 0.9vh, 0.85rem) 0 0;
      flex-shrink: 0;
      width: 100%;
    }

    .header-wrap {
      max-width: 100vw;
      width: 100%;
      margin: 0 auto;
      padding: 0 clamp(0.5rem, 1.2vw, 1.25rem);
    }

    .header-banner-box {
      width: 100%;
      background: linear-gradient(135deg, #0b3960, #166096);
      color: #ffffff;
      border-radius: 12px;
      border: 1px solid var(--border);
      padding: clamp(0.35rem, 0.7vh, 0.55rem) clamp(0.75rem, 1.5vw, 1.5rem) clamp(0.75rem, 1.4vh, 1.25rem);
      box-shadow: 0 4px 14px rgba(0, 0, 0, 0.08);
      position: relative;
      overflow: hidden;
    }

    .header-container {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: clamp(0.5rem, 1.2vw, 1.25rem);
      position: relative;
    }

    .header-center {
      text-align: center;
      flex: 1;
      padding-top: 0.25rem;
    }

    .header-center h1 {
      font-size: clamp(1.15rem, 1.9vw, 1.85rem);
      font-weight: 700;
      letter-spacing: 0.3px;
      margin-bottom: 0.15rem;
    }

    .header-center p {
      font-size: clamp(0.78rem, 1vw, 0.96rem);
      opacity: 0.92;
    }

    .header-meta {
      margin-top: 0.5rem;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 0.45rem;
      align-items: center;
    }

    .live-pill {
      background: rgba(255, 255, 255, 0.16);
      padding: 0.32rem 0.85rem;
      border-radius: 999px;
      font-size: 0.82rem;
      font-weight: 500;
      display: inline-flex;
      align-items: center;
      gap: 0.4rem;
    }

    .pulse-dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: #4ade80;
      box-shadow: 0 0 0 rgba(74, 222, 128, 0.7);
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0% { box-shadow: 0 0 0 0 rgba(74, 222, 128, 0.7); }
      70% { box-shadow: 0 0 0 7px rgba(74, 222, 128, 0); }
      100% { box-shadow: 0 0 0 0 rgba(74, 222, 128, 0); }
    }

    .action-btn {
      background: rgba(255, 255, 255, 0.16);
      border: 1px solid rgba(255, 255, 255, 0.3);
      color: #ffffff;
      padding: 0.32rem 0.8rem;
      border-radius: 999px;
      font-size: 0.8rem;
      cursor: pointer;
      transition: background 0.2s;
    }

    .action-btn:hover {
      background: rgba(255, 255, 255, 0.28);
    }

    .header-logo-slot {
      height: clamp(190px, 28vh, 380px);
      max-width: clamp(190px, 31vw, 440px);
      width: clamp(190px, 31vw, 440px);
      margin-top: 0;
      padding: 0;
      border-radius: 0;
      background: transparent;
      border: none;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
      z-index: 3;
      transition: width 0.25s ease, height 0.25s ease;
    }

    .header-logo-slot:empty {
      display: none;
    }

    .header-logo-slot img {
      width: 100%;
      height: 100%;
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
      background: transparent;
      filter: drop-shadow(0 2px 6px rgba(0, 0, 0, 0.28));
      display: block;
    }

    /* Main Layout memenuhi ruang vertikal & horizontal layar */
    .main-container {
      max-width: 100vw;
      width: 100%;
      flex: 1;
      display: flex;
      flex-direction: column;
      margin: clamp(0.45rem, 0.8vh, 0.75rem) auto 0;
      padding: 0 clamp(0.5rem, 1.2vw, 1.25rem) clamp(0.35rem, 0.7vh, 0.6rem);
    }

    /* Summary Grid */
    .summary-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: clamp(0.55rem, 1vw, 0.9rem);
      margin-bottom: clamp(0.5rem, 0.9vh, 0.85rem);
      align-items: stretch;
      flex-shrink: 0;
    }

    .summary-card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: clamp(0.6rem, 1.1vh, 0.95rem) clamp(0.8rem, 1.3vw, 1.15rem);
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      min-height: clamp(74px, 10vh, 106px);
      opacity: 1 !important;
      visibility: visible !important;
      transition: border-color 0.2s ease;
    }

    .summary-card:hover {
      border-color: var(--primary);
    }

    .summary-card.static-card,
    .summary-card.static-card:hover {
      transform: none !important;
      transition: none !important;
      border-color: var(--border);
      cursor: default;
      position: relative;
      z-index: 2;
    }

    .summary-label {
      font-size: clamp(0.68rem, 0.82vw, 0.78rem);
      text-transform: uppercase;
      letter-spacing: 0.5px;
      color: var(--text-main);
      font-weight: 700;
      line-height: 1.3;
      white-space: normal;
      overflow: visible;
      opacity: 1;
      visibility: visible;
      display: block;
    }

    .summary-value {
      font-size: clamp(1.1rem, 1.55vw, 1.55rem);
      font-weight: 700;
      color: var(--primary);
      margin-top: 0.2rem;
      line-height: 1.2;
      font-variant-numeric: tabular-nums;
      white-space: normal;
      overflow: visible;
      opacity: 1;
      visibility: visible;
      display: block;
    }

    .summary-sub {
      font-size: clamp(0.7rem, 0.85vw, 0.8rem);
      color: var(--text-main);
      margin-top: 0.2rem;
      line-height: 1.3;
      opacity: 0.92;
      visibility: visible;
      display: block;
      font-weight: 500;
      white-space: normal;
      overflow: visible;
    }

    @media (max-width: 1024px) {
      .summary-grid {
        grid-template-columns: repeat(3, minmax(0, 1fr));
      }
    }

    @media (max-width: 640px) {
      .summary-grid {
        grid-template-columns: 1fr;
      }
      .summary-card {
        min-height: auto;
      }
    }

    /* Sync Info Bar */
    .sync-status-bar {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      font-size: clamp(0.72rem, 0.85vw, 0.82rem);
      color: var(--text-muted);
      margin-bottom: clamp(0.35rem, 0.65vh, 0.55rem);
      padding: 0 0.25rem;
      gap: 0.5rem;
      flex-shrink: 0;
    }

    .refresh-btn {
      background: var(--card-bg);
      border: 1px solid var(--border);
      color: var(--text-main);
      padding: 0.3rem 0.75rem;
      border-radius: 8px;
      font-size: 0.78rem;
      font-weight: 600;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 0.35rem;
      transition: all 0.2s;
    }

    .refresh-btn:hover {
      border-color: var(--primary);
      color: var(--primary);
    }

    .refresh-btn:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }

    /* Table memenuhi sisa tinggi layar agar seluruh baris terlihat utuh dalam satu layar */
    .table-card {
      position: relative;
      background-color: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 4px 14px rgba(0, 0, 0, 0.04);
      flex: 1;
      display: flex;
      flex-direction: column;
      min-height: 0;
    }

    body.dark-mode .table-card {
      background-color: var(--card-bg);
    }

    .table-responsive {
      overflow-x: auto;
      overflow-y: auto;
      flex: 1;
      display: flex;
      flex-direction: column;
    }

    table {
      width: 100%;
      height: 100%;
      border-collapse: collapse;
      text-align: left;
      background: transparent;
    }

    thead {
      background: var(--bg);
      border-bottom: 2px solid var(--border);
      position: sticky;
      top: 0;
      z-index: 2;
    }

    body.dark-mode thead {
      background: #0f1a2e;
    }

    th {
      padding: var(--fit-head-py, 0.75rem) clamp(0.65rem, 1vw, 1.05rem);
      font-size: var(--fit-head-fs, clamp(0.7rem, 0.85vw, 0.82rem));
      text-transform: uppercase;
      letter-spacing: 0.5px;
      color: var(--text-muted);
      font-weight: 700;
      white-space: nowrap;
    }

    td {
      padding: var(--fit-row-py, 0.75rem) clamp(0.65rem, 1vw, 1.05rem);
      border-bottom: 1px solid var(--border);
      font-size: var(--fit-row-fs, clamp(0.8rem, 1vw, 0.98rem));
      vertical-align: middle;
    }

    tbody tr:hover {
      background: var(--row-hover);
    }

    body.dark-mode tbody tr:hover {
      background: var(--row-hover);
    }

    .ship-name {
      font-weight: 700;
      color: var(--primary);
      font-size: var(--fit-ship-fs, clamp(0.84rem, 1.05vw, 1.04rem));
    }

    .gate-pill {
      display: inline-block;
      padding: 0.2rem 0.58rem;
      border-radius: 6px;
      font-weight: 700;
      font-size: var(--fit-badge-fs, clamp(0.74rem, 0.88vw, 0.86rem));
      background: var(--badge-info-bg);
      color: var(--badge-info-text);
    }

    .status-badge {
      display: inline-block;
      padding: 0.24rem 0.68rem;
      border-radius: 999px;
      font-size: var(--fit-badge-fs, clamp(0.74rem, 0.88vw, 0.86rem));
      font-weight: 700;
      white-space: nowrap;
    }

    .status-ok { background: var(--badge-ok-bg); color: var(--badge-ok-text); }
    .status-warn { background: var(--badge-warn-bg); color: var(--badge-warn-text); }
    .status-info { background: var(--badge-info-bg); color: var(--badge-info-text); }
    .status-neutral { background: var(--badge-neutral-bg); color: var(--badge-neutral-text); }

    .empty-msg {
      text-align: center;
      padding: 2.2rem 1rem;
      color: var(--text-muted);
      display: none;
    }

    /* Operational Note Card */
    .note-box {
      margin-top: 1.25rem;
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-left: 4px solid #eab308;
      border-radius: 10px;
      padding: 1rem 1.2rem;
      font-size: 0.86rem;
      color: var(--text-main);
    }

    /* Modal Tambah Logo */
    .modal-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(15, 23, 42, 0.65);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 999;
      padding: 1rem;
    }

    .modal-backdrop.open {
      display: flex;
    }

    .modal-card {
      background: var(--card-bg);
      color: var(--text-main);
      border: 1px solid var(--border);
      border-radius: 14px;
      max-width: 440px;
      width: 100%;
      padding: 1.4rem;
      box-shadow: 0 20px 35px rgba(0, 0, 0, 0.25);
    }

    .modal-card h3 {
      margin-bottom: 0.85rem;
      font-size: 1.1rem;
    }

    .form-group {
      margin-bottom: 0.9rem;
    }

    .form-group label {
      display: block;
      font-size: 0.82rem;
      font-weight: 600;
      margin-bottom: 0.3rem;
      color: var(--text-muted);
    }

    .form-group input[type="text"],
    .form-group input[type="file"],
    .form-group textarea {
      width: 100%;
      padding: 0.5rem 0.7rem;
      border: 1px solid var(--border);
      border-radius: 8px;
      background: var(--bg);
      color: var(--text-main);
      font-size: 0.84rem;
      font-family: inherit;
    }

    .form-group textarea {
      min-height: 110px;
      resize: vertical;
      line-height: 1.45;
    }

    .form-hint {
      margin-top: 0.35rem;
      font-size: 0.75rem;
      color: var(--text-muted);
      line-height: 1.35;
    }

    .modal-actions {
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-end;
      gap: 0.5rem;
      margin-top: 1rem;
    }

    .btn-secondary, .btn-primary {
      padding: 0.48rem 0.95rem;
      border-radius: 8px;
      border: none;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
    }

    .btn-secondary {
      background: var(--border);
      color: var(--text-main);
    }

    .btn-primary {
      background: var(--primary);
      color: #ffffff;
    }

    body.dark-mode .btn-primary {
      color: #0f172a;
    }

    footer {
      text-align: center;
      padding: clamp(0.3rem, 0.6vh, 0.55rem) 0.75rem;
      font-size: clamp(0.7rem, 0.82vw, 0.8rem);
      color: var(--text-muted);
      flex-shrink: 0;
    }

    @media (max-width: 640px) {
      .header-container {
        flex-wrap: wrap;
        justify-content: center;
      }
      .header-center {
        order: -1;
        width: 100%;
        margin-bottom: 0.35rem;
        padding-top: 0;
      }
      .header-center h1 {
        font-size: 1.15rem;
      }
      .header-logo-slot {
        width: 196px;
        height: 196px;
        max-width: 196px;
        margin-top: 0;
      }
      .header-logo-slot img {
        max-width: 196px;
        max-height: 196px;
      }
    }

    @media (orientation: landscape) and (max-height: 620px) {
      .header-logo-slot {
        height: clamp(136px, 22vh, 200px);
        width: clamp(136px, 22vh, 200px);
        max-width: 200px;
      }
      .summary-card {
        min-height: 60px;
        padding: 0.45rem 0.8rem;
      }
    }
  </style>
</head>
<body class="dark-mode">

  <!-- Header -->
  <header>
    <div class="header-wrap">
      <div class="header-banner-box" id="headerBannerBox">
        <div class="header-container">
          <div class="header-logo-slot" id="headerLogoLeft"></div>

          <div class="header-center">
            <h1>JADWAL KEBERANGKATAN KAPAL PELABUHAN DUMAI</h1>
            <p>Sistem Informasi Keberangkatan &amp; Kedatangan Terminal Penumpang Pelabuhan Dumai</p>
            <div class="header-meta">
              <span class="live-pill"><span class="pulse-dot"></span> <span id="liveClock">Memuat waktu WIB...</span></span>
              <button type="button" class="action-btn" id="fullscreenToggleBtn">⛶ Layar Penuh</button>
              <button type="button" class="action-btn" id="openLogoModalBtn">🖼️ Atur Logo</button>
              <button type="button" class="action-btn" id="saveRunningTextBtn">✏️ Ubah Teks</button>
              <button type="button" class="action-btn" id="themeToggleBtn">☀️ Mode Terang</button>
            </div>
          </div>

          <div class="header-logo-slot" id="headerLogoRight"></div>
        </div>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <main class="main-container">
    <!-- Summary Cards -->
    <section class="summary-grid">
      <div class="summary-card static-card">
        <div class="summary-label">Kapal Tercatat di Papan</div>
        <div class="summary-value" id="statTableCount">3</div>
        <div class="summary-sub">Jumlah baris jadwal aktif</div>
      </div>
      <div class="summary-card static-card">
        <div class="summary-label">Status Debarkasi / Aktif</div>
        <div class="summary-value" id="statActiveCount">2</div>
        <div class="summary-sub">Kapal dalam proses layanan</div>
      </div>
      <div class="summary-card static-card">
        <div class="summary-label">Cuaca Perairan Dumai</div>
        <div class="summary-value" id="statWeather">⛅ 29°C</div>
        <div class="summary-sub" id="statWeatherDesc">Cerah Berawan • Dumai (Open-Meteo)</div>
      </div>
    </section>

    <!-- Status Sinkronisasi -->
    <div class="sync-status-bar">
      <div style="display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap; flex: 1; min-width: 0;">
        <div class="inline-ticker-wrap" id="inlineTickerWrap">
          <span class="inline-ticker-badge">INFO</span>
          <div class="inline-ticker-marquee">
            <span class="inline-ticker-text" id="inlineTickerText">Memuat informasi pelabuhan...</span>
          </div>
        </div>
      </div>
      <button type="button" class="refresh-btn" id="manualRefreshBtn">🔄 Refresh</button>
    </div>

    <!-- Tabel Jadwal -->
    <section class="table-card">
      <div class="table-responsive">
        <table>
          <thead id="scheduleTableHead">
            <tr>
              <th>Nama Kapal</th>
              <th>Destinasi</th>
              <th>EST. Datang</th>
              <th>EST. Berangkat</th>
              <th>Gate / Line</th>
              <th>Status Keberangkatan</th>
            </tr>
          </thead>
          <tbody id="scheduleTableBody"></tbody>
        </table>
      </div>
      <div class="empty-msg" id="emptyMsg">Tidak ada jadwal kapal yang sesuai dengan filter atau kata kunci pencarian.</div>
    </section>
  </main>

  <!-- Modal Atur Logo Kiri & Kanan -->
  <div class="modal-backdrop" id="logoModal">
    <div class="modal-card">
      <h3>Atur Logo Header (Kiri &amp; Kanan)</h3>
      <div class="form-group">
        <label for="leftLogoFile">Upload Logo 1 (Pojok Kiri Atas)</label>
        <input type="file" id="leftLogoFile" accept="image/*" />
      </div>
      <div class="form-group">
        <label for="leftLogoUrl">Atau Tempel URL Logo 1 (Kiri)</label>
        <input type="text" id="leftLogoUrl" placeholder="https://contoh.com/logo-kiri.png" />
      </div>
      <div class="form-group">
        <label for="rightLogoFile">Upload Logo 2 (Pojok Kanan Atas)</label>
        <input type="file" id="rightLogoFile" accept="image/*" />
      </div>
      <div class="form-group">
        <label for="rightLogoUrl">Atau Tempel URL Logo 2 (Kanan)</label>
        <input type="text" id="rightLogoUrl" placeholder="https://contoh.com/logo-kanan.png" />
      </div>
      <div class="modal-actions">
        <button type="button" class="btn-secondary" id="resetLogoBtn">Hapus Logo</button>
        <button type="button" class="btn-secondary" id="closeLogoModalBtn">Tutup</button>
        <button type="button" class="btn-primary" id="saveLogoBtn">Simpan Logo</button>
      </div>
    </div>
  </div>

  <!-- Modal Ubah Running Text -->
  <div class="modal-backdrop" id="runningTextModal">
    <div class="modal-card">
      <h3>Ubah Running Text Informasi</h3>
      <div class="form-group">
        <label for="modalRunningTextInput">Ketik Teks Berjalan (Bisa Lebih dari 1 Baris / Informasi)</label>
        <textarea id="modalRunningTextInput" rows="4" placeholder="Baris 1: Informasi keberangkatan kapal...&#10;Baris 2: Pengumuman keselamatan pelabuhan...&#10;Baris 3: Info cuaca & pasang surut..."></textarea>
        <div class="form-hint">Tekan <strong>Enter</strong> untuk menambah baris/informasi baru (lebih dari 1 teks). Setiap baris otomatis digabung menjadi satu <em>running text</em> berjalan.</div>
      </div>
      <div class="modal-actions">
        <button type="button" class="btn-secondary" id="resetRunningTextBtn">Default</button>
        <button type="button" class="btn-secondary" id="closeRunningTextModalBtn">Batal</button>
        <button type="button" class="btn-primary" id="confirmRunningTextBtn">Simpan</button>
      </div>
    </div>
  </div>

  <footer>
    &copy; 2026 Layanan Informasi Pelabuhan Dumai • Sinkronisasi Otomatis Google Sheets
  </footer>

  <script>
    (function () {
      function initDashboard() {
        try {
          var PUBLISHED_CSV_URL = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSGvYpxgf_nsfNkpd2u_FDCDTENw6PkgeBbJZWZulGIdDjsiDhzKQJO76QcR_Hp4LvARZXgBjCL1-eK/pub?gid=0&single=true&output=csv";
          var GVIZ_JSONP_BASE = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSGvYpxgf_nsfNkpd2u_FDCDTENw6PkgeBbJZWZulGIdDjsiDhzKQJO76QcR_Hp4LvARZXgBjCL1-eK/gviz/tq?gid=0";

          var state = {
            rows: [
              { no: "1", ship: "Memuat data Google Sheets...", dest: "-", arr: "-", dep: "-", gate: "-", status: "-" }
            ],
            totalText: "-",
            noteText: "",
            liveWeather: "⛅ 29°C Cerah Berawan",
            filter: "all",
            isFetching: false,
            hasLiveSheetData: false,
            lastSignature: ""
          };

          var thead = document.getElementById("scheduleTableHead");
          var tbody = document.getElementById("scheduleTableBody");
          var emptyMsg = document.getElementById("emptyMsg");
          var statTableCount = document.getElementById("statTableCount");
          var statActiveCount = document.getElementById("statActiveCount");
          var statWeather = document.getElementById("statWeather");
          var statWeatherDesc = document.getElementById("statWeatherDesc");
          var manualRefreshBtn = document.getElementById("manualRefreshBtn");
          var operationalNoteBox = document.getElementById("operationalNoteBox");
          var tickerText = document.getElementById("tickerText");
          var inlineTickerText = document.getElementById("inlineTickerText");
          var runningTextInput = document.getElementById("runningTextInput");
          var saveRunningTextBtn = document.getElementById("saveRunningTextBtn");
          var runningTextModal = document.getElementById("runningTextModal");
          var modalRunningTextInput = document.getElementById("modalRunningTextInput");
          var confirmRunningTextBtn = document.getElementById("confirmRunningTextBtn");
          var closeRunningTextModalBtn = document.getElementById("closeRunningTextModalBtn");
          var resetRunningTextBtn = document.getElementById("resetRunningTextBtn");

          var DEFAULT_RUNNING_TEXT = "";
          var runningTextItems = [];
          var runningTextIndex = 0;
          var runningTextTimer = null;

          function parseRunningTextItems(rawText) {
            var cleaned = String(rawText || "").replace(/\s+•\s+/g, "\n");
            return cleaned
              .split(/\r?\n/)
              .map(function (line) { return line.trim(); })
              .filter(function (line) { return line.length > 0; });
          }

          function formatMultiRunningText(rawText) {
            return parseRunningTextItems(rawText).join("   •   ");
          }

          function showRunningTextSlide(index) {
            if (!inlineTickerText) return;
            if (!runningTextItems.length) {
              inlineTickerText.classList.remove("is-fading");
              inlineTickerText.textContent = "";
              return;
            }
            var safeIdx = ((index % runningTextItems.length) + runningTextItems.length) % runningTextItems.length;
            runningTextIndex = safeIdx;
            inlineTickerText.classList.add("is-fading");
            setTimeout(function () {
              if (!inlineTickerText) return;
              inlineTickerText.textContent = runningTextItems[runningTextIndex];
              inlineTickerText.classList.remove("is-fading");
            }, 180);
          }

          function restartRunningTextRotation() {
            if (runningTextTimer) {
              clearInterval(runningTextTimer);
              runningTextTimer = null;
            }
            if (!inlineTickerText) return;
            if (!runningTextItems.length) {
              inlineTickerText.classList.remove("is-fading");
              inlineTickerText.textContent = "";
              return;
            }
            runningTextIndex = 0;
            inlineTickerText.classList.remove("is-fading");
            inlineTickerText.textContent = runningTextItems[0];

            if (runningTextItems.length > 1) {
              runningTextTimer = setInterval(function () {
                showRunningTextSlide(runningTextIndex + 1);
              }, 6000);
            }
          }

          function syncRunningTextDisplay(text) {
            var val = formatMultiRunningText(text);
            runningTextItems = parseRunningTextItems(text);
            if (operationalNoteBox) operationalNoteBox.textContent = val;
            if (tickerText) tickerText.textContent = val;
            restartRunningTextRotation();
          }

          var RUNNING_TEXT_STORAGE_KEY = "dumai_custom_running_text";
          var savedRunningText = localStorage.getItem(RUNNING_TEXT_STORAGE_KEY);
          if (savedRunningText && savedRunningText.trim()) {
            state.noteText = savedRunningText.trim();
          }
          if (runningTextInput) {
            runningTextInput.value = state.noteText;
          }
          if (modalRunningTextInput) {
            modalRunningTextInput.value = state.noteText;
          }
          syncRunningTextDisplay(state.noteText);

          function applyCustomRunningText(rawValue) {
            var sourceText = typeof rawValue === "string"
              ? rawValue
              : (modalRunningTextInput && runningTextModal && runningTextModal.classList.contains("open"))
                ? modalRunningTextInput.value
                : (runningTextInput ? runningTextInput.value : state.noteText);

            var formattedText = formatMultiRunningText(sourceText);
            if (!formattedText) {
              localStorage.removeItem(RUNNING_TEXT_STORAGE_KEY);
              state.noteText = DEFAULT_RUNNING_TEXT;
            } else {
              localStorage.setItem(RUNNING_TEXT_STORAGE_KEY, formattedText);
              state.noteText = formattedText;
            }

            if (runningTextInput) runningTextInput.value = state.noteText;
            if (modalRunningTextInput) {
              modalRunningTextInput.value = state.noteText.split("   •   ").join("\n");
            }
            syncRunningTextDisplay(state.noteText);
          }

          function openRunningTextModal() {
            if (!runningTextModal) return;
            if (modalRunningTextInput) {
              var currentVal = (runningTextInput && runningTextInput.value.trim())
                ? runningTextInput.value
                : state.noteText;
              modalRunningTextInput.value = currentVal.split("   •   ").join("\n");
            }
            runningTextModal.classList.add("open");
            if (modalRunningTextInput) {
              setTimeout(function () {
                modalRunningTextInput.focus();
              }, 30);
            }
          }

          function closeRunningTextModal() {
            if (runningTextModal) {
              runningTextModal.classList.remove("open");
            }
          }

          if (saveRunningTextBtn) {
            saveRunningTextBtn.addEventListener("click", openRunningTextModal);
          }
          if (confirmRunningTextBtn) {
            confirmRunningTextBtn.addEventListener("click", function () {
              applyCustomRunningText(modalRunningTextInput ? modalRunningTextInput.value : "");
              closeRunningTextModal();
            });
          }
          if (closeRunningTextModalBtn) {
            closeRunningTextModalBtn.addEventListener("click", closeRunningTextModal);
          }
          if (resetRunningTextBtn) {
            resetRunningTextBtn.addEventListener("click", function () {
              localStorage.removeItem(RUNNING_TEXT_STORAGE_KEY);
              applyCustomRunningText(DEFAULT_RUNNING_TEXT);
              closeRunningTextModal();
            });
          }
          if (runningTextModal) {
            runningTextModal.addEventListener("click", function (e) {
              if (e.target === runningTextModal) {
                closeRunningTextModal();
              }
            });
          }
          if (modalRunningTextInput) {
            modalRunningTextInput.addEventListener("keydown", function (e) {
              if ((e.ctrlKey || e.metaKey) && e.key === "Enter") {
                e.preventDefault();
                applyCustomRunningText(modalRunningTextInput.value);
                closeRunningTextModal();
              }
            });
          }
          if (runningTextInput) {
            runningTextInput.addEventListener("keydown", function (e) {
              if (e.key === "Enter") {
                e.preventDefault();
                applyCustomRunningText(runningTextInput.value);
              }
            });
          }

          function escapeHtml(str) {
            return String(str || "")
              .replace(/&/g, "&amp;")
              .replace(/</g, "&lt;")
              .replace(/>/g, "&gt;")
              .replace(/"/g, "&quot;")
              .replace(/'/g, "&#39;");
          }

          // Jam Real-time WIB
          function updateClock() {
            var clockEl = document.getElementById("liveClock");
            if (!clockEl) return;
            var now = new Date();
            var dateStr = now.toLocaleDateString("id-ID", {
              weekday: "long",
              day: "numeric",
              month: "short",
              year: "numeric"
            });
            var timeStr = now.toLocaleTimeString("id-ID", {
              hour: "2-digit",
              minute: "2-digit",
              second: "2-digit"
            });
            clockEl.textContent = dateStr + " • " + timeStr + " WIB";
          }
          updateClock();
          setInterval(updateClock, 1000);

          // Mode Fullscreen Otomatis & Responsif Sesuai Ukuran Layar
          var fullscreenToggleBtn = document.getElementById("fullscreenToggleBtn");
          var pseudoFullscreenActive = false;

          function isFullscreenActive() {
            return Boolean(
              document.fullscreenElement ||
              document.webkitFullscreenElement ||
              document.mozFullScreenElement ||
              document.msFullscreenElement ||
              pseudoFullscreenActive
            );
          }

          function applyPseudoFullscreen(enable) {
            pseudoFullscreenActive = Boolean(enable);
            document.body.classList.toggle("pseudo-fullscreen", pseudoFullscreenActive);
            syncFullscreenUi();
          }

          async function enterFullscreenMode() {
            if (isFullscreenActive()) {
              syncFullscreenUi();
              return;
            }
            var rootEl = document.documentElement;
            try {
              var req =
                rootEl.requestFullscreen ||
                rootEl.webkitRequestFullscreen ||
                rootEl.mozRequestFullScreen ||
                rootEl.msRequestFullscreen;

              if (req) {
                var promise = req.call(rootEl);
                if (promise && typeof promise.then === "function") {
                  await promise;
                }
                setTimeout(function () {
                  if (
                    !(
                      document.fullscreenElement ||
                      document.webkitFullscreenElement ||
                      document.mozFullScreenElement ||
                      document.msFullscreenElement
                    )
                  ) {
                    applyPseudoFullscreen(true);
                  }
                }, 120);
                return;
              }
            } catch (fsErr) {
              // Fallback ke mode layar penuh aplikasi bila Fullscreen API diblokir iframe/browser
            }
            applyPseudoFullscreen(true);
          }

          async function exitFullscreenMode() {
            try {
              var exitFn =
                document.exitFullscreen ||
                document.webkitExitFullscreen ||
                document.mozCancelFullScreen ||
                document.msExitFullscreen;

              if (
                exitFn &&
                (document.fullscreenElement ||
                  document.webkitFullscreenElement ||
                  document.mozFullScreenElement ||
                  document.msFullscreenElement)
              ) {
                var promise = exitFn.call(document);
                if (promise && typeof promise.then === "function") {
                  await promise;
                }
              }
            } catch (exitErr) {
              // Abaikan error keluar fullscreen
            }
            applyPseudoFullscreen(false);
          }

          function syncFullscreenUi() {
            var nativeFs = Boolean(
              document.fullscreenElement ||
              document.webkitFullscreenElement ||
              document.mozFullScreenElement ||
              document.msFullscreenElement
            );
            var active = nativeFs || pseudoFullscreenActive;
            document.body.classList.toggle("is-fullscreen", active);
            if (fullscreenToggleBtn) {
              fullscreenToggleBtn.textContent = active ? "🗗 Keluar Penuh" : "⛶ Layar Penuh";
            }
            adjustViewportFit();
          }

          // Hitung & sesuaikan skala baris tabel agar seluruh jadwal tampak utuh dalam satu layar
          function adjustViewportFit() {
            try {
              var tableCard = document.querySelector(".table-card");
              var theadEl = document.querySelector("thead");
              var rowsCount = tbody ? tbody.querySelectorAll("tr").length : 0;
              var vw = window.innerWidth || document.documentElement.clientWidth || 1280;
              var vh = window.innerHeight || document.documentElement.clientHeight || 720;

              document.body.classList.add("fit-screen-active");

              if (!tableCard || rowsCount <= 0) return;

              var cardRect = tableCard.getBoundingClientRect();
              var headHeight = theadEl ? theadEl.getBoundingClientRect().height : 42;
              var availableBodyHeight = Math.max(120, vh - cardRect.top - headHeight - 30);
              var idealRowHeight = availableBodyHeight / rowsCount;

              // Batasi padding & font-size vertikal agar semua baris muat tanpa terpotong maupun terlalu sempit
              var rowPadY = Math.max(4, Math.min(22, Math.round((idealRowHeight - 24) / 2)));
              var headPadY = Math.max(5, Math.min(14, Math.round(rowPadY * 0.72)));

              var scaleFactor = Math.max(0.82, Math.min(1.38, Math.sqrt((vw * vh) / (1366 * 768))));
              var rowFontSize = Math.max(12, Math.min(22, (14.5 * scaleFactor))).toFixed(1) + "px";
              var shipFontSize = Math.max(12.5, Math.min(23, (15.5 * scaleFactor))).toFixed(1) + "px";
              var headFontSize = Math.max(11, Math.min(17, (12.5 * scaleFactor))).toFixed(1) + "px";
              var badgeFontSize = Math.max(11, Math.min(17, (12.5 * scaleFactor))).toFixed(1) + "px";

              tableCard.style.setProperty("--fit-row-py", rowPadY + "px");
              tableCard.style.setProperty("--fit-head-py", headPadY + "px");
              tableCard.style.setProperty("--fit-row-fs", rowFontSize);
              tableCard.style.setProperty("--fit-ship-fs", shipFontSize);
              tableCard.style.setProperty("--fit-head-fs", headFontSize);
              tableCard.style.setProperty("--fit-badge-fs", badgeFontSize);
            } catch (fitErr) {
              // Hindari gangguan jika pengukuran layout belum siap
            }
          }

          if (fullscreenToggleBtn) {
            fullscreenToggleBtn.addEventListener("click", function (e) {
              e.preventDefault();
              if (isFullscreenActive()) {
                exitFullscreenMode();
              } else {
                enterFullscreenMode();
              }
            });
          }

          ["fullscreenchange", "webkitfullscreenchange", "mozfullscreenchange", "MSFullscreenChange"].forEach(function (evtName) {
            document.addEventListener(evtName, function () {
              var nativeFs = Boolean(
                document.fullscreenElement ||
                document.webkitFullscreenElement ||
                document.mozFullScreenElement ||
                document.msFullscreenElement
              );
              if (nativeFs) {
                pseudoFullscreenActive = false;
                document.body.classList.remove("pseudo-fullscreen");
              }
              syncFullscreenUi();
            });
          });

          // Aktifkan fullscreen saat interaksi pertama jika browser memblokir saat load
          var unlockFullscreenOnFirstGesture = function () {
            if (!isFullscreenActive()) {
              enterFullscreenMode();
            }
            window.removeEventListener("pointerdown", unlockFullscreenOnFirstGesture);
            window.removeEventListener("keydown", unlockFullscreenOnFirstGesture);
          };
          window.addEventListener("pointerdown", unlockFullscreenOnFirstGesture, { once: true });
          window.addEventListener("keydown", unlockFullscreenOnFirstGesture, { once: true });
          window.addEventListener("resize", function () {
            syncFullscreenUi();
            adjustViewportFit();
          });
          window.addEventListener("orientationchange", function () {
            setTimeout(function () {
              syncFullscreenUi();
              adjustViewportFit();
            }, 120);
          });
          syncFullscreenUi();

          // Dark Mode Toggle (Default: Mode Gelap)
          var themeToggleBtn = document.getElementById("themeToggleBtn");
          var savedTheme = localStorage.getItem("dumai_theme");
          if (savedTheme === "light") {
            document.body.classList.remove("dark-mode");
          } else {
            document.body.classList.add("dark-mode");
          }

          function updateThemeButtonLabel() {
            if (!themeToggleBtn) return;
            var isDark = document.body.classList.contains("dark-mode");
            themeToggleBtn.textContent = isDark ? "☀️ Mode Terang" : "🌙 Mode Gelap";
          }
          updateThemeButtonLabel();

          if (themeToggleBtn) {
            themeToggleBtn.addEventListener("click", function () {
              document.body.classList.toggle("dark-mode");
              var isDark = document.body.classList.contains("dark-mode");
              localStorage.setItem("dumai_theme", isDark ? "dark" : "light");
              updateThemeButtonLabel();
            });
          }

          // Pengaturan Logo Header
          var logoModal = document.getElementById("logoModal");
          var headerLogoLeft = document.getElementById("headerLogoLeft");
          var headerLogoRight = document.getElementById("headerLogoRight");
          var leftLogoUrlInput = document.getElementById("leftLogoUrl");
          var rightLogoUrlInput = document.getElementById("rightLogoUrl");
          var leftLogoFileInput = document.getElementById("leftLogoFile");
          var rightLogoFileInput = document.getElementById("rightLogoFile");

          // Hapus latar belakang hitam (mis. pada logo Danantara) via Canvas menjadi PNG transparan
          function removeBlackBackground(src) {
            return new Promise(function (resolve) {
              if (!src) {
                resolve("");
                return;
              }
              var img = new Image();
              img.crossOrigin = "anonymous";
              img.onload = function () {
                try {
                  var canvas = document.createElement("canvas");
                  canvas.width = img.naturalWidth || img.width;
                  canvas.height = img.naturalHeight || img.height;
                  var ctx = canvas.getContext("2d");
                  if (!ctx || !canvas.width || !canvas.height) {
                    resolve(src);
                    return;
                  }
                  ctx.drawImage(img, 0, 0);
                  var imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                  var data = imageData.data;

                  for (var i = 0; i < data.length; i += 4) {
                    var r = data[i];
                    var g = data[i + 1];
                    var b = data[i + 2];
                    var maxCh = Math.max(r, g, b);

                    // Piksel hitam pekat dijadikan transparan penuh; tepian gelap dihaluskan (anti-aliasing)
                    if (maxCh <= 28) {
                      data[i + 3] = 0;
                    } else if (maxCh <= 65) {
                      var factor = (maxCh - 28) / (65 - 28);
                      data[i + 3] = Math.round(data[i + 3] * factor);
                    }
                  }

                  ctx.putImageData(imageData, 0, 0);
                  resolve(canvas.toDataURL("image/png"));
                } catch (e) {
                  // Fallback jika gambar eksternal memblokir CORS canvas
                  resolve(src);
                }
              };
              img.onerror = function () {
                resolve(src);
              };
              img.src = src;
            });
          }

          async function applyLogos() {
            var leftSrc = localStorage.getItem("dumai_logo_left") || "";
            var rightSrc = localStorage.getItem("dumai_logo_right") || "";

            if (leftLogoUrlInput) leftLogoUrlInput.value = leftSrc.indexOf("data:") === 0 ? "" : leftSrc;
            if (rightLogoUrlInput) rightLogoUrlInput.value = rightSrc.indexOf("data:") === 0 ? "" : rightSrc;

            var cleanLeft = leftSrc ? await removeBlackBackground(leftSrc) : "";
            var cleanRight = rightSrc ? await removeBlackBackground(rightSrc) : "";

            if (headerLogoLeft) {
              headerLogoLeft.innerHTML = cleanLeft
                ? '<img src="' + escapeHtml(cleanLeft) + '" alt="Logo 1" style="mix-blend-mode: ' + (cleanLeft.indexOf("data:image/png") === 0 ? "normal" : "screen") + ';" onerror="this.remove()" />'
                : "";
            }
            if (headerLogoRight) {
              headerLogoRight.innerHTML = cleanRight
                ? '<img src="' + escapeHtml(cleanRight) + '" alt="Logo 2" style="mix-blend-mode: ' + (cleanRight.indexOf("data:image/png") === 0 ? "normal" : "screen") + ';" onerror="this.remove()" />'
                : "";
            }
          }

          function readFileAsDataUrl(file) {
            return new Promise(function (resolve) {
              if (!file) {
                resolve("");
                return;
              }
              var reader = new FileReader();
              reader.onload = function (e) {
                resolve((e.target && e.target.result) || "");
              };
              reader.onerror = function () {
                resolve("");
              };
              reader.readAsDataURL(file);
            });
          }

          var openLogoBtn = document.getElementById("openLogoModalBtn");
          var closeLogoBtn = document.getElementById("closeLogoModalBtn");
          var resetLogoBtn = document.getElementById("resetLogoBtn");
          var saveLogoBtn = document.getElementById("saveLogoBtn");

          if (openLogoBtn && logoModal) {
            openLogoBtn.addEventListener("click", function () {
              logoModal.classList.add("open");
            });
          }
          if (closeLogoBtn && logoModal) {
            closeLogoBtn.addEventListener("click", function () {
              logoModal.classList.remove("open");
            });
          }
          if (logoModal) {
            logoModal.addEventListener("click", function (e) {
              if (e.target === logoModal) logoModal.classList.remove("open");
            });
          }
          if (resetLogoBtn) {
            resetLogoBtn.addEventListener("click", function () {
              localStorage.removeItem("dumai_logo_left");
              localStorage.removeItem("dumai_logo_right");
              if (leftLogoFileInput) leftLogoFileInput.value = "";
              if (rightLogoFileInput) rightLogoFileInput.value = "";
              if (leftLogoUrlInput) leftLogoUrlInput.value = "";
              if (rightLogoUrlInput) rightLogoUrlInput.value = "";
              applyLogos();
            });
          }
          if (saveLogoBtn && logoModal) {
            saveLogoBtn.addEventListener("click", async function () {
              var leftFile = leftLogoFileInput && leftLogoFileInput.files && leftLogoFileInput.files[0];
              var rightFile = rightLogoFileInput && rightLogoFileInput.files && rightLogoFileInput.files[0];

              var leftData = await readFileAsDataUrl(leftFile);
              var rightData = await readFileAsDataUrl(rightFile);

              var rawLeft = leftData || (leftLogoUrlInput ? leftLogoUrlInput.value.trim() : "");
              var rawRight = rightData || (rightLogoUrlInput ? rightLogoUrlInput.value.trim() : "");

              var finalLeft = rawLeft ? await removeBlackBackground(rawLeft) : "";
              var finalRight = rawRight ? await removeBlackBackground(rawRight) : "";

              if (finalLeft) localStorage.setItem("dumai_logo_left", finalLeft);
              else localStorage.removeItem("dumai_logo_left");

              if (finalRight) localStorage.setItem("dumai_logo_right", finalRight);
              else localStorage.removeItem("dumai_logo_right");

              await applyLogos();
              logoModal.classList.remove("open");
            });
          }

          localStorage.removeItem("dumai_table_bg");
          applyLogos();

          // Klasifikasi Badge Status
          function getStatusInfo(statusText) {
            var s = String(statusText || "").toLowerCase();
            if (s.indexOf("tunda") !== -1 || s.indexOf("batal") !== -1 || s.indexOf("delay") !== -1) {
              return { cls: "status-warn", category: "tunda" };
            }
            if (s.indexOf("debarkasi") !== -1 || s.indexOf("sandar") !== -1 || s.indexOf("tiba") !== -1) {
              return { cls: "status-info", category: "debarkasi" };
            }
            if (s.indexOf("boarding") !== -1 || s.indexOf("berangkat") !== -1 || s.indexOf("on time") !== -1 || s.indexOf("sesuai") !== -1) {
              return { cls: "status-ok", category: "boarding" };
            }
            return { cls: "status-neutral", category: "other" };
          }

          // Render Seluruh Kartu Ringkasan & Tabel
          function renderAll() {
            try {
              var filtered = state.rows;

              if (statTableCount) statTableCount.textContent = String(state.rows.length);

              var activeCount = state.rows.filter(function (r) {
                var cat = getStatusInfo(r.status).category;
                return cat === "debarkasi" || cat === "boarding";
              }).length;
              if (statActiveCount) statActiveCount.textContent = String(activeCount);

              if (operationalNoteBox) operationalNoteBox.textContent = state.noteText;
              if (tickerText) tickerText.textContent = state.noteText;
              if (inlineTickerText && !runningTextItems.length) {
                inlineTickerText.textContent = state.noteText;
              }

              if (!tbody) return;
              tbody.innerHTML = "";

              if (filtered.length === 0) {
                if (emptyMsg) emptyMsg.style.display = "block";
                adjustViewportFit();
                return;
              }
              if (emptyMsg) emptyMsg.style.display = "none";

              filtered.forEach(function (row) {
                var info = getStatusInfo(row.status);
                var tr = document.createElement("tr");
                tr.innerHTML =
                  '<td><div class="ship-name">' + escapeHtml(row.ship) + "</div></td>" +
                  "<td>" + escapeHtml(row.dest) + "</td>" +
                  "<td>" + escapeHtml(row.arr) + "</td>" +
                  "<td>" + escapeHtml(row.dep) + "</td>" +
                  '<td><span class="gate-pill">' + escapeHtml(row.gate) + "</span></td>" +
                  '<td><span class="status-badge ' + info.cls + '">' + escapeHtml(row.status) + "</span></td>";
                tbody.appendChild(tr);
              });

              requestAnimationFrame(adjustViewportFit);
            } catch (renderErr) {
              // Hindari kegagalan render keseluruhan halaman
            }
          }

          // Parser CSV RFC-4180
          function parseCsv(text) {
            var rows = [];
            var row = [];
            var cur = "";
            var inQuotes = false;

            for (var i = 0; i < text.length; i++) {
              var ch = text[i];
              var next = text[i + 1];

              if (inQuotes) {
                if (ch === '"' && next === '"') {
                  cur += '"';
                  i++;
                } else if (ch === '"') {
                  inQuotes = false;
                } else {
                  cur += ch;
                }
              } else {
                if (ch === '"') {
                  inQuotes = true;
                } else if (ch === ",") {
                  row.push(cur.trim());
                  cur = "";
                } else if (ch === "\r" && next === "\n") {
                  row.push(cur.trim());
                  rows.push(row);
                  row = [];
                  cur = "";
                  i++;
                } else if (ch === "\n" || ch === "\r") {
                  row.push(cur.trim());
                  rows.push(row);
                  row = [];
                  cur = "";
                } else {
                  cur += ch;
                }
              }
            }

            if (cur.length > 0 || row.length > 0) {
              row.push(cur.trim());
              rows.push(row);
            }
            return rows;
          }

          function processMatrix(matrix) {
            if (!Array.isArray(matrix) || matrix.length < 2) return false;

            // Cari baris header utama di spreadsheet
            var headerRowIdx = -1;
            for (var i = 0; i < Math.min(matrix.length, 10); i++) {
              var rowJoined = (matrix[i] || []).join(" ").toLowerCase();
              if (
                rowJoined.indexOf("nama kapal") !== -1 ||
                rowJoined.indexOf("destinasi") !== -1 ||
                (rowJoined.indexOf("no") !== -1 && rowJoined.indexOf("gate") !== -1)
              ) {
                headerRowIdx = i;
                break;
              }
            }

            if (headerRowIdx === -1) headerRowIdx = 0;

            var rawHeader = matrix[headerRowIdx] || [];
            // Deteksi apakah ada kolom Perkiraan Cuaca di spreadsheet (biasanya kolom ke-7 / index 6)
            var cuacaColIdx = -1;
            var statusColIdx = -1;

            rawHeader.forEach(function (h, idx) {
              var low = String(h || "").toLowerCase().trim();
              if (low.indexOf("cuaca") !== -1) cuacaColIdx = idx;
              if (low.indexOf("status") !== -1 || low.indexOf("keterangan") !== -1) statusColIdx = idx;
            });

            // Jika status tidak ditemukan lewat teks header, tentukan berdasarkan posisi kolom setelah Gate (index 5)
            if (statusColIdx === -1) {
              if (cuacaColIdx === 6 && rawHeader.length > 7) {
                statusColIdx = 7;
              } else if (rawHeader.length > 7) {
                statusColIdx = 7;
              } else if (rawHeader.length > 6) {
                statusColIdx = 6;
              } else {
                statusColIdx = 6;
              }
            }

            // Perbarui header tabel sesuai header di Google Sheets (kecuali kolom Perkiraan Cuaca)
            if (thead && rawHeader.length >= 6) {
              var hShip = escapeHtml(rawHeader[1] || "Nama Kapal");
              var hDest = escapeHtml(rawHeader[2] || "Destinasi");
              var hArr = escapeHtml(rawHeader[3] || "EST. Datang");
              var hDep = escapeHtml(rawHeader[4] || "EST. Berangkat");
              var hGate = escapeHtml(rawHeader[5] || "Gate / Line");
              var hStatus = escapeHtml(rawHeader[statusColIdx] || "Status Keberangkatan");
              thead.innerHTML =
                "<tr>" +
                  "<th>" + hShip + "</th>" +
                  "<th>" + hDest + "</th>" +
                  "<th>" + hArr + "</th>" +
                  "<th>" + hDep + "</th>" +
                  "<th>" + hGate + "</th>" +
                  "<th>" + hStatus + "</th>" +
                "</tr>";
            }

            var parsedRows = [];
            var foundTotal = "";
            var foundNote = "";

            for (var r = headerRowIdx + 1; r < matrix.length; r++) {
              var cols = matrix[r];
              if (!Array.isArray(cols) || cols.length === 0) continue;

              var joined = cols.join(" ").trim();
              if (!joined) continue;

              if (joined.toUpperCase().indexOf("TOTAL KEBERANGKATAN") !== -1) {
                for (var c = cols.length - 1; c >= 0; c--) {
                  if (cols[c] && String(cols[c]).toUpperCase().indexOf("TOTAL") === -1) {
                    foundTotal = String(cols[c]).trim();
                    break;
                  }
                }
                continue;
              }

              if (joined.indexOf("Catatan Operasional") !== -1 || joined.indexOf("ℹ️") !== -1) {
                continue;
              }

              var shipVal = String(cols[1] || "").trim();
              var destVal = String(cols[2] || "").trim();
              var arrVal = String(cols[3] || "").trim();
              var depVal = String(cols[4] || "").trim();
              var gateVal = String(cols[5] || "").trim();

              var rawStatus = cols[statusColIdx];
              // Jika statusColIdx kosong tetapi ada kolom setelahnya (misal geser 1 kolom), cek kolom sebelahnya
              if ((!rawStatus || String(rawStatus).trim() === "") && cols.length > statusColIdx + 1) {
                rawStatus = cols[statusColIdx + 1];
              }
              var statusVal = String(rawStatus || "-").trim() || "-";

              if (shipVal || destVal || arrVal || depVal) {
                parsedRows.push({
                  ship: shipVal || "-",
                  dest: destVal || "-",
                  arr: arrVal || "-",
                  dep: depVal || "-",
                  gate: gateVal || "-",
                  status: statusVal
                });
              }
            }

            var signature = JSON.stringify({ rows: parsedRows, total: foundTotal, note: foundNote });
            if (parsedRows.length > 0 || foundTotal || foundNote) {
              state.rows = parsedRows;
              if (foundTotal) state.totalText = foundTotal;
              state.hasLiveSheetData = true;

              if (signature !== state.lastSignature) {
                state.lastSignature = signature;
                renderAll();
              }
              return true;
            }
            return false;
          }

          // Fallback JSONP gviz
          function fetchViaJsonp() {
            return new Promise(function (resolve, reject) {
              var cbName = "gvizCb_" + Date.now() + "_" + Math.floor(Math.random() * 10000);
              var script = document.createElement("script");
              var timer = setTimeout(function () {
                cleanup();
                reject(new Error("JSONP timeout"));
              }, 6000);

              function cleanup() {
                clearTimeout(timer);
                delete window[cbName];
                if (script.parentNode) script.parentNode.removeChild(script);
              }

              window[cbName] = function (resp) {
                cleanup();
                try {
                  var table = resp && resp.table;
                  if (!table || !Array.isArray(table.rows)) {
                    reject(new Error("Invalid gviz table"));
                    return;
                  }
                  var matrix = [];
                  if (Array.isArray(table.cols)) {
                    matrix.push(table.cols.map(function (col) {
                      return (col && (col.label || col.id)) || "";
                    }));
                  }
                  table.rows.forEach(function (r) {
                    var cells = (r && r.c) || [];
                    matrix.push(cells.map(function (cell) {
                      if (!cell) return "";
                      return cell.f != null ? String(cell.f) : (cell.v != null ? String(cell.v) : "");
                    }));
                  });
                  resolve(matrix);
                } catch (e) {
                  reject(e);
                }
              };

              script.onerror = function () {
                cleanup();
                reject(new Error("JSONP script error"));
              };

              script.src = GVIZ_JSONP_BASE + "&tqx=out:json;responseHandler:" + cbName + "&_=" + Date.now();
              document.head.appendChild(script);
            });
          }

          async function syncGoogleSheet(isManual) {
            if (state.isFetching) return;
            state.isFetching = true;

            if (isManual && manualRefreshBtn) {
              manualRefreshBtn.disabled = true;
              manualRefreshBtn.textContent = "⏳ Memuat...";
            }

            var ts = Date.now();
            var freshCsvUrl = PUBLISHED_CSV_URL + "&_=" + ts;
            var fetchedSuccess = false;

            // 1. Utamakan CSV langsung dari URL Google Sheets yang dipublikasikan (dengan multi-proxy fallback)
            var endpoints = [
              freshCsvUrl,
              "https://api.codetabs.com/v1/proxy?quest=" + encodeURIComponent(freshCsvUrl),
              "https://api.allorigins.win/raw?url=" + encodeURIComponent(freshCsvUrl),
              "https://corsproxy.io/?" + encodeURIComponent(freshCsvUrl)
            ];

            for (var i = 0; i < endpoints.length; i++) {
              try {
                var res = await fetch(endpoints[i], { cache: "no-store" });
                if (!res.ok) continue;
                var csvText = await res.text();
                if (!csvText || csvText.trim().charAt(0) === "<") continue;
                var csvMatrix = parseCsv(csvText);
                if (processMatrix(csvMatrix)) {
                  fetchedSuccess = true;
                  break;
                }
              } catch (errFetch) {
                // Coba endpoint berikutnya
              }
            }

            // 2. Fallback ke JSONP gviz jika semua jalur CSV terblokir CORS/jaringan
            if (!fetchedSuccess) {
              try {
                var matrix = await fetchViaJsonp();
                if (processMatrix(matrix)) {
                  fetchedSuccess = true;
                }
              } catch (errJsonp) {
                // Semua jalur gagal
              }
            }

            state.isFetching = false;
            if (manualRefreshBtn) {
              manualRefreshBtn.disabled = false;
              manualRefreshBtn.textContent = "🔄 Refresh";
            }
          }

          // Cuaca Real-time Dumai via Open-Meteo
          async function syncDumaiWeather() {
            try {
              var url = "https://api.open-meteo.com/v1/forecast?latitude=1.6667&longitude=101.45&current=temperature_2m,weather_code&timezone=Asia%2FJakarta";
              var res = await fetch(url, { cache: "no-store" });
              if (!res.ok) return;
              var data = await res.json();
              if (!data || !data.current) return;

              var temp = Math.round(data.current.temperature_2m);
              var code = data.current.weather_code;
              var icon = "⛅";
              var desc = "Cerah Berawan";

              if (code === 0) { icon = "☀️"; desc = "Cerah"; }
              else if (code >= 1 && code <= 3) { icon = "⛅"; desc = "Cerah Berawan"; }
              else if (code >= 45 && code <= 48) { icon = "🌫️"; desc = "Berkabut"; }
              else if (code >= 51 && code <= 67) { icon = "🌦️"; desc = "Hujan Ringan"; }
              else if (code >= 80 && code <= 82) { icon = "🌧️"; desc = "Hujan Lebat"; }
              else if (code >= 95) { icon = "⛈️"; desc = "Hujan Petir"; }

              state.liveWeather = icon + " " + temp + "°C " + desc;
              if (statWeather) statWeather.textContent = icon + " " + temp + "°C";
              if (statWeatherDesc) statWeatherDesc.textContent = desc + " • Dumai (Open-Meteo)";
            } catch (errWeather) {
              // Pertahankan nilai cuaca terakhir jika offline
            }
          }

          if (manualRefreshBtn) {
            manualRefreshBtn.addEventListener("click", function () {
              syncGoogleSheet(true);
              syncDumaiWeather();
            });
          }

          // Render awal dan jalankan sinkronisasi otomatis
          renderAll();
          syncGoogleSheet(false);
          syncDumaiWeather();

          setInterval(function () {
            syncGoogleSheet(false);
          }, 5000);

          setInterval(syncDumaiWeather, 300000);
        } catch (initErr) {
          // Pengaman inisialisasi utama
        }
      }

      if (document.readyState === "loading") {
        document.addEventListener("DOMContentLoaded", initDashboard);
      } else {
        initDashboard();
      }
    })();
  </script>
</body>
</html>
