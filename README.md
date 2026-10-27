<!DOCTYPE html>
<html lang="ur">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JJWine - Real Earning Game</title>
    <script src="https://tailwindcss.com"></script>
    <style>
        body { background: linear-gradient(135deg, #0f172a, #1e1b4b); color: white; font-family: sans-serif; }
        .hidden { display: none; }
    </style>
</head>
<body>

    <!-- 1. AUTH SCREEN (LOGIN / REGISTER) -->
    <div id="auth-screen" class="flex flex-col items-center justify-center min-h-screen px-4">
        <div class="bg-slate-800 p-6 rounded-2xl shadow-2xl w-full max-w-sm border border-slate-700">
            <h1 class="text-3xl font-extrabold text-center text-yellow-400 mb-6 tracking-wide">JJ WINE</h1>
            
            <div id="auth-tabs" class="flex justify-around mb-6 border-b border-slate-700 pb-2">
                <button onclick="switchAuthTab('login')" id="login-tab-btn" class="text-yellow-400 font-bold border-b-2 border-yellow-400 pb-1">لاگ ان</button>
                <button onclick="switchAuthTab('register')" id="register-tab-btn" class="text-slate-400 font-bold pb-1">اکاؤنٹ بنائیں</button>
            </div>

            <!-- Inputs -->
            <div class="space-y-4">
                <input type="text" id="auth-username" placeholder="صارف کا نام (Username)" class="w-full p-3 rounded-lg bg-slate-900 border border-slate-700 text-white focus:outline-none focus:border-yellow-400 text-right">
                <input type="password" id="auth-password" placeholder="پاس ورڈ (Password)" class="w-full p-3 rounded-lg bg-slate-900 border border-slate-700 text-white focus:outline-none focus:border-yellow-400 text-right">
                
                <button onclick="handleAuth()" id="auth-submit-btn" class="w-full bg-yellow-500 hover:bg-yellow-600 text-slate-950 font-extrabold p-3 rounded-lg transition duration-200">داخل ہوں</button>
            </div>
            <p id="auth-error" class="text-red-500 text-sm text-center mt-3 hidden"></p>
        </div>
    </div>

    <!-- 2. MAIN GAME LOBBY -->
    <div id="lobby-screen" class="hidden min-h-screen flex flex-col">
        <!-- Header / Wallet -->
        <header class="bg-slate-900 p-4 flex justify-between items-center border-b border-slate-800 shadow-md">
            <div class="flex items-center space-x-3">
                <span class="text-sm bg-slate-800 px-3 py-1 rounded-full text-slate-300">صارف: <b id="user-display" class="text-white">---</b></span>
                <button onclick="logout()" class="text-xs text-red-400 hover:underline">لاگ آؤٹ</button>
                <button id="admin-btn" onclick="openAdminPanel()" class="hidden text-xs text-yellow-400 bg-yellow-950/50 px-2 py-0.5 rounded border border-yellow-700">ایڈمن پینل ⚙️</button>
            </div>
            <div class="bg-gradient-to-r from-yellow-500 to-amber-600 text-slate-950 font-black px-4 py-1.5 rounded-full flex items-center space-x-1 shadow-lg">
                <span>Rs.</span>
                <span id="wallet-balance">0</span>
            </div>
        </header>

        <!-- Main Content -->
        <main class="flex-1 p-4 max-w-md mx-auto w-full space-y-6 pb-24">
            <div class="grid grid-cols-2 gap-3">
                <button onclick="openModal('deposit-modal')" class="bg-green-600 hover:bg-green-700 font-bold py-3 rounded-xl shadow transition">ڈپازٹ (EasyPaisa)</button>
                <button onclick="openModal('withdraw-modal')" class="bg-red-600 hover:bg-red-700 font-bold py-3 rounded-xl shadow transition">ودڈرا (JazzCash)</button>
            </div>

            <h2 class="text-xl font-bold text-yellow-400 border-r-4 border-yellow-400 pr-2 text-right">مقبول گیمز</h2>

            <div class="grid grid-cols-2 gap-4">
                <div onclick="openGame('slots')" class="bg-slate-800 p-4 rounded-2xl border border-slate-700 text-center cursor-pointer hover:scale-105 transition transform">
                    <div class="text-4xl mb-2">🎰</div>
                    <div class="font-bold text-lg">Slots Game</div>
                    <div class="text-xs text-emerald-400 mt-1">ابھی کھیلیں ➔</div>
                </div>
                <div onclick="openGame('spin')" class="bg-slate-800 p-4 rounded-2xl border border-slate-700 text-center cursor-pointer hover:scale-105 transition transform">
                    <div class="text-4xl mb-2">🎡</div>
                    <div class="font-bold text-lg">Lucky Wheel</div>
                    <div class="text-xs text-emerald-400 mt-1">قسمت آزمائیں ➔</div>
                </div>
            </div>
        </main>
    </div>

    <!-- ADMIN PANEL SCREEN -->
    <div id="admin-screen" class="hidden min-h-screen p-4">
        <div class="max-w-md mx-auto bg-slate-900 border border-slate-700 rounded-2xl p-6 space-y-6">
            <div class="flex justify-between items-center border-b border-slate-800 pb-3">
                <button onclick="closeAdminPanel()" class="text-sm text-slate-400 hover:text-white">◀ واپس لابی</button>
                <h2 class="text-2xl font-black text-yellow-400">ہوسٹ / ایڈمن پینل</h2>
            </div>

            <!-- Host Wallet Settings -->
            <div class="bg-slate-800 p-4 rounded-xl border border-slate-700 space-y-3">
                <h3 class="text-md font-bold text-emerald-400 text-right">اپنا ایزی پیسہ نمبر سیٹ کریں</h3>
                <input type="text" id="admin-easypaisa-phone" placeholder="ایزی پیسہ موبائل نمبر" class="w-full p-2.5 bg-slate-900 border border-slate-700 rounded text-right text-sm">
                <input type="text" id="admin-easypaisa-name" placeholder="اکاؤنٹ ہولڈر کا نام" class="w-full p-2.5 bg-slate-900 border border-slate-700 rounded text-right text-sm">
                <button onclick="saveAdminSettings()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-2 rounded text-sm transition">معلومات سیو کریں</button>
            </div>

            <!-- User Management -->
            <div class="bg-slate-800 p-4 rounded-xl border border-slate-700 space-y-3">
                <h3 class="text-md font-bold text-yellow-400 text-right">صارفین کے کوائنز کنٹرول کریں</h3>
                <input type="text" id="manage-target-user" placeholder="صارف کا نام (Username)" class="w-full p-2.5 bg-slate-900 border border-slate-700 rounded text-right text-sm">
                <input type="number" id="manage-coins-amount" placeholder="کوائنز کی تعداد (مثال: 500 یا -500)" class="w-full p-2.5 bg-slate-900 border border-slate-700 rounded text-right text-sm">
                <button onclick="adjustUserCoins()" class="w-full bg-yellow-500 hover:bg-yellow-600 text-slate-950 font-bold py-2 rounded text-sm transition">کوائنز اپڈیٹ کریں</button>
            </div>
        </div>
    </div>

    <!-- 3. SLOTS GAME SCREEN -->
    <div id="slots-screen" class="hidden min-h-screen flex flex-col items-center justify-center p-4">
        <div class="bg-slate-800 p-6 rounded-2xl border border-slate-700 w-full max-w-sm text-center shadow-2xl relative">
            <button onclick="backToLobby()" class="absolute top-4 left-4 text-sm text-slate-400 hover:text-white">◀ لابی</button>
            <h2 class="text-2xl font-black text-yellow-400 mb-6">🎰 SLOTS EXTRA</h2>
            <div class="flex justify-center space-x-4 bg-slate-900 p-6 rounded-xl border-2 border-slate-700 mb-6 text-4xl">
                <span id="slot1">🍒</span><span id="slot2">🍋</span><span id="slot3">🍉</span>
            </div>
            <div class="mb-6">
                <label class="block text-xs text-slate-400 mb-1">بیٹ کی رقم (روپے)</label>
                <input type="number" id="slots-bet" value="50" class="w-32 text-center p-2 rounded bg-slate-900 border border-slate-700 font-bold text-yellow-400">
            </div>
            <button onclick="playSlots()" class="w-full bg-gradient-to-r from-yellow-500 to-amber-500 text-slate-950 font-black p-4 rounded-xl text-lg shadow-lg hover:from-yellow-400 hover:to-amber-400 transition">اسپن کریں (Spin)</button>
            <p id="slots-result" class="mt-4 font-bold text-lg"></p>
        </div>
    </div>

    <!-- 4. LUCKY SPIN SCREEN -->
    <div id="spin-screen" class="hidden min-h-screen flex flex-col items-center justify-center p-4">
        <div class="bg-slate-800 p-6 rounded-2xl border border-slate-700 w-full max-w-sm text-center shadow-2xl relative">
            <button onclick="backToLobby()" class="absolute top-4 left-4 text-sm text-slate-400 hover:text-white">◀ لابی</button>
            <h2 class="text-2xl font-black text-yellow-400 mb-6">🎡 LUCKY SPIN</h2>
            <div id="wheel" class="w-48 h-48 rounded-full border-4 border-yellow-400 mx-auto flex items-center justify-center text-3xl bg-slate-900 shadow-inner mb-6 transition-all duration-1000">💰</div>
            <p class="text-sm text-slate-300 mb-6">فیس: <b>Rs. 20</b> فی اسپن</p>
            <button onclick="playWheel()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-black p-4 rounded-xl text-lg shadow-lg transition">ویل گھمائیں</button>
            <p id="wheel-result" class="mt-4 font-bold text-lg"></p>
        </div>
    </div>

    <!-- MODALS (DEPOSIT / WITHDRAW) -->
    <div id="deposit-modal" class="hidden fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center p-4">
        <div class="bg-slate-800 p-6 rounded-xl w-full max-w-xs border border-slate-700 text-right">
            <h3 class="text-lg font-bold text-green-400 mb-4">رقم ڈپازٹ کریں</h3>
            <p class="text-xs text-slate-400 mb-3">نیچے دیے گئے ہوسٹ کے ایزی پیسہ نمبر پر رقم بھیج کر ٹرانزیکشن ID لکھیں۔</p>
            <div class="bg-slate-900 p-3 rounded text-center mb-4 border border-slate-700">
                <span class="text-xs text-slate-500 block">EasyPaisa اکاؤنٹ نمبر</span>
                <b id="display-host-phone" class="font-mono text-yellow-400 text-md block">03001234567</b>
