<!DOCTYPE html>
<html lang="fr">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<title>Colossus Stock</title>
<meta name="theme-color" content="#0d0e1a">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Colossus Stock">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800;900&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,500;0,9..40,600;1,9..40,300&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/html5-qrcode/2.3.8/html5-qrcode.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
<style>

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0d0f14;
    --bg2: #13161e;
    --surface: #1a1d27;
    --surface2: #21253a;
    --border: rgba(255,255,255,0.06);
    --accent: #5b8cff;
    --accent2: #a78bfa;
    --warn: #f59e0b;
    --danger: #ef4444;
    --ok: #34d399;
    --text: #f0f2f8;
    --muted: #7b82a0;
    --font-display: 'Syne', sans-serif;
    --font-body: 'DM Sans', sans-serif;
  }

  html { scroll-behavior: smooth; }

html {
  background: var(--bg); /* INDISPENSABLE : remplit l'espace si le body raccourcit */
  height: -webkit-fill-available;
  overflow: hidden;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  position: relative; /* FIX: fixed créait un stacking context piégeant la nav */
  width: 100%;
  height: 100%;
  height: -webkit-fill-available;
  margin: 0;
  padding: 0 !important;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

input, textarea, [contenteditable] {
  -webkit-user-select: text !important;
  user-select: text !important;
}

  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
    opacity: 0.03;
    pointer-events: none;
    z-index: 0;
  }

  .glow-orb {
    position: fixed;
    width: 500px; height: 500px;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
    z-index: 0;
  }
  .glow-orb-1 { background: rgba(91,140,255,0.12); top: -100px; right: -100px; }
  .glow-orb-2 { background: rgba(167,139,250,0.08); bottom: -100px; left: -100px; }

header {
  position: relative; z-index: 10;
  padding: max(env(safe-area-inset-top, 44px), 44px) 24px 16px;
    display: flex; justify-content: space-between; align-items: flex-end;
  }
  .header-eyebrow {
    font-family: var(--font-display);
    font-size: 10px; font-weight: 800; letter-spacing: 0.2em;
    color: var(--accent); text-transform: uppercase; margin-bottom: 8px;
  }
  .header-name {
    font-family: var(--font-display);
    font-size: 42px; font-weight: 900; line-height: 1;
    background: linear-gradient(135deg, #fff 30%, var(--accent2));
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .avatar {
    width: 52px; height: 52px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 18px;
    display: flex; align-items: center; justify-content: center;
    font-size: 24px;
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
    cursor: pointer;
    transition: transform 0.2s;
  }
  .avatar:active { transform: scale(0.94); }

  main { position: relative; z-index: 10; padding: 0 20px; flex: 1; min-height: 0; display: flex; flex-direction: column; overflow: hidden; }

  .tab-content { display: none; }
  .tab-content.active { animation: fadeUp 0.3s ease; }
#stock { display: none; }
#stock.active { 
  display: flex; 
  flex-direction: column; 
  flex: 1;        /* FIX: remplace height:100% */
  min-height: 0;  /* FIX: essentiel pour le scroll dans un flex */
  overflow: hidden; 
  padding-bottom: 0; 
}

.tab-content.active:not(#stock) {
  display: flex;
  flex-direction: column;
  flex: 1;        /* FIX: remplace height:100% */
  min-height: 0;  /* FIX: essentiel pour le scroll dans un flex */
  padding-bottom: 140px;
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
}

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .stats-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 20px; }
  .stat-card {
    padding: 22px 20px;
    border-radius: 28px;
    position: relative; overflow: hidden;
    border: 1px solid var(--border);
    cursor: default;
    transition: transform 0.2s;
  }
  .stat-card:active { transform: scale(0.97); }
  .stat-card-blue { background: linear-gradient(145deg, #1e3a8a, #1d4ed8); box-shadow: 0 20px 60px rgba(37,99,235,0.3); }
  .stat-card-orange { background: linear-gradient(145deg, #78350f, #b45309); box-shadow: 0 20px 60px rgba(180,83,9,0.3); }
  .stat-card::after {
    content: '';
    position: absolute; top: -30px; right: -30px;
    width: 100px; height: 100px;
    border-radius: 50%;
    background: rgba(255,255,255,0.05);
  }
  .stat-icon { font-size: 22px; margin-bottom: 14px; }
  .stat-num {
    font-family: var(--font-display);
    font-size: 38px; font-weight: 900; line-height: 1;
    color: #fff;
  }
  .stat-label {
    font-size: 9px; font-weight: 600; letter-spacing: 0.18em;
    color: rgba(255,255,255,0.7); text-transform: uppercase; margin-top: 4px;
  }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 28px;
    padding: 24px;
    margin-bottom: 20px;
  }
  .card-title {
    font-family: var(--font-display);
    font-size: 10px; font-weight: 800; letter-spacing: 0.18em;
    color: var(--muted); text-transform: uppercase; margin-bottom: 18px;
  }
  .field {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 14px 16px;
    color: var(--text);
    font-family: var(--font-body);
    font-size: 15px; font-weight: 500;
    width: 100%;
    outline: none;
    transition: border-color 0.2s, box-shadow 0.2s;
    -webkit-appearance: none;
    appearance: none;
  }
  .field:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(91,140,255,0.15); }
  .field::placeholder { color: var(--muted); }
  .fields-row { display: flex; gap: 10px; }
  .fields-row .field { flex: 1; }
  .field-qty { width: 80px !important; flex: 0 0 80px !important; text-align: center; }

  select.field { background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%237b82a0' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 14px center; padding-right: 36px; }

  .form-space { display: flex; flex-direction: column; gap: 10px; }

  .btn-primary {
    width: 100%;
    padding: 16px;
    border-radius: 16px;
    border: none; cursor: pointer;
    background: var(--accent);
    color: #fff;
    font-family: var(--font-display);
    font-size: 13px; font-weight: 800; letter-spacing: 0.12em;
    text-transform: uppercase;
    box-shadow: 0 8px 32px rgba(91,140,255,0.4);
    transition: all 0.2s;
    position: relative; overflow: hidden;
  }
  .btn-primary::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.15), transparent);
  }
  .btn-primary:active { transform: scale(0.97); box-shadow: 0 4px 16px rgba(91,140,255,0.3); }
  .btn-primary.loading { opacity: 0.7; pointer-events: none; }

  .section-header {
    display: flex; justify-content: space-between; align-items: center;
    margin-bottom: 14px; padding: 0 4px;
  }
  .section-title {
    font-family: var(--font-display);
    font-size: 20px; font-weight: 800; color: var(--text);
  }
  .btn-refresh {
    font-size: 12px; font-weight: 600; color: var(--accent);
    background: none; border: none; cursor: pointer;
    padding: 6px 12px; border-radius: 10px;
    background: rgba(91,140,255,0.1);
    transition: background 0.2s;
  }
  .btn-refresh:active { background: rgba(91,140,255,0.2); }

  .chips { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 4px; margin-bottom: 16px; scrollbar-width: none; }
  .chips::-webkit-scrollbar { display: none; }
  .chip {
    flex-shrink: 0;
    padding: 6px 14px;
    border-radius: 100px;
    font-size: 12px; font-weight: 600;
    border: 1px solid var(--border);
    background: var(--surface);
    color: var(--muted);
    cursor: pointer;
    transition: all 0.2s;
  }
  .chip.active { background: var(--accent); border-color: var(--accent); color: #fff; }

  .stock-list { display: flex; flex-direction: column; gap: 10px; }

  .item-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 22px;
    padding: 16px;
    display: flex; align-items: center; gap: 14px;
    transition: transform 0.15s, border-color 0.2s;
    animation: fadeUp 0.3s ease both;
    position: relative; overflow: hidden;
  }
  .item-card.expired { border-color: rgba(239,68,68,0.3); background: rgba(239,68,68,0.05); }
  .item-card.urgent { border-color: rgba(245,158,11,0.3); background: rgba(245,158,11,0.04); }
  .item-card:active { transform: scale(0.98); }

  .item-icon {
    width: 50px; height: 50px; flex-shrink: 0;
    border-radius: 16px;
    display: flex; align-items: center; justify-content: center;
    font-size: 22px;
  }
  .icon-frigo { background: rgba(59,130,246,0.15); }
  .icon-conge { background: rgba(167,139,250,0.15); }
  .icon-placard { background: rgba(249,115,22,0.15); }
  .icon-cave { background: rgba(52,211,153,0.15); }

  .item-info { flex: 1; min-width: 0; }
  .item-name {
    font-family: var(--font-display);
    font-size: 15px; font-weight: 700; color: var(--text);
    white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
  }
  .item-cat { font-size: 11px; color: var(--muted); font-weight: 500; margin-top: 2px; }

  .item-right { display: flex; flex-direction: column; align-items: flex-end; gap: 6px; }
  .item-qty {
    font-family: var(--font-display);
    font-size: 12px; font-weight: 700;
    background: var(--bg2); color: var(--muted);
    padding: 3px 10px; border-radius: 8px;
    border: 1px solid var(--border);
  }
  .item-status {
    font-size: 10px; font-weight: 700; letter-spacing: 0.08em;
    text-transform: uppercase;
  }
  .status-ok { color: var(--ok); }
  .status-warn { color: var(--warn); }
  .status-bad { color: var(--danger); }

  .item-bar-wrap {
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 2px; background: rgba(255,255,255,0.04);
    border-radius: 0 0 22px 22px;
  }
  .item-bar { height: 100%; border-radius: 22px; transition: width 0.6s ease; }
  .bar-ok { background: var(--ok); }
  .bar-warn { background: var(--warn); }
  .bar-bad { background: var(--danger); }

  .item-delete {
    width: 36px; height: 36px; flex-shrink: 0;
    border-radius: 12px; border: 1px solid rgba(239,68,68,0.2);
    background: rgba(239,68,68,0.08);
    color: var(--danger); font-size: 16px;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; opacity: 0.4; transition: opacity 0.2s;
  }
  .item-card:hover .item-delete { opacity: 1; }

  .empty {
    text-align: center; padding: 60px 20px;
    color: var(--muted);
  }
  .empty-icon { font-size: 48px; margin-bottom: 12px; opacity: 0.4; }
  .empty-text { font-size: 14px; font-weight: 500; }

  .menu-hero {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 28px;
    padding: 40px 24px;
    text-align: center;
  }
  .menu-hero .big-icon { font-size: 56px; margin-bottom: 16px; opacity: 0.6; }
  .menu-hero p { color: var(--muted); font-size: 14px; line-height: 1.6; }
  .menu-hero h3 {
    font-family: var(--font-display);
    font-size: 22px; font-weight: 800; margin-bottom: 8px;
  }
  .btn-ghost {
    margin-top: 20px;
    padding: 12px 24px;
    border-radius: 14px;
    border: 1px solid var(--border);
    background: none;
    color: var(--accent);
    font-family: var(--font-display);
    font-size: 12px; font-weight: 800; letter-spacing: 0.1em;
    cursor: pointer; transition: all 0.2s;
  }
  .btn-ghost:active { background: rgba(91,140,255,0.1); }

  #toast {
    position: fixed; bottom: 110px; left: 50%; transform: translateX(-50%) translateY(20px);
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text);
    padding: 12px 20px; border-radius: 14px;
    font-size: 13px; font-weight: 600;
    opacity: 0; transition: all 0.3s;
    z-index: 100; pointer-events: none;
    white-space: nowrap;
    box-shadow: 0 8px 32px rgba(0,0,0,0.5);
  }
  #toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

  body {
  margin: 0;
}

nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  display: flex;
  justify-content: space-around;
  background: var(--bg);
  border-top: 1px solid rgba(255,255,255,0.08);
  padding-top: 8px;
  /* max() garantit qu'on couvre la home bar même si safe-area-inset-bottom = 0 */
  padding-bottom: max(env(safe-area-inset-bottom), 16px);
  box-sizing: border-box;
}

  .nav-btn {
  background: none; border: none; color: var(--text-muted);
  display: flex; flex-direction: column; align-items: center;
  gap: 4px; cursor: pointer; padding: 4px 8px;
  transition: color 0.2s; font-size: 9px; font-weight: 600;
  letter-spacing: 0.05em; text-transform: uppercase;
  flex: 1; min-width: 0;
}
  .nav-btn .nav-icon { font-size: 22px; transition: transform 0.2s; }
  .nav-btn .nav-label {
    font-family: var(--font-display);
    font-size: 9px; font-weight: 800; letter-spacing: 0.12em;
    color: var(--muted); text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-btn.active .nav-label { color: var(--accent); }
  .nav-btn.active .nav-icon { transform: scale(1.15); }
  .nav-btn:active { background: rgba(255,255,255,0.05); }

  .skeleton {
    background: linear-gradient(90deg, var(--surface) 25%, var(--surface2) 50%, var(--surface) 75%);
    background-size: 200% 100%;
    animation: shimmer 1.4s infinite;
    border-radius: 22px; height: 82px;
    border: 1px solid var(--border);
  }
  @keyframes shimmer { from { background-position: 200% 0; } to { background-position: -200% 0; } }

  #scan-modal {
    position: fixed; inset: 0; z-index: 200;
    background: rgba(0,0,0,0.92);
    display: flex; flex-direction: column;
    align-items: center; justify-content: flex-start;
    padding-top: 60px;
    opacity: 0; pointer-events: none;
    transition: opacity 0.3s;
  }
  #scan-modal.open { opacity: 1; pointer-events: all; }

  .scan-header {
    width: 100%; display: flex; justify-content: space-between; align-items: center;
    padding: 0 24px; margin-bottom: 28px;
  }
  .scan-title {
    font-family: var(--font-display);
    font-size: 22px; font-weight: 900; color: #fff;
  }
  .scan-close {
    width: 40px; height: 40px; border-radius: 14px;
    background: rgba(255,255,255,0.1); border: none;
    color: #fff; font-size: 18px; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: background 0.2s;
  }
  .scan-close:active { background: rgba(255,255,255,0.2); }

  .scan-viewport {
    position: relative;
    width: 300px; height: 300px;
    border-radius: 28px; overflow: hidden;
    box-shadow: 0 0 0 4px rgba(91,140,255,0.4), 0 0 60px rgba(91,140,255,0.2);
  }
  #scan-video {
    width: 100%; height: 100%;
    object-fit: cover;
    transform: scaleX(-1);
  }
  .scan-viewport::before, .scan-viewport::after {
    content: ''; position: absolute;
    width: 36px; height: 36px;
    border-color: var(--accent); border-style: solid;
    z-index: 5;
  }
  .scan-viewport::before { top: 10px; left: 10px; border-width: 3px 0 0 3px; border-radius: 4px 0 0 0; }
  .scan-viewport::after  { bottom: 10px; right: 10px; border-width: 0 3px 3px 0; border-radius: 0 0 4px 0; }

  .scan-laser {
    position: absolute; left: 16px; right: 16px;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    box-shadow: 0 0 8px var(--accent);
    top: 50%;
    animation: laserScan 2s ease-in-out infinite;
    z-index: 4;
  }
  @keyframes laserScan {
    0%   { top: 20%; opacity: 1; }
    50%  { top: 80%; opacity: 0.7; }
    100% { top: 20%; opacity: 1; }
  }

  .scan-status {
    margin-top: 24px;
    font-size: 13px; font-weight: 600; color: var(--muted);
    text-align: center; padding: 0 40px;
    min-height: 40px;
  }
  .scan-status.found { color: var(--ok); font-weight: 700; }
  .scan-status.error { color: var(--danger); }

  #scan-result-panel {
    position: absolute; bottom: 0; left: 0; right: 0;
    background: var(--surface);
    border-radius: 28px 28px 0 0;
    border-top: 1px solid var(--border);
    padding: 28px 24px 48px;
    transform: translateY(100%);
    transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  }
  #scan-result-panel.open { transform: translateY(0); }
  .result-product-name {
    font-family: var(--font-display);
    font-size: 20px; font-weight: 800; color: var(--text);
    margin-bottom: 4px;
  }
  .result-brand { font-size: 13px; color: var(--muted); font-weight: 500; margin-bottom: 20px; }
  .result-fields { display: flex; flex-direction: column; gap: 10px; margin-bottom: 16px; }
  .btn-scan-add {
    width: 100%; padding: 16px; border-radius: 16px; border: none;
    background: var(--ok); color: #fff;
    font-family: var(--font-display);
    font-size: 13px; font-weight: 800; letter-spacing: 0.1em;
    cursor: pointer; transition: all 0.2s;
    box-shadow: 0 8px 24px rgba(52,211,153,0.4);
  }
  .btn-scan-add:active { transform: scale(0.97); }
  .btn-scan-again {
    width: 100%; padding: 12px; border-radius: 14px; border: 1px solid var(--border);
    background: none; color: var(--muted);
    font-family: var(--font-display); font-size: 12px; font-weight: 700;
    cursor: pointer; margin-top: 8px; transition: all 0.2s;
  }
  .btn-scan-again:active { background: var(--surface2); }

  #scan-video-wrap > img { display: none !important; }
  #scan-video-wrap video { width: 100% !important; height: 100% !important; object-fit: cover !important; border-radius: 28px; }
  #scan-video-wrap canvas { display: none !important; }
  #html5-qrcode-button-camera-permission,
  #html5-qrcode-button-camera-stop,
  #html5-qrcode-button-camera-start,
  #html5qr-code-full-region__header_message,
  #html5qr-code-full-region__dashboard { display: none !important; }

  .quick-scan-btn {
    width: 100%;
    display: flex; align-items: center; justify-content: center; gap: 10px;
    padding: 16px;
    border-radius: 20px;
    border: 1.5px dashed rgba(91,140,255,0.4);
    background: rgba(91,140,255,0.06);
    color: var(--accent);
    font-family: var(--font-display);
    font-size: 13px; font-weight: 800; letter-spacing: 0.1em;
    cursor: pointer; transition: all 0.2s;
    margin-bottom: 20px;
  }
  .quick-scan-btn:active { background: rgba(91,140,255,0.14); border-style: solid; }
  .quick-scan-btn .qsb-icon {
    font-size: 20px;
    animation: pulse-icon 2s ease infinite;
  }
  @keyframes pulse-icon {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.15); }
  }

  .chef-header { padding: 8px 4px 24px; }
  .chef-badge {
    display: inline-block;
    font-family: var(--font-display);
    font-size: 10px; font-weight: 800; letter-spacing: 0.2em;
    color: var(--accent2); background: rgba(167,139,250,0.12);
    border: 1px solid rgba(167,139,250,0.25);
    padding: 4px 12px; border-radius: 100px; margin-bottom: 12px;
  }
  .chef-title {
    font-family: var(--font-display);
    font-size: 36px; font-weight: 900; line-height: 1.05;
    background: linear-gradient(135deg, #fff 20%, var(--accent2));
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    margin-bottom: 8px;
  }
  .chef-sub { font-size: 14px; color: var(--muted); font-weight: 500; }

  .btn-chef-generate {
    width: 100%; display: flex; align-items: center; justify-content: space-between;
    padding: 20px 24px; border-radius: 22px; border: none; cursor: pointer;
    background: linear-gradient(135deg, #4c1d95, #7c3aed);
    color: #fff; margin-bottom: 24px;
    box-shadow: 0 12px 40px rgba(124,58,237,0.45);
    transition: all 0.2s;
    font-family: var(--font-display); font-size: 15px; font-weight: 800;
  }
  .btn-chef-generate:active { transform: scale(0.98); box-shadow: 0 6px 20px rgba(124,58,237,0.4); }
  .btn-chef-generate.loading { opacity: 0.6; pointer-events: none; }
  .chef-btn-icon { font-size: 24px; }
  .chef-btn-arrow { font-size: 20px; opacity: 0.7; }

  .chef-loading { text-align: center; padding: 40px 0; color: var(--muted); font-size: 14px; }
  .chef-dots { display: flex; justify-content: center; gap: 8px; margin-bottom: 14px; }
  .chef-dots span {
    width: 10px; height: 10px; border-radius: 50%;
    background: var(--accent2); opacity: 0.3;
    animation: dotPulse 1.2s ease-in-out infinite;
  }
  .chef-dots span:nth-child(2) { animation-delay: 0.2s; }
  .chef-dots span:nth-child(3) { animation-delay: 0.4s; }
  @keyframes dotPulse { 0%,100% { opacity: 0.3; transform: scale(1); } 50% { opacity: 1; transform: scale(1.3); } }

  .recipe-list { display: flex; flex-direction: column; gap: 14px; }
  .recipe-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 24px; padding: 20px;
    display: flex; align-items: center; gap: 16px;
    cursor: pointer; transition: all 0.2s;
    animation: fadeUp 0.35s ease both;
    position: relative; overflow: hidden;
  }
  .recipe-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent2), var(--accent));
    opacity: 0; transition: opacity 0.2s;
  }
  .recipe-card:active { transform: scale(0.98); }
  .recipe-card:hover::before { opacity: 1; }

  .recipe-emoji {
    width: 58px; height: 58px; flex-shrink: 0;
    background: rgba(167,139,250,0.1); border-radius: 18px;
    display: flex; align-items: center; justify-content: center;
    font-size: 28px;
  }
  .recipe-info { flex: 1; min-width: 0; }
  .recipe-name {
    font-family: var(--font-display);
    font-size: 16px; font-weight: 800; color: var(--text);
    white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
  }
  .recipe-meta { font-size: 12px; color: var(--muted); font-weight: 500; margin-top: 3px; }
  .recipe-ingredients {
    display: flex; flex-wrap: wrap; gap: 4px; margin-top: 8px;
  }
  .recipe-tag {
    font-size: 10px; font-weight: 700; padding: 2px 8px; border-radius: 8px;
    background: rgba(91,140,255,0.12); color: var(--accent);
    border: 1px solid rgba(91,140,255,0.2);
  }
  .recipe-tag.missing {
    background: rgba(239,68,68,0.08); color: var(--danger);
    border-color: rgba(239,68,68,0.15);
  }
  .recipe-card-thumb {
    width: 56px; height: 56px; border-radius: 14px; object-fit: cover;
    flex-shrink: 0;
  }
  .recipe-arrow { color: var(--muted); font-size: 18px; }

  .recipe-modal {
    position: fixed; inset: 0; z-index: 300;
    background: rgba(0,0,0,0.85);
    display: flex; align-items: flex-end;
    opacity: 0; pointer-events: none;
    transition: opacity 0.3s;
  }
  .recipe-modal.open { opacity: 1; pointer-events: all; }
  .recipe-modal-inner {
    background: var(--bg2);
    border-radius: 32px 32px 0 0;
    border: 1px solid var(--border);
    border-bottom: none;
    width: 100%; max-height: 85dvh;
    overflow-y: auto; padding: 28px 24px 120px;
    transform: translateY(40px);
    transition: transform 0.4s cubic-bezier(0.34, 1.3, 0.64, 1);
  }
  .recipe-modal.open .recipe-modal-inner { transform: translateY(0); }
  .recipe-modal-header {
    display: flex; justify-content: space-between; align-items: flex-start;
    margin-bottom: 24px;
  }
  .recipe-modal-emoji { font-size: 40px; margin-bottom: 8px; }
  .recipe-modal-title {
    font-family: var(--font-display);
    font-size: 26px; font-weight: 900; color: var(--text); line-height: 1.1;
  }
  .recipe-modal-meta { font-size: 13px; color: var(--muted); font-weight: 500; margin-top: 4px; }
  .recipe-modal-close {
    width: 40px; height: 40px; border-radius: 14px; flex-shrink: 0;
    background: var(--surface2); border: 1px solid var(--border);
    color: var(--muted); font-size: 16px; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }
  .recipe-modal-close:active { background: var(--surface); color: var(--text); }
  .recipe-modal-body { line-height: 1.7; }

  .recipe-img-wrap {
    width: 100%; height: 200px; border-radius: 20px; overflow: hidden;
    margin-bottom: 20px; background: var(--surface2);
    display: flex; align-items: center; justify-content: center;
  }
  .recipe-img-placeholder { font-size: 64px; opacity: 0.5; }
  .recipe-img {
    width: 100%; height: 200px;
    object-fit: cover; object-position: center;
    border-radius: 20px; display: block;
  }

  .btn-cook {
    width: 100%; margin-top: 28px; padding: 18px; border-radius: 18px; border: none;
    background: linear-gradient(135deg, #059669, #34d399);
    color: #fff; font-family: var(--font-display);
    font-size: 15px; font-weight: 900; letter-spacing: 0.08em;
    cursor: pointer; transition: all 0.2s;
    box-shadow: 0 10px 30px rgba(52,211,153,0.4);
    display: flex; align-items: center; justify-content: center; gap: 10px;
  }
  .btn-cook:active { transform: scale(0.97); }
  .btn-cook:disabled { opacity: 0.5; }

  .recipe-section-title {
    font-family: var(--font-display);
    font-size: 11px; font-weight: 800; letter-spacing: 0.16em;
    color: var(--muted); text-transform: uppercase; margin: 24px 0 12px;
  }
  .recipe-ingredients-list { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 8px; }
  .ing-pill {
    font-size: 13px; font-weight: 600; padding: 6px 14px; border-radius: 12px;
    background: var(--surface); border: 1px solid var(--border); color: var(--text);
  }
  .ing-pill.have { border-color: rgba(52,211,153,0.3); background: rgba(52,211,153,0.07); color: var(--ok); }
  .ing-pill.need { border-color: rgba(245,158,11,0.3); background: rgba(245,158,11,0.07); color: var(--warn); }

  .step-item {
    display: flex; gap: 14px; margin-bottom: 18px; align-items: flex-start;
    animation: fadeUp 0.3s ease both;
  }
  .step-num {
    flex-shrink: 0; width: 30px; height: 30px; border-radius: 10px;
    background: linear-gradient(135deg, var(--accent2), var(--accent));
    display: flex; align-items: center; justify-content: center;
    font-family: var(--font-display); font-size: 13px; font-weight: 900; color: #fff;
    margin-top: 1px;
  }
  .step-text { font-size: 15px; color: var(--text); font-weight: 400; line-height: 1.6; padding-top: 4px; }

  .recipe-tip {
    background: rgba(245,158,11,0.08); border: 1px solid rgba(245,158,11,0.2);
    border-radius: 16px; padding: 14px 16px; margin-top: 24px;
    font-size: 13px; color: var(--warn); font-weight: 500; line-height: 1.5;
  }
  .recipe-tip strong { font-weight: 800; }
  .item-card:nth-child(1) { animation-delay: 0.0s; }
  .item-card:nth-child(2) { animation-delay: 0.04s; }
  .item-card:nth-child(3) { animation-delay: 0.08s; }
  .item-card:nth-child(4) { animation-delay: 0.12s; }
  .item-card:nth-child(5) { animation-delay: 0.16s; }
  .item-card:nth-child(6) { animation-delay: 0.20s; }
  .item-card:nth-child(7) { animation-delay: 0.24s; }
  .item-card:nth-child(8) { animation-delay: 0.28s; }

  .planning-wrap { margin-top: 32px; margin-bottom: 20px; }
  .planning-header {
    display: flex; justify-content: space-between; align-items: flex-start;
    margin-bottom: 18px;
  }
  .planning-title {
    font-family: var(--font-display);
    font-size: 22px; font-weight: 900; color: var(--text);
  }
  .planning-reset {
    width: 36px; height: 36px; border-radius: 12px;
    background: var(--surface); border: 1px solid var(--border);
    color: var(--muted); font-size: 18px; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }
  .planning-reset:active { background: var(--surface2); color: var(--text); }

  .planning-days { display: flex; flex-direction: column; gap: 10px; }

  .planning-day-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 22px; overflow: hidden;
    animation: fadeUp 0.3s ease both;
  }
  .planning-day-header {
    display: flex; align-items: center; gap: 12px;
    padding: 14px 16px 10px;
  }
  .planning-day-dot {
    width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0;
  }
  .planning-day-name {
    font-family: var(--font-display);
    font-size: 13px; font-weight: 800; color: var(--text); flex: 1;
    text-transform: uppercase; letter-spacing: 0.08em;
  }
  .planning-day-date { font-size: 11px; color: var(--muted); font-weight: 500; }

  .planning-slots { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; padding: 0 12px 12px; }

  .planning-slot {
    border-radius: 14px; padding: 12px 14px; cursor: pointer;
    border: 1.5px dashed rgba(255,255,255,0.08);
    background: var(--bg2);
    transition: all 0.2s; min-height: 70px;
    display: flex; flex-direction: column; justify-content: space-between;
    position: relative; overflow: hidden;
  }
  .planning-slot:active { transform: scale(0.97); }
  .planning-slot.has-meal {
    border-style: solid; border-color: rgba(91,140,255,0.25);
    background: rgba(91,140,255,0.06);
  }
  .planning-slot.has-meal.dinner {
    border-color: rgba(167,139,250,0.25);
    background: rgba(167,139,250,0.06);
  }
  .slot-label {
    font-size: 9px; font-weight: 800; letter-spacing: 0.14em;
    color: var(--muted); text-transform: uppercase; margin-bottom: 6px;
  }
  .slot-meal {
    font-family: var(--font-display);
    font-size: 13px; font-weight: 700; color: var(--text);
    line-height: 1.3;
  }
  .slot-empty {
    font-size: 11px; color: rgba(255,255,255,0.2);
    font-weight: 500; line-height: 1.4;
  }
  .slot-add-icon {
    position: absolute; bottom: 8px; right: 10px;
    font-size: 16px; opacity: 0.2;
  }
  .slot-emoji { font-size: 18px; margin-bottom: 4px; }

  .pm-custom-row { display: flex; gap: 8px; margin-bottom: 16px; }
  .pm-custom-btn {
    width: 50px; height: 50px; flex-shrink: 0; border-radius: 14px;
    background: var(--accent); border: none; color: #fff;
    font-size: 22px; font-weight: 900; cursor: pointer;
    transition: all 0.2s;
  }
  .pm-custom-btn:active { transform: scale(0.95); }
  .pm-section-label {
    text-align: center; font-size: 11px; color: var(--muted);
    font-weight: 600; letter-spacing: 0.08em; margin: 4px 0 12px;
  }
  .pm-recipe-list { display: flex; flex-direction: column; gap: 8px; }
  .pm-recipe-option {
    display: flex; align-items: center; gap: 12px;
    background: var(--bg2); border: 1px solid var(--border);
    border-radius: 14px; padding: 12px 14px; cursor: pointer;
    transition: all 0.2s;
  }
  .pm-recipe-option:active { background: var(--surface2); border-color: var(--accent); }
  .pm-recipe-option-emoji { font-size: 22px; }
  .pm-recipe-option-name {
    font-family: var(--font-display); font-size: 14px; font-weight: 700; color: var(--text); flex: 1;
  }
  .pm-recipe-option-time { font-size: 11px; color: var(--muted); }
  .pm-clear-btn {
    width: 100%; margin-top: 12px; padding: 12px; border-radius: 14px;
    background: none; border: 1px solid rgba(239,68,68,0.2);
    color: var(--danger); font-family: var(--font-display);
    font-size: 12px; font-weight: 800; cursor: pointer; transition: all 0.2s;
  }
  .pm-clear-btn:active { background: rgba(239,68,68,0.08); }

  .fab {
    position: fixed; bottom: 100px; right: 24px; z-index: 60;
    width: 60px; height: 60px; border-radius: 20px; border: none;
    background: linear-gradient(135deg, var(--accent2), var(--accent));
    box-shadow: 0 8px 32px rgba(91,140,255,0.5);
    cursor: pointer; transition: all 0.25s;
    display: flex; align-items: center; justify-content: center;
  }
  .fab:active { transform: scale(0.9); }
  .fab-plus { font-size: 32px; color: #fff; font-weight: 300; line-height: 1; margin-top: -2px; }

  .add-modal-scan-btn {
    width: 100%; display: flex; align-items: center; gap: 14px;
    padding: 16px 18px; border-radius: 18px; border: none; cursor: pointer;
    background: rgba(91,140,255,0.08); border: 1px solid rgba(91,140,255,0.2);
    margin-bottom: 4px; transition: all 0.2s;
  }
  .add-modal-scan-btn:active { background: rgba(91,140,255,0.15); }
  .add-modal-scan-icon { font-size: 28px; }
  .add-modal-scan-text { flex: 1; text-align: left; }
  .add-modal-scan-title { display: block; font-family: var(--font-display); font-size: 14px; font-weight: 800; color: var(--text); }
  .add-modal-scan-sub { display: block; font-size: 11px; color: var(--muted); margin-top: 2px; }
  .add-modal-divider {
    text-align: center; position: relative; margin: 16px 0;
    color: var(--muted); font-size: 11px; font-weight: 600; letter-spacing: 0.08em;
  }
  .add-modal-divider::before, .add-modal-divider::after {
    content: ''; position: absolute; top: 50%;
    width: 38%; height: 1px; background: var(--border);
  }
  .add-modal-divider::before { left: 0; }
  .add-modal-divider::after { right: 0; }

  .inv-header {
    display: flex; justify-content: space-between; align-items: center;
    padding: 14px 4px; cursor: pointer; user-select: none;
  }
  .inv-chevron {
    font-size: 20px; color: var(--muted); display: inline-block;
    transition: transform 0.3s;
  }
  .inv-chevron.open { transform: rotate(0deg); }
  .inv-chevron:not(.open) { transform: rotate(-90deg); }
.inv-collapsible {
  overflow-y: auto;
  flex: 1;
  min-height: 0;
  opacity: 1;
  padding-bottom: 160px;
  -webkit-overflow-scrolling: touch;
  overscroll-behavior: contain;
  scroll-behavior: smooth;
    scrollbar-width: none;
}
.inv-collapsible::-webkit-scrollbar { display: none; }
  .inv-collapsible:not(.open) { flex: 0; max-height: 0; opacity: 0; overflow: hidden; }

  .store-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-bottom: 20px; }
  .store-btn {
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    padding: 12px 8px; border-radius: 18px;
    background: var(--surface); border: 1px solid var(--border);
    cursor: pointer; transition: all 0.2s;
  }
  .store-btn:active { transform: scale(0.95); border-color: var(--accent); }
  .store-logo {
    width: 56px; height: 56px; border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px; font-family: var(--font-display);
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
  }
  .store-name { font-family: var(--font-display); font-size: 10px; font-weight: 800; color: var(--text); text-align: center; }
  .store-info { background: rgba(91,140,255,0.06); border: 1px solid rgba(91,140,255,0.15); border-radius: 14px; padding: 14px 16px; }
  .store-info p { font-size: 12px; color: var(--muted); line-height: 1.6; font-weight: 500; }

  .servings-row {
    display: flex; align-items: center; justify-content: space-between;
    background: var(--surface2); border: 1px solid var(--border);
    border-radius: 16px; padding: 14px 16px; margin-bottom: 20px;
  }
  .servings-label { font-size: 14px; font-weight: 600; color: var(--text); }
  .servings-ctrl { display: flex; align-items: center; gap: 14px; }
  .serv-btn {
    width: 34px; height: 34px; border-radius: 10px; border: none;
    background: var(--surface); border: 1px solid var(--border);
    color: var(--text); font-size: 20px; font-weight: 700;
    cursor: pointer; display: flex; align-items: center; justify-content: center;
    transition: all 0.15s; line-height: 1;
  }
  .serv-btn:active { background: var(--accent); border-color: var(--accent); color: #fff; transform: scale(0.92); }
  .serv-count {
    font-family: var(--font-display); font-size: 22px; font-weight: 900;
    color: var(--accent); min-width: 28px; text-align: center;
  }

  .btn-share-list {
    width: 100%; display: flex; align-items: center; gap: 14px;
    padding: 18px 20px; border-radius: 22px; border: none; cursor: pointer;
    background: var(--surface);
    border: 1px solid rgba(167,139,250,0.25);
    background: linear-gradient(135deg, rgba(167,139,250,0.08), rgba(91,140,255,0.06));
    transition: all 0.2s;
  }
  .btn-share-list:active { transform: scale(0.98); }
  .share-btn-icon {
    width: 44px; height: 44px; border-radius: 14px; flex-shrink: 0;
    background: linear-gradient(135deg, var(--accent2), var(--accent));
    display: flex; align-items: center; justify-content: center;
    font-size: 20px; color: #fff; font-weight: 900;
    box-shadow: 0 6px 20px rgba(167,139,250,0.4);
  }
  .share-btn-text { flex: 1; text-align: left; }
  .share-btn-title {
    display: block; font-family: var(--font-display);
    font-size: 14px; font-weight: 800; color: var(--text);
  }
  .share-btn-sub { display: block; font-size: 11px; color: var(--muted); font-weight: 500; margin-top: 2px; }
  .share-btn-arrow { font-size: 20px; color: var(--muted); }

  .share-preview {
    background: var(--bg2); border: 1px solid var(--border);
    border-radius: 16px; padding: 16px; margin-bottom: 20px;
    font-size: 13px; line-height: 1.8; color: var(--text);
    max-height: 160px; overflow-y: auto; white-space: pre-line;
    font-family: 'Courier New', monospace;
    scrollbar-width: thin;
  }
  .share-grid {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px;
  }
  .share-option {
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    padding: 16px 10px; border-radius: 18px;
    background: var(--surface); border: 1px solid var(--border);
    cursor: pointer; transition: all 0.2s;
    font-family: var(--font-display); font-size: 11px; font-weight: 700;
    color: var(--text);
  }
  .share-option:active { transform: scale(0.95); background: var(--surface2); }
  .share-option-icon {
    width: 52px; height: 52px; border-radius: 16px;
    border: 1px solid; display: flex; align-items: center; justify-content: center;
  }

  .courses-sources { display: flex; gap: 8px; margin-bottom: 20px; }
  .source-btn {
    flex: 1; padding: 10px 14px; border-radius: 14px;
    border: 1px solid var(--border); background: var(--surface);
    color: var(--muted); font-family: var(--font-display);
    font-size: 11px; font-weight: 800; letter-spacing: 0.08em;
    cursor: pointer; transition: all 0.2s; text-align: center;
  }
  .source-btn.active { background: rgba(52,211,153,0.12); border-color: rgba(52,211,153,0.35); color: var(--ok); }

  .courses-list { display: flex; flex-direction: column; gap: 10px; margin-bottom: 20px; }

  .course-item {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 20px; padding: 16px 18px;
    display: flex; align-items: center; gap: 14px;
    animation: fadeUp 0.25s ease both;
    transition: all 0.2s;
  }
  .course-item.checked { opacity: 0.45; }
  .course-item.checked .course-name { text-decoration: line-through; }

  .course-check {
    width: 26px; height: 26px; flex-shrink: 0;
    border-radius: 8px; border: 2px solid var(--border);
    background: var(--bg2); cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px; transition: all 0.2s;
  }
  .course-check.checked { background: var(--ok); border-color: var(--ok); }

  .course-info { flex: 1; min-width: 0; }
  .course-name {
    font-family: var(--font-display);
    font-size: 15px; font-weight: 700; color: var(--text);
  }
  .course-source { font-size: 11px; color: var(--muted); font-weight: 500; margin-top: 2px; }

  .course-tag {
    font-size: 10px; font-weight: 700; padding: 3px 10px; border-radius: 8px;
    flex-shrink: 0;
  }
  .course-tag-expire { background: rgba(239,68,68,0.1); color: var(--danger); border: 1px solid rgba(239,68,68,0.2); }
  .course-tag-recipe { background: rgba(167,139,250,0.1); color: var(--accent2); border: 1px solid rgba(167,139,250,0.2); }
  .course-tag-manual { background: rgba(91,140,255,0.1); color: var(--accent); border: 1px solid rgba(91,140,255,0.2); }

  .course-del {
    width: 30px; height: 30px; border-radius: 10px; flex-shrink: 0;
    background: none; border: 1px solid transparent;
    color: var(--muted); font-size: 14px; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
  }
  .course-del:active { background: rgba(239,68,68,0.1); color: var(--danger); }

  .courses-cta {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 24px; padding: 20px; margin-bottom: 20px;
    animation: fadeUp 0.3s ease;
  }
  .courses-cta-hint { font-size: 12px; color: var(--muted); text-align: center; margin-top: 10px; font-weight: 500; }

  .csm-item {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 16px; padding: 14px 16px;
    margin-bottom: 10px;
  }
  .csm-item-name {
    font-family: var(--font-display); font-size: 15px; font-weight: 700;
    color: var(--text); margin-bottom: 10px;
  }
  .csm-row { display: flex; gap: 8px; }
  .csm-row .field { font-size: 13px; padding: 10px 12px; }

  .header-icon-btn {
    width: 40px; height: 40px; border-radius: 14px;
    background: var(--surface2); border: 1px solid var(--border);
    font-size: 18px; cursor: pointer; transition: all 0.2s;
    display: flex; align-items: center; justify-content: center;
  }
  .header-icon-btn:active { transform: scale(0.9); }

  .date-shortcuts { display: flex; gap: 6px; flex-wrap: wrap; margin-bottom: 10px; }
  .date-shortcut {
    padding: 6px 12px; border-radius: 10px;
    background: var(--surface2); border: 1px solid var(--border);
    color: var(--muted); font-size: 11px; font-weight: 700;
    cursor: pointer; transition: all 0.15s; font-family: var(--font-display);
  }
  .date-shortcut:active { background: var(--accent); color: #fff; border-color: var(--accent); }

  .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
  .stats-big-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 20px; padding: 18px; text-align: center;
    animation: fadeUp 0.3s ease both;
  }
  .stats-big-num { font-family: var(--font-display); font-size: 36px; font-weight: 900; }
  .stats-big-label { font-size: 11px; color: var(--muted); font-weight: 600; margin-top: 4px; }
  .stats-big-icon { font-size: 24px; margin-bottom: 6px; }

  .stats-categories { display: flex; flex-direction: column; gap: 10px; }
  .stats-cat-row { display: flex; align-items: center; gap: 10px; }
  .stats-cat-label { font-family: var(--font-display); font-size: 12px; font-weight: 700; width: 80px; flex-shrink: 0; }
  .stats-cat-bar-wrap { flex: 1; height: 8px; background: var(--surface2); border-radius: 4px; overflow: hidden; }
  .stats-cat-bar { height: 100%; border-radius: 4px; transition: width 0.6s ease; }
  .stats-cat-count { font-size: 11px; color: var(--muted); font-weight: 600; width: 24px; text-align: right; }

  .diet-filters { display: flex; gap: 8px; flex-wrap: wrap; }
  .diet-btn {
    padding: 8px 14px; border-radius: 12px;
    background: var(--surface); border: 1px solid var(--border);
    color: var(--muted); font-size: 12px; font-weight: 700;
    cursor: pointer; transition: all 0.2s; font-family: var(--font-display);
  }
  .diet-btn.active { background: rgba(52,211,153,0.12); border-color: rgba(52,211,153,0.4); color: var(--ok); }

  .meal-history { display: flex; flex-direction: column; gap: 8px; margin-bottom: 8px; }
  .history-item {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 16px; padding: 12px 16px;
    display: flex; align-items: center; gap: 12px;
    animation: fadeUp 0.2s ease;
  }
  .history-emoji { font-size: 22px; }
  .history-info { flex: 1; }
  .history-name { font-family: var(--font-display); font-size: 14px; font-weight: 700; color: var(--text); }
  .history-date { font-size: 11px; color: var(--muted); margin-top: 2px; }
  .history-persons { font-size: 11px; color: var(--accent); font-weight: 600; }

  .waste-card { background: var(--surface); border: 1px solid var(--border); border-radius: 20px; padding: 20px; }
  .waste-title { font-family: var(--font-display); font-size: 14px; font-weight: 800; color: var(--text); margin-bottom: 14px; }
  .waste-bar-wrap { height: 10px; background: var(--surface2); border-radius: 5px; overflow: hidden; margin-bottom: 8px; }
  .waste-bar { height: 100%; border-radius: 5px; background: linear-gradient(90deg, var(--ok), var(--warn)); transition: width 0.8s ease; }
  .waste-label { font-size: 12px; color: var(--muted); font-weight: 600; }

  body.light {
    --bg: #f4f5f8; --bg2: #ffffff; --surface: #ffffff; --surface2: #eef0f6;
    --border: rgba(0,0,0,0.08); --text: #1a1d27; --muted: #6b7280;
  }
  body.light header { background: rgba(244,245,248,0.95); }
  body.light nav { background: rgba(244,245,248,0.95); }
  body.light .glow-orb-1 { background: rgba(91,140,255,0.06); }
  body.light .glow-orb-2 { background: rgba(167,139,250,0.04); }

  .item-note {
    position: absolute; top: 10px; right: 36px;
    width: 26px; height: 26px; border-radius: 8px;
    background: transparent; border: none;
    font-size: 14px; cursor: pointer; opacity: 0;
    transition: opacity 0.2s; display: flex;
    align-items: center; justify-content: center;
  }
  .item-card:hover .item-note { opacity: 1; }
  @media (hover: none) { .item-note { opacity: 0.6 !important; } }
  .item-note-badge {
    position: absolute; top: 8px; right: 34px;
    font-size: 12px; opacity: 0.7;
  }

  .budget-presets { display: flex; gap: 8px; flex-wrap: wrap; }
  .budget-result-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 16px; padding: 14px 16px; margin-bottom: 8px;
    display: flex; align-items: center; gap: 12px;
  }
  .budget-result-price {
    font-family: var(--font-display); font-size: 18px; font-weight: 900;
    color: var(--ok); flex-shrink: 0;
  }

  #pwa-banner {
    position: fixed; bottom: 96px; left: 16px; right: 16px;
    background: linear-gradient(135deg, #1e1b4b, #312e81);
    border: 1px solid rgba(167,139,250,0.3);
    border-radius: 20px; padding: 16px 18px;
    display: flex; align-items: center; gap: 12px;
    z-index: 50; animation: fadeUp 0.3s ease;
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
  }
  #pwa-banner .pwa-icon { font-size: 28px; }
  #pwa-banner .pwa-text { flex: 1; }
  #pwa-banner .pwa-title { font-family: var(--font-display); font-size: 13px; font-weight: 800; color: #fff; }
  #pwa-banner .pwa-sub { font-size: 11px; color: rgba(255,255,255,0.6); margin-top: 2px; }
  #pwa-banner .pwa-btn {
    background: rgba(167,139,250,0.2); border: 1px solid rgba(167,139,250,0.4);
    color: #a78bfa; border-radius: 10px; padding: 8px 14px;
    font-size: 12px; font-weight: 700; cursor: pointer; white-space: nowrap;
  }
  #pwa-banner .pwa-close {
    background: none; border: none; color: rgba(255,255,255,0.4);
    font-size: 16px; cursor: pointer; padding: 4px;
  }

  .nutri-badge {
    display: inline-block; padding: 2px 6px; border-radius: 6px;
    font-size: 9px; font-weight: 700; font-family: var(--font-display);
    margin-left: 4px; letter-spacing: 0.05em;
  }
  .nutri-a { background: rgba(52,211,153,0.15); color: var(--ok); }
  .nutri-b { background: rgba(132,204,22,0.15); color: #84cc16; }
  .nutri-c { background: rgba(245,158,11,0.15); color: var(--warn); }
  .nutri-d { background: rgba(249,115,22,0.15); color: #f97316; }
  .nutri-e { background: rgba(239,68,68,0.15); color: var(--danger); }

/* NEW FEATURES */
.item-note-btn{opacity:0.4;transition:opacity 0.2s}
.item-card:hover .item-note-btn{opacity:1}
@media(hover:none){.item-note-btn{opacity:0.7!important}}
.item-fav{width:30px;height:30px;border-radius:10px;background:none;border:none;font-size:16px;cursor:pointer;opacity:0.4;transition:all 0.2s;display:flex;align-items:center;justify-content:center}
.item-fav.active{opacity:1}
.item-fav:active{transform:scale(1.3)}
.user-chip{display:flex;flex-direction:column;align-items:center;gap:6px;cursor:pointer;flex-shrink:0}
.user-avatar{width:48px;height:48px;border-radius:16px;background:var(--surface2);border:2px solid transparent;display:flex;align-items:center;justify-content:center;font-size:20px;transition:all 0.2s;overflow:hidden}
.user-avatar img{width:100%;height:100%;object-fit:cover}
.user-avatar.active{border-color:var(--accent);box-shadow:0 0 0 2px rgba(91,140,255,0.3)}
.user-chip-name{font-family:var(--font-display);font-size:10px;font-weight:800;color:var(--muted)}
.user-chip.active .user-chip-name{color:var(--accent)}
.user-add-btn{width:48px;height:48px;border-radius:16px;background:var(--surface);border:1.5px dashed rgba(255,255,255,0.15);display:flex;align-items:center;justify-content:center;font-size:22px;color:var(--muted);cursor:pointer;transition:all 0.2s}
.users-row{display:flex;gap:10px;margin-bottom:16px;overflow-x:auto;padding-bottom:4px;scrollbar-width:none}
.users-row::-webkit-scrollbar{display:none}
.recipe-fav-btn{position:absolute;top:12px;right:12px;background:none;border:none;font-size:18px;cursor:pointer;opacity:0.5;transition:all 0.2s}
.recipe-fav-btn.active{opacity:1}
.fav-section{margin-bottom:20px}
.fav-title{font-family:var(--font-display);font-size:16px;font-weight:800;color:var(--text);margin-bottom:12px;display:flex;align-items:center;gap:8px}
.country-chips{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:16px;scrollbar-width:none}
.country-chips::-webkit-scrollbar{display:none}
.btn-auto-planning{width:100%;padding:16px;border-radius:18px;border:none;cursor:pointer;background:linear-gradient(135deg,#fbbf24,#f59e0b);color:#000;font-family:var(--font-display);font-size:13px;font-weight:800;letter-spacing:0.1em;margin-bottom:16px;transition:all 0.2s;box-shadow:0 8px 24px rgba(245,158,11,0.4)}
.btn-auto-planning:active{transform:scale(0.97)}
#cook-mode{position:fixed;inset:0;z-index:500;background:var(--bg);display:none;flex-direction:column}
#cook-mode.open{display:flex}
.cook-header{padding:50px 24px 20px;display:flex;justify-content:space-between;align-items:center}
.cook-title{font-family:var(--font-display);font-size:18px;font-weight:800;color:var(--text)}
.cook-close{width:40px;height:40px;border-radius:14px;background:var(--surface2);border:1px solid var(--border);color:var(--muted);font-size:18px;cursor:pointer;display:flex;align-items:center;justify-content:center}
.cook-progress{padding:0 24px;margin-bottom:20px}
.cook-progress-bar{height:4px;background:var(--surface2);border-radius:2px;overflow:hidden}
.cook-progress-fill{height:100%;background:linear-gradient(90deg,var(--accent2),var(--accent));border-radius:2px;transition:width 0.4s ease}
.cook-body{flex:1;overflow-y:auto;padding:0 24px}
.cook-step-num{font-family:var(--font-display);font-size:12px;font-weight:800;color:var(--muted);letter-spacing:0.12em;margin-bottom:12px}
.cook-step-title{font-family:var(--font-display);font-size:28px;font-weight:900;color:var(--text);margin-bottom:16px;line-height:1.1}
.cook-step-detail{font-size:17px;color:var(--text);line-height:1.7;opacity:0.85;margin-bottom:32px}
.cook-timer-wrap{background:var(--surface);border:1px solid var(--border);border-radius:24px;padding:24px;text-align:center;margin-bottom:24px}
.cook-timer-display{font-family:var(--font-display);font-size:56px;font-weight:900;color:var(--accent);letter-spacing:0.05em}
.cook-timer-label{font-size:12px;color:var(--muted);font-weight:600;margin-top:4px}
.cook-timer-btns{display:flex;gap:10px;margin-top:16px;justify-content:center}
.cook-timer-btn{padding:10px 20px;border-radius:12px;border:1px solid var(--border);background:var(--surface2);color:var(--text);font-family:var(--font-display);font-size:12px;font-weight:800;cursor:pointer;transition:all 0.2s}
.cook-timer-btn.start{background:var(--accent);border-color:var(--accent);box-shadow:0 4px 16px rgba(91,140,255,0.4)}
.cook-timer-btn:active{transform:scale(0.95)}
.cook-footer{padding:20px 24px 40px;display:flex;gap:12px}
.cook-prev{flex:1;padding:16px;border-radius:16px;background:var(--surface);border:1px solid var(--border);color:var(--muted);font-family:var(--font-display);font-size:13px;font-weight:800;cursor:pointer;transition:all 0.2s}
.cook-next{flex:2;padding:16px;border-radius:16px;background:var(--accent);border:none;color:#fff;font-family:var(--font-display);font-size:13px;font-weight:800;cursor:pointer;transition:all 0.2s;box-shadow:0 6px 20px rgba(91,140,255,0.4)}
.cook-finish{flex:2;padding:16px;border-radius:16px;background:linear-gradient(135deg,#059669,#34d399);border:none;color:#fff;font-family:var(--font-display);font-size:13px;font-weight:800;cursor:pointer;box-shadow:0 6px 20px rgba(52,211,153,0.4)}
.chart-wrap{background:var(--surface);border:1px solid var(--border);border-radius:20px;padding:20px;margin-bottom:16px}
.chart-title{font-family:var(--font-display);font-size:13px;font-weight:800;color:var(--text);margin-bottom:16px}
.temp-card{background:var(--surface);border:1px solid var(--border);border-radius:20px;padding:20px;margin-bottom:16px}
.temp-zones{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:16px}
.temp-zone{background:var(--bg2);border:1px solid var(--border);border-radius:16px;padding:16px;text-align:center;cursor:pointer;transition:all 0.2s}
.temp-zone:active{transform:scale(0.97)}
.temp-zone-icon{font-size:28px;margin-bottom:8px}
.temp-zone-label{font-family:var(--font-display);font-size:11px;font-weight:800;color:var(--muted);text-transform:uppercase;letter-spacing:0.1em;margin-bottom:6px}
.temp-zone-val{font-family:var(--font-display);font-size:28px;font-weight:900}
.temp-zone-val.ok{color:var(--ok)}
.temp-zone-val.warn{color:var(--warn)}
.temp-zone-val.danger{color:var(--danger)}
.temp-zone-ideal{font-size:10px;color:var(--muted);margin-top:2px}
.temp-history{display:flex;flex-direction:column;gap:6px}
.temp-entry{display:flex;justify-content:space-between;align-items:center;padding:8px 12px;background:var(--bg2);border-radius:10px;font-size:12px}
.temp-entry-val{font-family:var(--font-display);font-weight:800}
.note-tags{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:12px}
.note-tag-btn{padding:5px 12px;border-radius:100px;border:1px solid var(--border);background:var(--surface);color:var(--muted);font-size:11px;font-weight:700;cursor:pointer;transition:all 0.2s}
.note-tag-btn.active{background:var(--accent2);border-color:var(--accent2);color:#fff}
.note-photo-preview{width:100%;border-radius:14px;max-height:160px;object-fit:cover;margin-bottom:10px;display:none}
.ocr-items-list{display:flex;flex-direction:column;gap:8px;margin-bottom:16px}
.ocr-item{display:flex;align-items:center;gap:10px;background:var(--surface);border:1px solid var(--border);border-radius:14px;padding:10px 14px}
.ocr-item-name{font-family:var(--font-display);font-size:13px;font-weight:700;flex:1}
.ocr-item-check{width:24px;height:24px;border-radius:8px;border:2px solid var(--border);background:var(--bg2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:12px;transition:all 0.2s;flex-shrink:0}
.ocr-item-check.checked{background:var(--ok);border-color:var(--ok)}
.ocr-preview{width:100%;max-height:200px;border-radius:16px;object-fit:contain;background:var(--surface2);margin-bottom:12px;display:none}
.profile-photo-wrap{display:flex;flex-direction:column;align-items:center;gap:12px;margin-bottom:24px}
.profile-photo-big{width:90px;height:90px;border-radius:28px;background:var(--surface2);border:2px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:40px;overflow:hidden;cursor:pointer;position:relative}
.profile-photo-big img{width:100%;height:100%;object-fit:cover}
.profile-photo-overlay{position:absolute;bottom:0;left:0;right:0;background:rgba(0,0,0,0.5);padding:5px;text-align:center;font-size:11px;font-weight:700;color:#fff}
.members-list{display:flex;flex-direction:column;gap:8px;margin-bottom:12px}
body.light{--bg:#f4f5f8;--bg2:#ffffff;--surface:#ffffff;--surface2:#eef0f6;--border:rgba(0,0,0,0.08);--text:#1a1d27;--muted:#6b7280}
body.light nav{background:rgba(244,245,248,0.95)}

/* ── STYLE MARMITON ── */
.marmiton-badge {
  position:absolute; bottom:-2px; right:-2px;
  width:18px; height:18px; border-radius:50%;
  background:linear-gradient(135deg,#FF6B35,#FF8C42);
  color:#fff; font-size:10px; font-weight:900;
  display:flex; align-items:center; justify-content:center;
  box-shadow:0 2px 6px rgba(255,107,53,0.5); z-index:2;
}
.recipe-thumb {
  width:72px; height:72px; border-radius:16px;
  background:var(--surface2); display:flex; align-items:center;
  justify-content:center; overflow:hidden; flex-shrink:0;
}
.recipe-card-img {
  width:100%; height:100%; object-fit:cover; border-radius:16px;
}
.recipe-stars { font-size:12px; color:#FF6B35; letter-spacing:2px; margin-top:3px; }
.marmiton-note-row {
  display:flex; align-items:center; gap:8px;
  background:rgba(255,107,53,0.08); border:1px solid rgba(255,107,53,0.2);
  border-radius:14px; padding:10px 14px; margin-bottom:18px;
}
.marmiton-stars { font-size:18px; color:#FF6B35; letter-spacing:1px; }
.marmiton-note-val { font-family:var(--font-display); font-size:18px; font-weight:900; color:#FF6B35; }
.marmiton-note-avis { font-size:12px; color:var(--muted); font-weight:500; }
.marmiton-meta-row { display:grid; grid-template-columns:1fr 1fr 1fr 1fr; gap:8px; margin-bottom:20px; }
.marmiton-meta-item { display:flex; flex-direction:column; align-items:center; gap:3px; background:var(--surface2); border:1px solid var(--border); border-radius:14px; padding:12px 8px; text-align:center; }
.marmiton-meta-icon { font-size:18px; }
.marmiton-meta-label { font-size:9px; color:var(--muted); font-weight:700; letter-spacing:0.08em; text-transform:uppercase; }
.marmiton-meta-val { font-family:var(--font-display); font-size:12px; font-weight:800; color:var(--text); }
.marmiton-conseil { display:flex; gap:10px; align-items:flex-start; background:rgba(255,107,53,0.07); border:1px solid rgba(255,107,53,0.18); border-radius:16px; padding:14px 16px; margin:18px 0; font-size:13px; color:var(--text); line-height:1.5; }
.marmiton-conseil-icon { font-size:18px; flex-shrink:0; }
.marmiton-source-badge { text-align:center; font-size:11px; color:var(--muted); margin:20px 0 8px; padding:8px; border-radius:10px; background:var(--surface2); border:1px solid var(--border); }
.marmiton-source-badge strong { color:#FF6B35; }
.recipe-modal-photo-wrap { width:100%; height:180px; border-radius:20px; overflow:hidden; background:var(--surface2); display:flex; align-items:center; justify-content:center; margin-bottom:20px; }
.recipe-modal-full-img { width:100%; height:100%; object-fit:cover; }
.recipe-img-placeholder { display:flex; align-items:center; justify-content:center; width:100%; height:100%; }
#country-chips .chip.active { background:#FF6B35; border-color:#FF6B35; }
.recipe-card { position:relative; }
.diet-btn.active { background:rgba(255,107,53,0.12); border-color:rgba(255,107,53,0.4); color:#FF6B35; }

</style>
</head>
<body>
<div class="glow-orb glow-orb-1"></div>
<div class="glow-orb glow-orb-2"></div>
<div id="toast"></div>

<header style="background:var(--bg);">
  <div>
    <div class="header-eyebrow">Tableau de bord</div>
    <h1 class="header-name" id="header-name">Mathis</h1>
  </div>
  <div style="display:flex;align-items:center;gap:8px">
    <button class="header-icon-btn" id="notif-btn" onclick="requestNotifPermission()" title="Notifications">&#128276;</button>
    <button class="header-icon-btn" id="theme-btn" onclick="toggleTheme()" title="Theme">&#9728;&#65039;</button>
    <div class="avatar" id="main-avatar" onclick="openProfileModal()">&#128100;</div>
  </div>
</header>

<main>
<!-- ═══ STOCK TAB ═══ -->
<section id="stock" class="tab-content active">
  <div style="flex-shrink:0; position:sticky; top:0; z-index:20; background:var(--bg); padding-top:8px">
    <div class="users-row" id="users-row"></div>
    <div class="stats-row">
    <div class="stat-card stat-card-blue"><div class="stat-icon">&#128230;</div><div class="stat-num" id="total-items">&mdash;</div><div class="stat-label">Articles</div></div>
    <div class="stat-card stat-card-orange"><div class="stat-icon">&#9889;</div><div class="stat-num" id="urgent-items">&mdash;</div><div class="stat-label">Urgents</div></div>
  </div>
  </div>
  <div class="inv-header" onclick="toggleInventory()" style="flex-shrink:0">
    <span class="section-title">Inventaire</span>
    <div style="display:flex;align-items:center;gap:8px">
      <button class="btn-refresh" onclick="event.stopPropagation();fetchStock()">&#8635;</button>
      <span id="inv-chevron" class="inv-chevron open">&#9662;</span>
    </div>
  </div>
  <div id="inv-collapsible" class="inv-collapsible open">
    <div class="chips" id="filter-chips">
      <div class="chip active" onclick="filterItems('Tous',this)">Tous</div>
      <div class="chip" onclick="filterItems('Frigo',this)">&#10052;&#65039; Frigo</div>
      <div class="chip" onclick="filterItems('Placard',this)">&#129379; Placard</div>
      <div class="chip" onclick="filterItems('Congelo',this)">&#129408; Cong&eacute;lo</div>
      <div class="chip" onclick="filterItems('Cave',this)">&#127863; Cave</div>
      <div class="chip" onclick="filterItems('Urgent',this)">&#9889; Urgents</div>
      <div class="chip" onclick="filterItems('Favoris',this)">&#11088; Favoris</div>
    </div>
    <div id="stock-list" class="stock-list">
      <div class="skeleton"></div><div class="skeleton" style="animation-delay:.1s"></div><div class="skeleton" style="animation-delay:.2s"></div>
    </div>
  </div>
</section>

<!-- ═══ CHEF TAB ═══ -->
<section id="menu" class="tab-content">
  <div class="chef-header">
    <div class="chef-badge">&#10022; IA</div>
    <h2 class="chef-title">Suggestion<br>du Chef</h2>
    <p class="chef-sub">Recettes g&eacute;n&eacute;r&eacute;es d&apos;apr&egrave;s ton stock actuel</p>
  </div>
  <div class="country-chips chips" id="country-chips">
    <div class="chip active" onclick="filterCountry('',this)">&#127758; Toutes</div>
    <div class="chip" onclick="filterCountry('French',this)">&#127467;&#127479; Fran&ccedil;aise</div>
    <div class="chip" onclick="filterCountry('Italian',this)">&#127470;&#127481; Italienne</div>
    <div class="chip" onclick="filterCountry('American',this)">&#127482;&#127480; Am&eacute;ricaine</div>
    <div class="chip" onclick="filterCountry('Chinese',this)">&#127464;&#127475; Chinoise</div>
    <div class="chip" onclick="filterCountry('Indian',this)">&#127470;&#127475; Indienne</div>
    <div class="chip" onclick="filterCountry('Mexican',this)">&#127474;&#127485; Mexicaine</div>
    <div class="chip" onclick="filterCountry('Japanese',this)">&#127471;&#127477; Japonaise</div>
    <div class="chip" onclick="filterCountry('Moroccan',this)">&#127474;&#127462; Marocaine</div>
  </div>
  <button class="btn-chef-generate" id="btn-generate" onclick="generateRecipes()">
    <span class="chef-btn-icon">&#128104;&#8205;&#127859;</span><span>G&eacute;n&eacute;rer des recettes</span><span class="chef-btn-arrow">&rarr;</span>
  </button>
  <div id="chef-loading" style="display:none" class="chef-loading"><div class="chef-dots"><span></span><span></span><span></span></div><p>Le chef analyse votre frigo&hellip;</p></div>
  <div id="fav-section" class="fav-section" style="display:none">
    <div class="fav-title">&#11088; Recettes favorites <span id="fav-count" style="font-size:12px;color:var(--muted);font-weight:600"></span></div>
    <div id="fav-list" class="recipe-list" style="margin-bottom:20px"></div>
  </div>
  <div id="recipe-list" class="recipe-list"></div>
  <div class="planning-wrap">
    <div class="planning-header">
      <div><div class="chef-badge" style="background:rgba(251,191,36,0.1);border-color:rgba(251,191,36,0.25);color:#fbbf24;margin-bottom:8px">&#128197; Planning</div><h3 class="planning-title">Semaine du chef</h3></div>
      <button class="planning-reset" onclick="resetPlanning()">&#8635;</button>
    </div>
    <button class="btn-auto-planning" onclick="autoFillPlanning()">&#9889; G&eacute;n&eacute;rer le planning automatiquement</button>
    <div id="planning-days" class="planning-days"></div>
  </div>

  <!-- Recipe modal -->
  <div id="recipe-modal" class="recipe-modal">
    <div class="recipe-modal-inner">
      <div class="recipe-modal-header">
        <div><div class="recipe-modal-emoji" id="modal-emoji">&#127859;</div><h2 class="recipe-modal-title" id="modal-title">&mdash;</h2><p class="recipe-modal-meta" id="modal-meta">&mdash;</p></div>
        <div style="display:flex;gap:8px;align-items:center">
          <button id="modal-fav-btn" onclick="toggleModalFav()" style="font-size:24px;background:none;border:none;cursor:pointer;opacity:0.5;transition:all 0.2s">&#9825;</button>
          <button class="recipe-modal-close" onclick="closeRecipeModal()">&#10005;</button>
        </div>
      </div>
      <div class="recipe-modal-body" id="modal-body"></div>
    </div>
  </div>

  <!-- Planning modal -->
  <div id="planning-modal" class="recipe-modal">
    <div class="recipe-modal-inner" style="max-height:80dvh">
      <div class="recipe-modal-header" style="margin-bottom:16px">
        <div><div style="font-size:28px;margin-bottom:4px" id="pm-day-icon">&#128197;</div><h2 class="recipe-modal-title" id="pm-day-title">Lundi</h2><p class="recipe-modal-meta" id="pm-slot-label">D&eacute;jeuner</p></div>
        <button class="recipe-modal-close" onclick="closePlanningModal()">&#10005;</button>
      </div>
      <div class="pm-custom-row"><input type="text" id="pm-custom-input" class="field" placeholder="Saisir un plat&hellip;"><button class="pm-custom-btn" onclick="setPlanningCustom()">+</button></div>
      <div id="pm-recipe-pick"><div class="pm-section-label">&mdash; ou choisir parmi les suggestions &mdash;</div><div id="pm-recipe-list" class="pm-recipe-list"></div></div>
      <button class="pm-clear-btn" id="pm-clear-btn" onclick="clearPlanningSlot()" style="display:none">&#128465; Effacer ce repas</button>
    </div>
  </div>
</section>

<!-- ═══ COOK MODE ═══ -->
<div id="cook-mode">
  <div class="cook-header"><span class="cook-title" id="cook-recipe-title">Recette</span><button class="cook-close" onclick="closeCookMode()">&#10005;</button></div>
  <div class="cook-progress"><div class="cook-progress-bar"><div class="cook-progress-fill" id="cook-progress-fill" style="width:0%"></div></div></div>
  <div class="cook-body">
    <div class="cook-step-num" id="cook-step-num">ÉTAPE 1 / 1</div>
    <div class="cook-step-title" id="cook-step-title"></div>
    <div class="cook-step-detail" id="cook-step-detail"></div>
    <div class="cook-timer-wrap" id="cook-timer-wrap" style="display:none">
      <div class="cook-timer-display" id="cook-timer-display">05:00</div>
      <div class="cook-timer-label">Minuteur</div>
      <div class="cook-timer-btns">
        <button class="cook-timer-btn start" onclick="startTimer()" id="cook-timer-start-btn">&#9654; D&eacute;marrer</button>
        <button class="cook-timer-btn" onclick="resetTimer()">&#9632; Reset</button>
      </div>
    </div>
  </div>
  <div class="cook-footer">
    <button class="cook-prev" id="cook-prev-btn" onclick="cookPrev()" style="display:none">&#8592; Pr&eacute;c.</button>
    <button class="cook-next" id="cook-next-btn" onclick="cookNext()">Suivant &#8594;</button>
    <button class="cook-finish" id="cook-finish-btn" onclick="cookFinish()" style="display:none">&#127869;&#65039; Terminer</button>
  </div>
</div>

<!-- ═══ SCAN MODAL ═══ -->
<div id="scan-modal">
  <div class="scan-header"><span class="scan-title">&#128248; Scanner</span><button class="scan-close" onclick="closeScanner()">&#10005;</button></div>
  <div class="scan-viewport">
    <div id="scan-video-wrap" style="width:100%;height:100%;border-radius:28px;overflow:hidden;"></div>
    <div class="scan-laser"></div>
  </div>
  <p class="scan-status" id="scan-status">Pointez sur un code-barres&hellip;</p>
  <div id="scan-result-panel">
    <div class="result-product-name" id="res-name">&mdash;</div>
    <div class="result-brand" id="res-brand">&mdash;</div>
    <div class="result-fields">
      <div style="display:flex;gap:8px;align-items:center">
        <div id="res-photo-preview" onclick="takeProductPhoto('scan')" style="width:50px;height:50px;border-radius:12px;background:var(--surface2);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0;overflow:hidden;cursor:pointer">&#128247;</div>
        <select id="res-cat" class="field"><option>Frigo</option><option>Placard</option><option>Congelo</option><option>Cave</option></select>
      </div>
      <div class="fields-row">
        <input type="number" id="res-qty" value="1" min="1" class="field field-qty">
        <select id="res-unit" class="field" style="flex:1"><option value="piece">pi&egrave;ce(s)</option><option value="g">g</option><option value="kg">kg</option><option value="ml">ml</option><option value="l">L</option></select>
        <input type="date" id="res-date" class="field">
      </div>
    </div>
    <button class="btn-scan-add" onclick="saveScanResult()">&#10003; Ajouter au stock</button>
    <button class="btn-scan-again" onclick="restartScan()">&#8635; Scanner autre produit</button>
  </div>
</div>

<!-- ═══ COURSES TAB ═══ -->
<section id="courses" class="tab-content">
  <div class="chef-header">
    <div class="chef-badge" style="background:rgba(52,211,153,0.1);border-color:rgba(52,211,153,0.25);color:var(--ok)">&#128722; Liste</div>
    <h2 class="chef-title" style="font-size:32px">Ma Liste<br>de Courses</h2>
    <p class="chef-sub">Articles manquants et produits expir&eacute;s &agrave; racheter</p>
  </div>
  <div class="courses-sources">
    <button class="source-btn active" id="src-expire" onclick="toggleSource('expire',this)">&#9889; Expir&eacute;s</button>
    <button class="source-btn" id="src-recettes" onclick="toggleSource('recettes',this)">&#128104;&#8205;&#127859; Recettes</button>
  </div>
  <!-- OCR Ticket -->
  <div class="card" style="margin-bottom:16px">
    <div class="card-title">&#128247; Scanner un ticket de caisse</div>
    <input type="file" id="ticket-file" accept="image/*" style="display:none" onchange="processTicket(event)">
    <button class="btn-primary" style="background:linear-gradient(135deg,#0f172a,#1e3a8a)" onclick="document.getElementById('ticket-file').click()">&#128247; Prendre une photo du ticket</button>
    <div id="ocr-result" style="display:none;margin-top:14px">
      <img id="ocr-preview" class="ocr-preview">
      <div id="ocr-items-list" class="ocr-items-list"></div>
      <button class="btn-primary" style="background:linear-gradient(135deg,#059669,#34d399);margin-top:8px" onclick="addOcrItemsToList()">&#10003; Ajouter les articles s&eacute;lectionn&eacute;s</button>
    </div>
  </div>
  <div class="card" style="margin-bottom:16px">
    <div class="card-title">&#10022; Ajouter manuellement</div>
    <div class="fields-row" style="gap:8px">
      <input type="text" id="course-name" class="field" placeholder="Ex: Beurre, Lait&hellip;" style="flex:1">
      <button class="btn-primary" style="width:auto;padding:14px 18px;border-radius:14px" onclick="addManualCourse()">+</button>
    </div>
  </div>
  <div class="section-header">
    <span class="section-title" id="courses-count">0 article</span>
    <button class="btn-refresh" onclick="clearChecked()" id="btn-clear-checked" style="display:none;background:rgba(239,68,68,0.1);color:var(--danger)">&#128465; Supprimer coch&eacute;s</button>
  </div>
  <div id="courses-list" class="courses-list"><div class="empty"><div class="empty-icon">&#128722;</div><div class="empty-text">Aucun article pour l'instant</div></div></div>
  <div id="courses-share-wrap" style="display:none;margin-bottom:12px">
    <button class="btn-share-list" onclick="openShareModal()"><span class="share-btn-icon">&#8599;</span><div class="share-btn-text"><span class="share-btn-title">Envoyer la liste</span><span class="share-btn-sub">WhatsApp &middot; Drive &middot; Email&hellip;</span></div><span style="font-size:20px;color:var(--muted)">&rsaquo;</span></button>
    <button class="btn-share-list" style="margin-top:8px;border-color:rgba(52,211,153,0.3);background:rgba(52,211,153,0.06)" onclick="openSupermarketModal()"><span class="share-btn-icon" style="background:linear-gradient(135deg,#059669,#34d399)">&#127978;</span><div class="share-btn-text"><span class="share-btn-title">Cr&eacute;er un panier en ligne</span><span class="share-btn-sub">Leclerc &middot; Carrefour &middot; Auchan&hellip;</span></div><span style="font-size:20px;color:var(--muted)">&rsaquo;</span></button>
  </div>
  <div id="courses-cta" style="display:none" class="courses-cta">
    <button class="btn-cook" style="background:linear-gradient(135deg,#1d4ed8,#5b8cff);box-shadow:0 10px 30px rgba(91,140,255,0.4)" onclick="addCheckedToStock()"><span>&#128230;</span> Ajouter au stock</button>
    <p class="courses-cta-hint">Les articles coch&eacute;s seront ajout&eacute;s &agrave; votre r&eacute;serve</p>
  </div>
  <!-- Share modal -->
  <div id="share-modal" class="recipe-modal">
    <div class="recipe-modal-inner" style="max-height:85dvh;padding-bottom:40px">
      <div class="recipe-modal-header" style="margin-bottom:20px"><div><div style="font-size:32px;margin-bottom:6px">&#8599;</div><h2 class="recipe-modal-title">Partager la liste</h2><p class="recipe-modal-meta" id="share-count-label"></p></div><button class="recipe-modal-close" onclick="closeShareModal()">&#10005;</button></div>
      <div class="share-preview" id="share-preview"></div>
      <div class="share-grid">
        <button class="share-option" onclick="shareWhatsApp()"><div class="share-option-icon" style="background:rgba(37,211,102,0.15);border-color:rgba(37,211,102,0.25)"><svg viewBox="0 0 24 24" fill="#25d366" width="26" height="26"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347z"/><path d="M12 0C5.373 0 0 5.373 0 12c0 2.108.547 4.088 1.502 5.814L0 24l6.335-1.482A11.945 11.945 0 0012 24c6.627 0 12-5.373 12-12S18.627 0 12 0zm0 21.818a9.818 9.818 0 01-5.015-1.374l-.36-.214-3.732.872.944-3.641-.234-.374A9.818 9.818 0 012.182 12C2.182 6.58 6.58 2.182 12 2.182S21.818 6.58 21.818 12 17.42 21.818 12 21.818z"/></svg></div><span>WhatsApp</span></button>
        <button class="share-option" onclick="shareEmail()"><div class="share-option-icon" style="background:rgba(234,88,12,0.12);border-color:rgba(234,88,12,0.2)"><svg viewBox="0 0 24 24" fill="none" stroke="#ea580c" stroke-width="2" width="24" height="24"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m2 7 10 7 10-7"/></svg></div><span>Email</span></button>
        <button class="share-option" onclick="copyToClipboard()"><div class="share-option-icon" style="background:rgba(91,140,255,0.12);border-color:rgba(91,140,255,0.2)"><svg viewBox="0 0 24 24" fill="none" stroke="#5b8cff" stroke-width="2" width="24" height="24"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 01-2-2V4a2 2 0 012-2h9a2 2 0 012 2v1"/></svg></div><span>Copier</span></button>
        <button class="share-option" onclick="shareNative()"><div class="share-option-icon" style="background:rgba(167,139,250,0.12);border-color:rgba(167,139,250,0.2)"><svg viewBox="0 0 24 24" fill="none" stroke="#a78bfa" stroke-width="2" width="24" height="24"><circle cx="18" cy="5" r="3"/><circle cx="6" cy="12" r="3"/><circle cx="18" cy="19" r="3"/><path d="m8.59 13.51 6.83 3.98M15.41 6.51l-6.82 3.98"/></svg></div><span>Partager</span></button>
        <button class="share-option" onclick="downloadTxt()"><div class="share-option-icon" style="background:rgba(52,211,153,0.1);border-color:rgba(52,211,153,0.2)"><svg viewBox="0 0 24 24" fill="none" stroke="#34d399" stroke-width="2" width="24" height="24"><path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg></div><span>.txt</span></button>
        <button class="share-option" onclick="openGoogleDrive()"><div class="share-option-icon" style="background:rgba(66,133,244,0.12);border-color:rgba(66,133,244,0.2)"><svg viewBox="0 0 87.3 78" width="26" height="26"><path d="M6.6 66.85l3.85 6.65c.8 1.4 1.95 2.5 3.3 3.3L27.5 53H0c0 1.55.4 3.1 1.2 4.5z" fill="#0066da"/><path d="M43.65 25L29.9 1.2C28.55.4 27 0 25.45 0c-1.55 0-3.1.4-4.5 1.2L6.6 10.85 23.35 40z" fill="#00ac47"/><path d="M73.55 76.8c1.35-.8 2.5-1.9 3.3-3.3l1.6-2.75 7.65-13.25c.8-1.4 1.2-2.95 1.2-4.5H59.8l5.45 10z" fill="#ea4335"/><path d="M43.65 25L57.4 1.2C56 .4 54.45 0 52.9 0H34.4c-1.55 0-3.1.4-4.5 1.2z" fill="#00832d"/><path d="M59.8 53H27.5L13.75 76.8c1.4.8 2.95 1.2 4.5 1.2h50.8c1.55 0 3.1-.4 4.5-1.2z" fill="#2684fc"/><path d="M73.4 10.85L59.65 1.2C58.3.4 56.75 0 55.2 0c-1.55 0-3.1.4-4.5 1.2L36.95 25l20.3 35z" fill="#ffba00"/></svg></div><span>Drive</span></button>
      </div>
    </div>
  </div>
  <!-- Supermarket modal -->
  <div id="supermarket-modal" class="recipe-modal">
    <div class="recipe-modal-inner" style="max-height:90dvh;padding-bottom:44px">
      <div class="recipe-modal-header" style="margin-bottom:16px"><div><div style="font-size:32px;margin-bottom:4px">&#127978;</div><h2 class="recipe-modal-title">Cr&eacute;er un panier</h2></div><button class="recipe-modal-close" onclick="closeSupermarketModal()">&#10005;</button></div>
      <div class="store-grid">
        <button class="store-btn" onclick="openStoreCart('leclerc')"><div class="store-logo" style="background:#0055a4;color:#fff;font-weight:900;font-size:11px">E.LECLERC</div><span class="store-name">E.Leclerc</span></button>
        <button class="store-btn" onclick="openStoreCart('carrefour')"><div class="store-logo" style="background:#004b9b;color:#e3000b;font-weight:900;font-size:16px">C</div><span class="store-name">Carrefour</span></button>
        <button class="store-btn" onclick="openStoreCart('intermarche')"><div class="store-logo" style="background:#e30613;color:#fff;font-weight:900;font-size:10px">INTER<br>MARCHE</div><span class="store-name">Intermarch&eacute;</span></button>
        <button class="store-btn" onclick="openStoreCart('auchan')"><div class="store-logo" style="background:#e4022d;color:#fff;font-weight:900;font-size:14px">auchan</div><span class="store-name">Auchan</span></button>
        <button class="store-btn" onclick="openStoreCart('lidl')"><div class="store-logo" style="background:#0050aa;color:#f5c400;font-weight:900;font-size:16px">lidl</div><span class="store-name">Lidl</span></button>
        <button class="store-btn" onclick="openStoreCart('monoprix')"><div class="store-logo" style="background:#e4022d;color:#fff;font-weight:900;font-size:10px">MONOPRIX</div><span class="store-name">Monoprix</span></button>
      </div>
      <div class="store-info"><p>&#128203; Ta liste est <strong>copi&eacute;e automatiquement</strong>. Colle-la dans la recherche du site choisi.</p></div>
    </div>
  </div>
  <!-- Course-stock modal -->
  <div id="course-stock-modal" class="recipe-modal">
    <div class="recipe-modal-inner" style="max-height:80dvh">
      <div class="recipe-modal-header"><div><div style="font-size:32px;margin-bottom:8px">&#128230;</div><h2 class="recipe-modal-title" id="csm-title">Ajouter au stock</h2></div><button class="recipe-modal-close" onclick="closeCourseModal()">&#10005;</button></div>
      <div id="csm-items"></div>
      <button class="btn-cook" onclick="confirmAddToStock()">&#10003; Confirmer l'ajout</button>
    </div>
  </div>
</section>

<!-- ═══ FAB ═══ -->
<button id="fab-btn" class="fab" onclick="openAddModal()"><span class="fab-plus">+</span></button>

<!-- ═══ ADD MODAL ═══ -->
<div id="add-modal" class="recipe-modal">
  <div class="recipe-modal-inner" style="max-height:90dvh">
    <div class="recipe-modal-header" style="margin-bottom:20px"><div><div style="font-size:28px;margin-bottom:6px">&#128230;</div><h2 class="recipe-modal-title">Ajouter un produit</h2></div><button class="recipe-modal-close" onclick="closeAddModal()">&#10005;</button></div>
    <button class="add-modal-scan-btn" onclick="closeAddModal();openScanner()"><div class="add-modal-scan-icon">&#128248;</div><div class="add-modal-scan-text"><span class="add-modal-scan-title">Scanner un code-barres</span><span class="add-modal-scan-sub">Identification automatique</span></div><span style="color:var(--muted);font-size:20px">&rsaquo;</span></button>
    <button class="add-modal-scan-btn" onclick="startVoiceInput()" style="background:rgba(167,139,250,0.08);border-color:rgba(167,139,250,0.2);margin-top:8px"><div class="add-modal-scan-icon">&#127897;&#65039;</div><div class="add-modal-scan-text"><span class="add-modal-scan-title">Ajouter par la voix</span><span class="add-modal-scan-sub" id="voice-status-label">Dictez le nom du produit</span></div><span id="voice-indicator" style="font-size:12px;color:var(--muted)">&#9679;</span></button>
    <div class="add-modal-divider"><span>ou saisie manuelle</span></div>
    <div class="form-space">
      <div style="display:flex;align-items:center;gap:12px">
        <div id="add-photo-preview" onclick="takeProductPhoto('add')" style="width:56px;height:56px;border-radius:16px;background:var(--surface2);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:24px;cursor:pointer;flex-shrink:0;overflow:hidden">&#128247;</div>
        <input type="text" id="itemName" class="field" placeholder="Nom du produit (ex: Lait)">
      </div>
      <div class="fields-row">
        <select id="itemCat" class="field"><option>Frigo</option><option>Placard</option><option>Congelo</option><option>Cave</option></select>
        <input type="text" inputmode="numeric" pattern="[0-9]*" id="itemQty" value="" placeholder="Qté" class="field field-qty">
        <select id="itemUnit" class="field" style="flex:0.8"><option value="piece">pc</option><option value="g">g</option><option value="kg">kg</option><option value="ml">ml</option><option value="l">L</option></select>
      </div>
      <input type="date" id="itemDate" class="field">
      <div class="date-shortcuts">
        <button class="date-shortcut" onclick="setDateOffset(3,this)">+3j</button>
        <button class="date-shortcut" onclick="setDateOffset(7,this)">+7j</button>
        <button class="date-shortcut" onclick="setDateOffset(14,this)">+14j</button>
        <button class="date-shortcut" onclick="setDateOffset(30,this)">+1 mois</button>
        <button class="date-shortcut" onclick="setDateOffset(180,this)">+6 mois</button>
        <button class="date-shortcut" onclick="setDateOffset(365,this)">+1 an</button>
      </div>
      <input type="file" id="product-photo-input" accept="image/*" capture="environment" style="display:none" onchange="handleProductPhoto(event)">
      <button class="btn-primary" id="save-btn" onclick="saveToCloud()">&#10003; Valider dans le Cloud</button>
    </div>
  </div>
</div>

<!-- ═══ STATS TAB ═══ -->
<section id="stats" class="tab-content">
  <div class="chef-header">
    <div class="chef-badge" style="background:rgba(91,140,255,0.1);border-color:rgba(91,140,255,0.25);color:var(--accent)">&#128202; Stats</div>
    <h2 class="chef-title" style="font-size:32px">Analyse<br>du stock</h2>
  </div>
  <div class="stats-grid" id="stats-grid"></div>
  <div class="chart-wrap" style="margin-top:20px"><div class="chart-title">&#128200; &Eacute;volution du stock (7 jours)</div><canvas id="chart-stock" height="120"></canvas></div>
  <div class="chart-wrap"><div class="chart-title">&#127859; Repas cuisin&eacute;s ce mois</div><canvas id="chart-meals" height="120"></canvas></div>
  <div class="section-header" style="margin-top:8px"><span class="section-title">R&eacute;partition par cat&eacute;gorie</span></div>
  <div id="stats-categories" class="stats-categories"></div>
  <div class="section-header" style="margin-top:20px"><span class="section-title">Filtres alimentaires</span></div>
  <div class="diet-filters" id="diet-filters">
    <button class="diet-btn" onclick="toggleDiet('vegan',this)">&#127807; Vegan</button>
    <button class="diet-btn" onclick="toggleDiet('gluten',this)">&#127806; Sans gluten</button>
    <button class="diet-btn" onclick="toggleDiet('lactose',this)">&#129371; Sans lactose</button>
    <button class="diet-btn" onclick="toggleDiet('bio',this)">&#9851;&#65039; Bio</button>
  </div>
  <div class="section-header" style="margin-top:24px">
    <span class="section-title">&#127777;&#65039; Temp&eacute;ratures</span>
    <button class="btn-refresh" onclick="openTempModal()">+ Saisir</button>
  </div>
  <div class="temp-card"><div class="temp-zones" id="temp-zones"></div><div class="temp-history" id="temp-history"></div></div>
  <div class="section-header" style="margin-top:24px">
    <span class="section-title">Historique des repas</span>
    <button class="btn-refresh" onclick="clearHistory()" style="background:rgba(239,68,68,0.1);color:var(--danger)">&#128465; Effacer</button>
  </div>
  <div id="meal-history" class="meal-history"></div>
  <div style="display:flex;gap:10px;margin-top:20px">
    <button class="btn-primary" style="flex:1;background:linear-gradient(135deg,#059669,#34d399)" onclick="document.getElementById('budget-modal').classList.add('open')">&#128176; Budget</button>
    <button class="btn-primary" style="flex:1;background:linear-gradient(135deg,#7c3aed,#a78bfa)" onclick="installPWA()">&#128241; Installer</button>
  </div>
  <div class="waste-card" style="margin-top:20px;margin-bottom:80px">
    <div class="waste-title">&#9851;&#65039; Taux de gaspillage estim&eacute;</div>
    <div class="waste-bar-wrap"><div class="waste-bar" id="waste-bar"></div></div>
    <div class="waste-label" id="waste-label">Calcul en cours&hellip;</div>
  </div>
</section>

<!-- ═══ NOTE MODAL ═══ -->
<div id="note-modal" class="recipe-modal">
  <div class="recipe-modal-inner" style="max-height:75dvh">
    <div class="recipe-modal-header" style="margin-bottom:16px"><div><div style="font-size:28px;margin-bottom:4px">&#128221;</div><h2 class="recipe-modal-title" id="note-modal-title">Note</h2></div><button class="recipe-modal-close" onclick="closeNoteModal()">&#10005;</button></div>
    <div class="note-tags" id="note-tags-row">
      <button class="note-tag-btn" data-tag="ouvert" onclick="toggleNoteTag(this,'ouvert')">&#128230; Ouvert</button>
      <button class="note-tag-btn" data-tag="promo" onclick="toggleNoteTag(this,'promo')">&#127991; Promo</button>
      <button class="note-tag-btn" data-tag="bio" onclick="toggleNoteTag(this,'bio')">&#127807; Bio</button>
      <button class="note-tag-btn" data-tag="entame" onclick="toggleNoteTag(this,'entame')">&#128290; Entam&eacute;</button>
      <button class="note-tag-btn" data-tag="congele" onclick="toggleNoteTag(this,'congele')">&#129408; Congel&eacute;</button>
    </div>
    <input type="file" id="note-photo-input" accept="image/*" capture="environment" style="display:none" onchange="handleNotePhoto(event)">
    <img id="note-photo-preview" class="note-photo-preview">
    <button onclick="document.getElementById('note-photo-input').click()" style="width:100%;padding:10px;border-radius:12px;border:1px dashed rgba(255,255,255,0.15);background:none;color:var(--muted);font-size:12px;font-weight:700;cursor:pointer;margin-bottom:10px">&#128247; Joindre une photo</button>
    <textarea id="note-input" class="field" rows="4" placeholder="Ex: Ouvert le 12/02, achet&eacute; en promo&hellip;" style="resize:none;height:100px;font-family:var(--font-body);line-height:1.5"></textarea>
    <button class="btn-primary" style="margin-top:12px" onclick="saveNote()">&#128190; Enregistrer la note</button>
  </div>
</div>

<!-- ═══ BUDGET MODAL ═══ -->
<div id="budget-modal" class="recipe-modal">
  <div class="recipe-modal-inner" style="max-height:80dvh;padding-bottom:40px">
    <div class="recipe-modal-header" style="margin-bottom:16px"><div><div style="font-size:28px;margin-bottom:4px">&#128176;</div><h2 class="recipe-modal-title">Budget courses</h2></div><button class="recipe-modal-close" onclick="document.getElementById('budget-modal').classList.remove('open')">&#10005;</button></div>
    <div class="fields-row" style="margin-bottom:16px"><input type="number" id="budget-input" class="field" placeholder="Budget en &#8364;" min="5" max="500" step="5" style="font-size:18px;font-weight:700"><button class="btn-primary" style="width:auto;padding:14px 20px;border-radius:14px" onclick="searchByBudget()">&#128269;</button></div>
    <div class="budget-presets">
      <button class="date-shortcut" onclick="document.getElementById('budget-input').value=10">10&euro;</button>
      <button class="date-shortcut" onclick="document.getElementById('budget-input').value=20">20&euro;</button>
      <button class="date-shortcut" onclick="document.getElementById('budget-input').value=30">30&euro;</button>
      <button class="date-shortcut" onclick="document.getElementById('budget-input').value=50">50&euro;</button>
    </div>
    <div id="budget-results" style="margin-top:16px"></div>
  </div>
</div>

<!-- ═══ TEMP MODAL ═══ -->
<div id="temp-modal" class="recipe-modal">
  <div class="recipe-modal-inner" style="max-height:60dvh">
    <div class="recipe-modal-header" style="margin-bottom:16px"><div><div style="font-size:28px;margin-bottom:4px">&#127777;&#65039;</div><h2 class="recipe-modal-title">Saisir une temp&eacute;rature</h2></div><button class="recipe-modal-close" onclick="closeTempModal()">&#10005;</button></div>
    <div class="form-space">
      <select id="temp-zone-select" class="field"><option value="frigo">&#10052;&#65039; Frigo (2°C – 5°C)</option><option value="congelo">&#129408; Cong&eacute;lo (-18°C – -15°C)</option><option value="cave">&#127863; Cave (10°C – 16°C)</option><option value="placard">&#129379; Placard (15°C – 22°C)</option></select>
      <div class="fields-row"><input type="number" id="temp-value" class="field" placeholder="Temp&eacute;rature" step="0.1"><span style="display:flex;align-items:center;color:var(--text);font-size:18px;font-weight:700;padding:0 8px">&deg;C</span></div>
      <button class="btn-primary" onclick="saveTemperature()">&#128190; Enregistrer</button>
    </div>
  </div>
</div>

<!-- ═══ PROFILE MODAL ═══ -->
<div id="profile-modal" class="recipe-modal">
  <div class="recipe-modal-inner" style="max-height:90dvh">
    <div class="recipe-modal-header" style="margin-bottom:16px"><div><div style="font-size:28px;margin-bottom:4px">&#128100;</div><h2 class="recipe-modal-title">Mon profil</h2></div><button class="recipe-modal-close" onclick="closeProfileModal()">&#10005;</button></div>
    <div class="profile-photo-wrap">
      <div class="profile-photo-big" id="profile-photo-big" onclick="changeProfilePhoto()"><span id="profile-emoji-display">&#128100;</span><div class="profile-photo-overlay">Changer</div></div>
      <input type="file" id="profile-photo-input" accept="image/*" style="display:none" onchange="handleProfilePhoto(event)">
    </div>
    <div class="form-space">
      <input type="text" id="profile-name-input" class="field" placeholder="Votre pr&eacute;nom">
      <button class="btn-primary" onclick="saveProfile()">&#128190; Sauvegarder le profil</button>
    </div>
    <div style="margin-top:24px">
      <div class="recipe-section-title" style="font-family:var(--font-display);font-size:11px;font-weight:800;letter-spacing:0.16em;color:var(--muted);text-transform:uppercase;margin:24px 0 12px">&#128101; Membres famille / coloc</div>
      <div id="members-list" style="display:flex;flex-direction:column;gap:8px;margin-bottom:12px"></div>
      <div class="fields-row" style="gap:8px"><input type="text" id="new-member-name" class="field" placeholder="Ajouter un membre&hellip;"><button class="btn-primary" style="width:auto;padding:14px 18px;border-radius:14px" onclick="addMember()">+</button></div>
    </div>
    <div style="margin-top:20px">
      <div style="font-family:var(--font-display);font-size:11px;font-weight:800;letter-spacing:0.16em;color:var(--muted);text-transform:uppercase;margin-bottom:12px">&#127881; Emoji avatar</div>
      <div style="display:flex;flex-wrap:wrap;gap:8px">
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#128100;')">&#128100;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#128102;')">&#128102;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#128103;')">&#128103;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#128104;')">&#128104;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#128105;')">&#128105;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#129489;')">&#129489;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#128104;&#8205;&#127859;')">&#128104;&#8205;&#127859;</span>
        <span style="font-size:28px;cursor:pointer;padding:6px;border-radius:10px" onclick="setProfileEmoji(this,'&#129307;')">&#129307;</span>
      </div>
    </div>
  </div>
</div>

</main>

<nav id="main-nav">
  <div class="nav-liquid-pill" id="nav-pill"></div>
  <button class="nav-btn active" id="btn-stock" onclick="showTab('stock')"><span class="nav-icon">&#127968;</span><span class="nav-label">R&eacute;serve</span></button>
  <button class="nav-btn" id="btn-menu" onclick="showTab('menu')"><span class="nav-icon">&#128104;&#8205;&#127859;</span><span class="nav-label">Chef IA</span></button>
  <button class="nav-btn" id="btn-courses" onclick="showTab('courses');buildCoursesList()"><span class="nav-icon">&#128722;</span><span class="nav-label">Courses</span></button>
  <button class="nav-btn" id="btn-stats" onclick="showTab('stats');renderStats()"><span class="nav-icon">&#128202;</span><span class="nav-label">Stats</span></button>
</nav>

<script>
var URL_BASE = "https://nghdlzkqutkxhxffskgq.supabase.co/rest/v1/aliment";
var API_KEY  = "sb_publishable_JdKSNEEF9pwdT1lJ-XW-Qw_d9OUxGbx";

var allItems = [], currentFilter = 'Tous', currentCountry = '';
var currentRecipes = [], activeRecipeIdx = null, currentServings = 2, BASE_SERVINGS = 2;

// ── TOAST ──
function showToast(msg, dur) {
  dur = dur || 2400;
  var t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(window._tt);
  window._tt = setTimeout(function(){ t.classList.remove('show'); }, dur);
}

// ── TAB ──
function showTab(id) {
  document.querySelectorAll('.tab-content').forEach(function(s){ s.classList.remove('active'); });
  document.querySelectorAll('.nav-btn').forEach(function(b){ b.classList.remove('active'); });
  document.getElementById(id).classList.add('active');
  document.getElementById('btn-'+id).classList.add('active');
  var fab = document.getElementById('fab-btn');
  if(fab) fab.style.display = id==='stock'?'flex':'none';
}

function filterItems(cat, el) {
  currentFilter = cat;
  document.querySelectorAll('#filter-chips .chip').forEach(function(c){ c.classList.remove('active'); });
  el.classList.add('active');
  renderStock(allItems);
}

function filterCountry(c, el) {
  currentCountry = c;
  document.querySelectorAll('#country-chips .chip').forEach(function(x){ x.classList.remove('active'); });
  el.classList.add('active');
  if(currentRecipes.length) renderRecipes(currentRecipes);
}

// ── FETCH STOCK ──
async function fetchStock() {
  document.getElementById('stock-list').innerHTML = '<div class="skeleton"></div><div class="skeleton" style="animation-delay:.1s"></div><div class="skeleton" style="animation-delay:.2s"></div>';
  try {
    var r = await fetch(URL_BASE+'?select=*&order=date_perempt.asc',{ headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY} });
    allItems = await r.json();
    renderStock(allItems);
    updateStockHistory();
    if(document.getElementById('stats').classList.contains('active')) renderStats();
  } catch(e) {
    document.getElementById('stock-list').innerHTML = '<div class="empty"><div class="empty-icon">⚠️</div><div class="empty-text">Erreur de connexion</div></div>';
  }
}

// ── RENDER STOCK ──
function getCatInfo(cat) {
  var m = { 'Frigo':{'emoji':'❄️','cls':'icon-frigo'}, 'Congelo':{'emoji':'🧊','cls':'icon-conge'}, 'Placard':{'emoji':'🫙','cls':'icon-placard'}, 'Cave':{'emoji':'🍷','cls':'icon-cave'} };
  return m[cat] || {'emoji':'📦','cls':'icon-placard'};
}
function formatDate(d) { if(!d) return ''; var p=d.split('-'); return p[2]+'/'+p[1]+'/'+p[0]; }
function getFavItems() { try{ return JSON.parse(localStorage.getItem('colossus_fav_items')||'[]'); }catch(e){ return []; } }
function saveFavItems(f) { localStorage.setItem('colossus_fav_items',JSON.stringify(f)); }

function renderStock(items) {
  var list=document.getElementById('stock-list'), today=new Date(); today.setHours(0,0,0,0);
  var fav=getFavItems(), filtered=items;
  if(currentFilter==='Urgent') filtered=items.filter(function(i){ return Math.ceil((new Date(i.date_perempt)-today)/86400000)<=3; });
  else if(currentFilter==='Favoris') filtered=items.filter(function(i){ return fav.includes(i.id); });
  else if(currentFilter!=='Tous') filtered=items.filter(function(i){ return i.categorie===currentFilter; });
  var urg=0;
  items.forEach(function(i){ if(Math.ceil((new Date(i.date_perempt)-today)/86400000)<=3) urg++; });
  document.getElementById('total-items').textContent=items.length;
  document.getElementById('urgent-items').textContent=urg;
  if(!filtered.length){ list.innerHTML='<div class="empty"><div class="empty-icon">🌿</div><div class="empty-text">Aucun article ici</div></div>'; return; }
  list.innerHTML=filtered.map(function(item,i){
    var diff=Math.ceil((new Date(item.date_perempt)-today)/86400000);
    var cc=diff<=0?'expired':diff<=3?'urgent':'';
    var ci=getCatInfo(item.categorie);
    var sc,st,bc;
    if(diff<=0){sc='status-bad';st='Expiré';bc='bar-bad';}
    else if(diff<=3){sc='status-warn';st='Dans '+diff+'j';bc='bar-warn';}
    else{sc='status-ok';st='Dans '+diff+'j';bc='bar-ok';}
    var pct=diff<=0?100:Math.max(5,Math.min(100,((30-diff)/30)*100));
    var isFav=fav.includes(item.id);
    var note=itemNotes[item.id];
    var photoHtml=item.photo?'<img src="'+item.photo+'" style="width:100%;height:100%;object-fit:cover;border-radius:16px">':ci.emoji;
    var unitStr=item.unite&&item.unite!=='piece'?' · '+item.unite:'';
    return '<div class="item-card '+cc+'" style="animation-delay:'+(i*.04)+'s">'+
      '<div class="item-icon '+ci.cls+'">'+photoHtml+'</div>'+
      '<div class="item-info">'+
        '<div class="item-name">'+item.nom+(note?'<span style="font-size:11px;margin-left:4px;opacity:.6">📝</span>':'')+'</div>'+
        '<div class="item-cat">'+item.categorie+' · '+formatDate(item.date_perempt)+unitStr+'</div>'+
      '</div>'+
      '<div class="item-right">'+
        '<div class="item-qty">×'+(item.quantite||1)+'</div>'+
        '<div class="item-status '+sc+'">'+st+'</div>'+
      '</div>'+
      '<button class="item-fav'+(isFav?' active':'')+'" onclick="toggleFavItem('+item.id+',event)">'+(isFav?'⭐':'☆')+'</button>'+
      '<button class="item-note-btn" onclick="openNoteModal('+item.id+',event)" title="Note" style="width:30px;height:30px;border-radius:10px;background:none;border:none;font-size:14px;cursor:pointer;color:var(--muted)">📝</button>'+
      '<button class="item-delete" onclick="deleteItem('+item.id+',event)">✕</button>'+
      '<div class="item-bar-wrap"><div class="item-bar '+bc+'" style="width:'+pct+'%"></div></div>'+
    '</div>';
  }).join('');
}

function toggleFavItem(id,e) {
  e.stopPropagation();
  var f=getFavItems();
  if(f.includes(id)) f=f.filter(function(x){return x!==id;}); else f.push(id);
  saveFavItems(f);
  renderStock(allItems);
  showToast(f.includes(id)?'⭐ Ajouté aux favoris':'Retiré des favoris');
}

// ── SAVE / DELETE ──
var pendingPhotoData=null;
async function saveToCloud() {
  var nom=document.getElementById('itemName').value.trim(), cat=document.getElementById('itemCat').value, qty=document.getElementById('itemQty').value, date=document.getElementById('itemDate').value, unit=document.getElementById('itemUnit').value;
  if(!nom||!date){ showToast('⚠️ Remplis le nom et la date !'); return; }
  var btn=document.getElementById('save-btn'); btn.classList.add('loading'); btn.textContent='Envoi...';
  try {
    var payload={nom:nom,categorie:cat,date_perempt:date,ajoute_par:getCurrentUserName(),quantite:parseFloat(qty)||1};
    if(pendingPhotoData) payload.photo=pendingPhotoData;
    var res=await fetch(URL_BASE,{method:'POST',headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY,"Content-Type":"application/json","Prefer":"return=minimal"},body:JSON.stringify(payload)});
    if(!res.ok && res.status!==201){ var errText = await res.text(); console.error('Supabase error:', res.status, errText); }if(res.ok||res.status===201){
      showToast('✅ '+nom+' ajouté !');
      document.getElementById('itemName').value=''; document.getElementById('itemDate').value=new Date().toISOString().split('T')[0]; document.getElementById('itemQty').value='1';
      pendingPhotoData=null; document.getElementById('add-photo-preview').innerHTML='📷';
      closeAddModal(); fetchStock();
    } else showToast('❌ Erreur d\'ajout');
  } catch(e){ showToast('❌ Erreur réseau'); }
  finally{ btn.classList.remove('loading'); btn.textContent='✓ Valider dans le Cloud'; }
}

async function deleteItem(id,e) {
  e.stopPropagation();
  if(!confirm('Supprimer cet article ?')) return;
  try{ await fetch(URL_BASE+'?id=eq.'+id,{method:'DELETE',headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY}}); showToast('🗑️ Supprimé'); fetchStock(); }catch(err){ showToast('❌ Erreur'); }
}

// ── PHOTO PRODUIT ──
function takeProductPhoto(ctx) { var inp=document.getElementById('product-photo-input'); inp.setAttribute('data-ctx',ctx); inp.click(); }
function handleProductPhoto(e) {
  var file=e.target.files[0]; if(!file) return;
  var r=new FileReader(); r.onload=function(ev){
    pendingPhotoData=ev.target.result;
    var ctx=document.getElementById('product-photo-input').getAttribute('data-ctx');
    if(ctx==='add') document.getElementById('add-photo-preview').innerHTML='<img src="'+ev.target.result+'" style="width:100%;height:100%;object-fit:cover;border-radius:16px">';
    else if(ctx==='scan') document.getElementById('res-photo-preview').innerHTML='<img src="'+ev.target.result+'" style="width:100%;height:100%;object-fit:cover;border-radius:12px">';
  }; r.readAsDataURL(file);
}

// ── ADD/CLOSE MODALS ──
function openAddModal(){ document.getElementById('add-modal').classList.add('open'); }
function closeAddModal(){ document.getElementById('add-modal').classList.remove('open'); }
document.getElementById('add-modal').addEventListener('click',function(e){if(e.target===this)closeAddModal();});

// ── INVENTORY TOGGLE ──
var invOpen=true;
function toggleInventory(){
  invOpen=!invOpen;
  document.getElementById('inv-collapsible').classList.toggle('open',invOpen);
  document.getElementById('inv-chevron').classList.toggle('open',invOpen);
}

// ── DATE SHORTCUTS ──
function setDateOffset(days,btn){
  var d=new Date(); d.setDate(d.getDate()+days);
  document.getElementById('itemDate').value=d.toISOString().split('T')[0];
  document.querySelectorAll('.date-shortcut').forEach(function(b){b.style.background='';b.style.color='';});
  if(btn){btn.style.background='var(--accent)';btn.style.color='#fff';setTimeout(function(){btn.style.background='';btn.style.color='';},700);}
}
document.getElementById('itemDate').value=new Date().toISOString().split('T')[0];
document.getElementById('res-date').value=new Date().toISOString().split('T')[0];

// ══════════════════════════════════════
//  MULTI-USER / PROFIL
// ══════════════════════════════════════
var profileData = JSON.parse(localStorage.getItem('colossus_profile')||'{"name":"Mathis","emoji":"👤","photo":null}');
var members = JSON.parse(localStorage.getItem('colossus_members')||'[]');
var activeUser = profileData.name;

function getCurrentUserName(){ return activeUser || profileData.name || 'Mathis'; }

function renderUsersRow(){
  var row=document.getElementById('users-row');
  document.getElementById('header-name').textContent=profileData.name||'Mathis';
  var avatar=document.getElementById('main-avatar');
  if(profileData.photo){ avatar.innerHTML='<img src="'+profileData.photo+'" style="width:100%;height:100%;object-fit:cover;border-radius:18px">'; }
  else { avatar.textContent=profileData.emoji||'👤'; }
  var allUsers=[{name:profileData.name,emoji:profileData.emoji,photo:profileData.photo}].concat(members);
  row.innerHTML=allUsers.map(function(u,i){
    var isActive=u.name===activeUser;
    var avatarHtml=u.photo?'<img src="'+u.photo+'" style="width:100%;height:100%;object-fit:cover;border-radius:14px">':u.emoji||'👤';
    return '<div class="user-chip'+(isActive?' active':'')+'" onclick="switchUser(\''+u.name+'\','+i+')">'+
      '<div class="user-avatar'+(isActive?' active':'')+'">'+avatarHtml+'</div>'+
      '<span class="user-chip-name">'+u.name+'</span>'+
    '</div>';
  }).join('')+'<div class="user-chip"><div class="user-add-btn" onclick="openProfileModal()">+</div><span class="user-chip-name">Ajouter</span></div>';
}

function switchUser(name,idx){ activeUser=name; renderUsersRow(); showToast('👤 Connecté en tant que '+name); }

function openProfileModal(){
  document.getElementById('profile-name-input').value=profileData.name||'';
  var big=document.getElementById('profile-photo-big');
  if(profileData.photo) big.innerHTML='<img src="'+profileData.photo+'" style="width:100%;height:100%;object-fit:cover;border-radius:28px"><div class="profile-photo-overlay">Changer</div>';
  else { big.innerHTML='<span id="profile-emoji-display">'+(profileData.emoji||'👤')+'</span><div class="profile-photo-overlay">Changer</div>'; }
  renderMembersList();
  document.getElementById('profile-modal').classList.add('open');
}
function closeProfileModal(){ document.getElementById('profile-modal').classList.remove('open'); }
document.getElementById('profile-modal').addEventListener('click',function(e){if(e.target===this)closeProfileModal();});

function saveProfile(){
  profileData.name=document.getElementById('profile-name-input').value.trim()||'Mathis';
  localStorage.setItem('colossus_profile',JSON.stringify(profileData));
  activeUser=profileData.name;
  renderUsersRow(); closeProfileModal();
  showToast('✅ Profil sauvegardé !');
}

function changeProfilePhoto(){ document.getElementById('profile-photo-input').click(); }
function handleProfilePhoto(e){
  var file=e.target.files[0]; if(!file) return;
  var r=new FileReader(); r.onload=function(ev){
    profileData.photo=ev.target.result;
    var big=document.getElementById('profile-photo-big');
    big.innerHTML='<img src="'+ev.target.result+'" style="width:100%;height:100%;object-fit:cover;border-radius:28px"><div class="profile-photo-overlay">Changer</div>';
  }; r.readAsDataURL(file);
}

function setProfileEmoji(el,emoji){
  profileData.emoji=emoji; profileData.photo=null;
  var big=document.getElementById('profile-photo-big');
  big.innerHTML='<span id="profile-emoji-display">'+emoji+'</span><div class="profile-photo-overlay">Changer</div>';
  document.querySelectorAll('#profile-modal [onclick*="setProfileEmoji"]').forEach(function(b){b.style.background='';});
  el.style.background='rgba(91,140,255,0.2)';
}

function renderMembersList(){
  var list=document.getElementById('members-list');
  list.innerHTML=members.map(function(m,i){
    return '<div style="display:flex;align-items:center;gap:10px;background:var(--surface);border:1px solid var(--border);border-radius:14px;padding:12px 14px">'+
      '<span style="font-size:20px">'+( m.emoji||'👤')+'</span>'+
      '<span style="flex:1;font-family:var(--font-display);font-size:14px;font-weight:700">'+m.name+'</span>'+
      '<button onclick="removeMember('+i+')" style="background:none;border:none;color:var(--danger);font-size:16px;cursor:pointer">✕</button>'+
    '</div>';
  }).join('');
}

function addMember(){
  var inp=document.getElementById('new-member-name'), name=inp.value.trim();
  if(!name) return;
  members.push({name:name,emoji:'👤',photo:null});
  localStorage.setItem('colossus_members',JSON.stringify(members));
  inp.value=''; renderMembersList(); renderUsersRow();
  showToast('✅ '+name+' ajouté(e) !');
}

function removeMember(i){
  members.splice(i,1);
  localStorage.setItem('colossus_members',JSON.stringify(members));
  renderMembersList(); renderUsersRow();
}

// ══════════════════════════════════════
//  RECIPE FAVOURITES
// ══════════════════════════════════════
var recipeFavs=JSON.parse(localStorage.getItem('colossus_fav_recipes')||'[]');
function saveRecipeFavs(){ localStorage.setItem('colossus_fav_recipes',JSON.stringify(recipeFavs)); }
function isRecipeFav(nom){ return recipeFavs.some(function(r){return r.nom===nom;}); }

function toggleRecipeFav(idx){
  var r=currentRecipes[idx]; if(!r) return;
  if(isRecipeFav(r.nom)){ recipeFavs=recipeFavs.filter(function(x){return x.nom!==r.nom;}); showToast('Retiré des favoris'); }
  else{ recipeFavs.unshift(r); showToast('⭐ Recette sauvegardée !'); }
  saveRecipeFavs(); renderFavSection(); renderRecipes(currentRecipes);
}

function toggleModalFav(){
  if(activeRecipeIdx===null) return;
  toggleRecipeFav(activeRecipeIdx);
  var r=currentRecipes[activeRecipeIdx];
  var btn=document.getElementById('modal-fav-btn');
  if(btn&&r){ btn.textContent=isRecipeFav(r.nom)?'⭐':'☆'; btn.style.opacity=isRecipeFav(r.nom)?'1':'0.5'; }
}

function renderFavSection(){
  var sec=document.getElementById('fav-section'), list=document.getElementById('fav-list');
  if(!recipeFavs.length){sec.style.display='none';return;}
  sec.style.display='block';
  document.getElementById('fav-count').textContent='('+recipeFavs.length+')';
  list.innerHTML=recipeFavs.slice(0,3).map(function(r,i){
    var thumb=r.mealDbThumb?'<img src="'+r.mealDbThumb+'/preview" class="recipe-card-thumb" onerror="this.style.display=\'none\'">':'<div class="recipe-emoji">'+r.emoji+'</div>';
    return '<div class="recipe-card" style="animation-delay:'+(i*.05)+'s" onclick="openFavRecipe('+i+')">'+thumb+'<div class="recipe-info"><div class="recipe-name">'+r.nom+'</div><div class="recipe-meta">⏱ '+r.temps+' · '+r.difficulte+'</div></div><span style="font-size:18px;color:#fbbf24">⭐</span></div>';
  }).join('');
}

function openFavRecipe(i){
  var savedCurrent=currentRecipes;
  currentRecipes=recipeFavs;
  openRecipe(i);
  currentRecipes=savedCurrent;
}

// ══════════════════════════════════════
//  CHEF IA — BASE RECETTES MARMITON
// ══════════════════════════════════════

// ─── BASE DE RECETTES (style Marmiton) ───
var RECETTES_DB = [
  {nom:"Quiche lorraine",categorie:"Plat principal",cuisine:"française",emoji:"🥧",temps_prep:20,temps_cuisson:40,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.7,nb_avis:3241,conseil:"Préchauffez bien le four à 180°C et laissez reposer 5 minutes avant de couper.",mots_cles:["oeuf","lardons","creme","fromage","lait","pate","farine","beurre"],ingredients:[{nom:"Pâte brisée",q:1,u:"rouleau"},{nom:"Lardons fumés",q:200,u:"g"},{nom:"Oeufs",q:3,u:""},{nom:"Crème fraîche épaisse",q:20,u:"cl"},{nom:"Lait",q:10,u:"cl"},{nom:"Gruyère râpé",q:80,u:"g"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préchauffer",d:"Préchauffez votre four à 180°C (thermostat 6). Foncez un moule à tarte avec la pâte brisée et piquez-la à la fourchette."},{n:2,t:"Faire revenir les lardons",d:"Faites revenir les lardons à la poêle sans matière grasse jusqu'à ce qu'ils soient légèrement dorés. Égouttez-les sur du papier absorbant."},{n:3,t:"Préparer l'appareil",d:"Dans un bol, battez les oeufs avec la crème fraîche et le lait. Salez légèrement (les lardons sont déjà salés) et poivrez."},{n:4,t:"Garnir et cuire",d:"Répartissez les lardons sur la pâte, versez l'appareil aux oeufs, parsemez de gruyère râpé. Enfournez 35-40 minutes jusqu'à dorure."}]},

  {nom:"Poulet rôti aux herbes",categorie:"Plat principal",cuisine:"française",emoji:"🍗",temps_prep:15,temps_cuisson:75,difficulte:"Très facile",budget:"Moyen",nb_personnes:4,note:4.8,nb_avis:2876,conseil:"Arrosez le poulet toutes les 20 minutes avec le jus de cuisson pour qu'il reste bien moelleux.",mots_cles:["poulet","ail","beurre","thym","citron"],ingredients:[{nom:"Poulet entier",q:1,u:""},{nom:"Beurre",q:50,u:"g"},{nom:"Ail",q:4,u:"gousses"},{nom:"Thym",q:3,u:"brins"},{nom:"Citron",q:1,u:""},{nom:"Huile d'olive",q:2,u:"c. à soupe"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer le poulet",d:"Préchauffez le four à 200°C. Sortez le poulet du réfrigérateur 30 minutes avant. Mélangez le beurre mou avec le thym émietté, sel et poivre. Glissez ce beurre sous la peau."},{n:2,t:"Farcir et assaisonner",d:"Coupez le citron en deux et glissez-le dans la cavité du poulet avec les gousses d'ail écrasées. Badigeonnez l'extérieur d'huile d'olive, salez et poivrez."},{n:3,t:"Cuire",d:"Enfournez le poulet sur le dos pendant 45 minutes à 200°C, puis retournez-le et prolongez 30 minutes. Il est cuit quand le jus qui s'écoule est clair."},{n:4,t:"Reposer",d:"Sortez le poulet du four, couvrez-le d'aluminium et laissez reposer 10 minutes avant de découper."}]},

  {nom:"Gratin dauphinois",categorie:"Accompagnement",cuisine:"française",emoji:"🥔",temps_prep:25,temps_cuisson:60,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.9,nb_avis:4512,conseil:"Utilisez des pommes de terre à chair ferme type Charlotte ou Roseval pour un meilleur résultat.",mots_cles:["pomme de terre","pommes de terre","creme","lait","ail","fromage"],ingredients:[{nom:"Pommes de terre",q:1,u:"kg"},{nom:"Crème fraîche liquide",q:30,u:"cl"},{nom:"Lait entier",q:20,u:"cl"},{nom:"Ail",q:2,u:"gousses"},{nom:"Gruyère râpé",q:100,u:"g"},{nom:"Beurre",q:20,u:"g"},{nom:"Noix de muscade",q:1,u:"pincée"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer les pommes de terre",d:"Épluchez et coupez les pommes de terre en fines rondelles (3mm) à la mandoline. Ne les rincez pas pour garder l'amidon."},{n:2,t:"Préparer le lait à l'ail",d:"Frottez le plat à gratin avec une gousse d'ail coupée en deux, puis beurrez-le. Faites chauffer le lait avec la crème, l'ail écrasé, sel, poivre et muscade."},{n:3,t:"Assembler",d:"Disposez les rondelles de pommes de terre en couches dans le plat, versez le mélange lait-crème chaud dessus. Parsemez de gruyère."},{n:4,t:"Cuire",d:"Enfournez à 160°C pendant 60 à 70 minutes. Le gratin est cuit quand les pommes de terre sont tendres et le dessus bien doré."}]},

  {nom:"Soupe à l'oignon gratinée",categorie:"Entrée",cuisine:"française",emoji:"🍲",temps_prep:15,temps_cuisson:50,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.6,nb_avis:1893,conseil:"La clé : caraméliser lentement les oignons à feu doux pendant 30 minutes minimum.",mots_cles:["oignon","oignons","fromage","beurre","pain","vin"],ingredients:[{nom:"Oignons",q:6,u:""},{nom:"Beurre",q:40,u:"g"},{nom:"Vin blanc sec",q:10,u:"cl"},{nom:"Bouillon de boeuf",q:1,u:"L"},{nom:"Pain (baguette)",q:8,u:"tranches"},{nom:"Comté ou Gruyère râpé",q:150,u:"g"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:["Bouillon de boeuf (1 L)"],etapes:[{n:1,t:"Caraméliser les oignons",d:"Émincez finement les oignons. Faites-les fondre dans le beurre à feu très doux pendant 30 à 40 minutes en remuant régulièrement jusqu'à ce qu'ils soient bien dorés et caramélisés."},{n:2,t:"Déglacer et cuire",d:"Ajoutez le vin blanc, laissez réduire 2 minutes, puis versez le bouillon chaud. Salez, poivrez et laissez mijoter 20 minutes à feu doux."},{n:3,t:"Gratiner",d:"Répartissez la soupe dans des bols allant au four. Posez les tranches de pain grillé sur la soupe, couvrez généreusement de fromage râpé. Faites gratiner sous le gril 5 minutes."}]},

  {nom:"Tarte aux pommes",categorie:"Dessert",cuisine:"française",emoji:"🍎",temps_prep:30,temps_cuisson:40,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.8,nb_avis:5621,conseil:"Parsemez de sucre glace et d'une noix de beurre juste avant d'enfourner pour une tarte brillante.",mots_cles:["pomme","pommes","farine","beurre","sucre","oeuf","pate"],ingredients:[{nom:"Pâte brisée",q:1,u:"rouleau"},{nom:"Pommes (type Golden)",q:4,u:""},{nom:"Sucre",q:60,u:"g"},{nom:"Beurre",q:30,u:"g"},{nom:"Cannelle",q:1,u:"pincée"},{nom:"Sucre glace",q:20,u:"g"}],manquants:[],etapes:[{n:1,t:"Préparer la tarte",d:"Préchauffez le four à 180°C. Étalez la pâte dans un moule à tarte beurré. Piquez le fond avec une fourchette et saupoudrez de sucre."},{n:2,t:"Préparer les pommes",d:"Épluchez, épépinez et coupez les pommes en fines lamelles. Disposez-les en rosace sur la pâte en les faisant se chevaucher légèrement."},{n:3,t:"Cuire",d:"Parsemez de sucre, de cannelle et de petites noisettes de beurre. Enfournez 35-40 minutes jusqu'à ce que les pommes soient dorées et caramélisées."}]},

  {nom:"Carbonara (recette authentique)",categorie:"Plat principal",cuisine:"italienne",emoji:"🍝",temps_prep:10,temps_cuisson:15,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.5,nb_avis:2134,conseil:"Ne jamais mettre de crème fraîche ! Le secret : incorporer les oeufs hors du feu pour éviter qu'ils coagulent.",mots_cles:["pates","spaghetti","oeuf","lardons","bacon","fromage","parmesan"],ingredients:[{nom:"Spaghettis",q:400,u:"g"},{nom:"Guanciale ou lardons",q:150,u:"g"},{nom:"Oeufs entiers",q:2,u:""},{nom:"Jaunes d'oeufs",q:2,u:""},{nom:"Parmesan râpé",q:80,u:"g"},{nom:"Pecorino râpé",q:40,u:"g"},{nom:"Poivre noir",q:1,u:"pincée"}],manquants:["Pecorino (40g)"],etapes:[{n:1,t:"Cuire les pâtes",d:"Faites cuire les spaghettis dans une grande quantité d'eau bouillante salée, al dente selon les indications du paquet. Conservez une louche d'eau de cuisson."},{n:2,t:"Préparer la sauce",d:"Mélangez dans un bol les oeufs, les jaunes, le parmesan et le pecorino. Poivrez généreusement."},{n:3,t:"Faire revenir la charcuterie",d:"Faites dorer le guanciale ou les lardons à la poêle sans matière grasse jusqu'à ce qu'ils soient croustillants."},{n:4,t:"Assembler hors du feu",d:"Égouttez les pâtes et versez-les dans la poêle avec la charcuterie, hors du feu. Ajoutez le mélange oeufs-fromage en remuant vivement. Ajoutez un peu d'eau de cuisson pour lier. Poivrez et servez aussitôt."}]},

  {nom:"Ratatouille niçoise",categorie:"Plat principal",cuisine:"française",emoji:"🫑",temps_prep:30,temps_cuisson:45,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.4,nb_avis:1567,conseil:"Faites revenir chaque légume séparément pour conserver leur saveur respective.",mots_cles:["courgette","tomate","poivron","oignon","aubergine","ail","huile"],ingredients:[{nom:"Courgettes",q:2,u:""},{nom:"Aubergines",q:1,u:""},{nom:"Poivrons (rouge + vert)",q:2,u:""},{nom:"Tomates",q:4,u:""},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:3,u:"gousses"},{nom:"Huile d'olive",q:6,u:"c. à soupe"},{nom:"Thym, laurier",q:1,u:"bouquet"}],manquants:["Aubergines (1)"],etapes:[{n:1,t:"Couper les légumes",d:"Lavez et coupez tous les légumes en dés réguliers d'environ 2 cm. Pelez et émincez les oignons et l'ail."},{n:2,t:"Faire revenir séparément",d:"Dans une grande poêle avec de l'huile d'olive, faites revenir chaque légume séparément (aubergines, courgettes, poivrons) pendant 5 minutes. Réservez."},{n:3,t:"Mijoter ensemble",d:"Dans une cocotte, faites revenir les oignons et l'ail dans l'huile. Ajoutez les tomates concassées, les herbes, sel et poivre. Incorporez tous les légumes et laissez mijoter 30 minutes à feu doux."}]},

  {nom:"Omelette au fromage et fines herbes",categorie:"Plat principal",cuisine:"française",emoji:"🍳",temps_prep:5,temps_cuisson:5,difficulte:"Très facile",budget:"Bon marché",nb_personnes:2,note:4.3,nb_avis:987,conseil:"Une omelette doit se cuire rapidement à feu vif. Elle doit rester baveuse à l'intérieur.",mots_cles:["oeuf","oeufs","fromage","beurre","lait","persil","ciboulette"],ingredients:[{nom:"Oeufs",q:4,u:""},{nom:"Beurre",q:20,u:"g"},{nom:"Emmental ou gruyère râpé",q:60,u:"g"},{nom:"Ciboulette",q:3,u:"brins"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Battre les oeufs",d:"Cassez les oeufs dans un bol, salez, poivrez et battez-les en omelette jusqu'à ce que le mélange soit homogène. Ajoutez la ciboulette ciselée."},{n:2,t:"Cuire",d:"Faites fondre le beurre dans une poêle antiadhésive à feu vif. Versez les oeufs battus. Avec une spatule, ramenez les bords vers le centre en inclinant la poêle."},{n:3,t:"Garnir et plier",d:"Quand l'omelette est encore baveuse dessus, parsemez le fromage râpé sur la moitié. Pliez l'omelette en deux et glissez-la dans le plat."}]},

  {nom:"Soupe de légumes maison",categorie:"Entrée",cuisine:"française",emoji:"🥕",temps_prep:20,temps_cuisson:30,difficulte:"Très facile",budget:"Bon marché",nb_personnes:6,note:4.5,nb_avis:2341,conseil:"Mixez une partie de la soupe pour obtenir une texture veloutée tout en gardant des morceaux.",mots_cles:["carotte","poireau","pomme de terre","oignon","courgette","navet"],ingredients:[{nom:"Carottes",q:3,u:""},{nom:"Poireaux",q:2,u:""},{nom:"Pommes de terre",q:2,u:""},{nom:"Oignons",q:1,u:""},{nom:"Courgette",q:1,u:""},{nom:"Bouillon de légumes",q:1.5,u:"L"},{nom:"Huile d'olive",q:2,u:"c. à soupe"},{nom:"Sel, poivre, persil",q:1,u:"pincée"}],manquants:["Bouillon de légumes (1,5 L)"],etapes:[{n:1,t:"Préparer les légumes",d:"Épluchez et coupez en dés les carottes, pommes de terre, oignons et courgette. Nettoyez et émincez les poireaux."},{n:2,t:"Faire revenir",d:"Faites revenir les oignons et les poireaux dans l'huile d'olive pendant 5 minutes dans une grande casserole."},{n:3,t:"Cuire",d:"Ajoutez tous les légumes, versez le bouillon chaud, salez et poivrez. Laissez cuire 25-30 minutes à feu moyen jusqu'à ce que les légumes soient tendres."},{n:4,t:"Mixer et servir",d:"Mixez la moitié de la soupe pour obtenir une texture crémeuse. Rectifiez l'assaisonnement, parsemez de persil frais et servez chaud."}]},

  {nom:"Poulet au citron et au miel",categorie:"Plat principal",cuisine:"française",emoji:"🍋",temps_prep:15,temps_cuisson:40,difficulte:"Facile",budget:"Moyen",nb_personnes:4,note:4.6,nb_avis:1765,conseil:"Marinée quelques heures, la viande sera encore plus savoureuse et tendre.",mots_cles:["poulet","citron","miel","ail","thym","moutarde"],ingredients:[{nom:"Escalopes ou cuisses de poulet",q:600,u:"g"},{nom:"Citrons",q:2,u:""},{nom:"Miel",q:3,u:"c. à soupe"},{nom:"Moutarde",q:1,u:"c. à soupe"},{nom:"Ail",q:2,u:"gousses"},{nom:"Huile d'olive",q:2,u:"c. à soupe"},{nom:"Thym",q:2,u:"brins"}],manquants:[],etapes:[{n:1,t:"Préparer la marinade",d:"Mélangez le jus des citrons, le miel, la moutarde, l'ail écrasé, l'huile d'olive et le thym. Badigeonnez le poulet de cette marinade. Laissez mariner 30 minutes minimum."},{n:2,t:"Saisir le poulet",d:"Faites dorer le poulet dans une poêle avec un peu d'huile à feu vif, 3 minutes par face."},{n:3,t:"Finir la cuisson",d:"Versez le reste de marinade dans la poêle, couvrez et laissez cuire 20-25 minutes à feu doux en retournant à mi-cuisson. La sauce doit caraméliser légèrement."}]},

  {nom:"Riz cantonais",categorie:"Plat principal",cuisine:"asiatique",emoji:"🍚",temps_prep:15,temps_cuisson:20,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:1432,conseil:"Utilisez du riz cuit de la veille pour un riz cantonais plus savoureux et moins collant.",mots_cles:["riz","oeuf","lardons","jambon","crevettes","petits pois"],ingredients:[{nom:"Riz cuit (de la veille)",q:300,u:"g"},{nom:"Oeufs",q:3,u:""},{nom:"Lardons ou jambon",q:100,u:"g"},{nom:"Petits pois",q:100,u:"g"},{nom:"Sauce soja",q:3,u:"c. à soupe"},{nom:"Huile de sésame",q:1,u:"c. à soupe"},{nom:"Huile neutre",q:2,u:"c. à soupe"}],manquants:["Huile de sésame","Sauce soja"],etapes:[{n:1,t:"Cuire les oeufs",d:"Battez les oeufs avec une pincée de sel. Faites-les scrambler dans un wok avec un peu d'huile, découpez-les en morceaux et réservez."},{n:2,t:"Faire revenir",d:"Dans le même wok à feu vif, faites revenir les lardons ou le jambon jusqu'à dorure. Ajoutez les petits pois et faites sauter 2 minutes."},{n:3,t:"Ajouter le riz",d:"Incorporez le riz froid en émiettant les grains. Faites sauter à feu très vif en remuant constamment 3-4 minutes."},{n:4,t:"Assaisonner",d:"Ajoutez les oeufs, la sauce soja et l'huile de sésame. Mélangez bien et servez immédiatement."}]},

  {nom:"Crêpes sucrées",categorie:"Dessert",cuisine:"française",emoji:"🥞",temps_prep:10,temps_cuisson:20,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.9,nb_avis:6234,conseil:"Laissez reposer la pâte 1 heure au réfrigérateur pour des crêpes plus légères et moins élastiques.",mots_cles:["farine","oeuf","lait","beurre","sucre"],ingredients:[{nom:"Farine",q:250,u:"g"},{nom:"Oeufs",q:3,u:""},{nom:"Lait",q:50,u:"cl"},{nom:"Beurre fondu",q:50,u:"g"},{nom:"Sucre",q:2,u:"c. à soupe"},{nom:"Sel",q:1,u:"pincée"},{nom:"Vanille",q:1,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Préparer la pâte",d:"Tamisez la farine dans un bol, creusez un puits. Ajoutez les oeufs, le sel et le sucre. Incorporez progressivement le lait en fouettant pour éviter les grumeaux. Ajoutez le beurre fondu et la vanille. Laissez reposer 1h."},{n:2,t:"Cuire les crêpes",d:"Chauffez une poêle antiadhésive légèrement beurrée à feu moyen-vif. Versez une petite louche de pâte, inclinez la poêle pour répartir. Cuisez 1 minute par face."}]},

  {nom:"Soupe à la tomate fraîche",categorie:"Entrée",cuisine:"française",emoji:"🍅",temps_prep:15,temps_cuisson:25,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.3,nb_avis:876,conseil:"Utilisez des tomates bien mûres pour une saveur optimale. Une touche de basilic frais en finition est indispensable.",mots_cles:["tomate","tomates","oignon","ail","basilic","creme"],ingredients:[{nom:"Tomates mûres",q:800,u:"g"},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Bouillon de légumes",q:50,u:"cl"},{nom:"Crème fraîche",q:10,u:"cl"},{nom:"Basilic frais",q:6,u:"feuilles"},{nom:"Huile d'olive",q:3,u:"c. à soupe"}],manquants:[],etapes:[{n:1,t:"Monder les tomates",d:"Incisez les tomates en croix, plongez-les 30 secondes dans l'eau bouillante puis dans l'eau froide. Pelez-les, épépinez-les et concassez-les grossièrement."},{n:2,t:"Faire revenir",d:"Faites revenir les oignons et l'ail émincés dans l'huile d'olive 5 minutes. Ajoutez les tomates et laissez compoter 10 minutes."},{n:3,t:"Mixer",d:"Versez le bouillon, laissez cuire 10 minutes, puis mixez finement. Incorporez la crème fraîche. Rectifiez l'assaisonnement. Servez avec du basilic frais ciselé."}]},

  {nom:"Tarte au citron meringuée",categorie:"Dessert",cuisine:"française",emoji:"🍋",temps_prep:45,temps_cuisson:30,difficulte:"Moyenne",budget:"Moyen",nb_personnes:8,note:4.8,nb_avis:3456,conseil:"La crème citron doit refroidir complètement avant d'ajouter la meringue.",mots_cles:["citron","oeuf","beurre","farine","sucre"],ingredients:[{nom:"Pâte sablée",q:1,u:"rouleau"},{nom:"Citrons non traités",q:3,u:""},{nom:"Oeufs",q:4,u:""},{nom:"Sucre",q:180,u:"g"},{nom:"Beurre",q:80,u:"g"},{nom:"Maïzena",q:1,u:"c. à soupe"},{nom:"Blancs d'oeufs (meringue)",q:3,u:""},{nom:"Sucre glace",q:150,u:"g"}],manquants:["Maïzena"],etapes:[{n:1,t:"Cuire le fond de tarte",d:"Foncez le moule avec la pâte, piquez le fond, couvrez de papier sulfurisé et de billes. Cuire 15 min à 180°C, retirez les billes et finissez 5 min."},{n:2,t:"Préparer la crème au citron",d:"Mélangez les oeufs, le sucre, le zeste et le jus des citrons, la maïzena. Faites épaissir à feu moyen en remuant. Incorporez le beurre hors du feu. Versez sur le fond de tarte refroidi."},{n:3,t:"Meringue italienne",d:"Montez les blancs en neige ferme, incorporez le sucre glace progressivement. Étalez sur la crème. Dorez au chalumeau ou sous le gril."}]},

  {nom:"Blanquette de veau",categorie:"Plat principal",cuisine:"française",emoji:"🍖",temps_prep:30,temps_cuisson:90,difficulte:"Moyenne",budget:"Assez cher",nb_personnes:6,note:4.7,nb_avis:1876,conseil:"Ne faites jamais bouillir la sauce après avoir ajouté la crème pour éviter qu'elle tourne.",mots_cles:["veau","creme","carotte","oignon","champignon","beurre","farine"],ingredients:[{nom:"Épaule de veau",q:1.2,u:"kg"},{nom:"Carottes",q:3,u:""},{nom:"Oignons",q:2,u:""},{nom:"Champignons de Paris",q:200,u:"g"},{nom:"Crème fraîche",q:20,u:"cl"},{nom:"Beurre",q:50,u:"g"},{nom:"Farine",q:40,u:"g"},{nom:"Bouquet garni",q:1,u:""},{nom:"Jaunes d'oeufs",q:2,u:""}],manquants:["Épaule de veau (1.2kg)"],etapes:[{n:1,t:"Blanchir la viande",d:"Plongez les morceaux de veau dans l'eau froide, portez à ébullition 2 minutes, égouttez et rincez à l'eau froide. Remettez dans la casserole avec les carottes, oignons et bouquet garni, couvrez d'eau froide et cuisez 1h à feu doux."},{n:2,t:"Préparer le roux",d:"Faites fondre le beurre dans une casserole, ajoutez la farine et remuez 2 minutes. Incorporez progressivement 50 cl de bouillon de cuisson filtré en fouettant. Faites épaissir à feu doux."},{n:3,t:"Lier la sauce",d:"Mélangez les jaunes d'oeufs et la crème fraîche. Hors du feu, incorporez ce mélange à la sauce. Ajoutez la viande et les légumes, les champignons sautés au beurre. Réchauffez sans bouillir."}]},

  {nom:"Salade niçoise",categorie:"Entrée",cuisine:"française",emoji:"🥗",temps_prep:20,temps_cuisson:10,difficulte:"Très facile",budget:"Moyen",nb_personnes:4,note:4.5,nb_avis:2132,conseil:"Tous les ingrédients doivent être à température ambiante pour que la salade soit à son meilleur.",mots_cles:["thon","oeuf","tomate","concombre","salade","olive","anchois"],ingredients:[{nom:"Thon en boîte",q:200,u:"g"},{nom:"Oeufs durs",q:4,u:""},{nom:"Tomates",q:3,u:""},{nom:"Concombre",q:1,u:""},{nom:"Olives noires",q:80,u:"g"},{nom:"Anchois",q:6,u:"filets"},{nom:"Haricots verts",q:200,u:"g"},{nom:"Huile d'olive, vinaigre",q:3,u:"c. à soupe"}],manquants:["Anchois","Olives noires"],etapes:[{n:1,t:"Préparer les légumes",d:"Faites cuire les haricots verts 8 minutes à l'eau bouillante salée, puis passez-les sous l'eau froide. Coupez les tomates en quartiers, le concombre en rondelles."},{n:2,t:"Composer la salade",d:"Disposez dans un grand saladier les haricots, les tomates, le concombre, les oeufs durs coupés en quartiers, le thon émietté, les olives et les anchois."},{n:3,t:"Assaisonner",d:"Préparez une vinaigrette avec huile d'olive, vinaigre, sel et poivre. Versez sur la salade juste avant de servir."}]},

  {nom:"Cake salé jambon-fromage",categorie:"Entrée",cuisine:"française",emoji:"🧀",temps_prep:15,temps_cuisson:45,difficulte:"Très facile",budget:"Bon marché",nb_personnes:8,note:4.6,nb_avis:3421,conseil:"Le cake se conserve 3 jours au réfrigérateur. Réchauffez-le légèrement avant de servir.",mots_cles:["jambon","fromage","oeuf","farine","lait","beurre","lardons"],ingredients:[{nom:"Farine",q:200,u:"g"},{nom:"Oeufs",q:3,u:""},{nom:"Lait",q:10,u:"cl"},{nom:"Huile",q:10,u:"cl"},{nom:"Gruyère râpé",q:150,u:"g"},{nom:"Jambon blanc",q:200,u:"g"},{nom:"Levure chimique",q:1,u:"sachet"},{nom:"Olives vertes",q:60,u:"g"}],manquants:[],etapes:[{n:1,t:"Préparer la pâte",d:"Mélangez la farine et la levure. Ajoutez les oeufs un à un, puis l'huile et le lait tiède. Salez, poivrez."},{n:2,t:"Garnir",d:"Incorporez le jambon coupé en dés, le gruyère râpé et les olives. Versez dans un moule à cake beurré et fariné."},{n:3,t:"Cuire",d:"Enfournez à 180°C pendant 40 à 45 minutes. Vérifiez la cuisson avec la pointe d'un couteau qui doit ressortir sèche. Laissez refroidir avant de démouler."}]},

  {nom:"Poulet basquaise",categorie:"Plat principal",cuisine:"française",emoji:"🫑",temps_prep:25,temps_cuisson:60,difficulte:"Facile",budget:"Moyen",nb_personnes:4,note:4.7,nb_avis:1543,conseil:"Ce plat est encore meilleur réchauffé le lendemain.",mots_cles:["poulet","poivron","tomate","oignon","ail","jambon"],ingredients:[{nom:"Poulet en morceaux",q:1.2,u:"kg"},{nom:"Poivrons rouges et verts",q:3,u:""},{nom:"Tomates",q:4,u:""},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:3,u:"gousses"},{nom:"Jambon de Bayonne",q:100,u:"g"},{nom:"Vin blanc",q:10,u:"cl"},{nom:"Piment d'Espelette",q:1,u:"pincée"}],manquants:["Jambon de Bayonne","Piment d'Espelette"],etapes:[{n:1,t:"Saisir le poulet",d:"Salez et poivrez les morceaux de poulet. Faites-les dorer dans de l'huile d'olive sur toutes les faces. Réservez."},{n:2,t:"Préparer la sauce",d:"Dans la même cocotte, faites revenir les oignons émincés, les poivrons coupés en lanières et l'ail. Ajoutez les tomates concassées et le jambon en dés."},{n:3,t:"Mijoter",d:"Remettez le poulet, déglacez avec le vin blanc, ajoutez le piment d'Espelette. Laissez mijoter 45 minutes à couvert à feu doux."}]},

  {nom:"Gâteau au yaourt",categorie:"Dessert",cuisine:"française",emoji:"🎂",temps_prep:15,temps_cuisson:35,difficulte:"Très facile",budget:"Bon marché",nb_personnes:8,note:4.8,nb_avis:8932,conseil:"Le pot de yaourt sert de mesure. C'est la recette la plus simple pour débuter la pâtisserie !",mots_cles:["yaourt","oeuf","farine","sucre","beurre","huile","levure"],ingredients:[{nom:"Yaourt nature",q:1,u:"pot"},{nom:"Farine",q:3,u:"pots"},{nom:"Sucre",q:2,u:"pots"},{nom:"Oeufs",q:3,u:""},{nom:"Huile",q:0.5,u:"pot"},{nom:"Levure chimique",q:1,u:"sachet"},{nom:"Vanille",q:1,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Préparer la pâte",d:"Videz le yaourt dans un saladier (gardez le pot comme mesure). Ajoutez les oeufs, le sucre, l'huile et la vanille. Mélangez bien."},{n:2,t:"Incorporer la farine",d:"Ajoutez la farine et la levure. Mélangez jusqu'à obtenir une pâte lisse sans grumeaux."},{n:3,t:"Cuire",d:"Versez dans un moule beurré et fariné. Enfournez à 180°C pendant 30 à 35 minutes. Le gâteau est cuit quand la pointe d'un couteau ressort sèche."}]},

  {nom:"Mousse au chocolat",categorie:"Dessert",cuisine:"française",emoji:"🍫",temps_prep:20,temps_cuisson:0,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.9,nb_avis:7654,conseil:"Incorporez les blancs d'oeufs très délicatement pour préserver l'aération et obtenir une mousse légère.",mots_cles:["chocolat","oeuf","beurre","sucre","creme"],ingredients:[{nom:"Chocolat noir",q:200,u:"g"},{nom:"Oeufs",q:6,u:""},{nom:"Beurre",q:30,u:"g"},{nom:"Sucre",q:40,u:"g"},{nom:"Sel",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Faire fondre le chocolat",d:"Faites fondre le chocolat cassé en morceaux avec le beurre au bain-marie ou au micro-ondes par tranches de 30 secondes. Laissez tiédir."},{n:2,t:"Incorporer les jaunes",d:"Séparez les blancs des jaunes. Mélangez les jaunes d'oeufs et le sucre au chocolat fondu."},{n:3,t:"Monter et incorporer les blancs",d:"Montez les blancs en neige ferme avec une pincée de sel. Incorporez-les délicatement au mélange chocolat en trois fois avec une maryse."},{n:4,t:"Réfrigérer",d:"Répartissez dans des verrines ou un grand bol. Laissez prendre au réfrigérateur au moins 3 heures."}]},

  {nom:"Risotto aux champignons",categorie:"Plat principal",cuisine:"italienne",emoji:"🍄",temps_prep:15,temps_cuisson:25,difficulte:"Facile",budget:"Moyen",nb_personnes:4,note:4.6,nb_avis:2134,conseil:"Ajoutez le bouillon louche par louche en attendant l'absorption complète à chaque fois.",mots_cles:["riz","champignon","champignons","oignon","vin","parmesan","creme","beurre"],ingredients:[{nom:"Riz à risotto (Arborio)",q:300,u:"g"},{nom:"Champignons de Paris",q:300,u:"g"},{nom:"Oignon",q:1,u:""},{nom:"Ail",q:1,u:"gousse"},{nom:"Vin blanc sec",q:10,u:"cl"},{nom:"Bouillon de légumes",q:1,u:"L"},{nom:"Parmesan",q:60,u:"g"},{nom:"Beurre",q:40,u:"g"},{nom:"Persil",q:4,u:"brins"}],manquants:["Riz Arborio","Bouillon de légumes"],etapes:[{n:1,t:"Faire revenir",d:"Émincez l'oignon et l'ail. Nettoyez et coupez les champignons en lamelles. Faites revenir l'oignon dans le beurre, puis ajoutez les champignons jusqu'à dorure."},{n:2,t:"Nacrer le riz",d:"Ajoutez le riz et faites-le nacrer 2 minutes en remuant. Versez le vin blanc et laissez absorber."},{n:3,t:"Cuire le risotto",d:"Versez le bouillon chaud louche par louche en attendant l'absorption complète entre chaque ajout. Continuez 18-20 minutes jusqu'à ce que le riz soit al dente."},{n:4,t:"Mantecatura",d:"Hors du feu, incorporez le beurre froid en dés et le parmesan râpé. Remuez vigoureusement pour obtenir un risotto crémeux. Parsemez de persil."}]},

  {nom:"Pain perdu caramélisé",categorie:"Dessert",cuisine:"française",emoji:"🍞",temps_prep:10,temps_cuisson:10,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.7,nb_avis:3234,conseil:"Utilisez du pain rassis pour qu'il absorbe mieux l'appareil sans s'effondrer.",mots_cles:["pain","oeuf","lait","sucre","beurre","vanille","cannelle"],ingredients:[{nom:"Pain rassis (baguette)",q:8,u:"tranches"},{nom:"Oeufs",q:3,u:""},{nom:"Lait",q:20,u:"cl"},{nom:"Sucre",q:50,u:"g"},{nom:"Beurre",q:30,u:"g"},{nom:"Vanille",q:1,u:"c. à café"},{nom:"Cannelle",q:0.5,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Préparer l'appareil",d:"Battez les oeufs avec le lait, 30g de sucre, la vanille et la cannelle dans un plat creux."},{n:2,t:"Tremper le pain",d:"Trempez les tranches de pain dans l'appareil pendant 1 minute de chaque côté pour bien imbiber."},{n:3,t:"Cuire et caraméliser",d:"Faites fondre le beurre dans une poêle. Faites dorer les tranches de pain 2-3 minutes par face. Saupoudrez de sucre restant en fin de cuisson pour caraméliser."}]},

  {nom:"Salade de lentilles",categorie:"Entrée",cuisine:"française",emoji:"🫘",temps_prep:15,temps_cuisson:25,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.3,nb_avis:876,conseil:"Assaisonnez les lentilles encore chaudes pour qu'elles absorbent bien la vinaigrette.",mots_cles:["lentilles","lardons","jambon","carotte","oignon","moutarde","vinaigre"],ingredients:[{nom:"Lentilles vertes",q:250,u:"g"},{nom:"Lardons",q:100,u:"g"},{nom:"Carottes",q:2,u:""},{nom:"Oignons",q:1,u:""},{nom:"Ail",q:1,u:"gousse"},{nom:"Moutarde",q:1,u:"c. à soupe"},{nom:"Vinaigre de vin",q:2,u:"c. à soupe"},{nom:"Huile d'olive",q:3,u:"c. à soupe"},{nom:"Persil",q:4,u:"brins"}],manquants:[],etapes:[{n:1,t:"Cuire les lentilles",d:"Rincez les lentilles. Faites cuire dans 3 fois leur volume d'eau avec la carotte et l'oignon pendant 20-25 minutes. Elles doivent rester légèrement fermes."},{n:2,t:"Faire revenir les lardons",d:"Pendant ce temps, faites revenir les lardons à la poêle jusqu'à légère dorure."},{n:3,t:"Assaisonner",d:"Égouttez les lentilles encore chaudes. Préparez une vinaigrette avec moutarde, vinaigre et huile. Mélangez avec les lentilles, les lardons et le persil ciselé."}]},

  {nom:"Gratin de courgettes",categorie:"Accompagnement",cuisine:"française",emoji:"🫑",temps_prep:20,temps_cuisson:35,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:1231,conseil:"Faites dégorger les courgettes avec du sel pendant 15 minutes pour éviter trop d'eau dans le gratin.",mots_cles:["courgette","courgettes","fromage","oeuf","creme","oignon","ail"],ingredients:[{nom:"Courgettes",q:800,u:"g"},{nom:"Oeufs",q:2,u:""},{nom:"Crème fraîche",q:15,u:"cl"},{nom:"Gruyère râpé",q:100,u:"g"},{nom:"Oignons",q:1,u:""},{nom:"Ail",q:1,u:"gousse"},{nom:"Huile d'olive",q:2,u:"c. à soupe"},{nom:"Sel, poivre, herbes",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer les courgettes",d:"Coupez les courgettes en rondelles, salez et laissez dégorger 15 minutes. Épongez à l'aide de papier absorbant."},{n:2,t:"Faire revenir",d:"Faites revenir l'oignon émincé et l'ail dans l'huile d'olive. Ajoutez les courgettes et faites sauter 5 minutes."},{n:3,t:"Gratiner",d:"Battez les oeufs avec la crème, poivrez. Disposez les courgettes dans un plat à gratin, versez l'appareil aux oeufs, parsemez de gruyère. Enfournez 30-35 minutes à 180°C."}]},

// 56 recettes supplémentaires à insérer avant le ]; final

  // ──── PLATS FRANÇAIS CLASSIQUES ────
  {nom:"Boeuf bourguignon",categorie:"Plat principal",cuisine:"française",emoji:"🥩",temps_prep:30,temps_cuisson:150,difficulte:"Moyenne",budget:"Assez cher",nb_personnes:6,note:4.9,nb_avis:5432,conseil:"Ce plat est 10 fois meilleur réchauffé le lendemain. Préparez-le la veille !",mots_cles:["boeuf","vin","carotte","oignon","champignon","lardons","ail","thym","laurier"],ingredients:[{nom:"Boeuf à braiser (paleron)",q:1.5,u:"kg"},{nom:"Vin rouge (Bourgogne)",q:75,u:"cl"},{nom:"Carottes",q:3,u:""},{nom:"Oignons",q:2,u:""},{nom:"Champignons",q:200,u:"g"},{nom:"Lardons",q:150,u:"g"},{nom:"Ail",q:3,u:"gousses"},{nom:"Farine",q:2,u:"c. à soupe"},{nom:"Bouquet garni",q:1,u:""},{nom:"Beurre",q:30,u:"g"}],manquants:["Vin rouge (75cl)"],etapes:[{n:1,t:"Faire mariner",d:"Coupez la viande en gros cubes. Faites mariner 2h dans le vin avec les légumes, l'ail et le bouquet garni."},{n:2,t:"Saisir la viande",d:"Égouttez la viande, épongez-la et faites-la dorer en plusieurs fois dans le beurre. Farinez légèrement. Réservez."},{n:3,t:"Faire revenir les légumes",d:"Dans la même cocotte, faites revenir les lardons, oignons et carottes. Replacez la viande, versez la marinade filtrée."},{n:4,t:"Mijoter",d:"Couvrez et laissez mijoter 2h30 à feu très doux. Ajoutez les champignons sautés 20 min avant la fin. Rectifiez l'assaisonnement."}]},

  {nom:"Pot-au-feu traditionnel",categorie:"Plat principal",cuisine:"française",emoji:"🍲",temps_prep:30,temps_cuisson:180,difficulte:"Facile",budget:"Moyen",nb_personnes:6,note:4.7,nb_avis:2341,conseil:"Servez le bouillon en entrée avec des vermicelles, puis la viande et les légumes en plat.",mots_cles:["boeuf","carotte","poireau","navet","celeri","oignon","os"],ingredients:[{nom:"Plat de côtes de boeuf",q:800,u:"g"},{nom:"Carottes",q:4,u:""},{nom:"Poireaux",q:2,u:""},{nom:"Navets",q:2,u:""},{nom:"Oignons",q:2,u:""},{nom:"Os à moelle",q:2,u:""},{nom:"Céleri branche",q:2,u:"branches"},{nom:"Bouquet garni",q:1,u:""},{nom:"Gros sel, poivre en grains",q:1,u:"pincée"}],manquants:["Navets","Os à moelle"],etapes:[{n:1,t:"Blanchir la viande",d:"Plongez la viande dans l'eau froide, portez à ébullition, écumez soigneusement et changez l'eau."},{n:2,t:"Cuire le bouillon",d:"Remettez dans l'eau froide avec le bouquet garni, les oignons et le gros sel. Cuisez 1h à petit frémissement."},{n:3,t:"Ajouter les légumes",d:"Ajoutez les carottes, navets et céleri. Poursuivez 45 min. Ajoutez les poireaux et les os à moelle 20 min avant la fin."},{n:4,t:"Servir",d:"Filtrez le bouillon. Servez la viande tranchée avec les légumes, accompagnée de cornichons, moutarde et fleur de sel."}]},

  {nom:"Hachis parmentier",categorie:"Plat principal",cuisine:"française",emoji:"🥔",temps_prep:25,temps_cuisson:40,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.6,nb_avis:3876,conseil:"La couche de purée doit être lisse et généreuse. Ajoutez du parmesan pour une croûte dorée parfaite.",mots_cles:["boeuf","pomme de terre","oignon","ail","tomate","fromage","beurre","lait"],ingredients:[{nom:"Boeuf haché",q:600,u:"g"},{nom:"Pommes de terre",q:1,u:"kg"},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Concentré de tomate",q:2,u:"c. à soupe"},{nom:"Lait",q:15,u:"cl"},{nom:"Beurre",q:60,u:"g"},{nom:"Gruyère râpé",q:80,u:"g"},{nom:"Herbes de Provence",q:1,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Faire la purée",d:"Cuisez les pommes de terre à l'eau salée. Écrasez-les avec le lait chaud et le beurre. Assaisonnez généreusement."},{n:2,t:"Cuire la viande",d:"Faites revenir les oignons et l'ail. Ajoutez le boeuf haché, faites dorer en émiettant. Incorporez le concentré de tomate et les herbes. Salez, poivrez."},{n:3,t:"Assembler et gratiner",d:"Dans un plat à gratin, étalez la viande en couche uniforme. Recouvrez entièrement de purée. Parsemez de gruyère. Enfournez 25-30 min à 200°C jusqu'à dorure."}]},

  {nom:"Coq au vin",categorie:"Plat principal",cuisine:"française",emoji:"🍗",temps_prep:30,temps_cuisson:90,difficulte:"Moyenne",budget:"Moyen",nb_personnes:4,note:4.8,nb_avis:2134,conseil:"Plus le vin est bon, plus le plat sera savoureux. Choisissez un vin que vous aimeriez boire.",mots_cles:["poulet","vin","champignon","lardons","oignon","carotte","ail","thym"],ingredients:[{nom:"Poulet en morceaux",q:1.5,u:"kg"},{nom:"Vin rouge",q:50,u:"cl"},{nom:"Lardons",q:150,u:"g"},{nom:"Champignons",q:200,u:"g"},{nom:"Petits oignons grelots",q:150,u:"g"},{nom:"Ail",q:3,u:"gousses"},{nom:"Farine",q:2,u:"c. à soupe"},{nom:"Beurre",q:30,u:"g"},{nom:"Thym, laurier",q:1,u:"bouquet"}],manquants:["Vin rouge (50cl)","Petits oignons grelots"],etapes:[{n:1,t:"Faire dorer le poulet",d:"Salez et poivrez les morceaux. Faites-les dorer dans le beurre sur toutes les faces. Réservez. Dans la même cocotte, faites revenir les lardons et les oignons."},{n:2,t:"Déglacer et mijoter",d:"Remettez le poulet, farinez légèrement, mélangez. Versez le vin rouge, ajoutez l'ail et le bouquet garni. Laissez mijoter 45 min à couvert."},{n:3,t:"Ajouter les champignons",d:"Faites sauter les champignons séparément dans du beurre. Ajoutez-les à la cocotte 15 min avant la fin. Rectifiez l'assaisonnement."}]},

  {nom:"Tartiflette",categorie:"Plat principal",cuisine:"française",emoji:"🧀",temps_prep:20,temps_cuisson:30,difficulte:"Très facile",budget:"Moyen",nb_personnes:4,note:4.9,nb_avis:4231,conseil:"N'hésitez pas à mettre généreusement de reblochon — c'est le secret d'une tartiflette réussie.",mots_cles:["pomme de terre","lardons","oignon","creme","fromage","reblochon","vin"],ingredients:[{nom:"Pommes de terre",q:1,u:"kg"},{nom:"Reblochon",q:450,u:"g"},{nom:"Lardons fumés",q:200,u:"g"},{nom:"Oignons",q:2,u:""},{nom:"Crème fraîche",q:15,u:"cl"},{nom:"Vin blanc sec",q:10,u:"cl"},{nom:"Beurre",q:20,u:"g"}],manquants:["Reblochon (450g)"],etapes:[{n:1,t:"Cuire les pommes de terre",d:"Faites cuire les pommes de terre en robe des champs 20 min. Laissez refroidir, pelez et coupez en rondelles épaisses."},{n:2,t:"Faire revenir",d:"Faites revenir les oignons émincés dans le beurre. Ajoutez les lardons et faites dorer 5 min. Déglacez au vin blanc."},{n:3,t:"Assembler",d:"Beurrez un plat à gratin. Disposez les pommes de terre, versez la préparation lardons-oignons, ajoutez la crème. Coupez le reblochon en deux dans l'épaisseur, posez-le croûte vers le haut."},{n:4,t:"Cuire",d:"Enfournez 25-30 min à 200°C jusqu'à ce que le fromage soit fondu et doré."}]},

  {nom:"Cassoulet",categorie:"Plat principal",cuisine:"française",emoji:"🫘",temps_prep:30,temps_cuisson:120,difficulte:"Moyenne",budget:"Moyen",nb_personnes:6,note:4.7,nb_avis:1876,conseil:"La croûte qui se forme en surface est précieuse — enfoncez-la 3 fois pendant la cuisson pour qu'elle se reforme.",mots_cles:["haricots","saucisse","confit","lardons","tomate","oignon","ail"],ingredients:[{nom:"Haricots blancs secs",q:500,u:"g"},{nom:"Saucisses de Toulouse",q:400,u:"g"},{nom:"Lardons",q:150,u:"g"},{nom:"Confit de canard",q:2,u:"cuisses"},{nom:"Tomates concassées",q:400,u:"g"},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:4,u:"gousses"},{nom:"Bouquet garni",q:1,u:""}],manquants:["Haricots blancs secs (500g)","Confit de canard"],etapes:[{n:1,t:"Tremper les haricots",d:"Faites tremper les haricots 12h dans l'eau froide. Égouttez, cuisez-les 45 min dans l'eau bouillante salée."},{n:2,t:"Préparer la base",d:"Faites revenir les lardons, oignons et ail. Ajoutez les tomates, le bouquet garni. Incorporez les haricots égouttés."},{n:3,t:"Assembler et cuire",d:"Dans une cassole ou plat en terre, disposez en alternant la préparation aux haricots, les saucisses dorées et le confit de canard. Enfournez 1h à 160°C en reformant la croûte 3 fois."}]},

  {nom:"Daube provençale",categorie:"Plat principal",cuisine:"française",emoji:"🍷",temps_prep:30,temps_cuisson:180,difficulte:"Facile",budget:"Moyen",nb_personnes:6,note:4.6,nb_avis:1234,conseil:"La daube est meilleure réchauffée. Préparez-la la veille et le mariage des saveurs sera incomparable.",mots_cles:["boeuf","vin","carotte","oignon","olive","tomate","thym","orange"],ingredients:[{nom:"Boeuf à braiser",q:1.2,u:"kg"},{nom:"Vin rouge",q:50,u:"cl"},{nom:"Carottes",q:3,u:""},{nom:"Oignons",q:2,u:""},{nom:"Olives noires",q:100,u:"g"},{nom:"Tomates",q:3,u:""},{nom:"Peau d'orange",q:1,u:""},{nom:"Thym, laurier, romarin",q:1,u:"bouquet"},{nom:"Huile d'olive",q:3,u:"c. à soupe"}],manquants:["Olives noires"],etapes:[{n:1,t:"Mariner",d:"Coupez le boeuf en gros cubes. Marinez 12h dans le vin avec légumes, herbes et peau d'orange."},{n:2,t:"Saisir et assembler",d:"Égouttez et saisissez la viande. Dans une cocotte en fonte, disposez en couches : viande, légumes marinés, olives. Versez le vin de marinade filtré."},{n:3,t:"Cuire à l'étouffée",d:"Fermez hermétiquement la cocotte (soudez le couvercle avec un peu de farine et d'eau si possible). Cuisez 3h à 150°C au four sans ouvrir."}]},

  // ──── SOUPES & VELOUTÉS ────
  {nom:"Velouté de potiron",categorie:"Entrée",cuisine:"française",emoji:"🎃",temps_prep:20,temps_cuisson:30,difficulte:"Très facile",budget:"Bon marché",nb_personnes:6,note:4.6,nb_avis:2341,conseil:"Une touche de crème de coco à la place de la crème fraîche donne une version exotique délicieuse.",mots_cles:["potiron","potimarron","courge","oignon","creme","ail","gingembre"],ingredients:[{nom:"Potiron ou potimarron",q:1,u:"kg"},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Crème fraîche",q:15,u:"cl"},{nom:"Bouillon de légumes",q:1,u:"L"},{nom:"Gingembre frais",q:1,u:"c. à café"},{nom:"Huile d'olive",q:2,u:"c. à soupe"},{nom:"Noix de muscade",q:1,u:"pincée"}],manquants:["Potiron/potimarron (1kg)"],etapes:[{n:1,t:"Préparer le potiron",d:"Épluchez et coupez le potiron en cubes. Émincez les oignons et l'ail."},{n:2,t:"Faire revenir",d:"Faites revenir les oignons dans l'huile d'olive. Ajoutez le potiron, l'ail et le gingembre. Faites sauter 5 min."},{n:3,t:"Cuire et mixer",d:"Versez le bouillon, cuisez 25 min à feu doux. Mixez finement, incorporez la crème. Assaisonnez avec la muscade, sel et poivre."}]},

  {nom:"Gaspacho andalou",categorie:"Entrée",cuisine:"méditerranéenne",emoji:"🍅",temps_prep:20,temps_cuisson:0,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.5,nb_avis:1543,conseil:"Préparez-le la veille et servez très froid. Plus les tomates sont mûres et parfumées, meilleur sera le résultat.",mots_cles:["tomate","concombre","poivron","oignon","ail","vinaigre","huile"],ingredients:[{nom:"Tomates très mûres",q:800,u:"g"},{nom:"Concombre",q:0.5,u:""},{nom:"Poivron rouge",q:1,u:""},{nom:"Oignon rouge",q:0.5,u:""},{nom:"Ail",q:1,u:"gousse"},{nom:"Vinaigre de xérès",q:2,u:"c. à soupe"},{nom:"Huile d'olive",q:4,u:"c. à soupe"},{nom:"Pain rassis",q:2,u:"tranches"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer les légumes",d:"Mondez les tomates. Épépinez le concombre et le poivron. Coupez grossièrement tous les légumes."},{n:2,t:"Mixer",d:"Mixez tous les légumes avec le pain trempé, l'ail, le vinaigre et l'huile d'olive. Mixez finement."},{n:3,t:"Passer et refroidir",d:"Passez au tamis pour une texture lisse. Assaisonnez. Réfrigérez au moins 4h. Servez très frais avec une garniture de dés de légumes."}]},

  {nom:"Velouté de brocoli au bleu",categorie:"Entrée",cuisine:"française",emoji:"🥦",temps_prep:15,temps_cuisson:20,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.2,nb_avis:876,conseil:"Le fromage bleu se marie parfaitement avec le brocoli. Dosez selon votre goût.",mots_cles:["brocoli","fromage","creme","oignon","ail","bouillon"],ingredients:[{nom:"Brocoli",q:700,u:"g"},{nom:"Oignon",q:1,u:""},{nom:"Ail",q:1,u:"gousse"},{nom:"Bouillon de légumes",q:80,u:"cl"},{nom:"Crème fraîche",q:10,u:"cl"},{nom:"Fourme d'Ambert ou Roquefort",q:60,u:"g"},{nom:"Beurre",q:20,u:"g"}],manquants:["Fourme d'Ambert (60g)"],etapes:[{n:1,t:"Faire revenir",d:"Faites revenir l'oignon émincé dans le beurre. Ajoutez les bouquets de brocoli et l'ail."},{n:2,t:"Cuire",d:"Versez le bouillon et laissez cuire 15 min jusqu'à ce que le brocoli soit tendre."},{n:3,t:"Mixer et lier",d:"Mixez finement. Ajoutez la crème et le fromage émietté. Réchauffez doucement en remuant jusqu'à ce que le fromage soit fondu."}]},

  // ──── POISSONS & FRUITS DE MER ────
  {nom:"Saumon en papillote",categorie:"Plat principal",cuisine:"française",emoji:"🐟",temps_prep:15,temps_cuisson:20,difficulte:"Très facile",budget:"Assez cher",nb_personnes:2,note:4.7,nb_avis:3421,conseil:"La papillote doit être bien fermée pour que la vapeur reste à l'intérieur. Ouvrez-la à table pour l'effet waouh !",mots_cles:["saumon","citron","herbes","courgette","creme","aneth"],ingredients:[{nom:"Pavés de saumon",q:2,u:""},{nom:"Citron",q:1,u:""},{nom:"Courgette",q:1,u:""},{nom:"Aneth frais",q:3,u:"brins"},{nom:"Crème fraîche",q:2,u:"c. à soupe"},{nom:"Beurre",q:10,u:"g"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:["Aneth"],etapes:[{n:1,t:"Préparer les papillotes",d:"Préchauffez le four à 180°C. Découpez 2 grandes feuilles de papier sulfurisé. Disposez des rondelles de courgette et de citron au centre."},{n:2,t:"Déposer le poisson",d:"Posez le saumon sur les légumes. Nappez de crème fraîche, ajoutez l'aneth ciselé, sel, poivre et une noisette de beurre."},{n:3,t:"Fermer et cuire",d:"Fermez hermétiquement les papillotes en repliant les bords. Enfournez 18-20 min. Servez immédiatement en ouvrant à table."}]},

  {nom:"Moules marinière",categorie:"Plat principal",cuisine:"française",emoji:"🦪",temps_prep:15,temps_cuisson:15,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.6,nb_avis:2876,conseil:"Les moules sont cuites quand elles s'ouvrent. Jetez celles qui restent fermées après cuisson.",mots_cles:["moules","vin","oignon","echalote","persil","beurre","creme"],ingredients:[{nom:"Moules de bouchot",q:2,u:"kg"},{nom:"Echalotes",q:3,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Vin blanc sec",q:20,u:"cl"},{nom:"Beurre",q:40,u:"g"},{nom:"Persil",q:6,u:"brins"},{nom:"Crème fraîche (optionnel)",q:10,u:"cl"}],manquants:["Moules de bouchot (2kg)"],etapes:[{n:1,t:"Nettoyer les moules",d:"Grattez et rincez les moules. Jetez celles qui sont ouvertes et ne se referment pas."},{n:2,t:"Faire la base",d:"Dans une grande cocotte, faites revenir les échalotes et l'ail ciselés dans le beurre 2 minutes."},{n:3,t:"Cuire les moules",d:"Versez le vin blanc, portez à ébullition. Ajoutez les moules. Couvrez et cuisez 5-8 min à feu vif en secouant la cocotte plusieurs fois. Ajoutez la crème et le persil ciselé."}]},

  {nom:"Thon mi-cuit au sésame",categorie:"Plat principal",cuisine:"asiatique",emoji:"🐟",temps_prep:10,temps_cuisson:5,difficulte:"Facile",budget:"Assez cher",nb_personnes:2,note:4.5,nb_avis:1234,conseil:"Le thon doit rester rosé à coeur. Saisissez-le très brièvement à feu très vif.",mots_cles:["thon","sesame","sauce soja","gingembre","ail","salade"],ingredients:[{nom:"Steaks de thon rouge",q:2,u:""},{nom:"Graines de sésame",q:3,u:"c. à soupe"},{nom:"Sauce soja",q:3,u:"c. à soupe"},{nom:"Gingembre frais",q:1,u:"c. à café"},{nom:"Ail",q:1,u:"gousse"},{nom:"Huile de sésame",q:1,u:"c. à soupe"},{nom:"Citron",q:1,u:""}],manquants:["Thon rouge","Graines de sésame","Sauce soja","Huile de sésame"],etapes:[{n:1,t:"Préparer la marinade",d:"Mélangez la sauce soja, le gingembre râpé, l'ail écrasé et l'huile de sésame. Faites mariner le thon 15 min."},{n:2,t:"Enrober de sésame",d:"Égouttez le thon et roulez-le dans les graines de sésame pour bien l'enrober."},{n:3,t:"Saisir",d:"Faites chauffer une poêle à feu très vif. Saisissez le thon 30 secondes par face — il doit être doré dehors et encore cru à coeur. Servez aussitôt avec du citron."}]},

  // ──── VÉGÉTARIEN ────
  {nom:"Curry de légumes au lait de coco",categorie:"Plat principal",cuisine:"indienne",emoji:"🍛",temps_prep:20,temps_cuisson:30,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.6,nb_avis:2134,conseil:"Ajustez les épices à votre goût. Un filet de citron vert en finition rehausse toutes les saveurs.",mots_cles:["courgette","carotte","pois chiches","tomate","oignon","ail","curry","lait de coco","coriandre","gingembre"],ingredients:[{nom:"Lait de coco",q:40,u:"cl"},{nom:"Pois chiches (boîte)",q:400,u:"g"},{nom:"Courgettes",q:2,u:""},{nom:"Carottes",q:2,u:""},{nom:"Tomates concassées",q:400,u:"g"},{nom:"Oignon",q:1,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Curry en poudre",q:2,u:"c. à café"},{nom:"Gingembre",q:1,u:"c. à café"},{nom:"Coriandre fraîche",q:4,u:"brins"}],manquants:["Lait de coco","Pois chiches","Coriandre"],etapes:[{n:1,t:"Faire revenir les aromates",d:"Faites revenir l'oignon émincé, l'ail et le gingembre dans l'huile. Ajoutez le curry et toastez 1 minute."},{n:2,t:"Ajouter les légumes",d:"Incorporez les carottes en rondelles, les courgettes en dés et les tomates concassées. Mélangez bien."},{n:3,t:"Mijoter",d:"Versez le lait de coco, ajoutez les pois chiches égouttés. Laissez mijoter 20 min. Servez avec du riz basmati et de la coriandre fraîche."}]},

  {nom:"Falafels maison",categorie:"Entrée",cuisine:"méditerranéenne",emoji:"🧆",temps_prep:20,temps_cuisson:15,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:1432,conseil:"Utilisez des pois chiches secs trempés (pas en boîte) pour des falafels qui tiennent bien à la friture.",mots_cles:["pois chiches","ail","persil","coriandre","oignon","cumin","farine"],ingredients:[{nom:"Pois chiches secs (trempés 12h)",q:250,u:"g"},{nom:"Oignon",q:1,u:""},{nom:"Ail",q:3,u:"gousses"},{nom:"Persil frais",q:20,u:"g"},{nom:"Coriandre",q:10,u:"g"},{nom:"Cumin",q:1,u:"c. à café"},{nom:"Farine",q:2,u:"c. à soupe"},{nom:"Huile de friture",q:1,u:"L"}],manquants:["Pois chiches secs","Coriandre","Huile de friture"],etapes:[{n:1,t:"Mixer",d:"Mixez les pois chiches égouttés (non cuits!) avec l'oignon, l'ail, les herbes et les épices. La texture doit être granuleuse, pas lisse. Ajoutez la farine."},{n:2,t:"Former",d:"Formez des boulettes de la taille d'une noix. Réfrigérez 30 min."},{n:3,t:"Frire",d:"Faites chauffer l'huile à 180°C. Faites frire les falafels par petites quantités 3-4 min jusqu'à dorure. Égouttez sur papier absorbant."}]},

  {nom:"Tarte aux légumes du soleil",categorie:"Plat principal",cuisine:"méditerranéenne",emoji:"🫑",temps_prep:30,temps_cuisson:45,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.5,nb_avis:1654,conseil:"Faites suer les légumes à la poêle avant de les mettre sur la tarte pour éviter de la détremper.",mots_cles:["courgette","tomate","poivron","oignon","fromage","oeuf","creme","pate"],ingredients:[{nom:"Pâte brisée",q:1,u:"rouleau"},{nom:"Courgettes",q:2,u:""},{nom:"Tomates",q:3,u:""},{nom:"Poivron rouge",q:1,u:""},{nom:"Oignons",q:2,u:""},{nom:"Oeufs",q:2,u:""},{nom:"Crème fraîche",q:15,u:"cl"},{nom:"Gruyère râpé",q:80,u:"g"},{nom:"Herbes de Provence",q:1,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Faire suer les légumes",d:"Coupez tous les légumes en tranches. Faites-les revenir séparément à la poêle avec de l'huile d'olive. Assaisonnez, ajoutez les herbes."},{n:2,t:"Préparer l'appareil",d:"Battez les oeufs avec la crème, sel et poivre."},{n:3,t:"Assembler et cuire",d:"Foncez le moule avec la pâte. Disposez les légumes en rosace. Versez l'appareil, parsemez de gruyère. Enfournez 40 min à 180°C."}]},

  {nom:"Gratin de chou-fleur",categorie:"Accompagnement",cuisine:"française",emoji:"🥦",temps_prep:20,temps_cuisson:35,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.3,nb_avis:1123,conseil:"La béchamel doit être bien assaisonnée avec de la muscade. C'est elle qui fait toute la différence.",mots_cles:["chou fleur","chou-fleur","fromage","beurre","farine","lait","muscade","fromage"],ingredients:[{nom:"Chou-fleur",q:1,u:""},{nom:"Beurre",q:40,u:"g"},{nom:"Farine",q:40,u:"g"},{nom:"Lait",q:50,u:"cl"},{nom:"Gruyère râpé",q:120,u:"g"},{nom:"Noix de muscade",q:1,u:"pincée"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:["Chou-fleur"],etapes:[{n:1,t:"Cuire le chou-fleur",d:"Découpez le chou-fleur en bouquets. Cuisez 10 min dans l'eau bouillante salée. Égouttez."},{n:2,t:"Faire la béchamel",d:"Faites un roux avec beurre et farine. Incorporez le lait chaud progressivement en fouettant. Laissez épaissir. Assaisonnez avec muscade, sel, poivre. Ajoutez les 2/3 du fromage."},{n:3,t:"Gratiner",d:"Disposez le chou-fleur dans un plat à gratin. Nappez de béchamel, parsemez du reste de fromage. Enfournez 25 min à 200°C."}]},

  // ──── PÂTES & RIZ ────
  {nom:"Penne à l'arrabiata",categorie:"Plat principal",cuisine:"italienne",emoji:"🍝",temps_prep:10,temps_cuisson:20,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:1876,conseil:"Ne lésinez pas sur le piment — arrabiata signifie 'en colère' en italien !",mots_cles:["pates","tomate","ail","piment","huile","persil"],ingredients:[{nom:"Penne",q:400,u:"g"},{nom:"Tomates concassées",q:400,u:"g"},{nom:"Ail",q:4,u:"gousses"},{nom:"Piment rouge",q:1,u:""},{nom:"Huile d'olive",q:4,u:"c. à soupe"},{nom:"Persil frais",q:4,u:"brins"},{nom:"Parmesan",q:40,u:"g"}],manquants:["Piment rouge"],etapes:[{n:1,t:"Préparer la sauce",d:"Faites revenir l'ail et le piment émincés dans l'huile d'olive à feu doux 2 min. Ajoutez les tomates concassées, salez et laissez réduire 15 min à feu moyen."},{n:2,t:"Cuire les pâtes",d:"Faites cuire les penne al dente dans une grande quantité d'eau bouillante salée."},{n:3,t:"Servir",d:"Égouttez les pâtes en réservant un peu d'eau de cuisson. Mélangez à la sauce, ajoutez une louche d'eau si besoin. Parsemez de persil et de parmesan."}]},

  {nom:"Lasagnes bolognaise",categorie:"Plat principal",cuisine:"italienne",emoji:"🍝",temps_prep:40,temps_cuisson:60,difficulte:"Moyenne",budget:"Moyen",nb_personnes:6,note:4.8,nb_avis:4321,conseil:"Préparez la bolognaise la veille — elle sera encore meilleure et les lasagnes n'en seront que plus savoureuses.",mots_cles:["boeuf","pates","tomate","oignon","carotte","ail","lait","farine","beurre","fromage"],ingredients:[{nom:"Feuilles de lasagne",q:12,u:"feuilles"},{nom:"Boeuf haché",q:500,u:"g"},{nom:"Tomates concassées",q:800,u:"g"},{nom:"Oignons",q:2,u:""},{nom:"Carottes",q:2,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Lait",q:50,u:"cl"},{nom:"Beurre",q:50,u:"g"},{nom:"Farine",q:50,u:"g"},{nom:"Parmesan",q:100,u:"g"},{nom:"Gruyère râpé",q:80,u:"g"}],manquants:["Feuilles de lasagne","Parmesan"],etapes:[{n:1,t:"Bolognaise",d:"Faites revenir oignons, carottes et ail. Ajoutez le boeuf haché, faites brunir. Incorporez les tomates, sel, poivre et herbes. Laissez mijoter 30 min."},{n:2,t:"Béchamel",d:"Faites un roux beurre-farine. Incorporez le lait chaud en fouettant. Assaisonnez avec sel, poivre et muscade."},{n:3,t:"Assembler et cuire",d:"Alternez couches de béchamel, feuilles de lasagne, bolognaise et fromage. Finissez par de la béchamel et du fromage. Enfournez 40 min à 180°C."}]},

  {nom:"Tagliatelles au saumon fumé et citron",categorie:"Plat principal",cuisine:"italienne",emoji:"🍝",temps_prep:10,temps_cuisson:15,difficulte:"Très facile",budget:"Moyen",nb_personnes:2,note:4.5,nb_avis:2134,conseil:"Ajoutez le saumon fumé hors du feu pour qu'il ne cuise pas et conserve sa texture soyeuse.",mots_cles:["saumon","pates","creme","citron","aneth","parmesan"],ingredients:[{nom:"Tagliatelles",q:200,u:"g"},{nom:"Saumon fumé",q:120,u:"g"},{nom:"Crème fraîche",q:20,u:"cl"},{nom:"Citron",q:1,u:""},{nom:"Aneth",q:3,u:"brins"},{nom:"Parmesan",q:30,u:"g"},{nom:"Beurre",q:10,u:"g"}],manquants:["Saumon fumé","Aneth"],etapes:[{n:1,t:"Cuire les pâtes",d:"Faites cuire les tagliatelles al dente."},{n:2,t:"Préparer la sauce",d:"Faites chauffer la crème avec le beurre, le jus et le zeste de citron. Assaisonnez."},{n:3,t:"Assembler",d:"Égouttez les pâtes et mélangez à la sauce. Hors du feu, ajoutez le saumon fumé coupé en lanières. Parsemez d'aneth et de parmesan."}]},

  {nom:"Riz pilaf",categorie:"Accompagnement",cuisine:"française",emoji:"🍚",temps_prep:5,temps_cuisson:20,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.3,nb_avis:987,conseil:"La méthode pilaf donne un riz parfaitement aéré. Chaque grain doit rester distinct.",mots_cles:["riz","oignon","bouillon","beurre","ail"],ingredients:[{nom:"Riz long grain",q:300,u:"g"},{nom:"Oignon",q:1,u:""},{nom:"Bouillon de légumes ou volaille",q:60,u:"cl"},{nom:"Beurre",q:30,u:"g"},{nom:"Ail",q:1,u:"gousse"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Nacrer le riz",d:"Faites revenir l'oignon et l'ail émincés dans le beurre. Ajoutez le riz et faites-le nacrer 2 min en remuant jusqu'à ce qu'il soit translucide."},{n:2,t:"Cuire",d:"Versez le bouillon chaud (2 fois le volume du riz). Salez légèrement. Portez à ébullition, couvrez et laissez cuire 18 min à feu très doux sans soulever le couvercle."},{n:3,t:"Égrener",d:"Ôtez du feu et laissez reposer 5 min. Égrainé à la fourchette avant de servir."}]},

  // ──── VIANDES ────
  {nom:"Steak haché maison sauce marchand de vin",categorie:"Plat principal",cuisine:"française",emoji:"🥩",temps_prep:10,temps_cuisson:15,difficulte:"Facile",budget:"Moyen",nb_personnes:2,note:4.5,nb_avis:1543,conseil:"Formez le steak à la main sans trop le travailler. Faites-le cuire dans une poêle très chaude.",mots_cles:["boeuf","vin","echalote","beurre","persil"],ingredients:[{nom:"Boeuf haché 15% MG",q:300,u:"g"},{nom:"Echalotes",q:2,u:""},{nom:"Vin rouge",q:10,u:"cl"},{nom:"Beurre",q:40,u:"g"},{nom:"Persil",q:3,u:"brins"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer la sauce",d:"Faites suer les échalotes ciselées dans 20g de beurre. Déglacez au vin rouge, laissez réduire de moitié. Incorporez hors du feu le reste du beurre froid en dés. Ajoutez le persil."},{n:2,t:"Cuire le steak",d:"Formez 2 steaks. Faites chauffer une poêle à feu très vif. Saisissez 2-3 min par face selon la cuisson souhaitée."},{n:3,t:"Servir",d:"Nappez les steaks de sauce marchand de vin. Servez avec des frites ou de la purée."}]},

  {nom:"Côtes de porc miel-moutarde",categorie:"Plat principal",cuisine:"française",emoji:"🥓",temps_prep:10,temps_cuisson:25,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:2341,conseil:"Badigeonnez la viande de marinade à mi-cuisson pour qu'elle caramélise bien.",mots_cles:["porc","miel","moutarde","ail","thym","huile"],ingredients:[{nom:"Côtes de porc",q:4,u:""},{nom:"Miel",q:2,u:"c. à soupe"},{nom:"Moutarde à l'ancienne",q:2,u:"c. à soupe"},{nom:"Ail",q:2,u:"gousses"},{nom:"Thym",q:2,u:"brins"},{nom:"Huile d'olive",q:2,u:"c. à soupe"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer la marinade",d:"Mélangez le miel, la moutarde, l'ail écrasé, l'huile, le thym, sel et poivre. Badigeonnez les côtes de porc et laissez mariner 30 min minimum."},{n:2,t:"Cuire",d:"Faites cuire les côtes sur un grill ou à la poêle bien chaude, 8-10 min par face. Badigeonnez régulièrement avec le reste de marinade."},{n:3,t:"Repos",d:"Laissez reposer 3 min dans du papier alu avant de servir pour que les jus se redistribuent."}]},

  {nom:"Veau Marengo",categorie:"Plat principal",cuisine:"française",emoji:"🍖",temps_prep:25,temps_cuisson:90,difficulte:"Facile",budget:"Assez cher",nb_personnes:4,note:4.5,nb_avis:987,conseil:"Ce plat mijote longuement — la patience est la clé pour obtenir une viande fondante.",mots_cles:["veau","tomate","champignon","oignon","ail","vin","creme"],ingredients:[{nom:"Épaule de veau",q:800,u:"g"},{nom:"Tomates",q:4,u:""},{nom:"Champignons",q:200,u:"g"},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Vin blanc",q:15,u:"cl"},{nom:"Farine",q:2,u:"c. à soupe"},{nom:"Huile d'olive",q:3,u:"c. à soupe"},{nom:"Bouquet garni",q:1,u:""}],manquants:["Épaule de veau"],etapes:[{n:1,t:"Faire dorer",d:"Coupez le veau en gros cubes, farinez légèrement. Faites dorer à l'huile d'olive. Réservez. Faites revenir oignons et ail."},{n:2,t:"Mijoter",d:"Remettez la viande, déglacez au vin blanc. Ajoutez les tomates concassées, le bouquet garni. Laissez mijoter 1h à couvert."},{n:3,t:"Finir",d:"Ajoutez les champignons sautés au beurre. Prolongez 20 min. Rectifiez l'assaisonnement."}]},

  {nom:"Escalope milanaise",categorie:"Plat principal",cuisine:"italienne",emoji:"🍖",temps_prep:15,temps_cuisson:10,difficulte:"Très facile",budget:"Moyen",nb_personnes:4,note:4.6,nb_avis:2876,conseil:"Aplatissez bien les escalopes avec un rouleau à pâtisserie pour qu'elles soient uniformément fines.",mots_cles:["veau","poulet","oeuf","chapelure","farine","beurre","citron","parmesan"],ingredients:[{nom:"Escalopes de veau ou poulet",q:4,u:""},{nom:"Chapelure",q:150,u:"g"},{nom:"Oeufs",q:2,u:""},{nom:"Farine",q:60,u:"g"},{nom:"Parmesan râpé",q:50,u:"g"},{nom:"Beurre",q:60,u:"g"},{nom:"Citron",q:1,u:""},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:["Chapelure"],etapes:[{n:1,t:"Préparer la panure",d:"Mélangez la chapelure avec le parmesan. Battez les oeufs. Aplatissez les escalopes entre deux feuilles de film alimentaire."},{n:2,t:"Paner",d:"Passez chaque escalope dans la farine (tapotez pour enlever l'excès), puis dans l'oeuf battu, puis dans la chapelure au parmesan."},{n:3,t:"Cuire",d:"Faites chauffer le beurre à feu moyen jusqu'à ce qu'il mousse. Faites cuire les escalopes 3-4 min par face jusqu'à dorure. Servez avec du citron."}]},

  // ──── DESSERTS ────
  {nom:"Fondant au chocolat coeur coulant",categorie:"Dessert",cuisine:"française",emoji:"🍫",temps_prep:15,temps_cuisson:12,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.9,nb_avis:8765,conseil:"La cuisson est le secret : 12 min exactement pour un coeur coulant parfait. Testez avec un moule avant d'inviter !",mots_cles:["chocolat","oeuf","beurre","sucre","farine"],ingredients:[{nom:"Chocolat noir 70%",q:150,u:"g"},{nom:"Beurre",q:100,u:"g"},{nom:"Oeufs",q:3,u:""},{nom:"Jaunes d'oeufs",q:2,u:""},{nom:"Sucre",q:80,u:"g"},{nom:"Farine",q:50,u:"g"}],manquants:[],etapes:[{n:1,t:"Fondre le chocolat",d:"Faites fondre le chocolat et le beurre au bain-marie. Laissez tiédir."},{n:2,t:"Préparer la pâte",d:"Fouettez les oeufs, les jaunes et le sucre jusqu'à blanchiment. Incorporez le mélange chocolat. Ajoutez la farine tamisée."},{n:3,t:"Cuire",d:"Beurrez et farinez des ramequins. Versez la pâte. Réfrigérez 1h minimum (ou toute une nuit). Enfournez à 200°C pendant 11-12 min exactement. Le centre doit rester fondant."}]},

  {nom:"Tarte tatin",categorie:"Dessert",cuisine:"française",emoji:"🍎",temps_prep:25,temps_cuisson:40,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.8,nb_avis:3987,conseil:"Renversez la tarte délicatement dès la sortie du four et laissez couler le caramel sur les pommes.",mots_cles:["pomme","beurre","sucre","farine","pate","caramel"],ingredients:[{nom:"Pommes Golden",q:8,u:""},{nom:"Beurre",q:80,u:"g"},{nom:"Sucre",q:150,u:"g"},{nom:"Pâte feuilletée",q:1,u:"rouleau"},{nom:"Cannelle",q:0.5,u:"c. à café"}],manquants:["Pâte feuilletée"],etapes:[{n:1,t:"Faire le caramel",d:"Dans un moule à manqué allant sur le feu, faites un caramel avec le beurre et le sucre jusqu'à coloration dorée."},{n:2,t:"Disposer les pommes",d:"Épluchez et coupez les pommes en quartiers. Disposez-les serrées dans le caramel encore chaud. Saupoudrez de cannelle. Faites cuire 15 min à feu moyen."},{n:3,t:"Couvrir et cuire",d:"Couvrez les pommes avec la pâte feuilletée en rentrant les bords. Enfournez 25 min à 200°C. Retournez immédiatement sur un plat à la sortie du four."}]},

  {nom:"Crème brûlée",categorie:"Dessert",cuisine:"française",emoji:"🍮",temps_prep:20,temps_cuisson:45,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.9,nb_avis:5432,conseil:"La crème doit trembler légèrement au centre en fin de cuisson — elle se raffermira en refroidissant.",mots_cles:["creme","oeuf","sucre","vanille","lait"],ingredients:[{nom:"Crème liquide entière",q:50,u:"cl"},{nom:"Jaunes d'oeufs",q:5,u:""},{nom:"Sucre",q:80,u:"g"},{nom:"Vanille",q:1,u:"gousse"},{nom:"Cassonade",q:4,u:"c. à café"}],manquants:["Crème liquide entière","Cassonade"],etapes:[{n:1,t:"Préparer la crème",d:"Faites chauffer la crème avec la vanille fendue. Fouettez les jaunes avec le sucre jusqu'à blanchiment. Versez la crème chaude progressivement en fouettant."},{n:2,t:"Cuire au bain-marie",d:"Répartissez dans des ramequins. Faites cuire au bain-marie 45 min à 150°C. La crème doit trembler légèrement. Laissez refroidir puis réfrigérez 4h."},{n:3,t:"Brûler la cassonade",d:"Saupoudrez de cassonade. Caramélisez au chalumeau ou sous le gril très chaud jusqu'à obtenir une croûte dorée et craquante."}]},

  {nom:"Île flottante",categorie:"Dessert",cuisine:"française",emoji:"🍮",temps_prep:30,temps_cuisson:15,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.7,nb_avis:2341,conseil:"Les blancs peuvent être pochés à l'avance. Préparez la crème anglaise la veille pour plus de sérénité.",mots_cles:["oeuf","lait","sucre","vanille","amande"],ingredients:[{nom:"Oeufs (blancs et jaunes séparés)",q:4,u:""},{nom:"Lait",q:50,u:"cl"},{nom:"Sucre",q:120,u:"g"},{nom:"Vanille",q:1,u:"gousse"},{nom:"Amandes effilées",q:30,u:"g"}],manquants:["Amandes effilées"],etapes:[{n:1,t:"Crème anglaise",d:"Faites chauffer le lait avec la vanille. Fouettez les jaunes avec 80g de sucre. Versez le lait chaud, remettez sur feu doux en remuant jusqu'à napper la cuillère."},{n:2,t:"Pocher les blancs",d:"Montez les blancs en neige avec le reste du sucre. Faites pocher des quenelles de blanc dans le lait frémissant 2 min de chaque côté."},{n:3,t:"Dressage",d:"Versez la crème anglaise dans des coupes. Posez les îles flottantes dessus. Faites un caramel doré et nappez. Parsemez d'amandes grillées."}]},

  {nom:"Clafoutis aux cerises",categorie:"Dessert",cuisine:"française",emoji:"🍒",temps_prep:15,temps_cuisson:40,difficulte:"Très facile",budget:"Bon marché",nb_personnes:6,note:4.7,nb_avis:3211,conseil:"Laissez les cerises avec leurs noyaux — ils parfument le dessert. Prévenez vos convives !",mots_cles:["cerise","oeuf","lait","sucre","farine","beurre","creme","fraise","framboise"],ingredients:[{nom:"Cerises ou fruits rouges",q:500,u:"g"},{nom:"Oeufs",q:3,u:""},{nom:"Lait",q:30,u:"cl"},{nom:"Sucre",q:100,u:"g"},{nom:"Farine",q:80,u:"g"},{nom:"Beurre",q:20,u:"g"},{nom:"Vanille",q:1,u:"c. à café"},{nom:"Sel",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Préparer la pâte",d:"Fouettez les oeufs avec le sucre jusqu'à blanchiment. Ajoutez la farine, le sel, puis le lait progressivement. Incorporez la vanille. La pâte doit être lisse."},{n:2,t:"Assembler",d:"Beurrez un plat à gratin. Disposez les cerises (avec noyaux) ou fruits rouges. Versez la pâte dessus."},{n:3,t:"Cuire",d:"Enfournez 35-40 min à 180°C jusqu'à ce que le clafoutis soit gonflé et doré. Servez tiède ou froid, saupoudré de sucre glace."}]},

  {nom:"Financiers aux amandes",categorie:"Dessert",cuisine:"française",emoji:"🍰",temps_prep:15,temps_cuisson:15,difficulte:"Facile",budget:"Bon marché",nb_personnes:12,note:4.8,nb_avis:4321,conseil:"La clé est le beurre noisette — faites-le chauffer jusqu'à une légère odeur de noisette et une couleur ambrée.",mots_cles:["amande","oeuf","beurre","sucre","farine","blanc d oeuf"],ingredients:[{nom:"Blancs d'oeufs",q:4,u:""},{nom:"Beurre",q:125,u:"g"},{nom:"Poudre d'amandes",q:100,u:"g"},{nom:"Sucre glace",q:150,u:"g"},{nom:"Farine",q:50,u:"g"},{nom:"Sel",q:1,u:"pincée"}],manquants:["Poudre d'amandes","Sucre glace"],etapes:[{n:1,t:"Beurre noisette",d:"Faites chauffer le beurre jusqu'à ce qu'il prenne une couleur noisette et dégage une odeur de caramel. Filtrez et laissez tiédir."},{n:2,t:"Préparer la pâte",d:"Mélangez la poudre d'amandes, le sucre glace, la farine et le sel. Incorporez les blancs non montés, puis le beurre noisette."},{n:3,t:"Cuire",d:"Versez dans des moules à financiers beurrés. Enfournez 12-15 min à 200°C. Les financiers sont cuits quand les bords sont dorés et le centre légèrement moelleux."}]},

  // ──── PETIT-DÉJEUNER & BRUNCH ────
  {nom:"Pancakes américains",categorie:"Petit-déjeuner",cuisine:"américaine",emoji:"🥞",temps_prep:10,temps_cuisson:20,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.8,nb_avis:6543,conseil:"Ne mélangez pas trop la pâte — quelques grumeaux donnent des pancakes plus moelleux.",mots_cles:["farine","oeuf","lait","beurre","sucre","levure","yaourt","babeurre"],ingredients:[{nom:"Farine",q:200,u:"g"},{nom:"Lait ou babeurre",q:25,u:"cl"},{nom:"Oeufs",q:2,u:""},{nom:"Beurre fondu",q:40,u:"g"},{nom:"Sucre",q:2,u:"c. à soupe"},{nom:"Levure chimique",q:1,u:"sachet"},{nom:"Sel",q:1,u:"pincée"},{nom:"Vanille",q:1,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Préparer la pâte",d:"Mélangez farine, sucre, levure et sel. Dans un autre bol, battez les oeufs avec le lait, le beurre fondu et la vanille. Incorporez les liquides aux secs sans trop mélanger."},{n:2,t:"Cuire",d:"Faites chauffer une poêle antiadhésive légèrement beurrée à feu moyen. Versez une louche de pâte. Quand des bulles apparaissent en surface et que les bords sont pris, retournez. Cuisez encore 1 min."}]},

  {nom:"Granola maison",categorie:"Petit-déjeuner",cuisine:"américaine",emoji:"🌾",temps_prep:10,temps_cuisson:30,difficulte:"Très facile",budget:"Bon marché",nb_personnes:8,note:4.7,nb_avis:3214,conseil:"Remuez à mi-cuisson et laissez bien refroidir avant de briser en morceaux pour des clusters croustillants.",mots_cles:["flocons d avoine","miel","huile","amande","noix","fruit sec","chocolat"],ingredients:[{nom:"Flocons d'avoine",q:300,u:"g"},{nom:"Miel",q:80,u:"g"},{nom:"Huile neutre",q:4,u:"c. à soupe"},{nom:"Amandes effilées",q:60,u:"g"},{nom:"Noix de cajou",q:50,u:"g"},{nom:"Cannelle",q:1,u:"c. à café"},{nom:"Sel",q:1,u:"pincée"}],manquants:["Flocons d'avoine","Amandes effilées"],etapes:[{n:1,t:"Mélanger",d:"Mélangez les flocons avec l'huile, le miel, la cannelle et le sel. Incorporez les fruits secs."},{n:2,t:"Cuire",d:"Étalez sur une plaque recouverte de papier sulfurisé. Enfournez 25-30 min à 160°C en remuant à mi-cuisson."},{n:3,t:"Refroidir",d:"Laissez refroidir complètement sur la plaque sans toucher pour que le granola forme des clusters croustillants. Conservez dans un bocal hermétique."}]},

  // ──── SNACKS & FINGER FOOD ────
  {nom:"Bruschetta tomate-basilic",categorie:"Entrée",cuisine:"italienne",emoji:"🍞",temps_prep:10,temps_cuisson:5,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.5,nb_avis:2134,conseil:"Frottez les toasts avec de l'ail cru à la sortie du four — c'est le secret de la bruschetta authentique.",mots_cles:["pain","tomate","ail","basilic","huile","sel"],ingredients:[{nom:"Pain de campagne",q:8,u:"tranches"},{nom:"Tomates mûres",q:4,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Basilic frais",q:10,u:"feuilles"},{nom:"Huile d'olive",q:4,u:"c. à soupe"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:[],etapes:[{n:1,t:"Griller le pain",d:"Faites griller les tranches de pain sous le gril du four ou dans un grille-pain jusqu'à légère dorure."},{n:2,t:"Frotter à l'ail",d:"Frottez immédiatement chaque tranche avec une gousse d'ail coupée en deux."},{n:3,t:"Garnir",d:"Coupez les tomates en dés, assaisonnez avec l'huile d'olive, sel et poivre. Disposez sur le pain. Ajoutez le basilic ciselé et une filet d'huile d'olive."}]},

  {nom:"Guacamole maison",categorie:"Entrée",cuisine:"mexicaine",emoji:"🥑",temps_prep:10,temps_cuisson:0,difficulte:"Très facile",budget:"Moyen",nb_personnes:4,note:4.7,nb_avis:3421,conseil:"Gardez les noyaux d'avocat dans le guacamole pour éviter qu'il noircisse.",mots_cles:["avocat","tomate","oignon","citron","coriandre","ail","piment"],ingredients:[{nom:"Avocats mûrs",q:3,u:""},{nom:"Tomates",q:2,u:""},{nom:"Oignon rouge",q:0.5,u:""},{nom:"Citron vert",q:1,u:""},{nom:"Coriandre fraîche",q:6,u:"brins"},{nom:"Ail",q:1,u:"gousse"},{nom:"Sel, poivre",q:1,u:"pincée"}],manquants:["Avocats","Coriandre","Citron vert"],etapes:[{n:1,t:"Écraser les avocats",d:"Coupez les avocats en deux, retirez les noyaux (gardez-les). Écrasez la chair à la fourchette — gardez de la texture."},{n:2,t:"Ajouter les garnitures",d:"Incorporez les tomates épépinées en petits dés, l'oignon rouge finement ciselé, l'ail écrasé et la coriandre hachée."},{n:3,t:"Assaisonner",d:"Pressez le citron vert, salez, poivrez. Goûtez et ajustez. Remettez les noyaux pour retarder l'oxydation. Servez immédiatement avec des chips."}]},

  {nom:"Croque-monsieur gratiné",categorie:"Plat principal",cuisine:"française",emoji:"🥪",temps_prep:10,temps_cuisson:10,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.6,nb_avis:4321,conseil:"L'ajout d'un oeuf poché transforme le croque-monsieur en croque-madame — encore meilleur !",mots_cles:["pain","jambon","fromage","beurre","lait","farine","bechamel"],ingredients:[{nom:"Pain de mie",q:8,u:"tranches"},{nom:"Jambon blanc",q:4,u:"tranches"},{nom:"Gruyère râpé",q:120,u:"g"},{nom:"Beurre",q:30,u:"g"},{nom:"Farine",q:20,u:"g"},{nom:"Lait",q:25,u:"cl"},{nom:"Moutarde",q:1,u:"c. à café"}],manquants:[],etapes:[{n:1,t:"Béchamel rapide",d:"Faites un roux avec beurre et farine. Incorporez le lait chaud en fouettant. Laissez épaissir 2 min. Assaisonnez. Incorporez la moitié du gruyère."},{n:2,t:"Assembler",d:"Tartinez l'intérieur des tranches de moutarde. Posez le jambon et 1 c. à soupe de béchamel. Refermez les sandwichs."},{n:3,t:"Gratiner",d:"Étalez le reste de béchamel sur le dessus. Parsemez du reste de gruyère. Passez sous le gril 8-10 min jusqu'à dorure."}]},

  // ──── RECETTES RAPIDES ────
  {nom:"Oeufs cocotte à la crème",categorie:"Entrée",cuisine:"française",emoji:"🥚",temps_prep:5,temps_cuisson:12,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:1234,conseil:"La cuisson au bain-marie doit être douce. Le blanc doit être pris mais le jaune encore coulant.",mots_cles:["oeuf","creme","lardons","fromage","beurre","sel"],ingredients:[{nom:"Oeufs",q:4,u:""},{nom:"Crème fraîche",q:4,u:"c. à soupe"},{nom:"Lardons",q:60,u:"g"},{nom:"Gruyère râpé",q:40,u:"g"},{nom:"Beurre",q:10,u:"g"},{nom:"Ciboulette",q:3,u:"brins"}],manquants:[],etapes:[{n:1,t:"Préparer les ramequins",d:"Préchauffez le four à 180°C. Beurrez 4 ramequins. Faites revenir les lardons. Répartissez-les dans les ramequins."},{n:2,t:"Ajouter les oeufs",d:"Versez 1 c. à soupe de crème dans chaque ramequin. Cassez délicatement un oeuf dessus. Parsemez de gruyère et de ciboulette."},{n:3,t:"Cuire",d:"Disposez les ramequins dans un plat rempli d'eau chaude (bain-marie). Enfournez 10-12 min — le blanc doit être pris et le jaune encore coulant."}]},

  {nom:"Piperade basquaise",categorie:"Plat principal",cuisine:"française",emoji:"🫑",temps_prep:15,temps_cuisson:30,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.4,nb_avis:876,conseil:"La piperade est prête quand les légumes sont fondants et les oeufs juste coagulés — arrêtez la cuisson tôt.",mots_cles:["oeuf","poivron","tomate","oignon","ail","jambon","piment"],ingredients:[{nom:"Poivrons (rouge et vert)",q:3,u:""},{nom:"Tomates",q:4,u:""},{nom:"Oignons",q:2,u:""},{nom:"Ail",q:2,u:"gousses"},{nom:"Oeufs",q:4,u:""},{nom:"Jambon de Bayonne",q:100,u:"g"},{nom:"Piment d'Espelette",q:1,u:"pincée"},{nom:"Huile d'olive",q:3,u:"c. à soupe"}],manquants:["Piment d'Espelette"],etapes:[{n:1,t:"Faire les légumes",d:"Faites revenir les oignons et l'ail dans l'huile. Ajoutez les poivrons en lanières, faites cuire 15 min. Incorporez les tomates concassées et le piment. Laissez mijoter 15 min."},{n:2,t:"Ajouter les oeufs",d:"Battez légèrement les oeufs. Versez-les sur la préparation. Mélangez doucement hors du feu jusqu'à ce qu'ils soient juste coagulés."},{n:3,t:"Servir",d:"Disposez les tranches de jambon de Bayonne à côté ou par-dessus. Servez immédiatement avec du pain de campagne."}]},

  {nom:"Soupe de poireaux-pommes de terre",categorie:"Entrée",cuisine:"française",emoji:"🥬",temps_prep:15,temps_cuisson:25,difficulte:"Très facile",budget:"Bon marché",nb_personnes:4,note:4.5,nb_avis:1987,conseil:"Servie froide avec de la crème et de la ciboulette, cette soupe devient une vichyssoise raffinée.",mots_cles:["poireau","pomme de terre","oignon","creme","beurre","bouillon"],ingredients:[{nom:"Poireaux",q:3,u:""},{nom:"Pommes de terre",q:3,u:""},{nom:"Oignon",q:1,u:""},{nom:"Bouillon de légumes",q:1,u:"L"},{nom:"Crème fraîche",q:10,u:"cl"},{nom:"Beurre",q:30,u:"g"},{nom:"Ciboulette",q:3,u:"brins"}],manquants:[],etapes:[{n:1,t:"Faire fondre les légumes",d:"Émincez les poireaux et l'oignon. Faites-les fondre dans le beurre à feu doux 10 min sans coloration."},{n:2,t:"Ajouter et cuire",d:"Épluchez et coupez les pommes de terre en dés. Ajoutez-les avec le bouillon chaud. Laissez cuire 20 min à feu moyen."},{n:3,t:"Mixer",d:"Mixez finement. Incorporez la crème, rectifiez l'assaisonnement. Servez chaud avec de la ciboulette ciselée."}]},

  {nom:"Tarte flambée (flammekueche)",categorie:"Plat principal",cuisine:"française",emoji:"🫓",temps_prep:20,temps_cuisson:12,difficulte:"Facile",budget:"Bon marché",nb_personnes:4,note:4.7,nb_avis:2341,conseil:"La pâte doit être ultra-fine — plus elle est mince, plus la tarte sera croustillante comme en Alsace.",mots_cles:["farine","oignon","lardons","creme","fromage blanc","beurre"],ingredients:[{nom:"Farine",q:250,u:"g"},{nom:"Eau tiède",q:12,u:"cl"},{nom:"Huile",q:2,u:"c. à soupe"},{nom:"Oignons",q:2,u:""},{nom:"Lardons",q:150,u:"g"},{nom:"Crème fraîche épaisse",q:15,u:"cl"},{nom:"Fromage blanc",q:15,u:"cl"},{nom:"Sel, poivre, muscade",q:1,u:"pincée"}],manquants:["Fromage blanc"],etapes:[{n:1,t:"Préparer la pâte",d:"Mélangez la farine, l'eau tiède, l'huile et le sel. Pétrissez jusqu'à obtenir une pâte lisse. Laissez reposer 30 min."},{n:2,t:"Préparer la garniture",d:"Mélangez crème et fromage blanc, assaisonnez avec sel, poivre et muscade."},{n:3,t:"Assembler et cuire",d:"Étalez la pâte très finement sur du papier sulfurisé. Étalez le mélange crème-fromage blanc. Répartissez les oignons émincés et les lardons. Enfournez 10-12 min à 250°C (four très chaud)."}]},

  {nom:"Chili con carne",categorie:"Plat principal",cuisine:"mexicaine",emoji:"🌶️",temps_prep:20,temps_cuisson:60,difficulte:"Facile",budget:"Bon marché",nb_personnes:6,note:4.6,nb_avis:3214,conseil:"Préparez-le la veille — le mariage des épices sera encore plus savoureux le lendemain.",mots_cles:["boeuf","haricots","tomate","oignon","ail","poivron","cumin","piment"],ingredients:[{nom:"Boeuf haché",q:600,u:"g"},{nom:"Haricots rouges (boîte)",q:400,u:"g"},{nom:"Tomates concassées",q:400,u:"g"},{nom:"Oignons",q:2,u:""},{nom:"Poivron rouge",q:1,u:""},{nom:"Ail",q:3,u:"gousses"},{nom:"Cumin",q:1,u:"c. à café"},{nom:"Paprika fumé",q:1,u:"c. à café"},{nom:"Piment de Cayenne",q:0.5,u:"c. à café"}],manquants:["Haricots rouges","Piment de Cayenne"],etapes:[{n:1,t:"Faire revenir",d:"Faites revenir les oignons, l'ail et le poivron en dés. Ajoutez le boeuf haché et faites brunir."},{n:2,t:"Ajouter les épices",d:"Incorporez le cumin, le paprika, le piment. Toastez 1 min. Ajoutez les tomates concassées."},{n:3,t:"Mijoter",d:"Laissez mijoter 30 min. Ajoutez les haricots rouges égouttés, prolongez 15 min. Servez avec du riz ou du pain de maïs."}]}

];

// ─── MOTEUR DE CORRESPONDANCE INTELLIGENT ───

// Table de synonymes et variantes d'ingrédients
var SYNONYMES = {
  // Oeufs
  'oeuf':['oeufs','oeuf','egg','eggs','jaune d oeuf','blanc d oeuf','jaunes','blancs'],
  // Laitages
  'lait':['lait','lait entier','lait demi ecreme','lait ecreme','lait uht','lait de vache'],
  'creme':['creme','creme fraiche','creme liquide','creme epaisse','creme fleurette','creme entiere','creme semi epaisse'],
  'beurre':['beurre','beurre doux','beurre sale','beurre demi sel','beurre fondu','margarine'],
  'fromage':['fromage','gruyere','emmental','comté','comte','parmesan','mozzarella','reblochon','brie','camembert','roquefort','cheddar','gouda','fromage rape','fromage blanc'],
  'yaourt':['yaourt','yaourt nature','yaourt grec','yogourt'],
  // Viandes
  'poulet':['poulet','poulet entier','escalope de poulet','blanc de poulet','cuisse de poulet','filet de poulet','poulet role'],
  'boeuf':['boeuf','steak','bavette','entrecote','cote de boeuf','boeuf hache','viande hachee','viande de boeuf','paleron','rumsteck','bourguignon'],
  'porc':['porc','cote de porc','filet de porc','porc hache','echine','lard','ventrèche'],
  'lardons':['lardons','lard fume','bacon','poitrine fumee','lardons fumes','lardons nature'],
  'jambon':['jambon','jambon blanc','jambon cuit','jambon de paris','jambon de bayonne','jambon sec','jambon de pays'],
  'saucisse':['saucisse','saucisses','merguez','chipolata','saucisse de toulouse','knacki'],
  'veau':['veau','escalope de veau','cote de veau','epaule de veau','blanquette de veau'],
  'agneau':['agneau','gigot','cote d agneau','souris d agneau','epaule d agneau'],
  // Poissons
  'saumon':['saumon','saumon fume','pave de saumon','filet de saumon','saumon frais'],
  'thon':['thon','thon en boite','thon rouge','steak de thon','thon entinat'],
  'moules':['moules','moules de bouchot','moules mariniere'],
  // Légumes
  'tomate':['tomate','tomates','tomates cerises','tomates concassees','coulis de tomate','concentre de tomate','tomates pelees'],
  'oignon':['oignon','oignons','oignon rouge','oignon blanc','echalote','echalotes','oignon grelot'],
  'ail':['ail','gousses d ail','ail en poudre','ail frais','gousse d ail'],
  'carotte':['carotte','carottes','carottes râpées','carottes baby'],
  'pomme de terre':['pomme de terre','pommes de terre','patate','patates','charlotte','bintje','ratte','grenaille'],
  'courgette':['courgette','courgettes','zucchini'],
  'poivron':['poivron','poivrons','poivron rouge','poivron vert','poivron jaune'],
  'champignon':['champignon','champignons','champignons de paris','champignons shiitake','pleurotes','cèpes','cepes'],
  'aubergine':['aubergine','aubergines'],
  'poireau':['poireau','poireaux'],
  'epinard':['epinard','epinards','pousses d epinards'],
  'salade':['salade','laitue','roquette','mache','mesclun','scarole'],
  'concombre':['concombre','concombres'],
  'brocoli':['brocoli','brocolis','brocoli surgele'],
  // Féculents
  'pates':['pates','spaghetti','spaghettis','penne','tagliatelles','fusilli','rigatoni','farfalle','macaroni','linguine','fettuccine'],
  'riz':['riz','riz basmati','riz long','riz rond','riz arborio','riz complet','riz pour risotto'],
  'pain':['pain','baguette','pain de mie','pain de campagne','pain rassis','pain complet','pain brio'],
  'farine':['farine','farine de ble','farine complete','farine t55','farine t65','maizena','amidon'],
  // Autres
  'sucre':['sucre','sucre blanc','sucre glace','cassonade','sucre roux','sucre de canne','vergeoise'],
  'huile':['huile','huile d olive','huile olive','huile de tournesol','huile neutre','huile vegetale'],
  'vinaigre':['vinaigre','vinaigre de vin','vinaigre balsamique','vinaigre de cidre','vinaigre blanc'],
  'moutarde':['moutarde','moutarde de dijon','moutarde a l ancienne'],
  'chocolat':['chocolat','chocolat noir','chocolat au lait','chocolat blanc','cacao'],
  'citron':['citron','citrons','citron jaune','citron vert','jus de citron','zeste de citron'],
  'pomme':['pomme','pommes','pomme golden','pomme granny'],
  'lentilles':['lentilles','lentilles vertes','lentilles corail','lentilles beluga'],
  'haricots':['haricots','haricots verts','haricots blancs','haricots rouges','pois chiches','flageolets'],
  'miel':['miel','miel d acacia','miel toutes fleurs'],
};

// Table inverse : chaque mot-clé renvoie vers sa famille
var FAMILLE_ING = {};
(function(){
  for(var fam in SYNONYMES) {
    SYNONYMES[fam].forEach(function(syn){
      FAMILLE_ING[syn] = fam;
    });
  }
})();

function normStr(s) {
  return (s||'').toLowerCase()
    .normalize('NFD').replace(/[\u0300-\u036f]/g,'')
    .replace(/[éèêë]/g,'e').replace(/[àâ]/g,'a').replace(/[ôo]/g,'o')
    .replace(/[^a-z0-9 ]/g,' ')
    .replace(/\s+/g,' ').trim();
}

function getFamille(nom) {
  var n = normStr(nom);
  // Exact match
  if(FAMILLE_ING[n]) return FAMILLE_ING[n];
  // Partial match - check if any synonym is included in the name
  for(var syn in FAMILLE_ING) {
    if(n.includes(syn) || syn.includes(n)) return FAMILLE_ING[syn];
  }
  return null;
}

function ingredientMatch(ingNom, stockItem) {
  var ingN = normStr(ingNom);
  var itN = normStr(stockItem.nom);

  // 1. Direct inclusion
  if(itN.includes(ingN) || ingN.includes(itN)) return true;

  // 2. Family match via synonymes
  var famIng = getFamille(ingNom);
  var famIt = getFamille(stockItem.nom);
  if(famIng && famIt && famIng === famIt) return true;

  // 3. Word-level match (at least one meaningful word in common)
  var ingWords = ingN.split(' ').filter(function(w){ return w.length >= 4; });
  var itWords = itN.split(' ').filter(function(w){ return w.length >= 4; });
  return ingWords.some(function(w){ return itWords.includes(w); });
}

function scoreRecette(recette, stockItems) {
  var dispo = [], manquant = [];
  var allIngs = recette.ingredients || [];

  allIngs.forEach(function(ing) {
    // Also check mots_cles of the recipe for broader matching
    var found = stockItems.some(function(it) {
      // Direct ingredient match
      if(ingredientMatch(ing.nom, it)) return true;
      // Check against recipe keywords
      return (recette.mots_cles||[]).some(function(k){
        var kN = normStr(k);
        var itN = normStr(it.nom);
        return itN.includes(kN) || kN.includes(itN) ||
               (getFamille(k) && getFamille(k) === getFamille(it.nom));
      });
    });
    if(found) dispo.push({nom:ing.nom, quantite:ing.q, unite:ing.u});
    else manquant.push(ing.nom + (ing.q ? ' (' + ing.q + (ing.u?' '+ing.u:'') + ')' : ''));
  });

  return {
    matched: dispo.length,
    total: allIngs.length,
    pct: allIngs.length ? dispo.length / allIngs.length : 0,
    dispo: dispo,
    manquant: manquant
  };
}

async function generateRecipes() {
  if(!allItems || !allItems.length) { showToast('⚠️ Stock vide — ajoute des produits d\'abord !'); return; }

  var btn = document.getElementById('btn-generate');
  var loadEl = document.getElementById('chef-loading');
  var listEl = document.getElementById('recipe-list');

  btn.classList.add('loading');
  btn.querySelector('span:nth-child(2)').textContent = 'Le chef cuisine…';
  loadEl.style.display = 'block';
  listEl.innerHTML = '';

  // Small delay so the UI updates before the calculation
  await new Promise(function(r){ setTimeout(r, 300); });

  try {
    currentRecipes = buildRecipesFromStock(allItems);
  } catch(e) {
    listEl.innerHTML = '<div class="empty"><div class="empty-icon">❌</div><div class="empty-text">Erreur : ' + (e.message||e) + '</div></div>';
    btn.classList.remove('loading');
    btn.querySelector('span:nth-child(2)').textContent = 'Générer des recettes';
    loadEl.style.display = 'none';
    return;
  }

  if(!currentRecipes.length) {
    listEl.innerHTML = '<div class="empty"><div class="empty-icon">🤔</div><div class="empty-text">Aucune recette ne correspond à votre stock.</div></div>';
  } else {
    renderRecipes(currentRecipes);
    renderFavSection();
  }

  btn.classList.remove('loading');
  btn.querySelector('span:nth-child(2)').textContent = 'Générer des recettes';
  loadEl.style.display = 'none';
}

function buildRecipesFromStock(items) {
  var today = new Date(); today.setHours(0,0,0,0);

  // Score each recipe
  var scored = RECETTES_DB.map(function(r) {
    var s = scoreRecette(r, items);
    // Bonus for using urgent items
    var urgentBonus = items.filter(function(it) {
      var diff = Math.ceil((new Date(it.date_perempt) - today) / 86400000);
      if(diff > 3) return false;
      return r.mots_cles.some(function(k){ return normStr(it.nom).includes(normStr(k)); });
    }).length * 0.15;

    return {
      recette: r,
      score: s.pct + urgentBonus,
      dispo: s.dispo,
      manquant: s.manquant,
      matched: s.matched,
      total: s.total
    };
  });

  // Filter: at least 1 ingredient available, sort by score desc
  var filtered = scored
    .filter(function(s){ return s.matched >= 1; })
    .sort(function(a,b){ return b.score - a.score; });

  // Apply cuisine filter
  if(currentCountry) {
    var cl = currentCountry.toLowerCase();
    var cuisineFiltered = filtered.filter(function(s){
      return normStr(s.recette.cuisine).includes(cl) || normStr(s.recette.categorie).includes(cl);
    });
    if(cuisineFiltered.length) filtered = cuisineFiltered;
  }

  // Apply diet filters
  if(activeDiets && activeDiets.includes('vegan')) {
    var veganFiltered = filtered.filter(function(s){ return s.recette.cuisine !== 'française' || normStr(s.recette.categorie).includes('veg'); });
    if(veganFiltered.length) filtered = veganFiltered;
  }

  // Take top 6
  return filtered.slice(0, 6).map(function(s) {
    var r = s.recette;
    return {
      nom: r.nom,
      categorie: r.categorie,
      cuisine: r.cuisine,
      emoji: r.emoji,
      temps: (r.temps_prep + r.temps_cuisson) + ' min',
      temps_prep: r.temps_prep,
      temps_cuisson: r.temps_cuisson,
      difficulte: r.difficulte,
      budget: r.budget,
      nb_personnes: r.nb_personnes || 4,
      note: r.note,
      nb_avis: r.nb_avis,
      conseil: r.conseil,
      ingredients_dispo: s.dispo,
      ingredients_manquants: s.manquant,
      etapes: (r.etapes||[]).map(function(e){ return {numero:e.n, titre:e.t, detail:e.d}; }),
      score_pct: Math.round(s.score * 100)
    };
  });
}


// ─── PHOTOS AUTOMATIQUES ───
var photoCache = {};

function buildUnsplashQuery(recipe) {
  var keywords = {
    'quiche':'quiche lorraine food',
    'poulet':'roasted chicken food',
    'gratin':'gratin potatoes food',
    'soupe':'french onion soup food',
    'carbonara':'carbonara pasta',
    'risotto':'mushroom risotto',
    'moules':'moules marinière seafood',
    'saumon':'salmon dish food',
    'tarte':'tarte food pastry',
    'crêpes':'french crepes food',
    'mousse':'chocolate mousse dessert',
    'gâteau':'chocolate cake food',
    'clafoutis':'clafoutis cherry dessert',
    'fondant':'chocolate fondant dessert',
    'tatin':'tarte tatin apple',
    'crème brûlée':'crème brûlée dessert',
    'boeuf':'beef bourguignon stew',
    'blanquette':'veal blanquette french',
    'coq au vin':'coq au vin chicken wine',
    'ratatouille':'ratatouille vegetables',
    'lasagnes':'lasagna bolognese',
    'pizza':'pizza food',
    'curry':'curry vegetables',
    'chili':'chili con carne',
    'pancakes':'pancakes breakfast',
    'pain perdu':'french toast',
    'tartiflette':'tartiflette cheese potatoes',
    'cassoulet':'cassoulet beans',
    'gaspacho':'gazpacho tomato soup',
    'falafels':'falafel plate',
    'guacamole':'guacamole avocado',
    'bruschetta':'bruschetta tomato',
    'croque':'croque monsieur sandwich',
    'hachis':'shepherd pie food',
    'gratin de chou':'cauliflower gratin',
    'velouté':'cream soup velvet',
    'daube':'beef stew provençal',
    'pot-au-feu':'pot au feu french',
    'veau':'veal marengo',
    'escalope':'schnitzel wiener',
    'steak':'steak red wine sauce',
    'penne':'penne arrabiata pasta',
    'lentilles':'lentil salad warm',
    'riz':'fried rice asian',
    'tarte flambée':'flammekueche alsace',
    'financiers':'financier almond cake',
    'île flottante':'île flottante dessert'
  };
  var nom = (recipe.nom||'').toLowerCase();
  for(var k in keywords) {
    if(nom.includes(k)) return keywords[k];
  }
  // Fallback to category
  var catMap = {
    'dessert':'dessert food photography',
    'entrée':'appetizer food photography',
    'plat principal':'main course food photography',
    'accompagnement':'side dish food photography',
    'petit-déjeuner':'breakfast food photography'
  };
  var cat = (recipe.categorie||'').toLowerCase();
  return catMap[cat] || (recipe.nom + ' food recipe');
}

async function loadRecipeCardPhoto(idx, elementId) {
  var r = currentRecipes[idx]; if(!r) return;
  var el = document.getElementById(elementId); if(!el) return;
  var query = buildUnsplashQuery(r);
  var cacheKey = query.replace(/\s+/g,'_');
  
  if(photoCache[cacheKey]) {
    el.innerHTML = '<img src="'+photoCache[cacheKey]+'" class="recipe-card-img" alt="'+r.nom+'">';
    return;
  }
  
  // Use Unsplash source (no API key needed)
  var seed = encodeURIComponent(r.nom);
  var url = 'https://source.unsplash.com/120x120/?' + encodeURIComponent(query) + '&sig=' + seed;
  
  var img = new Image();
  img.onload = function() {
    photoCache[cacheKey] = url;
    if(document.getElementById(elementId)) {
      document.getElementById(elementId).innerHTML = '<img src="'+url+'" class="recipe-card-img" alt="'+r.nom+'">';
    }
  };
  img.onerror = function() { /* keep emoji fallback */ };
  img.src = url;
}

async function loadRecipeModalPhoto(recipe) {
  var wrap = document.getElementById('recipe-modal-photo'); if(!wrap) return;
  var query = buildUnsplashQuery(recipe);
  var seed = encodeURIComponent(recipe.nom);
  var url = 'https://source.unsplash.com/700x300/?' + encodeURIComponent(query) + '&sig=' + seed;
  
  var img = new Image();
  img.onload = function() {
    wrap.innerHTML = '<img src="'+url+'" class="recipe-modal-full-img" alt="'+recipe.nom+'">';
  };
  img.onerror = function() {
    wrap.innerHTML = '<div class="recipe-img-placeholder" style="font-size:60px">'+recipe.emoji+'</div>';
  };
  img.src = url;
}

function renderStars(note) {
  var full = Math.floor(note), half = note - full >= 0.5 ? 1 : 0, s = '';
  for(var i=0;i<full;i++) s += '★';
  if(half) s += '½';
  for(var j=full+half;j<5;j++) s += '☆';
  return s;
}

function renderRecipes(recettes) {
  var list = document.getElementById('recipe-list');
  if(!recettes || !recettes.length) {
    list.innerHTML = '<div class="empty"><div class="empty-icon">🤔</div><div class="empty-text">Aucune recette pour ce filtre.</div></div>';
    return;
  }

  list.innerHTML = recettes.map(function(r, i) {
    var have = (r.ingredients_dispo||[]).length;
    var total = have + (r.ingredients_manquants||[]).length;
    var pct = total ? Math.round(have/total*100) : 100;
    var badgeCol = pct>=80 ? 'var(--ok)' : pct>=50 ? 'var(--warn)' : 'var(--muted)';
    var isFav = isRecipeFav(r.nom);
    var dTags = (r.ingredients_dispo||[]).slice(0,3).map(function(ing){ return '<span class="recipe-tag">'+(ing.nom||ing)+'</span>'; }).join('');
    var mTags = (r.ingredients_manquants||[]).slice(0,2).map(function(ing){ return '<span class="recipe-tag missing">+ '+ing.split(' (')[0]+'</span>'; }).join('');
    var noteStr = r.note ? renderStars(Math.round(r.note*2)/2) + ' <span style="color:var(--muted);font-size:10px">('+r.nb_avis+')</span>' : '';

    var photoId = 'rphoto_' + i + '_' + Date.now();
    setTimeout(function(idx, pid){ loadRecipeCardPhoto(idx, pid); }, i*50, i, photoId);
    return '<div class="recipe-card" style="animation-delay:'+(i*.07)+'s;position:relative" onclick="openRecipe('+i+')">' +
      '<div style="position:relative">' +
        '<div class="recipe-thumb" id="' + photoId + '">' +
          '<div class="recipe-emoji">' + r.emoji + '</div>' +
        '</div>' +
        '<div class="marmiton-badge">M</div>' +
      '</div>' +
      '<div class="recipe-info">' +
        '<div class="recipe-name">' + r.nom + '</div>' +
        '<div class="recipe-meta">⏱ ' + r.temps + ' · ' + r.difficulte + ' · ' + (r.budget||'') + '</div>' +
        (noteStr ? '<div class="recipe-stars">' + noteStr + '</div>' : '') +
        '<div class="recipe-ingredients">' + dTags + mTags + '</div>' +
      '</div>' +
      '<div style="display:flex;flex-direction:column;align-items:flex-end;gap:4px;flex-shrink:0">' +
        '<span style="font-family:var(--font-display);font-size:13px;font-weight:900;color:'+badgeCol+'">' + have + '/' + total + '</span>' +
        '<span style="font-size:9px;color:var(--muted);font-weight:600">ingred.</span>' +
        '<button class="recipe-fav-btn' + (isFav?' active':'') + '" onclick="event.stopPropagation();toggleRecipeFav('+i+')" style="font-size:18px;background:none;border:none;cursor:pointer">' + (isFav?'⭐':'☆') + '</button>' +
      '</div>' +
    '</div>';
  }).join('');
}

function renderIngredients(dispo, manquant, servings) {
  var factor = servings / BASE_SERVINGS;
  var dH = (dispo||[]).map(function(i) {
    var qty = i.quantite ? Math.round(i.quantite * factor * 10) / 10 : null;
    var qtyStr = qty ? (qty%1===0?qty:qty.toFixed(1)) + (i.unite&&i.unite!==''?' '+i.unite:'') : '';
    return '<span class="ing-pill have">✓ ' + (i.nom||i) + (qtyStr?' — '+qtyStr:'') + '</span>';
  }).join('');
  var mH = (manquant||[]).map(function(i){ return '<span class="ing-pill need">+ ' + i + '</span>'; }).join('');
  return dH + mH;
}

function openRecipe(idx) {
  var r = currentRecipes[idx]; if(!r) return;
  activeRecipeIdx = idx; currentServings = r.nb_personnes || 4; BASE_SERVINGS = currentServings;

  document.getElementById('modal-emoji').textContent = r.emoji;
  document.getElementById('modal-title').textContent = r.nom;
  document.getElementById('modal-meta').textContent = '⏱ ' + r.temps + ' · ' + r.difficulte + ' · ' + (r.cuisine||'');

  var mfb = document.getElementById('modal-fav-btn');
  if(mfb) { mfb.textContent = isRecipeFav(r.nom) ? '⭐' : '☆'; mfb.style.opacity = isRecipeFav(r.nom) ? '1' : '0.5'; }

  var noteHtml = r.note ? '<div class="marmiton-note-row"><span class="marmiton-stars">'+renderStars(r.note)+'</span><span class="marmiton-note-val">'+r.note.toFixed(1)+'/5</span><span class="marmiton-note-avis">('+r.nb_avis+' avis)</span></div>' : '';
  var metaHtml = '<div class="marmiton-meta-row">' +
    '<div class="marmiton-meta-item"><span class="marmiton-meta-icon">⏱</span><span class="marmiton-meta-label">Prépa</span><span class="marmiton-meta-val">'+(r.temps_prep||15)+' min</span></div>' +
    '<div class="marmiton-meta-item"><span class="marmiton-meta-icon">🔥</span><span class="marmiton-meta-label">Cuisson</span><span class="marmiton-meta-val">'+(r.temps_cuisson||0)+' min</span></div>' +
    '<div class="marmiton-meta-item"><span class="marmiton-meta-icon">📊</span><span class="marmiton-meta-label">Difficulté</span><span class="marmiton-meta-val">'+r.difficulte+'</span></div>' +
    '<div class="marmiton-meta-item"><span class="marmiton-meta-icon">💰</span><span class="marmiton-meta-label">Budget</span><span class="marmiton-meta-val">'+(r.budget||'')+'</span></div>' +
  '</div>';
  var conseil = r.conseil ? '<div class="marmiton-conseil"><span class="marmiton-conseil-icon">💡</span><span>'+r.conseil+'</span></div>' : '';

  document.getElementById('modal-body').innerHTML =
    '<div id="recipe-modal-photo" class="recipe-modal-photo-wrap"><div class="recipe-img-placeholder" style="font-size:60px">'+r.emoji+'</div></div>' +
    noteHtml + metaHtml +
    '<div class="servings-row"><span class="servings-label">👥 Personnes</span><div class="servings-ctrl"><button class="serv-btn" onclick="changeServings('+idx+',-1)">−</button><span class="serv-count" id="serv-count">'+currentServings+'</span><button class="serv-btn" onclick="changeServings('+idx+',1)">+</button></div></div>' +
    '<div class="recipe-section-title">🛒 Ingrédients</div>' +
    '<div class="recipe-ingredients-list" id="ing-list">'+renderIngredients(r.ingredients_dispo, r.ingredients_manquants, currentServings)+'</div>' +
    conseil +
    '<div class="recipe-section-title">📋 Étapes de préparation</div>' +
    (r.etapes||[]).map(function(e){ return '<div class="step-item"><div class="step-num">'+e.numero+'</div><div class="step-text"><strong>'+(e.titre||'Étape '+e.numero)+'</strong><br>'+e.detail+'</div></div>'; }).join('') +
    '<div class="marmiton-source-badge">Recette <strong>Marmiton</strong> 🧡 — Sélection du Chef IA</div>' +
    '<button class="btn-cook" onclick="openCookMode('+idx+')"><span>👨‍🍳</span> Mode Cuisson guidé</button>' +
    '<button class="btn-cook" style="background:linear-gradient(135deg,#059669,#34d399);margin-top:8px;box-shadow:0 10px 30px rgba(52,211,153,0.4)" onclick="cookRecipe('+idx+')"><span>🍽️</span> Cuire & déduire du stock</button>';

  document.getElementById('recipe-modal').classList.add('open');
  loadRecipeModalPhoto(r);
}

function changeServings(idx, delta) {
  var nv = Math.max(1, Math.min(12, currentServings+delta));
  if(nv===currentServings) return;
  currentServings = nv;
  document.getElementById('serv-count').textContent = nv;
  var r = currentRecipes[idx]; if(!r) return;
  var il = document.getElementById('ing-list');
  if(il) il.innerHTML = renderIngredients(r.ingredients_dispo, r.ingredients_manquants, nv);
}

function closeRecipeModal() { document.getElementById('recipe-modal').classList.remove('open'); activeRecipeIdx = null; }
document.getElementById('recipe-modal').addEventListener('click', function(e){ if(e.target===this) closeRecipeModal(); });

async function cookRecipe(idx) {
  var r = currentRecipes[idx]; if(!r) return;
  var factor = currentServings / BASE_SERVINGS;
  var dispo = r.ingredients_dispo || [];
  if(!dispo.length) { showToast('Aucun ingrédient à déduire.'); return; }
  var btn = document.querySelector('.btn-cook');
  if(btn) { btn.textContent='⏳ Déduction...'; btn.style.opacity='.6'; btn.disabled=true; }
  var ok = 0;
  for(var i=0;i<dispo.length;i++) {
    var ingNom=(dispo[i].nom||dispo[i]).toLowerCase();
    var match=allItems.find(function(it){ return it.nom.toLowerCase().includes(ingNom)||ingNom.includes(it.nom.toLowerCase()); });
    if(!match) continue;
    var usedQty=Math.ceil((dispo[i].quantite||1)*factor);
    var newQty=(match.quantite||1)-usedQty;
    try {
      if(newQty<=0) await fetch(URL_BASE+'?id=eq.'+match.id,{method:'DELETE',headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY}});
      else await fetch(URL_BASE+'?id=eq.'+match.id,{method:'PATCH',headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY,"Content-Type":"application/json","Prefer":"return=minimal"},body:JSON.stringify({quantite:newQty})});
      ok++;
    } catch(e) { console.error(e); }
  }
  addToHistory(r, currentServings);
  closeRecipeModal(); await fetchStock(); showTab('stock');
  showToast('✅ Bon appétit ! '+ok+' ingrédient'+(ok>1?'s':'')+' déduit'+(ok>1?'s':'')+'.',3500);
}

function filterCountry(c, el) {
  currentCountry = c;
  document.querySelectorAll('#country-chips .chip').forEach(function(x){ x.classList.remove('active'); });
  el.classList.add('active');
  if(currentRecipes.length) renderRecipes(currentRecipes);
}

// ══════════════════════════════════════
//  MODE CUISSON GUIDÉ (step-by-step)
// ══════════════════════════════════════
var cookSteps=[], cookStepIdx=0, cookTimerInterval=null, cookTimerSeconds=0, cookTimerRunning=false;

function openCookMode(idx){
  var r=currentRecipes[idx]; if(!r) return;
  cookSteps=r.etapes||[]; cookStepIdx=0;
  document.getElementById('cook-recipe-title').textContent=r.nom;
  closeRecipeModal();
  renderCookStep();
  document.getElementById('cook-mode').classList.add('open');
  if(navigator.wakeLock) navigator.wakeLock.request('screen').catch(function(){});
}

function closeCookMode(){
  document.getElementById('cook-mode').classList.remove('open');
  clearInterval(cookTimerInterval); cookTimerRunning=false;
}

function renderCookStep(){
  var step=cookSteps[cookStepIdx]; if(!step) return;
  var total=cookSteps.length;
  document.getElementById('cook-step-num').textContent='ÉTAPE '+(cookStepIdx+1)+' / '+total;
  document.getElementById('cook-step-title').textContent=step.titre;
  document.getElementById('cook-step-detail').textContent=step.detail;
  var pct=((cookStepIdx+1)/total)*100;
  document.getElementById('cook-progress-fill').style.width=pct+'%';
  // Timer: estimate based on step keyword
  var hasTimer=/(cuire|faire revenir|chauffer|bouillir|mijoter|cuisson|rôtir|griller|préchauffer|attendre|repos|refroidir)/i.test(step.detail+step.titre);
  var timerWrap=document.getElementById('cook-timer-wrap');
  timerWrap.style.display=hasTimer?'block':'none';
  if(hasTimer){
    var mins=estimateCookTime(step.detail);
    cookTimerSeconds=mins*60;
    clearInterval(cookTimerInterval); cookTimerRunning=false;
    document.getElementById('cook-timer-start-btn').textContent='▶ Démarrer';
    updateTimerDisplay();
  }
  document.getElementById('cook-prev-btn').style.display=cookStepIdx===0?'none':'flex';
  document.getElementById('cook-next-btn').style.display=cookStepIdx===total-1?'none':'flex';
  document.getElementById('cook-finish-btn').style.display=cookStepIdx===total-1?'flex':'none';
}

function estimateCookTime(text){
  var m=text.match(/(\d+)\s*(?:à|a|-)\s*(\d+)\s*min/i); if(m) return parseInt(m[2]);
  var m2=text.match(/(\d+)\s*min/i); if(m2) return parseInt(m2[1]);
  var m3=text.match(/(\d+)\s*h/i); if(m3) return parseInt(m3[1])*60;
  return 5;
}

function startTimer(){
  if(cookTimerRunning){clearInterval(cookTimerInterval);cookTimerRunning=false;document.getElementById('cook-timer-start-btn').textContent='▶ Continuer';return;}
  cookTimerRunning=true; document.getElementById('cook-timer-start-btn').textContent='⏸ Pause';
  cookTimerInterval=setInterval(function(){
    cookTimerSeconds--; updateTimerDisplay();
    if(cookTimerSeconds<=0){clearInterval(cookTimerInterval);cookTimerRunning=false;showToast('⏰ Minuteur terminé !');try{new Notification('⏰ Colossus Stock',{body:'Le minuteur est terminé !'});}catch(e){};}
  },1000);
}

function resetTimer(){clearInterval(cookTimerInterval);cookTimerRunning=false;var step=cookSteps[cookStepIdx];if(step){cookTimerSeconds=estimateCookTime(step.detail)*60;}updateTimerDisplay();document.getElementById('cook-timer-start-btn').textContent='▶ Démarrer';}

function updateTimerDisplay(){
  var m=Math.floor(cookTimerSeconds/60),s=cookTimerSeconds%60;
  document.getElementById('cook-timer-display').textContent=(m<10?'0':'')+m+':'+(s<10?'0':'')+s;
  document.getElementById('cook-timer-display').style.color=cookTimerSeconds<=30?'var(--danger)':cookTimerSeconds<=60?'var(--warn)':'var(--accent)';
}

function cookNext(){if(cookStepIdx<cookSteps.length-1){cookStepIdx++;clearInterval(cookTimerInterval);cookTimerRunning=false;renderCookStep();}}
function cookPrev(){if(cookStepIdx>0){cookStepIdx--;clearInterval(cookTimerInterval);cookTimerRunning=false;renderCookStep();}}
function cookFinish(){closeCookMode();showToast('🎉 Recette terminée ! Bon appétit !',3000);}

// ══════════════════════════════════════
//  PLANNING SEMAINE
// ══════════════════════════════════════
var DAYS=['Lundi','Mardi','Mercredi','Jeudi','Vendredi','Samedi','Dimanche'];
var DAY_COLORS=['#5b8cff','#a78bfa','#34d399','#fbbf24','#f87171','#f472b6','#38bdf8'];
var planning=JSON.parse(localStorage.getItem('colossus_planning')||'null')||DAYS.map(function(){return{lunch:null,dinner:null};});
var pmTarget=null;

function savePlanning(){try{localStorage.setItem('colossus_planning',JSON.stringify(planning));}catch(e){}}
function getWeekDates(){
  var now=new Date(),mon=new Date(now),day=now.getDay(),diff=day===0?-6:1-day;
  mon.setDate(now.getDate()+diff);
  return DAYS.map(function(_,i){var d=new Date(mon);d.setDate(mon.getDate()+i);return d.toLocaleDateString('fr-FR',{day:'numeric',month:'short'});});
}
function guessEmoji(n){n=n.toLowerCase();if(/omelette|oeuf/.test(n))return'🍳';if(/pates|pasta|spagh/.test(n))return'🍝';if(/pizza/.test(n))return'🍕';if(/salade/.test(n))return'🥗';if(/soupe|vel/.test(n))return'🍲';if(/poulet/.test(n))return'🍗';if(/boeuf|steak|burger/.test(n))return'🥩';if(/poisson|saumon/.test(n))return'🐟';if(/riz|risotto/.test(n))return'🍚';if(/tarte|quiche/.test(n))return'🥧';if(/crepe/.test(n))return'🥞';if(/sandwich|croque/.test(n))return'🥪';if(/curry/.test(n))return'🍛';if(/dessert|gateau/.test(n))return'🎂';return'🍽️';}

function renderPlanning(){
  var wrap=document.getElementById('planning-days'),dates=getWeekDates(),today=new Date().getDay(),todayIdx=today===0?6:today-1;
  wrap.innerHTML=DAYS.map(function(day,i){
    var p=planning[i],isToday=i===todayIdx,c=DAY_COLORS[i];
    return '<div class="planning-day-card" style="animation-delay:'+(i*.04)+'s'+(isToday?';border-color:rgba(255,255,255,0.12)':'')+'">'+
      '<div class="planning-day-header"><div class="planning-day-dot" style="background:'+c+'"></div><span class="planning-day-name">'+day+(isToday?' <span style="color:'+c+';font-size:9px">● Aujourd\'hui</span>':'')+'</span><span class="planning-day-date">'+dates[i]+'</span></div>'+
      '<div class="planning-slots">'+slotHTML(p.lunch,'lunch',i)+slotHTML(p.dinner,'dinner',i)+'</div></div>';
  }).join('');
}

function slotHTML(meal,slot,dayIdx){
  var label=slot==='lunch'?'☀️ Déjeuner':'🌙 Dîner',cls=slot==='dinner'?'dinner':'';
  if(meal) return '<div class="planning-slot has-meal '+cls+'" onclick="openPlanningModal('+dayIdx+',\''+slot+'\')"><div class="slot-label">'+label+'</div><div class="slot-emoji">'+(meal.emoji||'🍽️')+'</div><div class="slot-meal">'+meal.nom+'</div></div>';
  return '<div class="planning-slot '+cls+'" onclick="openPlanningModal('+dayIdx+',\''+slot+'\')"><div class="slot-label">'+label+'</div><div class="slot-empty">Appuyer pour<br>ajouter</div><span class="slot-add-icon">+</span></div>';
}

function openPlanningModal(dayIdx,slot){
  pmTarget={dayIdx:dayIdx,slot:slot};
  var meal=planning[dayIdx][slot];
  document.getElementById('pm-day-icon').textContent=slot==='lunch'?'☀️':'🌙';
  document.getElementById('pm-day-title').textContent=DAYS[dayIdx];
  document.getElementById('pm-slot-label').textContent=slot==='lunch'?'Déjeuner':'Dîner';
  document.getElementById('pm-custom-input').value=meal?meal.nom:'';
var currentMeal = planning[dayIdx][slot];
document.getElementById('pm-clear-btn').style.display = currentMeal ? 'block' : 'none';
  var rl=document.getElementById('pm-recipe-list');
  rl.innerHTML=currentRecipes.length?currentRecipes.map(function(r,i){return '<div class="pm-recipe-option" onclick="setPlanningRecipe('+i+')"><span class="pm-recipe-option-emoji">'+r.emoji+'</span><span class="pm-recipe-option-name">'+r.nom+'</span><span class="pm-recipe-option-time">'+r.temps+'</span></div>';}).join(''):'<div style="color:var(--muted);font-size:12px;text-align:center;padding:10px">Génère des recettes pour les voir ici</div>';
  document.getElementById('planning-modal').classList.add('open');
  setTimeout(function(){document.getElementById('pm-custom-input').focus();},400);
}
function closePlanningModal(){document.getElementById('planning-modal').classList.remove('open');pmTarget=null;}
document.getElementById('planning-modal').addEventListener('click',function(e){if(e.target===this)closePlanningModal();});
document.getElementById('pm-custom-input').addEventListener('keydown',function(e){if(e.key==='Enter')setPlanningCustom();});

function setPlanningCustom(){
  var nom=document.getElementById('pm-custom-input').value.trim();
  if(!nom||!pmTarget){showToast('⚠️ Saisis un nom de plat');return;}
  planning[pmTarget.dayIdx][pmTarget.slot]={nom:nom,emoji:guessEmoji(nom)};
  savePlanning();closePlanningModal();renderPlanning();
  showToast('✅ '+nom+' ajouté !');
}
function setPlanningRecipe(i){
  if(!pmTarget) return;
  var r=currentRecipes[i]; if(!r) return;
  planning[pmTarget.dayIdx][pmTarget.slot]={nom:r.nom,emoji:r.emoji};
  savePlanning();closePlanningModal();renderPlanning();
  showToast('✅ '+r.emoji+' '+r.nom+' placé !');
}
function clearPlanningSlot(){
  if(!pmTarget) { showToast('⚠️ Aucun repas sélectionné'); return; }
  planning[pmTarget.dayIdx][pmTarget.slot] = null;
  savePlanning();
  closePlanningModal();
  renderPlanning();
  showToast('🗑️ Repas supprimé');
}function closePlanningModal(){
  document.getElementById('planning-modal').classList.remove('open');
  pmTarget = null;  // ← déjà présent, vérifie qu'il y est
}
function resetPlanning(){if(!confirm('Réinitialiser tout le planning ?')) return;planning=DAYS.map(function(){return{lunch:null,dinner:null};});savePlanning();renderPlanning();showToast('🗑️ Planning réinitialisé');}

function autoFillPlanning(){
  if(!currentRecipes.length&&!recipeFavs.length){showToast('⚠️ Génère des recettes d\'abord !',3000);return;}
  var pool=currentRecipes.length?currentRecipes:recipeFavs;
  var today=new Date();today.setHours(0,0,0,0);
  var urgents=allItems.filter(function(it){return Math.ceil((new Date(it.date_perempt)-today)/86400000)<=3;}).map(function(it){return it.nom;});
  // Prioritise recipes using urgent items
  var prioritized=pool.slice().sort(function(a,b){
    var aScore=a.ingredients_dispo.filter(function(i){return urgents.some(function(u){return i.nom.toLowerCase().includes(u.toLowerCase());});}).length;
    var bScore=b.ingredients_dispo.filter(function(i){return urgents.some(function(u){return i.nom.toLowerCase().includes(u.toLowerCase());});}).length;
    return bScore-aScore;
  });
  var ri=0;
  DAYS.forEach(function(_,i){
    planning[i].lunch=prioritized[ri%prioritized.length]?{nom:prioritized[ri%prioritized.length].nom,emoji:prioritized[ri%prioritized.length].emoji}:null;ri++;
    planning[i].dinner=prioritized[ri%prioritized.length]?{nom:prioritized[ri%prioritized.length].nom,emoji:prioritized[ri%prioritized.length].emoji}:null;ri++;
  });
  savePlanning();renderPlanning();
  showToast('⚡ Planning généré automatiquement !',3000);
}

renderPlanning();
renderFavSection();

// ══════════════════════════════════════
//  SCANNER / BARCODE
// ══════════════════════════════════════
var html5Scanner=null, lastBarcode=null;

function openScanner(){
  var modal=document.getElementById('scan-modal');
  modal.classList.add('open');
  document.getElementById('scan-result-panel').classList.remove('open');
  setStatus('Initialisation caméra...','');
  lastBarcode=null; startScanner();
}
function closeScanner(){ stopScanner(); document.getElementById('scan-modal').classList.remove('open'); document.getElementById('scan-result-panel').classList.remove('open'); }
async function stopScanner(){ if(html5Scanner){ try{if(html5Scanner.isScanning)await html5Scanner.stop();html5Scanner.clear();}catch(e){}html5Scanner=null; } }

async function startScanner(){
  await stopScanner();
  var container=document.getElementById('scan-video-wrap'); container.innerHTML='';
  try{
    html5Scanner=new Html5Qrcode('scan-video-wrap');
    var cfg={fps:15,qrbox:{width:240,height:180},aspectRatio:1.0,formatsToSupport:[Html5QrcodeSupportedFormats.EAN_13,Html5QrcodeSupportedFormats.EAN_8,Html5QrcodeSupportedFormats.CODE_128,Html5QrcodeSupportedFormats.UPC_A,Html5QrcodeSupportedFormats.UPC_E]};
    await html5Scanner.start({facingMode:'environment'},cfg,async function(code){
      if(code===lastBarcode) return;
      lastBarcode=code; await stopScanner(); onBarcodeDetected(code);
    },function(){});
    setStatus('Pointez sur un code-barres...','');
  }catch(err){
    var msg=err.toString();
    if(msg.includes('NotAllowedError')||msg.includes('Permission')) setStatus('🔒 Accès caméra refusé. Autorisez dans les réglages.','error');
    else if(msg.includes('NotFoundError')) setStatus('📷 Aucune caméra trouvée.','error');
    else setStatus('⚠️ '+(err.message||err),'error');
  }
}

function setStatus(msg,type){ var el=document.getElementById('scan-status'); el.textContent=msg; el.className='scan-status'+(type?' '+type:''); }

async function onBarcodeDetected(barcode){
  setStatus('🔍 '+barcode+' — Recherche...','');
  try{
    var r=await fetch('https://world.openfoodfacts.org/api/v3/product/'+barcode+'.json');
    var data=await r.json();
    if(data.status==='success'&&data.product){
      var p=data.product;
      var name=p.product_name_fr||p.product_name||'Produit '+barcode;
      var brand=p.brands||'';
      document.getElementById('res-name').textContent=name;
      document.getElementById('res-brand').textContent=brand?'🏷 '+brand:'📦 '+barcode;
      var cats=(p.categories||'').toLowerCase();
      var cat='Placard';
      if(/surgel|congel|frozen/.test(cats)) cat='Congelo';
      else if(/frais|refrigere|dairy|lait|fromage|yaourt|charcuter/.test(cats)) cat='Frigo';
      else if(/vin|biere|alcool|cave/.test(cats)) cat='Cave';
      document.getElementById('res-cat').value=cat;
      setStatus('✅ Produit identifié !','found');
    } else {
      document.getElementById('res-name').textContent='Produit inconnu';
      document.getElementById('res-brand').textContent='📦 Code : '+barcode;
      setStatus('⚠️ Non trouvé. Compléter manuellement.','error');
    }
  }catch(e){
    document.getElementById('res-name').textContent='Inconnu';
    document.getElementById('res-brand').textContent='📦 '+barcode;
    setStatus('⚠️ Vérifiez votre connexion.','error');
  }
  document.getElementById('res-qty').value='1';
  document.getElementById('res-date').value=new Date().toISOString().split('T')[0];
  document.getElementById('scan-result-panel').classList.add('open');
}

async function saveScanResult(){
  var nom=document.getElementById('res-name').textContent;
  var cat=document.getElementById('res-cat').value, qty=document.getElementById('res-qty').value, date=document.getElementById('res-date').value, unit=document.getElementById('res-unit').value;
  if(!date||nom==='—'){showToast('⚠️ Remplis la date !');return;}
  var btn=document.querySelector('.btn-scan-add'); btn.textContent='Ajout...'; btn.style.opacity='0.7';
  try{
    var payload={nom:nom,categorie:cat,date_perempt:date,ajoute_par:getCurrentUserName(),quantite:parseFloat(qty)};
    if(pendingPhotoData) payload.photo=pendingPhotoData;
    var r=await fetch(URL_BASE,{method:'POST',headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY,"Content-Type":"application/json","Prefer":"return=minimal"},body:JSON.stringify(payload)});
    if(r.ok||r.status===201){ showToast('✅ '+nom+' ajouté !'); closeScanner(); fetchStock(); showTab('stock'); pendingPhotoData=null; }
    else showToast('❌ Erreur');
  }catch(e){showToast('❌ Erreur réseau');}
  finally{btn.textContent='✓ Ajouter au stock'; btn.style.opacity='1';}
}

async function restartScan(){
  document.getElementById('scan-result-panel').classList.remove('open');
  lastBarcode=null; setStatus('Redémarrage...',''); await startScanner();
}

document.getElementById('scan-modal').addEventListener('click',function(e){if(e.target===this)closeScanner();});

// ══════════════════════════════════════
//  OCR TICKET DE CAISSE
// ══════════════════════════════════════
async function processTicket(event){
  var file=event.target.files[0]; if(!file) return;
  var reader=new FileReader();
  reader.onload=async function(e){
    var base64=e.target.result.split(',')[1];
    document.getElementById('ocr-result').style.display='block';
    var preview=document.getElementById('ocr-preview');
    preview.src=e.target.result; preview.style.display='block';
    document.getElementById('ocr-items-list').innerHTML='<div style="text-align:center;color:var(--muted);padding:20px">🔍 Analyse du ticket en cours...</div>';
    try{
      var resp=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-haiku-4-5-20251001',max_tokens:1000,messages:[{role:'user',content:[{type:'image',source:{type:'base64',media_type:file.type,data:base64}},{type:'text',text:'Tu es un assistant qui lit les tickets de caisse. Extrais la liste des produits alimentaires de ce ticket. Réponds UNIQUEMENT avec un JSON valide: {"produits":["produit1","produit2",...]}. Ignore les totaux, taxes et non-alimentaires. Mets les noms en français, courts et clairs.'}]}]})});
      var data=await resp.json();
      var text=(data.content&&data.content[0]&&data.content[0].text)||'{}';
      var json=JSON.parse(text.replace(/```json|```/g,'').trim());
      var produits=json.produits||[];
      if(!produits.length){document.getElementById('ocr-items-list').innerHTML='<div style="text-align:center;color:var(--muted)">Aucun produit détecté.</div>';return;}
      document.getElementById('ocr-items-list').innerHTML=produits.map(function(p,i){
        return '<div class="ocr-item"><div class="ocr-item-check checked" id="ocr-chk-'+i+'" onclick="toggleOcrItem('+i+',this)">✓</div><span class="ocr-item-name">'+p+'</span></div>';
      }).join('');
    }catch(err){document.getElementById('ocr-items-list').innerHTML='<div style="color:var(--danger);text-align:center">❌ Erreur d\'analyse. Essayez une photo plus nette.</div>';}
  };
  reader.readAsDataURL(file);
}

function toggleOcrItem(i,el){ el.classList.toggle('checked'); el.textContent=el.classList.contains('checked')?'✓':''; }

function addOcrItemsToList(){
  var checks=document.querySelectorAll('[id^="ocr-chk-"]');
  var names=document.querySelectorAll('.ocr-item-name');
  var added=0;
  checks.forEach(function(chk,i){
    if(chk.classList.contains('checked')&&names[i]){
      var nom=names[i].textContent.trim();
      coursesList.push({id:'ocr_'+Date.now()+'_'+i,nom:nom,source:'manual',sourceLabel:'📷 Ticket de caisse',checked:false});
      added++;
    }
  });
  document.getElementById('ocr-result').style.display='none';
  document.getElementById('ticket-file').value='';
  renderCoursesList();
  showToast('✅ '+added+' article'+(added>1?'s':'')+' ajouté'+(added>1?'s':'')+' !');
}

// ══════════════════════════════════════
//  COURSES
// ══════════════════════════════════════
var coursesList=[], activeSources={expire:true,recettes:false};

function toggleSource(src,el){ activeSources[src]=!activeSources[src]; el.classList.toggle('active',activeSources[src]); buildCoursesList(); }

function buildCoursesList(){
  var today=new Date();today.setHours(0,0,0,0);
  var manuals=coursesList.filter(function(c){return c.source==='manual'||c.source==='ocr'||c.source==='ocr_ticket';});
  var autoItems=[];
  if(activeSources.expire) allItems.forEach(function(item){var d=Math.ceil((new Date(item.date_perempt)-today)/86400000);if(d<=3) autoItems.push({id:'exp_'+item.id,nom:item.nom,source:'expire',sourceLabel:d<=0?'🔴 Expiré':'⚡ Expire dans '+d+'j',checked:false});});
  if(activeSources.recettes&&currentRecipes.length){var seen=new Set();currentRecipes.forEach(function(r){(r.ingredients_manquants||[]).forEach(function(ing){var k=ing.toLowerCase();if(!seen.has(k)&&!allItems.some(function(it){return it.nom.toLowerCase().includes(k);})){seen.add(k);autoItems.push({id:'rec_'+k,nom:ing,source:'recipe',sourceLabel:'👨‍🍳 Manquant recette',checked:false});}});}); }
  var merged=autoItems.map(function(a){var ex=coursesList.find(function(c){return c.id===a.id;});return ex?Object.assign({},a,{checked:ex.checked}):a;});
  coursesList=merged.concat(manuals);
  renderCoursesList();
}

function renderCoursesList(){
  var list=document.getElementById('courses-list'),countEl=document.getElementById('courses-count'),ctaEl=document.getElementById('courses-cta'),clearBtn=document.getElementById('btn-clear-checked'),shareWrap=document.getElementById('courses-share-wrap');
  if(!coursesList.length){list.innerHTML='<div class="empty"><div class="empty-icon">✅</div><div class="empty-text">Rien à acheter !</div></div>';countEl.textContent='0 article';ctaEl.style.display='none';clearBtn.style.display='none';shareWrap.style.display='none';return;}
  var checked=coursesList.filter(function(c){return c.checked;}).length;
  countEl.textContent=coursesList.length+' article'+(coursesList.length>1?'s':'');
  clearBtn.style.display=checked>0?'block':'none';
  ctaEl.style.display=checked>0?'block':'none';
  shareWrap.style.display='block';
  list.innerHTML=coursesList.map(function(c,i){
    var tc=c.source==='expire'?'course-tag-expire':c.source==='recipe'?'course-tag-recipe':'course-tag-manual';
    var tl=c.source==='expire'?'⚡ Urgent':c.source==='recipe'?'👨‍🍳 Recette':'✏️ Manuel';
    return '<div class="course-item'+(c.checked?' checked':'')+'" style="animation-delay:'+(i*.04)+'s">'+
      '<div class="course-check'+(c.checked?' checked':'')+'" onclick="toggleCheck('+i+')">'+(c.checked?'✓':'')+'</div>'+
      '<div class="course-info"><div class="course-name">'+c.nom+'</div><div class="course-source">'+(c.sourceLabel||c.source)+'</div></div>'+
      '<span class="course-tag '+tc+'">'+tl+'</span>'+
      '<button class="course-del" onclick="deleteCourseItem('+i+')">✕</button></div>';
  }).join('');
}

function toggleCheck(i){coursesList[i].checked=!coursesList[i].checked;renderCoursesList();}
function deleteCourseItem(i){coursesList.splice(i,1);renderCoursesList();}
function clearChecked(){coursesList=coursesList.filter(function(c){return !c.checked;});renderCoursesList();}

function addManualCourse(){
  var inp=document.getElementById('course-name'),nom=inp.value.trim();
  if(!nom){showToast('⚠️ Saisis un nom d\'article');return;}
  coursesList.push({id:'man_'+Date.now(),nom:nom,source:'manual',sourceLabel:'✏️ Ajout manuel',checked:false});
  inp.value=''; renderCoursesList(); showToast('✅ '+nom+' ajouté !');
}

function addCheckedToStock(){
  var checked=coursesList.filter(function(c){return c.checked;});
  if(!checked.length) return;
  document.getElementById('csm-title').textContent='Ajouter '+checked.length+' article'+(checked.length>1?'s':'')+' au stock';
  var today=new Date().toISOString().split('T')[0];
  document.getElementById('csm-items').innerHTML=checked.map(function(c,i){return '<div class="csm-item"><div class="csm-item-name">📦 '+c.nom+'</div><div class="csm-row"><select class="field csm-cat" style="flex:1"><option>Frigo</option><option>Placard</option><option>Congelo</option><option>Cave</option></select><input type="number" class="field csm-qty" value="1" min="1" style="width:70px;text-align:center"><input type="date" class="field csm-date" value="'+today+'" style="flex:1.2"></div></div>';}).join('');
  document.getElementById('course-stock-modal').classList.add('open');
}
function closeCourseModal(){document.getElementById('course-stock-modal').classList.remove('open');}
document.getElementById('course-stock-modal').addEventListener('click',function(e){if(e.target===this)closeCourseModal();});

async function confirmAddToStock(){
  var checked=coursesList.filter(function(c){return c.checked;});
  var cats=document.querySelectorAll('.csm-cat'),qtys=document.querySelectorAll('.csm-qty'),dates=document.querySelectorAll('.csm-date');
  var btn=document.querySelector('#course-stock-modal .btn-cook'); btn.textContent='⏳ Ajout...'; btn.style.opacity='0.6';
  var ok=0;
  for(var i=0;i<checked.length;i++){
    try{var r=await fetch(URL_BASE,{method:'POST',headers:{"apiKey":API_KEY,"Authorization":"Bearer "+API_KEY,"Content-Type":"application/json","Prefer":"return=minimal"},body:JSON.stringify({nom:checked[i].nom,categorie:(cats[i]&&cats[i].value)||'Placard',date_perempt:(dates[i]&&dates[i].value)||new Date().toISOString().split('T')[0],ajoute_par:getCurrentUserName(),quantite:parseFloat((qtys[i]&&qtys[i].value)||1)})});if(r.ok||r.status===201) ok++;}catch(e){}
  }
  coursesList=coursesList.filter(function(c){return !c.checked;});
  closeCourseModal(); await fetchStock(); renderCoursesList(); showTab('stock');
  showToast('✅ '+ok+' article'+(ok>1?'s':'')+' ajouté'+(ok>1?'s':'')+' au stock !',3000);
}

// ══ SHARE ══
function buildShareText(){
  var date=new Date().toLocaleDateString('fr-FR',{weekday:'long',day:'numeric',month:'long'});
  var unc=coursesList.filter(function(c){return !c.checked;}),chk=coursesList.filter(function(c){return c.checked;});
  var t='🛒 LISTE DE COURSES — Colossus Stock\n📅 '+date+'\n'+'─'.repeat(30)+'\n';
  if(unc.length){t+='\n📋 À acheter ('+unc.length+'):\n';unc.forEach(function(c){t+='  ☐  '+c.nom+'\n';});}
  if(chk.length){t+='\n✅ Déjà acheté ('+chk.length+'):\n';chk.forEach(function(c){t+='  ✓  '+c.nom+'\n';});}
  t+='\n'+'─'.repeat(30)+'\n📱 Généré par Colossus Stock';
  return t;
}
function openShareModal(){if(!coursesList.length){showToast('⚠️ Ta liste est vide !');return;}var t=buildShareText();document.getElementById('share-preview').textContent=t;var n=coursesList.length;document.getElementById('share-count-label').textContent=n+' article'+(n>1?'s':'')+' dans la liste';document.getElementById('share-modal').classList.add('open');}
function closeShareModal(){document.getElementById('share-modal').classList.remove('open');}
document.getElementById('share-modal').addEventListener('click',function(e){if(e.target===this)closeShareModal();});
function shareWhatsApp(){window.open('https://wa.me/?text='+encodeURIComponent(buildShareText()),'_blank');closeShareModal();}
function shareEmail(){window.open('mailto:?subject='+encodeURIComponent('🛒 Ma liste de courses')+'&body='+encodeURIComponent(buildShareText()),'_blank');closeShareModal();}
async function copyToClipboard(){try{await navigator.clipboard.writeText(buildShareText());showToast('✅ Liste copiée !');}catch(e){showToast('✅ Copié !');}closeShareModal();}
async function shareNative(){if(navigator.share){try{await navigator.share({title:'🛒 Ma liste de courses',text:buildShareText()});closeShareModal();}catch(e){}}else await copyToClipboard();}
function downloadTxt(){var blob=new Blob([buildShareText()],{type:'text/plain;charset=utf-8'});var a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='courses-'+new Date().toISOString().split('T')[0]+'.txt';document.body.appendChild(a);a.click();document.body.removeChild(a);showToast('📥 Fichier téléchargé !');closeShareModal();}
function openGoogleDrive(){navigator.clipboard.writeText(buildShareText()).catch(function(){});showToast('📋 Liste copiée ! Colle dans Google Docs 👇',4000);setTimeout(function(){window.open('https://docs.google.com/document/create','_blank');},800);closeShareModal();}

var STORE_URLS={leclerc:'https://www.google.fr/search?q=E.Leclerc+Drive',carrefour:'https://www.google.fr/search?q=Carrefour+Drive',intermarche:'https://www.google.fr/search?q=Intermarche+Drive',auchan:'https://www.google.fr/search?q=Auchan+Drive',lidl:'https://www.google.fr/search?q=Lidl+courses+en+ligne',monoprix:'https://www.google.fr/search?q=Monoprix+livraison'};
function openSupermarketModal(){if(!coursesList.length){showToast('⚠️ Liste vide !');return;}document.getElementById('supermarket-modal').classList.add('open');}
function closeSupermarketModal(){document.getElementById('supermarket-modal').classList.remove('open');}
async function openStoreCart(store){var text=buildShareText();try{await navigator.clipboard.writeText(text);}catch(e){}showToast('📋 Liste copiée ! Colle dans la recherche du site 👇',4000);setTimeout(function(){window.open(STORE_URLS[store]||'https://www.google.fr/search?q='+encodeURIComponent(store+' drive'),'_blank');},500);closeSupermarketModal();}
document.getElementById('supermarket-modal').addEventListener('click',function(e){if(e.target===this)closeSupermarketModal();});

// ══════════════════════════════════════
//  NOTES AVANCÉES
// ══════════════════════════════════════
var noteTargetId=null, itemNotes=JSON.parse(localStorage.getItem('colossus_notes')||'{}');
var activeNoteTags=[];

function openNoteModal(id,evt){
  evt.stopPropagation();
  noteTargetId=id;
  var item=allItems.find(function(it){return it.id===id;});
  document.getElementById('note-modal-title').textContent=item?item.nom:'Article';
  document.getElementById('note-input').value=itemNotes[id]?itemNotes[id].text||itemNotes[id]:'';
  var tags=itemNotes[id]?itemNotes[id].tags||[]:[]; activeNoteTags=tags.slice();
  document.querySelectorAll('.note-tag-btn').forEach(function(b){b.classList.toggle('active',tags.includes(b.getAttribute('data-tag')));});
  var noteImg=document.getElementById('note-photo-preview');
  if(itemNotes[id]&&itemNotes[id].photo){noteImg.src=itemNotes[id].photo;noteImg.style.display='block';}
  else noteImg.style.display='none';
  document.getElementById('note-modal').classList.add('open');
  setTimeout(function(){document.getElementById('note-input').focus();},300);
}
function closeNoteModal(){document.getElementById('note-modal').classList.remove('open');noteTargetId=null;}
document.getElementById('note-modal').addEventListener('click',function(e){if(e.target===this)closeNoteModal();});

function toggleNoteTag(btn,tag){
  btn.classList.toggle('active');
  if(activeNoteTags.includes(tag)) activeNoteTags=activeNoteTags.filter(function(t){return t!==tag;});
  else activeNoteTags.push(tag);
}

function handleNotePhoto(e){
  var file=e.target.files[0]; if(!file) return;
  var r=new FileReader(); r.onload=function(ev){var img=document.getElementById('note-photo-preview');img.src=ev.target.result;img.style.display='block';img.setAttribute('data-photo',ev.target.result);}; r.readAsDataURL(file);
}

function saveNote(){
  if(!noteTargetId) return;
  var text=document.getElementById('note-input').value.trim();
  var photo=document.getElementById('note-photo-preview').getAttribute('data-photo')||null;
  if(text||activeNoteTags.length||photo) itemNotes[noteTargetId]={text:text,tags:activeNoteTags,photo:photo,date:new Date().toISOString()};
  else delete itemNotes[noteTargetId];
  localStorage.setItem('colossus_notes',JSON.stringify(itemNotes));
  closeNoteModal(); showToast(text||activeNoteTags.length?'📝 Note enregistrée !':'🗑️ Note supprimée'); fetchStock();
}

// ══════════════════════════════════════
//  STATS & GRAPHIQUES
// ══════════════════════════════════════
var mealHistory=JSON.parse(localStorage.getItem('colossus_history')||'[]');
var activeDiets=JSON.parse(localStorage.getItem('colossus_diets')||'[]');
var stockHistory=JSON.parse(localStorage.getItem('colossus_stock_history')||'[]');

function updateStockHistory(){
  var today=new Date().toISOString().split('T')[0];
  var last=stockHistory[stockHistory.length-1];
  if(!last||last.date!==today) stockHistory.push({date:today,count:allItems.length});
  if(stockHistory.length>30) stockHistory=stockHistory.slice(-30);
  localStorage.setItem('colossus_stock_history',JSON.stringify(stockHistory));
}

function addToHistory(recipe,servings){
  mealHistory.unshift({nom:recipe.nom,emoji:recipe.emoji,date:new Date().toISOString(),personnes:servings});
  if(mealHistory.length>50) mealHistory=mealHistory.slice(0,50);
  localStorage.setItem('colossus_history',JSON.stringify(mealHistory));
}
function clearHistory(){if(!confirm('Effacer tout l\'historique ?')) return;mealHistory=[];localStorage.setItem('colossus_history','[]');renderStats();showToast('🗑️ Historique effacé');}

function toggleDiet(diet,btn){
  if(activeDiets.includes(diet)) activeDiets=activeDiets.filter(function(d){return d!==diet;});else activeDiets.push(diet);
  btn.classList.toggle('active',activeDiets.includes(diet));
  localStorage.setItem('colossus_diets',JSON.stringify(activeDiets));
  showToast(activeDiets.length?'✅ Filtre '+diet+' actif':'Filtres désactivés');
}
function initDietButtons(){activeDiets.forEach(function(d){var b=document.querySelector('[onclick*="toggleDiet(\''+d+'\'"]');if(b)b.classList.add('active');});}
initDietButtons();

var chartStock=null, chartMeals=null;

function renderStats(){
  var today=new Date();today.setHours(0,0,0,0);
  var total=allItems.length;
  var expired=allItems.filter(function(it){return Math.ceil((new Date(it.date_perempt)-today)/86400000)<0;}).length;
  var urgent=allItems.filter(function(it){var d=Math.ceil((new Date(it.date_perempt)-today)/86400000);return d>=0&&d<=3;}).length;
  var fresh=total-expired-urgent;
  var GRID=[{icon:'📦',num:total,label:'Articles',color:'var(--accent)'},{icon:'✅',num:fresh,label:'Frais',color:'var(--ok)'},{icon:'⚡',num:urgent,label:'Urgents',color:'var(--warn)'},{icon:'🗑️',num:expired,label:'Expirés',color:'var(--danger)'}];
  var grid=document.getElementById('stats-grid');
  if(grid) grid.innerHTML=GRID.map(function(d,i){return '<div class="stats-big-card" style="animation-delay:'+(i*.06)+'s"><div class="stats-big-icon">'+d.icon+'</div><div class="stats-big-num" style="color:'+d.color+'">'+d.num+'</div><div class="stats-big-label">'+d.label+'</div></div>';}).join('');

  // Bar chart — categories
  var CAT_COLORS={'Frigo':'#5b8cff','Placard':'#f59e0b','Congelo':'#34d399','Cave':'#a78bfa'};
  var catCounts={};
  allItems.forEach(function(it){catCounts[it.categorie]=(catCounts[it.categorie]||0)+1;});
  var maxCat=Math.max.apply(null,Object.values(catCounts).concat([1]));
  var catEl=document.getElementById('stats-categories');
  if(catEl) catEl.innerHTML=Object.keys(catCounts).map(function(cat){return '<div class="stats-cat-row"><span class="stats-cat-label">'+cat+'</span><div class="stats-cat-bar-wrap"><div class="stats-cat-bar" style="width:'+(catCounts[cat]/maxCat*100)+'%;background:'+(CAT_COLORS[cat]||'var(--muted)')+'"></div></div><span class="stats-cat-count">'+catCounts[cat]+'</span></div>';}).join('');

  // Chart.js — stock evolution
  var ctx1=document.getElementById('chart-stock');
  if(ctx1&&typeof Chart!=='undefined'){
    if(chartStock) chartStock.destroy();
    var last7=[];
    for(var i=6;i>=0;i--){var d=new Date();d.setDate(d.getDate()-i);var ds=d.toISOString().split('T')[0];var entry=stockHistory.find(function(e){return e.date===ds;});last7.push({date:d.toLocaleDateString('fr-FR',{weekday:'short'}),count:entry?entry.count:null});}
    chartStock=new Chart(ctx1,{type:'line',data:{labels:last7.map(function(e){return e.date;}),datasets:[{label:'Articles',data:last7.map(function(e){return e.count;}),borderColor:'#5b8cff',backgroundColor:'rgba(91,140,255,0.1)',fill:true,tension:0.4,pointBackgroundColor:'#5b8cff',pointRadius:4,borderWidth:2,spanGaps:true}]},options:{responsive:true,plugins:{legend:{display:false}},scales:{x:{grid:{color:'rgba(255,255,255,0.04)'},ticks:{color:'#7b82a0',font:{size:11}}},y:{grid:{color:'rgba(255,255,255,0.04)'},ticks:{color:'#7b82a0',font:{size:11},stepSize:1}}}}});
  }

  // Chart.js — meals this month
  var ctx2=document.getElementById('chart-meals');
  if(ctx2&&typeof Chart!=='undefined'){
    if(chartMeals) chartMeals.destroy();
    var now=new Date(), monthStart=new Date(now.getFullYear(),now.getMonth(),1);
    var daysInMonth=new Date(now.getFullYear(),now.getMonth()+1,0).getDate();
    var weekLabels=[],weekData=[];
    for(var w=0;w<4;w++){weekLabels.push('S.'+(w+1));var wStart=new Date(monthStart);wStart.setDate(1+w*7);var wEnd=new Date(wStart);wEnd.setDate(wStart.getDate()+6);var cnt=mealHistory.filter(function(m){var d=new Date(m.date);return d>=wStart&&d<=wEnd;}).length;weekData.push(cnt);}
    chartMeals=new Chart(ctx2,{type:'bar',data:{labels:weekLabels,datasets:[{label:'Repas',data:weekData,backgroundColor:['rgba(167,139,250,0.7)','rgba(91,140,255,0.7)','rgba(52,211,153,0.7)','rgba(251,191,36,0.7)'],borderRadius:8,borderSkipped:false}]},options:{responsive:true,plugins:{legend:{display:false}},scales:{x:{grid:{color:'rgba(255,255,255,0.04)'},ticks:{color:'#7b82a0'}},y:{grid:{color:'rgba(255,255,255,0.04)'},ticks:{color:'#7b82a0',stepSize:1}}}}});
  }

  // Meal history list
  var histEl=document.getElementById('meal-history');
  if(histEl) histEl.innerHTML=!mealHistory.length?'<div class="empty"><div class="empty-icon">🍽️</div><div class="empty-text">Cuisinez une recette pour voir l\'historique</div></div>':mealHistory.slice(0,10).map(function(h){var d=new Date(h.date);return '<div class="history-item"><span class="history-emoji">'+h.emoji+'</span><div class="history-info"><div class="history-name">'+h.nom+'</div><div class="history-date">'+d.toLocaleDateString('fr-FR',{weekday:'short',day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'})+'</div></div><span class="history-persons">👥 '+h.personnes+'</span></div>';}).join('');

  // Waste
  var wr=total>0?Math.round(expired/total*100):0;
  var wb=document.getElementById('waste-bar'),wl=document.getElementById('waste-label');
  if(wb){wb.style.width=wr+'%';wb.style.background=wr>30?'linear-gradient(90deg,var(--warn),var(--danger))':'linear-gradient(90deg,var(--ok),var(--warn))';}
  if(wl) wl.textContent=wr===0?'🌟 Excellent ! Aucun gaspillage':wr<=15?'👍 '+wr+'% — Bon score !':wr<=30?'⚠️ '+wr+'% — Quelques produits périmés':'🚨 '+wr+'% — Attention au gaspillage !';

  // Temperature
  renderTempZones();
}

// ══════════════════════════════════════
//  TEMPÉRATURE
// ══════════════════════════════════════
var tempData=JSON.parse(localStorage.getItem('colossus_temps')||'[]');
var TEMP_IDEAL={frigo:{min:2,max:5,label:'2°C – 5°C',icon:'❄️',color:'#5b8cff'},congelo:{min:-20,max:-15,label:'-18°C – -15°C',icon:'🧊',color:'#a78bfa'},cave:{min:10,max:16,label:'10°C – 16°C',icon:'🍷',color:'#34d399'},placard:{min:15,max:22,label:'15°C – 22°C',icon:'🫙',color:'#f59e0b'}};

function openTempModal(){document.getElementById('temp-modal').classList.add('open');}
function closeTempModal(){document.getElementById('temp-modal').classList.remove('open');}
document.getElementById('temp-modal').addEventListener('click',function(e){if(e.target===this)closeTempModal();});

function saveTemperature(){
  var zone=document.getElementById('temp-zone-select').value;
  var val=parseFloat(document.getElementById('temp-value').value);
  if(isNaN(val)){showToast('⚠️ Saisis une valeur valide');return;}
  tempData.push({zone:zone,val:val,date:new Date().toISOString()});
  if(tempData.length>100) tempData=tempData.slice(-100);
  localStorage.setItem('colossus_temps',JSON.stringify(tempData));
  var ideal=TEMP_IDEAL[zone];
  if(ideal){
    if(val<ideal.min||val>ideal.max) showToast('⚠️ Température hors norme pour '+zone+' !',4000);
    else showToast('✅ Température enregistrée — '+val+'°C');
  }
  document.getElementById('temp-value').value='';
  closeTempModal(); renderTempZones();
}

function renderTempZones(){
  var zonesEl=document.getElementById('temp-zones');
  var histEl=document.getElementById('temp-history');
  if(!zonesEl) return;
  var latest={};
  tempData.forEach(function(t){if(!latest[t.zone]||new Date(t.date)>new Date(latest[t.zone].date)) latest[t.zone]=t;});
  zonesEl.innerHTML=Object.keys(TEMP_IDEAL).map(function(z){
    var id=TEMP_IDEAL[z],lt=latest[z];
    var val=lt?lt.val+'°C':'—';
    var cls='';
    if(lt){if(lt.val<id.min||lt.val>id.max) cls='danger';else if(lt.val<id.min+1||lt.val>id.max-1) cls='warn';else cls='ok';}
    return '<div class="temp-zone" onclick="openTempModal()"><div class="temp-zone-icon">'+id.icon+'</div><div class="temp-zone-label">'+z.charAt(0).toUpperCase()+z.slice(1)+'</div><div class="temp-zone-val'+(cls?' '+cls:'')+'">'+val+'</div><div class="temp-zone-ideal">Idéal : '+id.label+'</div></div>';
  }).join('');
  if(histEl){
    var recent=tempData.slice(-5).reverse();
    histEl.innerHTML=recent.length?recent.map(function(t){var id=TEMP_IDEAL[t.zone],ok=t.val>=id.min&&t.val<=id.max;return '<div class="temp-entry"><span class="temp-entry-zone">'+id.icon+' '+t.zone+'</span><span style="font-size:11px;color:var(--muted)">'+new Date(t.date).toLocaleDateString('fr-FR',{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'})+'</span><span class="temp-entry-val" style="color:'+(ok?'var(--ok)':'var(--danger)')+'">'+t.val+'°C</span></div>';}).join(''):'<div style="text-align:center;color:var(--muted);font-size:12px;padding:8px">Aucune mesure enregistrée</div>';
  }
}

// ══════════════════════════════════════
//  BUDGET
// ══════════════════════════════════════
var PRIX_INDICATIFS={'oeuf':0.25,'oeufs':0.25,'lait':0.9,'beurre':2.5,'fromage':3,'farine':1.2,'sucre':1,'sel':0.5,'huile':2,'ail':0.8,'oignon':0.6,'tomate':2,'poulet':5,'boeuf':8,'porc':5,'agneau':10,'saumon':8,'thon':2,'crevettes':6,'riz':1.5,'pates':1.5,'pain':1.5,'pomme de terre':1.2,'carotte':0.8,'champignon':2,'courgette':1.5,'lardons':2,'jambon':2.5,'creme':1.5,'yaourt':0.8,'chocolat':2,'default':2};
function estimateRecipePrice(r){var t=0;((r.ingredients_dispo||[]).concat(r.ingredients_manquants||[])).forEach(function(ing){var nom=(ing.nom||ing).toLowerCase(),prix=PRIX_INDICATIFS.default;for(var k in PRIX_INDICATIFS){if(nom.includes(k)){prix=PRIX_INDICATIFS[k];break;}}t+=prix;});return Math.round(t*10)/10;}

async function searchByBudget(){
  var budget=parseFloat(document.getElementById('budget-input').value);
  if(!budget||budget<1){showToast('⚠️ Entre un budget valide');return;}
  var re=document.getElementById('budget-results');
  re.innerHTML='<div style="text-align:center;color:var(--muted);padding:20px">🔍 Recherche...</div>';
  var recipes=currentRecipes;
  if(!recipes.length){showToast('💡 Génère des recettes d\'abord',3000);re.innerHTML='<div class="empty"><div class="empty-icon">👨‍🍳</div><div class="empty-text">Va dans Chef IA et génère des recettes !</div></div>';return;}
  var res=recipes.map(function(r){return Object.assign({},r,{prix:estimateRecipePrice(r)});}).filter(function(r){return r.prix<=budget;}).sort(function(a,b){return a.prix-b.prix;});
  if(!res.length){re.innerHTML='<div class="empty"><div class="empty-icon">💸</div><div class="empty-text">Aucune recette dans ce budget. Essaie avec '+(budget+10)+'€ !</div></div>';return;}
  re.innerHTML=res.map(function(r){return '<div class="budget-result-card"><span style="font-size:24px">'+r.emoji+'</span><div style="flex:1"><div style="font-family:var(--font-display);font-size:14px;font-weight:800;color:var(--text)">'+r.nom+'</div><div style="font-size:11px;color:var(--muted);margin-top:2px">⏱ '+r.temps+' · '+r.difficulte+'</div></div><span class="budget-result-price">≈ '+r.prix+'€</span></div>';}).join('');
}

// ══════════════════════════════════════
//  SCANNER
// ══════════════════════════════════════
var html5Scanner2=null, lastBarcode2=null;

// ══════════════════════════════════════
//  VOIX
// ══════════════════════════════════════
var recognition=null, isListening=false;
function startVoiceInput(){
  if(!('webkitSpeechRecognition' in window)&&!('SpeechRecognition' in window)){showToast('⚠️ Non supporté sur ce navigateur');return;}
  if(isListening){if(recognition)recognition.stop();return;}
  var SR=window.SpeechRecognition||window.webkitSpeechRecognition;
  recognition=new SR();recognition.lang='fr-FR';recognition.continuous=false;recognition.interimResults=false;
  recognition.onstart=function(){isListening=true;document.getElementById('voice-indicator').textContent='🔴';document.getElementById('voice-status-label').textContent='Écoute en cours...';};
  recognition.onresult=function(e){var t=e.results[0][0].transcript;document.getElementById('itemName').value=t;document.getElementById('voice-status-label').textContent='✓ "'+t+'"';document.getElementById('voice-indicator').textContent='●';showToast('🎙️ Détecté : '+t);};
  recognition.onerror=function(){isListening=false;document.getElementById('voice-indicator').textContent='●';document.getElementById('voice-status-label').textContent='Dictez le nom du produit';showToast('⚠️ Impossible de capter la voix');};
  recognition.onend=function(){isListening=false;document.getElementById('voice-indicator').textContent='●';};
  recognition.start();
}

// ══════════════════════════════════════
//  THEME
// ══════════════════════════════════════
var isLight=localStorage.getItem('colossus_theme')==='light';
function applyTheme(){document.body.classList.toggle('light',isLight);document.getElementById('theme-btn').textContent=isLight?'🌙':'☀️';}
function toggleTheme(){isLight=!isLight;localStorage.setItem('colossus_theme',isLight?'light':'dark');applyTheme();}
applyTheme();

// ══════════════════════════════════════
//  NOTIFICATIONS
// ══════════════════════════════════════
var notifEnabled=false;
async function requestNotifPermission(){
  if(!('Notification' in window)){showToast('⚠️ Non supporté');return;}
  if(Notification.permission==='granted'){notifEnabled=true;scheduleExpiryCheck();showToast('✅ Notifications déjà activées !');return;}
  var perm=await Notification.requestPermission();
  if(perm==='granted'){notifEnabled=true;scheduleExpiryCheck();document.getElementById('notif-btn').textContent='🔔';showToast('✅ Notifications activées !');new Notification('Colossus Stock',{body:'Les alertes d\'expiration sont activées !'});}
  else showToast('❌ Permission refusée');
}
function scheduleExpiryCheck(){checkExpiryNotifications();setInterval(checkExpiryNotifications,3600000);}
function checkExpiryNotifications(){
  if(!notifEnabled||Notification.permission!=='granted') return;
  var today=new Date();today.setHours(0,0,0,0);
  var urgent=allItems.filter(function(it){var d=Math.ceil((new Date(it.date_perempt)-today)/86400000);return d>=0&&d<=1;});
  if(urgent.length>0) new Notification('⚡ Colossus Stock — Expirations !',{body:urgent.map(function(it){var d=Math.ceil((new Date(it.date_perempt)-today)/86400000);return '• '+it.nom+' expire '+(d===0?"aujourd'hui":'demain');}).join('\n')});
}
if(Notification.permission==='granted'){notifEnabled=true;scheduleExpiryCheck();document.getElementById('notif-btn').textContent='🔔';}

// ══════════════════════════════════════
//  DATE SHORTCUTS
// ══════════════════════════════════════
function setDateOffset(days,btn){var d=new Date();d.setDate(d.getDate()+days);document.getElementById('itemDate').value=d.toISOString().split('T')[0];document.querySelectorAll('.date-shortcut').forEach(function(b){b.style.background='';b.style.color='';});if(btn){btn.style.background='var(--accent)';btn.style.color='#fff';setTimeout(function(){btn.style.background='';btn.style.color='';},700);}}

// ══════════════════════════════════════
//  PWA
// ══════════════════════════════════════
var deferredInstallPrompt=null;
window.addEventListener('beforeinstallprompt',function(e){e.preventDefault();deferredInstallPrompt=e;setTimeout(showPWABanner,3000);});
function showPWABanner(){if(document.getElementById('pwa-banner')) return;var b=document.createElement('div');b.id='pwa-banner';b.innerHTML='<span class="pwa-icon">🧀</span><div class="pwa-text"><div class="pwa-title">Installer Colossus Stock</div><div class="pwa-sub">Accès rapide depuis l\'écran d\'accueil</div></div><button class="pwa-btn" onclick="installPWA()">Installer</button><button class="pwa-close" onclick="this.parentElement.remove()">✕</button>';document.body.appendChild(b);}
async function installPWA(){var b=document.getElementById('pwa-banner');if(b) b.remove();if(deferredInstallPrompt){deferredInstallPrompt.prompt();var r=await deferredInstallPrompt.userChoice;if(r.outcome==='accepted') showToast('✅ Application installée !');deferredInstallPrompt=null;}else showToast('📱 Sur iOS : appuie sur Partager → "Sur l\'écran d\'accueil"',5000);}
window.addEventListener('appinstalled',function(){showToast('🎉 Colossus Stock installé !');}); 
// ── LIQUID GLASS NAV ──
(function(){
  var nav = document.getElementById('main-nav');
  var pill = document.getElementById('nav-pill');
  var btns = nav.querySelectorAll('.nav-btn');
  var isDragging = false;
  var activeIdx = 0;
  var lastPillX = null;

  function pillToBtn(btn) {
    var navRect = nav.getBoundingClientRect();
    var btnRect = btn.getBoundingClientRect();
    var x = btnRect.left - navRect.left + btnRect.width/2 - 40;
    pill.style.transform = 'translateX(' + x + 'px)';
  }

  // Attendre que le DOM soit rendu
requestAnimationFrame(function() {
  pillToBtn(btns[0]);
});

btns.forEach(function(btn, i) {
  btn.addEventListener('click', function() {
    activeIdx = i;
    pill.style.transition = 'transform 0.25s cubic-bezier(0.34,1.56,0.64,1)';
    pillToBtn(btn);
  });
});

  nav.addEventListener('touchstart', function(e) {
    isDragging = true;
    pill.style.transition = 'none';
    movePill(e.touches[0].clientX);
  }, {passive: true});

  nav.addEventListener('touchmove', function(e) {
    if(!isDragging) return;
    movePill(e.touches[0].clientX);
  }, {passive: true});

  nav.addEventListener('touchend', function(e) {
    isDragging = false;
    pill.style.transition = 'transform 0.25s cubic-bezier(0.34,1.56,0.64,1), width 0.2s ease';
    var x = e.changedTouches[0].clientX;
    var closest = null, minDist = Infinity;
    btns.forEach(function(btn) {
      var r = btn.getBoundingClientRect();
      var center = r.left + r.width/2;
      var dist = Math.abs(center - x);
      if(dist < minDist) { minDist = dist; closest = btn; }
    });
    if(closest) { pillToBtn(closest); closest.click(); }
  }, {passive: true});

function movePill(clientX) {
    var navRect = nav.getBoundingClientRect();
    var x = clientX - navRect.left - 40;
    x = Math.max(0, Math.min(navRect.width - 80, x));
    
    var delta = clientX - (lastPillX || clientX);
    var stretch = Math.min(Math.abs(delta) * 0.3, 20);
    var scaleX = 1 + stretch / 80;
    var scaleY = 1 - stretch / 200;
    
    pill.style.transform = 'translateX(' + x + 'px) scaleX(' + scaleX + ') scaleY(' + scaleY + ')';
    lastPillX = clientX;
  }
})();

// ══════════════════════════════════════
//  INIT

// ══════════════════════════════════════
//  INIT
// ══════════════════════════════════════
// Si malgré tout l'écran tourne, forcer via transform
  function checkOrientation() {
    if(window.innerWidth > window.innerHeight) {
      document.body.style.transform = 'rotate(-90deg)';
      document.body.style.transformOrigin = 'left top';
      document.body.style.width = window.innerHeight + 'px';
      document.body.style.height = window.innerWidth + 'px';
      document.body.style.position = 'absolute';
      document.body.style.top = window.innerWidth + 'px';
      document.body.style.left = '0';
      document.body.style.overflow = 'hidden';
    } else {
      // ON NE TOUCHE PAS À POSITION: FIXED ICI POUR NE PAS CASSER LE CSS
      document.body.style.transform = '';
      document.body.style.width = '';
      document.body.style.height = '';
      document.body.style.top = '';
      document.body.style.left = '';
    }
  }
fetchStock();
renderUsersRow();
renderFavSection();
renderPlanning();
renderTempZones();

document.getElementById('add-modal').addEventListener('click',function(e){if(e.target===this)closeAddModal();});
document.getElementById('budget-modal').addEventListener('click',function(e){if(e.target===this)document.getElementById('budget-modal').classList.remove('open');});

</script>
</body>
</html>
