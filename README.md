<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0, viewport-fit=cover">
    <title>PANA STUDIO | SUPREME EDITION</title>

    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="PANA STUDIO">
    <link rel="apple-touch-icon" href="logo14.png">

    <style>
        :root {
            --bg: #000;
            --card: #0c0c0c;
            --border: rgba(255, 255, 255, 0.1);
            --gold: linear-gradient(135deg, #bf953f 0%, #fcf6ba 30%, #b38728 50%, #fbf5b7 70%, #aa771c 100%);
            --silver: linear-gradient(135deg, #707070, #e0e0e0, #808080, #f0f0f0, #909090);
            --diamond: linear-gradient(135deg, #e0f7fa 0%, #80deea 30%, #e0f7fa 50%, #26c6da 70%, #b2ebf2 100%);
            --bronce: linear-gradient(135deg, #804a00, #b08d57, #804a00, #d9a05b, #59351a);
        }

        #ban-screen { 
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; 
            background: #000; z-index: 999999; color: #ff4444; 
            flex-direction: column; justify-content: center; align-items: center; text-align: center; padding: 20px;
        }

        html, body { 
            overflow-x: hidden; 
            width: 100%; 
            position: relative;
            margin: 0; 
            padding: 0;
            background: var(--bg);
            -webkit-user-select: none; user-select: none;
        }

        body { color: #fff; font-family: -apple-system, system-ui, sans-serif; -webkit-font-smoothing: antialiased; }
        
        .container { 
            width: 100%; 
            max-width: 450px; 
            margin: auto; 
            padding: 25px; 
            padding-bottom: 180px; 
            box-sizing: border-box; 
        }
        
        header { padding: 50px 0 30px; text-align: center; }
        .logo-pana { font-size: 42px; font-weight: 900; letter-spacing: -2px; text-transform: uppercase; margin-bottom: 8px; }
        
        #main-badge { display: inline-block; padding: 12px 30px; border-radius: 10px; font-size: 13px; font-weight: 900; text-transform: uppercase; letter-spacing: 1px; border: 1px solid var(--border); background: #111; color: #555; transition: 0.5s; }

        .view { display: none; }
        .view.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .tabs { display: flex; background: #1a1a1a; padding: 5px; border-radius: 15px; margin: 25px 0; }
        .tab-btn { flex: 1; background: none; border: none; color: #888; padding: 15px; font-size: 13px; font-weight: 700; border-radius: 12px; cursor: pointer; }
        .tab-btn.active { background: #333; color: #fff; }

        .section-title { font-size: 15px; font-weight: 800; margin: 35px 0 20px; text-transform: uppercase; border-left: 4px solid #fff; padding-left: 12px; }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .item-card { background: var(--card); border-radius: 25px; padding: 18px; border: 1px solid var(--border); text-align: center; }
        .item-img { width: 100%; border-radius: 18px; margin-bottom: 12px; }
        .price { font-size: 18px; font-weight: 800; margin-bottom: 15px; }
        .buy-btn { width: 100%; background: #fff; color: #000; border: none; padding: 14px; border-radius: 14px; font-size: 13px; font-weight: 800; cursor: pointer; text-decoration: none; display: inline-block; box-sizing: border-box; }
        .buy-btn.disabled { background: #222 !important; color: #555 !important; cursor: not-allowed; border: 1px solid #333; }

        @keyframes memShimmer { 0% { background-position: -200% 0; } 100% { background-position: 200% 0; } }
        .metal-plate { position: relative; border-radius: 25px; padding: 45px 25px; margin-bottom: 25px; text-align: center; overflow: hidden; border: 1px solid rgba(255,255,255,0.15); box-shadow: 0 15px 35px rgba(0,0,0,0.6); background-size: 200% auto !important; animation: memShimmer 5s infinite linear; }

        .dueño-oro { background: var(--gold); color: #000; text-decoration: none; display: flex; flex-direction: column; align-items: center; justify-content: center; margin-bottom: 25px; }
        .plate-bronce { background: var(--bronce); color: #fff; }
        .plate-plata { background: var(--silver); color: #000; }
        .plate-oro { background: var(--gold); color: #000; }
        .plate-diamante { background: var(--diamond); color: #000; }
        .plate-leyenda { background: #000; color: #ff00ff; border: 2px solid #ff00ff; }
        .plate-text { font-size: 22px; font-weight: 900; text-transform: uppercase; }

        .download-row { display: flex; align-items: center; background: #0c0c0c; padding: 18px; border-radius: 25px; margin-bottom: 15px; border: 1px solid var(--border); }
        .download-row img { width: 60px; height: 60px; border-radius: 15px; margin-right: 18px; object-fit: cover; }
        .download-row .download-info { flex-grow: 1; }
        .download-row h4 { margin: 0; font-size: 16px; }
        .download-row p { margin: 4px 0 0; font-size: 11px; color: #666; line-height: 1.2; }
        .dl-btn { width: 85px; padding: 12px; text-align: center; border-radius: 13px; font-size: 11px; font-weight: 900; cursor: pointer; text-decoration: none; border: none; }

        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.98); z-index: 5000; justify-content: center; align-items: center; backdrop-filter: blur(10px); }
        .modal-box { width: 85%; background: #0a0a0a; border-radius: 40px; padding: 50px; text-align: center; border: 1px solid var(--border); }
        .paypal-btn { display: block; background: #fff; color: #000; text-decoration: none; padding: 18px; border-radius: 18px; font-weight: 800; font-size: 15px; margin-top: 30px; }
        .spinner { border: 4px solid #222; border-top: 4px solid #fff; border-radius: 50%; width: 40px; height: 40px; animation: spin 1s linear infinite; margin: 0 auto 25px; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        /* AJUSTE BARRA NAVEGACIÓN INFERIOR */
        .bottom-nav { 
            position: fixed; 
            bottom: max(10px, env(safe-area-inset-bottom)); /* BAJADO MÁS CERCA DEL BORDE */
            left: 50%; 
            transform: translateX(-50%); 
            width: 92%; 
            height: 70px; 
            background: rgba(15,15,15,0.9); 
            backdrop-filter: blur(25px); 
            -webkit-backdrop-filter: blur(25px);
            border-radius: 35px; 
            border: 1px solid var(--border); 
            display: flex; 
            justify-content: space-around; 
            align-items: center; 
            z-index: 9999; 
        }
        .nav-link { background: none; border: none; color: #555; font-size: 11px; font-weight: 700; text-transform: uppercase; cursor: pointer; }
        .nav-link.active { color: #fff; }

        #dl-frame { display: none; }
    </style>
</head>
<body oncontextmenu="return false;">

<iframe id="dl-frame"></iframe>

<div id="ban-screen">
    <h1 style="font-size: 60px;">🚫</h1>
    <h2 style="font-weight: 900;">ACCESO BLOQUEADO</h2>
    <p style="font-size: 14px; max-width: 80%;">Tu acceso ha sido revocado permanentemente por intentar clonar el sitio.</p>
</div>

<div id="app-content" class="container">
    <header>
        <div class="logo-pana">PANA STUDIO</div>
        <div id="main-badge">NO VERIFICADO</div>
    </header>

    <div id="view-inicio" class="view active">
        <img src="logo14.png" style="width:100%; border-radius:30px; margin-bottom:25px; border: 1px solid var(--border);">
        <a href="https://www.tiktok.com/@momkey_sb?_r=1&_t=ZS-95xyg1rSmlF" target="_blank" class="metal-plate dueño-oro">
            <div style="font-size: 12px; font-weight: 900; opacity: 0.7;">DUEÑO DEL PROYECTO</div>
            <div style="font-size: 24px; font-weight: 900;">PANA STUDIOS</div>
        </a>
        <div class="item-card" style="text-align: left; background: #050505;">
            <h3 style="margin:0; font-size:16px;">PORTAL VIP ADRIAN</h3>
            <p style="color:#666; font-size:13px; margin-top:8px;">Selecciona tus créditos o membresías.</p>
        </div>
    </div>

    <div id="view-tienda" class="view">
        <div class="tabs">
            <button class="tab-btn active" onclick="subTab('items')">TARJETAS</button>
            <button class="tab-btn" onclick="subTab('mems')">PLACAS VIP</button>
        </div>

        <div id="sub-items">
            <div class="section-title">ROBLOX (7)</div>
            <div class="grid">
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$0.79</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$3.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$7.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$15.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$39.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$79.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="roblox_logo.png" class="item-img"><div class="price">$159.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
            </div>
            <div class="section-title">FORTNITE (4)</div>
            <div class="grid">
                <div class="item-card"><img src="fortnite_vbucks.png" class="item-img"><div class="price">$7.19</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="fortnite_vbucks.png" class="item-img"><div class="price">$18.39</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="fortnite_vbucks.png" class="item-img"><div class="price">$29.59</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="fortnite_vbucks.png" class="item-img"><div class="price">$71.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
            </div>
            <div class="section-title">FREE FIRE (6)</div>
            <div class="grid">
                <div class="item-card"><img src="ff_diamonds.png" class="item-img"><div class="price">$0.88</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="ff_diamonds.png" class="item-img"><div class="price">$2.56</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="ff_diamonds.png" class="item-img"><div class="price">$4.32</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="ff_diamonds.png" class="item-img"><div class="price">$8.79</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="ff_diamonds.png" class="item-img"><div class="price">$17.59</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
                <div class="item-card"><img src="ff_diamonds.png" class="item-img"><div class="price">$39.99</div><button class="buy-btn" onclick="openGate()">BUY</button></div>
            </div>
        </div>

        <div id="sub-mems" style="display:none;">
            <div class="metal-plate plate-bronce"><div class="plate-text">MEMBRESÍA BRONCE</div><button class="buy-btn" style="margin-top:20px;" onclick="setRank('BRONCE','var(--bronce)')">ACTIVAR</button></div>
            <div class="metal-plate plate-plata"><div class="plate-text">MEMBRESÍA PLATA</div><button class="buy-btn" style="margin-top:20px;" onclick="setRank('PLATA','var(--silver)')">ACTIVAR</button></div>
            <div class="metal-plate plate-oro"><div class="plate-text">MEMBRESÍA ORO</div><button class="buy-btn" style="margin-top:20px;" onclick="setRank('ORO','var(--gold)')">ACTIVAR</button></div>
            <div class="metal-plate plate-diamante"><div class="plate-text">MEMBRESÍA DIAMANTE</div><button class="buy-btn" style="margin-top:20px;" onclick="setRank('DIAMANTE','var(--diamond)')">ACTIVAR</button></div>
            <div class="metal-plate plate-leyenda"><div class="plate-text">MEMBRESÍA LEYENDA</div><button class="buy-btn" style="margin-top:20px; background:#ff00ff; color:#fff;" onclick="setRank('LEYENDA','#ff00ff')">ACTIVAR</button></div>
        </div>
    </div>

    <div id="view-descargas" class="view">
        <div class="section-title">SERVIDOR ELITE</div>
        <div class="metal-plate plate-diamante" style="padding: 30px; text-align: left;">
            <div style="font-weight: 900; font-size: 22px;">CARPETA PRINCIPAL</div>
            <p style="font-size: 13px; margin-bottom: 25px;">Acceso total a Gofile.</p>
            <a href="javascript:void(0)" onclick="dl_sec('https://gofile.io/d/KlIC47')" class="buy-btn" style="text-align: center;">ABRIR SERVIDOR</a>
        </div>

        <div class="section-title">DNS ANTI-REVOKE</div>
        <div class="download-row">
            <img src="g1.png">
            <div class="download-info"><h4>CONFIG DNS</h4><p>INSTALACIÓN DIRECTA</p></div>
            <a href="javascript:void(0)" onclick="dl_dns('https://github.com/dns-khoindvn/top-country-stats/releases/download/DNS/khoindvn.io.vn.mobileconfig')" class="dl-btn" style="background:#fff; color:#000;">INSTALAR</a>
        </div>

        <div class="section-title">CATÁLOGO ANDROID (APK)</div>
        <div class="download-row"><img src="logo233.png"><div class="download-info"><h4>Game Guardian</h4><p>ZIP</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/hz2wtxd79sln791/GameGuardian.101.1.apk.zip/file')" class="dl-btn" style="background:#00ff00; color:#000;">ZIP</a></div>
        <div class="download-row"><img src="logo234.png"><div class="download-info"><h4>Virtual Space</h4><p>APK</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/xp6q6p858dglp38/Virtual_Space_1.2.0_gg_signed.apk/file')" class="dl-btn" style="background:#00ff00; color:#000;">APK</a></div>
        <div class="download-row"><img src="logo230.png"><div class="download-info"><h4>HappyMod</h4><p>APK</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/c0ludb1qvhd32de/HappyMod-3-3-1.apk/file')" class="dl-btn" style="background:#00ff00; color:#000;">APK</a></div>

        <div class="section-title">CATÁLOGO IPA (19 DISPONIBLES)</div>
        <div class="download-row"><img src="x3.png"><div class="download-info"><h4>E•Sign</h4><p>Directo</p></div><a href="javascript:void(0)" onclick="dl_sec('https://api.khoindvn.io.vn/jCh80j')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="K1.png"><div class="download-info"><h4>K•Sign</h4><p>Exclusivo</p></div><a href="javascript:void(0)" onclick="dl_sec('https://api.khoindvn.io.vn/1TVLIL')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="C15.png"><div class="download-info"><h4>Idle Drift</h4><p>Mod</p></div><a href="javascript:void(0)" onclick="dl_sec('https://s3.glehack.site/ipas/com.idle.drift/Idle_Drift_v1.0.1%5BURSAxGLE%5D.ipa')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="F1.png"><div class="download-info"><h4>Driving Zone</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/qufht79c5xjvfo1/Driving-Zone-Offroad-Lite.ipa/file')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="F2.png"><div class="download-info"><h4>Chrome Valley</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/dsux9er39ttrzqo/Chrome-Valley-Custom.ipa/file')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="F3.png"><div class="download-info"><h4>Free VPN</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/izy8609u4ryu6hc/Free-VPN-CN.ipa/file')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="x7.png"><div class="download-info"><h4>Scarlet</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/6mlo13p9hskggne/Scarlet%25282%2529.ipa/file')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="x5.png"><div class="download-info"><h4>Feather</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/6jra7duvfkqfqmw/Feather-LB7.ipa/file')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="x1.png"><div class="download-info"><h4>FREE FIRE ZORO</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://i.authtool.app/ios/69bd3fc0b4de5e3eee8e525b')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>
        <div class="download-row"><img src="x2.png"><div class="download-info"><h4>GBox iOS</h4><p>IPA</p></div><a href="javascript:void(0)" onclick="dl_sec('https://www.mediafire.com/file/7hk596gcul4fc2v/Gbox.ipa/file')" class="dl-btn" style="background:#00ff00; color:#000;">IPA</a></div>

        <div class="section-title">SIN FIRMA</div>
        <div class="download-row"><img src="c1.png"><div class="download-info"><h4>GTA SA</h4><p>WAIT</p></div><button class="dl-btn disabled">WAIT</button></div>
        <div class="download-row"><img src="c3.png"><div class="download-info"><h4>CarX Street</h4><p>WAIT</p></div><button class="dl-btn disabled">WAIT</button></div>
        <div class="download-row"><img src="c4.png"><div class="download-info"><h4>Minecraft</h4><p>WAIT</p></div><button class="dl-btn disabled">WAIT</button></div>
        <div class="download-row"><img src="c5.png"><div class="download-info"><h4>BASEBALL 9</h4><p>WAIT</p></div><button class="dl-btn disabled">WAIT</button></div>
        <div class="download-row"><img src="c6.png"><div class="download-info"><h4>NBA 2K20</h4><p>WAIT</p></div><button class="dl-btn disabled">WAIT</button></div>
        <div class="download-row"><img src="c7.png"><div class="download-info"><h4>Asphalt</h4><p>WAIT</p></div><button class="dl-btn disabled">WAIT</button></div>
    </div>
</div>

<div id="gate" class="modal">
    <div class="modal-box">
        <div id="loading-gate" style="display:none;"><div class="spinner"></div><p id="gate-status">VERIFICANDO PAGO...</p></div>
        <div id="pay-gate">
            <h2 style="font-size:22px; font-weight:900;">PAGO SEGURO</h2>
            <a href="https://www.paypal.me/CarmenDeleoncepeda" target="_blank" class="paypal-btn" onclick="startProcess()">PAYPAL</a>
            <p onclick="closeGate()" style="margin-top:25px; font-size:13px; color:#444; cursor:pointer;">VOLVER</p>
        </div>
    </div>
</div>

<nav class="bottom-nav">
    <button class="nav-link active" onclick="nav('inicio', this)">INICIO</button>
    <button class="nav-link" onclick="nav('tienda', this)">TIENDA</button>
    <button class="nav-link" onclick="nav('descargas', this)">DESCARGAS</button>
</nav>

<script>
    function dl_sec(l) { window.open(l, '_blank'); }
    function dl_dns(l) { document.getElementById('dl-frame').src = l; }

    (function() {
        const host = window.location.hostname;
        const valid = ['neocities.org', 'localhost', '127.0.0.1'];
        if(!valid.some(v => host.includes(v))) {
            document.getElementById('app-content').style.display = 'none';
            document.getElementById('ban-screen').style.display = 'flex';
        }
    })();

    let pendingRank = ""; let pendingStyle = "";
    window.onload = function() {
        const r = localStorage.getItem('panaRank');
        const s = localStorage.getItem('panaStyle');
        if(r && s) updateBadge(r, s);
    }
    function setRank(n, s) { pendingRank = n; pendingStyle = s; openGate(); }
    function openGate() { document.getElementById('gate').style.display = 'flex'; }
    function closeGate() { document.getElementById('gate').style.display = 'none'; document.getElementById('loading-gate').style.display = 'none'; document.getElementById('pay-gate').style.display = 'block'; }
    function startProcess() {
        document.getElementById('pay-gate').style.display = 'none';
        document.getElementById('loading-gate').style.display = 'block';
        setTimeout(() => {
            document.getElementById('gate-status').innerText = "¡PROCESADO!";
            if(pendingRank) {
                localStorage.setItem('panaRank', pendingRank);
                localStorage.setItem('panaStyle', pendingStyle);
                updateBadge(pendingRank, pendingStyle);
            }
            setTimeout(closeGate, 1500);
        }, 3000);
    }
    function updateBadge(n, s) {
        const b = document.getElementById('main-badge');
        b.innerText = "RANGO: " + n; b.style.background = s;
        b.style.color = (n === 'LEYENDA' ? '#fff' : '#000');
    }
    function nav(id, btn) {
        document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        document.getElementById('view-' + id).classList.add('active');
        btn.classList.add('active');
    }
    function subTab(id) {
        document.getElementById('sub-items').style.display = id === 'items' ? 'block' : 'none';
        document.getElementById('sub-mems').style.display = id === 'mems' ? 'block' : 'none';
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        event.target.classList.add('active');
    }
</script>
</body>
</html>
