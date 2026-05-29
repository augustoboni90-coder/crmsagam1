<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SAGAM CRM Next Pro</title>
  <style>
    :root{
      --bg:#f4f7fb;
      --panel:#ffffff;
      --panel-2:#f8fbff;
      --text:#0f172a;
      --muted:#64748b;
      --line:#dbe4ef;
      --primary:#1d4ed8;
      --primary-2:#2563eb;
      --good:#15803d;
      --warn:#b45309;
      --bad:#b91c1c;
      --shadow:0 14px 40px rgba(15,23,42,.12);
      --radius:16px;
      --radius-sm:12px;
      --border:#dbe4ef;
      --shadow-sm:0 8px 24px rgba(15,23,42,.06);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;background:var(--bg);color:var(--text);font:14px/1.45 Inter,ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif}
    button,input,select,textarea{font:inherit}
    .app{display:grid;grid-template-columns:250px 1fr;min-height:100vh}
    .sidebar{background:#fff;color:#0f172a;padding:14px 12px;position:sticky;top:0;height:100vh;overflow:auto;border-right:1px solid #e8edf4;width:250px}
    .brand{display:flex;align-items:center;gap:9px;font-weight:800;font-size:15px;padding:4px 8px 14px;border-bottom:1px solid #e8edf4;margin-bottom:8px;color:#0f172a}
    .brand .mark{width:32px;height:32px;border-radius:10px;background:#1d4ed8;display:grid;place-items:center;color:#fff;font-size:14px;font-weight:900}
    .sub{margin:10px 0 18px;color:#64748b;font-size:12px}
    .nav{display:grid;gap:2px}
    .nav button{border:none;background:transparent;color:#475569;padding:9px 10px;border-radius:10px;text-align:left;cursor:pointer;font-size:13px;font-weight:500;display:flex;align-items:center;gap:7px;transition:background .12s,color .12s}
    .nav button:hover{background:#f1f5f9;color:#0f172a}
    .nav button.active{background:#eff6ff;color:#1d4ed8;font-weight:700}
    .sidecard{margin-top:14px;border:1px solid #e8edf4;background:#f8fafc;padding:11px;border-radius:12px}
    .sidecard .row{display:flex;justify-content:space-between;gap:10px;margin-top:8px;font-size:12px;color:#64748b}
    .main{display:flex;flex-direction:column;min-width:0}
    .topbar{position:sticky;top:0;z-index:5;background:rgba(244,247,251,.88);backdrop-filter:blur(10px);border-bottom:1px solid var(--line)}
    .topinner{display:flex;align-items:center;justify-content:space-between;gap:12px;padding:16px 20px;max-width:1500px;width:100%;margin:0 auto}
    .content{padding:18px 20px 40px;max-width:1500px;width:100%;margin:0 auto}
    .view{display:none}
    .view.active{display:block}
    .grid{display:grid;gap:14px}
    .grid.kpi{grid-template-columns:repeat(auto-fit,minmax(220px,1fr))}
    .grid.two{grid-template-columns:repeat(auto-fit,minmax(400px,1fr))}
    .grid.three{grid-template-columns:repeat(auto-fit,minmax(320px,1fr))}
    .grid.four{grid-template-columns:repeat(auto-fit,minmax(230px,1fr))}
    .card{background:var(--panel);border:1px solid var(--line);border-radius:var(--radius);box-shadow:var(--shadow);padding:16px;min-width:0}
    .card.soft{background:linear-gradient(180deg,#fff,#f8fbff)}
    .card h2,.card h3{margin:0 0 8px}
    .muted{color:var(--muted)}
    .small{font-size:12px}
    .toolbar{display:flex;gap:10px;align-items:center;flex-wrap:wrap;justify-content:space-between}
    .row{display:flex;gap:10px;align-items:center;flex-wrap:wrap}
    .actions{display:flex;gap:8px;flex-wrap:wrap}
    .btn{border:none;border-radius:12px;padding:10px 14px;font-weight:800;cursor:pointer}
    .btn.primary{background:var(--primary);color:#fff}
    .btn.secondary{background:#fff;border:1px solid var(--line);color:var(--text)}
    .btn.good{background:#dcfce7;color:#14532d;border:1px solid #bbf7d0}
    .btn.warn{background:#fef3c7;color:#92400e;border:1px solid #fde68a}
    .btn.bad{background:#fee2e2;color:#991b1b;border:1px solid #fecaca}
    .btn.small{padding:7px 10px;font-size:12px}
    .badge{display:inline-flex;align-items:center;border-radius:999px;padding:4px 10px;font-size:11px;font-weight:800;background:#eff6ff;color:#1d4ed8;border:1px solid #bfdbfe}
    .badge.good{background:#dcfce7;color:#166534;border-color:#bbf7d0}
    .badge.warn{background:#fef3c7;color:#854d0e;border-color:#fde68a}
    .badge.bad{background:#fee2e2;color:#991b1b;border-color:#fecaca}
    .kpi .card .value{font-size:34px;font-weight:900;letter-spacing:-1px;line-height:1}
    .kpi-trend{display:flex;align-items:center;gap:5px;font-size:11px;font-weight:700;margin-top:6px}
    .kpi-trend.up{color:#15803d}.kpi-trend.down{color:#b91c1c}.kpi-trend.neutral{color:#64748b}
    .kpi-sparkline{display:flex;align-items:flex-end;gap:2px;height:26px;margin-top:8px}
    .kpi-sparkline span{flex:1;border-radius:3px 3px 0 0;background:#dbeafe;min-width:4px;transition:height .3s}
    .kpi-sparkline span.hi{background:#1d4ed8}
    .kpi-sparkline.warn span.hi{background:#b45309}
    .kpi-sparkline.danger span.hi{background:#b91c1c}
    .kpi-sparkline.good span.hi{background:#15803d}
    .form-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
    .field label{display:block;font-size:12px;color:var(--muted);margin-bottom:5px;font-weight:700}
    input,select,textarea{width:100%;padding:10px 12px;background:#fff;border:1px solid var(--line);border-radius:12px;outline:none}
    textarea{min-height:90px;resize:vertical}
    input:focus,select:focus,textarea:focus{border-color:#93c5fd;box-shadow:0 0 0 3px rgba(59,130,246,.12)}
    .input-error:focus{border-color:#ef4444 !important;box-shadow:0 0 0 3px rgba(239,68,68,.18) !important}
    .tablewrap{overflow:auto;border:1px solid var(--line);border-radius:14px;background:#fff}
    table{width:100%;border-collapse:separate;border-spacing:0;min-width:900px}
    th,td{padding:9px 12px;border-bottom:1px solid #f0f4f8;vertical-align:middle;text-align:left}
    th{position:sticky;top:0;background:#f8fafc;font-size:11px;color:#64748b;font-weight:700;z-index:1;letter-spacing:.04em;text-transform:uppercase}
    tbody tr:hover td{background:#f8fbff}
    tbody tr:hover .tbl-actions{opacity:1}
    .tbl-main{font-size:13px;font-weight:600;color:#0f172a;line-height:1.3}
    .tbl-sub{font-size:11px;color:#94a3b8;margin-top:1px;line-height:1.3}
    .tbl-avatar{width:30px;height:30px;border-radius:50%;display:inline-flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;background:#dbeafe;color:#1d4ed8}
    .tbl-actions{display:flex;gap:4px;align-items:center;opacity:.3;transition:opacity .15s}
    .tbl-btn{width:28px;height:28px;border-radius:8px;border:1px solid #e8edf4;background:#fff;cursor:pointer;display:inline-flex;align-items:center;justify-content:center;font-size:13px;color:#64748b;transition:background .12s,color .12s;text-decoration:none;padding:0}
    .tbl-btn:hover{background:#eff6ff;color:#1d4ed8;border-color:#bfdbfe}
    .tbl-btn.danger:hover{background:#fee2e2;color:#b91c1c;border-color:#fecaca}
    .tbl-btn.wa:hover{background:#ecfdf5;color:#15803d;border-color:#bbf7d0}
    canvas{width:100%;height:260px;background:#fff;border:1px solid var(--line);border-radius:14px}
    .timeline{border-left:3px solid #cbd5e1;padding-left:14px}
    .timeline .item{margin:0 0 14px}
    .timeline .title{font-weight:900}
    .hr{height:1px;background:var(--line);margin:14px 0}
    .toast{position:fixed;top:16px;right:18px;left:auto;transform:none;padding:0;background:transparent;border-radius:0;box-shadow:none;display:flex;flex-direction:column;gap:8px;z-index:9999;max-width:min(400px,calc(100vw - 36px));pointer-events:none}
    .toast.show{display:flex}
    .toast-card{background:#fff;border:1px solid #e2e8f0;border-radius:16px;box-shadow:0 8px 32px rgba(15,23,42,.14);padding:12px 14px;display:flex;align-items:flex-start;gap:10px;pointer-events:all;animation:toastIn .22s ease}
    .toast-card.good{border-left:4px solid #15803d}
    .toast-card.bad{border-left:4px solid #b91c1c}
    .toast-card.warn{border-left:4px solid #b45309}
    .toast-card.info{border-left:4px solid #1d4ed8}
    .toast-icon{width:28px;height:28px;border-radius:8px;display:grid;place-items:center;flex-shrink:0;font-size:14px}
    .toast-icon.good{background:#dcfce7}.toast-icon.bad{background:#fee2e2}.toast-icon.warn{background:#fef3c7}.toast-icon.info{background:#dbeafe}
    .toast-body{flex:1;min-width:0}
    .toast-title{font-size:13px;font-weight:700;color:#0f172a;line-height:1.3}
    .toast-sub{font-size:11px;color:#64748b;margin-top:2px;line-height:1.4}
    .toast-action{font-size:12px;font-weight:700;margin-top:5px;cursor:pointer;display:inline-flex;align-items:center;gap:3px;text-decoration:none}
    .toast-action.blue{color:#1d4ed8}.toast-action.red{color:#b91c1c}
    .toast-close{font-size:16px;color:#94a3b8;cursor:pointer;flex-shrink:0;line-height:1;padding:0 2px}
    .toast-close:hover{color:#0f172a}
    @keyframes toastIn{from{opacity:0;transform:translateX(20px)}to{opacity:1;transform:none}}
    .mono{font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace}
    .helper{padding:12px;border-radius:14px;background:#eff6ff;border:1px solid #bfdbfe;color:#1e3a8a}
    .hide{display:none !important}
    @media (max-width:980px){
      .app{grid-template-columns:1fr}
      .sidebar{position:static;height:auto}
      .topinner,.content{padding-left:14px;padding-right:14px}
      table{min-width:760px}
    }
    .tablewrap table td{max-width:360px;overflow:hidden;text-overflow:ellipsis}
    /* ===== PAGINAZIONE TABELLE ===== */
    .pagination{display:flex;align-items:center;gap:8px;flex-wrap:wrap;padding:10px 0 2px;justify-content:flex-end}
    .pagination .pg-btn{border:1px solid var(--line);background:#fff;border-radius:10px;padding:6px 12px;font-size:12px;font-weight:800;cursor:pointer;color:var(--text)}
    .pagination .pg-btn:hover{background:#eff6ff;border-color:#93c5fd}
    .pagination .pg-btn.active{background:#1d4ed8;color:#fff;border-color:#1d4ed8}
    .pagination .pg-btn:disabled{opacity:.4;cursor:not-allowed}
    .pagination .pg-info{font-size:12px;color:var(--muted)}

    /* ===== TOPBAR MOBILE MIGLIORATA ===== */
    @media (max-width:980px){
      .top-quick-actions{display:flex;gap:6px;flex-wrap:wrap}
      .top-quick-actions .btn{font-size:11px;padding:7px 9px}
    }
    @media (max-width:640px){
      .top-quick-actions{display:none}
      .top-quick-actions.open{display:flex;flex-direction:column;position:absolute;top:60px;right:14px;background:#fff;border:1px solid var(--line);border-radius:16px;padding:10px;box-shadow:var(--shadow);z-index:10;gap:6px}
      #btnTopQuickToggle{display:inline-flex !important}
      .topinner{flex-wrap:wrap;gap:8px;position:relative}
      .topinner .actions{flex-wrap:wrap;gap:6px}
    }

    /* ===== SIDEBAR MOBILE ===== */
    @media (max-width:980px){
      .sidebar{max-height:none;overflow:visible}
    }

    /* ===== DATA LIMITE RITIRO: avviso se vuoto ===== */
    .field-hint{font-size:11px;color:var(--muted);margin-top:3px}
    .field-hint.warn{color:#b45309}

    /* ===== TABELLA ROW COUNT BADGE ===== */
    .table-meta{display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px;margin-bottom:6px}
    .row-count{font-size:12px;color:var(--muted);font-weight:700}

    .input-error{border-color:#ef4444 !important;box-shadow:0 0 0 3px rgba(239,68,68,.12) !important}
    .data-quality{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:10px;margin-top:12px}
    .data-quality .dq{border:1px solid var(--line);border-radius:14px;background:#fff;padding:10px}
    .data-quality .dq b{display:block;font-size:18px;margin-top:4px}
    @media print{
      .sidebar,.topbar,.btn,.toolbar .actions{display:none !important}
      body{background:#fff}
      .card{box-shadow:none}
      .view{display:none !important}
      .view.active{display:block !important}
    }
  
    .iconbtn{display:inline-flex;align-items:center;justify-content:center;width:32px;height:32px;border-radius:999px;border:1px solid var(--border);background:#fff;text-decoration:none;font-size:16px;line-height:1;box-shadow:var(--shadow-sm);vertical-align:middle}
    .iconbtn:hover{transform:translateY(-1px)}
    .iconbtn.wa{background:#ecfdf5;border-color:#bbf7d0}
    .iconbtn.mail{background:#eff6ff;border-color:#bfdbfe}
    .actionicons{display:inline-flex;gap:6px;align-items:center;flex-wrap:wrap}


    .sales-hero{background:linear-gradient(135deg,#0f172a 0%,#1d4ed8 55%,#60a5fa 100%);color:#fff;border:none}
    .sales-hero .muted,.sales-hero .small{color:#dbeafe}
    .sales-hero .hero-grid{display:grid;grid-template-columns:1.2fr .8fr;gap:16px;align-items:center}
    .sales-hero .hero-title{font-size:30px;font-weight:900;letter-spacing:-1px;line-height:1.05;margin:0 0 8px}
    .sales-hero .hero-copy{max-width:720px}
    .sales-hero .hero-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
    .hero-stat{background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.18);border-radius:16px;padding:12px}
    .hero-stat .label{font-size:11px;color:#dbeafe;font-weight:800;text-transform:uppercase;letter-spacing:.04em}
    .hero-stat .num{font-size:26px;font-weight:900;line-height:1;margin-top:6px}
    .quick-shell{display:grid;gap:14px}
    .quick-cf-row{display:grid;grid-template-columns:minmax(260px,420px) auto;gap:10px;align-items:end}
    .quick-status{padding:14px 16px;border-radius:16px;background:#eef6ff;border:1px solid #bfdbfe;color:#1e3a8a}
    .quick-status.good{background:#ecfdf5;border-color:#bbf7d0;color:#166534}
    .quick-status.warn{background:#fff7ed;border-color:#fdba74;color:#9a3412}
    .sales-steps{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
    .sales-step{border:1px solid var(--line);border-radius:18px;background:#fff;padding:14px;box-shadow:var(--shadow)}
    .sales-step .step-n{width:34px;height:34px;border-radius:999px;background:#dbeafe;color:#1d4ed8;display:grid;place-items:center;font-weight:900;margin-bottom:10px}
    .sales-step h4{margin:0 0 4px;font-size:16px}
    .choice-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
    .choice-card{border:1px solid var(--line);border-radius:18px;background:linear-gradient(180deg,#fff,#f8fbff);padding:14px;box-shadow:var(--shadow);display:flex;flex-direction:column;gap:8px}
    .choice-card .icon{font-size:22px}
    .choice-card .title{font-weight:900;font-size:16px}
    .choice-card .desc{color:var(--muted);font-size:12px;min-height:32px}
    .choice-card .btn{margin-top:auto}
    .client-summary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:10px}
    .summary-pill{padding:10px 12px;border-radius:14px;background:#f8fafc;border:1px solid var(--line)}
    .summary-pill .k{font-size:11px;color:var(--muted);font-weight:800;text-transform:uppercase}
    .summary-pill .v{font-size:14px;font-weight:800;margin-top:4px;word-break:break-word}
    .news-frame{width:100%;height:78vh;min-height:720px;border:1px solid var(--line);border-radius:18px;background:#fff}
    @media (max-width:980px){
      .sales-hero .hero-grid,.sales-steps,.choice-grid,.client-summary-grid,.quick-cf-row{grid-template-columns:1fr}
      .sales-hero .hero-stats{grid-template-columns:1fr 1fr 1fr}
      .news-frame{height:65vh;min-height:560px}
    }


    .module-hero{background:linear-gradient(180deg,#ffffff,#f8fbff);border:1px solid #dbeafe}
    .module-hero .lead{color:var(--muted);font-size:13px}
    .module-actions{display:flex;gap:10px;flex-wrap:wrap}
    .module-statbar{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:12px}
    .module-stat{padding:12px;border-radius:16px;background:#fff;border:1px solid var(--line)}
    .module-stat .k{font-size:11px;color:var(--muted);font-weight:800;text-transform:uppercase}
    .module-stat .v{font-size:18px;font-weight:900;margin-top:4px}
    .form-shell{display:grid;gap:14px}
    .form-shell .card{box-shadow:0 10px 26px rgba(15,23,42,.08)}
    .section-label{display:inline-flex;align-items:center;gap:8px;padding:6px 10px;border-radius:999px;background:#eff6ff;border:1px solid #bfdbfe;color:#1d4ed8;font-size:11px;font-weight:900;letter-spacing:.04em;text-transform:uppercase}
    @media (max-width:980px){ .module-statbar{grid-template-columns:1fr} }


    .timeline-card{background:#fff;border:1px solid var(--line);border-radius:16px;padding:14px;margin-bottom:12px;box-shadow:0 8px 22px rgba(15,23,42,.06)}
    .timeline-head{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
    .timeline-meta{display:flex;gap:8px;flex-wrap:wrap;align-items:center}



    .postit-shell{display:grid;grid-template-columns:340px 1fr;gap:14px}
    .postit-board{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px;align-items:start}
    .postit-note{position:relative;padding:14px 14px 12px;border-radius:18px;min-height:180px;box-shadow:0 14px 30px rgba(15,23,42,.14);border:1px solid rgba(15,23,42,.08);display:flex;flex-direction:column;gap:10px;transform:rotate(-1deg)}
    .postit-note:nth-child(even){transform:rotate(1deg)}
    .postit-note.yellow{background:#fef9c3;border-color:#fde68a}
    .postit-note.blue{background:#dbeafe;border-color:#93c5fd}
    .postit-note.green{background:#dcfce7;border-color:#86efac}
    .postit-note.pink{background:#fce7f3;border-color:#f9a8d4}
    .postit-note.orange{background:#ffedd5;border-color:#fdba74}
    .postit-note.hidden-dashboard{opacity:.72;filter:grayscale(.15)}
    .postit-top{display:flex;justify-content:space-between;gap:10px;align-items:flex-start}
    .postit-title{font-weight:900;font-size:15px;line-height:1.2}
    .postit-body{white-space:pre-wrap;line-height:1.45;font-size:13px;min-height:72px}
    .postit-meta{margin-top:auto;font-size:11px;color:#475569;display:grid;gap:4px}
    .postit-empty{padding:18px;border-radius:16px;border:1px dashed var(--line);background:#f8fafc;color:var(--muted)}
    .postit-launcher{display:flex;align-items:center;gap:10px}
    .postit-mascot{width:42px;height:42px;border-radius:14px;display:grid;place-items:center;background:linear-gradient(135deg,#fef08a,#f9a8d4);box-shadow:0 10px 24px rgba(15,23,42,.16);font-size:22px;animation:postitWiggle 2.2s ease-in-out infinite;transform-origin:bottom center}
    .postit-launcher h3{margin:0}
    .postit-dash-card{background:linear-gradient(180deg,#fffdf7,#fff7ed);border:1px solid #fde68a}
    .postit-dash-card .helper{background:#fff7ed;border-color:#fdba74;color:#9a3412}
    @keyframes postitWiggle{0%,100%{transform:rotate(0deg) translateY(0)}20%{transform:rotate(-8deg) translateY(-2px)}40%{transform:rotate(6deg) translateY(0)}60%{transform:rotate(-4deg) translateY(-1px)}80%{transform:rotate(3deg) translateY(0)}}
    @media (max-width:980px){.postit-shell{grid-template-columns:1fr}}


    .login-locked .app{filter:blur(6px);pointer-events:none;user-select:none}
    .login-locked .topbar,.login-locked .sidebar{pointer-events:none}
    .auth-screen{position:fixed;inset:0;z-index:1000;display:none;align-items:center;justify-content:center;padding:24px;background:radial-gradient(circle at top left,rgba(37,99,235,.35),transparent 32%),linear-gradient(135deg,#0f172a,#1e3a8a 55%,#60a5fa);}
    .auth-screen.show{display:flex}
    .auth-card{width:min(460px,100%);background:rgba(255,255,255,.96);border:1px solid rgba(255,255,255,.65);border-radius:28px;box-shadow:0 30px 90px rgba(15,23,42,.34);padding:24px;backdrop-filter:blur(16px)}
    .auth-logo{width:58px;height:58px;border-radius:22px;display:grid;place-items:center;background:linear-gradient(135deg,#1d4ed8,#60a5fa);color:#fff;font-weight:900;font-size:24px;box-shadow:0 14px 32px rgba(37,99,235,.32)}
    .auth-title{font-size:28px;line-height:1.05;font-weight:950;letter-spacing:-1px;margin:14px 0 6px;color:#0f172a}
    .auth-copy{color:#64748b;font-size:13px;margin-bottom:16px}
    .auth-status{margin-top:12px;padding:11px 12px;border-radius:14px;background:#eff6ff;border:1px solid #bfdbfe;color:#1e3a8a;font-size:12px;font-weight:800}
    .auth-status.bad{background:#fee2e2;border-color:#fecaca;color:#991b1b}
    .auth-status.good{background:#dcfce7;border-color:#bbf7d0;color:#166534}
    .auth-card .field{margin-top:10px}
    .auth-card .btn{width:100%;margin-top:14px}
    .auth-foot{display:flex;justify-content:space-between;gap:10px;margin-top:14px;color:#64748b;font-size:11px;flex-wrap:wrap}
    .session-pill{display:inline-flex;align-items:center;gap:6px;border:1px solid var(--line);background:#fff;border-radius:999px;padding:7px 10px;font-size:12px;font-weight:800;color:#334155}


/* === SAGAM CRM - MODULI SMART CLIENTE/CONTATTI/RICHIAMI/DOCUMENTI === */
.smart-shell{display:grid;gap:14px}
.smart-hero{background:linear-gradient(135deg,#0f172a,#1d4ed8 58%,#60a5fa);color:#fff;border:none}
.smart-hero .muted,.smart-hero .small{color:#dbeafe}
.smart-tabs{display:flex;gap:8px;flex-wrap:wrap;margin:12px 0}
.smart-tab{border:1px solid var(--line);background:#fff;border-radius:999px;padding:8px 12px;font-weight:900;cursor:pointer}
.smart-tab.active{background:#dbeafe;color:#1d4ed8;border-color:#93c5fd}
.smart-panel{display:none}
.smart-panel.active{display:block}
.smart-mini-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
.smart-stat{background:#fff;border:1px solid var(--line);border-radius:16px;padding:12px}
.smart-stat .k{font-size:11px;color:var(--muted);font-weight:900;text-transform:uppercase}
.smart-stat .v{font-size:20px;font-weight:900;margin-top:4px}
.smart-note{padding:12px 14px;border-radius:16px;background:#eff6ff;border:1px solid #bfdbfe;color:#1e3a8a}
.smart-warn{padding:12px 14px;border-radius:16px;background:#fff7ed;border:1px solid #fdba74;color:#9a3412}
.client-head{display:grid;grid-template-columns:1.2fr .8fr;gap:14px;align-items:start}
.client-avatar{width:58px;height:58px;border-radius:20px;background:linear-gradient(135deg,#dbeafe,#bfdbfe);display:grid;place-items:center;color:#1d4ed8;font-weight:900;font-size:22px}
.client-title{display:flex;gap:12px;align-items:center}
.client-name{font-size:24px;font-weight:900;line-height:1.05}
.client-meta{display:flex;gap:8px;flex-wrap:wrap;margin-top:8px}
.status-pill{display:inline-flex;border-radius:999px;padding:4px 10px;font-size:11px;font-weight:900;border:1px solid var(--line);background:#f8fafc;color:#475569}
.status-pill.good{background:#dcfce7;color:#166534;border-color:#bbf7d0}
.status-pill.warn{background:#fef3c7;color:#854d0e;border-color:#fde68a}
.status-pill.bad{background:#fee2e2;color:#991b1b;border-color:#fecaca}
.doc-preview{background:#fff;border:1px solid var(--line);border-radius:16px;padding:18px;min-height:280px;white-space:pre-wrap;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:12px}
@media(max-width:980px){.client-head{grid-template-columns:1fr}}
@media print{.smart-no-print{display:none!important}.doc-preview{border:none}}


    .nav-grouped{display:flex;flex-direction:column;gap:10px}
    .nav-section-label{
      font-size:10px;
      font-weight:700;
      letter-spacing:.07em;
      color:#94a3b8;
      padding:10px 10px 3px;
      text-transform:uppercase;
    }
    .nav-section{
      display:flex;
      flex-direction:column;
      gap:2px;
      padding:0 0 6px;
      border-bottom:1px solid #f0f4f8;
    }
    .nav-section:last-child{border-bottom:none;padding-bottom:0}
    .nav-grouped button{
      text-align:left;
    }
    

    .nav-accordion .nav-acc-head{
      cursor:pointer;
      user-select:none;
      border-radius:10px;
      transition:.18s;
      display:flex;
      align-items:center;
      justify-content:space-between;
    }
    .nav-accordion .nav-acc-head:hover{background:#f1f5f9;color:#1d4ed8}
    .nav-acc-body.collapsed{display:none}
    .nav-count{
      float:right;
      min-width:18px;
      height:18px;
      padding:1px 5px;
      border-radius:999px;
      background:#dbeafe;
      color:#1d4ed8;
      font-size:10px;
      font-weight:700;
      display:inline-flex;
      align-items:center;
      justify-content:center;
      margin-left:auto;
    }
    .nav-count.hot{background:#fee2e2;color:#991b1b}
    .nav-count.ok{background:#dcfce7;color:#166534}
    .top-quick-actions{
      display:flex;
      gap:8px;
      flex-wrap:wrap;
      align-items:center;
      padding:8px 10px;
      border:1px solid var(--line);
      border-radius:16px;
      background:#fff;
      box-shadow:var(--shadow-sm,0 8px 24px rgba(15,23,42,.06));
    }
    .mode-toggle{
      display:inline-flex;
      align-items:center;
      gap:6px;
      padding:8px 10px;
      border-radius:999px;
      border:1px solid var(--line);
      background:#f8fafc;
      font-size:12px;
      font-weight:800;
      cursor:pointer;
      user-select:none;
    }
    .mode-toggle input{width:auto}
    body.simple-mode [data-advanced="true"]{display:none!important}
    body.simple-mode .nav-section:empty{display:none!important}
    /* Riparazioni sempre visibile - non nascondere mai */
    [data-view="riparazioni"]{display:flex!important}
    [data-group-body="laboratorio"]{display:block!important}
    .nav-section-label[data-group="laboratorio"]{display:block!important}
    .ux-mini-note{
      font-size:11px;
      color:var(--muted);
      margin-top:6px;
      padding:0 10px;
    }


    .sync-gate{
      position:fixed;
      inset:0;
      z-index:9998;
      background:linear-gradient(135deg,#0f172a,#1d4ed8 60%,#38bdf8);
      color:#fff;
      display:none;
      align-items:center;
      justify-content:center;
      padding:24px;
    }
    .sync-gate.show{display:flex}
    .sync-card{
      width:min(720px,94vw);
      background:rgba(255,255,255,.96);
      color:#0f172a;
      border-radius:28px;
      box-shadow:0 26px 90px rgba(15,23,42,.35);
      padding:28px;
      border:1px solid rgba(255,255,255,.45);
    }
    .sync-title{font-size:28px;font-weight:950;margin:0 0 8px}
    .sync-sub{color:#475569;margin-bottom:18px}
    .sync-spinner{
      width:42px;height:42px;border-radius:999px;
      border:5px solid #dbeafe;border-top-color:#1d4ed8;
      animation:spin .9s linear infinite;
      margin-right:14px;
    }
    @keyframes spin{to{transform:rotate(360deg)}}
    .sync-row{display:flex;align-items:center;margin:16px 0}
    .sync-log{
      background:#f8fafc;
      border:1px solid #dbe4ef;
      border-radius:16px;
      padding:12px;
      max-height:180px;
      overflow:auto;
      font-size:12px;
      color:#334155;
      white-space:pre-wrap;
    }
    .sync-actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:16px}
    .backup-alert{
      border:1px solid #bfdbfe;
      background:#eff6ff;
      color:#1e3a8a;
      border-radius:16px;
      padding:12px 14px;
      margin-top:12px;
      display:flex;
      gap:10px;
      align-items:center;
      justify-content:space-between;
      flex-wrap:wrap;
    }
    .change-log-list{
      display:flex;
      flex-direction:column;
      gap:8px;
      max-height:520px;
      overflow:auto;
    }
    .change-log-item{
      border:1px solid var(--line);
      background:#fff;
      border-radius:14px;
      padding:10px 12px;
      display:grid;
      grid-template-columns:160px 130px 1fr;
      gap:10px;
      align-items:start;
    }
    .change-log-item .when{font-weight:900;color:#0f172a}
    .change-log-item .area{font-weight:900;color:#1d4ed8}
    .change-log-item .detail{color:#334155}
    @media(max-width:900px){.change-log-item{grid-template-columns:1fr}.sync-card{padding:20px}}


    .gs-import-panel{
      border-color:#bfdbfe;
      background:linear-gradient(180deg,#ffffff,#f8fbff);
    }


    .dashboard-data-ticker{
      overflow:hidden;
      border:1px solid #bfdbfe;
      background:linear-gradient(90deg,#eff6ff,#ffffff,#f8fafc);
      color:#1e3a8a;
      border-radius:18px;
      padding:12px 0;
      margin-top:14px;
      box-shadow:0 10px 28px rgba(15,23,42,.06);
      position:relative;
    }
    .dashboard-data-ticker:before,
    .dashboard-data-ticker:after{
      content:"";
      position:absolute;
      top:0;
      width:60px;
      height:100%;
      z-index:2;
      pointer-events:none;
    }
    .dashboard-data-ticker:before{
      left:0;
      background:linear-gradient(90deg,#eff6ff,rgba(239,246,255,0));
    }
    .dashboard-data-ticker:after{
      right:0;
      background:linear-gradient(270deg,#f8fafc,rgba(248,250,252,0));
    }
    .ticker-track{
      display:inline-flex;
      gap:42px;
      white-space:nowrap;
      padding-left:100%;
      animation:sagamTicker 85s linear infinite;
      font-size:13px;
      font-weight:800;
      align-items:center;
    }
    .ticker-track span{
      display:inline-flex;
      align-items:center;
    }
    .dashboard-data-ticker:hover .ticker-track{
      animation-play-state:paused;
    }
    @keyframes sagamTicker{
      from{transform:translateX(0)}
      to{transform:translateX(-100%)}
    }


    /* ===== RICERCA GLOBALE CTRL+K ===== */
    #globalSearchBar{display:flex;align-items:center;gap:8px;background:#f8fafc;border:1px solid #e2e8f0;border-radius:12px;padding:8px 12px;cursor:pointer;min-width:200px;transition:border-color .15s}
    #globalSearchBar:hover{border-color:#93c5fd;background:#fff}
    #globalSearchBar span{font-size:13px;color:#94a3b8;flex:1}
    #globalSearchBar kbd{font-size:10px;padding:2px 6px;border-radius:5px;border:1px solid #e2e8f0;background:#fff;color:#64748b;font-family:ui-monospace,monospace}
    .gsearch-overlay{position:fixed;inset:0;background:rgba(15,23,42,.45);z-index:5000;display:none;align-items:flex-start;justify-content:center;padding-top:80px}
    .gsearch-overlay.open{display:flex !important}
    .gsearch-box{background:#fff;border-radius:20px;box-shadow:0 24px 80px rgba(15,23,42,.22);width:min(640px,calc(100vw - 32px));overflow:hidden}
    .gsearch-input-row{display:flex;align-items:center;gap:10px;padding:14px 18px;border-bottom:1px solid #f0f4f8}
    .gsearch-input-row .gsearch-icon{font-size:18px;color:#94a3b8;flex-shrink:0}
    #gsearchInput{border:none;background:transparent;font-size:16px;flex:1;outline:none;color:#0f172a;font-family:inherit}
    #gsearchInput::placeholder{color:#94a3b8}
    .gsearch-results{max-height:420px;overflow:auto}
    .gsr-item{display:flex;align-items:center;gap:10px;padding:11px 16px;cursor:pointer;border-bottom:1px solid #f8fafc;transition:background .1s}
    .gsr-item:hover,.gsr-item.selected{background:#f0f7ff}
    .gsr-item:last-child{border-bottom:none}
    .gsr-avatar{width:32px;height:32px;border-radius:10px;display:grid;place-items:center;font-size:12px;font-weight:700;flex-shrink:0}
    .gsr-avatar.client{background:#dbeafe;color:#1d4ed8}
    .gsr-avatar.contratto{background:#dcfce7;color:#15803d}
    .gsr-avatar.device{background:#fef3c7;color:#92400e}
    .gsr-avatar.riparazione{background:#fee2e2;color:#b91c1c}
    .gsr-main{font-size:13px;font-weight:600;color:#0f172a;line-height:1.3}
    .gsr-sub{font-size:11px;color:#94a3b8;margin-top:1px}
    .gsr-type{font-size:10px;padding:2px 8px;border-radius:999px;font-weight:700;margin-left:auto;flex-shrink:0}
    .gsr-type.client{background:#dbeafe;color:#1d4ed8}
    .gsr-type.contratto{background:#dcfce7;color:#15803d}
    .gsr-type.device{background:#fef3c7;color:#92400e}
    .gsr-type.riparazione{background:#fee2e2;color:#b91c1c}
    .gsr-empty{padding:24px 18px;text-align:center;color:#94a3b8;font-size:13px}
    .gsr-hint{padding:10px 16px;font-size:11px;color:#94a3b8;border-top:1px solid #f0f4f8;display:flex;gap:12px}
    .gsr-hint kbd{padding:1px 5px;border-radius:4px;border:1px solid #e2e8f0;background:#f8fafc;font-family:monospace;font-size:10px}

    /* ===== SIDE PANEL / DRAWER ===== */
    #clientDrawer{border-left:1px solid #e8edf4}
    .drawer-tab-bar{display:flex;gap:4px;padding:0 0 10px;border-bottom:1px solid #e8edf4;margin-bottom:12px;flex-wrap:wrap}
    .drawer-tab{padding:6px 12px;border-radius:8px;font-size:12px;font-weight:600;cursor:pointer;border:1px solid transparent;color:#64748b;background:transparent}
    .drawer-tab:hover{background:#f1f5f9}
    .drawer-tab.active{background:#eff6ff;color:#1d4ed8;border-color:#bfdbfe}


/* =============================================
   RESPONSIVE — SAGAM CRM v6
   Breakpoints: 768px (tablet), 480px (phone)
   ============================================= */

/* --- Hamburger button (hidden on desktop) --- */
#menuToggle{
  display:none;
  border:none;
  background:none;
  cursor:pointer;
  padding:6px 8px;
  border-radius:8px;
  font-size:22px;
  line-height:1;
  flex-shrink:0;
  color:#1d4ed8;
}
#menuToggle:hover{background:#eff6ff}

/* --- Sidebar overlay backdrop --- */
.sidebar-backdrop{
  display:none;
  position:fixed;
  inset:0;
  background:rgba(15,23,42,.45);
  z-index:99;
}
.sidebar-backdrop.open{display:block}

/* ========================
   TABLET  (max 900px)
   ======================== */
@media(max-width:900px){
  /* Layout: sidebar nascosta, main piena larghezza */
  .app{grid-template-columns:1fr !important}

  .sidebar{
    position:fixed !important;
    top:0;left:0;
    height:100vh;
    width:260px;
    z-index:100;
    transform:translateX(-100%);
    transition:transform .25s cubic-bezier(.4,0,.2,1);
    box-shadow:none;
  }
  .sidebar.open{
    transform:translateX(0) !important;
    box-shadow:4px 0 24px rgba(0,0,0,.18);
  }

  /* Hamburger visibile */
  #menuToggle{display:flex !important}

  /* Topbar più compatta */
  .topinner{padding:10px 14px !important;gap:8px !important;flex-wrap:wrap}
  #pageTitle{font-size:16px !important}
  #pageSubtitle{display:none}

  /* Barra di ricerca */
  #globalSearchBar{flex:1 !important;min-width:0;font-size:12px}
  #globalSearchBar kbd{display:none}

  /* Nascondi azioni rapide nel topbar, mostra solo bottone compatto */
  .top-quick-actions{display:none !important}
  #btnTopQuickToggle{display:flex !important}

  /* Grids a colonna singola */
  .grid.kpi{grid-template-columns:repeat(2,1fr) !important}
  .grid.two,.grid.three,.grid.four{grid-template-columns:1fr !important}

  /* Tabelle scrollabili */
  .tablewrap{overflow-x:auto}
  table{min-width:520px}

  /* Content padding ridotto */
  .content{padding:12px 14px 32px !important}

  /* Toolbar wraap */
  .toolbar{flex-wrap:wrap;gap:8px}
  .toolbar .actions{flex-wrap:wrap;gap:6px}

  /* Form grid tablet: 2 colonne */
  .form-grid{grid-template-columns:repeat(2,1fr) !important}

  /* Drawer più largo */
  .client-drawer{width:min(520px,95vw) !important}

  /* Dashboard ticker */
  .dashboard-data-ticker{font-size:12px}

  /* Postit grid */
  .postit-shell{grid-template-columns:repeat(2,1fr) !important}

  /* Campagna libera form */
  #smartCampPanel-libera .form-grid{grid-template-columns:1fr 1fr !important}
}

/* ========================
   PHONE (max 480px)
   ======================== */
@media(max-width:480px){
  .sidebar{width:100vw}

  .topinner{padding:8px 10px !important;gap:6px}
  #pageTitle{font-size:15px !important}

  /* Nascondi elementi non essenziali nel topbar */
  #btnLogout{display:none}
  .session-pill{display:none}

  /* 1 colonna ovunque */
  .grid.kpi,.grid.two,.grid.three,.grid.four{grid-template-columns:1fr !important}

  /* Form in colonna singola */
  .form-grid{grid-template-columns:1fr !important}

  /* Pulsanti più grandi per tocco */
  .btn{padding:9px 14px;font-size:13px}
  .btn.small{padding:7px 11px;font-size:12px}
  .nav button{padding:11px 10px;font-size:13px}

  /* Tabelle scrollabili */
  table{min-width:440px;font-size:12px}
  th,td{padding:7px 9px}

  /* Content padding minimo */
  .content{padding:10px 10px 28px !important}

  /* Drawer full screen */
  .client-drawer{width:100vw !important;border-radius:0 !important}

  /* Scheda cliente: layout verticale */
  .client-head{grid-template-columns:1fr !important}

  /* Postit griglia singola */
  .postit-shell{grid-template-columns:1fr !important}

  /* KPI cards: orizzontali compatti */
  .card.kpi-card{display:flex;align-items:center;gap:14px;padding:12px}
  .card.kpi-card .kpi-number{font-size:28px;flex-shrink:0}

  /* Search overlay */
  #gsearch-overlay .gsearch-box{width:100vw;border-radius:0 !important}

  /* Modal full screen */
  .modal-box{width:100vw !important;max-width:100vw;border-radius:12px 12px 0 0 !important;position:fixed;bottom:0;top:auto !important;transform:none !important}

  /* Campagna libera */
  #smartCampPanel-libera .form-grid{grid-template-columns:1fr !important}
  #smartCampPanel-libera .actions{flex-direction:column;gap:6px}
  #smartCampPanel-libera .actions button{width:100%}

  /* Rimuovi sparkline su mobile (troppo stretto) */
  .sparkline-wrap{display:none}

  /* Toolbar verticale */
  .toolbar{flex-direction:column;align-items:flex-start}
  .toolbar .actions{width:100%;justify-content:flex-start}

  /* Riduci padding card */
  .card{padding:12px}
}

/* ========================
   PRINT — ricevuta pulita
   ======================== */
@media print{
  .sidebar,.topbar,.btn,.toolbar .actions,
  #menuToggle,.sidebar-backdrop,
  .smart-no-print,.no-print-btn,
  .tab-controls,.client-head .actions{
    display:none !important
  }
  .app{display:block !important}
  .main{margin:0 !important}
  .content{padding:0 !important}
  body{background:#fff !important}
}


/* ===== SCANNER DOCUMENTI DA QR ===== */
.scanner-hero{background:linear-gradient(135deg,#0f172a,#1d4ed8 58%,#60a5fa);color:#fff;border:none}
.scanner-hero .muted,.scanner-hero .small{color:#dbeafe}
.scanner-grid{display:grid;grid-template-columns:minmax(280px,420px) 1fr;gap:14px;align-items:start}
.scanner-qr-box{display:grid;gap:10px;place-items:center;text-align:center;background:#fff;border:1px solid var(--line);border-radius:18px;padding:16px}
.scanner-qr-box img{width:240px;height:240px;border:1px solid #e2e8f0;border-radius:14px;background:#fff;padding:8px}
.scanner-video-wrap{position:relative;background:#000;border-radius:18px;overflow:hidden;min-height:280px;border:1px solid #0f172a}
.scanner-video-wrap video,.scanner-video-wrap canvas{width:100%;max-height:420px;display:block;background:#000}
.scanner-frame{position:absolute;inset:14%;border:3px solid rgba(255,255,255,.85);border-radius:16px;box-shadow:0 0 0 999px rgba(0,0,0,.35);pointer-events:none}
.scanner-result{white-space:pre-wrap;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:12px;background:#f8fafc;border:1px solid var(--line);border-radius:14px;padding:12px;min-height:150px;max-height:360px;overflow:auto}
.scanner-pill{display:inline-flex;align-items:center;gap:6px;border-radius:999px;padding:5px 10px;background:#eff6ff;border:1px solid #bfdbfe;color:#1d4ed8;font-size:11px;font-weight:900}
@media(max-width:980px){.scanner-grid{grid-template-columns:1fr}.scanner-qr-box img{width:220px;height:220px}}

</style>
<script>

/* Sync: niente patch globale di fetch. La scelta list/pullAll è gestita esplicitamente da gsPullAll(). */

</script>
</head>
<body>


<input id="fileJsonBackupGlobal" type="file" accept=".json,application/json" style="display:none" />

<div id="syncGate" class="sync-gate">
  <div class="sync-card">
    <div class="sync-row">
      <div class="sync-spinner"></div>
      <div>
        <div class="sync-title">Sincronizzazione dati</div>
        <div class="sync-sub">Sto caricando i dati salvati prima di aprire il CRM, così l'utente non vede schermate vuote o dati incompleti.</div>
      </div>
    </div>
    <div class="sync-log" id="syncGateLog">Accesso confermato. Preparazione sincronizzazione...</div>
    <div class="sync-actions">
      <button class="btn primary" id="btnSyncGateRetry">Riprova sincronizzazione</button>
      <button class="btn secondary" id="btnSyncGateOffline">Lavora offline con ultimi dati locali</button>
    </div>
  </div>
</div>

<div class="sidebar-backdrop" id="sidebarBackdrop"></div>
<div class="app">
  <aside class="sidebar">
    <div class="brand"><div class="mark">V</div><div>SAGAM CRM <span class="badge">NEXT</span></div></div>
    
    

<div class="nav nav-grouped nav-accordion">
      <div class="nav-section-label nav-acc-head" data-group="panoramica">▾ PANORAMICA</div>
      <div class="nav-section nav-acc-body" data-group-body="panoramica">
        <button class="active" data-view="dashboard">📊 Dashboard</button>
      </div>

      <div class="nav-section-label nav-acc-head" data-group="clienti">▾ CLIENTI E RELAZIONE</div>
      <div class="nav-section nav-acc-body" data-group-body="clienti">
        <button data-view="anagrafica">👤 Anagrafica</button>
        <button data-view="scheda">🧾 Scheda cliente</button>
        <button data-view="contatti">☎️ Registro contatti</button>
        <button data-view="richiami">🔔 Richiami <span class="nav-count" id="navCountRichiami">0</span></button>
        <button data-view="consensi" data-advanced="true">✅ Consensi</button>
        <button data-view="documenti">🖨 Documenti</button>
        <button data-view="docscanner">📷 Scanner QR documenti</button>
        <button data-view="timeline" data-advanced="true">🕒 Timeline</button>
      </div>

      <div class="nav-section-label nav-acc-head" data-group="vendite">▾ VENDITE E CONTRATTI</div>
      <div class="nav-section nav-acc-body" data-group-body="vendite">
        <button data-view="contratti">📄 Contratti</button>
        <button data-view="lucegas">⚡ Luce/Gas <span class="nav-count" id="navCountLuceGas">0</span></button>
        <button data-view="device">📱 Device</button>
        <button data-view="magazzino">📦 Magazzino <span class="nav-count" id="navCountMagazzino">0</span></button>
        <button data-view="usato">♻️ Ritiro usato</button>
      </div>

      <div class="nav-section-label nav-acc-head" data-group="laboratorio">▾ LABORATORIO</div>
      <div class="nav-section nav-acc-body" data-group-body="laboratorio">
        <button data-view="riparazioni">🛠 Riparazioni <span class="nav-count" id="navCountRiparazioni">0</span></button>
      </div>

      <div class="nav-section-label nav-acc-head" data-group="marketing" data-advanced="true">▾ ANALISI E MARKETING</div>
      <div class="nav-section nav-acc-body" data-group-body="marketing" data-advanced="true">
        <button data-view="report" data-advanced="true">📈 Report</button>
        <button data-view="automation">📣 Campagne <span class="nav-count" id="navCountCampagne">0</span></button>
        <button data-view="news" data-advanced="true">📰 News telefonia</button>
      </div>

      <div class="nav-section-label nav-acc-head" data-group="dati" data-advanced="true">▾ DATI E SINCRONIZZAZIONE</div>
      <div class="nav-section nav-acc-body" data-group-body="dati" data-advanced="true">
        <button data-view="importexport">⬆️⬇️ Import / Export</button>
        <button data-view="settings" data-advanced="true">⚙️ Google Sheets</button>
      </div>
    </div>
    <div class="sidecard">
      <div class="small muted">Stato ambiente</div>
      <div class="row"><span>Storage</span><b id="envMode">localStorage</b></div>
      <div class="row"><span>Ultimo sync</span><b id="lastSync">—</b></div>
      <div class="row"><span>Record totali</span><b id="totalRecords">0</b></div>
    </div>
    <div class="sidecard">
      <div class="small muted">Azioni rapide</div>
      <div class="actions" style="margin-top:10px">
        <button class="btn secondary small" id="btnSeed">Carica demo</button>
        <button class="btn secondary small" id="btnReset">Reset</button>
        <button class="btn primary small" id="btnSave">Salva</button>
        <button class="btn secondary small" style="width:100%;margin-top:6px;background:#fef3c7;color:#92400e;border-color:#fcd34d" onclick="showView('riparazioni')">🛠 Vai a Riparazioni</button>
      </div>
    </div>
  </aside>

  <main class="main">
    <header class="topbar">
      <div class="topinner">
        <button id="menuToggle" aria-label="Apri menu" title="Menu">&#9776;</button>
        <div>
          <div id="pageTitle" style="font-weight:900;font-size:18px">Dashboard</div>
          <div id="pageSubtitle" class="muted small">Controllo operativo completo • menu organizzato per reparti</div>
        </div>
        <div id="globalSearchBar" title="Cerca ovunque (Ctrl+K)" onclick="gsearchOpen()" style="flex:0 0 auto">
          <span class="gsearch-icon">🔍</span>
          <span>Cerca clienti, CF, IMEI...</span>
          <kbd>Ctrl K</kbd>
        </div>
        <div class="actions">
          <div class="top-quick-actions" id="topQuickActionsBar">
            <button class="btn primary small" id="topQuickCliente">+ Cliente</button>
            <button class="btn primary small" id="topQuickContratto">+ Contratto</button>
            <button class="btn primary small" id="topQuickRiparazione">+ Riparazione</button>
            <button class="btn primary small" id="topQuickLuceGas">+ Luce/Gas</button>
            <label class="mode-toggle" title="Nasconde funzioni avanzate per rendere il CRM più semplice">
              <input type="checkbox" id="simpleModeToggle"> Modalità semplice
            </label>
          </div>
          <button class="btn secondary small" id="btnTopQuickToggle" style="display:none" title="Azioni rapide">⚡ Azioni</button>
          <span class="session-pill" id="sessionStatus">🔒 Accesso richiesto</span>
          <button class="btn secondary small" id="btnLogout">Esci</button>
          <button class="btn secondary small" id="btnManualBackupTop">Backup</button>
          <button class="btn secondary small" id="btnRefresh">Refresh</button>
        </div>
      </div>
    </header>

    <div class="content">
      

<section id="view-dashboard" class="view active">
        <div class="dashboard-data-ticker" aria-label="Messaggi utili gestione dati">
          <div class="ticker-track">
            <span>📌 Un dato inserito bene oggi evita errori domani: codice fiscale, telefono e consenso sempre controllati.</span>
            <span>📊 Ogni cliente racconta una storia: contratti, riparazioni, vendite e richiami devono restare collegati alla scheda cliente.</span>
            <span>✅ Dati ordinati significano campagne migliori, richiami puntuali e meno tempo perso a cercare informazioni.</span>
            <span>🔐 Prima di sincronizzare o fare modifiche importanti, crea sempre un backup di sicurezza.</span>
            <span>🚀 Un CRM funziona davvero quando ogni operazione viene registrata subito, in modo semplice e preciso.</span>
            <span>📌 Un dato inserito bene oggi evita errori domani: codice fiscale, telefono e consenso sempre controllati.</span>
            <span>📊 Ogni cliente racconta una storia: contratti, riparazioni, vendite e richiami devono restare collegati alla scheda cliente.</span>
          </div>
        </div>


        <div class="card sales-hero">
          <div class="hero-grid">
            <div class="hero-copy">
              <div class="badge" style="background:rgba(255,255,255,.15);color:#fff;border-color:rgba(255,255,255,.22)">Flusso vendita rapido</div>
              <div class="hero-title">Apri una nuova attività in pochi secondi</div>
              <div class="small">Identifica il cliente dal codice fiscale, correggi al volo i dati se servono, poi entra direttamente in contratto, device o riparazione.</div>
            </div>
            <div class="hero-stats">
              <div class="hero-stat"><div class="label">Clienti</div><div class="num" id="heroKpiClienti">0</div></div>
              <div class="hero-stat"><div class="label">Contratti 30gg</div><div class="num" id="heroKpiContratti">0</div></div>
              <div class="hero-stat"><div class="label">Device 30gg</div><div class="num" id="heroKpiDevice">0</div></div>
            </div>
          </div>
        </div>

          <div class="card soft" style="margin-top:14px">
            <div style="display:flex;align-items:center;gap:14px;flex-wrap:wrap">
              <div style="flex:1;min-width:260px">
                <h3 style="margin:0 0 4px">Nuova attività rapida</h3>
                <div class="muted small">Inserisci il codice fiscale per trovare il cliente e aprire subito contratto, device o riparazione.</div>
              </div>
              <div style="display:flex;gap:8px;align-items:flex-end;flex:1;min-width:260px">
                <div class="field" style="margin:0;flex:1">
                  <label>Codice fiscale</label>
                  <input id="quickStartCF" placeholder="Inserisci codice fiscale" />
                </div>
                <button class="btn primary" id="btnQuickStart" style="flex-shrink:0">Cerca</button>
              </div>
            </div>
            <div id="quickStartStatus" class="quick-status hide" style="margin-top:10px">Nessuna verifica eseguita.</div>
            <div id="quickStartBox" class="hide" style="margin-top:12px;border-top:1px solid var(--line);padding-top:12px">
              <div id="quickStartClientSummary" style="margin-bottom:10px">Nessun cliente selezionato.</div>
              <div id="quickStartClientEditor" class="form-grid hide" style="margin-top:12px">
                <div class="field"><label>Codice fiscale</label><input id="qs_cf" readonly /></div>
                <div class="field"><label>Tipo cliente</label><select id="qs_tipo"><option value="">—</option><option>PRIVATO</option><option>BUSINESS</option></select></div>
                <div class="field"><label>Nome</label><input id="qs_nome" /></div>
                <div class="field"><label>Cognome</label><input id="qs_cognome" /></div>
                <div class="field"><label>Telefono</label><input id="qs_telefono" /></div>
                <div class="field"><label>Email</label><input id="qs_email" /></div>
                <div class="field"><label>Città</label><input id="qs_citta" /></div>
                <div class="field"><label>Indirizzo</label><input id="qs_indirizzo" /></div>
                <div class="field"><label>Data nascita</label><input id="qs_data_nascita" type="date" /></div>
                <div class="field"><label>Consenso marketing</label><select id="qs_consenso_marketing"><option value="">Da verificare</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
                <div class="field"><label>Consenso WhatsApp</label><select id="qs_consenso_whatsapp"><option value="">Da verificare</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
                <div class="field"><label>Consenso email</label><select id="qs_consenso_email"><option value="">Da verificare</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
                <div class="field"><label>Non disturbare</label><select id="qs_non_disturbare"><option value="">NO</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
              </div>
              <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:10px;align-items:center">
                <button class="btn secondary small" id="btnQuickTimeline">Apri timeline</button>
                <button class="btn primary small" id="btnQuickSaveClient">Salva dati cliente</button>
                <span class="muted small" style="margin-left:auto">Scegli attività →</span>
              </div>
              <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:8px;margin-top:10px">
                <button class="btn primary small" id="btnQuickToContratto" style="display:flex;flex-direction:column;align-items:center;gap:4px;padding:12px 8px"><span style="font-size:18px">📄</span><span>Contratto</span></button>
                <button class="btn primary small" id="btnQuickToDevice" style="display:flex;flex-direction:column;align-items:center;gap:4px;padding:12px 8px"><span style="font-size:18px">📱</span><span>Device</span></button>
                <button class="btn primary small" id="btnQuickToRiparazione" style="display:flex;flex-direction:column;align-items:center;gap:4px;padding:12px 8px"><span style="font-size:18px">🛠</span><span>Riparazione</span></button>
                <button class="btn primary small" id="btnQuickToLuceGas" style="display:flex;flex-direction:column;align-items:center;gap:4px;padding:12px 8px"><span style="font-size:18px">⚡</span><span>Luce/Gas</span></button>
              </div>
            </div>
          </div>

        <div class="card postit-dash-card" style="margin-top:14px">
          <div class="toolbar">
            <div>
              <div class="postit-launcher"><div class="postit-mascot">🗒️</div><div><h3>Post-it veloci</h3><div class="muted small">Scrivili al volo dalla dashboard e assegnali dopo al cliente giusto.</div></div></div>
              <div class="muted small">Prima scrivi il post-it qui dalla dashboard, anche senza codice fiscale. Quando poi apri il cliente in anagrafica puoi assegnarlo al CF corretto e ritrovarlo sempre salvato. Usa <b>Togli da Dashboard</b> per archiviarlo dalla vista generale senza eliminarlo dal cliente.</div><div class="helper" style="margin-top:10px">Suggerimento post-it: per assegnare una bozza puoi scrivere il CF nel campo “Codice fiscale”, nel filtro CF, oppure aprire il cliente e premere “Assegna a cliente”.</div>
            </div>
            <div class="actions">
              <input id="postit_filter_cf" placeholder="Filtra per codice fiscale" style="min-width:240px" />
              <button class="btn secondary small" id="btnPostitFilterCurrent">Usa CF attuale</button>
              <button class="btn secondary small" id="btnPostitShowUnassigned">Vedi bozze</button><button class="btn primary small" id="btnAssignVisibleDraftsToCF">Assegna bozze al CF</button>
            </div>
          </div>
          <div class="hr"></div>
          <div class="postit-shell">
            <div class="card soft">
              <div class="form-grid">
                <div class="field"><label>Codice fiscale (facoltativo)</label><input id="postit_cf" placeholder="Puoi lasciarlo vuoto e assegnarlo dopo" /></div>
                <div class="field"><label>Titolo</label><input id="postit_title" placeholder="Es. Da richiamare martedì" /></div>
                <div class="field"><label>Colore</label><select id="postit_color"><option value="yellow">Giallo</option><option value="blue">Blu</option><option value="green">Verde</option><option value="pink">Rosa</option><option value="orange">Arancione</option></select></div>
                <div class="field" style="grid-column:1/-1"><label>Nota</label><textarea id="postit_text" placeholder="Scrivi qui il tuo promemoria stile post-it"></textarea></div>
              </div>
              <div class="actions" style="margin-top:12px">
                <button class="btn primary" id="btnSavePostit">Salva post-it</button>
                <button class="btn secondary" id="btnAssignPostitToForm">Assegna post-it al CF</button>
                <button class="btn secondary" id="btnClearPostit">Pulisci</button>
              </div>
            </div>
            <div>
              <div class="toolbar" style="margin-bottom:10px">
                <div class="muted small" id="postitBoardTitle">Post-it salvati</div>
              </div>
              <div id="postitBoard" class="postit-board"></div>
            </div>
          </div>


        <div class="grid kpi" style="margin-top:14px">
          <div class="card soft"><div class="muted small">Clienti totali</div><div class="value" id="kpiClienti">0</div><div class="kpi-trend neutral" id="kpiClientiTrend">—</div><div class="kpi-sparkline good" id="kpiClientiSpark"></div></div>
          <div class="card soft"><div class="muted small">Contratti 30gg</div><div class="value" id="kpiContratti">0</div><div class="kpi-trend neutral" id="kpiContrattiTrend">—</div><div class="kpi-sparkline" id="kpiContrattiSpark"></div></div>
          <div class="card soft"><div class="muted small">Device 30gg</div><div class="value" id="kpiDevice">0</div><div class="kpi-trend neutral" id="kpiDeviceTrend">—</div><div class="kpi-sparkline" id="kpiDeviceSpark"></div></div>
          <div class="card soft"><div class="muted small">Riparazioni aperte</div><div class="value" id="kpiRip">0</div><div class="kpi-trend neutral" id="kpiRipTrend">—</div><div class="kpi-sparkline warn" id="kpiRipSpark"></div></div>
          <div class="card soft"><div class="muted small">Scadenze 30gg</div><div class="value" id="kpiLuceGas">0</div><div class="kpi-trend neutral" id="kpiLuceGasTrend">—</div><div class="kpi-sparkline danger" id="kpiLuceGasSpark"></div></div>
        </div>
        <div class="card" style="margin-top:14px">
          <div class="toolbar"><div><h3>Qualità dati</h3><div class="muted small">Controllo rapido di clienti, contatti e record collegati.</div></div><div class="actions"><button class="btn secondary small" onclick="backupLocalData('manuale')">Backup JSON</button></div></div>
          <div class="data-quality" id="dataQualityBox"></div>
        </div>

        <div class="grid two" style="margin-top:14px">
          <div class="card"><h3>Attività ultimi 30 giorni</h3><canvas id="chartTypes"></canvas></div>
          <div class="card"><h3>Top venditori</h3><canvas id="chartSellers"></canvas></div>
        </div>
        <div class="grid two" style="margin-top:14px">
          <div class="card"><h3>Contratti per compagnia</h3><canvas id="chartCompanies"></canvas></div>
          <div class="card"><h3>Contratti Luce/Gas</h3><canvas id="chartLuceGas"></canvas><div class="muted small" style="margin-top:8px">Divisione per LUCE, GAS e DUAL negli ultimi 30 giorni.</div></div>
        </div>
        <div class="grid two" style="margin-top:14px">
          <div class="card"><h3>Stato pratiche Luce/Gas</h3><canvas id="chartLuceGasStati"></canvas><div class="muted small" style="margin-top:8px">Controllo pratiche inserite, in attesa, OK, KO o annullate.</div></div>
          <div class="card"><h3>Timeline operativa 30gg</h3><div class="timeline" id="dashboardTimeline"></div></div>
        </div>
      </section>



      <section id="view-anagrafica" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card">
          <div class="toolbar">
            <div>
              <h3>Anagrafica clienti</h3>
              <div class="muted small">PK = Codice Fiscale. Dati normalizzati e pronti per Google Sheets.</div><div class="helper" style="margin-top:10px">Ora i consensi si inseriscono direttamente quando crei o modifichi il cliente. Servono per campagne WhatsApp/email e per rispettare il “non disturbare”.</div>
            </div>
            <div class="actions">
              <input id="searchAnag" placeholder="Cerca cliente" style="min-width:260px" />
              <button class="btn secondary small" data-export="anagrafica">Export CSV</button>
            </div>
          </div>
          <div class="hr"></div>
          <div class="form-grid">
            <div class="field"><label>Codice fiscale *</label><input id="a_cf" /></div>
            <div class="field"><label>Nome *</label><input id="a_nome" /></div>
            <div class="field"><label>Cognome *</label><input id="a_cognome" /></div>
            <div class="field"><label>Tipo cliente</label><select id="a_tipo"><option value="">—</option><option>PRIVATO</option><option>BUSINESS</option></select></div>
            <div class="field"><label>Telefono</label><input id="a_telefono" /></div>
            <div class="field"><label>Email</label><input id="a_email" /></div>
            <div class="field"><label>Città</label><input id="a_citta" /></div>
            <div class="field"><label>Indirizzo</label><input id="a_indirizzo" /></div>
            <div class="field"><label>Data nascita</label><input id="a_data_nascita" type="date" /></div>
            <div class="field"><label>Consenso marketing</label><select id="a_consenso_marketing"><option value="">Da verificare</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
            <div class="field"><label>Consenso WhatsApp</label><select id="a_consenso_whatsapp"><option value="">Da verificare</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
            <div class="field"><label>Consenso email</label><select id="a_consenso_email"><option value="">Da verificare</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
            <div class="field"><label>Non disturbare</label><select id="a_non_disturbare"><option value="">NO</option><option value="SI">SI</option><option value="NO">NO</option></select></div>
            <div class="field"><label>Data consenso</label><input id="a_data_consenso" type="date" /></div>
            <div class="field" style="grid-column:1/-1"><label>Note privacy / consensi</label><textarea id="a_note_privacy" placeholder="Es. consenso raccolto in negozio, telefonico, revocato, da aggiornare..."></textarea></div>
          </div>
          <div class="actions" style="margin-top:12px">
            <button class="btn primary" id="btnSaveAnag">Salva cliente</button>
            <button class="btn secondary" id="btnClearAnag">Pulisci</button>
          </div>
        </div>
        <div class="card" style="margin-top:14px">
          <h3>Clienti</h3>
          <div class="tablewrap"><table id="tblAnag"><thead><tr><th>Cliente</th><th>Contatti</th><th>Tipo</th><th>Attività</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>

      </section>

      
<section id="view-contratti" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card module-hero">
          <div class="toolbar">
            <div>
              <div class="section-label">📄 Vendita contratti</div>
              <h3 style="margin-top:10px">Attivazioni, rinnovi e portabilità</h3>
              <div class="lead">Compila la pratica in modo guidato: verifica cliente, configura offerta, indica eventuale utilizzatore reale della SIM e completa MNP o telefono incluso.</div>
            </div>
            <div class="module-actions">
              <input id="searchCon" placeholder="Cerca contratto" style="min-width:260px" />
              <button class="btn secondary" data-export="contratti">Export CSV</button>
            </div>
          </div>
          <div class="module-statbar">
            <div class="module-stat"><div class="k">Focus</div><div class="v">Cliente → Offerta</div></div>
            <div class="module-stat"><div class="k">Flusso</div><div class="v">Anagrafica + Contratto</div></div>
            <div class="module-stat"><div class="k">Consiglio</div><div class="v">Controlla MNP e vincoli</div></div>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <div class="helper">Flusso corretto: inserisci il CF, il sistema verifica subito se il cliente esiste. Se manca, lo crei in Anagrafica e poi salvi il contratto.</div>
          <div class="hr"></div>
          <div class="form-shell">
            <div class="card soft">
              <div class="toolbar"><div><h3>Dati principali contratto</h3><div class="muted small">Campi principali della pratica commerciale.</div></div></div>
              <div class="form-grid">
                <div class="field"><label>ID contratto</label><input id="c_id" placeholder="Auto se vuoto" /></div>
                <div class="field"><label>ID cliente</label><input id="c_id_cliente" /></div>
                <div class="field"><label>Codice fiscale *</label><input id="c_cf" /></div>
                <div class="field"><label>Data contratto *</label><input id="c_data_contratto" type="date" /></div>
                <div class="field"><label>Tipo cliente</label><select id="c_tipo_cliente"><option value="">—</option><option>PRIVATO</option><option>BUSINESS</option></select></div>
                <div class="field"><label>Compagnia</label><select id="c_compagnia"><option value="">—</option><option>TIM</option><option>VODAFONE</option><option>WINDTRE</option><option>SKY WIFI</option><option>SKY TV</option><option>ILIAD</option><option>FASTWEB</option><option>POSTEMOBILE</option><option>HO.</option><option>KENA</option><option>VERY MOBILE</option><option>TISCALI</option></select></div>
                <div class="field"><label>Tecnologia</label><select id="c_tecnologia"><option value="">—</option><option>SIM</option><option>FIBRA</option><option>FWA</option><option>ADSL</option><option>TV</option></select></div>
                <div class="field"><label>Tipo attivazione</label><select id="c_tipo_attivazione"><option value="">—</option><option>NUOVA</option><option>MNP</option><option>MIGRAZIONE</option><option>SUBENTRO</option><option>VARIAZIONE</option></select></div>
                <div class="field"><label>Numero lavorato</label><input id="c_numero_lavorato" /></div>
                <div class="field"><label>Utilizzatore reale SIM</label><input id="c_utilizzatore_nome" placeholder="Es. figlio, marito, nonno..." /></div>
                <div class="field"><label>Relazione utilizzatore</label><select id="c_utilizzatore_relazione"><option value="">—</option><option>TITOLARE</option><option>FIGLIO/A</option><option>MARITO/MOGLIE</option><option>GENITORE</option><option>NONNO/A</option><option>DIPENDENTE</option><option>ALTRO</option></select></div>
                <div class="field"><label>Telefono utilizzatore</label><input id="c_utilizzatore_telefono" placeholder="Facoltativo" /></div>
                <div class="field"><label>Note utilizzatore</label><input id="c_utilizzatore_note" placeholder="Es. SIM usata dal figlio minorenne" /></div>
                <div class="field"><label>Nome offerta</label><input id="c_nome_offerta" /></div>
                <div class="field"><label>Costo offerta (€)</label><input id="c_costo_offerta" type="number" step="0.01" /></div>
                <div class="field"><label>Tipo pagamento</label><select id="c_tipo_pagamento"><option value="">—</option><option>CREDITO RESIDUO</option><option>SDD</option><option>CARTA DI CREDITO</option></select></div>
                <div class="field"><label>Vincolo offerta (mesi)</label><input id="c_vincolo_offerta_mesi" type="number" step="1" /></div>
                <div class="field"><label>Data attivazione</label><input id="c_data_attivazione" type="date" /></div>
                <div class="field"><label>Fine vincolo offerta</label><input id="c_data_fine_vincolo_offerta" type="date" readonly /></div>
                <div class="field"><label>Convergenza</label><select id="c_convergenza"><option value="">—</option><option>SI</option><option>NO</option></select></div>
                <div class="field"><label>Telefono incluso</label><select id="c_telefono_incluso"><option value="">—</option><option>SI</option><option>NO</option></select></div>
                <div class="field"><label>MNP</label><input id="c_mnp" readonly /></div>
              </div>
            </div>

            <div class="grid two">
              <div class="card soft">
                <h3>Dati MNP</h3>
                <div class="muted small">Compila solo se il contratto prevede portabilità.</div>
                <div class="form-grid" style="margin-top:10px">
                  <div class="field"><label>Compagnia provenienza</label><input id="c_compagnia_provenienza" /></div>
                  <div class="field"><label>ICCID vecchio</label><input id="c_iccid_vecchio" /></div>
                  <div class="field"><label>ICCID nuovo</label><input id="c_iccid_nuovo" /></div>
                  <div class="field"><label>Data portabilità</label><input id="c_data_portabilita" type="date" /></div>
                </div>
              </div>
              <div class="card soft">
                <h3>Telefono incluso</h3>
                <div class="muted small">Dati del device eventualmente associato al contratto.</div>
                <div class="form-grid" style="margin-top:10px">
                  <div class="field" style="grid-column:1/-1"><label>Telefono incluso da magazzino Kolme</label><select id="c_magazzino_id"><option value="">— Nessun telefono da magazzino —</option></select><div class="muted small">Mostra solo smartphone DISPONIBILI con fornitore Kolme.</div></div>
                  <div class="field"><label>IMEI</label><input id="c_imei" /></div>
                  <div class="field"><label>Marca</label><input id="c_tel_marca" /></div>
                  <div class="field"><label>Modello</label><input id="c_modello" /></div>
                  <div class="field"><label>Modalità pagamento</label><select id="c_tel_modalita_pagamento"><option value="">—</option><option>SDD</option><option>CARTA DI CREDITO</option><option>COMPASS</option><option>FINDOMESTIC</option></select></div>
                  <div class="field"><label>Mesi vincolo telefono</label><input id="c_mesi_vincolo_telefono" type="number" step="1" /></div>
                  <div class="field"><label>Costo rate</label><input id="c_tel_costo_rate" type="number" step="0.01" /></div>
                  <div class="field"><label>Fine vincolo telefono</label><input id="c_data_fine_vincolo_telefono" type="date" readonly /></div>
                </div>
              </div>
            </div>

            <div class="actions"><button class="btn primary" id="btnSaveCon">Salva contratto</button><button class="btn secondary" id="btnClearCon">Pulisci</button></div>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <h3>Archivio contratti</h3>
          <div class="tablewrap"><table id="tblCon"><thead><tr><th>ID</th><th>Data</th><th>CF</th><th>Cliente</th><th>Compagnia</th><th>Offerta</th><th>Tecnologia</th><th>Attivazione</th><th>MNP</th><th>Numero</th><th>Utilizzatore</th><th>Portabilità</th><th>ICCID</th><th>Pagamento</th><th>Telefono</th><th>Note</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>
      </section>


      

      
      <section id="view-usato" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card module-hero">
          <div class="toolbar">
            <div>
              <div class="section-label">♻️ Ritiro smartphone usato da privato</div>
              <h3 style="margin-top:10px">Acquisto da privato, laboratorio o magazzino</h3>
              <div class="lead">Registra il venditore privato, genera la dichiarazione da firmare e scegli se mandare subito il telefono a magazzino oppure fermarlo in laboratorio.</div>
            </div>
            <div class="module-actions">
              <input id="searchUsato" placeholder="Cerca venditore, marca, modello, IMEI" style="min-width:260px" />
              <button class="btn secondary" data-export="usato">Export CSV</button>
            </div>
          </div>
          <div class="module-statbar">
            <div class="module-stat"><div class="k">Ritiri totali</div><div class="v" id="usatoKpiTot">0</div></div>
            <div class="module-stat"><div class="k">Da decidere</div><div class="v" id="usatoKpiDaDecidere">0</div></div>
            <div class="module-stat"><div class="k">In laboratorio</div><div class="v" id="usatoKpiLab">0</div></div>
            <div class="module-stat"><div class="k">In magazzino</div><div class="v" id="usatoKpiMag">0</div></div>
          </div>
        </div>

        <div class="grid two" style="margin-top:14px">
          <div class="card">
            <h3>Modulo ritiro usato</h3>
            <div class="muted small">Compila i dati del privato che vende il telefono e i dati tecnici del dispositivo. La ricevuta segue il modello che hai allegato.</div>
            <div class="form-grid" style="margin-top:14px">
              <div class="field"><label>ID ritiro</label><input id="u_id" placeholder="Auto se vuoto" /></div>
              <div class="field"><label>Data ritiro</label><input id="u_data" type="date" /></div>
              <div class="field"><label>Numero ricevuta</label><input id="u_numero_ricevuta" placeholder="Es. ACQ-0001/2026" /></div>
              <div class="field"><label>Prezzo acquisto (€)</label><input id="u_prezzo_acquisto" /></div>

              <div class="field"><label>Nome venditore *</label><input id="u_nome" /></div>
              <div class="field"><label>Cognome venditore *</label><input id="u_cognome" /></div>
              <div class="field"><label>Codice fiscale venditore *</label><input id="u_cf" /></div>
              <div class="field"><label>Telefono venditore</label><input id="u_telefono" /></div>
              <div class="field"><label>Nato/a a</label><input id="u_luogo_nascita" /></div>
              <div class="field"><label>Provincia nascita</label><input id="u_prov_nascita" maxlength="2" /></div>
              <div class="field"><label>Data nascita</label><input id="u_data_nascita" type="date" /></div>
              <div class="field"><label>Documento identità</label><input id="u_documento" placeholder="Tipo e numero documento" /></div>
              <div class="field"><label>Indirizzo residenza</label><input id="u_indirizzo" /></div>
              <div class="field"><label>N°</label><input id="u_civico" /></div>
              <div class="field"><label>CAP</label><input id="u_cap" /></div>
              <div class="field"><label>Città / Provincia</label><input id="u_citta_prov" placeholder="Es. Viterbo (VT)" /></div>

              <div class="field"><label>Marca *</label><input id="u_marca" /></div>
              <div class="field"><label>Modello *</label><input id="u_modello" /></div>
              <div class="field"><label>IMEI *</label><input id="u_imei" /></div>
              <div class="field"><label>Memoria</label><input id="u_memoria" placeholder="Es. 128GB" /></div>
              <div class="field"><label>Colore</label><input id="u_colore" /></div>
              <div class="field"><label>Accessori inclusi</label><input id="u_accessori" placeholder="Scatola, caricatore, cavo..." /></div>
              <div class="field"><label>Stato estetico/funzionale</label><select id="u_condizioni"><option value="BUONO">BUONO</option><option>OTTIMO</option><option>DA TESTARE</option><option>DA RIPARARE</option><option>DANNEGGIATO</option></select></div>
              <div class="field"><label>Destinazione iniziale</label><select id="u_destinazione"><option value="DA_DECIDERE">DA DECIDERE</option><option value="MAGAZZINO">SUBITO A MAGAZZINO</option><option value="LABORATORIO">FERMA IN LABORATORIO</option></select></div>
              <div class="field"><label>Prezzo vendita consigliato (€)</label><input id="u_prezzo_vendita" /></div>
              <div class="field"><label>Costo riparazione stimato (€)</label><input id="u_costo_riparazione" /></div>
              <div class="field" style="grid-column:1/-1"><label>Note / difetti dichiarati</label><textarea id="u_note" placeholder="Es. batteria da verificare, display graffiato, Face ID ok..."></textarea></div>
              <div class="field" style="grid-column:1/-1"><label>Parti riparate / interventi eseguiti</label><textarea id="u_parti_riparate" placeholder="Da compilare solo dopo laboratorio: display, batteria, connettore, pulizia, test..."></textarea></div>
            </div>
            <div class="actions" style="margin-top:14px">
              <button class="btn primary" id="btnSaveUsato">Salva ritiro</button>
              <button class="btn secondary" id="btnPrintUsato">Genera / stampa dichiarazione</button>
              <button class="btn good" id="btnUsatoToMag">Invia a magazzino</button>
              <button class="btn warn" id="btnUsatoToLab">Ferma in laboratorio</button>
              <button class="btn good" id="btnUsatoLabToMag">Dopo riparazione → magazzino</button>
              <button class="btn secondary" id="btnClearUsato">Pulisci</button>
            </div>
          </div>

          <div class="card">
            <h3>Flusso operativo consigliato</h3>
            <div class="info-box" style="margin-top:10px">
              <b>1. Ritiro da privato</b><br>Compila venditore, telefono, IMEI, prezzo e stampa la dichiarazione da far firmare.
            </div>
            <div class="info-box" style="margin-top:10px">
              <b>2A. Telefono pronto</b><br>Premi <b>Invia a magazzino</b>: il CRM crea automaticamente il pezzo in Magazzino come DISPONIBILE.
            </div>
            <div class="info-box" style="margin-top:10px">
              <b>2B. Telefono da sistemare</b><br>Premi <b>Ferma in laboratorio</b>: il CRM crea una pratica riparazione interna collegata al ritiro.
            </div>
            <div class="info-box" style="margin-top:10px">
              <b>3. Dopo laboratorio</b><br>Compila parti riparate e costo, poi premi <b>Dopo riparazione → magazzino</b> per renderlo vendibile.
            </div>
            <div class="helper" style="margin-top:12px">
              <b>Nota fiscale</b><br>La dichiarazione riporta la cessione fuori campo IVA da privato e lo spazio per marca da bollo da 2,00 € ove dovuta.
            </div>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <h3>Ritiri usato da privato</h3>
          <div class="tablewrap"><table id="tblUsato"><thead><tr><th>ID</th><th>Data</th><th>Venditore</th><th>CF</th><th>Telefono</th><th>Device</th><th>IMEI</th><th>Prezzo</th><th>Stato</th><th>Collegamenti</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>
      </section>

      <section id="view-magazzino" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card module-hero">
          <div class="toolbar">
            <div>
              <div class="section-label">📦 Magazzino smartphone</div>
              <h3 style="margin-top:10px">Carico telefoni, IMEI e disponibilità</h3>
              <div class="lead">Inserisci i telefoni a magazzino. Quando vendi un device o colleghi un telefono incluso nei contratti da fornitore Kolme, il CRM scarica automaticamente l'IMEI e lo segna come venduto.</div>
            </div>
            <div class="module-actions">
              <input id="searchMag" placeholder="Cerca marca, modello, IMEI, fornitore" style="min-width:260px" />
              <button class="btn secondary" data-export="magazzino">Export CSV</button>
            </div>
          </div>
          <div class="module-statbar">
            <div class="module-stat"><div class="k">Disponibili</div><div class="v" id="magKpiDisp">0</div></div>
            <div class="module-stat"><div class="k">Venduti</div><div class="v" id="magKpiSold">0</div></div>
            <div class="module-stat"><div class="k">Valore stock</div><div class="v" id="magKpiValue">€ 0</div></div>
          </div>
        </div>

        <div class="grid two" style="margin-top:14px">
          <div class="card">
            <h3>Carica / modifica smartphone</h3>
            <div class="muted small">L'IMEI è la chiave principale: non puoi caricare due telefoni disponibili con lo stesso IMEI.</div>
            <div class="form-grid" style="margin-top:12px">
              <div class="field"><label>ID magazzino</label><input id="m_id" placeholder="Auto se vuoto" /></div>
              <div class="field"><label>Data carico</label><input id="m_data_carico" type="date" /></div>
              <div class="field"><label>Numero fattura / ordine</label><input id="m_numero_fattura" placeholder="Es. FT 123/2026 o ordine Kolme" /></div>
              <div class="field"><label>Marca *</label><input id="m_marca" /></div>
              <div class="field"><label>Modello *</label><input id="m_modello" /></div>
              <div class="field"><label>IMEI *</label><input id="m_imei" /></div>
              <div class="field"><label>Memoria</label><input id="m_memoria" placeholder="Es. 128GB" /></div>
              <div class="field"><label>Colore</label><input id="m_colore" /></div>
              <div class="field"><label>Fornitore</label><input id="m_fornitore" /></div>
              <div class="field"><label>Prezzo acquisto (€)</label><input id="m_prezzo_acquisto" type="number" step="0.01" /></div>
              <div class="field"><label>Prezzo vendita consigliato (€)</label><input id="m_prezzo_vendita" type="number" step="0.01" /></div>
              <div class="field"><label>Stato</label><select id="m_stato"><option>DISPONIBILE</option><option>VENDUTO</option><option>RISERVATO</option><option>RESO</option></select></div>
              <div class="field" style="grid-column:1/-1"><label>Note</label><textarea id="m_note" placeholder="Es. promo, provenienza, accessori inclusi..."></textarea></div>
            </div>
            <div class="actions" style="margin-top:12px">
              <button class="btn primary" id="btnSaveMag">Salva smartphone</button>
              <button class="btn secondary" id="btnClearMag">Pulisci</button>
            </div>
          </div>

          <div class="card soft">
            <h3>Come funziona lo scarico automatico</h3>
            <div class="helper" style="margin-top:10px">
              1) Carichi il telefono in Magazzino con IMEI.<br>
              2) In <b>Device</b> scegli lo smartphone dal menu “Da magazzino”.<br>
              3) Quando salvi la vendita, il telefono passa a <b>VENDUTO</b> e viene collegato al cliente.
            </div>
            <div class="hr"></div>
            <h3>Attenzione</h3>
            <div class="muted small">Se cancelli una vendita device collegata al magazzino, il CRM rimette quel telefono come DISPONIBILE.</div>
          </div>
        </div>


        <!-- FORM CARICA FATTURA FORNITORE -->
        <div class="card" style="margin-top:14px;border:2px solid #bfdbfe;background:#eff6ff">
          <div class="toolbar">
            <div>
              <h3 style="margin:0;color:#1d4ed8">&#128196; Carica fattura fornitore</h3>
              <div class="muted small">Inserisci i dati della fattura e aggiungi le righe — il CRM crea i record in magazzino automaticamente.</div>
            </div>
            <div class="actions">
              <button class="btn secondary small" id="btnToggleFattura" onclick="(function(){var w=document.getElementById('fatturaFormWrap');if(!w)return;var open=w.style.display!=='none';w.style.display=open?'none':'block';this.textContent=open?'▼ Mostra form fattura':'▲ Nascondi form fattura';if(!open&&!window.fatturaRighe.length)window.addFatturaRiga();}).call(this)">&#9660; Mostra form fattura</button>
            </div>
          </div>
          <div id="fatturaFormWrap" style="display:none;margin-top:16px">
            <!-- TESTATA FATTURA -->
            <div class="card soft" style="margin-bottom:14px">
              <h4 style="margin-bottom:12px;color:#374151">Dati fattura</h4>
              <div class="form-grid">
                <div class="field"><label>Numero fattura *</label><input id="fat_numero" placeholder="Es. FT-2026-001" /></div>
                <div class="field"><label>Fornitore *</label><input id="fat_fornitore" placeholder="Es. Apple, Samsung, Ingram" /></div>
                <div class="field"><label>Data fattura *</label><input id="fat_data" type="date" /></div>
                <div class="field"><label>Note fattura</label><input id="fat_note" placeholder="Note opzionali" /></div>
              </div>
            </div>
            <!-- RIGHE ARTICOLI -->
            <div class="card soft" style="margin-bottom:14px">
              <div class="toolbar" style="margin-bottom:12px">
                <h4 style="margin:0;color:#374151">Articoli</h4>
                <button class="btn secondary small" id="btnAddFatRiga" onclick="window.addFatturaRiga()">+ Aggiungi riga</button>
              </div>
              <div id="fatturaRighe">
                <!-- righe generate dinamicamente -->
              </div>
              <div id="fatturaEmpty" style="text-align:center;padding:20px;color:#94a3b8;font-size:13px">
                Nessun articolo ancora. Clicca "+ Aggiungi riga" per iniziare.
              </div>
            </div>
            <!-- RIEPILOGO -->
            <div id="fatturaRiepilogo" style="display:none;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;padding:14px;margin-bottom:14px">
              <div style="font-size:13px;font-weight:600;color:#15803d;margin-bottom:4px" id="fatturaRiepilogoTxt"></div>
            </div>
            <div class="actions">
              <button class="btn primary" id="btnImportaFattura" onclick="window.importaFattura()">&#128230; Importa in magazzino</button>
              <button class="btn secondary" id="btnResetFattura" onclick="window.resetFattura()">Pulisci</button>
            </div>
          </div>
        </div>

        <!-- MODAL SCANNER IMEI -->
        <div id="imeiScannerModal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.8);z-index:9998;align-items:center;justify-content:center">
          <div style="background:#fff;border-radius:16px;padding:24px;width:min(480px,95vw);max-width:100%">
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:16px">
              <h3 style="margin:0">&#128247; Scansiona IMEI</h3>
              <button onclick="closeImeiScanner()" style="background:none;border:none;font-size:20px;cursor:pointer;color:#64748b">&#x2715;</button>
            </div>
            <div id="scannerContainer" style="width:100%;aspect-ratio:4/3;background:#000;border-radius:8px;overflow:hidden;position:relative;margin-bottom:16px">
              <video id="scannerVideo" style="width:100%;height:100%;object-fit:cover" playsinline></video>
              <div style="position:absolute;inset:0;display:flex;align-items:center;justify-content:center;pointer-events:none">
                <div style="width:60%;height:2px;background:rgba(204,0,0,.8);box-shadow:0 0 10px rgba(204,0,0,.8)"></div>
              </div>
              <div id="scannerStatus" style="position:absolute;bottom:10px;left:0;right:0;text-align:center;color:#fff;font-size:12px;font-weight:600;background:rgba(0,0,0,.5);padding:4px">Punta la fotocamera sul barcode IMEI...</div>
            </div>
            <div style="display:flex;gap:8px">
              <input id="imeiManualInput" placeholder="Oppure inserisci IMEI manualmente" style="flex:1;padding:9px 12px;border:1px solid #e2e8f0;border-radius:8px;font-size:13px;font-family:monospace">
              <button onclick="confirmManualImei()" style="background:#1d4ed8;color:#fff;border:none;padding:9px 16px;border-radius:8px;font-size:13px;font-weight:700;cursor:pointer">OK</button>
            </div>
            <div style="margin-top:12px;font-size:11px;color:#94a3b8;text-align:center">
              Su iPhone/iPad: il browser deve avere accesso alla fotocamera. Su Chrome Android funziona nativamente.
            </div>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <h3>Smartphone a magazzino</h3>
          <div class="tablewrap"><table id="tblMag"><thead><tr><th>Stato</th><th>Data carico</th><th>Fattura/Ordine</th><th>Marca</th><th>Modello</th><th>IMEI</th><th>Memoria</th><th>Colore</th><th>Acquisto</th><th>Vendita</th><th>Fornitore</th><th>Cliente vendita</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>
      </section>

<section id="view-device" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card module-hero">
          <div class="toolbar">
            <div>
              <div class="section-label">📱 Vendita device</div>
              <h3 style="margin-top:10px">Smartphone, garanzie e finanziamenti</h3>
              <div class="lead">Registra velocemente la vendita, stampa la ricevuta e tieni sotto controllo garanzia e rate.</div>
            </div>
            <div class="module-actions">
              <input id="searchDev" placeholder="Cerca device" style="min-width:260px" />
              <button class="btn secondary" data-export="device">Export CSV</button>
            </div>
          </div>
          <div class="module-statbar">
            <div class="module-stat"><div class="k">Focus</div><div class="v">Vendita + ricevuta</div></div>
            <div class="module-stat"><div class="k">Controllo</div><div class="v">Garanzia e pagamenti</div></div>
            <div class="module-stat"><div class="k">Suggerimento</div><div class="v">Stampa subito la ricevuta</div></div>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <div class="form-shell">
            <div class="card soft">
              <div class="toolbar"><div><h3>Dati vendita device</h3><div class="muted small">Campi principali della vendita e del pagamento.</div></div></div>
              <div class="form-grid">
                <div class="field"><label>ID device</label><input id="d_id" placeholder="Auto se vuoto" /></div>
                <div class="field" style="grid-column:1/-1"><label>Da magazzino</label><select id="d_magazzino_id"><option value="">— Vendita libera / non da stock —</option></select></div>
                <div class="field"><label>CF *</label><input id="d_cf" /></div>
                <div class="field"><label>Data vendita *</label><input id="d_data" type="date" /></div>
                <div class="field"><label>Marca *</label><input id="d_marca" /></div>
                <div class="field"><label>Modello *</label><input id="d_modello" /></div>
                <div class="field"><label>IMEI *</label><input id="d_imei" /></div>
                <div class="field"><label>Prezzo (€) *</label><input id="d_prezzo" type="number" step="0.01" /></div>
                <div class="field"><label>Garanzia (mesi)</label><input id="d_garanzia_mesi" type="number" step="1" value="24" /></div>
                <div class="field"><label>Fine garanzia</label><input id="d_fine_garanzia" type="date" readonly /></div>
                <div class="field"><label>Pagamento</label><select id="d_pagamento"><option value="">—</option><option>CASH</option><option>ELETTRONICO</option><option>FINANZIAMENTO</option></select></div>
                <div class="field"><label>Venditore</label><input id="d_venditore" /></div>
                <div class="field"><label>Finanziaria</label><select id="d_finanziaria"><option value="">—</option><option>COMPASS</option><option>FINDOMESTIC</option></select></div>
                <div class="field"><label>Costo rata</label><input id="d_costo_rata" type="number" step="0.01" /></div>
                <div class="field"><label>Durata rate (mesi)</label><input id="d_durata_rata_mesi" type="number" step="1" /></div>
                <div class="field"><label>Fine pagamento</label><input id="d_fine_pagamento" type="date" readonly /></div>
              </div>
            </div>
            <div class="actions"><button class="btn primary" id="btnSaveDev">Salva device</button><button class="btn secondary" id="btnPrintDevReceipt">Stampa ricevuta</button><button class="btn secondary" id="btnClearDev">Pulisci</button></div>
          </div>
        </div>

        <div class="card" style="margin-top:14px"><h3>Device venduti</h3><div class="tablewrap"><table id="tblDev"><thead><tr><th>ID</th><th>Data</th><th>CF</th><th>Cliente</th><th>Marca</th><th>Modello</th><th>IMEI</th><th>Prezzo</th><th>Pagamento</th><th>Fine garanzia</th><th>Finanziaria</th><th>Venditore</th><th>Azioni</th></tr></thead><tbody></tbody></table></div></div>
      </section>


      
<section id="view-riparazioni" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card module-hero">
          <div class="toolbar">
            <div>
              <div class="section-label">🛠 Laboratorio</div>
              <h3 style="margin-top:10px">Riparazioni, stato pratica e consegna</h3>
              <div class="lead">Apri la pratica, aggiorna lo stato del laboratorio e ristampa la ricevuta quando ti serve. Ora include anche la clausola di presa in carico e mancato ritiro.</div>
            </div>
            <div class="module-actions">
              <input id="searchRip" placeholder="Cerca riparazione" style="min-width:260px" />
              <button class="btn secondary" data-export="riparazioni">Export CSV</button>
            </div>
          </div>
          <div class="module-statbar">
            <div class="module-stat"><div class="k">Focus</div><div class="v">Ingresso laboratorio</div></div>
            <div class="module-stat"><div class="k">Controllo</div><div class="v">Stato e note</div></div>
            <div class="module-stat"><div class="k">Suggerimento</div><div class="v">Rilascia la ricevuta subito</div></div>
          </div>
        </div>

        <div class="card" style="margin-top:14px">
          <div class="form-shell">
            <div class="card soft">
              <div class="toolbar"><div><h3>Dati pratica riparazione</h3><div class="muted small">Informazioni essenziali della presa in carico.</div></div></div>
              <div class="form-grid">
                <div class="field"><label>ID riparazione</label><input id="r_id" placeholder="Auto se vuoto" /></div>
                <div class="field"><label>CF *</label><input id="r_cf" /></div>
                <div class="field"><label>Data ingresso *</label><input id="r_data_ingresso" type="date" /></div>
                <div class="field"><label>Marca *</label><input id="r_marca" /></div>
                <div class="field"><label>Modello *</label><input id="r_modello" /></div>
                <div class="field"><label>IMEI</label><input id="r_imei" /></div>
                <div class="field"><label>Problematica</label><input id="r_problema" /></div>
                <div class="field"><label>Stato *</label><select id="r_stato"><option value="">—</option><option>APERTA</option><option>IN LAVORAZIONE</option><option>PRONTA</option><option>CONSEGNATA</option></select></div>
                <div class="field"><label>Costo (€)</label><input id="r_costo" type="number" step="0.01" /></div>
                <div class="field" style="grid-column:1/-1"><label>Note</label><textarea id="r_note"></textarea></div>
                <div class="field"><label>Giorni per ritiro dopo avviso</label><input id="r_giorni_ritiro" type="number" min="1" step="1" value="90" /></div>
                <div class="field"><label>Data avviso dispositivo pronto</label><input id="r_data_avviso_pronto" type="date" /></div>
                <div class="field"><label>Data limite ritiro</label><input id="r_data_limite_ritiro" type="date" readonly /><div class="field-hint warn" id="r_data_limite_ritiro_hint" style="display:none">⚠️ Compilare "Data avviso dispositivo pronto" per calcolare il limite</div></div>
                <div class="field"><label>Condizioni ritiro accettate</label><select id="r_accetta_condizioni"><option value="SI">SI</option><option value="NO">NO</option></select></div>
                <div class="field" style="grid-column:1/-1"><label>Condizioni di presa in carico / ritiro</label><textarea id="r_condizioni_ritiro" readonly>CONDIZIONI DI PRESA IN CARICO E RITIRO DISPOSITIVO
Il cliente dichiara di consegnare il dispositivo per diagnosi/riparazione e autorizza SAGAM alla custodia del bene fino al ritiro. Il dispositivo dovrà essere ritirato entro il termine indicato nella ricevuta a partire dalla comunicazione di dispositivo pronto o dalla data concordata per il ritiro.

In caso di mancato ritiro entro il termine indicato, SAGAM potrà inviare sollecito scritto ai recapiti forniti dal cliente, applicare eventuali costi di custodia previamente comunicati e trattenere il bene fino al pagamento delle somme dovute per prestazioni, conservazione o miglioramento, nei limiti dell'art. 2756 c.c.

Il dispositivo non sarà automaticamente smaltito senza ulteriore comunicazione al cliente. Decorso inutilmente un ulteriore termine dopo sollecito, SAGAM si riserva di procedere secondo la normativa vigente e con modalità proporzionate al valore/stato del bene, anche mediante vendita o smaltimento quando consentito e documentato. Il cliente è invitato a rimuovere o salvare dati personali prima della consegna; SAGAM non risponde della perdita dati se non dovuta a dolo o colpa grave.</textarea></div>
              </div>
            </div>
            <div class="actions"><button class="btn primary" id="btnSaveRip">Salva riparazione</button><button class="btn secondary" id="btnPrintRipReceipt">Stampa ricevuta</button><button class="btn secondary" id="btnClearRip">Pulisci</button></div>
          </div>
        </div>

        <div class="card" style="margin-top:14px"><h3>Riparazioni</h3><div class="tablewrap"><table id="tblRip"><thead><tr><th>ID</th><th>Data</th><th>CF</th><th>Cliente</th><th>Marca</th><th>Modello</th><th>IMEI</th><th>Problema</th><th>Stato</th><th>Costo</th><th>Limite ritiro</th><th>Note</th><th>Azioni</th></tr></thead><tbody></tbody></table></div></div>
      </section>


      <section id="view-report" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card">
          <div class="toolbar"><div><h3>Report avanzati</h3><div class="muted small">Report unificato su clienti, contratti, device, riparazioni e scadenze.</div></div><div class="actions"><button class="btn secondary small" id="btnResetReport">Reset</button><button class="btn primary small" id="btnRunReport">Applica</button><button class="btn secondary small" id="btnExportReport">Export CSV</button></div></div>
          <div class="hr"></div>
          <div class="form-grid">
            <div class="field"><label>Tipo</label><select id="f_tipo"><option value="">Tutti</option><option value="CONTRATTO">Contratti</option><option value="DEVICE">Device</option><option value="RIPARAZIONE">Riparazioni</option></select></div>
            <div class="field"><label>CF</label><input id="f_cf" /></div>
            <div class="field"><label>Nome / Cognome</label><input id="f_nome" /></div>
            <div class="field"><label>Contatto</label><input id="f_contatto" /></div>
            <div class="field"><label>Città</label><input id="f_citta" /></div>
            <div class="field"><label>Compagnia</label><input id="f_compagnia" /></div>
            <div class="field"><label>Offerta</label><input id="f_offerta" /></div>
            <div class="field"><label>Tecnologia</label><input id="f_tecnologia" /></div>
            <div class="field"><label>Stato riparazione</label><input id="f_stato_rip" /></div>
            <div class="field"><label>Venditore</label><input id="f_venditore" /></div>
            <div class="field"><label>Data da</label><input id="f_from" type="date" /></div>
            <div class="field"><label>Data a</label><input id="f_to" type="date" /></div>
          </div>
        </div>
        
        <div class="card" style="margin-top:14px">
          <div class="toolbar">
            <div>
              <h3>Registro modifiche</h3>
              <div class="muted small">Storico locale delle principali azioni effettuate nel CRM.</div>
            </div>
            <div class="actions">
              <button class="btn secondary small" id="btnExportChangeLog">Export registro</button>
              <button class="btn bad small" id="btnClearChangeLog">Svuota registro</button>
            </div>
          </div>
          <div id="changeLogList" class="change-log-list"></div>
        </div>
<div class="grid kpi" style="margin-top:14px">
          <div class="card"><div class="muted small">Righe report</div><div class="value" id="repRows">0</div></div>
          <div class="card"><div class="muted small">€ Device</div><div class="value" id="repDevice">€ 0</div></div>
          <div class="card"><div class="muted small">€ Riparazioni</div><div class="value" id="repRip">€ 0</div></div>
          <div class="card"><div class="muted small">Compleanni 30gg</div><div class="value" id="repBirth">0</div></div>
        </div>
        <div class="grid two" style="margin-top:14px">
          <div class="card"><h3>Distribuzione report</h3><canvas id="chartReport"></canvas></div>
          <div class="card"><h3>Scadenze prossimi 60 giorni</h3><div class="tablewrap"><table id="tblScadenze"><thead><tr><th>Data</th><th>Tipo</th><th>CF</th><th>Cliente</th><th>Compagnia</th><th>Offerta</th></tr></thead><tbody></tbody></table></div></div>
        </div>
        <div class="card" style="margin-top:14px"><h3>Risultati report</h3><div class="tablewrap"><table id="tblReport"><thead><tr><th>Tipo</th><th>Data</th><th>CF</th><th>Cliente</th><th>Contatto</th><th>Città</th><th>Descrizione</th><th>Extra</th></tr></thead><tbody></tbody></table></div></div>
        <div class="card" style="margin-top:14px">
          <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
            <h3 style="margin:0">&#127942; Top Clienti per Punteggio CLV</h3>
            <button class="btn secondary small" onclick="renderTopClienti()">Aggiorna classifica</button>
          </div>
          <div id="topClientiList"><div class="muted small">Clicca "Aggiorna classifica" per vedere i top clienti.</div></div>
        </div>
      </section>


      
<section id="view-automation" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
  <div class="card sales-hero">
    <div class="hero-grid">
      <div class="hero-copy">
        <div class="badge" style="background:rgba(255,255,255,.15);color:#fff;border-color:rgba(255,255,255,.22)">Centrale campagne</div>
        <div class="hero-title">Azioni clienti già divise per lavoro da fare</div>
        <div class="small">Niente più filtri confusi: qui trovi MNP di oggi, follow-up riparazioni, follow-up telefoni, vincoli in scadenza il mese prossimo e una campagna libera guidata.</div>
      </div>
      <div class="hero-stats">
        <div class="hero-stat"><div class="label">MNP oggi</div><div class="num" id="smartCampKpiMnp">0</div></div>
        <div class="hero-stat"><div class="label">Follow-up 7gg</div><div class="num" id="smartCampKpiFollow">0</div></div>
        <div class="hero-stat"><div class="label">Vincoli mese prossimo</div><div class="num" id="smartCampKpiVincoli">0</div></div>
      </div>
    </div>
  </div>

  <div class="grid five" style="display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:10px;margin-top:14px">
    <button class="btn primary smart-camp-tab" data-smart-camp-tab="mnp">MNP di oggi</button>
    <button class="btn secondary smart-camp-tab" data-smart-camp-tab="riparazioni">Riparazioni 7 giorni</button>
    <button class="btn secondary smart-camp-tab" data-smart-camp-tab="device">Telefoni 7 giorni</button>
    <button class="btn secondary smart-camp-tab" data-smart-camp-tab="vincoli">Vincoli mese prossimo</button>
    <button class="btn secondary smart-camp-tab" data-smart-camp-tab="libera">Campagna libera</button>
    <button class="btn secondary smart-camp-tab" data-smart-camp-tab="compleanni">&#127874; Compleanni</button>
  </div>

  <div id="smartCampPanel-mnp" class="smart-camp-panel card" style="margin-top:14px">
    <div class="toolbar">
      <div><h3 style="margin:0">MNP di oggi</h3><div class="muted small">Clienti con portabilità prevista oggi. Apri WhatsApp, controlla che la portabilità sia andata bene e segna lo stato.</div></div>
      <div class="actions"><button class="btn secondary small" data-smart-copy="mnp">Copia numeri</button></div>
    </div>
    <div class="tablewrap" style="margin-top:10px"><table id="tblSmartCampMnp"><thead><tr><th>Data</th><th>Cliente</th><th>Telefono</th><th>Operatore provenienza</th><th>Nuovo operatore</th><th>Offerta</th><th>Stato</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
  </div>

  <div id="smartCampPanel-riparazioni" class="smart-camp-panel card hide" style="margin-top:14px">
    <div class="toolbar">
      <div><h3 style="margin:0">Follow-up riparazioni dopo 7 giorni</h3><div class="muted small">Messaggio per sapere se va tutto bene e chiedere una recensione.</div></div>
      <div class="actions"><button class="btn secondary small" data-smart-copy="repair">Copia numeri</button></div>
    </div>
    <div class="tablewrap" style="margin-top:10px"><table id="tblSmartCampRepair"><thead><tr><th>Data ingresso</th><th>Cliente</th><th>Telefono</th><th>Device</th><th>Problema/Stato</th><th>Giorni</th><th>Stato</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
  </div>

  <div id="smartCampPanel-device" class="smart-camp-panel card hide" style="margin-top:14px">
    <div class="toolbar">
      <div><h3 style="margin:0">Follow-up vendita telefoni dopo 7 giorni</h3><div class="muted small">Messaggio post-vendita per controllo soddisfazione e richiesta recensione.</div></div>
      <div class="actions"><button class="btn secondary small" data-smart-copy="device">Copia numeri</button></div>
    </div>
    <div class="tablewrap" style="margin-top:10px"><table id="tblSmartCampDevice"><thead><tr><th>Data vendita</th><th>Cliente</th><th>Telefono</th><th>Telefono venduto</th><th>Prezzo</th><th>Giorni</th><th>Stato</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
  </div>

  <div id="smartCampPanel-vincoli" class="smart-camp-panel card hide" style="margin-top:14px">
    <div class="toolbar">
      <div><h3 style="margin:0">Fine vincolo del mese successivo</h3><div class="muted small">Clienti con vincolo offerta o telefono che termina nel prossimo mese di calendario.</div></div>
      <div class="actions"><button class="btn secondary small" data-smart-copy="deadline">Copia numeri</button></div>
    </div>
    <div class="tablewrap" style="margin-top:10px"><table id="tblSmartCampVincoli"><thead><tr><th>Scadenza</th><th>Tipo</th><th>Cliente</th><th>Telefono</th><th>Compagnia</th><th>Offerta</th><th>Giorni</th><th>Stato</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
  </div>

  <div id="smartCampPanel-libera" class="smart-camp-panel card hide" style="margin-top:14px">
    <div class="toolbar">
      <div><h3 style="margin:0">Campagna libera avanzata</h3><div class="muted small">Filtra con precisione, scegli il pubblico esatto, personalizza il messaggio.</div></div>
      <div class="actions"><span class="badge">Target: <b id="smartFreeCount" style="margin-left:6px">0</b></span><button class="btn primary" id="btnSmartFreeRun">&#128269; Genera pubblico</button></div>
    </div>
    <div class="hr"></div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:10px 0 6px">&#128100; Cliente</div>
    <div class="form-grid">
      <div class="field"><label>Nome campagna</label><input id="smartFreeTitle" placeholder="Es. Promo WINDTRE" /></div>
      <div class="field"><label>Tipo cliente</label><select id="smartFreeTipo"><option value="">Tutti</option><option>PRIVATO</option><option>BUSINESS</option></select></div>
      <div class="field"><label>Citta</label><input id="smartFreeCitta" placeholder="Es. ROMA" /></div>
      <div class="field"><label>Ricerca libera</label><input id="smartFreeSearch" placeholder="nome, cognome, CF..." /></div>
    </div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:12px 0 6px">&#128196; Contratti</div>
    <div class="form-grid">
      <div class="field"><label>Compagnia attuale</label><input id="smartFreeCompagnia" placeholder="Es. TIM, WINDTRE" /></div>
      <div class="field"><label>Tecnologia</label><select id="smartFreeTecnologia"><option value="">Tutte</option><option>SIM</option><option>FIBRA</option><option>ADSL</option><option>FWA</option></select></div>
      <div class="field"><label>Tipo attivazione</label><select id="smartFreeTipoAtt"><option value="">Tutti</option><option>NUOVA</option><option>MNP</option><option>RINNOVO</option><option>MIGRAZIONE</option></select></div>
      <div class="field"><label>Offerta contiene</label><input id="smartFreeOfferta" placeholder="Es. 5G, FIBRA" /></div>
      <div class="field"><label>Compagnia provenienza MNP</label><input id="smartFreeProvenienzaMnp" placeholder="Es. TIM" /></div>
      <div class="field"><label>Vincolo scade entro (gg)</label><input id="smartFreeVincoloGg" type="number" min="0" placeholder="Es. 60" /></div>
      <div class="field"><label>Vincolo scaduto da almeno (gg)</label><input id="smartFreeVincoloScaduto" type="number" min="0" placeholder="Es. 30" /></div>
      <div class="field"><label>Contratto ultimi (mesi)</label><input id="smartFreeMesi" type="number" min="0" value="12" /></div>
    </div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:12px 0 6px">&#128241; Device</div>
    <div class="form-grid">
      <div class="field"><label>Marca device</label><input id="smartFreeDevMarca" placeholder="Es. APPLE, SAMSUNG" /></div>
      <div class="field"><label>Garanzia scade entro (gg)</label><input id="smartFreeGaranziaGg" type="number" min="0" placeholder="Es. 30" /></div>
      <div class="field"><label>Device acquistato ultimi (mesi)</label><input id="smartFreeDevMesi" type="number" min="0" placeholder="Es. 6" /></div>
    </div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:12px 0 6px">&#128296; Riparazioni</div>
    <div class="form-grid">
      <div class="field"><label>Stato riparazione</label><select id="smartFreeRipStato"><option value="">Tutti</option><option value="APERTA">Aperta</option><option value="PRONTA">Pronta da ritirare</option><option value="CONSEGNATA">Consegnata (follow-up)</option></select></div>
      <div class="field"><label>Riparazione ultimi (mesi)</label><input id="smartFreeRipMesi" type="number" min="0" placeholder="Es. 3" /></div>
    </div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:12px 0 6px">&#9989; Consensi e contatti</div>
    <div class="form-grid">
      <div class="field"><label>Consenso WhatsApp</label><select id="smartFreeConsWa"><option value="">Non filtrare</option><option value="SI">Solo con consenso WA</option><option value="NO">Solo senza consenso WA</option></select></div>
      <div class="field"><label>Consenso marketing</label><select id="smartFreeConsMkt"><option value="">Non filtrare</option><option value="SI">Solo con consenso MKT</option></select></div>
      <div class="field"><label>Non disturbare</label><select id="smartFreeNonDist"><option value="escludi">Escludi non disturbare</option><option value="includi">Includi tutti</option><option value="solo">Solo non disturbare</option></select></div>
      <div class="field"><label>Non contattati negli ultimi (mesi)</label><input id="smartFreeNoContact" type="number" min="0" placeholder="Es. 6 = clienti freddi" /></div>
    </div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:12px 0 6px">&#9881; Opzioni</div>
    <div class="form-grid">
      <div class="field"><label>Sorgente principale</label><select id="smartFreeSource"><option value="all">Tutti i clienti</option><option value="contratti">Solo con contratto</option><option value="device">Solo con device</option><option value="riparazioni">Solo con riparazione</option></select></div>
      <div class="field"><label>Punteggio CLV minimo</label><input id="smartFreeScoreMin" type="number" min="0" placeholder="Es. 15 = solo Argento+" /></div>
      <div class="field"><label>Livello CLV</label><select id="smartFreeScoreLvl"><option value="">Tutti</option><option value="platino">&#128142; Platino (40+)</option><option value="oro">&#127947; Oro (25-39)</option><option value="argento">&#129352; Argento (15-24)</option><option value="bronze">&#129353; Bronze (8-14)</option><option value="base">&#11088; Base (0-7)</option></select></div>
    </div>
    <div class="actions" style="margin-top:10px;flex-wrap:wrap;gap:8px">
      <label class="small muted"><input type="checkbox" id="smartFreePhone" checked /> Solo con telefono</label>
      <label class="small muted"><input type="checkbox" id="smartFreeEmail" /> Solo con email</label>
      <label class="small muted"><input type="checkbox" id="smartFreeUnici" checked /> Clienti unici</label>
    </div>
    <div class="muted small" style="font-weight:700;text-transform:uppercase;letter-spacing:.05em;margin:12px 0 6px">&#128172; Messaggio WhatsApp</div>
    <div class="field"><textarea id="smartFreeTemplate" rows="4" placeholder="Ciao {{nome}}, ti contatto da SAGAM..."></textarea></div>
    <div class="helper" style="margin-top:6px">Variabili: <b>{{nome}}</b>, <b>{{cliente}}</b>, <b>{{compagnia}}</b>, <b>{{tecnologia}}</b>, <b>{{offerta}}</b>, <b>{{citta}}</b>, <b>{{telefono}}</b>, <b>{{scadenza_vincolo}}</b></div>
    <div class="actions" style="margin-top:10px;flex-wrap:wrap;gap:8px">
      <button class="btn secondary small" id="btnSmartFreeCopyNumbers">&#128203; Copia numeri</button>
      <button class="btn secondary small" id="btnSmartFreeExport">&#128190; Export CSV</button>
      <button class="btn secondary small" id="btnSmartFreeRichiamo">&#128276; Crea richiami per tutti</button>
    </div>
    <div class="tablewrap" style="margin-top:10px"><table id="tblSmartFree"><thead><tr><th>Cliente</th><th>Telefono</th><th>Email</th><th>Compagnia</th><th>Info</th><th>Azione</th></tr></thead><tbody></tbody></table></div>
  </div>

  <div class="grid two" style="margin-top:14px">
    <div class="card soft">
      <h3>Template messaggi automatici</h3>
      <div class="muted small">Sono già compilati, ma puoi cambiarli e salvarli.</div>
      <div class="form-grid" style="margin-top:10px">
        <div class="field"><label>MNP</label><textarea id="smartTplMnp"></textarea></div>
        <div class="field"><label>Riparazione 7 giorni</label><textarea id="smartTplRepair"></textarea></div>
        <div class="field"><label>Telefono 7 giorni</label><textarea id="smartTplDevice"></textarea></div>
        <div class="field"><label>Vincolo mese prossimo</label><textarea id="smartTplDeadline"></textarea></div>
      </div>
      <div class="actions" style="margin-top:10px"><button class="btn secondary" id="btnSmartTplSave">Salva template</button><button class="btn secondary" id="btnSmartTplReset">Ripristina default</button></div>
    </div>
    <div class="card soft">
      <div class="toolbar"><div><h3 style="margin:0">Storico contatti campagne</h3><div class="muted small">Ogni WhatsApp o email aperta da qui viene registrata.</div></div><div class="actions"><button class="btn secondary small" id="btnSmartHistClear">Svuota</button></div></div>
      <div class="tablewrap" style="margin-top:10px"><table id="tblSmartCampHistory"><thead><tr><th>Quando</th><th>Tipo</th><th>Cliente</th><th>Canale</th><th>Messaggio</th></tr></thead><tbody></tbody></table></div>
    </div>
  </div>

  <div id="legacyCampaignHidden" class="hide">
    <button id="btnAutoSaveCfg"></button><button id="btnAutoRefresh"></button>
    <input type="checkbox" id="camp_src_contratti" checked><input type="checkbox" id="camp_src_device"><input type="checkbox" id="camp_src_riparazioni">
    <input id="camp_months" value="12"><input type="checkbox" id="camp_only_privati" checked><input type="checkbox" id="camp_only_business"><input type="checkbox" id="camp_only_phone" checked><input type="checkbox" id="camp_only_email">
    <div id="camp_compagnie"></div><div id="camp_tecnologie"></div><div id="camp_attivazioni"></div>
    <input type="checkbox" id="camp_tel_si"><input type="checkbox" id="camp_tel_no"><input type="checkbox" id="camp_mnp_only">
    <input id="camp_compagnia_provenienza"><input id="camp_offerta_contains"><input id="camp_citta"><input id="camp_dev_brand"><input id="camp_venditore"><input id="camp_rip_brand"><input id="camp_rip_stato">
    <div id="campKpiFound"></div><div id="campKpiPhone"></div><div id="campKpiEmail"></div><div id="campKpiUnique"></div>
    <textarea id="camp_message"></textarea><table id="tblCampaignResults"><tbody></tbody></table><div id="campPreviewTitle"></div><div id="campPreviewBox"></div>
    <button id="btnCampCopyNumbers"></button><button id="btnCampExportCsv"></button>
    <div id="smartEnhancer"></div><div id="campaignBuilderBox"></div>
    <table id="tblAutoMnp"><tbody></tbody></table><table id="tblAutoBirth"><tbody></tbody></table><table id="tblAutoDevice"><tbody></tbody></table><table id="tblAutoRepair"><tbody></tbody></table><table id="tblAutoDeadlines"><tbody></tbody></table>
  </div>

  <div id="smartCampPanel-compleanni" class="smart-camp-panel card hide" style="margin-top:14px">
    <div class="toolbar">
      <div>
        <h3 style="margin:0">&#127874; Compleanni del mese</h3>
        <div class="muted small">Clienti con compleanno nel mese selezionato, ordinati per giorno. Un click apre WhatsApp con gli auguri precompilati.</div>
      </div>
      <div class="actions">
        <select id="birthdayMonth" style="padding:6px 10px;border-radius:8px;border:1px solid #e2e8f0;font-size:13px">
          <option value="0">Gennaio</option><option value="1">Febbraio</option><option value="2">Marzo</option>
          <option value="3">Aprile</option><option value="4">Maggio</option><option value="5">Giugno</option>
          <option value="6">Luglio</option><option value="7">Agosto</option><option value="8">Settembre</option>
          <option value="9">Ottobre</option><option value="10">Novembre</option><option value="11">Dicembre</option>
        </select>
        <button class="btn primary small" id="btnCalcBirthdays">Calcola</button>
        <span class="badge">&#127874; <b id="birthdayCount">0</b> questo mese</span>
      </div>
    </div>
    <div class="tablewrap" style="margin-top:10px">
      <table id="tblBirthdays">
        <thead><tr><th>Giorno</th><th>Cliente</th><th>Eta</th><th>Telefono</th><th>Azioni</th></tr></thead>
        <tbody></tbody>
      </table>
    </div>
  </div>
</section>


      <section id="view-timeline" class="view">
      <button class="btn secondary small" onclick="showView('scheda')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Scheda cliente</button>
        <div class="card">
          <div class="toolbar"><div><h3>Timeline cliente</h3><div class="muted small">Stile gestionale: contratti, vendite e riparazioni in ordine cronologico.</div></div><div class="actions"><input id="t_cf" placeholder="Codice fiscale" /><button class="btn primary" id="btnTimeline">Carica timeline</button></div></div>
        </div>
        <div class="card" style="margin-top:14px"><div id="timelineHeader" class="muted">Nessun cliente selezionato.</div><div id="timelineBox" class="timeline" style="margin-top:12px"></div></div>
      </section>

      <section id="view-importexport" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card">
          <h3>Importazione dati</h3>
          <div class="muted small">Importa dati da file CSV o da testo strutturato. Il sistema riconosce le intestazioni principali e prepara l'archivio operativo.</div>
          <div class="grid two" style="margin-top:14px">
            <div class="card soft"><h3>Import file</h3><div class="form-grid"><div class="field"><label>Anagrafica CSV</label><input id="fileAnag" type="file" accept=".csv" /></div><div class="field"><label>Contratti CSV</label><input id="fileCon" type="file" accept=".csv" /></div><div class="field"><label>Device CSV</label><input id="fileDev" type="file" accept=".csv" /></div><div class="field"><label>Riparazioni CSV</label><input id="fileRip" type="file" accept=".csv" /></div></div><div class="actions" style="margin-top:12px"><button class="btn good" id="btnImportCombo">Import unico Anagrafica + Contratti</button><button class="btn primary" id="btnImportAnag">Import Anagrafica</button><button class="btn primary" id="btnImportCon">Import Contratti</button><button class="btn primary" id="btnImportDev">Import Device</button><button class="btn primary" id="btnImportRip">Import Riparazioni</button></div></div>
            <div class="card soft"><h3>Import da testo strutturato</h3><div class="field"><label>Tipo import singolo</label><select id="pasteType"><option value="anagrafica">Anagrafica</option><option value="contratti">Contratti</option><option value="device">Device</option><option value="magazzino">Magazzino</option><option value="riparazioni">Riparazioni</option></select></div><div class="field"><label>Dati incollati</label><textarea id="pasteRaw" placeholder="Incolla qui da Excel o Google Sheets"></textarea></div><div class="actions"><button class="btn secondary" id="btnPreviewPaste">Anteprima</button><button class="btn primary" id="btnRunPaste">Importa</button></div><div class="hr"></div><h3>Import guidato da testo libero</h3><div class="muted small">Incolla un blocco completo con dati cliente, contratto, offerta, portabilità, dispositivo, pagamento e note. Il CRM prepara automaticamente cliente e pratica commerciale.</div><div class="field" style="margin-top:10px"><label>Testo completo pratica</label><textarea id="pasteRawCombined" placeholder="Incolla qui l'intera pratica in formato testo libero" style="min-height:320px"></textarea></div><div class="actions"><button class="btn secondary" id="btnPreviewPasteCombined">Analizza testo</button><button class="btn primary" id="btnRunPasteCombined">Import rapido</button></div><div class="hr"></div><div id="combinedEditor" class="hide"><h3>Pratica importata da testo</h3><div class="muted small">Qui puoi correggere tutti i campi prima di salvare. Dopo il salvataggio puoi stampare la ricevuta completa.</div><div class="grid two" style="margin-top:12px"><div class="card"><h3>Cliente</h3><div class="form-grid"><div class="field"><label>Codice fiscale</label><input id="ce_cf" /></div><div class="field"><label>Nome</label><input id="ce_nome" /></div><div class="field"><label>Cognome</label><input id="ce_cognome" /></div><div class="field"><label>Tipo cliente</label><select id="ce_tipo"><option>PRIVATO</option><option>BUSINESS</option></select></div><div class="field"><label>Telefono</label><input id="ce_telefono" /></div><div class="field"><label>Email</label><input id="ce_email" /></div><div class="field"><label>Città</label><input id="ce_citta" /></div><div class="field"><label>Indirizzo</label><input id="ce_indirizzo" /></div><div class="field"><label>Data nascita</label><input id="ce_data_nascita" type="date" /></div></div></div><div class="card"><h3>Contratto</h3><div class="form-grid"><div class="field"><label>ID contratto</label><input id="xe_id" /></div><div class="field"><label>Data contratto</label><input id="xe_data_contratto" type="date" /></div><div class="field"><label>Compagnia</label><input id="xe_compagnia" /></div><div class="field"><label>Tecnologia</label><select id="xe_tecnologia"><option value="">—</option><option>SIM</option><option>FIBRA</option><option>FWA</option><option>ADSL</option><option>TV</option></select></div><div class="field"><label>Tipo attivazione</label><select id="xe_tipo_attivazione"><option value="">—</option><option>NUOVA</option><option>MNP</option><option>MIGRAZIONE</option><option>SUBENTRO</option><option>VARIAZIONE</option></select></div><div class="field"><label>Numero lavorato</label><input id="xe_numero_lavorato" /></div><div class="field"><label>Nome offerta</label><input id="xe_nome_offerta" /></div><div class="field"><label>Costo offerta (€)</label><input id="xe_costo_offerta" /></div><div class="field"><label>Tipo pagamento</label><select id="xe_tipo_pagamento"><option value="">—</option><option>SDD</option><option>CARTA DI CREDITO</option><option>CREDITO RESIDUO</option></select></div><div class="field"><label>MNP</label><select id="xe_mnp"><option value="">—</option><option>SI</option><option>NO</option></select></div><div class="field"><label>ICCID vecchio</label><input id="xe_iccid_vecchio" /></div><div class="field"><label>ICCID nuovo</label><input id="xe_iccid_nuovo" /></div><div class="field"><label>Data portabilità</label><input id="xe_data_portabilita" type="date" /></div><div class="field"><label>IMEI</label><input id="xe_imei" /></div><div class="field"><label>Modello telefono</label><input id="xe_modello" /></div><div class="field"><label>IBAN</label><input id="xe_iban" /></div><div class="field" style="grid-column:1/-1"><label>Note</label><textarea id="xe_note"></textarea></div></div></div></div><div class="actions" style="margin-top:12px"><button class="btn secondary" id="btnLoadCombinedToForms">Carica nei form</button><button class="btn primary" id="btnSaveCombinedEdited">Salva pratica</button><button class="btn secondary" id="btnPrintCombinedReceipt">Stampa ricevuta</button></div></div></div>
          </div>
        </div>
        <div class="card" style="margin-top:14px"><h3>Anteprima import testo</h3><div class="tablewrap"><table id="tblPastePreview"><thead></thead><tbody></tbody></table></div></div>
        <div class="card" style="margin-top:14px"><h3>Export</h3><div class="actions"><button class="btn secondary" data-export="anagrafica">Export Anagrafica</button><button class="btn secondary" data-export="contratti">Export Contratti</button><button class="btn secondary" data-export="device">Export Device</button><button class="btn secondary" data-export="magazzino">Export Magazzino</button><button class="btn secondary" data-export="riparazioni">Export Riparazioni</button><button class="btn secondary" id="btnExportAll">Export completo JSON</button></div></div>
      </section>

      <section id="view-settings" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card">
          <h3>Google Sheets / Apps Script</h3>
          <div class="muted small">Qui colleghi il CRM a una Web App di Google Apps Script. Il frontend è già pronto: basta inserire URL e nomi fogli.</div>
          <div class="hr"></div>
          <div class="form-grid">
            <div class="field" style="grid-column:1/-1"><label>Endpoint Web App *</label><input id="gs_endpoint" value="https://script.google.com/macros/s/AKfycbyz3UntLU4-jw9ioP6B02vKQMQWlPoFXi4xSW-kxs1jOsUKCvSiDv4PZZFSYcNomSJ_/exec" /></div>
            <div class="field"><label>Foglio Anagrafica</label><input id="gs_sheet_anagrafica" value="ANAGRAFICHE" /></div>
            <div class="field"><label>Foglio Contratti</label><input id="gs_sheet_contratti" value="CONTRATTI" /></div>
            <div class="field"><label>Foglio Device</label><input id="gs_sheet_device" value="DEVICE" /></div>
            <div class="field"><label>Foglio Magazzino</label><input id="gs_sheet_magazzino" value="MAGAZZINO" /></div>
            <div class="field"><label>Foglio Riparazioni</label><input id="gs_sheet_riparazioni" value="RIPARAZIONI" /></div>
            <div class="field"><label><input id="gs_auto_sync" type="checkbox" style="width:auto;margin-right:6px" /> Sync automatico dopo ogni salvataggio</label><div class="muted small">Consiglio: tienilo disattivato durante gli inserimenti veloci e usa CRM → Google a fine lavoro.</div></div>
          </div>
          <div class="actions" style="margin-top:12px">
            <button class="btn primary" id="btnSaveGs">Salva impostazioni</button>
            <button class="btn secondary" id="btnGsPing" onclick="gsPing()">Test collegamento</button>
            <button class="btn secondary" id="btnGsDown" onclick="gsPullAll(true)">Google → CRM</button>
            <button class="btn primary" id="btnGsUp" onclick="gsPushAll(true)">CRM → Google</button>
            <button class="btn secondary" id="btnGsImportJson">Importa archivio dati</button>
            <button class="btn secondary" id="btnRestoreSafetySnapshot" onclick="sagamRestoreLastGoodSnapshot()">Ripristina dati sicuri</button>
          </div>
          
          <div class="card soft gs-import-panel" style="margin-top:14px">
            <div class="toolbar">
              <div>
                <h3>Importa archivio dati</h3>
                <div class="muted small">Carica un archivio CRM in formato JSON per recuperare dati da backup, migrare da una versione precedente o ripristinare uno storico autorizzato.</div>
              </div>
              
              <div class="actions" style="align-items:end">
                <div class="field" style="min-width:240px;margin:0">
                  <label>Modalità import</label>
                  <select id="gsArchiveImportMode">
                    <option value="replace" selected>Sostituisci archivio attuale</option>
                    <option value="merge">Aggiungi / aggiorna dati</option>
                  </select>
                </div>
                <button class="btn secondary" id="btnGsImportJsonPanel">Seleziona file JSON</button>
              </div>
        
            </div>
            <div class="helper" style="margin-top:12px">
              Prima dell'import viene creato automaticamente un backup di sicurezza. Dopo l'import controlla i dati e usa <b>CRM → Google</b> per sincronizzare il foglio.
            </div>
          </div>

          <div class="helper" style="margin-top:14px">Protocollo collegato a questa Web App: <span class="mono">GET action=ping</span>, <span class="mono">GET action=list</span>, <span class="mono">POST action=pushAll</span>. La sincronizzazione CRM → Google usa un invio ottimizzato. Da qui puoi anche importare un backup JSON del vecchio CRM.</div>
        </div>
      </section>



      <section id="view-scheda" class="view">
        <div style="margin-bottom:10px">
          <button class="btn secondary small" onclick="showView('anagrafica')" style="display:inline-flex;align-items:center;gap:6px">← Tutti i clienti</button>
        </div>
        <div class="card smart-hero">
          <div class="toolbar">
            <div>
              <h3>🧾 Scheda cliente unica</h3>
              <div class="small">Cerca un cliente e lavora da una sola schermata: anagrafica, attività, post-it, contatti, richiami e documenti.</div>
            </div>
            <div class="actions smart-no-print">
              <input id="sc_search" placeholder="Cerca CF, nome, telefono o email" style="min-width:300px" />
              <button class="btn secondary" id="btnScSearch">Cerca</button>
            </div>
          </div>
        </div>
        <div class="grid two" style="margin-top:14px">
          <div class="card">
            <h3>Risultati ricerca</h3>
            <div class="tablewrap"><table id="tblScResults"><thead><tr><th>Cliente</th><th>CF</th><th>Contatti</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
          </div>
          <div class="card" id="scSummary">
            <div class="muted">Nessun cliente selezionato.</div>
          </div>
        </div>
        <div id="scDetail" class="hide" style="margin-top:14px">
          <div class="card">
            <div class="smart-tabs smart-no-print">
              <button class="smart-tab active" data-smart-tab="sc-overview">Panoramica</button>
              <button class="smart-tab" data-smart-tab="sc-attivita">Attività</button>
              <button class="smart-tab" data-smart-tab="sc-contatti">Contatti</button>
              <button class="smart-tab" data-smart-tab="sc-richiami">Richiami</button>
              <button class="smart-tab" data-smart-tab="sc-documenti">Documenti</button>
            </div>
            <div id="sc-overview" class="smart-panel active"></div>
            <div id="sc-attivita" class="smart-panel"></div>
            <div id="sc-contatti" class="smart-panel"></div>
            <div id="sc-richiami" class="smart-panel"></div>
            <div id="sc-documenti" class="smart-panel"></div>
          </div>
        </div>
      </section>

      <section id="view-contatti" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card smart-hero">
          <div class="toolbar">
            <div>
              <h3>☎️ Registro contatti</h3>
              <div class="small">Storico di telefonate, WhatsApp, email, campagne, recensioni e richiami. Ogni contatto può generare un richiamo futuro.</div>
            </div>
            <div class="actions smart-no-print">
              <input id="ct_search" placeholder="Cerca cliente, CF, esito, motivo" style="min-width:300px" />
              <button class="btn secondary" id="btnCtSearch">Cerca</button>
            </div>
          </div>
        </div>
        <div class="grid two" style="margin-top:14px">
          <div class="card">
            <h3>Nuovo contatto</h3>
            <div class="form-grid">
              <div class="field"><label>Codice fiscale cliente</label><input id="ct_cf" placeholder="CF" /></div>
              <div class="field"><label>Tipo contatto</label><select id="ct_tipo"><option>WHATSAPP</option><option>TELEFONATA</option><option>EMAIL</option><option>CAMPAGNA</option><option>NEGOZIO</option></select></div>
              <div class="field"><label>Motivo</label><select id="ct_motivo"><option>MNP</option><option>RIPARAZIONE</option><option>VENDITA TELEFONO</option><option>FINE VINCOLO</option><option>RECENSIONE</option><option>INFO</option><option>ALTRO</option></select></div>
              <div class="field"><label>Esito</label><select id="ct_esito"><option>CONTATTATO</option><option>DA_RICHIAMARE</option><option>NON_RISPONDE</option><option>INTERESSATO</option><option>NON_INTERESSATO</option><option>RECENSIONE_RICHIESTA</option></select></div>
              <div class="field"><label>Data richiamo opzionale</label><input id="ct_richiamo" type="date" /></div>
              <div class="field" style="grid-column:1/-1"><label>Messaggio / note</label><textarea id="ct_note" placeholder="Scrivi cosa è stato detto o il testo inviato"></textarea></div>
            </div>
            <div class="actions" style="margin-top:12px">
              <button class="btn primary" id="btnCtSave">Salva contatto</button>
              <button class="btn secondary" id="btnCtClear">Pulisci</button>
            </div>
          </div>
          <div class="card">
            <h3>Statistiche contatti</h3>
            <div class="smart-mini-grid" id="ctStats"></div>
            <div class="smart-note" style="margin-top:12px">Consiglio: quando una campagna produce un cliente interessato, salva sempre anche la data richiamo. Così non si perde più nessuna opportunità.</div>
          </div>
        </div>
        <div class="card" style="margin-top:14px">
          <div class="toolbar"><h3>Storico contatti</h3><button class="btn secondary small" id="btnCtExport">Export CSV</button></div>
          <div class="tablewrap"><table id="tblContatti"><thead><tr><th>Data</th><th>Cliente</th><th>Tipo</th><th>Motivo</th><th>Esito</th><th>Note</th><th>Richiamo</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>
      </section>

      <section id="view-richiami" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card smart-hero">
          <div class="toolbar">
            <div>
              <h3>🔔 Agenda richiami</h3>
              <div class="small">Clienti da ricontattare oggi, in ritardo o nei prossimi giorni.</div>
            </div>
            <div class="actions smart-no-print">
              <input id="rc_search" placeholder="Cerca richiamo" style="min-width:280px" />
              <button class="btn secondary" id="btnRcSearch">Cerca</button>
            </div>
          </div>
        </div>
        <div class="grid kpi" style="margin-top:14px">
          <div class="card"><div class="muted small">In ritardo</div><div class="value" id="rcOverdue">0</div></div>
          <div class="card"><div class="muted small">Oggi</div><div class="value" id="rcToday">0</div></div>
          <div class="card"><div class="muted small">Prossimi 7 giorni</div><div class="value" id="rcWeek">0</div></div>
          <div class="card"><div class="muted small">Completati</div><div class="value" id="rcDone">0</div></div>
        </div>
        <div class="grid two" style="margin-top:14px">
          <div class="card">
            <h3>Nuovo richiamo</h3>
            <div class="form-grid">
              <div class="field"><label>CF cliente</label><input id="rc_cf" /></div>
              <div class="field"><label>Data richiamo</label><input id="rc_data" type="date" /></div>
              <div class="field"><label>Motivo</label><select id="rc_motivo"><option>FINE VINCOLO</option><option>RIPARAZIONE</option><option>VENDITA TELEFONO</option><option>MNP</option><option>PREVENTIVO</option><option>ALTRO</option></select></div>
              <div class="field"><label>Priorità</label><select id="rc_priorita"><option>NORMALE</option><option>ALTA</option><option>BASSA</option></select></div>
              <div class="field" style="grid-column:1/-1"><label>Note</label><textarea id="rc_note"></textarea></div>
            </div>
            <div class="actions" style="margin-top:12px"><button class="btn primary" id="btnRcSave">Salva richiamo</button><button class="btn secondary" id="btnRcClear">Pulisci</button></div>
          </div>
          <div class="card">
            <h3>Richiami di oggi</h3>
            <div id="rcTodayBox"></div>
          </div>
        </div>
        <div class="card" style="margin-top:14px">
          <h3>Tutti i richiami</h3>
          <div class="tablewrap"><table id="tblRichiami"><thead><tr><th>Data</th><th>Cliente</th><th>Motivo</th><th>Priorità</th><th>Stato</th><th>Note</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>
      </section>

      <section id="view-consensi" class="view">
      <button class="btn secondary small" onclick="showView('anagrafica')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Anagrafica</button>
        <div class="card smart-hero">
          <div class="toolbar">
            <div>
              <h3>✅ Consensi e privacy</h3>
              <div class="small">Gestisci chi può essere contattato per campagne, WhatsApp, email e chi va escluso.</div>
            </div>
            <div class="actions smart-no-print">
              <input id="cs_search" placeholder="Cerca cliente" style="min-width:300px" />
              <button class="btn secondary" id="btnCsSearch">Cerca</button>
            </div>
          </div>
        </div>
        <div class="card" style="margin-top:14px">
          <div class="smart-warn"><b>Regola operativa:</b> nelle campagne contatta solo chi ha consenso marketing o una motivazione di servizio. Usa “Non disturbare” per escludere sempre il cliente.</div>
          <div class="tablewrap"><table id="tblConsensi"><thead><tr><th>Cliente</th><th>CF</th><th>Marketing</th><th>WhatsApp</th><th>Email</th><th>Non disturbare</th><th>Ultimo consenso</th><th>Note privacy</th><th>Azioni</th></tr></thead><tbody></tbody></table></div>
        </div>
      </section>

      <section id="view-documenti" class="view">
      <button class="btn secondary small" onclick="showView('anagrafica')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Anagrafica</button>
        <div class="card smart-hero">
          <div class="toolbar">
            <div>
              <h3>🖨 Documenti</h3>
              <div class="small">Genera testi stampabili per ricevute, riepiloghi cliente, presa in carico e consenso privacy.</div>
            </div>
            <div class="actions smart-no-print">
              <input id="dc_cf" placeholder="Codice fiscale cliente" style="min-width:260px" />
              <select id="dc_tipo" style="max-width:240px">
                <option value="scheda">Scheda riepilogo cliente</option>
                <option value="privacy">Modulo consenso privacy</option>
                <option value="riparazione">Modulo presa in carico riparazione</option>
                <option value="device">Ricevuta vendita device</option>
                <option value="contratto">Riepilogo contratto</option>
              </select>
              <button class="btn secondary" id="btnDcGenerate">Genera</button>
              <button class="btn primary" id="btnDcPrint">Stampa</button>
            </div>
          </div>
        </div>
        <div class="card" style="margin-top:14px">
          <div class="doc-preview" id="dcPreview">Inserisci un codice fiscale e scegli un documento.</div>
        </div>
      </section>

      <section id="view-news" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
        <div class="card">
          <div class="toolbar">
            <div>
              <h3>News telefonia</h3>
              <div class="muted small">Area rapida per restare aggiornato su offerte, operatori, MVNO, fibra e novità del settore.</div>
            </div>
            <div class="actions">
              <a class="btn secondary" href="https://www.mondomobileweb.it/" target="_blank" rel="noopener">Apri Mondomobileweb</a>
            </div>
          </div>
          <div class="helper" style="margin-top:14px">Provo a caricare qui dentro Mondomobileweb. Se il sito blocca la visualizzazione interna per motivi di sicurezza del browser, usa il pulsante qui sopra per aprirlo fuori dal gestionale.</div>
          <iframe class="news-frame" src="https://www.mondomobileweb.it/" title="Mondomobileweb"></iframe>
        </div>
      </section>

    </div>
  

<section id="view-lucegas" class="view">
      <button class="btn secondary small" onclick="showView('dashboard')" style="display:inline-flex;align-items:center;gap:6px;margin-bottom:10px">← Dashboard</button>
  <div class="card module-hero">
    <div class="toolbar">
      <div>
        <div class="section-label">⚡ Energia e utility</div>
        <h3 style="margin-top:10px">Contratti Luce e Gas</h3>
        <div class="lead">Gestisci contratti energia in modo guidato: cliente, POD/PDR, fornitore, documenti ricevuti, stato pratica e attivazione.</div>
      </div>
      <div class="module-actions">
        <input id="lg_search" placeholder="Cerca pratica energia" style="min-width:260px" />
        <button class="btn secondary" id="btnLgPrint">Stampa riepilogo</button>
        <button class="btn secondary" id="btnLgExport">Export CSV</button>
        <button class="btn good" id="btnLgClear">Nuovo</button>
      </div>
    </div>
    <div class="module-statbar">
      <div class="module-stat"><div class="k">Focus</div><div class="v">Cliente → Fornitura</div></div>
      <div class="module-stat"><div class="k">Flusso</div><div class="v">Anagrafica + Luce/Gas</div></div>
      <div class="module-stat"><div class="k">Consiglio</div><div class="v">Controlla POD / PDR e documenti</div></div>
    </div>
  </div>

  <div class="grid3" style="margin-top:14px">
    <div class="card soft">
      <div class="muted small">Pratiche energia</div>
      <div class="value" id="lgKpiTot">0</div>
      <div class="small muted">Totale archivio Luce/Gas</div>
    </div>
    <div class="card soft">
      <div class="muted small">In lavorazione</div>
      <div class="value" id="lgKpiWork">0</div>
