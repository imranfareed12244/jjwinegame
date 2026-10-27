<!DOCTYPE html>
<html lang="ur">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JJWine - Real Earning Game with Admin Panel</title>
    <script src="https://jsdelivr.net"></script>
    <style>
        body {
            background: linear-gradient(135deg, #0f172a, #1e1b4b);
            color: white;
            font-family: sans-serif;
        }
        .hidden { display: none; }
    </style>
</head>
<body class="flex flex-col min-h-screen items-center justify-center p-4">

    <!-- 1. AUTH SCREEN -->
    <div id="auth-screen" class="w-full max-w-md bg-slate-900/80 p-6 rounded-2xl shadow-2xl border border-slate-700 backdrop-blur-md">
        <h1 class="text-3xl font-black text-center mb-2 text-transparent bg-clip-text bg-gradient-to-r from-yellow-400 to-amber-500 tracking-wider">JJWINE GAME</h1>
        <p class="text-slate-400 text-center text-sm mb-6">The Best Game & Real Platform</p>
        
        <div class="flex bg-slate-800 p-1 rounded-xl mb-6">
            <button id="tab-login" class="flex-1 py-2.5 rounded-lg text-sm font-bold bg-amber-500 text-slate-950 transition-all">Login</button>
            <button id="tab-register" class="flex-1 py-2.5 rounded-lg text-sm font-bold text-slate-400 transition-all">Register</button>
        </div>

        <form id="auth-form" class="space-y-4">
            <div id="username-container" class="hidden">
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1">Full Name</label>
                <input type="text" id="auth-username" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-amber-500 transition-all" placeholder="Enter your name">
            </div>
            <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1">Mobile Number</label>
                <input type="tel" id="auth-phone" required class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-amber-500 transition-all" placeholder="03XXXXXXXXX">
            </div>
            <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-1">Password</label>
                <input type="password" id="auth-password" required class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3 text-white focus:outline-none focus:border-amber-500 transition-all" placeholder="••••••••">
            </div>
            <button type="submit" id="auth-btn" class="w-full bg-gradient-to-r from-yellow-400 to-amber-500 text-slate-950 font-black py-4 rounded-xl shadow-lg transition-all text-base tracking-wide mt-2">LOGIN TO ACCOUNT</button>
        </form>
    </div>

    <!-- 2. GAME MAIN SCREEN -->
    <div id="game-screen" class="w-full max-w-md bg-slate-900/80 rounded-2xl shadow-2xl border border-slate-700 backdrop-blur-md overflow-hidden hidden">
        <div class="bg-slate-800/80 p-4 border-b border-slate-700 flex justify-between items-center">
            <div>
                <p class="text-xs text-slate-400">Welcome back,</p>
                <h2 id="player-name" class="font-bold text-amber-400">Player</h2>
            </div>
            <div class="text-right">
                <p class="text-xs text-slate-400">Total Balance</p>
                <p class="text-xl font-black text-emerald-400">Rs. <span id="balance">0</span></p>
            </div>
        </div>

        <div class="p-6 flex flex-col items-center">
            <div class="w-full bg-slate-950 rounded-2xl p-6 border-2 border-slate-800 mb-6 flex justify-around items-center text-4xl h-28 shadow-inner">
                <div id="slot1">🍷</div>
                <div id="slot2">🍇</div>
                <div id="slot3">🍾</div>
            </div>

            <div class="w-full mb-6">
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-400 mb-2 text-center">Select Bet Amount</label>
                <div class="grid grid-cols-4 gap-2">
                    <button class="bet-btn bg-slate-800 py-2.5 rounded-xl font-bold border border-slate-700 active:bg-amber-500 text-sm" data-amount="20">20</button>
                    <button class="bet-btn bg-slate-800 py-2.5 rounded-xl font-bold border border-slate-700 active:bg-amber-500 text-sm" data-amount="50">50</button>
                    <button class="bet-btn bg-slate-800 py-2.5 rounded-xl font-bold border border-slate-700 active:bg-amber-500 text-sm" data-amount="100">100</button>
                    <button class="bet-btn bg-slate-800 py-2.5 rounded-xl font-bold border border-slate-700 active:bg-amber-500 text-sm" data-amount="200">200</button>
                </div>
                <p class="text-xs text-center text-slate-400 mt-3">Selected Bet: <span id="current-bet" class="text-amber-400 font-bold">Rs. 20</span></p>
            </div>
            <button id="spin-btn" class="w-full bg-gradient-to-r from-emerald-500 to-green-600 text-slate-950 font-black py-4 rounded-xl text-lg tracking-wider active:scale-95 transition-all">SPIN & EARN</button>
        </div>

        <div class="grid grid-cols-3 bg-slate-800 border-t border-slate-700 text-center text-xs font-bold">
            <button id="nav-game" class="py-4 text-amber-400 border-b-2 border-amber-400">Game</button>
            <button id="nav-deposit" class="py-4 text-slate-400">Deposit</button>
            <button id="nav-withdraw" class="py-4 text-slate-400">Withdraw</button>
        </div>
    </div>

    <!-- 3. DEPOSIT SCREEN -->
    <div id="deposit-screen" class="w-full max-w-md bg-slate-900/80 p-6 rounded-2xl shadow-2xl border border-slate-700 backdrop-blur-md hidden">
        <h2 class="text-2xl font-black text-amber-400 mb-4 text-center">EasyPaisa / JazzCash Deposit</h2>
        <div class="bg-slate-800 p-4 rounded-xl mb-4 text-sm space-y-2 border border-slate-700">
            <p><span class="text-slate-400">Account Name:</span> <strong class="text-white">JJWINE Admin</strong></p>
            <p><span class="text-slate-400">Account Number:</span> <strong id="admin-phone-display" class="text-amber-400 text-lg">03001234567</strong></p>
        </div>
        <form id="deposit-form" class="space-y-4">
            <div>
                <label class="block text-xs font-bold text-slate-400 mb-1">Amount Sent (Rs.)</label>
                <input type="number" id="dep-amount" required min="100" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3" placeholder="Minimum 100">
            </div>
            <div>
                <label class="block text-xs font-bold text-slate-400 mb-1">TRX ID / Transaction ID</label>
                <input type="text" id="dep-trx" required class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3" placeholder="Enter TRX ID">
            </div>
            <button type="submit" class="w-full bg-amber-500 text-slate-950 font-black py-3 rounded-xl">SUBMIT DEPOSIT REQUEST</button>
        </form>
        <button class="back-to-game w-full text-center text-sm font-bold text-slate-400 mt-4 underline">Back to Game</button>
    </div>

    <!-- 4. WITHDRAW SCREEN -->
    <div id="withdraw-screen" class="w-full max-w-md bg-slate-900/80 p-6 rounded-2xl shadow-2xl border border-slate-700 backdrop-blur-md hidden">
        <h2 class="text-2xl font-black text-rose-400 mb-4 text-center">Fast Withdrawal</h2>
        <form id="withdraw-form" class="space-y-4">
            <div>
                <label class="block text-xs font-bold text-slate-400 mb-1">Select Method</label>
                <select id="wit-method" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3 text-white">
                    <option value="EasyPaisa">EasyPaisa</option>
                    <option value="JazzCash">JazzCash</option>
                </select>
            </div>
            <div>
                <label class="block text-xs font-bold text-slate-400 mb-1">Account Number</label>
                <input type="tel" id="wit-number" required class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3" placeholder="03XXXXXXXXX">
            </div>
            <div>
                <label class="block text-xs font-bold text-slate-400 mb-1">Amount to Withdraw (Rs.)</label>
                <input type="number" id="wit-amount" required min="500" class="w-full bg-slate-800 border border-slate-700 rounded-xl px-4 py-3" placeholder="Minimum 500">
            </div>
            <button type="submit" class="w-full bg-rose-500 text-white font-black py-3 rounded-xl">REQUEST WITHDRAWAL</button>
        </form>
        <button class="back-to-game w-full text-center text-sm font-bold text-slate-400 mt-4 underline">Back to Game</button>
    </div>

    <!-- 5. HOST / ADMIN CONTROL PANEL SCREEN -->
    <div id="admin-screen" class="w-full max-w-xl bg-slate-900/90 p-6 rounded-2xl shadow-2xl border-2 border-amber-500 backdrop-blur-md hidden">
        <div class="flex justify-between items-center mb-6 border-b border-slate-700 pb-3">
            <h2 class="text-2xl font-black text-amber-400">👑 HOST CONTROL PANEL</h2>
            <button id="admin-logout" class="bg-rose-600 text-xs px-3 py-1.5 rounded-lg font-bold">Logout</button>
        </div>
        
        <!-- EasyPaisa Number Setup -->
        <div class="mb-6 bg-slate-800 p-4 rounded-xl border border-slate-700">
            <h3 class="text-sm font-bold text-slate-300 mb-2">Change EasyPaisa/JazzCash Receiving Number</h3>
            <div class="flex gap-2">
                <input type="tel" id="new-admin-phone" class="flex-1 bg-slate-900 border border-slate-700 rounded-lg px-3 py-2 text-sm text-white" placeholder="Enter new number">
