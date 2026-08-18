# game-fungsi
memahami fungsi dengan pendekatan game khas sunda
<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Interaktif Fungsi Matematika - Kuliner Sunda</title>
    <!-- Meta tags for Web App sharing -->
    <meta name="description" content="Eksplorasi Matematika Wajib Kelas XI (Fungsi, Komposisi, & Invers) dengan Tradisi Kuliner Khas Sunda">
    <meta name="theme-color" content="#065f46">

    <!-- Tailwind CSS & Confetti CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&family=Fredoka:wght@500;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #f0fdf4;
            background-image: radial-gradient(#dcfce7 1.5px, transparent 1.5px);
            background-size: 24px 24px;
        }
        .font-game {
            font-family: 'Fredoka', cursive, sans-serif;
        }
        .card-btn {
            transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        .card-btn:hover {
            transform: translateY(-2px) scale(1.01);
        }
        .card-btn:active {
            transform: translateY(2px) scale(0.98);
        }
        @keyframes gear-spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .spin-gear {
            animation: gear-spin 4s linear infinite;
        }
        @keyframes bounce-slow {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-6px); }
        }
        .floating-badge {
            animation: bounce-slow 3s ease-in-out infinite;
        }
        /* Custom Scrollbar for smooth web feel */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #e2e8f0;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb {
            background: #059669;
            border-radius: 4px;
        }
    </style>
</head>
<body class="min-h-screen text-slate-800 flex flex-col justify-between selection:bg-emerald-300 antialiased">

    <header class="bg-gradient-to-r from-emerald-800 via-green-700 to-teal-800 text-white shadow-xl sticky top-0 z-40">
        <div class="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-11 h-11 bg-amber-400 rounded-2xl flex items-center justify-center text-2xl shadow-md border-2 border-amber-200 floating-badge shrink-0">
                    🍱
                </div>
                <div>
                    <div class="flex items-center space-x-2">
                        <h1 class="font-game text-xl sm:text-2xl font-bold text-amber-300 leading-tight">Fungsi Kuliner Sunda</h1>
                        <span class="bg-amber-500 text-amber-950 font-game font-bold text-[10px] px-2 py-0.5 rounded-full uppercase">Kelas XI Web</span>
                    </div>
                    <p class="text-xs text-emerald-100 hidden sm:block">Eksplorasi Matematika Wajib dengan Tradisi Priangan</p>
                </div>
            </div>

            <!-- Controls (Score, Sound, Help, Reset) -->
            <div class="flex items-center space-x-2 sm:space-x-3">
                <div class="bg-emerald-950/70 backdrop-blur border border-emerald-400/30 rounded-2xl px-3 py-1.5 flex items-center space-x-1.5">
                    <span class="text-amber-400 text-base">⭐</span>
                    <span id="global-score" class="font-game text-lg sm:text-xl font-bold text-yellow-300">0</span>
                    <span class="text-xs text-emerald-200 hidden sm:inline">Poin</span>
                </div>

                <button onclick="toggleSound()" id="sound-toggle" class="p-2 bg-emerald-700/80 hover:bg-emerald-600 rounded-xl transition border border-emerald-500/30 text-lg sm:text-xl" title="Aktifkan/Matikan Suara">
                    🔊
                </button>

                <button onclick="openHelpModal()" class="p-2 bg-emerald-700/80 hover:bg-emerald-600 rounded-xl transition border border-emerald-500/30 text-lg sm:text-xl" title="Bantuan & Petunjuk">
                    ❓
                </button>

                <button onclick="confirmResetProgress()" class="p-2 bg-rose-700/80 hover:bg-rose-600 rounded-xl transition border border-rose-500/30 text-lg sm:text-xl text-white" title="Ulang Game">
                    🔄
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-6xl mx-auto px-4 py-6 flex-grow w-full">
        <!-- Level Progress Tabs -->
        <div class="mb-5 overflow-x-auto pb-2">
            <div class="flex space-x-2 min-w-max justify-start md:justify-center" id="level-tabs">
                <!-- Tabs will be rendered dynamically -->
            </div>
        </div>

        <!-- Notification Toast Banner -->
        <div id="toast-banner" class="hidden mb-4 p-3.5 rounded-2xl font-semibold text-sm transition-all duration-300 shadow-md flex items-center justify-between">
            <span id="toast-text"></span>
            <button onclick="hideToast()" class="text-xs underline ml-2 opacity-80 hover:opacity-100">Tutup</button>
        </div>

        <!-- Dynamic Game Container -->
        <div id="game-container" class="bg-white rounded-3xl shadow-2xl border-4 border-emerald-600/20 p-4 sm:p-6 md:p-8 min-h-[520px] flex flex-col justify-between relative overflow-hidden">
            <!-- Level Content Rendered via JavaScript -->
        </div>
    </main>

    <footer class="bg-emerald-950 text-emerald-200/80 py-4 text-center text-xs sm:text-sm border-t border-emerald-800">
        <div class="max-w-6xl mx-auto px-4 flex flex-col sm:flex-row justify-between items-center gap-2">
            <div class="flex items-center space-x-2">
                <span>🌾 Modul Web Interaktif Matematika</span>
                <span class="text-amber-400">•</span>
                <b class="text-amber-300">Kuliner Khas Sunda</b>
            </div>
            <div class="text-emerald-400 font-medium flex items-center gap-2">
                <span>Dapat diakses langsung di Peramban Web</span>
                <span class="bg-emerald-900 border border-emerald-700 px-2 py-0.5 rounded text-[10px] text-amber-300">Versi Web Ready</span>
            </div>
        </div>
    </footer>

    <!-- Universal Modal Container -->
    <div id="modal-backdrop" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div id="modal-box" class="bg-white rounded-3xl p-6 md:p-8 max-w-lg w-full shadow-2xl border-4 border-amber-400 text-center space-y-4 relative animate-fade-in max-h-[90vh] overflow-y-auto">
            <!-- Dynamic Modal Content -->
        </div>
    </div>

    <script>
        // Web Audio Sound Engine
        let soundEnabled = localStorage.getItem('sunda_sound_enabled') !== 'false';

        function updateSoundButtonUI() {
            const btn = document.getElementById('sound-toggle');
            if (btn) btn.innerText = soundEnabled ? '🔊' : '🔇';
        }

        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

        function playSound(type) {
            if (!soundEnabled) return;
            try {
                if (audioCtx.state === 'suspended') {
                    audioCtx.resume();
                }
                
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.connect(gain);
                gain.connect(audioCtx.destination);

                const now = audioCtx.currentTime;

                if (type === 'click') {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(450, now);
                    osc.frequency.exponentialRampToValueAtTime(850, now + 0.08);
                    gain.gain.setValueAtTime(0.15, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.08);
                    osc.start(now);
                    osc.stop(now + 0.08);
                } else if (type === 'correct') {
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(523.25, now);
                    osc.frequency.setValueAtTime(659.25, now + 0.09);
                    osc.frequency.setValueAtTime(783.99, now + 0.18);
                    osc.frequency.setValueAtTime(1046.50, now + 0.27);
                    gain.gain.setValueAtTime(0.2, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.45);
                    osc.start(now);
                    osc.stop(now + 0.45);
                } else if (type === 'wrong') {
                    osc.type = 'sawtooth';
                    osc.frequency.setValueAtTime(220, now);
                    osc.frequency.linearRampToValueAtTime(110, now + 0.25);
                    gain.gain.setValueAtTime(0.2, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.25);
                    osc.start(now);
                    osc.stop(now + 0.25);
                } else if (type === 'cook') {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(320, now);
                    osc.frequency.linearRampToValueAtTime(640, now + 0.3);
                    gain.gain.setValueAtTime(0.2, now);
                    gain.gain.linearRampToValueAtTime(0.01, now + 0.3);
                    osc.start(now);
                    osc.stop(now + 0.3);
                }
            } catch (e) {
                console.log("Audio not allowed yet:", e);
            }
        }

        function toggleSound() {
            soundEnabled = !soundEnabled;
            localStorage.setItem('sunda_sound_enabled', soundEnabled);
            updateSoundButtonUI();
            showToast(soundEnabled ? '🔊 Suara Efek Diaktifkan' : '🔇 Suara Efek Dimatikan', 'info');
        }

        function showToast(msg, type = 'info') {
            const banner = document.getElementById('toast-banner');
            const text = document.getElementById('toast-text');
            text.innerText = msg;

            if (type === 'success') {
                banner.className = "mb-4 p-3.5 rounded-2xl font-semibold text-sm transition-all duration-300 shadow-md flex items-center justify-between bg-emerald-100 text-emerald-900 border border-emerald-300";
            } else if (type === 'error') {
                banner.className = "mb-4 p-3.5 rounded-2xl font-semibold text-sm transition-all duration-300 shadow-md flex items-center justify-between bg-rose-100 text-rose-900 border border-rose-300";
            } else {
                banner.className = "mb-4 p-3.5 rounded-2xl font-semibold text-sm transition-all duration-300 shadow-md flex items-center justify-between bg-amber-100 text-amber-900 border border-amber-300";
            }
            banner.classList.remove('hidden');

            setTimeout(() => {
                hideToast();
            }, 4000);
        }

        function hideToast() {
            const banner = document.getElementById('toast-banner');
            if (banner) banner.classList.add('hidden');
        }
    </script>

    <script>
        // Global Game State with LocalStorage sync
        const defaultState = {
            currentLevel: 1,
            score: 0,
            completedLevels: [false, false, false, false, false]
        };

        let gameState = loadGameState();

        function loadGameState() {
            try {
                const saved = localStorage.getItem('sunda_game_math_state');
                if (saved) return JSON.parse(saved);
            } catch (e) {
                console.error("Failed to load state", e);
            }
            return { ...defaultState };
        }

        function saveGameState() {
            try {
                localStorage.setItem('sunda_game_math_state', JSON.stringify(gameState));
            } catch (e) {
                console.error("Failed to save state", e);
            }
        }

        const levelsMeta = [
            { id: 1, title: "Lvl 1: Input & Output", subtitle: "Pesan Makanan", icon: "🍜" },
            { id: 2, title: "Lvl 2: Domain & Range", subtitle: "Menu Warung Sunda", icon: "🗺️" },
            { id: 3, title: "Lvl 3: Jenis Fungsi", subtitle: "Linear & Kuadrat", icon: "📈" },
            { id: 4, title: "Lvl 4: Komposisi", subtitle: "Proses Memasak (f ∘ g)", icon: "🍳" },
            { id: 5, title: "Lvl 5: Fungsi Invers", subtitle: "Kasir & Struk f⁻¹(y)", icon: "🧾" }
        ];

        function addScore(pts) {
            gameState.score += pts;
            saveGameState();
            document.getElementById('global-score').innerText = gameState.score;
        }

        function renderNavigationTabs() {
            const tabsContainer = document.getElementById('level-tabs');
            tabsContainer.innerHTML = levelsMeta.map((lvl, index) => {
                const isActive = gameState.currentLevel === lvl.id;
                const isCompleted = gameState.completedLevels[index];
                
                let baseStyle = "flex items-center space-x-2 px-3.5 py-2 rounded-2xl font-game font-semibold text-xs sm:text-sm transition-all shadow-sm border-2 cursor-pointer select-none ";
                if (isActive) {
                    baseStyle += "bg-emerald-600 text-white border-emerald-700 scale-105 shadow-md";
                } else if (isCompleted) {
                    baseStyle += "bg-emerald-100 text-emerald-900 border-emerald-300 hover:bg-emerald-200";
                } else {
                    baseStyle += "bg-white text-slate-600 border-slate-200 hover:bg-slate-100";
                }

                return `
                    <button onclick="switchLevel(${lvl.id})" class="${baseStyle}">
                        <span>${lvl.icon}</span>
                        <span>${lvl.title}</span>
                        ${isCompleted ? '<span class="text-xs text-amber-500 font-bold ml-1">★</span>' : ''}
                    </button>
                `;
            }).join('');

            document.getElementById('global-score').innerText = gameState.score;
        }

        function switchLevel(lvlId) {
            playSound('click');
            gameState.currentLevel = lvlId;
            saveGameState();
            renderNavigationTabs();
            renderLevelContent();
        }

        function renderLevelContent() {
            const container = document.getElementById('game-container');
            switch (gameState.currentLevel) {
                case 1: renderLevel1(container); break;
                case 2: renderLevel2(container); break;
                case 3: renderLevel3(container); break;
                case 4: renderLevel4(container); break;
                case 5: renderLevel5(container); break;
                default: renderLevel1(container); break;
            }
        }

        function confirmResetProgress() {
            showCustomModal(`
                <div class="text-4xl">⚠️</div>
                <h3 class="font-game text-xl font-bold text-slate-800">Ulangi Seluruh Game?</h3>
                <p class="text-xs text-slate-600">Skor dan kemajuan level Anda akan direset ke awal.</p>
                <div class="flex gap-2 pt-2">
                    <button onclick="closeModal()" class="w-1/2 bg-slate-200 hover:bg-slate-300 text-slate-700 font-game font-bold py-2.5 rounded-xl">Batal</button>
                    <button onclick="resetGameConfirmed()" class="w-1/2 bg-rose-600 hover:bg-rose-700 text-white font-game font-bold py-2.5 rounded-xl">Ya, Reset</button>
                </div>
            `);
        }

        function resetGameConfirmed() {
            closeModal();
            gameState = { ...defaultState };
            saveGameState();
            currentL1Index = 0;
            currentL3Tab = 'linear';
            l2UserConnections = {};
            renderNavigationTabs();
            renderLevelContent();
            showToast("🎮 Game berhasil direset ke Level 1", "info");
        }
    </script>

    <script>
        // LEVEL 1: Mesin Pemesan Makanan (Input X -> Machine f(x) -> Output Y)
        const level1Data = [
            { id: 1, money: 50000, formula: "f(x) = x / 10000", dish: "Nasi Timbel Komplit 🍱", answer: 5, exp: "f(50.000) = 50.000 / 10.000 = 5 Porsi Nasi Timbel." },
            { id: 2, money: 30000, formula: "f(x) = (x - 6000) / 8000", dish: "Porsi Es Lilin Bandung 🍧", answer: 3, exp: "f(30.000) = (30.000 - 6.000) / 8.000 = 24.000 / 8.000 = 3 Porsi Es Lilin." },
            { id: 3, money: 45000, formula: "f(x) = (x * 2) / 1000", dish: "Kupon Poin Garut 🎟️", answer: 90, exp: "f(45.000) = (45.000 * 2) / 1000 = 90.000 / 1000 = 90 Kupon." }
        ];

        let currentL1Index = 0;

        function renderLevel1(container) {
            const q = level1Data[currentL1Index];
            container.innerHTML = `
                <div class="space-y-6">
                    <div class="bg-gradient-to-r from-amber-500 to-amber-600 text-white p-4 rounded-2xl shadow-md flex items-center justify-between">
                        <div>
                            <span class="bg-amber-700/60 px-3 py-1 rounded-full text-xs uppercase font-bold tracking-wider">Level 1 (${currentL1Index + 1}/${level1Data.length})</span>
                            <h2 class="font-game text-xl sm:text-2xl font-bold mt-1">Kenali Fungsi & Masukan / Keluaran (Input & Output)</h2>
                            <p class="text-amber-100 text-xs sm:text-sm">Masukan Uang Pembeli ($X$) ke Mesin Fungsi $f(x)$ untuk Menghasilkan Pesanan ($Y$)!</p>
                        </div>
                        <div class="hidden sm:block text-4xl">🏪</div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 items-center bg-emerald-50/80 p-5 rounded-2xl border-2 border-emerald-200">
                        <div class="bg-white p-4 rounded-2xl shadow border-2 border-amber-300 text-center">
                            <span class="text-[11px] font-bold text-amber-700 uppercase tracking-wider block mb-1">X (Masukan / Input)</span>
                            <div class="text-xl sm:text-2xl font-bold text-amber-600 font-game">Rp ${q.money.toLocaleString('id-ID')}</div>
                            <div class="text-xs text-slate-500 mt-1">Uang Pembeli Sunda</div>
                        </div>

                        <div class="bg-gradient-to-b from-emerald-600 to-teal-700 p-5 rounded-2xl shadow-lg text-white text-center border-4 border-emerald-800 relative">
                            <div class="absolute -top-3 left-1/2 -translate-x-1/2 bg-amber-400 text-amber-950 font-game font-bold text-xs px-3 py-0.5 rounded-full border border-amber-500 shadow">
                                MESIN FUNGSI f(x)
                            </div>
                            <div class="font-game text-lg sm:text-xl font-bold text-yellow-300 my-2 tracking-wide">${q.formula}</div>
                            <div class="text-xs text-emerald-100 flex items-center justify-center gap-1">
                                <span class="spin-gear inline-block">⚙️</span> Memproses X menjadi Y
                            </div>
                        </div>

                        <div class="bg-white p-4 rounded-2xl shadow border-2 border-emerald-300 text-center">
                            <span class="text-[11px] font-bold text-emerald-700 uppercase tracking-wider block mb-1">Y (Keluaran / Output)</span>
                            <div class="text-lg font-bold text-emerald-700 font-game mb-1">${q.dish}</div>
                            <div class="text-xs text-slate-500">Hasil Akhir Sesuai Rumus</div>
                        </div>
                    </div>

                    <div class="bg-white border-2 border-slate-200 rounded-2xl p-5 shadow-sm space-y-3">
                        <h3 class="font-game font-bold text-slate-800 text-base sm:text-lg">
                            Hitung Nilai Output Y = f(${q.money.toLocaleString('id-ID')}):
                        </h3>

                        <div class="flex flex-col sm:flex-row gap-3 items-center">
                            <input type="number" id="l1-input" placeholder="Masukkan angka..." onkeydown="if(event.key==='Enter') checkLevel1Answer()"
                                class="w-full sm:w-2/3 px-4 py-3 rounded-xl border-2 border-emerald-300 focus:outline-none focus:border-emerald-600 font-game text-lg">
                            <button onclick="checkLevel1Answer()" class="w-full sm:w-1/3 bg-emerald-600 hover:bg-emerald-700 text-white font-game font-bold py-3 px-6 rounded-xl shadow-md card-btn">
                                Jalankan Mesin ⚙️
                            </button>
                        </div>
                        
                        <div id="l1-feedback" class="hidden p-4 rounded-xl text-sm font-medium"></div>
                    </div>
                </div>
            `;
            setTimeout(() => {
                const el = document.getElementById('l1-input');
                if (el) el.focus();
            }, 100);
        }

        function checkLevel1Answer() {
            const inputEl = document.getElementById('l1-input');
            const userAns = parseFloat(inputEl.value);
            const q = level1Data[currentL1Index];
            const feedbackEl = document.getElementById('l1-feedback');

            if (isNaN(userAns)) {
                feedbackEl.className = "p-3 bg-amber-100 text-amber-800 rounded-xl text-xs sm:text-sm font-semibold border border-amber-300 block";
                feedbackEl.innerText = "⚠️ Masukkan angka jawaban Anda terlebih dahulu!";
                playSound('wrong');
                return;
            }

            if (Math.abs(userAns - q.answer) < 0.01) {
                playSound('correct');
                confetti({ particleCount: 60, spread: 60, origin: { y: 0.7 } });
                feedbackEl.className = "p-3 bg-emerald-100 text-emerald-900 rounded-xl text-xs sm:text-sm font-semibold border border-emerald-300 block";
                feedbackEl.innerHTML = `🎉 <b>Tepat Sekali!</b> ${q.exp} (+20 Poin)`;
                addScore(20);

                setTimeout(() => {
                    currentL1Index++;
                    if (currentL1Index < level1Data.length) {
                        renderLevel1(document.getElementById('game-container'));
                    } else {
                        gameState.completedLevels[0] = true;
                        saveGameState();
                        renderNavigationTabs();
                        showLevelCompletedModal("Level 1 Selesai!", "Kamu menguasai konsep dasar Input (X) dan Output (Y) dalam fungsi matematika!", 2);
                    }
                }, 1600);
            } else {
                playSound('wrong');
                feedbackEl.className = "p-3 bg-rose-100 text-rose-800 rounded-xl text-xs sm:text-sm font-semibold border border-rose-300 block";
                feedbackEl.innerText = `❌ Masih salah. Gunakan rumus ${q.formula} untuk nilai x = ${q.money}!`;
            }
        }
    </script>

    <script>
        // LEVEL 2: Relasi & Domain, Kodomain, Range (Menu Warung Sunda)
        const l2Dishes = [
            { id: "liwet", name: "Nasi Liwet 🍚", flavor: "Gurih" },
            { id: "karedok", name: "Karedok 🥗", flavor: "Pedas" },
            { id: "eslilin", name: "Es Lilin 🍦", flavor: "Manis" },
            { id: "surabi", name: "Surabi Kinca 🥞", flavor: "Manis" }
        ];

        const l2Flavors = ["Gurih", "Pedas", "Manis", "Asam", "Pahit"];
        let l2UserConnections = {};

        function renderLevel2(container) {
            container.innerHTML = `
                <div class="space-y-6">
                    <div class="bg-gradient-to-r from-emerald-600 to-teal-700 text-white p-4 rounded-2xl shadow-md flex items-center justify-between">
                        <div>
                            <span class="bg-emerald-800/60 px-3 py-1 rounded-full text-xs uppercase font-bold tracking-wider">Level 2</span>
                            <h2 class="font-game text-xl sm:text-2xl font-bold mt-1">Relasi & Domain, Kodomain, Range</h2>
                            <p class="text-emerald-100 text-xs sm:text-sm">Petakan Daftar Menu (Domain) ke Rasanya (Kodomain) untuk Menemukan Range!</p>
                        </div>
                        <div class="hidden sm:block text-4xl">🍃</div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-3 text-xs">
                        <div class="bg-blue-50 border border-blue-200 p-3 rounded-2xl text-blue-900 shadow-sm">
                            <b class="font-game text-xs sm:text-sm text-blue-700 block mb-1">1. Domain (Daerah Asal)</b>
                            Himpunan semua makanan khas Sunda yang ada di menu warung.
                        </div>
                        <div class="bg-purple-50 border border-purple-200 p-3 rounded-2xl text-purple-900 shadow-sm">
                            <b class="font-game text-xs sm:text-sm text-purple-700 block mb-1">2. Kodomain (Daerah Kawan)</b>
                            Himpunan semua variasi rasa yang tersedia di warung.
                        </div>
                        <div class="bg-amber-50 border border-amber-200 p-3 rounded-2xl text-amber-900 shadow-sm">
                            <b class="font-game text-xs sm:text-sm text-amber-700 block mb-1">3. Range (Daerah Hasil)</b>
                            Sub-himpunan rasa yang memiliki pasangan tepat dari menu.
                        </div>
                    </div>

                    <div class="bg-amber-50/60 p-5 rounded-2xl border-2 border-amber-200 flex flex-col md:flex-row justify-between items-center gap-6">
                        <div class="w-full md:w-5/12 space-y-3">
                            <h4 class="font-game font-bold text-center text-amber-800 text-sm sm:text-base border-b-2 border-amber-300 pb-2">
                                DOMAIN (Daftar Menu)
                            </h4>
                            ${l2Dishes.map(d => `
                                <div class="bg-white p-3 rounded-xl border-2 border-amber-200 shadow-sm flex items-center justify-between">
                                    <span class="font-game font-semibold text-slate-700 text-xs sm:text-sm">${d.name}</span>
                                    <select onchange="setL2Connection('${d.id}', this.value)" class="bg-amber-100 text-amber-900 text-xs font-bold px-2.5 py-1.5 rounded-lg border border-amber-300 focus:outline-none cursor-pointer">
                                        <option value="">-- Hubungkan --</option>
                                        ${l2Flavors.map(f => `<option value="${f}" ${l2UserConnections[d.id] === f ? 'selected' : ''}>${f}</option>`).join('')}
                                    </select>
                                </div>
                            `).join('')}
                        </div>

                        <div class="hidden md:flex flex-col items-center justify-center text-amber-600 font-bold">
                            <span class="text-[10px] uppercase bg-amber-200 px-2 py-0.5 rounded text-amber-900 mb-1 font-game">Pemetaan f(x)</span>
                            <span class="text-3xl">➔</span>
                        </div>

                        <div class="w-full md:w-5/12 space-y-3">
                            <h4 class="font-game font-bold text-center text-emerald-800 text-sm sm:text-base border-b-2 border-emerald-300 pb-2">
                                KODOMAIN & RANGE
                            </h4>
                            <div class="grid grid-cols-2 gap-2">
                                ${l2Flavors.map(f => {
                                    const isSelected = Object.values(l2UserConnections).includes(f);
                                    return `
                                        <div class="p-2.5 rounded-xl border-2 text-center font-game font-semibold text-xs transition-all ${isSelected ? 'bg-emerald-600 text-white border-emerald-700 shadow-md scale-105' : 'bg-white border-emerald-200 text-emerald-800'}">
                                            ✨ ${f} ${isSelected ? '<span class="block text-[10px] text-amber-300 mt-0.5">(Bagian Range)</span>' : ''}
                                        </div>
                                    `;
                                }).join('')}
                            </div>
                        </div>
                    </div>

                    <div class="bg-white border-2 border-slate-200 rounded-2xl p-5 shadow-sm flex flex-col sm:flex-row items-center justify-between gap-4">
                        <div class="text-xs sm:text-sm text-slate-600">
                            <b>Tugas:</b> Pasangkan ke-4 hidangan Sunda dengan pilihan rasa yang tepat!
                        </div>
                        <button onclick="checkLevel2Answer()" class="w-full sm:w-auto bg-emerald-600 hover:bg-emerald-700 text-white font-game font-bold py-3 px-8 rounded-xl shadow-md card-btn">
                            Verifikasi Pemetaan 🔍
                        </button>
                    </div>

                    <div id="l2-feedback" class="hidden p-4 rounded-xl text-sm font-medium"></div>
                </div>
            `;
        }

        function setL2Connection(dishId, flavor) {
            playSound('click');
            l2UserConnections[dishId] = flavor;
            renderLevel2(document.getElementById('game-container'));
        }

        function checkLevel2Answer() {
            let correctCount = 0;
            l2Dishes.forEach(d => {
                if (l2UserConnections[d.id] === d.flavor) {
                    correctCount++;
                }
            });

            const feedbackEl = document.getElementById('l2-feedback');

            if (correctCount === l2Dishes.length) {
                playSound('correct');
                confetti({ particleCount: 70, spread: 70, origin: { y: 0.7 } });
                feedbackEl.className = "p-3 bg-emerald-100 text-emerald-900 rounded-xl text-xs sm:text-sm font-semibold border border-emerald-300 block";
                feedbackEl.innerHTML = `🎉 <b>Pemetaan Sempurna!</b><br>
                • <b>Domain:</b> {Nasi Liwet, Karedok, Es Lilin, Surabi Kinca}<br>
                • <b>Kodomain:</b> {Gurih, Pedas, Manis, Asam, Pahit}<br>
                • <b>Range:</b> {Gurih, Pedas, Manis}`;
                addScore(25);

                setTimeout(() => {
                    gameState.completedLevels[1] = true;
                    saveGameState();
                    renderNavigationTabs();
                    showLevelCompletedModal("Level 2 Selesai!", "Kamu berhasil memahami perbedaan Domain, Kodomain, dan Range!", 3);
                }, 2000);
            } else {
                playSound('wrong');
                feedbackEl.className = "p-3 bg-rose-100 text-rose-800 rounded-xl text-xs sm:text-sm font-semibold border border-rose-300 block";
                feedbackEl.innerText = `❌ Kamu baru memasangkan ${correctCount} dari ${l2Dishes.length} hidangan dengan benar. Petunjuk: Nasi Liwet (Gurih), Karedok (Pedas), Es Lilin (Manis), Surabi (Manis)!`;
            }
        }
    </script>

    <script>
        // LEVEL 3: Jenis-Jenis Fungsi (Fungsi Linear & Fungsi Kuadrat)
        let currentL3Tab = 'linear';

        function renderLevel3(container) {
            container.innerHTML = `
                <div class="space-y-5">
                    <div class="bg-gradient-to-r from-blue-600 to-indigo-700 text-white p-4 rounded-2xl shadow-md flex items-center justify-between">
                        <div>
                            <span class="bg-blue-800/60 px-3 py-1 rounded-full text-xs uppercase font-bold tracking-wider">Level 3</span>
                            <h2 class="font-game text-xl sm:text-2xl font-bold mt-1">Jenis-Jenis Fungsi: Linear & Kuadrat</h2>
                            <p class="text-blue-100 text-xs sm:text-sm">Hitung Total Sate Maranggi (Linear) & Promosi Bakso (Kuadrat)!</p>
                        </div>
                        <div class="hidden sm:block text-4xl">📈</div>
                    </div>

                    <div class="flex border-b-2 border-indigo-200">
                        <button onclick="switchL3Tab('linear')" class="px-4 sm:px-6 py-2 font-game font-bold text-xs sm:text-sm border-b-4 transition ${currentL3Tab === 'linear' ? 'border-indigo-600 text-indigo-700 bg-indigo-50/50' : 'border-transparent text-slate-500 hover:text-slate-700'}">
                            1. Linear: Sate Maranggi
                        </button>
                        <button onclick="switchL3Tab('quadratic')" class="px-4 sm:px-6 py-2 font-game font-bold text-xs sm:text-sm border-b-4 transition ${currentL3Tab === 'quadratic' ? 'border-indigo-600 text-indigo-700 bg-indigo-50/50' : 'border-transparent text-slate-500 hover:text-slate-700'}">
                            2. Kuadrat: Promosi Bakso
                        </button>
                    </div>

                    <div id="l3-subcontent">
                        ${currentL3Tab === 'linear' ? renderL3Linear() : renderL3Quadratic()}
                    </div>
                </div>
            `;

            if (currentL3Tab === 'quadratic') {
                setTimeout(drawParabolaCanvas, 100);
            }
        }

        function switchL3Tab(tab) {
            playSound('click');
            currentL3Tab = tab;
            renderLevel3(document.getElementById('game-container'));
        }

        function renderL3Linear() {
            return `
                <div class="space-y-4">
                    <div class="bg-indigo-50 border-2 border-indigo-200 p-4 rounded-2xl space-y-2">
                        <span class="bg-indigo-600 text-white text-[10px] font-bold px-2.5 py-0.5 rounded-full uppercase">Fungsi Linear f(x) = px + q</span>
                        <h3 class="font-game text-lg font-bold text-indigo-900">Perhitungan Total Harga Sate Maranggi</h3>
                        <p class="text-slate-700 text-xs sm:text-sm leading-relaxed">
                            Di Warung Sate Maranggi, harga total bayar mengikuti fungsi linear: <br>
                            <b class="text-indigo-700 font-game text-base sm:text-lg">f(x) = 25.000x + 10.000</b><br>
                            (Di mana <b class="text-indigo-800">x</b> adalah jumlah porsi sate dan <b class="text-indigo-800">10.000</b> adalah biaya sewa nampan).
                        </p>
                    </div>

                    <div class="bg-white border-2 border-slate-200 rounded-2xl p-5 shadow-sm space-y-3">
                        <label class="font-game font-bold text-slate-800 text-sm sm:text-base block">
                            ❓ Berapa total harga yang harus dibayar jika membeli 3 porsi Sate Maranggi ($f(3)$)?
                        </label>

                        <div class="flex flex-col sm:flex-row gap-3">
                            <input type="number" id="l3-linear-input" placeholder="Total harga..." onkeydown="if(event.key==='Enter') checkL3LinearAnswer()"
                                class="w-full sm:w-2/3 px-4 py-3 rounded-xl border-2 border-indigo-300 focus:outline-none focus:border-indigo-600 font-game text-lg">
                            <button onclick="checkL3LinearAnswer()" class="w-full sm:w-1/3 bg-indigo-600 hover:bg-indigo-700 text-white font-game font-bold py-3 px-6 rounded-xl shadow-md card-btn">
                                Hitung Total 🧮
                            </button>
                        </div>

                        <div id="l3-linear-feedback" class="hidden p-3 rounded-xl text-xs sm:text-sm font-medium"></div>
                    </div>
                </div>
            `;
        }

        function checkL3LinearAnswer() {
            const val = parseFloat(document.getElementById('l3-linear-input').value);
            const feedbackEl = document.getElementById('l3-linear-feedback');

            if (val === 85000) {
                playSound('correct');
                feedbackEl.className = "p-3 bg-emerald-100 text-emerald-900 rounded-xl text-xs sm:text-sm font-semibold border border-emerald-300 block";
                feedbackEl.innerHTML = "🎉 <b>Tepat Sekali!</b> f(3) = 25.000(3) + 10.000 = 75.000 + 10.000 = Rp 85.000 (+15 Poin). Sekarang coba tab Fungsi Kuadrat!";
                addScore(15);
            } else {
                playSound('wrong');
                feedbackEl.className = "p-3 bg-rose-100 text-rose-800 rounded-xl text-xs sm:text-sm font-semibold border border-rose-300 block";
                feedbackEl.innerText = "❌ Masih belum tepat. Kalikan 25.000 dengan 3 porsi terlebih dahulu, lalu tambahkan 10.000!";
            }
        }

        function renderL3Quadratic() {
            return `
                <div class="space-y-4">
                    <div class="bg-indigo-50 border-2 border-indigo-200 p-4 rounded-2xl space-y-2">
                        <span class="bg-indigo-600 text-white text-[10px] font-bold px-2.5 py-0.5 rounded-full uppercase">Fungsi Kuadrat f(x) = ax² + bx + c</span>
                        <h3 class="font-game text-lg font-bold text-indigo-900">Promosi Kupon Bakso Pasundan</h3>
                        <p class="text-slate-700 text-xs sm:text-sm leading-relaxed">
                            Poin bonus promosi warung bakso dihitung dengan fungsi kuadrat: <br>
                            <b class="text-indigo-700 font-game text-base sm:text-lg">f(x) = x² + 10x + 50</b><br>
                            (Di mana <b class="text-indigo-800">x</b> adalah jumlah mangkok bakso).
                        </p>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 items-center">
                        <div class="bg-white p-3 rounded-2xl border-2 border-indigo-200 shadow-sm flex flex-col items-center">
                            <span class="font-game font-bold text-xs text-indigo-700 mb-1">Grafik Parabola Poin Promosi f(x)</span>
                            <canvas id="parabolaCanvas" width="280" height="170" class="border border-indigo-100 rounded-xl bg-slate-900 max-w-full"></canvas>
                        </div>

                        <div class="bg-white border-2 border-slate-200 rounded-2xl p-4 shadow-sm space-y-3">
                            <label class="font-game font-bold text-slate-800 text-xs sm:text-sm block">
                                ❓ Berapa poin bonus promosi jika pembeli memesan 5 mangkok bakso ($f(5)$)?
                            </label>

                            <input type="number" id="l3-quad-input" placeholder="Poin bonus..." onkeydown="if(event.key==='Enter') checkL3QuadAnswer()"
                                class="w-full px-4 py-2.5 rounded-xl border-2 border-indigo-300 focus:outline-none focus:border-indigo-600 font-game text-base">
                            
                            <button onclick="checkL3QuadAnswer()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-game font-bold py-2.5 px-6 rounded-xl shadow-md card-btn">
                                Hitung Poin Promosi 🎯
                            </button>

                            <div id="l3-quad-feedback" class="hidden p-3 rounded-xl text-xs font-semibold"></div>
                        </div>
                    </div>
                </div>
            `;
        }

        function drawParabolaCanvas() {
            const canvas = document.getElementById('parabolaCanvas');
            if (!canvas) return;
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Grid lines
            ctx.strokeStyle = '#334155';
            ctx.lineWidth = 1;
            for(let x=0; x<canvas.width; x+=30) {
                ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x, canvas.height); ctx.stroke();
            }
            for(let y=0; y<canvas.height; y+=30) {
                ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(canvas.width, y); ctx.stroke();
            }

            // Draw parabola curve f(x) = x^2 + 10x + 50
            ctx.strokeStyle = '#f59e0b';
            ctx.lineWidth = 3;
            ctx.beginPath();
            for(let px=0; px<=canvas.width; px++) {
                let xVal = (px - 40) / 20;
                let yVal = Math.pow(xVal, 2) + 10*xVal + 50;
                let py = canvas.height - (yVal * 0.8);
                if (px === 0) ctx.moveTo(px, py);
                else ctx.lineTo(px, py);
            }
            ctx.stroke();

            // Highlight point (5, 125)
            ctx.fillStyle = '#22c55e';
            ctx.beginPath();
            ctx.arc(140, 75, 5, 0, Math.PI * 2);
            ctx.fill();

            ctx.fillStyle = '#ffffff';
            ctx.font = '10px Fredoka';
            ctx.fillText("P(5, 125)", 150, 70);
        }

        function checkL3QuadAnswer() {
            const val = parseFloat(document.getElementById('l3-quad-input').value);
            const feedbackEl = document.getElementById('l3-quad-feedback');

            if (val === 125) {
                playSound('correct');
                confetti({ particleCount: 70, spread: 70, origin: { y: 0.7 } });
                feedbackEl.className = "p-3 bg-emerald-100 text-emerald-900 rounded-xl text-xs font-semibold border border-emerald-300 block";
                feedbackEl.innerHTML = "🎉 <b>Sempurna!</b> f(5) = (5)² + 10(5) + 50 = 25 + 50 + 50 = 125 Poin (+25 Poin).";
                addScore(25);

                setTimeout(() => {
                    gameState.completedLevels[2] = true;
                    saveGameState();
                    renderNavigationTabs();
                    showLevelCompletedModal("Level 3 Selesai!", "Kamu berhasil menguasai kalkulasi fungsi linear dan fungsi kuadrat!", 4);
                }, 2000);
            } else {
                playSound('wrong');
                feedbackEl.className = "p-3 bg-rose-100 text-rose-800 rounded-xl text-xs font-semibold border border-rose-300 block";
                feedbackEl.innerText = "❌ Perhitungan belum pas. Hitung (5)² = 25, ditambah 10(5) = 50, ditambah 50!";
            }
        }
    </script>

    <script>
        // LEVEL 4: Fungsi Komposisi (f ∘ g)(x) - Multi-Step Cooking Pipeline
        function renderLevel4(container) {
            container.innerHTML = `
                <div class="space-y-6">
                    <div class="bg-gradient-to-r from-purple-600 to-pink-600 text-white p-4 rounded-2xl shadow-md flex items-center justify-between">
                        <div>
                            <span class="bg-purple-800/60 px-3 py-1 rounded-full text-xs uppercase font-bold tracking-wider">Level 4</span>
                            <h2 class="font-game text-xl sm:text-2xl font-bold mt-1">Fungsi Komposisi (f ∘ g)(x)</h2>
                            <p class="text-purple-100 text-xs sm:text-sm">Proses Memasak 2 Tahap: Masukkan Bahan ke g(x) Dulu, Lalu Hasilnya ke f(y)!</p>
                        </div>
                        <div class="hidden sm:block text-4xl">🍳</div>
                    </div>

                    <div class="bg-purple-50 p-5 rounded-2xl border-2 border-purple-200 space-y-4">
                        <h3 class="font-game font-bold text-purple-900 text-center text-base sm:text-lg">
                            Alur Memasak Karedok Sunda: (f ∘ g)(x) = f(g(x))
                        </h3>

                        <div class="grid grid-cols-1 md:grid-cols-3 gap-3 text-center items-center">
                            <div class="bg-white p-3.5 rounded-2xl border-2 border-purple-300 shadow-sm space-y-1">
                                <span class="bg-purple-100 text-purple-800 font-bold text-[10px] px-2 py-0.5 rounded-full uppercase inline-block">Tahap 1: g(x)</span>
                                <div class="font-game text-purple-700 text-sm sm:text-base font-bold">Sambal Kacang</div>
                                <div class="text-xs text-slate-600 font-mono">g(x) = 2x + 10</div>
                                <div class="text-[10px] text-slate-400">x = gram cabai rawit</div>
                            </div>

                            <div class="text-purple-600 font-bold text-sm sm:text-base flex flex-col items-center">
                                <span>➔ Output g(x) ➔</span>
                                <span class="text-[10px] text-purple-400 font-normal">(Input untuk f)</span>
                            </div>

                            <div class="bg-white p-3.5 rounded-2xl border-2 border-pink-300 shadow-sm space-y-1">
                                <span class="bg-pink-100 text-pink-800 font-bold text-[10px] px-2 py-0.5 rounded-full uppercase inline-block">Tahap 2: f(y)</span>
                                <div class="font-game text-pink-700 text-sm sm:text-base font-bold">Karedok Komplit</div>
                                <div class="text-xs text-slate-600 font-mono">f(y) = 3y + 50</div>
                                <div class="text-[10px] text-slate-400">y = gram sambal kacang</div>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white border-2 border-slate-200 rounded-2xl p-5 shadow-sm space-y-3">
                        <div class="space-y-1">
                            <h4 class="font-game font-bold text-slate-800 text-sm sm:text-base">
                                ❓ Berapa gram total berat Hidangan Karedok jika koki menggunakan x = 5 gram cabai rawit?
                            </h4>
                            <p class="text-xs text-slate-500">
                                Hitung terlebih dahulu nilai $g(5)$, kemudian hasilnya digunakan untuk menghitung $f(g(5))$.
                            </p>
                        </div>

                        <div class="flex flex-col sm:flex-row gap-3">
                            <input type="number" id="l4-input" placeholder="Hasil akhir (f ∘ g)(5)..." onkeydown="if(event.key==='Enter') checkLevel4Answer()"
                                class="w-full sm:w-2/3 px-4 py-3 rounded-xl border-2 border-purple-300 focus:outline-none focus:border-purple-600 font-game text-lg">
                            <button onclick="checkLevel4Answer()" class="w-full sm:w-1/3 bg-purple-600 hover:bg-purple-700 text-white font-game font-bold py-3 px-6 rounded-xl shadow-md card-btn">
                                Masak Hidangan 🥗
                            </button>
                        </div>

                        <div id="l4-feedback" class="hidden p-4 rounded-xl text-sm font-medium"></div>
                    </div>
                </div>
            `;
            setTimeout(() => {
                const el = document.getElementById('l4-input');
                if (el) el.focus();
            }, 100);
        }

        function checkLevel4Answer() {
            const userAns = parseFloat(document.getElementById('l4-input').value);
            const feedbackEl = document.getElementById('l4-feedback');

            if (isNaN(userAns)) {
                feedbackEl.className = "p-3 bg-amber-100 text-amber-800 rounded-xl text-xs sm:text-sm font-semibold border border-amber-300 block";
                feedbackEl.innerText = "⚠️ Harap masukkan hasil perhitungan berat gram!";
                playSound('wrong');
                return;
            }

            if (userAns === 110) {
                playSound('cook');
                playSound('correct');
                confetti({ particleCount: 80, spread: 70, origin: { y: 0.7 } });
                feedbackEl.className = "p-3 bg-emerald-100 text-emerald-900 rounded-xl text-xs sm:text-sm font-semibold border border-emerald-300 block";
                feedbackEl.innerHTML = `🎉 <b>Masakan Karedok Sempurna!</b><br>
                1. g(5) = 2(5) + 10 = 20 gram Sambal Kacang.<br>
                2. f(20) = 3(20) + 50 = 60 + 50 = 110 gram Karedok! (+30 Poin)`;
                addScore(30);

                setTimeout(() => {
                    gameState.completedLevels[3] = true;
                    saveGameState();
                    renderNavigationTabs();
                    showLevelCompletedModal("Level 4 Selesai!", "Kamu berhasil mengoperasikan Fungsi Komposisi dua tahap pada proses memasak!", 5);
                }, 2000);
            } else {
                playSound('wrong');
                feedbackEl.className = "p-3 bg-rose-100 text-rose-800 rounded-xl text-xs sm:text-sm font-semibold border border-rose-300 block";
                feedbackEl.innerText = `❌ Hasil belum sesuai. Langkah 1: g(5) = 2(5) + 10 = 20. Langkah 2: f(20) = 3(20) + 50!`;
            }
        }
    </script>

    <script>
        // LEVEL 5: Fungsi Invers f⁻¹(y) - Receipt Audit Mini Game
        function renderLevel5(container) {
            container.innerHTML = `
                <div class="space-y-6">
                    <div class="bg-gradient-to-r from-rose-600 to-amber-700 text-white p-4 rounded-2xl shadow-md flex items-center justify-between">
                        <div>
                            <span class="bg-rose-800/60 px-3 py-1 rounded-full text-xs uppercase font-bold tracking-wider">Level 5</span>
                            <h2 class="font-game text-xl sm:text-2xl font-bold mt-1">Fungsi Invers f⁻¹(y): Dari Harga ke Pesanan</h2>
                            <p class="text-rose-100 text-xs sm:text-sm">Balikkan Fungsi Total Pembayaran ($y$) untuk Menemukan Jumlah Pesanan ($x$)!</p>
                        </div>
                        <div class="hidden sm:block text-4xl">🧾</div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-5 items-center">
                        <div class="bg-amber-50 border-2 border-dashed border-amber-400 p-5 rounded-2xl shadow-sm text-slate-800 font-mono space-y-2.5 relative">
                            <div class="text-center border-b border-amber-300 pb-2">
                                <b class="font-game text-base sm:text-lg text-amber-900 block">WARUNG SUNDA KASIR</b>
                                <span class="text-[10px] text-slate-500">Struk Pembelian #INV-SUNDA-2026</span>
                            </div>

                            <div class="flex justify-between text-xs sm:text-sm">
                                <span>Rumus Bayar f(x):</span>
                                <span class="font-bold">15.000x + 15.000</span>
                            </div>
                            
                            <div class="flex justify-between text-xs sm:text-sm border-t border-amber-200 pt-2 text-rose-700 font-bold">
                                <span>TOTAL BAYAR (y):</span>
                                <span>Rp 60.000</span>
                            </div>

                            <div class="text-[10px] text-slate-500 text-center border-t border-amber-300 pt-2 italic">
                                *Biaya awal Rp 15.000 adalah sewa gazebo lesihan.
                            </div>
                        </div>

                        <div class="bg-white border-2 border-slate-200 p-5 rounded-2xl space-y-2.5">
                            <h3 class="font-game font-bold text-rose-900 text-base sm:text-lg">
                                Rumus Fungsi Invers f⁻¹(y):
                            </h3>
                            <div class="bg-rose-50 p-3 rounded-xl border border-rose-200 text-center font-game font-bold text-base sm:text-lg text-rose-700">
                                f⁻¹(y) = (y - 15.000) / 15.000
                            </div>
                            <p class="text-xs text-slate-600 leading-relaxed">
                                Gantikan nilai total bayar <b class="text-rose-700">y = 60.000</b> ke dalam rumus fungsi invers di atas untuk menghitung berapa porsi Paket Es Lilin Spesial (<b class="text-slate-800">x</b>) yang dibeli!
                            </p>
                        </div>
                    </div>

                    <div class="bg-white border-2 border-slate-200 rounded-2xl p-5 shadow-sm space-y-3">
                        <label class="font-game font-bold text-slate-800 text-sm sm:text-base block">
                            ❓ Berapa porsi Paket Es Lilin Spesial (x) yang dibeli pembeli?
                        </label>

                        <div class="flex flex-col sm:flex-row gap-3">
                            <input type="number" id="l5-input" placeholder="Porsi x..." onkeydown="if(event.key==='Enter') checkLevel5Answer()"
                                class="w-full sm:w-2/3 px-4 py-3 rounded-xl border-2 border-rose-300 focus:outline-none focus:border-rose-600 font-game text-lg">
                            <button onclick="checkLevel5Answer()" class="w-full sm:w-1/3 bg-rose-600 hover:bg-rose-700 text-white font-game font-bold py-3 px-6 rounded-xl shadow-md card-btn">
                                Audit Struk Kasir 🔎
                            </button>
                        </div>

                        <div id="l5-feedback" class="hidden p-4 rounded-xl text-sm font-medium"></div>
                    </div>
                </div>
            `;
            setTimeout(() => {
                const el = document.getElementById('l5-input');
                if (el) el.focus();
            }, 100);
        }

        function checkLevel5Answer() {
            const userAns = parseFloat(document.getElementById('l5-input').value);
            const feedbackEl = document.getElementById('l5-feedback');

            if (isNaN(userAns)) {
                feedbackEl.className = "p-3 bg-amber-100 text-amber-800 rounded-xl text-xs sm:text-sm font-semibold border border-amber-300 block";
                feedbackEl.innerText = "⚠️ Harap masukkan angka jumlah porsi!";
                playSound('wrong');
                return;
            }

            if (userAns === 3) {
                playSound('correct');
                confetti({ particleCount: 120, spread: 90, origin: { y: 0.6 } });
                feedbackEl.className = "p-3 bg-emerald-100 text-emerald-900 rounded-xl text-xs sm:text-sm font-semibold border border-emerald-300 block";
                feedbackEl.innerHTML = `🎉 <b>Audit Struk Berhasil!</b><br>
                f⁻¹(60.000) = (60.000 - 15.000) / 15.000 = 45.000 / 15.000 = 3 Paket Es Lilin. (+30 Poin)`;
                addScore(30);

                setTimeout(() => {
                    gameState.completedLevels[4] = true;
                    saveGameState();
                    renderNavigationTabs();
                    showVictoryScreen();
                }, 2000);
            } else {
                playSound('wrong');
                feedbackEl.className = "p-3 bg-rose-100 text-rose-800 rounded-xl text-xs sm:text-sm font-semibold border border-rose-300 block";
                feedbackEl.innerText = `❌ Audit kurang tepat. Kurangi total harga 60.000 dengan 15.000 (menjadi 45.000), lalu bagi dengan 15.000!`;
            }
        }
    </script>

    <script>
        function showCustomModal(htmlContent) {
            const backdrop = document.getElementById('modal-backdrop');
            const box = document.getElementById('modal-box');
            box.innerHTML = htmlContent;
            backdrop.classList.remove('hidden');
        }

        function closeModal() {
            const backdrop = document.getElementById('modal-backdrop');
            backdrop.classList.add('hidden');
        }

        function showLevelCompletedModal(title, msg, nextLvlId) {
            showCustomModal(`
                <div class="text-5xl floating-badge">🏆</div>
                <h3 class="font-game text-2xl font-bold text-slate-800">${title}</h3>
                <p class="text-slate-600 text-sm">${msg}</p>
                <button onclick="closeModal(); switchLevel(${nextLvlId});" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-game font-bold py-3.5 rounded-2xl shadow-lg card-btn">
                    Lanjut ke Level ${nextLvlId} 🚀
                </button>
            `);
        }

        function showHelpModal() {
            showCustomModal(`
                <div class="text-3xl">📖</div>
                <h3 class="font-game text-xl font-bold text-slate-800">Panduan Bermain Web</h3>
                <div class="text-left text-xs sm:text-sm text-slate-600 space-y-2 font-medium border-y py-3 my-2 border-slate-200">
                    <p><b>1. Mesin Pemesan:</b> Hitung $y = f(x)$ untuk menentukan jumlah porsi makanan khas Sunda.</p>
                    <p><b>2. Domain & Range:</b> Hubungkan menu hidangan (Domain) ke rasanya (Kodomain & Range).</p>
                    <p><b>3. Linear & Kuadrat:</b> Hitung fungsi total bayar linear dan poin bonus promosi kuadrat.</p>
                    <p><b>4. Fungsi Komposisi:</b> Hitung memasak 2 tahap $f(g(x))$.</p>
                    <p><b>5. Fungsi Invers:</b> Balikkan total bayar $y$ untuk menemukan jumlah porsi $x$.</p>
                </div>
                <button onclick="closeModal()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-game font-bold py-2.5 rounded-xl shadow">
                    Mengerti & Lanjut Main 👍
                </button>
            `);
        }

        function openHelpModal() {
            playSound('click');
            showHelpModal();
        }

        function showVictoryScreen() {
            const container = document.getElementById('game-container');
            container.innerHTML = `
                <div class="text-center py-6 space-y-5">
                    <div class="inline-block p-4 bg-amber-100 rounded-full text-5xl sm:text-6xl shadow-inner floating-badge">
                        👑
                    </div>
                    <div>
                        <span class="bg-amber-400 text-amber-950 font-game font-bold px-3.5 py-1 rounded-full text-xs uppercase tracking-widest">Sertifikat Kelulusan Web</span>
                        <h2 class="font-game text-2xl sm:text-4xl font-bold text-emerald-800 mt-2">Selamat! Kamu Adalah Ahli Fungsi Sunda!</h2>
                        <p class="text-slate-600 max-w-lg mx-auto mt-2 text-xs sm:text-sm">
                            Kamu telah berhasil menyelesaikan seluruh 5 level materi Fungsi Matematika Wajib Kelas XI dengan studi kasus Kuliner Khas Sunda.
                        </p>
                    </div>

                    <div class="max-w-md mx-auto bg-gradient-to-r from-emerald-700 to-teal-800 text-white p-5 rounded-3xl shadow-xl space-y-2 border-4 border-amber-300">
                        <div class="text-xs uppercase tracking-wider text-emerald-200">Total Skor Akhir Kamu</div>
                        <div class="font-game text-4xl sm:text-5xl font-bold text-yellow-300">${gameState.score} Poin</div>
                        <div class="text-xs text-emerald-100">Bintang Matematika Priangan ⭐️⭐️⭐️⭐️⭐️</div>
                    </div>

                    <div class="flex flex-col sm:flex-row justify-center gap-3 max-w-md mx-auto">
                        <button onclick="copyResultsSummary()" class="w-full sm:w-1/2 bg-amber-500 hover:bg-amber-600 text-amber-950 font-game font-bold py-3 px-5 rounded-2xl shadow card-btn">
                            📋 Salin Sertifikat
                        </button>
                        <button onclick="resetGameConfirmed()" class="w-full sm:w-1/2 bg-emerald-600 hover:bg-emerald-700 text-white font-game font-bold py-3 px-5 rounded-2xl shadow card-btn">
                            🔄 Main Lagi dari Lvl 1
                        </button>
                    </div>
                </div>
            `;
            confetti({ particleCount: 150, spread: 100, origin: { y: 0.5 } });
        }

        function copyResultsSummary() {
            const summaryText = `🎓 SERTIFIKAT MATEMATIKA SUNDA 🌾\nSaya telah menyelesaikan Game Interaktif Fungsi Matematika (Kelas XI) dengan skor akhir: ${gameState.score} Poin! ⭐️⭐️⭐️⭐️⭐️`;
            
            try {
                const tempTextArea = document.createElement("textarea");
                tempTextArea.value = summaryText;
                document.body.appendChild(tempTextArea);
                tempTextArea.select();
                document.execCommand("copy");
                document.body.removeChild(tempTextArea);
                showToast("✅ Ringkasan Sertifikat telah disalin ke Clipboard!", "success");
            } catch (err) {
                showToast(" Gagal menyalin secara otomatis.", "error");
            }
        }

        // Initialize Web App on Load
        window.onload = function() {
            updateSoundButtonUI();
            renderNavigationTabs();
            renderLevelContent();
        };
    </script>
</body>
</html>
