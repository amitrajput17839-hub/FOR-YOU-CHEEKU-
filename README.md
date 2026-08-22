<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>For You ❤️</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <!-- Canvas Confetti -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  
  <!-- Custom Styling & Keyframe Animations -->
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap');
    
    * {
      touch-action: manipulation;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
      font-family: 'Plus Jakarta Sans', sans-serif;
    }

    body {
      background-color: #fffafb;
      color: #4a3e3e;
      overflow-x: hidden;
    }

    /* Soft Heartbeat Pulse */
    @keyframes heartbeat {
      0%, 100% { transform: scale(1); }
      15% { transform: scale(1.18); }
      30% { transform: scale(1); }
      45% { transform: scale(1.1); }
    }
    .animate-heartbeat {
      animation: heartbeat 1.8s infinite ease-in-out;
    }

    /* Gentle Floating Animation */
    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-8px); }
    }
    .animate-float {
      animation: float 3s infinite ease-in-out;
    }

    /* Gift Shake Animation */
    @keyframes giftShake {
      0%, 100% { transform: rotate(0deg) scale(1); }
      20% { transform: rotate(-8deg) scale(1.05); }
      40% { transform: rotate(8deg) scale(1.05); }
      60% { transform: rotate(-8deg) scale(1.05); }
      80% { transform: rotate(8deg) scale(1.05); }
    }
    .animate-shake {
      animation: giftShake 0.6s cubic-bezier(.36,.07,.19,.97) both;
    }

    /* Floating background hearts */
    .bg-heart {
      position: fixed;
      color: rgba(255, 182, 193, 0.25);
      pointer-events: none;
      z-index: 0;
      animation: float 4s infinite ease-in-out;
    }

    .screen {
      transition: opacity 0.35s ease, transform 0.35s ease;
    }
    
    .screen-hidden {
      opacity: 0;
      pointer-events: none;
      transform: scale(0.97);
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
    }

    .screen-visible {
      opacity: 1;
      pointer-events: auto;
      transform: scale(1);
      position: relative;
    }
  </style>
</head>
<body class="min-h-screen flex flex-col items-center justify-center p-4 selection:bg-rose-100">

  <!-- Ambient Floating Background Elements -->
  <div class="bg-heart text-4xl top-10 left-6" style="animation-delay: 0s;">🌸</div>
  <div class="bg-heart text-3xl top-1/4 right-8" style="animation-delay: 1s;">✨</div>
  <div class="bg-heart text-5xl bottom-20 left-10" style="animation-delay: 2s;">💖</div>
  <div class="bg-heart text-3xl bottom-10 right-8" style="animation-delay: 1.5s;">🧸</div>

  <!-- Main Container Mobile Wrapper -->
  <main class="w-full max-w-md min-h-[640px] h-[88vh] bg-white/80 backdrop-blur-md rounded-3xl shadow-xl shadow-rose-100/50 border border-rose-100 flex flex-col overflow-hidden relative z-10">

    <!-- ========================================== -->
    <!-- SCREEN 0: OPENING SPLASH SCREEN -->
    <!-- ========================================== -->
    <section id="screen-splash" class="screen screen-visible h-full flex flex-col items-center justify-center text-center p-6 bg-gradient-to-b from-rose-50/50 to-white">
      <div class="animate-heartbeat text-rose-500 mb-6 drop-shadow-sm">
        <i data-lucide="heart" class="w-24 h-24 fill-rose-400 stroke-rose-500"></i>
      </div>
      <h1 class="text-3xl font-bold text-gray-800 tracking-tight mb-2">For You</h1>
      <p class="text-rose-400 font-medium text-sm tracking-wide">A little place made only for you.</p>
    </section>

    <!-- Header Navigation Bar -->
    <header id="app-header" class="hidden px-6 pt-5 pb-2 flex items-center justify-between z-20">
      <button id="btn-back" onclick="navTo('home')" class="inline-flex items-center gap-1.5 text-sm font-semibold text-rose-400 hover:text-rose-600 transition-colors active:scale-95">
        <i data-lucide="chevron-left" class="w-5 h-5"></i>
        <span>For You</span>
      </button>
      <span id="header-title" class="text-xs font-semibold text-rose-300 tracking-widest uppercase"></span>
    </header>

    <!-- Dynamic Content Screens -->
    <div class="flex-1 relative overflow-y-auto overflow-x-hidden p-6 flex flex-col justify-center">

      <!-- ========================================== -->
      <!-- SCREEN 1: HOME SCREEN -->
      <!-- ========================================== -->
      <section id="screen-home" class="screen screen-hidden flex flex-col justify-between h-full py-1">
        <div class="text-center mb-4">
          <h2 class="text-2xl font-bold text-gray-800 flex items-center justify-center gap-2">
            For You <span class="animate-heartbeat inline-block text-rose-500">❤️</span>
          </h2>
          <p class="text-xs text-rose-300 mt-1">Choose a little card below</p>
        </div>

        <div class="grid grid-cols-1 gap-2.5 my-auto">
          <!-- Card 1 -->
          <button onclick="navTo('iloveyou')" class="group relative w-full p-3.5 bg-gradient-to-r from-rose-50 to-white rounded-2xl border border-rose-100/80 shadow-sm hover:shadow-md transition-all active:scale-[0.98] flex items-center justify-between text-left">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center shadow-inner">
                <i data-lucide="heart" class="w-5 h-5 fill-rose-400"></i>
              </div>
              <div>
                <h3 class="font-bold text-gray-800 text-sm group-hover:text-rose-500 transition-colors">I Love You</h3>
                <p class="text-[11px] text-rose-400/80 font-medium">Tap to hear sweet thoughts</p>
              </div>
            </div>
            <i data-lucide="sparkles" class="w-4 h-4 text-rose-300"></i>
          </button>

          <!-- Card 2 -->
          <button onclick="navTo('openwhen')" class="group relative w-full p-3.5 bg-gradient-to-r from-rose-50 to-white rounded-2xl border border-rose-100/80 shadow-sm hover:shadow-md transition-all active:scale-[0.98] flex items-center justify-between text-left">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center shadow-inner">
                <i data-lucide="mail" class="w-5 h-5"></i>
              </div>
              <div>
                <h3 class="font-bold text-gray-800 text-sm group-hover:text-rose-500 transition-colors">Open When...</h3>
                <p class="text-[11px] text-rose-400/80 font-medium">Digital love letters for any mood</p>
              </div>
            </div>
            <i data-lucide="heart-handshake" class="w-4 h-4 text-rose-300"></i>
          </button>

          <!-- Card 3 -->
          <button onclick="navTo('sorry')" class="group relative w-full p-3.5 bg-gradient-to-r from-rose-50 to-white rounded-2xl border border-rose-100/80 shadow-sm hover:shadow-md transition-all active:scale-[0.98] flex items-center justify-between text-left">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center shadow-inner">
                <i data-lucide="smile-plus" class="w-5 h-5"></i>
              </div>
              <div>
                <h3 class="font-bold text-gray-800 text-sm group-hover:text-rose-500 transition-colors">I'm Sorry</h3>
                <p class="text-[11px] text-rose-400/80 font-medium">From my heart to yours</p>
              </div>
            </div>
            <i data-lucide="heart-handshake" class="w-4 h-4 text-rose-300"></i>
          </button>

          <!-- Card 4 -->
          <button onclick="navTo('counter')" class="group relative w-full p-3.5 bg-gradient-to-r from-rose-50 to-white rounded-2xl border border-rose-100/80 shadow-sm hover:shadow-md transition-all active:scale-[0.98] flex items-center justify-between text-left">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center shadow-inner">
                <i data-lucide="infinity" class="w-5 h-5"></i>
              </div>
              <div>
                <h3 class="font-bold text-gray-800 text-sm group-hover:text-rose-500 transition-colors">How Much I Love You</h3>
                <p class="text-[11px] text-rose-400/80 font-medium">Let's try to count it</p>
              </div>
            </div>
            <i data-lucide="calculator" class="w-4 h-4 text-rose-300"></i>
          </button>

          <!-- Card 5 -->
          <button onclick="navTo('surprise')" class="group relative w-full p-3.5 bg-gradient-to-r from-rose-50 to-white rounded-2xl border border-rose-100/80 shadow-sm hover:shadow-md transition-all active:scale-[0.98] flex items-center justify-between text-left">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center shadow-inner">
                <i data-lucide="gift" class="w-5 h-5"></i>
              </div>
              <div>
                <h3 class="font-bold text-gray-800 text-sm group-hover:text-rose-500 transition-colors">A Little Surprise</h3>
                <p class="text-[11px] text-rose-400/80 font-medium">Unwrap something special</p>
              </div>
            </div>
            <i data-lucide="package-open" class="w-4 h-4 text-rose-300"></i>
          </button>
        </div>

        <div class="text-center pt-2">
          <p class="text-[11px] text-rose-300 font-medium">Always yours • No matter what</p>
        </div>
      </section>

      <!-- ========================================== -->
      <!-- FEATURE 1: I LOVE YOU -->
      <!-- ========================================== -->
      <section id="screen-iloveyou" class="screen screen-hidden flex flex-col items-center justify-between h-full text-center py-4">
        <div class="mt-2">
          <p class="text-xs font-semibold text-rose-400 uppercase tracking-widest mb-1">Interactive Love Heart</p>
          <p class="text-sm text-gray-500">Tap the heart whenever you need a reminder</p>
        </div>

        <div class="my-auto flex flex-col items-center w-full">
          <button id="heart-btn" onclick="triggerLoveMessage(event)" class="relative focus:outline-none active:scale-90 transition-transform duration-200 group">
            <div id="heart-icon" class="animate-heartbeat text-rose-500 drop-shadow-md group-hover:scale-105 transition-transform">
              <i data-lucide="heart" class="w-32 h-32 fill-rose-400 stroke-rose-500"></i>
            </div>
            <span class="absolute -bottom-3 left-1/2 -translate-x-1/2 bg-white/90 border border-rose-100 px-3 py-0.5 rounded-full text-xs font-medium text-rose-400 shadow-sm">
              Tap me
            </span>
          </button>

          <div class="min-h-[120px] mt-8 flex items-center justify-center px-4 w-full">
            <p id="love-message-display" class="text-lg font-medium text-gray-700 leading-relaxed transition-all duration-300 opacity-0 transform translate-y-2">
              "Tap the heart above... ❤️"
            </p>
          </div>
        </div>

        <div class="mb-2">
          <p class="text-xs text-rose-400 font-medium animate-pulse">Tap the heart again ❤️</p>
        </div>
      </section>

      <!-- ========================================== -->
      <!-- FEATURE 2: OPEN WHEN... LETTERS -->
      <!-- ========================================== -->
      <section id="screen-openwhen" class="screen screen-hidden flex flex-col items-center justify-between h-full text-center py-1">
        <div id="openwhen-list-view" class="w-full flex flex-col h-full">
          <div class="mb-3 text-left">
            <h2 class="text-xl font-bold text-gray-800">Open When...</h2>
            <p class="text-xs text-rose-400">Pick a letter for whatever you're feeling right now.</p>
          </div>

          <div class="flex-1 overflow-y-auto pr-1 space-y-2 max-h-[400px]" id="letters-container">
            <!-- Letters injected dynamically -->
          </div>
        </div>

        <!-- Single Letter Reading View -->
        <div id="openwhen-read-view" class="hidden w-full flex-col h-full text-left justify-between">
          <div class="bg-rose-50/60 border border-rose-100 p-5 rounded-2xl shadow-inner my-auto max-h-[360px] overflow-y-auto">
            <span id="letter-tag" class="text-[10px] uppercase tracking-wider font-bold text-rose-400 bg-rose-100/80 px-2.5 py-1 rounded-full mb-3 inline-block"></span>
            <h3 id="letter-title" class="text-base font-bold text-gray-800 mb-3"></h3>
            <p id="letter-body" class="text-xs text-gray-700 leading-relaxed whitespace-pre-line"></p>
          </div>

          <button onclick="closeLetter()" class="w-full mt-3 py-3 bg-rose-400 hover:bg-rose-500 text-white font-semibold rounded-xl transition-all active:scale-95 text-xs">
            Back to All Letters ❤️
          </button>
        </div>
      </section>

      <!-- ========================================== -->
      <!-- FEATURE 3: I'M SORRY -->
      <!-- ========================================== -->
      <section id="screen-sorry" class="screen screen-hidden flex flex-col items-center justify-between h-full text-center py-2">
        <div id="sorry-step-1" class="w-full flex flex-col items-center justify-between h-full py-2">
          <div>
            <h2 class="text-2xl font-bold text-gray-800 mb-1">I'm Sorry...</h2>
            <p class="text-xs text-rose-400">I know sometimes I mess things up.</p>
          </div>

          <div class="my-auto flex flex-col items-center">
            <div class="animate-float text-rose-300 my-4">
              <i data-lucide="frown" class="w-24 h-24 stroke-[1.5]"></i>
            </div>
          </div>

          <button onclick="showApologyText()" class="w-full py-3.5 bg-rose-400 hover:bg-rose-500 text-white font-semibold rounded-xl shadow-md shadow-rose-200 transition-all active:scale-95 flex items-center justify-center gap-2">
            <span>Listen to me</span>
            <i data-lucide="heart-handshake" class="w-5 h-5"></i>
          </button>
        </div>

        <div id="sorry-step-2" class="hidden w-full flex-col justify-between h-full py-2 text-left">
          <div class="bg-rose-50/70 border border-rose-100 p-5 rounded-2xl shadow-inner my-auto max-h-[320px] overflow-y-auto">
            <p class="text-sm text-gray-700 leading-relaxed font-normal">
              I know I don't always get everything right.<br><br>
              Sometimes I say things I shouldn't. Sometimes I make mistakes. But I never want my mistakes to make you feel like you are not important to me.<br><br>
              You mean too much to me. I'm genuinely sorry. And I'll always want to make things better between us. ❤️
            </p>
          </div>

          <div class="mt-4 text-center">
            <p class="text-sm font-semibold text-gray-700 mb-3">Forgive me?</p>
            <div class="grid grid-cols-3 gap-2">
              <button onclick="handleApologyChoice('yes')" class="py-2.5 px-3 bg-rose-500 hover:bg-rose-600 text-white text-xs font-semibold rounded-xl transition-all active:scale-95 shadow-sm">
                ❤️ Yes
              </button>
              <button onclick="handleApologyChoice('talk')" class="py-2.5 px-3 bg-rose-100 hover:bg-rose-200 text-rose-600 text-xs font-semibold rounded-xl transition-all active:scale-95">
                💬 Talk to me
              </button>
              <button onclick="handleApologyChoice('angry')" class="py-2.5 px-3 bg-gray-100 hover:bg-gray-200 text-gray-600 text-xs font-semibold rounded-xl transition-all active:scale-95">
                😤 Still angry
              </button>
            </div>
          </div>
        </div>

        <div id="sorry-outcome-yes" class="hidden w-full flex-col items-center justify-center h-full my-auto text-center space-y-4">
          <div class="animate-heartbeat text-rose-500">
            <i data-lucide="heart" class="w-24 h-24 fill-rose-400 stroke-[1.5]"></i>
          </div>
          <h3 class="text-2xl font-bold text-gray-800">Thank you ❤️</h3>
          <p class="text-sm text-rose-500 font-medium">I'll try to do better.</p>
        </div>

        <div id="sorry-outcome-talk" class="hidden w-full flex-col h-full text-left">
          <div class="mb-3">
            <h3 class="text-base font-bold text-gray-800">Okay... I'm listening.</h3>
            <p class="text-xs text-rose-400">Tell me what's in your heart.</p>
          </div>

          <div id="chat-box" class="flex-1 bg-rose-50/40 border border-rose-100 rounded-2xl p-3 overflow-y-auto space-y-2.5 mb-3 max-h-[260px]">
            <div class="bg-white border border-rose-100 text-gray-700 text-xs p-3 rounded-2xl rounded-tl-none max-w-[85%] shadow-sm">
              I'm here for you. Take all the time you need...
            </div>
          </div>

          <form onsubmit="sendPrivateMessage(event)" class="flex gap-2">
            <input type="text" id="chat-input" placeholder="Type what you feel..." class="flex-1 text-xs px-3.5 py-2.5 rounded-xl border border-rose-200 focus:outline-none focus:border-rose-400 bg-white shadow-sm" />
            <button type="submit" class="bg-rose-400 hover:bg-rose-500 text-white px-4 py-2.5 rounded-xl text-xs font-semibold transition-all active:scale-95 shadow-sm">
              Send
            </button>
          </form>
        </div>

        <div id="sorry-outcome-angry" class="hidden w-full flex-col items-center justify-center h-full my-auto text-center space-y-4">
          <div class="animate-float text-rose-300">
            <i data-lucide="shield-alert" class="w-20 h-20"></i>
          </div>
          <h3 class="text-xl font-bold text-gray-800">Okay... I understand.</h3>
          <p class="text-sm text-rose-400 font-medium">I'm still here. ❤️</p>
        </div>
      </section>

      <!-- ========================================== -->
      <!-- FEATURE 4: HOW MUCH I LOVE YOU -->
      <!-- ========================================== -->
      <section id="screen-counter" class="screen screen-hidden flex flex-col items-center justify-between h-full text-center py-4">
        <div>
          <h2 class="text-xl font-bold text-gray-800 mb-1">How Much I Love You</h2>
          <p class="text-xs text-rose-400">Want to know how much I love you?</p>
        </div>

        <div class="my-auto flex flex-col items-center w-full">
          <div class="w-full py-8 px-4 bg-gradient-to-b from-rose-50 to-white rounded-3xl border border-rose-100 shadow-inner flex flex-col items-center justify-center min-h-[180px]">
            <span id="counter-value" class="text-5xl font-extrabold text-rose-500 tracking-tight transition-all">0%</span>
            <p id="counter-subtext" class="text-xs text-rose-400 font-medium mt-3 opacity-0 transition-opacity duration-500 min-h-[16px]"></p>
          </div>
        </div>

        <button id="counter-btn" onclick="startLoveCounter()" class="w-full py-3.5 bg-rose-400 hover:bg-rose-500 text-white font-semibold rounded-xl shadow-md shadow-rose-200 transition-all active:scale-95 flex items-center justify-center gap-2">
          <i data-lucide="heart" class="w-5 h-5 fill-white"></i>
          <span id="counter-btn-text">MEASURE MY LOVE ❤️</span>
        </button>
      </section>

      <!-- ===================================
