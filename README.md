<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>For You ❤️</title>
  
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/lucide@latest"></script>
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap');
    
    * {
      touch-action: manipulation;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
      font-family: 'Plus Jakarta Sans', sans-serif;
    }

    body {
      background: linear-gradient(135deg, #fff5f7 0%, #ffeef2 100%);
      color: #4a3e3e;
      min-height: 100vh;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
    }

    @keyframes heartbeat {
      0%, 100% { transform: scale(1); }
      15% { transform: scale(1.15); }
      30% { transform: scale(1); }
      45% { transform: scale(1.08); }
    }
    .animate-heartbeat {
      animation: heartbeat 1.8s infinite ease-in-out;
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
    }
    .animate-float {
      animation: float 3s infinite ease-in-out;
    }

    @keyframes giftShake {
      0%, 100% { transform: rotate(0deg) scale(1); }
      20% { transform: rotate(-8deg) scale(1.05); }
      40% { transform: rotate(8deg) scale(1.05); }
      60% { transform: rotate(-8deg) scale(1.05); }
      80% { transform: rotate(8deg) scale(1.05); }
    }
    .animate-shake {
      animation: giftShake 0.6s ease-in-out both;
    }

    .app-screen {
      display: none;
      width: 100%;
      height: 100%;
      flex-direction: column;
      animation: fadeIn 0.3s ease-in-out forwards;
    }

    .app-screen.active {
      display: flex;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body class="min-h-screen w-full flex flex-col justify-between items-center p-4 md:p-8">

  <!-- Floating background decorations -->
  <div class="fixed top-8 left-8 text-3xl opacity-30 pointer-events-none animate-float">🌸</div>
  <div class="fixed top-12 right-12 text-2xl opacity-30 pointer-events-none animate-float" style="animation-delay: 1s;">✨</div>
  <div class="fixed bottom-12 left-12 text-4xl opacity-30 pointer-events-none animate-float" style="animation-delay: 2s;">💖</div>
  <div class="fixed bottom-8 right-8 text-3xl opacity-30 pointer-events-none animate-float" style="animation-delay: 1.5s;">🧸</div>

  <!-- Header Bar -->
  <header id="app-header" class="w-full max-w-2xl mx-auto flex items-center justify-between pb-4 border-b border-rose-200/60 mb-4 hidden">
    <button onclick="navTo('home')" class="inline-flex items-center gap-2 text-sm font-bold text-rose-500 hover:text-rose-600 bg-white/80 backdrop-blur px-4 py-2 rounded-full shadow-sm border border-rose-100 transition-all active:scale-95">
      <i data-lucide="arrow-left" class="w-4 h-4"></i>
      <span>← For You</span>
    </button>
    <span id="header-title" class="text-xs font-bold text-rose-400 tracking-wider uppercase"></span>
  </header>

  <!-- Main Responsive Container -->
  <main class="w-full max-w-2xl mx-auto flex-1 flex flex-col justify-center items-center relative z-10 my-auto">

    <!-- ========================================== -->
    <!-- SCREEN 0: SPLASH SCREEN -->
    <!-- ========================================== -->
    <section id="screen-splash" class="app-screen active items-center justify-center text-center py-12">
      <div class="animate-heartbeat text-rose-500 mb-6">
        <i data-lucide="heart" class="w-28 h-28 fill-rose-400 stroke-rose-500"></i>
      </div>
      <h1 class="text-4xl font-extrabold text-gray-800 tracking-tight mb-2">For You</h1>
      <p class="text-rose-400 font-medium text-base">A little place made only for you.</p>
      <button onclick="navTo('home')" class="mt-8 px-6 py-2.5 bg-rose-400 text-white rounded-full font-semibold text-xs shadow-md animate-pulse">
        Tap to Enter ❤️
      </button>
    </section>

    <!-- ========================================== -->
    <!-- SCREEN 1: HOME SCREEN -->
    <!-- ========================================== -->
    <section id="screen-home" class="app-screen text-center py-4 w-full">
      <div class="mb-6">
        <h2 class="text-3xl font-extrabold text-gray-800 flex items-center justify-center gap-2">
          For You <span class="animate-heartbeat text-rose-500">❤️</span>
        </h2>
        <p class="text-xs text-rose-400 font-medium mt-1">Tap any card below to open its experience</p>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 w-full max-w-xl mx-auto">
        <!-- Card 1 -->
        <button onclick="navTo('iloveyou')" class="p-5 bg-white/90 backdrop-blur rounded-2xl border border-rose-200/80 shadow-sm hover:shadow-md transition-all active:scale-95 flex items-center justify-between text-left group">
          <div class="flex items-center gap-4">
            <div class="w-12 h-12 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center">
              <i data-lucide="heart" class="w-6 h-6 fill-rose-400"></i>
            </div>
            <div>
              <h3 class="font-bold text-gray-800 text-base group-hover:text-rose-500">I Love You</h3>
              <p class="text-xs text-rose-400">Sweet thoughts</p>
            </div>
          </div>
          <i data-lucide="sparkles" class="w-5 h-5 text-rose-300"></i>
        </button>

        <!-- Card 2 -->
        <button onclick="navTo('openwhen')" class="p-5 bg-white/90 backdrop-blur rounded-2xl border border-rose-200/80 shadow-sm hover:shadow-md transition-all active:scale-95 flex items-center justify-between text-left group">
          <div class="flex items-center gap-4">
            <div class="w-12 h-12 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center">
              <i data-lucide="mail" class="w-6 h-6"></i>
            </div>
            <div>
              <h3 class="font-bold text-gray-800 text-base group-hover:text-rose-500">Open When...</h3>
              <p class="text-xs text-rose-400">Love letters</p>
            </div>
          </div>
          <i data-lucide="heart-handshake" class="w-5 h-5 text-rose-300"></i>
        </button>

        <!-- Card 3 -->
        <button onclick="navTo('sorry')" class="p-5 bg-white/90 backdrop-blur rounded-2xl border border-rose-200/80 shadow-sm hover:shadow-md transition-all active:scale-95 flex items-center justify-between text-left group">
          <div class="flex items-center gap-4">
            <div class="w-12 h-12 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center">
              <i data-lucide="smile-plus" class="w-6 h-6"></i>
            </div>
            <div>
              <h3 class="font-bold text-gray-800 text-base group-hover:text-rose-500">I'm Sorry</h3>
              <p class="text-xs text-rose-400">From my heart</p>
            </div>
          </div>
          <i data-lucide="heart" class="w-5 h-5 text-rose-300"></i>
        </button>

        <!-- Card 4 -->
        <button onclick="navTo('counter')" class="p-5 bg-white/90 backdrop-blur rounded-2xl border border-rose-200/80 shadow-sm hover:shadow-md transition-all active:scale-95 flex items-center justify-between text-left group">
          <div class="flex items-center gap-4">
            <div class="w-12 h-12 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center">
              <i data-lucide="infinity" class="w-6 h-6"></i>
            </div>
            <div>
              <h3 class="font-bold text-gray-800 text-base group-hover:text-rose-500">How Much I Love You</h3>
              <p class="text-xs text-rose-400">Love counter</p>
            </div>
          </div>
          <i data-lucide="calculator" class="w-5 h-5 text-rose-300"></i>
        </button>

        <!-- Card 5 -->
        <button onclick="navTo('surprise')" class="p-5 bg-white/90 backdrop-blur rounded-2xl border border-rose-200/80 shadow-sm hover:shadow-md transition-all active:scale-95 flex items-center justify-between text-left group sm:col-span-2">
          <div class="flex items-center gap-4">
            <div class="w-12 h-12 rounded-xl bg-rose-100 text-rose-500 flex items-center justify-center">
              <i data-lucide="gift" class="w-6 h-6"></i>
            </div>
            <div>
              <h3 class="font-bold text-gray-800 text-base group-hover:text-rose-500">A Little Surprise</h3>
              <p class="text-xs text-rose-400">Unwrap something sweet</p>
            </div>
          </div>
          <i data-lucide="package-open" class="w-5 h-5 text-rose-300"></i>
        </button>
      </div>
    </section>

    <!-- ========================================== -->
    <!-- SCREEN 2: I LOVE YOU -->
    <!-- ========================================== -->
    <section id="screen-iloveyou" class="app-screen text-center py-6 w-full items-center">
      <div class="mb-6">
        <h3 class="text-2xl font-bold text-gray-800">I Love You ❤️</h3>
        <p class="text-xs text-rose-400">Tap the heart to get a sweet message</p>
      </div>

      <button id="heart-btn" onclick="triggerLoveMessage()" class="my-auto focus:outline-none active:scale-90 transition-transform cursor-pointer">
        <div id="heart-icon" class="animate-heartbeat text-rose-500 drop-shadow-md hover:scale-105 transition-transform">
          <i data-lucide="heart" class="w-36 h-36 fill-rose-400 stroke-rose-500"></i>
        </div>
      </button>

      <div class="min-h-[100px] mt-8 max-w-md mx-auto flex items-center justify-center px-4">
        <p id="love-message-display" class="text-xl font-semibold text-gray-700 leading-relaxed transition-all duration-300">
          "Tap the heart above... ❤️"
        </p>
      </div>
    </section>

    <!-- ========================================== -->
    <!-- SCREEN 3: OPEN WHEN LETTERS -->
    <!-- ========================================== -->
    <section id="screen-openwhen" class="app-screen py-4 w-full">
      <div id="openwhen-list-view" class="w-full">
        <div class="mb-4 text-center">
          <h3 class="text-2xl font-bold text-gray-800">Open When...</h3>
          <p class="text-xs text-rose-400">Digital love letters written for any moment</p>
        </div>

        <div id="letters-container" class="space-y-3 max-w-md mx-auto"></div>
      </div>

      <div id="openwhen-read-view" class="hidden w-full max-w-md mx-auto flex-col">
        <div class="bg-white p-6 rounded-2xl border border-rose-200 shadow-sm mb-4">
          <span id="letter-tag" class="text-[10px] uppercase font-bold text-rose-500 bg-rose-100 px-3 py-1 rounded-full inline-block mb-3"></span>
          <h4 id="letter-title" class="text-lg font-bold text-gray-800 mb-3"></h4>
          <p id="letter-body" class="text-sm text-gray-700 leading-relaxed whitespace-pre-line"></p>
        </div>
        <button onclick="closeLetter()" class="w-full py-3 bg-rose-400 text-white font-bold rounded-xl shadow-md text-xs">
          Back to All Letters ❤️
        </button>
      </div>
    </section>

    <!-- ========================================== -->
    <!-- SCREEN 4: I'M SORRY -->
    <!-- ========================================== -->
    <section id="screen-sorry" class="app-screen text-center py-4 w-full items-center">
      <div id="sorry-step-1" class="w-full max-w-md mx-auto flex flex-col items-center">
        <h3 class="text-2xl font-bold text-gray-800 mb-1">I'm Sorry...</h3>
        <p class="text-xs text-rose-400 mb-6">I know sometimes I mess things up.</p>

        <div class="animate-float text-rose-300 my-6">
          <i data-lucide="frown" class="w-24 h-24 stroke-[1.5]"></i>
        </div>

        <button onclick="showApologyText()" class="w-full py-3.5 bg-rose-400 text-white font-bold rounded-xl shadow-md mt-6">
          Listen to me ❤️
        </button>
      </div>

      <div id="sorry-step-2" class="hidden w-full max-w-md mx-auto flex-col text-left">
        <div class="bg-white p-6 rounded-2xl border border-rose-200 shadow-sm mb-4">
          <p class="text-sm text-gray-700 leading-relaxed">
            I know I don't always get everything right.<br><br>
            Sometimes I say things I shouldn't. Sometimes I make mistakes. But I never want my mistakes to make you feel like you are not important to me.<br><br>
            You mean too much to me. I'm genuinely sorry. And I'll always want to make things better between us. ❤️
          </p>
        </div>

        <p class="text-center text-sm font-bold text-gray-700 mb-3">Forgive me?</p>
        <div class="grid grid-cols-3 gap-2">
          <button onclick="handleApologyChoice('yes')" class="py-3 bg-rose-500 text-white text-xs font-bold rounded-xl shadow-sm">❤️ Yes</button>
          <button onclick="handleApologyChoice('talk')" class="py-3 bg-rose-100 text-rose-600 text-xs font-bold rounded-xl">💬 Talk to me</button>
          <button onclick="handleApologyChoice('angry')" class="py-3 bg-gray-100 text-gray-600 text-xs font-bold rounded-xl">😤 Still angry</button>
        </div>
      </div>

      <div id="sorry-outcome-yes" class="hidden w-full max-w-md mx-auto flex-col items-center my-auto space-y-4">
        <i data-lucide="heart" class="w-20 h-20 fill-rose-400 text-rose-500 animate-heartbeat"></i>
        <h4 class="text-2xl font-bold text-gray-800">Thank you ❤️</h4>
        <p class="text-xs text-rose-500 font-medium">I'll try to do better.</p>
      </div>

      <div id="sorry-outcome-talk" class="hidden w-full max-w-md mx-auto flex-col text-left">
        <h4 class="text-base font-bold text-gray-800 mb-1">Okay... I'm listening.</h4>
        <p class="text-xs text-rose-400 mb-3">Tell me what's in your heart.</p>
        <div id="chat-box" class="bg-white border border-rose-200 rounded-2xl p-4 min-h-[160px] max-h-[220px] overflow-y-auto space-y-2 mb-3">
          <div class="bg-rose-50 text-gray-700 text-xs p-3 rounded-2xl rounded-tl-none max-w-[85%]">
            I'm here for you. Take all the time you need...
          </div>
        </div>
        <form onsubmit="sendPrivateMessage(event)" class="flex gap-2">
          <input type="text" id="chat-input" placeholder="Type what you feel..." class="flex-1 text-xs p-3 rounded-xl border border-rose-200 bg-white" />
          <button type="submit" class="bg-rose-400 text-white px-4 py-3 rounded-xl text-xs font-bold">Send</button>
        </form>
      </div>

      <div id="sorry-outcome-angry" class="hidden w-full max-w-md mx-auto flex-col items-center my-auto space-y-3">
        <i data-lucide="shield-alert" class="w-16 h-16 text-rose-300"></i>
        <h4 class="text-xl font-bold text-gray-800">Okay... I understand.</h4>
        <p class="text-xs text-rose-400 font-medium">I'm still here. ❤️</p>
      </div>
    </section>

    <!-- ========================================== -->
    <!-- SCREEN 5: HOW MUCH I LOVE YOU -->
    <!-- ========================================== -->
    <section id="screen-counter" class="app-screen text-center py-4 w-full items-center">
      <div class="mb-4">
        <h3 class="text-2xl font-bold text-gray-800">How Much I Love You</h3>
        <p class="text-xs text-rose-400">Want to know how much I love you?</p>
      </div>

      <div class="w-full max-w-md my-auto py-10 px-4 bg-white rounded-3xl border border-rose-200 shadow-sm flex flex-col items-center">
        <span id="counter-value" class="text-6xl font-extrabold text-rose-500 tracking-tight">0%</span>
        <p id="counter-subtext" class="text-xs text-rose-400 font-semibold mt-4 min-h-[20px]"></p>
      </div>

      <button id="counter-btn" onclick="startLoveCounter()" class="w-full max-w-md mt-6 py-3.5 bg-rose-400 text-white font-bold rounded-xl shadow-md">
        <span id="counter-btn-text">MEASURE MY LOVE ❤️</span>
      </button>
    </section>

    <!-- ========================================== -->
    <!-- SCREEN 6: A LITTLE SURPRISE -->
    <!-- ========================================== -->
    <section id="screen-surprise" class="app-screen text-center py-4 w-full items-center">
      <div class="mb-4">
        <h3 class="text-2xl font-bold text-gray-800">A Little Surprise</h3>
        <p class="text-xs text-rose-400">I made something for you...</p>
      </div>

      <div class="my-auto flex flex-col items-center w-full max-w-md">
        <div id="gift-box-icon" class="text-rose-400 cursor-pointer my-4" onclick="openSurprise()">
          <i data-lucide="gift" class="w-28 h-28 stroke-[1.25]"></i>
        </div>

        <div class="bg-white p-6 rounded-2xl border border-rose-200 shadow-sm w-full min-h-[120px] flex flex-col items-center justify-center">
          <p id="surprise-text" class="text-base font-semibold text-gray-700 italic">
            "Tap the button below to open your surprise..."
          </p>
          <span id="surprise-badge" class="hidden mt-2 text-[10px] font-bold bg-rose-100 text-rose-500 px-3 py-1 rounded-full"></span>
        </div>
      </div>

      <button onclick="openSurprise()" class="w-full max-w-md mt-6 py-3.5 bg-rose-400 text-white font-bold rounded-xl shadow-md">
        Open it ❤️
      </button>
    </section>

  </main>

  <footer class="w-full text-center py-2 text-[11px] text-rose-300 font-medium">
    Made with love • Always yours
  </footer>

  <script>
    const LOVE_MESSAGES = [
      "I love you.",
      "You are my favourite person.",
      "I would still choose you.",
      "You make ordinary days feel special.",
      "I hope you never forget how loved you are.",
      "I love having you in my life.",
      "You make my world a little better.",
      "I don't need a perfect life. I just want you in mine.",
      "You are one of the best things that ever happened to me.",
      "If you ask me why I love you, I probably won't know how to explain it.",
      "Somehow, my favourite place is wherever you are.",
      "I could tell you a thousand times and still not get tired of saying it.",
      "The world feels a little softer when you're around.",
      "I hope you know how special you are to me.",
      "I'd choose you in every version of my life."
    ];

    const OPEN_WHEN_LETTERS = [
      {
        title: "Open when... You miss me",
        icon: "heart-handshake",
        tag: "Missing You",
        body: "I wish I could wrap my arms around you right now. Distance or time doesn't change how much you mean to me.\n\nWhenever you feel this way, take a deep breath and close your eyes—I'm holding your hand in my heart."
      },
      {
        title: "Open when... You had a hard day",
        icon: "cloud-rain",
        tag: "Comfort",
        body: "Today might have been exhausting, but you made it through. I am so proud of you.\n\nUnwind, let go of the pressure, and rest easy. I am right here cheering for you, always."
      },
      {
        title: "Open when... You're feeling insecure",
        icon: "shield-check",
        tag: "Reminder",
        body: "You are more than enough. You don't have to prove anything to be worthy of love.\n\nTo me, you are radiant, kind, and precious. Don't let doubt make you forget how amazing you truly are."
      },
      {
        title: "Open when... You need a smile",
        icon: "smile",
        tag: "Joy",
        body: "Fun fact: Somewhere right now, I'm probably thinking about you and smiling like an idiot.\n\nNow it's your turn. Give me that beautiful smile. You deserve pure happiness today."
      },
      {
        title: "Open when... You can't sleep",
        icon: "moon",
        tag: "Nighttime",
        body: "The night is quiet, and so should your mind be. Turn off the
