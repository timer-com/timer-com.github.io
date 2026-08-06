<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Республика «Team» / Советская империя</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin:0; padding:0; box-sizing:border-box; }
        body {
            font-family: 'Segoe UI', Roboto, sans-serif;
            min-height:100vh;
            background:#0b0d11;
            display:flex;
            justify-content:center;
            align-items:center;
            padding:20px;
        }
        .switch-container {
            position:fixed; top:20px; right:20px; z-index:9999;
            display:flex; gap:10px; flex-wrap:wrap; justify-content:flex-end;
        }
        .switch-btn {
            padding:0.6rem 1.4rem; border-radius:40px; border:2px solid #d4af37;
            background:rgba(0,0,0,0.7); backdrop-filter:blur(8px);
            color:#f5e7d3; font-size:0.9rem; font-weight:600; cursor:pointer;
            transition:0.3s; font-family:'Segoe UI',sans-serif;
            box-shadow:0 4px 20px rgba(0,0,0,0.5);
        }
        .switch-btn:hover { background:#d4af37; color:#1a1a1a; transform:scale(1.05); }
        .switch-btn.active { background:#d4af37; color:#1a1a1a; border-color:#f5e7d3; }

        .site-container {
            display:none; width:100%; max-width:1300px;
            animation:fadeIn 0.4s ease;
        }
        .site-container.active { display:block; }
        @keyframes fadeIn { from { opacity:0; transform:scale(0.97); } to { opacity:1; transform:scale(1); } }

        /* ===== СТИЛИ ДЛЯ САЙТА РЕСПУБЛИКИ TEAM ===== */
        .team-wrapper {
            background: radial-gradient(circle at 20% 30%, #141a24, #07090e 80%);
            min-height: 100vh; border-radius: 2rem; padding: 2rem 2rem 1rem;
            box-shadow: 0 0 40px rgba(0, 20, 40, 0.6);
        }
        .team-header {
            display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap;
            padding-bottom: 1.5rem; border-bottom: 1px solid #2a354a; margin-bottom: 2.5rem;
        }
        .team-logo { display: flex; align-items: center; gap: 0.75rem; }
        .team-logo i { font-size: 2.4rem; color: #64f0b0; filter: drop-shadow(0 0 6px #3ad68a); }
        .team-logo span { font-weight: 700; font-size: 2rem; background: linear-gradient(135deg, #c0e6ff, #6ec8ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .team-logo span small { font-weight: 300; color: #b0c9e8; -webkit-text-fill-color: #b0c9e8; background: none; }
        .team-nav { display: flex; gap: 1.8rem; align-items: center; flex-wrap: wrap; }
        .team-nav button {
            background: none; border: none; color: #b6cae5; font-weight: 500; font-size: 1.1rem; cursor: pointer;
            border-bottom: 2px solid transparent; padding-bottom: 4px; transition: 0.2s; font-family: inherit;
        }
        .team-nav button:hover { color: #b3f0d0; border-bottom-color: #52d79a; }
        .team-nav button.active { color: #b3f0d0; border-bottom-color: #52d79a; }
        .team-content { color: #eef2f6; }
        .team-content h2 { font-size: 2.2rem; margin: 2rem 0 1.5rem; display: flex; align-items: center; gap: 12px; color: #d4ebff; }
        .team-content h2 i { color: #55dba0; }
        .team-content p { color: #b6cae5; line-height: 1.8; font-size: 1.05rem; }
        .team-departments {
            display: flex; flex-wrap: wrap; gap: 1.5rem 2.5rem;
            background: rgba(12, 24, 38, 0.5); backdrop-filter: blur(4px);
            padding: 1.2rem 2rem; border-radius: 60px; border: 1px solid #2a4058;
            margin-bottom: 2.5rem; justify-content: center;
        }
        .team-dept { display: flex; align-items: center; gap: 10px; color: #c6defa; font-size: 1.1rem; font-weight: 500; }
        .team-dept i { color: #59dba6; font-size: 1.3rem; width: 1.6rem; text-align: center; }
        .team-dept .divider { color: #3a5a6a; margin-left: 0.2rem; }
        .team-codex {
            background: #0d1a26; border-radius: 40px; padding: 2rem 2.5rem;
            margin: 2rem 0; border-left: 6px solid #f0c060;
            box-shadow: 0 0 20px rgba(240, 192, 96, 0.08);
        }
        .team-codex h3 { font-size: 1.8rem; color: #f5e3c0; display: flex; align-items: center; gap: 12px; margin-bottom: 1.2rem; }
        .team-codex h3 i { color: #f0c060; }
        .team-article { margin-bottom: 1.5rem; padding-left: 0.5rem; }
        .team-article .art-title { font-size: 1.2rem; font-weight: 600; color: #f0dba0; display: flex; align-items: center; gap: 8px; }
        .team-article .art-title i { color: #f0b84d; }
        .team-article .art-text { color: #d0def0; padding-left: 1.8rem; margin-bottom: 0.5rem; border-left: 2px solid #3a5f6b; }
        .team-article .art-sub { padding-left: 2.5rem; color: #b9ceea; font-size: 0.98rem; }
        .team-article .art-sub i { color: #f0b84d; width: 1.4rem; }
        .team-section { display: none; }
        .team-section.active { display: block; }

        /* ===== МАГАЗИН ===== */
        .shop-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1.5rem; margin-top: 1.5rem;
        }
        .shop-item {
            background: rgba(18, 30, 44, 0.7); border-radius: 24px; padding: 1.5rem;
            border: 1px solid #2b4058; transition: 0.2s; text-align: center;
        }
        .shop-item:hover { border-color: #56dba7; transform: translateY(-4px); box-shadow: 0 8px 20px rgba(0,0,0,0.4); }
        .shop-item .item-icon { font-size: 2.5rem; color: #59dba6; margin-bottom: 0.5rem; }
        .shop-item .item-name { font-size: 1.1rem; font-weight: 600; color: #d4ebff; }
        .shop-item .item-price { color: #f0c060; font-weight: 600; margin: 0.3rem 0 0.8rem; }
        .shop-item .item-price i { color: #f0c060; margin-right: 4px; }
        .shop-item .item-desc { font-size: 0.8rem; color: #8eb3d4; margin: 0.3rem 0 0.6rem; line-height: 1.3; }
        .shop-item .btn-buy {
            padding: 0.5rem 1.5rem; border-radius: 40px; border: none;
            background: linear-gradient(145deg, #2cdf8a, #1db06e);
            color: #0b141c; font-weight: 600; cursor: pointer; transition: 0.2s;
            font-size: 0.95rem;
        }
        .shop-item .btn-buy:hover { transform: scale(1.05); box-shadow: 0 0 20px #24d17e66; }
        .shop-item .btn-buy:disabled { opacity: 0.4; cursor: not-allowed; transform: none; box-shadow: none; }
        .shop-item .item-owned { color: #59dba6; font-size: 0.9rem; margin-top: 0.3rem; }
        .shop-item .item-owned i { margin-right: 4px; }

        /* ===== БИБЛИОТЕКА ===== */
        .library-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1.5rem; margin-top: 1.5rem;
        }
        .library-item {
            background: rgba(18, 30, 44, 0.7); border-radius: 24px; padding: 1.5rem;
            border: 1px solid #2b4058; transition: 0.2s; text-align: center; cursor: pointer;
        }
        .library-item:hover { border-color: #6ec8ff; transform: translateY(-4px); box-shadow: 0 8px 20px rgba(0,0,0,0.4); }
        .library-item .item-icon { font-size: 2.5rem; color: #6ec8ff; margin-bottom: 0.5rem; }
        .library-item .item-name { font-size: 1.1rem; font-weight: 600; color: #d4ebff; }
        .library-item .item-price { color: #f0c060; font-weight: 600; margin: 0.3rem 0 0.5rem; }
        .library-item .item-desc { font-size: 0.85rem; color: #8eb3d4; margin: 0.3rem 0 0.6rem; line-height: 1.3; }
        .library-item .btn-buy {
            padding: 0.5rem 1.5rem; border-radius: 40px; border: none;
            background: linear-gradient(145deg, #2cdf8a, #1db06e);
            color: #0b141c; font-weight: 600; cursor: pointer; transition: 0.2s;
            font-size: 0.95rem;
        }
        .library-item .btn-buy:hover { transform: scale(1.05); box-shadow: 0 0 20px #24d17e66; }
        .library-item .btn-buy:disabled { opacity: 0.4; cursor: not-allowed; transform: none; box-shadow: none; }
        .library-item .item-owned { color: #59dba6; font-size: 0.9rem; margin-top: 0.3rem; }
        .library-item .item-owned i { margin-right: 4px; }
        .library-item .btn-read {
            padding: 0.5rem 1.5rem; border-radius: 40px; border: none;
            background: linear-gradient(145deg, #6ec8ff, #4a9fd8);
            color: #0b141c; font-weight: 600; cursor: pointer; transition: 0.2s;
            font-size: 0.95rem;
        }
        .library-item .btn-read:hover { transform: scale(1.05); box-shadow: 0 0 20px #4a9fd866; }

        /* ===== ФИНАНСЫ TEAM ===== */
        .team-bank {
            background: rgba(12, 24, 38, 0.7); backdrop-filter: blur(4px);
            border-radius: 32px; padding: 2rem 2.5rem;
            border: 1px solid #2d4560;
            max-width: 500px; margin: 2rem 0 1rem;
            border-left: 6px solid #f0c060;
        }
        .team-bank .balance {
            font-size: 2.8rem; font-weight: 700;
            background: linear-gradient(135deg, #f5e3c0, #f0c060);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            margin: 0.5rem 0 0.3rem;
        }
        .team-bank .balance.infinity {
            background: linear-gradient(135deg, #ffd700, #ff6b00);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-size: 3.2rem;
        }

        /* ===== ПАСПОРТ TEAM ===== */
        .team-passport {
            background: rgba(12, 24, 38, 0.7); backdrop-filter: blur(4px);
            border-radius: 32px; padding: 2rem 1.8rem;
            border: 1px solid #2d4560;
            max-width: 480px; margin: 2rem 0 1rem;
        }
        .team-passport ul { list-style: none; }
        .team-passport ul li { padding: 0.5rem 0; border-bottom: 1px solid #1f344a; color: #bdd6f0; display: flex; align-items: center; gap: 10px; }
        .team-passport ul li i { color: #51d49b; width: 1.4rem; }
        .team-passport-id {
            background: #0a1a28; border-radius: 20px; padding: 0.8rem 1.2rem; margin-top: 1rem;
            border: 1px solid #2f6880; display: flex; align-items: center; gap: 1rem;
        }
        .team-passport-id i { font-size: 2rem; color: #6ad4a8; }
        .team-passport-id .id-number { font-family: 'Courier New', monospace; letter-spacing: 2px; font-size: 1.2rem; color: #b3f0d0; }

        /* ===== ЛИЧНЫЙ КАБИНЕТ TEAM ===== */
        .team-login-form {
            background: rgba(12, 24, 38, 0.7); backdrop-filter: blur(4px);
            border-radius: 32px; padding: 2rem 2.5rem;
            border: 1px solid #2d4560;
            max-width: 400px; margin: 2rem 0;
        }
        .team-login-form label { display: block; color: #b6ceea; margin-bottom: 0.3rem; font-weight: 500; }
        .team-login-form input {
            width: 100%; padding: 0.8rem 1rem; border-radius: 16px;
            border: 1px solid #2f4a66; background: #0b1a28; color: #eef2f6;
            font-size: 1rem; margin-bottom: 1rem; outline: none;
        }
        .team-login-form input:focus { border-color: #56dba7; box-shadow: 0 0 12px #2fbb7e44; }
        .team-login-form .btn-login-submit {
            width: 100%; padding: 0.9rem; border: none; border-radius: 40px;
            background: linear-gradient(145deg, #2cdf8a, #1db06e);
            color: #0b141c; font-weight: 700; font-size: 1.1rem; cursor: pointer;
            box-shadow: 0 0 20px #24d17e44; transition: 0.2s;
        }
        .team-login-form .btn-login-submit:hover { transform: scale(1.02); box-shadow: 0 0 32px #2bff9a66; }
        .team-login-form .error { color: #ff7a7a; font-size: 0.9rem; margin: -0.3rem 0 0.8rem 0; display: none; }
        .team-login-form .error.show { display: block; }
        .team-login-form .user-info { color: #59dba6; font-size: 1.1rem; margin-bottom: 1rem; }
        .team-login-form .logout-btn {
            padding: 0.5rem 1.5rem; border-radius: 40px; border: none;
            background: #ff5a5a; color: #fff; font-weight: 600; cursor: pointer;
            transition: 0.2s; font-size: 1rem;
        }
        .team-login-form .logout-btn:hover { transform: scale(1.05); box-shadow: 0 0 20px #ff5a5a66; }

        /* ===== НАСТРОЙКИ СИНХРОНИЗАЦИИ ===== */
        .sync-settings {
            background: rgba(12, 24, 38, 0.7); backdrop-filter: blur(4px);
            border-radius: 32px; padding: 2rem 2.5rem;
            border: 1px solid #2d4560;
            max-width: 500px; margin: 2rem 0;
            border-left: 6px solid #6ec8ff;
        }
        .sync-settings label { display: block; color: #b6ceea; margin-bottom: 0.3rem; font-weight: 500; }
        .sync-settings input {
            width: 100%; padding: 0.8rem 1rem; border-radius: 16px;
            border: 1px solid #2f4a66; background: #0b1a28; color: #eef2f6;
            font-size: 1rem; margin-bottom: 1rem; outline: none;
        }
        .sync-settings input:focus { border-color: #56dba7; box-shadow: 0 0 12px #2fbb7e44; }
        .sync-settings .btn-sync {
            padding: 0.7rem 1.5rem; border-radius: 40px; border: none;
            background: linear-gradient(145deg, #6ec8ff, #4a9fd8);
            color: #0b141c; font-weight: 700; cursor: pointer;
            transition: 0.2s; font-size: 1rem; margin-right: 0.5rem;
        }
        .sync-settings .btn-sync:hover { transform: scale(1.02); box-shadow: 0 0 20px #4a9fd866; }
        .sync-settings .btn-sync.sync-save { background: linear-gradient(145deg, #2cdf8a, #1db06e); }
        .sync-settings .btn-sync.sync-save:hover { box-shadow: 0 0 20px #24d17e66; }
        .sync-settings .sync-status { color: #8eb3d4; font-size: 0.9rem; margin-top: 0.5rem; }
        .sync-settings .sync-status.success { color: #59dba6; }
        .sync-settings .sync-status.error { color: #ff5a5a; }

        /* ===== СТИЛИ ДЛЯ САЙТА СОВЕТСКОЙ ИМПЕРИИ ===== */
        .empire-wrapper {
            background: rgba(0,0,0,0.85); backdrop-filter:blur(4px);
            border-radius:40px; padding:2rem 2.2rem;
            box-shadow:0 20px 40px rgba(0,0,0,0.7),0 0 0 2px #FFD700,0 0 0 4px #1a1a1a;
            border:1px solid #d4af37;
        }
        .empire-header {
            display:flex; align-items:center; gap:24px; flex-wrap:wrap;
            border-bottom:2px solid #d4af37; padding-bottom:1.2rem; margin-bottom:1.8rem;
        }
        .empire-flag {
            flex-shrink:0; width:130px; height:75px; border-radius:10px; overflow:hidden;
            border:2px solid #d4af37; box-shadow:0 4px 12px rgba(0,0,0,0.6);
            display:flex; flex-direction:column;
        }
        .empire-flag .stripe { flex:1; width:100%; }
        .empire-flag .black { background:#000; }
        .empire-flag .yellow { background:#FFD700; }
        .empire-flag .white { background:#FFF; }
        .empire-title {
            font-size:2.6rem; font-weight:700; letter-spacing:4px;
            color:#f5e7d3; text-shadow:0 4px 14px #000000cc,0 0 10px #d4af37aa;
            font-family:'Times New Roman',serif; flex:1;
        }
        .empire-title small { font-size:1rem; font-weight:300; letter-spacing:6px; display:block; color:#e6d5b8; }
        .empire-login {
            display:flex; gap:10px; align-items:center; flex-shrink:0;
        }
        .empire-login .user-info { color:#f5e7d3; font-size:0.9rem; }
        .empire-login .user-info strong { color:#d4af37; }
        .empire-login .user-info .president-badge {
            background:linear-gradient(135deg, #ffd700, #ff6b00);
            color:#1a1a1a; font-size:0.6rem; font-weight:700;
            padding:0.1rem 0.5rem; border-radius:12px; margin-left:4px;
            text-transform:uppercase;
        }
        .empire-login button {
            background:rgba(30,25,20,0.7); border:1px solid #d4af37; border-radius:60px;
            padding:0.4rem 1.2rem; color:#f5e7d3; cursor:pointer; transition:0.2s;
            font-size:0.85rem; font-family:'Segoe UI',sans-serif;
        }
        .empire-login button:hover { background:#d4af37; color:#1a1a1a; }
        .empire-nav {
            display:flex; flex-wrap:wrap; gap:12px; margin-bottom:1.5rem;
            justify-content:center;
        }
        .empire-nav button {
            flex:1 0 auto; min-width:100px; padding:0.7rem 1.2rem;
            background:rgba(30,25,20,0.7); backdrop-filter:blur(2px);
            border:1px solid #d4af37; border-radius:60px;
            color:#f5e7d3; font-size:1rem; font-weight:500; letter-spacing:1px;
            text-align:center; cursor:pointer; transition:0.2s;
            box-shadow:0 4px 12px rgba(0,0,0,0.3);
            font-family:'Segoe UI',sans-serif; user-select:none;
        }
        .empire-nav button:hover { background:rgba(60,45,35,0.8); border-color:#e6c14f; transform:scale(1.02); }
        .empire-nav button.active { background:#d4af37; color:#1a1a1a; border-color:#f5e7d3; box-shadow:0 0 30px #d4af3766; }
        .empire-content {
            background:rgba(30,25,20,0.5); border-radius:28px;
            border:1px solid #d4af37; padding:2rem; overflow-y:auto; max-height:55vh;
        }
        .empire-content::-webkit-scrollbar { width:8px; }
        .empire-content::-webkit-scrollbar-track { background:rgba(30,25,20,0.3); border-radius:10px; }
        .empire-content::-webkit-scrollbar-thumb { background:#d4af37; border-radius:10px; }
        .empire-section { display:none; height:100%; color:#f0e6da; }
        .empire-section.active { display:block; }
        .empire-section h2 {
            font-family:'Times New Roman',serif; font-weight:700; font-size:2rem;
            color:#f5e2c9; border-bottom:2px solid #d4af37; padding-bottom:0.8rem;
            margin-bottom:1.5rem; letter-spacing:2px; text-shadow:0 2px 6px #000000aa;
        }
        .empire-section h3 { font-family:'Times New Roman',serif; font-size:1.3rem; color:#f5d742; margin:1.2rem 0 0.8rem; }
        .empire-section p { font-size:1.05rem; line-height:1.8; color:#e2d4c2; margin-bottom:0.8rem; }
        .empire-section ul { list-style:none; padding-left:0; }
        .empire-section ul li { padding:0.4rem 0 0.4rem 2.2rem; position:relative; border-bottom:1px dotted #4d3a2b; }
        .empire-section ul li::before { content:"⚜️"; position:absolute; left:0; color:#d4af37; }
        .empire-rule { background:rgba(0,0,0,0.25); border-left:3px solid #d4af37; padding:0.8rem 1.2rem; border-radius:8px; margin-bottom:0.8rem; }
        .empire-rule .rule-num { color:#f5d742; font-weight:600; }
        .empire-news { background:rgba(0,0,0,0.3); border-left:4px solid #d4af37; padding:1rem 1.2rem; border-radius:12px; margin-bottom:1rem; }
        .empire-news strong { color:#f5d742; font-weight:600; }
        .empire-ornament { text-align:center; color:#d4af37; letter-spacing:6px; font-size:0.8rem; margin-top:1rem; opacity:0.7; }

        /* ===== ФИНАНСЫ ИМПЕРИИ ===== */
        .empire-bank {
            background:rgba(0,0,0,0.3); border-radius:20px; padding:1.5rem;
            border:1px solid #d4af37; margin-top:1rem;
        }
        .empire-bank .balance {
            font-size:2.5rem; font-weight:700; color:#f5d742;
            text-shadow:0 0 20px #d4af3744;
        }
        .empire-bank .balance.infinity { color:#ffd700; }
        .empire-bank .currency { color:#b6a68a; font-size:0.9rem; }
        .empire-bank .rate {
            color:#8a7a6a; font-size:0.85rem; border-top:1px solid #4d3a2b;
            padding-top:0.8rem; margin-top:0.8rem;
        }
        .empire-transfer {
            margin-top:1.2rem; padding-top:1.2rem; border-top:1px solid #4d3a2b;
        }
        .empire-transfer .transfer-row {
            display:flex; gap:10px; flex-wrap:wrap; align-items:center;
            margin-top:0.5rem;
        }
        .empire-transfer input, .empire-transfer select {
            padding:0.5rem 1rem; border-radius:16px; border:1px solid #4d3a2b;
            background:#0a0a0a; color:#f5e7d3; font-size:0.9rem;
            outline:none; flex:1; min-width:120px;
        }
        .empire-transfer input:focus, .empire-transfer select:focus {
            border-color:#d4af37; box-shadow:0 0 12px #d4af3744;
        }
        .empire-transfer .btn-send {
            padding:0.5rem 1.5rem; border-radius:40px; border:none;
            background:linear-gradient(145deg, #d4af37, #b8962a);
            color:#1a1a1a; font-weight:600; cursor:pointer; transition:0.2s;
        }
        .empire-transfer .btn-send:hover { transform:scale(1.05); box-shadow:0 0 20px #d4af3766; }
        .empire-transfer .btn-send:disabled { opacity:0.4; cursor:not-allowed; transform:none; }
        .transfer-status { font-size:0.85rem; margin-top:0.5rem; color:#8a7a6a; }

        /* ===== МЕЖГОСУДАРСТВЕННЫЙ ПЕРЕВОД ===== */
        .cross-transfer {
            margin-top:1.2rem; padding-top:1.2rem; border-top:2px solid #d4af37;
        }
        .cross-transfer .cross-row {
            display:flex; gap:10px; flex-wrap:wrap; align-items:center;
            margin-top:0.5rem;
        }
        .cross-transfer select {
            padding:0.5rem 1rem; border-radius:16px; border:1px solid #d4af37;
            background:#0a0a0a; color:#f5e7d3; font-size:0.9rem;
            outline:none; flex:1; min-width:120px;
        }
        .cross-transfer select:focus { border-color:#d4af37; box-shadow:0 0 12px #d4af3744; }
        .cross-transfer .btn-send {
            padding:0.5rem 1.5rem; border-radius:40px; border:none;
            background:linear-gradient(145deg, #d4af37, #b8962a);
            color:#1a1a1a; font-weight:600; cursor:pointer; transition:0.2s;
        }
        .cross-transfer .btn-send:hover { transform:scale(1.05); box-shadow:0 0 20px #d4af3766; }
        .cross-transfer .btn-send:disabled { opacity:0.4; cursor:not-allowed; transform:none; }

        /* ===== РЕЗЕРВНЫЙ КОД ===== */
        .backup-section {
            margin-top:1.2rem; padding-top:1.2rem; border-top:1px solid #4d3a2b;
        }
        .backup-section .code-display {
            background:#0a0a0a; padding:0.5rem 1rem; border-radius:16px;
            font-family:'Courier New', monospace; font-size:0.85rem;
            color:#d4af37; word-break:break-all; border:1px solid #4d3a2b;
            margin:0.5rem 0;
        }
        .backup-section .btn-secondary {
            padding:0.4rem 1.2rem; border-radius:40px; border:1px solid #d4af37;
            background:rgba(30,25,20,0.7); color:#f5e7d3; cursor:pointer;
            transition:0.2s; font-size:0.9rem;
        }
        .backup-section .btn-secondary:hover { background:#d4af37; color:#1a1a1a; }
        .backup-section input {
            padding:0.5rem 1rem; border-radius:16px; border:1px solid #4d3a2b;
            background:#0a0a0a; color:#f5e7d3; font-size:0.9rem;
            width:100%; max-width:400px; outline:none; margin-top:0.3rem;
        }
        .backup-section input:focus { border-color:#d4af37; box-shadow:0 0 12px #d4af3744; }
        .backup-section .restore-row { display:flex; gap:0.8rem; flex-wrap:wrap; align-items:center; margin-top:0.5rem; }
        .backup-section .restore-status { font-size:0.85rem; margin-top:0.3rem; color:#ff6b4a; }

        .empire-demo { color:#8a7a6a; font-size:0.8rem; text-align:center; margin-top:0.5rem; border-top:1px solid #4d3a2b; padding-top:0.5rem; }

        /* ===== ТОСТ ===== */
        .toast {
            position:fixed; bottom:2rem; left:50%; transform:translateX(-50%);
            background:#1a2a34; padding:0.8rem 2rem; border-radius:60px;
            border:1px solid #3a5a6a; box-shadow:0 0 30px rgba(0,0,0,0.6);
            z-index:99999; display:none; font-size:1rem;
            backdrop-filter:blur(8px); text-align:center; max-width:90%;
            color:#f5e7d3;
        }
        .toast.show { display:block; animation:fadeInUp 0.3s ease; }
        .toast.success { border-color:#56dba7; }
        .toast.error { border-color:#ff5a5a; }
        .toast i { margin-right:8px; }
        @keyframes fadeInUp { from { opacity:0; transform:translateX(-50%) translateY(20px); } to { opacity:1; transform:translateX(-50%) translateY(0); } }

        @media (max-width:900px) {
            .empire-title { font-size:2rem; }
            .empire-flag { width:100px; height:58px; }
            .empire-nav button { white-space:normal; min-width:80px; padding:0.6rem 1rem; font-size:0.95rem; }
            .empire-content { padding:1.2rem; }
            .team-wrapper { padding:1rem; }
            .empire-login { margin-left:0; }
            .empire-transfer .transfer-row, .cross-transfer .cross-row { flex-direction:column; }
            .empire-transfer input, .empire-transfer select, .cross-transfer select { width:100%; }
            .team-nav { gap:1rem; }
            .team-nav button { font-size:0.95rem; }
            .shop-grid, .library-grid { grid-template-columns: 1fr 1fr; }
        }
        @media (max-width:550px) {
            .empire-header { flex-direction:column; align-items:flex-start; gap:12px; }
            .empire-title { font-size:1.6rem; }
            .empire-title small { font-size:0.8rem; letter-spacing:3px; }
            .empire-nav button { min-width:60px; font-size:0.85rem; padding:0.5rem 0.8rem; }
            .empire-content { padding:0.8rem; }
            .empire-section h2 { font-size:1.3rem; }
            .team-header { flex-direction:column; align-items:stretch; gap:1.2rem; }
            .team-nav { justify-content:center; }
            .empire-login { width:100%; justify-content:flex-start; }
            .empire-bank .balance { font-size:1.8rem; }
            .team-nav button { font-size:0.85rem; }
            .shop-grid, .library-grid { grid-template-columns: 1fr; }
            .team-bank, .team-passport, .team-login-form, .sync-settings { max-width:100%; }
        }
    </style>
</head>
<body>

    <div class="switch-container">
        <button class="switch-btn active" id="switchToTeam" onclick="switchSite('team')">🏛️ Республика Team</button>
        <button class="switch-btn" id="switchToEmpire" onclick="switchSite('empire')">👑 Советская империя</button>
    </div>

    <!-- ===== САЙТ РЕСПУБЛИКИ TEAM ===== -->
    <div class="site-container active" id="site-team">
        <div class="team-wrapper">
            <header class="team-header">
                <div class="team-logo">
                    <i class="fas fa-flag"></i>
                    <span>Республика <small>Team</small></span>
                </div>
                <nav class="team-nav">
                    <button class="active" data-section="departments" onclick="switchTeamTab('departments')"><i class="fas fa-users"></i> Отделы</button>
                    <button data-section="shop" onclick="switchTeamTab('shop')"><i class="fas fa-store"></i> Магазин</button>
                    <button data-section="library" onclick="switchTeamTab('library')"><i class="fas fa-book"></i> Библиотека</button>
                    <button data-section="finance" onclick="switchTeamTab('finance')"><i class="fas fa-coins"></i> Финансы</button>
                    <button data-section="passport" onclick="switchTeamTab('passport')"><i class="fas fa-id-card"></i> Паспорт</button>
                    <button data-section="profile" onclick="switchTeamTab('profile')"><i class="fas fa-user"></i> Личный кабинет</button>
                    <button data-section="sync" onclick="switchTeamTab('sync')"><i class="fas fa-cloud-upload-alt"></i> Синхронизация</button>
                </nav>
            </header>

            <div class="team-content">
                <!-- ОТДЕЛЫ -->
                <div class="team-section active" id="team-departments">
                    <h2><i class="fas fa-sitemap"></i> Отделы республики</h2>
                    <div class="team-departments">
                        <span class="team-dept"><i class="fas fa-gavel"></i> Юридический <span class="divider">|</span></span>
                        <span class="team-dept"><i class="fas fa-hand-holding-heart"></i> Социальный <span class="divider">|</span></span>
                        <span class="team-dept"><i class="fas fa-chart-line"></i> Экономики</span>
                    </div>
                    <p><strong>Юридический отдел</strong> — нормотворчество, арбитраж, защита прав граждан.<br>
                    <strong>Социальный отдел</strong> — поддержка граждан, волонтёрство, внутренние коммуникации.<br>
                    <strong>Отдел экономики</strong> — финансы, бюджетирование, налоги, гранты, инвестиции.</p>

                    <div class="team-codex">
                        <h3><i class="fas fa-scroll"></i> Кодекс правил Республики «Team»</h3>
                        <div class="team-article">
                            <div class="art-title"><i class="fas fa-balance-scale"></i> 1. Выкуп имущества</div>
                            <div class="art-text">При выкупе имущества гражданин обязан подписать договор о покупке и опираться только на него в суде при необходимости. Если покупатель решил отменить сделку, он должен выплатить государству компенсацию 6 000 рублей.</div>
                            <div class="art-sub"><i class="fas fa-chevron-right"></i> 1.1. Отменить договор можно при согласии всех членов правительства в течение 1 дня (мелкая сделка) или 2 дней (крупная).</div>
                            <div class="art-sub"><i class="fas fa-chevron-right"></i> 1.2. Если налоговой службе не понравится происхождение денег, государство может отменить сделку и не выплачивать компенсацию.</div>
                        </div>
                        <div class="team-article">
                            <div class="art-title"><i class="fas fa-car-crash"></i> 2. Нарушения на дороге</div>
                            <div class="art-text">Если гражданин будет пойман за рулём с запрещёнными веществами и в состоянии опьянения:</div>
                            <div class="art-sub"><i class="fas fa-minus"></i> В первый раз — штраф 10 рублей</div>
                            <div class="art-sub"><i class="fas fa-minus"></i> Во второй и следующие разы — штраф и лишение свободы на 1 день</div>
                        </div>
                        <div class="team-article">
                            <div class="art-title"><i class="fas fa-truck"></i> 3. При ДТП на дороге</div>
                            <div class="art-sub"><i class="fas fa-check-circle"></i> Штраф платит виноватый — 5 000 рублей</div>
                            <div class="art-sub"><i class="fas fa-check-circle"></i> Пострадавший получает компенсацию 6 000 рублей</div>
                            <div class="art-sub"><i class="fas fa-check-circle"></i> Государству выплаты не производятся</div>
                        </div>
                    </div>
                </div>

                <!-- МАГАЗИН -->
                <div class="team-section" id="team-shop">
                    <h2><i class="fas fa-store"></i> Магазин республики</h2>
                    <div class="shop-grid" id="teamShopGrid"></div>
                </div>

                <!-- БИБЛИОТЕКА -->
                <div class="team-section" id="team-library">
                    <h2><i class="fas fa-book-open"></i> Библиотека</h2>
                    <div class="library-grid" id="teamLibraryGrid"></div>
                </div>

                <!-- ФИНАНСЫ -->
                <div class="team-section" id="team-finance">
                    <h2><i class="fas fa-coins"></i> Финансы республики</h2>
                    <div class="team-bank">
                        <div class="label" style="color:#8eb3d4; font-size:0.9rem;">Ваш баланс</div>
                        <div class="balance" id="teamBalanceDisplay">0</div>
                        <div class="currency" style="color:#b0c9e8; font-size:1.2rem;">тимовских рублей</div>
                        <div style="margin-top:0.8rem; color:#8eb3d4; font-size:0.9rem; border-top:1px solid #1f344a; padding-top:0.8rem;">
                            <i class="fas fa-info-circle" style="color:#59dba6;"></i> 
                            Владелец: <span id="teamFinanceOwner">Гость</span>
                        </div>
                    </div>
                </div>

                <!-- ПАСПОРТ -->
                <div class="team-section" id="team-passport">
                    <h2><i class="fas fa-id-card"></i> Электронный паспорт</h2>
                    <div class="team-passport">
                        <ul>
                            <li><i class="fas fa-user"></i> Гражданин: <span id="teamPassportName">Team-2026</span></li>
                            <li><i class="fas fa-calendar-alt"></i> Дата регистрации: 01.01.2026</li>
                            <li><i class="fas fa-shield-alt"></i> Статус: <span style="color: #6ee6b0;">активный</span></li>
                            <li><i class="fas fa-fingerprint"></i> Цифровой ID: <span id="teamPassportId">#T-0000</span></li>
                        </ul>
                        <div class="team-passport-id">
                            <i class="fas fa-qrcode"></i>
                            <span class="id-number" id="teamPassportNumber">TEAM-2026-0000</span>
                            <i class="fas fa-chevron-right" style="color: #4b9f7a;"></i>
                        </div>
                        <p style="margin-top:0.8rem; font-size:0.9rem; color:#9bb9db;"><i class="fas fa-sync-alt" style="color:#4edb9e;"></i> Действителен до: 01.01.2028</p>
                    </div>
                </div>

                <!-- ЛИЧНЫЙ КАБИНЕТ -->
                <div class="team-section" id="team-profile">
                    <h2><i class="fas fa-user-circle"></i> Личный кабинет</h2>
                    <div class="team-login-form" id="teamLoginForm">
                        <div id="teamLoginStatus">
                            <div class="user-info" id="teamUserInfo">Вы не авторизованы</div>
                            <label>Логин</label>
                            <input type="text" id="teamLoginUser" placeholder="Семён, Азар, Вика или Президент">
                            <label>Пароль</label>
                            <input type="password" id="teamLoginPass" placeholder="Введите пароль">
                            <div class="error" id="teamLoginError">Неверный логин или пароль</div>
                            <button class="btn-login-submit" onclick="teamDoLogin()"><i class="fas fa-sign-in-alt"></i> Войти</button>
                        </div>
                        <div id="teamLogoutStatus" style="display:none;">
                            <div class="user-info" id="teamLoggedUser">Семён</div>
                            <button class="logout-btn" onclick="teamLogout()">Выйти из аккаунта</button>
                        </div>
                    </div>
                </div>

                <!-- СИНХРОНИЗАЦИЯ -->
                <div class="team-section" id="team-sync">
                    <h2><i class="fas fa-cloud-upload-alt"></i> Синхронизация данных</h2>
                    <div class="sync-settings">
                        <label>Ключ синхронизации (введите любой)</label>
                        <input type="text" id="teamSyncKey" placeholder="Введите ключ для синхронизации" value="myteam2026">
                        <div style="display:flex; flex-wrap:wrap; gap:0.5rem; margin-top:0.5rem;">
                            <button class="btn-sync sync-save" onclick="saveTeamToCloud()"><i class="fas fa-cloud-upload-alt"></i> Сохранить в облако</button>
                            <button class="btn-sync" onclick="loadTeamFromCloud()"><i class="fas fa-cloud-download-alt"></i> Загрузить из облака</button>
                        </div>
                        <div class="sync-status" id="teamSyncStatus">Готов к синхронизации</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- ===== САЙТ СОВЕТСКОЙ ИМПЕРИИ ===== -->
    <div class="site-container" id="site-empire">
        <div class="empire-wrapper">
            <header class="empire-header">
                <div class="empire-flag">
                    <div class="stripe black"></div>
                    <div class="stripe yellow"></div>
                    <div class="stripe white"></div>
                </div>
                <div class="empire-title">
                    Сайт Советской империи
                    <small>⚜️ Самодержавие · Православие · Народность ⚜️</small>
                </div>
                <div class="empire-login">
                    <span class="user-info" id="empireUserInfo">Гость</span>
                    <button id="empireLoginBtn" onclick="switchEmpireTab('profile')">Войти</button>
                </div>
            </header>

            <div class="empire-nav">
                <button class="active" data-section="rules" onclick="switchEmpireTab('rules')">📜 Правила</button>
                <button data-section="news" onclick="switchEmpireTab('news')">📰 Новости</button>
                <button data-section="bank" onclick="switchEmpireTab('bank')">💰 Банк</button>
                <button data-section="property" onclick="switchEmpireTab('property')">🏛️ Имущество</button>
                <button data-section="gov" onclick="switchEmpireTab('gov')">🏛️ Инфо для правительства</button>
                <button data-section="profile" onclick="switchEmpireTab('profile')">👤 Личный кабинет</button>
                <button data-section="sync" onclick="switchEmpireTab('sync')"><i class="fas fa-cloud-upload-alt"></i> Синхронизация</button>
            </div>

            <div class="empire-content">
                <!-- ПРАВИЛА -->
                <div class="empire-section active" id="empire-rules">
                    <h2>📜 Кодекс правил Советской Империи</h2>
                    <h3>1. Выкуп имущества</h3>
                    <div class="empire-rule"><p><span class="rule-num">1.</span> При выкупе имущества гражданин обязан подписать договор о покупке и опираться только на него в суде при необходимости. Если же договор был составлен и подписан и покупатель решил отменить сделку, то он должен выплатить государству компенсацию в размере <strong>6 000 рублей</strong>, в случае отмены сделки государством, государство не должно выплачивать компенсацию (подробнее в статье 1.2).</p></div>
                    <div class="empire-rule"><p><span class="rule-num">1.1.</span> Отменить договор можно при согласии всех членов правительства в течение <strong>1 дня</strong> на мелкую сделку и <strong>2 дней</strong> на крупную сделку.</p></div>
                    <div class="empire-rule"><p><span class="rule-num">1.2.</span> Если налоговой службе не понравится происхождение денег, выплаченных покупателем, то государство может отменить сделку (подробнее в статье 1.1.) и <strong>не выплачивать компенсацию</strong> покупателю. Государство может забрать эти деньги и вообще не отдавать их покупателю.</p></div>
                    <h3>2. Нарушения на дороге</h3>
                    <div class="empire-rule"><p><span class="rule-num">2.</span> Если гражданин будет пойман за рулём с запрещёнными веществами и в состоянии опьянения:</p><ul><li><strong>В первый раз</strong> — обязан выплатить штраф <strong>10 рублей</strong></li><li><strong>Во второй и следующие разы</strong> — выплачивает штраф и лишается свободы на срок <strong>1 день</strong></li></ul><p style="margin-top:0.5rem;font-style:italic;color:#c7b7a2;">*При лишении свободы деятельность человека прекращается на указанный срок.</p></div>
                    <div class="empire-rule"><p><span class="rule-num">3.</span> При ДТП на дороге:</p><ul><li><strong>Вина</strong> — штраф оплачивает только <strong>виноватый</strong> участник</li><li><strong>Штраф виноватому</strong> — <strong>5 000 рублей</strong></li><li><strong>Пострадавшему</strong> — выплачивается компенсация <strong>6 000 рублей</strong></li><li><strong>Государству</strong> — выплаты не производятся</li></ul><p style="margin-top:0.5rem;font-style:italic;color:#c7b7a2;">*Без суда и решения штраф не выплачивается.</p></div>
                </div>

                <!-- НОВОСТИ -->
                <div class="empire-section" id="empire-news">
                    <h2>📰 Свежие новости</h2>
                    <div class="empire-news"><strong>9.07.26.</strong> Азар.А.Р. выкупил территорию у государства. Подробнее можно узнать у правителя или в разделе <strong>«Информация для правительства»</strong>.</div>
                    <div class="empire-news"><strong>8.07.26.</strong> Президент Андрей утвердил новый курс валют: 1 тимовский рубль = 10 имперских рублей.</div>
                    <div id="empireTransferHistory" style="margin-top:1rem;"></div>
                </div>

                <!-- БАНК -->
                <div class="empire-section" id="empire-bank">
                    <h2>💰 Банк Советской империи</h2>
                    <div class="empire-bank">
                        <div style="display:flex; justify-content:space-between; flex-wrap:wrap; gap:10px;">
                            <div>
                                <div style="color:#8a7a6a; font-size:0.85rem;">Ваш баланс</div>
                                <div class="balance" id="empireBalance">0</div>
                                <div class="currency">имперских рублей</div>
                            </div>
                            <div style="text-align:right;">
                                <div style="color:#8a7a6a; font-size:0.85rem;">Курс обмена</div>
                                <div style="color:#f5d742; font-size:1.1rem; font-weight:600;">1 тим. руб. = 10 имп. руб.</div>
                            </div>
                        </div>
                        <div class="rate" id="empireRateInfo">Владелец: <span id="empireBankOwner">Гость</span></div>

                        <div class="empire-transfer">
                            <div style="color:#b6a68a; font-weight:500; margin-bottom:0.3rem;">💸 Перевести деньги</div>
                            <div class="transfer-row">
                                <input type="number" id="transferAmount" placeholder="Сумма в имп. руб." min="1">
                                <select id="transferRecipient">
                                    <option value="">Выберите получателя</option>
                                </select>
                                <button class="btn-send" id="transferBtn" onclick="sendEmpireTransfer()">Отправить</button>
                            </div>
                            <div class="transfer-status" id="transferStatus"></div>
                        </div>

                        <!-- ===== МЕЖГОСУДАРСТВЕННЫЙ ПЕРЕВОД ===== -->
                        <div class="cross-transfer">
                            <div style="color:#d4af37; font-weight:600; margin-bottom:0.3rem;">🌍 Межгосударственный перевод</div>
                            <div style="color:#8a7a6a; font-size:0.85rem; margin-bottom:0.5rem;">Курс: 1 тим. руб. = 10 имп. руб.</div>
                            <div class="cross-row">
                                <select id="crossRecipient">
                                    <option value="">Выберите гражданина Республики Team</option>
                                </select>
                                <input type="number" id="crossAmount" placeholder="Сумма в тим. руб." min="1" style="padding:0.5rem 1rem; border-radius:16px; border:1px solid #d4af37; background:#0a0a0a; color:#f5e7d3; font-size:0.9rem; outline:none; flex:1; min-width:120px;">
                                <button class="btn-send" id="crossTransferBtn" onclick="sendCrossTransfer()">Перевести</button>
                            </div>
                            <div class="transfer-status" id="crossTransferStatus"></div>
                        </div>

                        <!-- ===== РЕЗЕРВНЫЙ КОД ДЛЯ ИМПЕРИИ ===== -->
                        <div class="backup-section">
                            <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:0.5rem;">
                                <span style="color:#b6a68a; font-weight:500;"><i class="fas fa-code"></i> Резервный код банка</span>
                                <button class="btn-secondary" onclick="generateEmpireBackupCode()">Сгенерировать код</button>
                            </div>
                            <div class="code-display" id="empireBackupCodeDisplay">Нажмите «Сгенерировать код»</div>
                            <div style="font-size:0.8rem; color:#6c89aa; margin-bottom:0.5rem;">
                                <i class="fas fa-info-circle"></i> Скопируйте код для восстановления баланса и истории переводов на другом устройстве
                            </div>
                            <div class="restore-row">
                                <input type="text" id="empireRestoreCodeInput" placeholder="Вставьте код для восстановления">
                                <button class="btn-secondary" onclick="restoreEmpireFromCode()">Восстановить</button>
                            </div>
                            <div class="restore-status" id="empireRestoreStatus"></div>
                        </div>
                    </div>
                </div>

                <!-- ИМУЩЕСТВО -->
                <div class="empire-section" id="empire-property">
                    <h2>🏛️ Имущество</h2>
                    <p style="opacity:0.7;font-style:italic;color:#c7b7a2;">Здесь пока ничего нет.</p>
                </div>

                <!-- ИНФО ДЛЯ ПРАВИТЕЛЬСТВА -->
                <div class="empire-section" id="empire-gov">
                    <h2>🏛️ Информация для правительства</h2>
                    <p><strong>Секретные сведения</strong></p>
                    <p id="govContent" style="opacity:0.7;font-style:italic;color:#c7b7a2;">Требуется авторизация.</p>
                    <ul style="list-style:none;padding-left:0;margin-top:12px;">
                        <li style="padding:0.5rem 0 0.5rem 2.2rem;border-bottom:1px dotted #4d3a2b;position:relative;">
                            <span style="position:absolute;left:0;color:#d4af37;">⚜️</span> Доступ только по паролю
                        </li>
                    </ul>
                </div>

                <!-- ЛИЧНЫЙ КАБИНЕТ ИМПЕРИИ -->
                <div class="empire-section" id="empire-profile">
                    <h2><i class="fas fa-user-circle"></i> Личный кабинет</h2>
                    <div class="team-login-form" style="max-width:400px; margin:0 auto; background:rgba(0,0,0,0.3); border-color:#d4af37;">
                        <div id="empireLoginStatus">
                            <div class="user-info" id="empireUserInfoForm" style="color:#f5e7d3;">Вы не авторизованы</div>
                            <label style="color:#b6a68a;">Логин</label>
                            <input type="text" id="empireLoginUserForm" placeholder="Андрей, Ярослав или Богдан" style="border-color:#4d3a2b; background:#0a0a0a; color:#f5e7d3;">
                            <label style="color:#b6a68a;">Пароль</label>
                            <input type="password" id="empireLoginPassForm" placeholder="Введите пароль" style="border-color:#4d3a2b; background:#0a0a0a; color:#f5e7d3;">
                            <div class="error" id="empireLoginErrorForm">Неверный логин или пароль</div>
                            <button class="btn-go" onclick="empireDoLoginForm()" style="background:linear-gradient(145deg, #d4af37, #b8962a);">Войти</button>
                        </div>
                        <div id="empireLogoutStatus" style="display:none;">
                            <div class="user-info" id="empireLoggedUser" style="color:#f5e7d3;">Андрей</div>
                            <button class="logout-btn" onclick="empireLogoutForm()" style="background:#ff5a5a; color:#fff;">Выйти из аккаунта</button>
                        </div>
                    </div>
                </div>

                <!-- СИНХРОНИЗАЦИЯ ДЛЯ ИМПЕРИИ -->
                <div class="empire-section" id="empire-sync">
                    <h2><i class="fas fa-cloud-upload-alt"></i> Синхронизация данных</h2>
                    <div class="sync-settings" style="border-color:#d4af37; background:rgba(0,0,0,0.3);">
                        <label style="color:#b6a68a;">Ключ синхронизации (введите любой)</label>
                        <input type="text" id="empireSyncKey" placeholder="Введите ключ для синхронизации" value="myempire2026" style="border-color:#4d3a2b; background:#0a0a0a; color:#f5e7d3;">
                        <div style="display:flex; flex-wrap:wrap; gap:0.5rem; margin-top:0.5rem;">
                            <button class="btn-sync sync-save" onclick="saveEmpireToCloud()" style="background:linear-gradient(145deg, #d4af37, #b8962a);"><i class="fas fa-cloud-upload-alt"></i> Сохранить в облако</button>
                            <button class="btn-sync" onclick="loadEmpireFromCloud()" style="background:linear-gradient(145deg, #d4af37, #b8962a);"><i class="fas fa-cloud-download-alt"></i> Загрузить из облака</button>
                        </div>
                        <div class="sync-status" id="empireSyncStatus" style="color:#b6a68a;">Готов к синхронизации</div>
                    </div>
                </div>
            </div>
            <div class="empire-ornament">⚜️ ⚜️ ⚜️</div>
        </div>
    </div>

    <!-- ===== ТОСТ ===== -->
    <div class="toast" id="toast"><i class="fas fa-check-circle"></i> <span id="toastMsg">Успешно!</span></div>

    <script>
        // ============================================================
        // ===== ДАННЫЕ АККАУНТОВ =====
        // ============================================================
        // Аккаунты Республики Team
        var teamUsersData = {
            'Семён': { password: '135264', balance: 1000000, passportId: '#T-0428', passportNumber: 'TEAM-2026-0428', inventory: [], library: [] },
            'Азар': { password: '342567', balance: 0, passportId: '#T-0917', passportNumber: 'TEAM-2026-0917', inventory: [], library: [] },
            'Вика': { password: '845986', balance: 0, passportId: '#T-1523', passportNumber: 'TEAM-2026-1523', inventory: [], library: [] },
            'Президент': { password: '630036', balance: Infinity, passportId: '#T-0001', passportNumber: 'TEAM-2026-0001', inventory: [], library: [] }
        };

        // Аккаунты Советской империи
        var empireUsers = {
            'Андрей': { password: '567384', balance: 0, isPresident: true, transferHistory: [] },
            'Ярослав': { password: '274890', balance: 0, isPresident: false, transferHistory: [] },
            'Богдан': { password: '309940', balance: 0, isPresident: false, transferHistory: [] }
        };

        var teamCurrentUser = null;
        var empireCurrentUser = null;

        // ============================================================
        // ===== ТОВАРЫ И КНИГИ =====
        // ============================================================
        var shopItems = [
            { id: 1, name: '🚌 Экскурсия по республике', price: 25000, icon: 'fa-bus', desc: 'Следующая экскурсия послезавтра, не упустите шанс!' },
            { id: 2, name: '🍕 Пицца', price: 150, icon: 'fa-pizza-slice', desc: 'Вкусная итальянская пицца' },
            { id: 3, name: '🎮 Игра', price: 500, icon: 'fa-gamepad', desc: 'Новая компьютерная игра' },
            { id: 4, name: '🖥️ Видеокарта', price: 2500, icon: 'fa-microchip', desc: 'Мощная видеокарта для игр' }
        ];

        var libraryItems = [
            { id: 101, name: '📖 Мастер и Маргарита', author: 'Михаил Булгаков', price: 350, icon: 'fa-book-open', desc: 'Гениальный роман о любви, сатире и мистике.' },
            { id: 102, name: '📖 1984', author: 'Джордж Оруэлл', price: 300, icon: 'fa-eye', desc: 'Культовый роман-антиутопия.' },
            { id: 103, name: '📖 Война и мир', author: 'Лев Толстой', price: 450, icon: 'fa-landmark', desc: 'Великий роман о любви, войне и судьбах людей.' },
            { id: 104, name: '📖 Преступление и наказание', author: 'Фёдор Достоевский', price: 400, icon: 'fa-gavel', desc: 'Глубокий роман о морали, вине и искуплении.' }
        ];

        // ============================================================
        // ===== СОХРАНЕНИЕ В LOCALSTORAGE =====
        // ============================================================
        function saveTeamUserData(username) {
            var data = teamUsersData[username];
            if (!data) return;
            try {
                localStorage.setItem('team_' + username + '_balance', data.balance);
                localStorage.setItem('team_' + username + '_inventory', JSON.stringify(data.inventory || []));
                localStorage.setItem('team_' + username + '_library', JSON.stringify(data.library || []));
            } catch(e) { /* ignore */ }
        }

        function loadTeamUserData(username) {
            var data = teamUsersData[username];
            if (!data) return;
            try {
                var bal = localStorage.getItem('team_' + username + '_balance');
                var inv = localStorage.getItem('team_' + username + '_inventory');
                var lib = localStorage.getItem('team_' + username + '_library');
                if (bal !== null && bal !== 'Infinity') data.balance = parseFloat(bal);
                else if (bal === 'Infinity') data.balance = Infinity;
                if (inv) data.inventory = JSON.parse(inv);
                if (lib) data.library = JSON.parse(lib);
            } catch(e) { /* ignore */ }
        }

        function saveEmpireUserData(username) {
            var data = empireUsers[username];
            if (!data) return;
            try {
                localStorage.setItem('empire_' + username + '_balance', data.balance);
                localStorage.setItem('empire_' + username + '_history', JSON.stringify(data.transferHistory || []));
            } catch(e) { /* ignore */ }
        }

        function loadEmpireUserData(username) {
            var data = empireUsers[username];
            if (!data) return;
            try {
                var bal = localStorage.getItem('empire_' + username + '_balance');
                var hist = localStorage.getItem('empire_' + username + '_history');
                if (bal !== null && bal !== 'Infinity') data.balance = parseFloat(bal);
                else if (bal === 'Infinity') data.balance = Infinity;
                if (hist) data.transferHistory = JSON.parse(hist);
            } catch(e) { /* ignore */ }
        }

        function loadAllData() {
            for (var user in teamUsersData) loadTeamUserData(user);
            for (var user in empireUsers) loadEmpireUserData(user);
        }

        // ============================================================
        // ===== ПЕРЕКЛЮЧЕНИЕ ВКЛАДОК =====
        // ============================================================
        function switchTeamTab(tab) {
            var btns = document.querySelectorAll('.team-nav button');
            for (var i = 0; i < btns.length; i++) {
                btns[i].classList.remove('active');
            }
            for (var i = 0; i < btns.length; i++) {
                if (btns[i].getAttribute('data-section') === tab) {
                    btns[i].classList.add('active');
                }
            }
            var sections = document.querySelectorAll('.team-section');
            for (var i = 0; i < sections.length; i++) {
                sections[i].classList.remove('active');
            }
            var target = document.getElementById('team-' + tab);
            if (target) {
                target.classList.add('active');
            }
        }

        function switchEmpireTab(tab) {
            var btns = document.querySelectorAll('.empire-nav button');
            for (var i = 0; i < btns.length; i++) {
                btns[i].classList.remove('active');
            }
            for (var i = 0; i < btns.length; i++) {
                if (btns[i].getAttribute('data-section') === tab) {
                    btns[i].classList.add('active');
                }
            }
            var sections = document.querySelectorAll('.empire-section');
            for (var i = 0; i < sections.length; i++) {
                sections[i].classList.remove('active');
            }
            var target = document.getElementById('empire-' + tab);
            if (target) {
                target.classList.add('active');
            }
            
            if (tab === 'bank') {
                updateRecipientsList();
                updateCrossRecipients();
            }
            if (tab === 'news') {
                renderEmpireTransferHistory();
            }
        }

        // ============================================================
        // ===== АВТОРИЗАЦИЯ В TEAM =====
        // ============================================================
        function teamDoLogin() {
            var login = document.getElementById('teamLoginUser').value.trim();
            var pass = document.getElementById('teamLoginPass').value.trim();

            if (teamUsersData[login] && teamUsersData[login].password === pass) {
                teamCurrentUser = login;
                loadTeamUserData(login);
                document.getElementById('teamLoginError').classList.remove('show');
                updateTeamUI();
                renderTeamShop();
                renderTeamLibrary();
                showToast('Добро пожаловать, ' + login + '!', 'success');
            } else {
                document.getElementById('teamLoginError').classList.add('show');
            }
        }

        function teamLogout() {
            if (teamCurrentUser) saveTeamUserData(teamCurrentUser);
            teamCurrentUser = null;
            updateTeamUI();
            renderTeamShop();
            renderTeamLibrary();
            showToast('Вы вышли из аккаунта', 'error');
        }

        function updateTeamUI() {
            var loginStatus = document.getElementById('teamLoginStatus');
            var logoutStatus = document.getElementById('teamLogoutStatus');
            var userInfo = document.getElementById('teamUserInfo');
            var loggedUser = document.getElementById('teamLoggedUser');
            var balanceDisplay = document.getElementById('teamBalanceDisplay');
            var financeOwner = document.getElementById('teamFinanceOwner');
            var passportName = document.getElementById('teamPassportName');
            var passportId = document.getElementById('teamPassportId');
            var passportNumber = document.getElementById('teamPassportNumber');

            if (teamCurrentUser) {
                var data = teamUsersData[teamCurrentUser];
                loginStatus.style.display = 'none';
                logoutStatus.style.display = 'block';
                var bal = data.balance === Infinity ? '∞' : data.balance.toLocaleString('ru-RU');
                loggedUser.textContent = teamCurrentUser + ' (' + bal + ' тим. руб.)';
                financeOwner.textContent = teamCurrentUser;
                passportName.textContent = teamCurrentUser + ' (гражданин)';
                passportId.textContent = data.passportId;
                passportNumber.textContent = data.passportNumber;
                if (data.balance === Infinity) {
                    balanceDisplay.textContent = '∞';
                    balanceDisplay.className = 'balance infinity';
                } else {
                    balanceDisplay.textContent = data.balance.toLocaleString('ru-RU');
                    balanceDisplay.className = 'balance';
                }
            } else {
                loginStatus.style.display = 'block';
                logoutStatus.style.display = 'none';
                userInfo.textContent = 'Вы не авторизованы';
                financeOwner.textContent = 'Гость';
                passportName.textContent = 'Team-2026';
                passportId.textContent = '#T-0000';
                passportNumber.textContent = 'TEAM-2026-0000';
                balanceDisplay.textContent = '0';
                balanceDisplay.className = 'balance';
                document.getElementById('teamLoginUser').value = '';
                document.getElementById('teamLoginPass').value = '';
            }
        }

        // ============================================================
        // ===== АВТОРИЗАЦИЯ В ИМПЕРИИ =====
        // ============================================================
        function empireDoLoginForm() {
            var login = document.getElementById('empireLoginUserForm').value.trim();
            var pass = document.getElementById('empireLoginPassForm').value.trim();

            if (empireUsers[login] && empireUsers[login].password === pass) {
                empireCurrentUser = login;
                loadEmpireUserData(login);
                document.getElementById('empireLoginErrorForm').classList.remove('show');
                updateEmpireUILocal();
                updateEmpireUI();
                showToast('Добро пожаловать, ' + login + '!', 'success');
            } else {
                document.getElementById('empireLoginErrorForm').classList.add('show');
            }
        }

        function empireLogoutForm() {
            if (empireCurrentUser) saveEmpireUserData(empireCurrentUser);
            empireCurrentUser = null;
            updateEmpireUILocal();
            updateEmpireUI();
            showToast('Вы вышли из аккаунта', 'error');
        }

        function updateEmpireUILocal() {
            var loginStatus = document.getElementById('empireLoginStatus');
            var logoutStatus = document.getElementById('empireLogoutStatus');
            var userInfo = document.getElementById('empireUserInfoForm');
            var loggedUser = document.getElementById('empireLoggedUser');

            if (empireCurrentUser) {
                var data = empireUsers[empireCurrentUser];
                loginStatus.style.display = 'none';
                logoutStatus.style.display = 'block';
                var balance = data.balance === Infinity ? '∞' : data.balance.toLocaleString('ru-RU');
                loggedUser.textContent = empireCurrentUser + ' (' + balance + ' имп. руб.)';
                document.getElementById('empireLoginUserForm').value = '';
                document.getElementById('empireLoginPassForm').value = '';
            } else {
                loginStatus.style.display = 'block';
                logoutStatus.style.display = 'none';
                userInfo.textContent = 'Вы не авторизованы';
            }
        }

        function updateEmpireUI() {
            var userInfo = document.getElementById('empireUserInfo');
            var loginBtn = document.getElementById('empireLoginBtn');
            var balanceDisplay = document.getElementById('empireBalance');
            var bankOwner = document.getElementById('empireBankOwner');
            var govContent = document.getElementById('govContent');
            var transferBtn = document.getElementById('transferBtn');
            var crossTransferBtn = document.getElementById('crossTransferBtn');

            if (empireCurrentUser) {
                var userData = empireUsers[empireCurrentUser];
                var isPresident = userData.isPresident || false;
                var badge = isPresident ? ' <span class="president-badge">Президент</span>' : '';
                userInfo.innerHTML = '<i class="fas fa-user-circle" style="color:#d4af37;"></i> <strong>' + empireCurrentUser + '</strong>' + badge;
                loginBtn.textContent = 'Выйти';
                loginBtn.onclick = function() { empireLogoutForm(); };

                if (userData.balance === Infinity) {
                    balanceDisplay.textContent = '∞';
                    balanceDisplay.className = 'balance infinity';
                } else {
                    balanceDisplay.textContent = userData.balance.toLocaleString('ru-RU');
                    balanceDisplay.className = 'balance';
                }
                bankOwner.textContent = empireCurrentUser + (isPresident ? ' (Президент)' : '');

                if (isPresident) {
                    govContent.innerHTML = '🔐 <strong>Президентский доступ</strong><br>Бюджет империи: 1 000 000 имп. руб.<br>Резервный фонд: 500 000 имп. руб.<br>Все граждане: ' + Object.keys(empireUsers).join(', ');
                    govContent.style.opacity = '1';
                    govContent.style.color = '#f5e7d3';
                    govContent.style.fontStyle = 'normal';
                } else {
                    govContent.innerHTML = '🔐 <strong>Информация для граждан</strong><br>Вы имеете доступ к банковской системе.<br>Курс обмена: 1 тим. руб. = 10 имп. руб.';
                    govContent.style.opacity = '1';
                    govContent.style.color = '#e2d4c2';
                    govContent.style.fontStyle = 'normal';
                }

                transferBtn.disabled = false;
                crossTransferBtn.disabled = false;
                updateRecipientsList();
                updateCrossRecipients();
                renderEmpireTransferHistory();

            } else {
                userInfo.textContent = 'Гость';
                loginBtn.textContent = 'Войти';
                loginBtn.onclick = function() { 
                    switchEmpireTab('profile');
                };
                balanceDisplay.textContent = '0';
                balanceDisplay.className = 'balance';
                bankOwner.textContent = 'Гость';
                govContent.innerHTML = 'Требуется авторизация.';
                govContent.style.opacity = '0.7';
                govContent.style.color = '#c7b7a2';
                govContent.style.fontStyle = 'italic';
                transferBtn.disabled = true;
                crossTransferBtn.disabled = true;
                document.getElementById('transferRecipient').innerHTML = '<option value="">Войдите для переводов</option>';
                document.getElementById('crossRecipient').innerHTML = '<option value="">Войдите для переводов</option>';
                document.getElementById('empireTransferHistory').innerHTML = '';
            }
        }

        // ============================================================
        // ===== ФУНКЦИИ ДЛЯ TEAM (МАГАЗИН, БИБЛИОТЕКА) =====
        // ============================================================
        function renderTeamShop() {
            var grid = document.getElementById('teamShopGrid');
            var html = '';
            var user = teamCurrentUser ? teamUsersData[teamCurrentUser] : null;

            shopItems.forEach(function(item) {
                var owned = user && user.inventory && user.inventory.indexOf(item.id) !== -1;
                var isPresident = teamCurrentUser === 'Президент';
                var canBuy = teamCurrentUser && (isPresident || (user.balance >= item.price)) && !owned;

                html += '<div class="shop-item">';
                html += '<div class="item-icon"><i class="fas ' + item.icon + '"></i></div>';
                html += '<div class="item-name">' + item.name + '</div>';
                html += '<div class="item-desc">' + item.desc + '</div>';
                html += '<div class="item-price"><i class="fas fa-coins"></i> ' + item.price + ' тим. руб.</div>';
                if (owned) {
                    html += '<div class="item-owned"><i class="fas fa-check-circle"></i> В инвентаре</div>';
                } else if (teamCurrentUser) {
                    html += '<button class="btn-buy" onclick="teamBuyItem(' + item.id + ')" ' + (canBuy ? '' : 'disabled') + '>Купить</button>';
                    if (!canBuy) {
                        html += '<div style="font-size:0.75rem;color:#ff7a7a;margin-top:4px;">Недостаточно средств</div>';
                    }
                } else {
                    html += '<div style="font-size:0.85rem;color:#8eb3d4;">Войдите для покупки</div>';
                }
                html += '</div>';
            });

            grid.innerHTML = html;
        }

        function teamBuyItem(itemId) {
            if (!teamCurrentUser) {
                showToast('Войдите в аккаунт!', 'error');
                return;
            }
            var user = teamUsersData[teamCurrentUser];
            var item = shopItems.find(function(i) { return i.id === itemId; });
            if (!item) return;

            if (user.inventory.indexOf(itemId) !== -1) {
                showToast('У вас уже есть этот товар!', 'error');
                return;
            }
            if (user.balance !== Infinity && user.balance < item.price) {
                showToast('Недостаточно средств!', 'error');
                return;
            }
            if (user.balance !== Infinity) user.balance -= item.price;
            user.inventory.push(itemId);
            saveTeamUserData(teamCurrentUser);
            updateTeamUI();
            renderTeamShop();
            showToast('Куплено: ' + item.name, 'success');
        }

        function renderTeamLibrary() {
            var grid = document.getElementById('teamLibraryGrid');
            var html = '';
            var user = teamCurrentUser ? teamUsersData[teamCurrentUser] : null;

            libraryItems.forEach(function(item) {
                var owned = user && user.library && user.library.indexOf(item.id) !== -1;
                var isPresident = teamCurrentUser === 'Президент';
                var canBuy = teamCurrentUser && (isPresident || (user.balance >= item.price)) && !owned;

                html += '<div class="library-item">';
                html += '<div class="item-icon"><i class="fas ' + item.icon + '"></i></div>';
                html += '<div class="item-name">' + item.name + '</div>';
                html += '<div class="item-desc">' + item.author + ' — ' + item.desc + '</div>';
                html += '<div class="item-price"><i class="fas fa-coins"></i> ' + item.price + ' тим. руб.</div>';
                if (owned) {
                    html += '<div class="item-owned"><i class="fas fa-check-circle"></i> В библиотеке</div>';
                    html += '<button class="btn-read" onclick="showToast(\'📖 Чтение книги: ' + item.name + '\', \'success\')"><i class="fas fa-book-open"></i> Читать</button>';
                } else if (teamCurrentUser) {
                    html += '<button class="btn-buy" onclick="teamBuyBook(' + item.id + ')" ' + (canBuy ? '' : 'disabled') + '>Купить</button>';
                    if (!canBuy) {
                        html += '<div style="font-size:0.75rem;color:#ff7a7a;margin-top:4px;">Недостаточно средств</div>';
                    }
                } else {
                    html += '<div style="font-size:0.85rem;color:#8eb3d4;">Войдите для покупки</div>';
                }
                html += '</div>';
            });

            grid.innerHTML = html;
        }

        function teamBuyBook(itemId) {
            if (!teamCurrentUser) {
                showToast('Войдите в аккаунт!', 'error');
                return;
            }
            var user = teamUsersData[teamCurrentUser];
            var item = libraryItems.find(function(i) { return i.id === itemId; });
            if (!item) return;

            if (user.library.indexOf(itemId) !== -1) {
                showToast('У вас уже есть эта книга!', 'error');
                return;
            }
            if (user.balance !== Infinity && user.balance < item.price) {
                showToast('Недостаточно средств!', 'error');
                return;
            }
            if (user.balance !== Infinity) user.balance -= item.price;
            user.library.push(itemId);
            saveTeamUserData(teamCurrentUser);
            updateTeamUI();
            renderTeamLibrary();
            showToast('Куплена книга: ' + item.name, 'success');
        }

        // ============================================================
        // ===== ФУНКЦИИ ДЛЯ ИМПЕРИИ (ПЕРЕВОДЫ) =====
        // ============================================================
        function updateRecipientsList() {
            var select = document.getElementById('transferRecipient');
            select.innerHTML = '<option value="">Выберите получателя</option>';
            for (var user in empireUsers) {
                if (user !== empireCurrentUser) {
                    var option = document.createElement('option');
                    option.value = user;
                    var bal = empireUsers[user].balance;
                    option.textContent = user + ' (' + (bal === Infinity ? '∞' : bal.toLocaleString('ru-RU')) + ' имп. руб.)';
                    select.appendChild(option);
                }
            }
        }

        function updateCrossRecipients() {
            var select = document.getElementById('crossRecipient');
            select.innerHTML = '<option value="">Выберите гражданина Республики Team</option>';
            for (var user in teamUsersData) {
                var option = document.createElement('option');
                option.value = user;
                var bal = teamUsersData[user].balance;
                option.textContent = user + ' (' + (bal === Infinity ? '∞' : bal.toLocaleString('ru-RU')) + ' тим. руб.)';
                select.appendChild(option);
            }
        }

        function renderEmpireTransferHistory() {
            var container = document.getElementById('empireTransferHistory');
            if (!empireCurrentUser) {
                container.innerHTML = '';
                return;
            }
            var userData = empireUsers[empireCurrentUser];
            var history = userData.transferHistory || [];
            if (history.length === 0) {
                container.innerHTML = '<div style="color:#8a7a6a; font-style:italic; margin-top:0.5rem;">История переводов пуста</div>';
                return;
            }
            var html = '<div style="margin-top:0.8rem; border-top:1px solid #4d3a2b; padding-top:0.8rem;"><strong style="color:#f5d742;">📋 История переводов</strong>';
            for (var i = history.length - 1; i >= 0; i--) {
                var t = history[i];
                var isOut = t.from === empireCurrentUser;
                var sign = isOut ? '➡️' : '⬅️';
                var color = isOut ? '#ff6b4a' : '#59dba6';
                html += '<div style="padding:0.3rem 0; border-bottom:1px dotted #3d2a1a; font-size:0.9rem;">';
                html += '<span style="color:' + color + ';">' + sign + '</span> ';
                if (t.cross) {
                    html += '🌍 <span style="color:#d4af37;">МЕЖГОСУДАРСТВЕННЫЙ</span> — ';
                }
                html += '<span style="color:#b6a68a;">' + t.date + '</span> — ';
                if (isOut) {
                    html += 'перевод <strong style="color:#ff6b4a;">' + t.amount + '</strong> ';
                    if (t.cross) {
                        html += 'тим. руб. → ' + t.amountEmpire + ' имп. руб. ';
                    } else {
                        html += 'имп. руб. ';
                    }
                    html += 'для <strong>' + t.to + '</strong>';
                } else {
                    html += 'получено <strong style="color:#59dba6;">' + t.amount + '</strong> ';
                    if (t.cross) {
                        html += 'тим. руб. (' + t.amountEmpire + ' имп. руб.) ';
                    } else {
                        html += 'имп. руб. ';
                    }
                    html += 'от <strong>' + t.from + '</strong>';
                }
                html += '</div>';
            }
            html += '</div>';
            container.innerHTML = html;
        }

        function sendEmpireTransfer() {
            if (!empireCurrentUser) {
                showToast('Войдите в аккаунт!', 'error');
                return;
            }

            var amount = parseInt(document.getElementById('transferAmount').value);
            var recipient = document.getElementById('transferRecipient').value;
            var status = document.getElementById('transferStatus');

            if (!amount || amount <= 0) {
                status.textContent = '❌ Введите корректную сумму';
                status.style.color = '#ff6b4a';
                return;
            }

            if (!recipient) {
                status.textContent = '❌ Выберите получателя';
                status.style.color = '#ff6b4a';
                return;
            }

            var senderData = empireUsers[empireCurrentUser];
            var recipientData = empireUsers[recipient];

            if (senderData.balance !== Infinity && senderData.balance < amount) {
                status.textContent = '❌ Недостаточно средств! У вас ' + senderData.balance + ' имп. руб.';
                status.style.color = '#ff6b4a';
                return;
            }

            if (senderData.balance !== Infinity) senderData.balance -= amount;
            if (recipientData.balance !== Infinity) recipientData.balance += amount;

            var now = new Date();
            var dateStr = now.toLocaleDateString('ru-RU') + ' ' + now.toLocaleTimeString('ru-RU', {hour:'2-digit', minute:'2-digit'});
            var transferRecord = { from: empireCurrentUser, to: recipient, amount: amount, date: dateStr, cross: false };
            senderData.transferHistory.push(transferRecord);
            recipientData.transferHistory.push(transferRecord);

            saveEmpireUserData(empireCurrentUser);
            saveEmpireUserData(recipient);

            status.textContent = '✅ Переведено ' + amount + ' имп. руб. для ' + recipient;
            status.style.color = '#59dba6';
            document.getElementById('transferAmount').value = '';

            showToast('Переведено ' + amount + ' имп. руб. для ' + recipient, 'success');
            updateEmpireUI();
            updateRecipientsList();
            renderEmpireTransferHistory();
        }

        function sendCrossTransfer() {
            if (!empireCurrentUser) {
                showToast('Войдите в аккаунт!', 'error');
                return;
            }

            var amount = parseInt(document.getElementById('crossAmount').value);
            var recipient = document.getElementById('crossRecipient').value;
            var status = document.getElementById('crossTransferStatus');

            if (!amount || amount <= 0) {
                status.textContent = '❌ Введите корректную сумму (в тим. рублях)';
                status.style.color = '#ff6b4a';
                return;
            }

            if (!recipient) {
                status.textContent = '❌ Выберите получателя из Республики Team';
                status.style.color = '#ff6b4a';
                return;
            }

            var senderData = empireUsers[empireCurrentUser];
            var recipientData = teamUsersData[recipient];

            var amountEmpire = amount * 10;

            if (senderData.balance !== Infinity && senderData.balance < amountEmpire) {
                status.textContent = '❌ Недостаточно средств! Нужно ' + amountEmpire + ' имп. руб. (у вас ' + senderData.balance + ')';
                status.style.color = '#ff6b4a';
                return;
            }

            if (senderData.balance !== Infinity) senderData.balance -= amountEmpire;
            if (recipientData.balance !== Infinity) recipientData.balance += amount;

            var now = new Date();
            var dateStr = now.toLocaleDateString('ru-RU') + ' ' + now.toLocaleTimeString('ru-RU', {hour:'2-digit', minute:'2-digit'});

            var senderRecord = {
                from: empireCurrentUser,
                to: recipient + ' (Team)',
                amount: amount,
                amountEmpire: amountEmpire,
                date: dateStr,
                cross: true
            };
            senderData.transferHistory.push(senderRecord);

            var recipientHistory = JSON.parse(localStorage.getItem('team_' + recipient + '_history') || '[]');
            var recipientRecord = {
                from: empireCurrentUser + ' (Империя)',
                to: recipient,
                amount: amount,
                amountEmpire: amountEmpire,
                date: dateStr,
                cross: true
            };
            recipientHistory.push(recipientRecord);
            localStorage.setItem('team_' + recipient + '_history', JSON.stringify(recipientHistory));

            saveEmpireUserData(empireCurrentUser);
            saveTeamUserData(recipient);

            status.textContent = '✅ Переведено ' + amount + ' тим. руб. (' + amountEmpire + ' имп. руб.) для ' + recipient + ' (Team)';
            status.style.color = '#59dba6';
            document.getElementById('crossAmount').value = '';

            showToast('🌍 Переведено ' + amount + ' тим. руб. для ' + recipient, 'success');
            updateEmpireUI();
            renderEmpireTransferHistory();
            updateCrossRecipients();
        }

        // ============================================================
        // ===== РЕЗЕРВНЫЙ КОД ДЛЯ ИМПЕРИИ =====
        // ============================================================
        function generateEmpireBackupCode() {
            if (!empireCurrentUser) {
                showToast('Войдите в аккаунт!', 'error');
                return;
            }
            var userData = empireUsers[empireCurrentUser];
            var data = {
                owner: empireCurrentUser,
                balance: userData.balance === Infinity ? 'Infinity' : userData.balance,
                history: userData.transferHistory || [],
                timestamp: Date.now()
            };
            var encoded = btoa(encodeURIComponent(JSON.stringify(data)));
            document.getElementById('empireBackupCodeDisplay').textContent = encoded;
            showToast('Код сгенерирован!', 'success');
        }

        function restoreEmpireFromCode() {
            if (!empireCurrentUser) {
                showToast('Войдите в аккаунт!', 'error');
                return;
            }
            var code = document.getElementById('empireRestoreCodeInput').value.trim();
            var statusEl = document.getElementById('empireRestoreStatus');
            if (!code) {
                statusEl.textContent = 'Введите код';
                statusEl.style.color = '#ff6b4a';
                return;
            }
            try {
                var decoded = JSON.parse(decodeURIComponent(atob(code)));
                if (!decoded.owner || decoded.balance === undefined) throw new Error('Неверный формат');
                if (decoded.owner !== empireCurrentUser) {
                    statusEl.textContent = 'Ошибка: код принадлежит ' + decoded.owner;
                    statusEl.style.color = '#ff6b4a';
                    showToast('Код принадлежит другому аккаунту!', 'error');
                    return;
                }
                var userData = empireUsers[empireCurrentUser];
                if (decoded.balance === 'Infinity') userData.balance = Infinity;
                else if (typeof decoded.balance === 'number') userData.balance = decoded.balance;
                if (decoded.history) userData.transferHistory = decoded.history;
                saveEmpireUserData(empireCurrentUser);
                updateEmpireUI();
                renderEmpireTransferHistory();
                statusEl.textContent = '✅ Баланс и история восстановлены!';
                statusEl.style.color = '#59dba6';
                showToast('Данные восстановлены!', 'success');
                document.getElementById('empireRestoreCodeInput').value = '';
            } catch(e) {
                statusEl.textContent = '❌ Неверный код';
                statusEl.style.color = '#ff6b4a';
                showToast('Неверный код!', 'error');
            }
        }

        // ============================================================
        // ===== СИНХРОНИЗАЦИЯ ЧЕРЕЗ JSONBIN.IO =====
        // ============================================================
        // Используем бесплатный JSONBin.io для хранения данных
        // БИН ID для Team: 67b0c69bace1f1eb2e9ae6bc
        // БИН ID для Empire: 67b0c744ace1f1eb2e9ae8e4

        function saveTeamToCloud() {
            var key = document.getElementById('teamSyncKey').value.trim() || 'myteam2026';
            var statusEl = document.getElementById('teamSyncStatus');

            var data = {
                key: key,
                teamUsers: teamUsersData,
                empireUsers: empireUsers,
                timestamp: new Date().toISOString()
            };

            statusEl.textContent = '⏳ Сохранение...';
            statusEl.className = 'sync-status';

            fetch('https://api.jsonbin.io/v3/b/67b0c69bace1f1eb2e9ae6bc', {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json',
                    'X-Master-Key': '$2a$10$t4vZGRy3a0Z5k7Q8V9wX0eY1f2g3h4i5j6k7l8m9n0'
                },
                body: JSON.stringify(data)
            })
            .then(function(res) {
                if (!res.ok) throw new Error('Ошибка сохранения: ' + res.status);
                return res.json();
            })
            .then(function() {
                statusEl.textContent = '✅ Данные успешно сохранены в облаке! (ключ: ' + key + ')';
                statusEl.className = 'sync-status success';
                showToast('✅ Данные сохранены в облаке!', 'success');
            })
            .catch(function(err) {
                statusEl.textContent = '❌ Ошибка: ' + err.message;
                statusEl.className = 'sync-status error';
                showToast('❌ Ошибка сохранения: ' + err.message, 'error');
            });
        }

        function loadTeamFromCloud() {
            var key = document.getElementById('teamSyncKey').value.trim() || 'myteam2026';
            var statusEl = document.getElementById('teamSyncStatus');

            statusEl.textContent = '⏳ Загрузка...';
            statusEl.className = 'sync-status';

            fetch('https://api.jsonbin.io/v3/b/67b0c69bace1f1eb2e9ae6bc/latest', {
                headers: {
                    'X-Master-Key': '$2a$10$t4vZGRy3a0Z5k7Q8V9wX0eY1f2g3h4i5j6k7l8m9n0'
                }
            })
            .then(function(res) {
                if (!res.ok) throw new Error('Ошибка загрузки: ' + res.status);
                return res.json();
            })
            .then(function(data) {
                var parsed = data.record;
                if (!parsed || parsed.key !== key) {
                    throw new Error('Неверный ключ синхронизации');
                }
                
                if (parsed.teamUsers) {
                    for (var user in parsed.teamUsers) {
                        if (teamUsersData[user]) {
                            teamUsersData[user].balance = parsed.teamUsers[user].balance;
                            teamUsersData[user].inventory = parsed.teamUsers[user].inventory || [];
                            teamUsersData[user].library = parsed.teamUsers[user].library || [];
                        }
                    }
                }
                if (parsed.empireUsers) {
                    for (var user in parsed.empireUsers) {
                        if (empireUsers[user]) {
                            empireUsers[user].balance = parsed.empireUsers[user].balance;
                            empireUsers[user].transferHistory = parsed.empireUsers[user].transferHistory || [];
                        }
                    }
                }

                for (var user in teamUsersData) saveTeamUserData(user);
                for (var user in empireUsers) saveEmpireUserData(user);

                updateTeamUI();
                renderTeamShop();
                renderTeamLibrary();
                updateEmpireUI();
                updateEmpireUILocal();
                if (empireCurrentUser) {
                    updateRecipientsList();
                    updateCrossRecipients();
                    renderEmpireTransferHistory();
                }

                statusEl.textContent = '✅ Данные успешно загружены из облака! (' + new Date(parsed.timestamp).toLocaleString() + ')';
                statusEl.className = 'sync-status success';
                showToast('✅ Данные загружены из облака!', 'success');
            })
            .catch(function(err) {
                statusEl.textContent = '❌ Ошибка: ' + err.message;
                statusEl.className = 'sync-status error';
                showToast('❌ Ошибка загрузки: ' + err.message, 'error');
            });
        }

        // ============================================================
        // ===== СИНХРОНИЗАЦИЯ ДЛЯ ИМПЕРИИ =====
        // ============================================================
        function saveEmpireToCloud() {
            var key = document.getElementById('empireSyncKey').value.trim() || 'myempire2026';
            var statusEl = document.getElementById('empireSyncStatus');

            var data = {
                key: key,
                teamUsers: teamUsersData,
                empireUsers: empireUsers,
                timestamp: new Date().toISOString()
            };

            statusEl.textContent = '⏳ Сохранение...';
            statusEl.className = 'sync-status';

            fetch('https://api.jsonbin.io/v3/b/67b0c744ace1f1eb2e9ae8e4', {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json',
                    'X-Master-Key': '$2a$10$t4vZGRy3a0Z5k7Q8V9wX0eY1f2g3h4i5j6k7l8m9n0'
                },
                body: JSON.stringify(data)
            })
            .then(function(res) {
                if (!res.ok) throw new Error('Ошибка сохранения: ' + res.status);
                return res.json();
            })
            .then(function() {
                statusEl.textContent = '✅ Данные успешно сохранены в облаке! (ключ: ' + key + ')';
                statusEl.className = 'sync-status success';
                showToast('✅ Данные сохранены в облаке!', 'success');
            })
            .catch(function(err) {
                statusEl.textContent = '❌ Ошибка: ' + err.message;
                statusEl.className = 'sync-status error';
                showToast('❌ Ошибка сохранения: ' + err.message, 'error');
            });
        }

        function loadEmpireFromCloud() {
            var key = document.getElementById('empireSyncKey').value.trim() || 'myempire2026';
            var statusEl = document.getElementById('empireSyncStatus');

            statusEl.textContent = '⏳ Загрузка...';
            statusEl.className = 'sync-status';

            fetch('https://api.jsonbin.io/v3/b/67b0c744ace1f1eb2e9ae8e4/latest', {
                headers: {
                    'X-Master-Key': '$2a$10$t4vZGRy3a0Z5k7Q8V9wX0eY1f2g3h4i5j6k7l8m9n0'
                }
            })
            .then(function(res) {
                if (!res.ok) throw new Error('Ошибка загрузки: ' + res.status);
                return res.json();
            })
            .then(function(data) {
                var parsed = data.record;
                if (!parsed || parsed.key !== key) {
                    throw new Error('Неверный ключ синхронизации');
                }
                
                if (parsed.teamUsers) {
                    for (var user in parsed.teamUsers) {
                        if (teamUsersData[user]) {
                            teamUsersData[user].balance = parsed.teamUsers[user].balance;
                            teamUsersData[user].inventory = parsed.teamUsers[user].inventory || [];
                            teamUsersData[user].library = parsed.teamUsers[user].library || [];
                        }
                    }
                }
                if (parsed.empireUsers) {
                    for (var user in parsed.empireUsers) {
                        if (empireUsers[user]) {
                            empireUsers[user].balance = parsed.empireUsers[user].balance;
                            empireUsers[user].transferHistory = parsed.empireUsers[user].transferHistory || [];
                        }
                    }
                }

                for (var user in teamUsersData) saveTeamUserData(user);
                for (var user in empireUsers) saveEmpireUserData(user);

                updateTeamUI();
                renderTeamShop();
                renderTeamLibrary();
                updateEmpireUI();
                updateEmpireUILocal();
                if (empireCurrentUser) {
                    updateRecipientsList();
                    updateCrossRecipients();
                    renderEmpireTransferHistory();
                }

                statusEl.textContent = '✅ Данные успешно загружены из облака! (' + new Date(parsed.timestamp).toLocaleString() + ')';
                statusEl.className = 'sync-status success';
                showToast('✅ Данные загружены из облака!', 'success');
            })
            .catch(function(err) {
                statusEl.textContent = '❌ Ошибка: ' + err.message;
                statusEl.className = 'sync-status error';
                showToast('❌ Ошибка загрузки: ' + err.message, 'error');
            });
        }

        // ============================================================
        // ===== ПЕРЕКЛЮЧЕНИЕ МЕЖДУ САЙТАМИ =====
        // ============================================================
        function switchSite(site) {
            document.querySelectorAll('.site-container').forEach(function(el) {
                el.classList.remove('active');
            });
            document.getElementById('site-' + site).classList.add('active');
            document.querySelectorAll('.switch-btn').forEach(function(btn) {
                btn.classList.remove('active');
            });
            if (site === 'team') {
                document.getElementById('switchToTeam').classList.add('active');
            } else {
                document.getElementById('switchToEmpire').classList.add('active');
                updateCrossRecipients();
            }
        }

        // ============================================================
        // ===== ТОСТ =====
        // ============================================================
        function showToast(msg, type) {
            var toast = document.getElementById('toast');
            var toastMsg = document.getElementById('toastMsg');
            toastMsg.textContent = msg;
            toast.className = 'toast show ' + type;
            clearTimeout(toast._timer);
            toast._timer = setTimeout(function() { toast.classList.remove('show'); }, 3500);
        }

        // ============================================================
        // ===== ИНИЦИАЛИЗАЦИЯ =====
        // ============================================================
        document.addEventListener('DOMContentLoaded', function() {
            loadAllData();
            updateTeamUI();
            renderTeamShop();
            renderTeamLibrary();
            updateEmpireUI();
            updateEmpireUILocal();
            updateCrossRecipients();
            if (empireCurrentUser) {
                updateRecipientsList();
                renderEmpireTransferHistory();
            }
        });
    </script>
</body>
</html>
