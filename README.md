[index.html](https://github.com/user-attachments/files/25271941/index.html)
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#8a05be">
    
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='%238a05be'><path d='M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4z'/></svg>">
    <title>Soberania Financeira v1.3.0 | WL SYSTEM</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800;900&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        :root {
            --p: #8a05be; --pd: #6a0492; --pl: #f4e8fa;
            --bg: #f8f9fd; --tx: #1c1c1c; --tx-s: #64748b;
            --sc: #22c55e; --dg: #ff3b30; --wn: #f59e0b;
            --border: #e2e8f0; --card: #ffffff;
            --sh: 0 10px 25px rgba(0,0,0,0.04);
            --radius-lg: 32px; --radius-md: 22px;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; outline: none; }
        html, body { height: 100%; width: 100%; overflow-x: hidden; }
        body { background-color: var(--bg); color: var(--tx); font-family: 'Inter', sans-serif; display: flex; justify-content: center; padding: env(safe-area-inset-top) 15px env(safe-area-inset-bottom); }

        #wl-toast-container { position: fixed; top: 30px; left: 0; right: 0; z-index: 999999; pointer-events: none; display: flex; flex-direction: column; align-items: center; gap: 10px; }
        .wl-toast { background: rgba(28, 28, 28, 0.95); backdrop-filter: blur(15px); color: white; padding: 16px 32px; border-radius: 50px; font-size: 0.85rem; font-weight: 800; text-align: center; box-shadow: 0 20px 40px rgba(0,0,0,0.25); border: 1px solid rgba(255,255,255,0.15); animation: toastEnter 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; max-width: 85%; pointer-events: auto; }
        @keyframes toastEnter { from { opacity: 0; transform: translateY(-30px) scale(0.8); } to { opacity: 1; transform: translateY(0) scale(1); } }
        @keyframes slideUp { from { transform: translateY(30px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        @keyframes pulse { 0% { opacity: 1; transform: scale(1); } 50% { opacity: 0.7; transform: scale(0.96); } 100% { opacity: 1; transform: scale(1); } }
        @keyframes float { 0% { transform: translateY(0px); } 50% { transform: translateY(-5px); } 100% { transform: translateY(0px); } }

        #splash { position: fixed; inset: 0; background: #fff; z-index: 100000; display: flex; flex-direction: column; justify-content: center; align-items: center; transition: opacity 0.8s ease, visibility 0.8s; }
        .splash-logo { width: 80px; height: 80px; fill: var(--p); animation: pulse 2s infinite ease-in-out; }
        .version-tag { margin-top: 25px; font-size: 0.65rem; letter-spacing: 6px; font-weight: 900; color: var(--p); opacity: 0.5; text-transform: uppercase; }

        #auth-screen { position: fixed; inset: 0; background: #fff; z-index: 50000; display: none; flex-direction: column; justify-content: center; align-items: center; padding: 30px; }
        .auth-card { width: 100%; max-width: 380px; text-align: center; animation: slideUp 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
        .auth-brand { font-size: 2.4rem; font-weight: 900; color: var(--p); margin-bottom: 40px; letter-spacing: -2px; }

        #app { width: 100%; max-width: 480px; display: none; flex-direction: column; opacity: 0; transition: opacity 0.6s ease; }
        #app.visible { display: flex; opacity: 1; }

        .nav-container { position: sticky; top: 12px; z-index: 9000; margin: 12px 0 28px; background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border-radius: var(--radius-md); padding: 7px; display: flex; border: 1px solid var(--border); box-shadow: var(--sh); }
        .nav-btn { flex: 1; border: none; background: transparent; padding: 16px 5px; font-size: 0.78rem; font-weight: 800; color: var(--tx-s); cursor: pointer; border-radius: 18px; transition: 0.3s; }
        .nav-btn.active { background: var(--p); color: white; box-shadow: 0 8px 16px rgba(138,5,190,0.2); }

        .hero { background: linear-gradient(155deg, var(--p), var(--pd)); color: white; padding: 45px 30px; border-radius: var(--radius-lg); text-align: center; margin-bottom: 30px; box-shadow: 0 20px 40px rgba(138, 5, 190, 0.2); }
        .hero-label { font-size: 0.68rem; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; opacity: 0.9; }
        .hero-value { font-size: 2.8rem; font-weight: 900; margin: 10px 0; letter-spacing: -1px; }
        .hero-progress { background: rgba(255,255,255,0.2); height: 10px; border-radius: 30px; margin-top: 20px; overflow: hidden; }
        .hero-bar { height: 100%; background: #fff; width: 0%; border-radius: 30px; transition: width 2s cubic-bezier(0.2, 1, 0.3, 1); }

        .chart-container { display: flex; justify-content: center; align-items: center; margin-bottom: 40px; }
        .chart-wrapper { position: relative; width: 180px; height: 180px; }

        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 30px; }
        .stat-card { background: var(--card); padding: 25px 20px; border-radius: 30px; border: 1px solid var(--border); text-align: center; box-shadow: var(--sh); }
        .stat-card.full { grid-column: span 2; display: flex; justify-content: space-between; align-items: center; text-align: left; padding: 30px; border-left: 10px solid var(--p); }
        .stat-label { font-size: 0.62rem; font-weight: 900; color: var(--tx-s); text-transform: uppercase; margin-bottom: 5px; display: block; }
        .stat-value { font-size: 1.25rem; font-weight: 900; color: var(--p); }

        .summary-box { background: #fff; border-radius: 32px; padding: 28px; margin-bottom: 40px; border: 1px solid var(--border); }
        .summary-title { font-size: 0.78rem; font-weight: 900; color: var(--p); text-transform: uppercase; margin-bottom: 12px; display: flex; align-items: center; gap: 8px; }
        .summary-text { font-size: 0.92rem; line-height: 1.6; color: #475569; }

        .form-card { background: var(--card); padding: 30px; border-radius: var(--radius-lg); border: 1px solid var(--border); margin-bottom: 25px; box-shadow: var(--sh); }
        input { width: 100%; padding: 20px; border: 2px solid #f1f5f9; border-radius: 20px; font-size: 1.1rem; font-weight: 800; color: var(--tx); margin-bottom: 18px; background: #fbfcfe; transition: 0.3s; }
        input:focus { border-color: var(--p); background: #fff; }
        
        .btn { width: 100%; padding: 22px; border: none; border-radius: 22px; font-size: 1.05rem; font-weight: 900; cursor: pointer; transition: 0.3s; display: flex; justify-content: center; align-items: center; gap: 12px; }
        .btn-p { background: var(--p); color: white; box-shadow: 0 10px 20px rgba(138,5,190,0.15); }
        .btn-s { background: var(--sc); color: white; }
        .btn-ghost { background: transparent; color: var(--tx-s); font-size: 0.88rem; font-weight: 700; }

        .list-item { background: white; padding: 22px; border-radius: 26px; margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; border: 1px solid var(--border); border-left: 7px solid var(--p); animation: slideUp 0.4s ease forwards; }
        .item-data small { font-size: 0.65rem; color: var(--tx-s); font-weight: 800; text-transform: uppercase; display: block; margin-bottom: 4px; }
        .item-data b { font-size: 1.1rem; font-weight: 900; }
        .item-del { border: none; background: #fff0f0; color: var(--dg); width: 44px; height: 44px; border-radius: 16px; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 1.2rem; }

        .modal { position: fixed; inset: 0; background: rgba(0,0,0,0.6); backdrop-filter: blur(10px); display: none; z-index: 100000; }
        .modal-body { position: absolute; bottom: 0; left: 50%; transform: translateX(-50%) translateY(100%); background: white; width: 100%; max-width: 480px; border-radius: 40px 40px 0 0; padding: 35px 25px 50px; transition: 0.5s cubic-bezier(0.16, 1, 0.3, 1); }
        .modal-body.active { transform: translateX(-50%) translateY(0); }
        
        .cat-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; }
        .cat-item { background: #f8fafc; padding: 18px 10px; border-radius: 22px; text-align: center; cursor: pointer; border: 2px solid transparent; transition: 0.2s; }
        .cat-item .icon-box { width: 50px; height: 50px; border-radius: 16px; background: white; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; margin: 0 auto 8px; box-shadow: 0 4px 10px rgba(0,0,0,0.02); }
        .cat-item label { font-size: 0.65rem; font-weight: 800; color: var(--tx-s); text-transform: uppercase; }
        
        .cat-item[data-theme="blue"] .icon-box { color: #0ea5e9; }
        .cat-item[data-theme="orange"] .icon-box { color: var(--wn); }
        .cat-item[data-theme="red"] .icon-box { color: var(--dg); }
        .cat-item[data-theme="purple"] .icon-box { color: var(--p); }
        .cat-item[data-theme="green"] .icon-box { color: var(--sc); }

        .invest-link { display: flex; align-items: center; justify-content: space-between; background: #f8fafc; padding: 18px; border-radius: 18px; margin-bottom: 10px; text-decoration: none; color: var(--tx); font-weight: 800; font-size: 0.9rem; border: 1px solid var(--border); transition: 0.2s; }
        .invest-link:hover { border-color: var(--p); background: var(--pl); }

        footer { text-align: center; padding: 40px 20px; font-size: 0.65rem; color: #cbd5e1; font-weight: 900; letter-spacing: 4px; text-transform: uppercase; }
        .no-data { text-align: center; padding: 40px; color: #cbd5e1; font-weight: 800; font-size: 0.75rem; text-transform: uppercase; }
    </style>
</head>
<body>

    <div id="wl-toast-container"></div>

    <div id="splash">
        <svg class="splash-logo" viewBox="0 0 24 24"><path d="M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4zm0 6c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3z"/></svg>
        <div class="version-tag">WL SYSTEM • v1.3.0</div>
    </div>

    <div id="auth-screen">
        <div class="auth-card" id="view-login">
            <div class="auth-brand">Soberania</div>
            <input type="email" id="log-email" placeholder="E-mail">
            <input type="password" id="log-pass" placeholder="Senha">
            <button class="btn btn-p" onclick="engine.auth.submitLogin()">Entrar</button>
            <button class="btn btn-ghost" onclick="engine.auth.switch('register')">Criar nova conta</button>
        </div>
        <div class="auth-card" id="view-register" style="display:none;">
            <div class="auth-brand">Nova Conta</div>
            <input type="text" id="reg-user" placeholder="Nome de Usuário">
            <input type="email" id="reg-email" placeholder="E-mail Válido">
            <input type="password" id="reg-pass" placeholder="Senha">
            <input type="password" id="reg-confirm" placeholder="Confirmar Senha">
            <button class="btn btn-p" onclick="engine.auth.submitRegister()">Confirmar Cadastro</button>
            <button class="btn btn-ghost" onclick="engine.auth.switch('login')">Já tenho conta</button>
        </div>
    </div>

    <div id="app">
        <nav class="nav-container">
            <button class="nav-btn active" onclick="engine.ui.tab('dash', this)">Início</button>
            <button class="nav-btn" onclick="engine.ui.tab('reserva', this)">Aportes</button>
            <button class="nav-btn" onclick="engine.ui.tab('gastos', this)">Gastos</button>
            <button class="nav-btn" onclick="engine.ui.tab('perfil', this)">Perfil</button>
        </nav>

        <main>
            <section id="tab-dash">
                <div class="hero">
                    <span class="hero-label">Disponível Real (Folga + Reserva)</span>
                    <div class="hero-value" id="disp-livre">R$ 0,00</div>
                    <div class="hero-progress"><div id="disp-bar" class="hero-bar"></div></div>
                    <div style="margin-top:12px; font-weight:900; font-size:0.75rem;" id="disp-pct">0.00% DA META</div>
                </div>

                <div class="chart-container"><div class="chart-wrapper"><canvas id="mainDoughnut"></canvas></div></div>

                <div class="stats-grid">
                    <div class="stat-card full">
                        <div><span class="stat-label">Patrimônio Acumulado (Aportes)</span><span class="stat-value" id="disp-total" style="color:var(--p); font-size:1.5rem;">R$ 0,00</span></div>
                        <div style="font-size:2rem; animation: float 3s infinite ease-in-out;">💼</div>
                    </div>
                    <div class="stat-card"><span class="stat-label">Total Gastos</span><span class="stat-value" id="disp-gastos" style="color:var(--dg)">R$ 0,00</span></div>
                    <div class="stat-card"><span class="stat-label">Falta p/ Meta</span><span class="stat-value" id="disp-falta">R$ 0,00</span></div>
                </div>

                <button class="btn btn-p" onclick="engine.ui.modalInvest(true)" style="margin-bottom: 30px; background: #1c1c1c;">🎯 Onde Investir?</button>

                <div class="summary-box">
                    <div class="summary-title">Seu Resumo</div>
                    <div class="summary-text" id="summary-data">Aguardando dados...</div>
                </div>
            </section>

            <section id="tab-reserva" style="display:none;">
                <div class="form-card">
                    <span class="stat-label">Valor do Aporte</span>
                    <input type="text" id="in-res-val" placeholder="R$ 0,00" oninput="engine.utils.mask(this)">
                    <button class="btn btn-s" onclick="engine.data.create('res')">Confirmar Aporte</button>
                </div>
                <div id="list-reserva"></div>
            </section>

            <section id="tab-gastos" style="display:none;">
                <div class="form-card">
                    <span class="stat-label">Valor do Gasto</span>
                    <input type="text" id="in-gas-val" placeholder="R$ 0,00" oninput="engine.utils.mask(this)">
                    <span class="stat-label">Escolha a Categoria</span>
                    <button class="btn" id="btn-cat-trigger" onclick="engine.ui.modal(true)" style="background:#f8fafc; border:2px solid #f1f5f9; justify-content:space-between; margin-bottom:20px; color:var(--tx-s);">
                        <span id="label-cat">Selecionar...</span><span>▼</span>
                    </button>
                    <input type="hidden" id="in-gas-cat">
                    <button class="btn btn-p" onclick="engine.data.create('gas')">Salvar Gasto</button>
                </div>
                <div id="list-gastos"></div>
            </section>

            <section id="tab-perfil" style="display:none;">
                <div class="form-card" style="text-align:center;">
                    <div id="u-avatar" style="width:70px; height:70px; background:var(--p); color:white; border-radius:24px; display:flex; align-items:center; justify-content:center; margin:0 auto 15px; font-weight:900; font-size:1.8rem;">?</div>
                    <b id="u-name">-</b><br><small id="u-mail">-</small>
                </div>
                <div class="form-card">
                    <span class="stat-label">Renda Mensal Estipulada</span>
                    <input type="text" id="set-renda" placeholder="R$ 0,00" oninput="engine.utils.mask(this)">
                    <span class="stat-label">Meta de Independência</span>
                    <input type="text" id="set-meta" placeholder="R$ 0,00" oninput="engine.utils.mask(this)">
                    <button class="btn btn-p" onclick="engine.data.saveSettings()">Salvar Perfil</button>
                    <button class="btn btn-ghost" onclick="engine.auth.logout()" style="margin-top:20px; color:var(--dg)">Sair</button>
                </div>
            </section>
        </main>
        <footer>WL SYSTEM ENGINE v1.3.0</footer>
    </div>

    <div id="modal-cat" class="modal" onclick="engine.ui.modal(false)">
        <div class="modal-body" id="modal-node" onclick="event.stopPropagation()">
            <div style="width:40px; height:5px; background:#eee; border-radius:10px; margin:0 auto 25px;"></div>
            <div class="cat-grid">
                <div class="cat-item" data-theme="blue" onclick="engine.data.selectCat('Moradia','🏠')"><div class="icon-box">🏠</div><label>Casa</label></div>
                <div class="cat-item" data-theme="orange" onclick="engine.data.selectCat('Comida','🍴')"><div class="icon-box">🍴</div><label>Comida</label></div>
                <div class="cat-item" data-theme="blue" onclick="engine.data.selectCat('Transporte','🚗')"><div class="icon-box">🚗</div><label>Transp.</label></div>
                <div class="cat-item" data-theme="purple" onclick="engine.data.selectCat('Lazer','🎡')"><div class="icon-box">🎡</div><label>Lazer</label></div>
                <div class="cat-item" data-theme="orange" onclick="engine.data.selectCat('Fixos','⚡')"><div class="icon-box">⚡</div><label>Fixos</label></div>
                <div class="cat-item" data-theme="red" onclick="engine.data.selectCat('Saúde','💊')"><div class="icon-box">💊</div><label>Saúde</label></div>
                <div class="cat-item" data-theme="green" onclick="engine.data.selectCat('Educação','📚')"><div class="icon-box">📚</div><label>Educ.</label></div>
                <div class="cat-item" data-theme="purple" onclick="engine.data.selectCat('Compras','🛍️')"><div class="icon-box">🛍️</div><label>Compras</label></div>
                <div class="cat-item" data-theme="blue" onclick="engine.data.selectCat('Outros','➕')"><div class="icon-box">➕</div><label>Outros</label></div>
            </div>
        </div>
    </div>

    <div id="modal-invest" class="modal" onclick="engine.ui.modalInvest(false)">
        <div class="modal-body" id="modal-invest-node" onclick="event.stopPropagation()">
            <div style="width:40px; height:5px; background:#eee; border-radius:10px; margin:0 auto 20px;"></div>
            <h3 style="margin-bottom:8px;">Onde Investir?</h3>
            <p style="font-size:0.8rem; color:var(--tx-s); margin-bottom:20px;">Consulte fontes oficiais atualizadas:</p>
            <div class="invest-list">
                <a href="https://www.tesourodireto.com.br/titulos/precos-e-taxas.htm" target="_blank" class="invest-link"><span>🏦 Tesouro Direto (Oficial)</span><span>↗️</span></a>
                <a href="https://www.b3.com.br/pt_br/produtos-e-servicos/investimento/renda-variavel/" target="_blank" class="invest-link"><span>📈 Ações e FIIs (B3)</span><span>↗️</span></a>
                <a href="https://meubolsoemdia.com.br/" target="_blank" class="invest-link"><span>🎓 Educação Financeira</span><span>↗️</span></a>
            </div>
            <button class="btn btn-ghost" onclick="engine.ui.modalInvest(false)" style="margin-top:10px;">Fechar</button>
        </div>
    </div>

    <script>
        const engine = {
            state: { activeUser: null, chart: null },
            toast: (msg) => {
                const container = document.getElementById('wl-toast-container');
                const toast = document.createElement('div');
                toast.className = 'wl-toast';
                toast.innerText = msg;
                container.appendChild(toast);
                setTimeout(() => {
                    toast.style.opacity = '0';
                    toast.style.transform = 'translateY(-20px) scale(0.9)';
                    setTimeout(() => toast.remove(), 500);
                }, 3000);
            },
            utils: {
                mask: (el) => {
                    let v = el.value.replace(/\D/g, "");
                    if (!v) { el.value = ""; return; }
                    el.value = (parseFloat(v) / 100).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
                },
                parse: (s) => parseFloat(String(s || "0").replace(/[R$\s.]/g, "").replace(",", ".")) || 0,
                format: (n) => n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' })
            },
            data: {
                db: () => JSON.parse(localStorage.getItem('wl_sob_db_v1') || '{}'),
                getUser: () => engine.data.db()[engine.state.activeUser] || null,
                sync: (data) => {
                    let db = engine.data.db();
                    db[engine.state.activeUser] = data;
                    localStorage.setItem('wl_sob_db_v1', JSON.stringify(db));
                    engine.ui.refresh();
                },
                create: (type) => {
                    let u = engine.data.getUser();
                    const now = new Date().toLocaleDateString('pt-BR');
                    if (type === 'gas') {
                        const val = engine.utils.parse(document.getElementById('in-gas-val').value);
                        const cat = document.getElementById('in-gas-cat').value;
                        if (val <= 0 || !cat) { engine.toast("⚠️ Valor e categoria obrigatórios"); return; }
                        u.h_gastos.unshift({ id: Date.now(), val, cat, date: now });
                        document.getElementById('in-gas-val').value = "";
                        document.getElementById('label-cat').innerText = "Selecionar...";
                        engine.toast("✅ Gasto Registrado!");
                    } else {
                        const val = engine.utils.parse(document.getElementById('in-res-val').value);
                        if (val <= 0) { engine.toast("⚠️ Valor de aporte inválido"); return; }
                        u.h_reserva.unshift({ id: Date.now(), val, date: now });
                        document.getElementById('in-res-val').value = "";
                        engine.toast("💰 Aporte Salvo!");
                    }
                    engine.data.sync(u);
                },
                delete: (id, type) => {
                    let u = engine.data.getUser();
                    if (type === 'g') u.h_gastos = u.h_gastos.filter(x => x.id !== id);
                    else u.h_reserva = u.h_reserva.filter(x => x.id !== id);
                    engine.data.sync(u);
                    engine.toast("🗑️ Item Removido");
                },
                selectCat: (n, e) => {
                    document.getElementById('label-cat').innerText = `${e} ${n}`;
                    document.getElementById('in-gas-cat').value = n;
                    engine.ui.modal(false);
                },
                saveSettings: () => {
                    let u = engine.data.getUser();
                    u.renda = document.getElementById('set-renda').value;
                    u.meta = document.getElementById('set-meta').value;
                    engine.data.sync(u);
                    engine.toast("💾 Perfil Atualizado!");
                }
            },
            ui: {
                tab: (id, btn) => {
                    document.querySelectorAll('section').forEach(s => s.style.display = 'none');
                    document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
                    document.getElementById('tab-' + id).style.display = 'block';
                    btn.classList.add('active');
                    if (id === 'dash') engine.ui.refresh();
                },
                modal: (show) => {
                    const m = document.getElementById('modal-cat');
                    const b = document.getElementById('modal-node');
                    if (show) { m.style.display = 'block'; setTimeout(() => b.classList.add('active'), 10); }
                    else { b.classList.remove('active'); setTimeout(() => m.style.display = 'none', 500); }
                },
                modalInvest: (show) => {
                    const m = document.getElementById('modal-invest');
                    const b = document.getElementById('modal-invest-node');
                    if (show) { m.style.display = 'block'; setTimeout(() => b.classList.add('active'), 10); }
                    else { b.classList.remove('active'); setTimeout(() => m.style.display = 'none', 500); }
                },
                refresh: () => {
                    const d = engine.data.getUser();
                    if (!d) return;
                    const tG = d.h_gastos.reduce((a, b) => a + b.val, 0);
                    const tR = d.h_reserva.reduce((a, b) => a + b.val, 0);
                    const ren = engine.utils.parse(d.renda);
                    const met = engine.utils.parse(d.meta);
                    const folga = Math.max(0, ren - tG);
                    const disp = folga + tR;
                    const fal = Math.max(0, met - tR);
                    const pct = met > 0 ? Math.min((tR / met) * 100, 100) : 0;
                    document.getElementById('disp-livre').innerText = engine.utils.format(disp);
                    document.getElementById('disp-total').innerText = engine.utils.format(tR);
                    document.getElementById('disp-gastos').innerText = engine.utils.format(tG);
                    document.getElementById('disp-falta').innerText = engine.utils.format(fal);
                    document.getElementById('disp-bar').style.width = pct + "%";
                    document.getElementById('disp-pct').innerText = `${pct.toFixed(2)}% DA META`;
                    engine.ui.renderChart(tR, fal, tG);
                    engine.ui.renderLists(d.h_gastos, d.h_reserva);
                    engine.ui.renderSummary(ren, tG, tR, met);
                },
                renderChart: (r, f, g) => {
                    const ctx = document.getElementById('mainDoughnut').getContext('2d');
                    if (engine.state.chart) engine.state.chart.destroy();
                    engine.state.chart = new Chart(ctx, {
                        type: 'doughnut',
                        data: {
                            labels: ['Patrimônio', 'Falta', 'Gastos'],
                            datasets: [{ data: [r || 0.1, f || 0, g || 0], backgroundColor: ['#8a05be', '#e2e8f0', '#ff3b30'], borderWidth: 0 }]
                        },
                        options: { cutout: '82%', plugins: { legend: { display: false } } }
                    });
                },
                renderLists: (gs, rs) => {
                    const cG = document.getElementById('list-gastos');
                    const cR = document.getElementById('list-reserva');
                    cG.innerHTML = gs.length ? gs.map(i => `<div class="list-item"><div class="item-data"><small>${i.date} • ${i.cat}</small><b style="color:var(--dg)">- ${engine.utils.format(i.val)}</b></div><button class="item-del" onclick="engine.data.delete(${i.id}, 'g')">🗑️</button></div>`).join('') : '<div class="no-data">Sem gastos registrados</div>';
                    cR.innerHTML = rs.length ? rs.map(i => `<div class="list-item" style="border-left-color:var(--sc)"><div class="item-data"><small>${i.date} • Aporte</small><b style="color:var(--sc)">+ ${engine.utils.format(i.val)}</b></div><button class="item-del" onclick="engine.data.delete(${i.id}, 'r')">🗑️</button></div>`).join('') : '<div class="no-data">Nenhum aporte realizado</div>';
                },
                renderSummary: (ren, gas, res, met) => {
                    const el = document.getElementById('summary-data');
                    if (ren <= 0) { el.innerHTML = "Vá em <b>Perfil</b> e configure sua renda para uma análise."; return; }
                    const gP = (gas / ren) * 100;
                    let msg = `Você consome <b>${gP.toFixed(1)}%</b> da sua renda. `;
                    if (met > 0) {
                        const poupanca = ren - gas;
                        const meses = Math.ceil((met - res) / (poupanca || 1));
                        msg += meses > 0 ? `Faltam aproximadamente <b>${meses} meses</b> para atingir sua meta final.` : "Parabéns! Você atingiu sua meta.";
                    }
                    el.innerHTML = msg;
                }
            },
            auth: {
                switch: (view) => {
                    document.getElementById('view-login').style.display = view === 'login' ? 'block' : 'none';
                    document.getElementById('view-register').style.display = view === 'register' ? 'block' : 'none';
                },
                submitRegister: () => {
                    const user = document.getElementById('reg-user').value.trim();
                    const email = document.getElementById('reg-email').value.toLowerCase().trim();
                    const pass = document.getElementById('reg-pass').value;
                    if(!user || !email || !pass) { engine.toast("❌ Preencha todos os campos"); return; }
                    let db = engine.data.db();
                    if(db[email]) { engine.toast("❌ E-mail já cadastrado"); return; }
                    db[email] = { username: user, password: pass, renda: "R$ 0,00", meta: "R$ 0,00", h_gastos: [], h_reserva: [] };
                    localStorage.setItem('wl_sob_db_v1', JSON.stringify(db));
                    engine.toast("✨ Conta Criada com Sucesso!"); engine.auth.switch('login');
                },
                submitLogin: () => {
                    const email = document.getElementById('log-email').value.toLowerCase().trim();
                    const pass = document.getElementById('log-pass').value;
                    const db = engine.data.db();
                    if(db[email] && db[email].password === pass) {
                        engine.state.activeUser = email;
                        localStorage.setItem('wl_sob_session_v1', email);
                        engine.auth.success();
                    } else engine.toast("❌ Login ou Senha inválidos");
                },
                success: () => {
                    document.getElementById('auth-screen').style.display = 'none';
                    const app = document.getElementById('app');
                    app.style.display = 'flex';
                    setTimeout(() => app.classList.add('visible'), 100);
                    const u = engine.data.getUser();
                    document.getElementById('u-name').innerText = u.username;
                    document.getElementById('u-mail').innerText = engine.state.activeUser;
                    document.getElementById('u-avatar').innerText = u.username[0].toUpperCase();
                    document.getElementById('set-renda').value = u.renda;
                    document.getElementById('set-meta').value = u.meta;
                    engine.ui.refresh();
                },
                logout: () => { localStorage.removeItem('wl_sob_session_v1'); window.location.reload(); }
            },
            init: () => {
                const session = localStorage.getItem('wl_sob_session_v1');
                const db = engine.data.db();
                setTimeout(() => {
                    document.getElementById('splash').style.opacity = '0';
                    setTimeout(() => {
                        document.getElementById('splash').style.visibility = 'hidden';
                        if(session && db[session]) { engine.state.activeUser = session; engine.auth.success(); }
                        else { document.getElementById('auth-screen').style.display = 'flex'; }
                    }, 800);
                }, 1800);
            }
        };
        window.onload = () => engine.init();
    </script>
</body>
</html>
