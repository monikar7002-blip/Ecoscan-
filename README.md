# Ecoscan-
Waste management 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>EcoScan - Scan it. Sort it. Save the planet!</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Canvas Confetti CDN for Celebrations -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  <!-- Google Fonts for Kid-Friendly Typography -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Quicksand:wght@500;600;700&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            'eco-leaf': '#4CAF50',
            'eco-leaf-dark': '#388E3C',
            'eco-sky': '#4FC3F7',
            'eco-sun': '#FFD54F',
            'eco-cream': '#FFFDE7',
            'eco-orange': '#FF8A65',
            'eco-bg': '#E8F5E9',
            'bin-plastic': '#FF9800',
            'bin-paper': '#2196F3',
            'bin-glass': '#4CAF50',
            'bin-metal': '#9C27B0',
            'bin-organic': '#795548',
          },
          fontFamily: {
            fredoka: ['Fredoka', 'sans-serif'],
            quicksand: ['Quicksand', 'sans-serif'],
          },
          boxShadow: {
            'pop': '0 8px 0px 0px rgba(0, 0, 0, 0.12)',
            'pop-sm': '0 4px 0px 0px rgba(0, 0, 0, 0.1)',
            'inner-soft': 'inset 0 2px 4px 0 rgba(0, 0, 0, 0.06)',
          }
        }
      }
    }
  </script>

  <style>
    body {
      font-family: 'Fredoka', 'Quicksand', sans-serif;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
      background-color: #121826;
    }

    /* Screen transition animations */
    .screen-view {
      transition: all 0.25s ease-in-out;
    }
    
    .screen-enter {
      opacity: 0;
      transform: scale(0.97) translateY(8px);
    }
    .screen-active {
      opacity: 1;
      transform: scale(1) translateY(0);
    }

    /* Custom Animations */
    @keyframes bounce-gentle {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-8px); }
    }
    .animate-bounce-gentle {
      animation: bounce-gentle 2.2s infinite ease-in-out;
    }

    @keyframes pulse-ring {
      0% { transform: scale(0.95); opacity: 0.8; }
      50% { transform: scale(1.08); opacity: 0.4; }
      100% { transform: scale(0.95); opacity: 0.8; }
    }
    .animate-pulse-ring {
      animation: pulse-ring 2s infinite ease-in-out;
    }

    @keyframes scan-beam {
      0% { top: 5%; }
      50% { top: 85%; }
      100% { top: 5%; }
    }
    .animate-scan-beam {
      animation: scan-beam 2s infinite ease-in-out;
    }

    /* Scrollbar Styling for Clean UI */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: transparent;
    }
    ::-webkit-scrollbar-thumb {
      background: #A5D6A7;
      border-radius: 10px;
    }
  </style>
</head>
<body class="flex justify-center items-center min-h-screen p-0 sm:p-4">

  <!-- Mobile Device Frame Container -->
  <div id="app-container" class="relative w-full max-w-md h-screen sm:h-[844px] bg-eco-bg sm:rounded-[40px] shadow-2xl overflow-hidden flex flex-col border-0 sm:border-8 border-gray-800">
    
    <!-- Top Status / Header Bar -->
    <header id="top-header" class="bg-white/80 backdrop-blur-md px-5 py-3 flex justify-between items-center z-20 border-b border-green-100 hidden">
      <div class="flex items-center space-x-2 cursor-pointer" onclick="app.navigateTo('screen-home')">
        <div class="w-9 h-9 bg-eco-leaf rounded-full flex items-center justify-center text-white font-bold text-lg shadow-sm">
          🌱
        </div>
        <div>
          <h1 class="text-lg font-bold text-gray-800 leading-tight">EcoScan</h1>
          <p class="text-[10px] text-green-700 font-semibold tracking-wide uppercase">Eco Hero</p>
        </div>
      </div>

      <!-- Points Pill -->
      <div class="flex items-center space-x-1.5 bg-amber-100 border-2 border-amber-300 px-3 py-1 rounded-full shadow-inner-soft cursor-pointer hover:scale-105 transition-transform" onclick="app.navigateTo('screen-achievements')">
        <span class="text-lg">⭐</span>
        <span id="user-points-display" class="font-bold text-amber-900 text-sm">0</span>
        <span class="text-xs text-amber-700 font-semibold">pts</span>
      </div>
    </header>

    <!-- MAIN DYNAMIC CONTENT CONTAINER -->
    <main id="main-stage" class="flex-1 overflow-y-auto relative flex flex-col">
      
      <!-- SCREEN 1: WELCOME -->
      <section id="screen-welcome" class="screen-view active flex-1 flex flex-col justify-between p-6 text-center bg-gradient-to-b from-eco-bg via-white to-green-50">
        <div class="pt-8">
          <div class="inline-block px-4 py-1.5 bg-green-200 text-green-800 rounded-full font-semibold text-xs tracking-wider uppercase mb-3 shadow-sm">
            Interactive Kids Prototype
          </div>
          <h1 class="text-4xl font-extrabold text-gray-800 tracking-tight">EcoScan</h1>
          <p class="text-green-700 font-medium text-sm mt-1">Scan it. Sort it. Save the planet!</p>
        </div>

        <!-- Eco Buddy Mascot Greeting -->
        <div class="my-auto flex flex-col items-center">
          <div class="relative w-48 h-48 flex items-center justify-center">
            <div class="absolute inset-0 bg-green-200 rounded-full animate-pulse-ring opacity-60"></div>
            <!-- Eco Buddy SVG Mascot -->
            <svg class="w-40 h-40 animate-bounce-gentle relative z-10" viewBox="0 0 100 100" fill="none">
              <circle cx="50" cy="50" r="42" fill="#4CAF50"/>
              <!-- Cheerful Eyes -->
              <circle cx="36" cy="42" r="5" fill="#1B5E20"/>
              <circle cx="64" cy="42" r="5" fill="#1B5E20"/>
              <circle cx="38" cy="40" r="1.5" fill="white"/>
              <circle cx="66" cy="40" r="1.5" fill="white"/>
              <!-- Rosy Cheeks -->
              <circle cx="28" cy="52" r="4" fill="#A5D6A7" opacity="0.8"/>
              <circle cx="72" cy="52" r="4" fill="#A5D6A7" opacity="0.8"/>
              <!-- Happy Smile -->
              <path d="M 36 54 Q 50 68 64 54" stroke="#1B5E20" stroke-width="4" stroke-linecap="round" fill="none"/>
              <!-- Leaf Crown -->
              <path d="M 50 8 Q 42 0 34 10 Q 45 15 50 8 Z" fill="#81C784"/>
              <path d="M 50 8 Q 58 0 66 10 Q 55 15 50 8 Z" fill="#66BB6A"/>
              <!-- Waving Hand -->
              <path d="M 10 50 Q 2 35 12 25 Q 18 35 12 50 Z" fill="#4CAF50"/>
            </svg>
          </div>
          
          <div class="mt-4 bg-white px-5 py-3 rounded-2xl border-2 border-green-200 shadow-sm max-w-xs">
            <p class="text-lg font-bold text-gray-800">Hello, Eco Hero! 👋</p>
            <p class="text-xs text-gray-600 mt-1">Let’s learn how to recycle together!</p>
          </div>
        </div>

        <!-- Avatar Selection & Start -->
        <div class="space-y-4 pb-4">
          <div class="bg-white/90 p-3.5 rounded-2xl border border-green-100 shadow-sm">
            <p class="text-xs font-bold text-gray-600 mb-2 uppercase tracking-wide">Choose Your Avatar</p>
            <div id="avatar-picker" class="flex justify-center space-x-3">
              <button onclick="app.selectAvatar('🚀', this)" class="avatar-opt text-2xl w-11 h-11 rounded-full border-2 border-transparent bg-green-100 flex items-center justify-center transition-all ring-2 ring-eco-leaf">🚀</button>
              <button onclick="app.selectAvatar('🦊', this)" class="avatar-opt text-2xl w-11 h-11 rounded-full border-2 border-transparent bg-amber-100 flex items-center justify-center transition-all">🦊</button>
              <button onclick="app.selectAvatar('🐼', this)" class="avatar-opt text-2xl w-11 h-11 rounded-full border-2 border-transparent bg-blue-100 flex items-center justify-center transition-all">🐼</button>
              <button onclick="app.selectAvatar('🦄', this)" class="avatar-opt text-2xl w-11 h-11 rounded-full border-2 border-transparent bg-purple-100 flex items-center justify-center transition-all">🦄</button>
            </div>
          </div>

          <button onclick="app.startApp()" class="w-full bg-eco-leaf hover:bg-eco-leaf-dark text-white font-bold text-xl py-4 rounded-2xl shadow-pop transition-transform active:translate-y-1 active:shadow-none flex items-center justify-center space-x-2">
            <span>Let’s Start!</span>
            <span class="text-2xl">➔</span>
          </button>
        </div>
      </section>

      <!-- SCREEN 2: HOME DASHBOARD -->
      <section id="screen-home" class="screen-view hidden flex-1 p-5 space-y-5">
        
        <!-- Eco Buddy Welcome Banner -->
        <div class="bg-gradient-to-r from-green-500 to-emerald-600 rounded-3xl p-4 text-white shadow-md relative overflow-hidden flex items-center justify-between">
          <div class="z-10 max-w-[200px]">
            <span class="bg-white/20 text-xs px-2.5 py-0.5 rounded-full font-semibold">Today's Goal</span>
            <h2 id="home-greeting" class="text-lg font-bold mt-1 leading-snug">Ready to make the Earth smile? 🌍</h2>
            <p class="text-xs text-green-100 mt-1">Scan items to earn points!</p>
          </div>
          <!-- Mascot graphic -->
          <div class="w-20 h-20 bg-white/10 rounded-full flex items-center justify-center backdrop-blur-sm border border-white/20">
            <span class="text-4xl animate-bounce-gentle">🌱</span>
          </div>
        </div>

        <!-- MAIN SCAN ACTION BUTTON -->
        <div class="text-center py-2">
          <button onclick="app.navigateTo('screen-scan')" class="group relative inline-flex items-center justify-center w-full bg-gradient-to-r from-eco-leaf to-emerald-500 hover:from-emerald-600 hover:to-green-700 text-white p-5 rounded-3xl shadow-pop transition-all active:translate-y-1 active:shadow-none">
            <div class="flex items-center space-x-4">
              <div class="w-14 h-14 bg-white/20 rounded-2xl flex items-center justify-center text-3xl group-hover:scale-110 transition-transform">
                📷
              </div>
              <div class="text-left">
                <span class="text-2xl font-extrabold tracking-wide block">Scan Waste</span>
                <span class="text-xs text-green-100 font-medium">Point camera & learn where it goes</span>
              </div>
            </div>
          </button>
        </div>

        <!-- Badge Progress Card -->
        <div class="bg-white p-4 rounded-2xl border border-green-100 shadow-sm space-y-2">
          <div class="flex justify-between items-center">
            <div class="flex items-center space-x-2">
              <span id="next-badge-icon" class="text-xl">🍃</span>
              <div>
                <p class="text-xs text-gray-500 uppercase font-semibold">Next Badge Progress</p>
                <p id="next-badge-title" class="text-sm font-bold text-gray-800">Leaf Badge</p>
              </div>
            </div>
            <span id="badge-points-needed" class="text-xs font-bold text-eco-leaf bg-green-50 px-2.5 py-1 rounded-full">0/50 pts</span>
          </div>
          <!-- Progress bar -->
          <div class="w-full bg-gray-100 rounded-full h-3.5 overflow-hidden p-0.5 border border-gray-200">
            <div id="badge-progress-bar" class="bg-gradient-to-r from-eco-sun to-eco-leaf h-full rounded-full transition-all duration-500" style="width: 0%"></div>
          </div>
        </div>

        <!-- Daily Optional Challenge -->
        <div class="bg-amber-50 border-2 border-amber-200 rounded-2xl p-3.5 flex items-center space-x-3">
          <div class="text-3xl">⭐</div>
          <div class="flex-1">
            <p class="text-xs font-bold text-amber-800 uppercase">Daily Quest (Optional)</p>
            <p class="text-xs text-amber-900 font-medium mt-0.5">Learn 1 new item category today!</p>
          </div>
          <button onclick="app.navigateTo('screen-learn')" class="bg-amber-400 hover:bg-amber-500 text-amber-950 text-xs font-bold px-3 py-1.5 rounded-xl shadow-sm">
            Go
          </button>
        </div>

        <!-- Quick Access Grid -->
        <div class="grid grid-cols-2 gap-3">
          <div onclick="app.navigateTo('screen-collection')" class="bg-white p-3.5 rounded-2xl border border-green-100 shadow-sm hover:border-green-300 transition-all cursor-pointer flex items-center space-x-3">
            <div class="w-10 h-10 bg-blue-100 rounded-xl flex items-center justify-center text-xl">🧸</div>
            <div>
              <p class="text-sm font-bold text-gray-800">Eco Friends</p>
              <p id="unlocked-count-preview" class="text-[11px] text-gray-500">1/5 Unlocked</p>
            </div>
          </div>

          <div onclick="app.navigateTo('screen-learn')" class="bg-white p-3.5 rounded-2xl border border-green-100 shadow-sm hover:border-green-300 transition-all cursor-pointer flex items-center space-x-3">
            <div class="w-10 h-10 bg-amber-100 rounded-xl flex items-center justify-center text-xl">📚</div>
            <div>
              <p class="text-sm font-bold text-gray-800">Learn Segregation</p>
              <p class="text-[11px] text-gray-500">Fun Quizzes</p>
            </div>
          </div>
        </div>

      </section>

      <!-- SCREEN 3: SCAN WASTE (Camera / Upload UI) -->
      <section id="screen-scan" class="screen-view hidden flex-1 flex flex-col p-4 bg-gray-900 text-white relative">
        
        <!-- Camera Viewfinder Box -->
        <div class="relative flex-1 bg-gray-800 rounded-3xl overflow-hidden border-2 border-gray-700 flex flex-col items-center justify-center shadow-inner">
          
          <!-- Mock Live Camera Stream / Upload Preview -->
          <div id="camera-stream-preview" class="absolute inset-0 flex items-center justify-center bg-gray-800">
            <div class="text-center p-6 space-y-2">
              <div class="text-5xl opacity-40">📷</div>
              <p class="text-sm text-gray-400">Point camera at waste item or choose a sample below</p>
            </div>
          </div>

          <!-- Image Preview overlay if uploaded -->
          <img id="scanned-image-render" class="absolute inset-0 w-full h-full object-cover hidden" src="" alt="Scanned item">

          <!-- Viewfinder Frame overlay -->
          <div class="relative z-10 w-64 h-64 border-4 border-dashed border-eco-leaf/80 rounded-3xl flex items-center justify-center pointer-events-none">
            <div id="scan-beam-bar" class="absolute left-2 right-2 h-1 bg-eco-leaf shadow-[0_0_15px_#4CAF50] rounded-full hidden animate-scan-beam"></div>
            <span class="text-xs bg-black/60 text-white px-3 py-1 rounded-full backdrop-blur-sm font-medium">Align item in frame</span>
          </div>

          <!-- Scanning Mascot status floating overlay -->
          <div class="absolute bottom-4 left-4 right-4 bg-black/70 backdrop-blur-md p-3 rounded-2xl border border-white/10 flex items-center space-x-3 z-10">
            <span class="text-2xl">🌱</span>
            <p id="scan-status-text" class="text-xs text-gray-200">Eco Buddy says: <span class="text-eco-sun font-bold">"Let me check that!"</span></p>
          </div>
        </div>

        <!-- Sample Item Selector for Prototype Convenience -->
        <div class="mt-4 bg-gray-800/80 p-3 rounded-2xl border border-gray-700">
          <p class="text-[11px] text-gray-400 font-semibold mb-2 uppercase tracking-wider text-center">Prototype Sample Selector</p>
          <div class="grid grid-cols-6 gap-1.5 text-center">
            <button onclick="app.selectSampleItem('plastic_bottle')" class="bg-gray-700 hover:bg-eco-leaf/30 p-2 rounded-xl text-lg transition-all" title="Plastic Bottle">🍾</button>
            <button onclick="app.selectSampleItem('paper_box')" class="bg-gray-700 hover:bg-eco-leaf/30 p-2 rounded-xl text-lg transition-all" title="Cardboard Box">📦</button>
            <button onclick="app.selectSampleItem('glass_jar')" class="bg-gray-700 hover:bg-eco-leaf/30 p-2 rounded-xl text-lg transition-all" title="Glass Jar">🫙</button>
            <button onclick="app.selectSampleItem('soda_can')" class="bg-gray-700 hover:bg-eco-leaf/30 p-2 rounded-xl text-lg transition-all" title="Metal Can">🥫</button>
            <button onclick="app.selectSampleItem('apple_core')" class="bg-gray-700 hover:bg-eco-leaf/30 p-2 rounded-xl text-lg transition-all" title="Apple Core">🍎</button>
            <button onclick="app.selectSampleItem('uncertain_item')" class="bg-gray-700 hover:bg-amber-500/30 p-2 rounded-xl text-lg transition-all" title="Uncertain Item">❓</button>
          </div>
        </div>

        <!-- Action Controls -->
        <div class="mt-4 flex space-x-3">
          <!-- Photo Upload Button -->
          <label class="flex-1 bg-gray-800 hover:bg-gray-700 text-white font-semibold text-sm py-3.5 rounded-2xl border border-gray-700 flex items-center justify-center space-x-2 cursor-pointer transition-colors">
            <span>🖼️ Upload</span>
            <input type="file" accept="image/*" class="hidden" onchange="app.handleImageUpload(event)">
          </label>

          <!-- Scan Trigger Button -->
          <button id="btn-scan-trigger" onclick="app.performScan()" class="flex-[2] bg-eco-leaf hover:bg-eco-leaf-dark text-white font-bold text-lg py-3.5 rounded-2xl shadow-pop transition-all active:translate-y-1 active:shadow-none flex items-center justify-center space-x-2">
            <span>Scan Now!</span>
            <span>⚡</span>
          </button>
        </div>
      </section>

      <!-- SCREEN 4: SCAN RESULT -->
      <section id="screen-result" class="screen-view hidden flex-1 p-5 space-y-4 bg-eco-bg flex flex-col justify-between">
        
        <div class="space-y-4">
          <!-- Item Category Result Header -->
          <div class="bg-white p-4 rounded-3xl border border-green-100 shadow-sm text-center relative overflow-hidden">
            <div id="result-badge-pill" class="inline-block px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider mb-2 bg-amber-100 text-amber-800">
              Plastic Waste
            </div>
            <div class="w-24 h-24 mx-auto my-2 rounded-2xl bg-green-50 flex items-center justify-center text-6xl shadow-inner-soft">
              <span id="result-item-icon">🍾</span>
            </div>
            <h2 id="result-item-title" class="text-xl font-extrabold text-gray-800">You scanned a Plastic Bottle!</h2>
            <p id="result-item-praise" class="text-xs text-eco-leaf font-bold mt-0.5">Great job, Eco Hero! 🌟</p>
          </div>

          <!-- Recommended Bin Visual -->
          <div id="recommended-bin-card" class="p-4 rounded-3xl text-white shadow-md transition-all flex items-center space-x-4 bg-bin-plastic">
            <div class="w-16 h-16 bg-white/20 rounded-2xl flex items-center justify-center text-3xl font-bold backdrop-blur-sm">
              🗑️
            </div>
            <div class="flex-1">
              <p class="text-xs text-white/80 font-semibold uppercase tracking-wider">Recommended Bin</p>
              <h3 id="result-bin-name" class="text-lg font-extrabold">Yellow Bin (Plastic & Dry)</h3>
              <p id="result-instruction" class="text-xs text-white/95 mt-1 font-medium">Empty and rinse it first!</p>
            </div>
          </div>

          <!-- Environmental Fun Fact -->
          <div class="bg-sky-50 border-2 border-sky-200 p-4 rounded-2xl space-y-1">
            <div class="flex items-center space-x-2 text-sky-800 font-bold text-xs">
              <span>💡 Did You Know?</span>
            </div>
            <p id="result-fun-fact" class="text-xs text-sky-900 leading-relaxed font-medium">
              Recycling 1 plastic bottle saves enough energy to power a light bulb for up to 3 hours!
            </p>
          </div>

          <!-- UNCERTAINTY STATE NOTICE (Shown only if item is ambiguous) -->
          <div id="uncertainty-notice" class="hidden bg-amber-50 border-2 border-amber-300 p-4 rounded-2xl space-y-2 text-amber-900">
            <div class="flex items-center space-x-2 font-bold text-sm text-amber-800">
              <span>🔍 Let's check this item together!</span>
            </div>
            <p class="text-xs leading-relaxed">
              This item might have mixed materials or special recycling rules in your city. Please check this item with an adult before throwing it away!
            </p>
          </div>
        </div>

        <!-- Action Buttons -->
        <div class="space-y-2 pt-2">
          <button id="btn-claim-points" onclick="app.claimPointsAndCelebrate()" class="w-full bg-eco-leaf hover:bg-eco-leaf-dark text-white font-bold text-lg py-3.5 rounded-2xl shadow-pop transition-all active:translate-y-1 active:shadow-none flex items-center justify-center space-x-2">
            <span>Got It! Claim Points</span>
            <span class="text-xl">⭐</span>
          </button>

          <button onclick="app.navigateTo('screen-scan')" class="w-full bg-white hover:bg-gray-50 text-gray-700 font-bold text-sm py-3 rounded-2xl border border-gray-200 transition-colors">
            Scan Another Item
          </button>
        </div>
      </section>

      <!-- SCREEN 5: ECO POINTS REWARD (Celebration Overlay State) -->
      <section id="screen-reward" class="screen-view hidden flex-1 p-6 flex flex-col justify-center items-center text-center bg-gradient-to-b from-amber-100 via-white to-green-100 relative overflow-hidden">
        
        <div class="space-y-6 z-10 max-w-xs">
          <!-- Animated Star Graphic -->
          <div class="relative inline-block">
            <div class="text-7xl animate-bounce-gentle">⭐</div>
            <span class="absolute -top-2 -right-2 bg-eco-leaf text-white font-bold text-xs px-2 py-0.5 rounded-full shadow-md">
              SUCCESS
            </span>
          </div>

          <div class="space-y-2">
            <h2 class="text-4xl font-extrabold text-amber-900 tracking-tight">+10 Eco Points!</h2>
            <p class="text-lg font-bold text-eco-leaf-dark">You helped the planet! 🌍</p>
            <p class="text-xs text-gray-600 font-medium">Eco Buddy is super proud of you!</p>
          </div>

          <!-- Mascot Celebration SVG -->
          <div class="bg-white p-4 rounded-3xl border-2 border-amber-200 shadow-sm flex items-center justify-center space-x-3">
            <span class="text-3xl">👏</span>
            <p class="text-xs text-left text-gray-700 font-semibold">
              Every correct sort keeps our oceans clean and trees green!
            </p>
          </div>

          <!-- Updated Total Points Display -->
          <div class="bg-amber-200/80 px-4 py-2 rounded-2xl border border-amber-300 inline-block">
            <span class="text-xs text-amber-900 font-bold uppercase">Total Balance: </span>
            <span id="reward-screen-total-points" class="text-lg font-extrabold text-amber-950">10 pts</span>
          </div>

          <button onclick="app.finishRewardAndReturn()" class="w-full bg-eco-leaf hover:bg-eco-leaf-dark text-white font-bold text-lg py-3.5 rounded-2xl shadow-pop transition-all active:translate-y-1">
            Keep Going! 🚀
          </button>
        </div>
      </section>

      <!-- SCREEN 6: CHARACTER COLLECTION (My Eco Friends) -->
      <section id="screen-collection" class="screen-view hidden flex-1 p-5 space-y-4">
        
        <div>
          <h2 class="text-2xl font-extrabold text-gray-800">My Eco Friends 🧸</h2>
          <p class="text-xs text-gray-600">Unlock cute waste characters as you earn points!</p>
        </div>

        <!-- Characters Grid -->
        <div id="characters-grid" class="grid grid-cols-2 gap-3.5">
          <!-- Rendered dynamically by JS -->
        </div>

        <!-- Milestone Badges Banner -->
        <div class="bg-white p-4 rounded-2xl border border-green-100 shadow-sm space-y-3">
          <h3 class="text-sm font-bold text-gray-800">Earned Badges</h3>
          <div id="badges-list-container" class="grid grid-cols-4 gap-2 text-center">
            <!-- Badges rendered by JS -->
          </div>
        </div>

      </section>

      <!-- SCREEN 7: LEARN RECYCLING (Interactive Quizzes) -->
      <section id="screen-learn" class="screen-view hidden flex-1 p-5 space-y-4">
        
        <div>
          <h2 class="text-2xl font-extrabold text-gray-800">Learn Recycling 📚</h2>
          <p class="text-xs text-gray-600">Test your knowledge with quick fun quizzes!</p>
        </div>

        <!-- Quiz Container Card -->
        <div class="bg-white p-5 rounded-3xl border border-green-100 shadow-sm space-y-4">
          <div class="flex justify-between items-center text-xs font-semibold text-gray-400">
            <span>Quiz Challenge</span>
            <span id="quiz-step-indicator">1 of 3</span>
          </div>

          <div class="text-center py-2 space-y-2">
            <span id="quiz-icon-display" class="text-5xl inline-block mb-1">🍾</span>
            <h3 id="quiz-question-text" class="text-base font-bold text-gray-800 leading-snug">
              Can a plastic bottle be recycled?
            </h3>
          </div>

          <!-- Quiz Answer Options -->
          <div id="quiz-options-container" class="space-y-2">
            <!-- Rendered by JS -->
          </div>

          <!-- Quiz Feedback Box -->
          <div id="quiz-feedback-box" class="hidden p-3 rounded-2xl text-xs font-bold text-center"></div>
        </div>

        <!-- Category Mini Guide -->
        <div class="space-y-2">
          <p class="text-xs font-bold text-gray-500 uppercase tracking-wider">Quick Recycling Rules</p>
          <div class="space-y-2 text-xs">
            <div class="bg-blue-50 border border-blue-200 p-3 rounded-2xl flex items-center space-x-3">
              <span class="text-2xl">📦</span>
              <div>
                <p class="font-bold text-blue-900">Keep Paper Clean & Dry</p>
                <p class="text-blue-700">Wet or greasy paper can't be recycled into new paper!</p>
              </div>
            </div>
            <div class="bg-amber-50 border border-amber-200 p-3 rounded-2xl flex items-center space-x-3">
              <span class="text-2xl">🍾</span>
              <div>
                <p class="font-bold text-amber-900">Empty Bottled Liquids</p>
                <p class="text-amber-700">Always pour out drinks before putting bottles in bins.</p>
              </div>
            </div>
          </div>
        </div>

      </section>

      <!-- SCREEN 8: PROGRESS AND ACHIEVEMENTS -->
      <section id="screen-achievements" class="screen-view hidden flex-1 p-5 space-y-4">
        
        <div>
          <h2 class="text-2xl font-extrabold text-gray-800">My Eco Progress 🏆</h2>
          <p class="text-xs text-gray-600">See all the wonderful work you've done!</p>
        </div>

        <!-- Stats Overview Cards -->
        <div class="grid grid-cols-2 gap-3">
          <div class="bg-amber-50 border border-amber-200 p-4 rounded-2xl text-center space-y-1">
            <p class="text-2xl">⭐</p>
            <p id="stats-total-points" class="text-2xl font-extrabold text-amber-900">0</p>
            <p class="text-[11px] font-semibold text-amber-700 uppercase">Total Eco Points</p>
          </div>

          <div class="bg-green-50 border border-green-200 p-4 rounded-2xl text-center space-y-1">
            <p class="text-2xl">📷</p>
            <p id="stats-scanned-count" class="text-2xl font-extrabold text-green-900">0</p>
            <p class="text-[11px] font-semibold text-green-700 uppercase">Items Scanned</p>
          </div>
        </div>

        <!-- Detailed Breakdown -->
        <div class="bg-white p-4 rounded-2xl border border-green-100 shadow-sm space-y-3">
          <h3 class="text-sm font-bold text-gray-800">Learned Categories</h3>
          
          <div class="space-y-2 text-xs">
            <div>
              <div class="flex justify-between font-semibold mb-1">
                <span>Plastic Waste</span>
                <span id="stat-cat-plastic">0 items</span>
              </div>
              <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden">
                <div id="stat-bar-plastic" class="bg-amber-500 h-full w-0 transition-all"></div>
              </div>
            </div>

            <div>
              <div class="flex justify-between font-semibold mb-1">
                <span>Paper & Cardboard</span>
                <span id="stat-cat-paper">0 items</span>
              </div>
              <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden">
                <div id="stat-bar-paper" class="bg-blue-500 h-full w-0 transition-all"></div>
              </div>
            </div>

            <div>
              <div class="flex justify-between font-semibold mb-1">
                <span>Glass Container</span>
                <span id="stat-cat-glass">0 items</span>
              </div>
              <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden">
                <div id="stat-bar-glass" class="bg-green-500 h-full w-0 transition-all"></div>
              </div>
            </div>
          </div>
        </div>

        <!-- Healthy Encouragement Footer -->
        <div class="bg-green-100/60 p-4 rounded-2xl text-center border border-green-200">
          <p class="text-xs text-green-800 font-semibold">
            🌟 Great work today! You can come back whenever you want to learn more.
          </p>
        </div>

      </section>

      <!-- SCREEN 9: SETTINGS & PARENT/TEACHER AREA -->
      <section id="screen-settings" class="screen-view hidden flex-1 p-5 space-y-4">
        
        <div>
          <h2 class="text-2xl font-extrabold text-gray-800">Settings ⚙️</h2>
          <p class="text-xs text-gray-600">Preferences & Parent/Teacher Controls</p>
        </div>

        <!-- General App Toggles -->
        <div class="bg-white p-4 rounded-2xl border border-green-100 shadow-sm space-y-3">
          <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider">App Preferences</h3>

          <div class="flex justify-between items-center py-1">
            <span class="text-sm font-semibold text-gray-700">Sound Effects 🔊</span>
            <input type="checkbox" id="setting-sound-toggle" class="w-5 h-5 accent-eco-leaf rounded cursor-pointer" checked onchange="app.toggleSound(this.checked)">
          </div>

          <div class="flex justify-between items-center py-1 border-t border-gray-100">
            <span class="text-sm font-semibold text-gray-700">Language 🌐</span>
            <select class="text-xs font-bold bg-gray-100 px-3 py-1.5 rounded-xl border-none outline-none">
              <option>English (Simple)</option>
              <option disabled>Spanish (Coming soon)</option>
            </select>
          </div>
        </div>

        <!-- Parent & Teacher Gate / Area -->
        <div class="bg-white p-4 rounded-2xl border border-green-100 shadow-sm space-y-3">
          <div class="flex justify-between items-center">
            <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider">Parent & Teacher Area 🔒</h3>
            <span class="text-[10px] bg-gray-100 text-gray-600 px-2 py-0.5 rounded-full font-bold">Kid-Safe</span>
          </div>

          <p class="text-xs text-gray-600">
            EcoScan does not store personal camera images or location data. Camera access is used solely for on-device prototype scanning.
          </p>

          <div class="pt-2">
            <button onclick="app.resetPrototypeData()" class="w-full bg-red-50 hover:bg-red-100 text-red-600 font-bold text-xs py-2.5 rounded-xl border border-red-200 transition-colors">
              Reset Progress & Points Data
            </button>
          </div>
        </div>

        <!-- Technical Integration Specs for Educators / Evaluation -->
        <div class="bg-blue-50 p-4 rounded-2xl border border-blue-200 space-y-1 text-xs text-blue-900">
          <p class="font-bold">🔌 AI & Custom Rule Integration Note</p>
          <p class="leading-relaxed text-[11px] text-blue-800">
            This prototype uses sample local classification data. It is pre-structured to plug into TensorFlow.js or a web classification API endpoint along with custom municipal waste sorting JSON rules.
          </p>
        </div>

      </section>

    </main>

    <!-- BOTTOM NAVIGATION BAR -->
    <nav id="bottom-nav" class="bg-white border-t border-gray-100 px-3 py-2 flex justify-around items-center z-20 hidden">
      <button onclick="app.navigateTo('screen-home')" class="nav-btn flex flex-col items-center text-eco-leaf font-bold" data-target="screen-home">
        <span class="text-2xl">🏠</span>
        <span class="text-[10px] mt-0.5">Home</span>
      </button>

      <button onclick="app.navigateTo('screen-scan')" class="nav-btn flex flex-col items-center text-gray-400 font-semibold hover:text-eco-leaf" data-target="screen-scan">
        <span class="text-2xl">📷</span>
        <span class="text-[10px] mt-0.5">Scan</span>
      </button>

      <button onclick="app.navigateTo('screen-collection')" class="nav-btn flex flex-col items-center text-gray-400 font-semibold hover:text-eco-leaf" data-target="screen-collection">
        <span class="text-2xl">🧸</span>
        <span class="text-[10px] mt-0.5">Friends</span>
      </button>

      <button onclick="app.navigateTo('screen-learn')" class="nav-btn flex flex-col items-center text-gray-400 font-semibold hover:text-eco-leaf" data-target="screen-learn">
        <span class="text-2xl">📚</span>
        <span class="text-[10px] mt-0.5">Learn</span>
      </button>

      <button onclick="app.navigateTo('screen-settings')" class="nav-btn flex flex-col items-center text-gray-400 font-semibold hover:text-eco-leaf" data-target="screen-settings">
        <span class="text-2xl">⚙️</span>
        <span class="text-[10px] mt-0.5">Settings</span>
      </button>
    </nav>

  </div>

  <!-- JavaScript Prototype Engine -->
  <script>
    /**
     * EcoScan Prototype Application Engine
     * Handles state persistence, camera UI, mock AI classification, reward logic, and quizzes.
     */
    const SAMPLE_DATABASE = {
      plastic_bottle: {
        id: 'plastic_bottle',
        title: 'Plastic Bottle',
        category: 'Plastic Waste',
        icon: '🍾',
        praise: 'Awesome scanning!',
        binName: 'Yellow Bin (Plastics)',
        binColorClass: 'bg-amber-500',
        instruction: 'Empty liquids & crush slightly to save space.',
        fact: 'Recycling 1 plastic bottle saves enough energy to run a TV for over 1 hour!',
        isUncertain: false
      },
      paper_box: {
        id: 'paper_box',
        title: 'Cardboard Box',
        category: 'Paper Waste',
        icon: '📦',
        praise: 'Super job!',
        binName: 'Blue Bin (Paper & Cardboard)',
        binColorClass: 'bg-blue-500',
        instruction: 'Flatten the box and keep it clean & dry.',
        fact: 'Recycling paper saves lots of trees and keeps wild animals happy!',
        isUncertain: false
      },
      glass_jar: {
        id: 'glass_jar',
        title: 'Glass Jar',
        category: 'Glass Container',
        icon: '🫙',
        praise: 'Great eye!',
        binName: 'Green Bin (Glass Containers)',
        binColorClass: 'bg-emerald-600',
        instruction: 'Rinse out food remnants safely.',
        fact: 'Glass can be recycled over and over again forever without wearing out!',
        isUncertain: false
      },
      soda_can: {
        id: 'soda_can',
        title: 'Aluminum Can',
        category: 'Metal Waste',
        icon: '🥫',
        praise: 'Metal Magic!',
        binName: 'Purple/Metal Bin',
        binColorClass: 'bg-purple-600',
        instruction: 'Make sure it is empty before sorting.',
        fact: 'Recycled soda cans can become parts of new bicycles!',
        isUncertain: false
      },
      apple_core: {
        id: 'apple_core',
        title: 'Apple Core',
        category: 'Organic Waste',
        icon: '🍎',
        praise: 'Natural choice!',
        binName: 'Brown Bin (Compost / Organic)',
        binColorClass: 'bg-amber-800',
        instruction: 'Put in compost or green organic bin.',
        fact: 'Food scraps make rich soil food called compost to grow fresh vegetables!',
        isUncertain: false
      },
      uncertain_item: {
        id: 'uncertain_item',
        title: 'Mixed Material Item',
        category: 'Uncertain Category',
        icon: '❓',
        praise: 'Good effort!',
        binName: 'Check Local Guidance',
        binColorClass: 'bg-gray-600',
        instruction: 'Ask an adult to help check local recycling rules.',
        fact: 'Some items have mixed plastic and foil that need special recycling treatment.',
        isUncertain: true
      }
    };

    const CHARACTERS = [
      { id: 'plastic_pete', name: 'Plastic Pete', icon: '🍾', requiredPts: 0, hint: 'Default Friend' },
      { id: 'paper_penny', name: 'Paper Penny', icon: '📦', requiredPts: 30, hint: 'Earn 30 Points to unlock' },
      { id: 'glassy', name: 'Glassy', icon: '🫙', requiredPts: 70, hint: 'Earn 70 Points to unlock' },
      { id: 'metal_max', name: 'Metal Max', icon: '🥫', requiredPts: 120, hint: 'Earn 120 Points to unlock' },
      { id: 'organic_ollie', name: 'Organic Ollie', icon: '🍎', requiredPts: 180, hint: 'Earn 180 Points to unlock' }
    ];

    const BADGES = [
      { id: 'leaf', name: 'Leaf Badge', icon: '🍃', requiredPts: 50 },
      { id: 'star', name: 'Recycling Star', icon: '⭐', requiredPts: 100 },
      { id: 'protector', name: 'Planet Protector', icon: '🛡️', requiredPts: 250 },
      { id: 'champion', name: 'Eco Champion', icon: '👑', requiredPts: 500 }
    ];

    const QUIZZES = [
      {
        icon: '🍾',
        question: 'Should you pour out leftover juice before recycling a plastic bottle?',
        options: [
          { text: 'Yes, empty it first! 💧', correct: true },
          { text: 'No, leave the juice inside 🧃', correct: false }
        ],
        explanation: 'Liquids can mess up recycling machines! Always empty bottles first.'
      },
      {
        icon: '📦',
        question: 'Can wet or greasy pizza boxes go in the clean paper bin?',
        options: [
          { text: 'Yes, paper is paper!', correct: false },
          { text: 'No, grease ruins clean paper! 🍕', correct: true }
        ],
        explanation: 'Grease contaminates clean paper. Put greasy spots in organic/trash bins!'
      }
    ];

    class EcoScanApp {
      constructor() {
        this.state = {
          points: 0,
          scannedCount: 0,
          avatar: '🚀',
          soundEnabled: true,
          scannedCategories: {
            plastic_bottle: 0,
            paper_box: 0,
            glass_jar: 0,
            soda_can: 0,
            apple_core: 0
          },
          lastScannedItemId: 'plastic_bottle',
          currentQuizIndex: 0
        };

        this.loadState();
      }

      init() {
        this.updateHeaderAndProgress();
        this.renderCharacters();
        this.renderBadges();
        this.loadQuiz(0);
      }

      // Audio Feedback Generator using Web Audio API (No external sound files needed)
      playSound(type) {
        if (!this.state.soundEnabled) return;
        try {
          const ctx = new (window.AudioContext || window.webkitAudioContext)();
          const osc = ctx.createOscillator();
          const gain = ctx.createGain();
          osc.connect(gain);
          gain.connect(ctx.destination);

          if (type === 'success') {
            osc.frequency.setValueAtTime(300, ctx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(600, ctx.currentTime + 0.15);
            gain.gain.setValueAtTime(0.2, ctx.currentTime);
            gain.gain.linearRampToValueAtTime(0.01, ctx.currentTime + 0.25);
            osc.start();
            osc.stop(ctx.currentTime + 0.25);
          } else if (type === 'click') {
            osc.frequency.setValueAtTime(400, ctx.currentTime);
            gain.gain.setValueAtTime(0.1, ctx.currentTime);
            gain.gain.linearRampToValueAtTime(0.01, ctx.currentTime + 0.08);
            osc.start();
            osc.stop(ctx.currentTime + 0.08);
          }
        } catch (e) {
          // Audio fallback gracefully handled
        }
      }

      // Local Persistence
      loadState() {
        const saved = localStorage.getItem('ecoscan_prototype_state');
        if (saved) {
          try {
            this.state = { ...this.state, ...JSON.parse(saved) };
          } catch(e){}
        }
      }

      saveState() {
        localStorage.setItem('ecoscan_prototype_state', JSON.stringify(this.state));
        this.updateHeaderAndProgress();
      }

      resetPrototypeData() {
        if (confirm("Reset all prototype points and unlock progress?")) {
          localStorage.removeItem('ecoscan_prototype_state');
          this.state = {
            points: 0,
            scannedCount: 0,
            avatar: '🚀',
            soundEnabled: true,
            scannedCategories: { plastic_bottle: 0, paper_box: 0, glass_jar: 0, soda_can: 0, apple_core: 0 },
            lastScannedItemId: 'plastic_bottle',
            currentQuizIndex: 0
          };
          this.saveState();
          this.navigateTo('screen-home');
          alert("Progress reset!");
        }
      }

      // Navigation Core
      navigateTo(screenId) {
        this.playSound('click');
        const screens = document.querySelectorAll('.screen-view');
        screens.forEach(s => {
          s.classList.add('hidden');
          s.classList.remove('active');
        });

        const targetScreen = document.getElementById(screenId);
        if (targetScreen) {
          targetScreen.classList.remove('hidden');
          setTimeout(() => targetScreen.classList.add('active'), 10);
        }

        // Toggle Top Header & Bottom Nav depending on Welcome screen
        const topHeader = document.getElementById('top-header');
        const bottomNav = document.getElementById('bottom-nav');

        if (screenId === 'screen-welcome') {
          topHeader.classList.add('hidden');
          bottomNav.classList.add('hidden');
        } else {
          topHeader.classList.remove('hidden');
          bottomNav.classList.remove('hidden');
        }

        // Highlight Active Bottom Navigation Button
        document.querySelectorAll('.nav-btn').forEach(btn => {
          if (btn.dataset.target === screenId) {
            btn.classList.add('text-eco-leaf');
            btn.classList.remove('text-gray-400');
          } else {
            btn.classList.remove('text-eco-leaf');
            btn.classList.add('text-gray-400');
          }
        });

        // Update view-specific dynamic stats
        if (screenId === 'screen-achievements') this.renderAchievements();
        if (screenId === 'screen-collection') this.renderCharacters();
      }

      selectAvatar(avatarChar, element) {
        this.playSound('click');
        this.state.avatar = avatarChar;
        document.querySelectorAll('.avatar-opt').forEach(el => el.classList.remove('ring-2', 'ring-eco-leaf'));
        element.classList.add('ring-2', 'ring-eco-leaf');
        this.saveState();
      }

      startApp() {
        this.navigateTo('screen-home');
      }

      // Scan Action Simulation
      selectSampleItem(itemId) {
        this.playSound('click');
        this.state.lastScannedItemId = itemId;
        const item = SAMPLE_DATABASE[itemId];
        
        // Update viewfinder indicator text
        document.getElementById('scan-status-text').innerHTML = `Selected: <span class="text-eco-sun font-bold">${item.title}</span>`;
      }

      handleImageUpload(event) {
        const file = event.target.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = (e) => {
            const img = document.getElementById('scanned-image-render');
            img.src = e.target.result;
            img.classList.remove('hidden');
            document.getElementById('scan-status-text').innerHTML = `Eco Buddy says: <span class="text-eco-sun font-bold">"Photo loaded!"</span>`;
          };
          reader.readAsDataURL(file);
        }
      }

      performScan() {
        this.playSound('click');
        const scanBeam = document.getElementById('scan-beam-bar');
        scanBeam.classList.remove('hidden');
        
        const triggerBtn = document.getElementById('btn-scan-trigger');
        triggerBtn.disabled = true;
        triggerBtn.classList.add('opacity-50');

        document.getElementById('scan-status-text').innerHTML = `Eco Buddy says: <span class="text-eco-sun font-bold">"Scanning item..."</span>`;

        // Simulate 1.5s AI Image Processing
        setTimeout(() => {
          scanBeam.classList.add('hidden');
          triggerBtn.disabled = false;
          triggerBtn.classList.remove('opacity-50');
          this.showScanResult(this.state.lastScannedItemId || 'plastic_bottle');
        }, 1400);
      }

      showScanResult(itemId) {
        const item = SAMPLE_DATABASE[itemId] || SAMPLE_DATABASE.plastic_bottle;
        
        document.getElementById('result-item-icon').textContent = item.icon;
        document.getElementById('result-item-title').textContent = `You scanned a ${item.title}!`;
        document.getElementById('result-item-praise').textContent = item.praise;
        
        const binCard = document.getElementById('recommended-bin-card');
        binCard.className = `p-4 rounded-3xl text-white shadow-md flex items-center space-x-4 ${item.binColorClass}`;
        
        document.getElementById('result-bin-name').textContent = item.binName;
        document.getElementById('result-instruction').textContent = item.instruction;
        document.getElementById('result-fun-fact').textContent = item.fact;

        // Toggle Uncertainty box
        const uncertaintyBox = document.getElementById('uncertainty-notice');
        if (item.isUncertain) {
          uncertaintyBox.classList.remove('hidden');
        } else {
          uncertaintyBox.classList.add('hidden');
        }

        this.navigateTo('screen-result');
      }

      claimPointsAndCelebrate() {
        // Prevent duplicate abuse logic: Record scan stats
        const currentItem = this.state.lastScannedItemId;
        if (this.state.scannedCategories[currentItem] !== undefined) {
          this.state.scannedCategories[currentItem]++;
        }
        
        this.state.points += 10;
        this.state.scannedCount++;
        this.saveState();

        // Launch celebratory confetti burst
        try {
          confetti({
            particleCount: 60,
            spread: 70,
            origin: { y: 0.6 }
          });
        } catch(e){}

        this.playSound('success');

        // Update reward screen display
        document.getElementById('reward-screen-total-points').textContent = `${this.state.points} pts`;
        this.navigateTo('screen-reward');
      }

      finishRewardAndReturn() {
        this.navigateTo('screen-home');
      }

      // UI State Helpers
      updateHeaderAndProgress() {
        document.getElementById('user-points-display').textContent = this.state.points;

        // Find Next Badge Goal
        let nextBadge = BADGES[0];
        for (let b of BADGES) {
          if (this.state.points < b.requiredPts) {
            nextBadge = b;
            break;
          }
          nextBadge = b; // highest reached
        }

        document.getElementById('next-badge-title').textContent = nextBadge.name;
        document.getElementById('next-badge-icon').textContent = nextBadge.icon;
        
        const progressPercent = Math.min(100, Math.round((this.state.points / nextBadge.requiredPts) * 100));
        document.getElementById('badge-points-needed').textContent = `${this.state.points}/${nextBadge.requiredPts} pts`;
        document.getElementById('badge-progress-bar').style.width = `${progressPercent}%`;

        // Update Friends Count Preview
        const unlockedCount = CHARACTERS.filter(c => this.state.points >= c.requiredPts).length;
        document.getElementById('unlocked-count-preview').textContent = `${unlockedCount}/${CHARACTERS.length} Unlocked`;
      }

      renderCharacters() {
        const grid = document.getElementById('characters-grid');
        grid.innerHTML = '';

        CHARACTERS.forEach(char => {
          const isUnlocked = this.state.points >= char.requiredPts;
          
          const card = document.createElement('div');
          card.className = `bg-white p-4 rounded-2xl border shadow-sm flex flex-col items-center text-center relative ${isUnlocked ? 'border-green-200' : 'border-gray-200 opacity-70'}`;
          
          card.innerHTML = `
            <div class="w-16 h-16 rounded-2xl ${isUnlocked ? 'bg-green-100' : 'bg-gray-200'} flex items-center justify-center text-4xl mb-2">
              ${isUnlocked ? char.icon : '🔒'}
            </div>
            <h4 class="font-bold text-sm text-gray-800">${char.name}</h4>
            <p class="text-[10px] text-gray-500 mt-0.5">${isUnlocked ? 'Friend Unlocked!' : char.hint}</p>
          `;
          grid.appendChild(card);
        });
      }

      renderBadges() {
        const container = document.getElementById('badges-list-container');
        container.innerHTML = '';

        BADGES.forEach(badge => {
          const isEarned = this.state.points >= badge.requiredPts;
          const div = document.createElement('div');
          div.className = `p-2 rounded-xl border flex flex-col items-center ${isEarned ? 'bg-amber-50 border-amber-300' : 'bg-gray-50 border-gray-200 opacity-50'}`;
          div.innerHTML = `
            <span class="text-2xl">${badge.icon}</span>
            <span class="text-[10px] font-bold mt-1 text-gray-700">${badge.name}</span>
          `;
          container.appendChild(div);
        });
      }

      renderAchievements() {
        document.getElementById('stats-total-points').textContent = this.state.points;
        document.getElementById('stats-scanned-count').textContent = this.state.scannedCount;

        const cats = this.state.scannedCategories;
        document.getElementById('stat-cat-plastic').textContent = `${cats.plastic_bottle || 0} items`;
        document.getElementById('stat-bar-plastic').style.width = `${Math.min(100, (cats.plastic_bottle || 0) * 20)}%`;

        document.getElementById('stat-cat-paper').textContent = `${cats.paper_box || 0} items`;
        document.getElementById('stat-bar-paper').style.width = `${Math.min(100, (cats.paper_box || 0) * 20)}%`;

        document.getElementById('stat-cat-glass').textContent = `${cats.glass_jar || 0} items`;
        document.getElementById('stat-bar-glass').style.width = `${Math.min(100, (cats.glass_jar || 0) * 20)}%`;
      }

      // Quiz System
      loadQuiz(index) {
        this.state.currentQuizIndex = index;
        const quiz = QUIZZES[index] || QUIZZES[0];

        document.getElementById('quiz-step-indicator').textContent = `${index + 1} of ${QUIZZES.length}`;
        document.getElementById('quiz-icon-display').textContent = quiz.icon;
        document.getElementById('quiz-question-text').textContent = quiz.question;

        const feedback = document.getElementById('quiz-feedback-box');
        feedback.classList.add('hidden');

        const optionsContainer = document.getElementById('quiz-options-container');
        optionsContainer.innerHTML = '';

        quiz.options.forEach(opt => {
          const btn = document.createElement('button');
          btn.className = "w-full bg-gray-50 hover:bg-green-50 border-2 border-gray-200 hover:border-eco-leaf text-gray-800 font-bold text-xs py-3 px-4 rounded-xl transition-all text-left flex justify-between items-center";
          btn.innerHTML = `<span>${opt.text}</span>`;
          btn.onclick = () => this.handleQuizAnswer(opt.correct, quiz.explanation);
          optionsContainer.appendChild(btn);
        });
      }

      handleQuizAnswer(isCorrect, explanation) {
        this.playSound('click');
        const feedback = document.getElementById('quiz-feedback-box');
        feedback.classList.remove('hidden');

        if (isCorrect) {
          this.playSound('success');
          feedback.className = "p-3 rounded-2xl text-xs font-bold text-center bg-green-100 text-green-900 border border-green-300";
          feedback.innerHTML = ` Correct! Great learning! 🎉<br><span class="font-normal text-[11px] mt-1 block">${explanation}</span>`;
        } else {
          feedback.className = "p-3 rounded-2xl text-xs font-bold text-center bg-amber-100 text-amber-900 border border-amber-300";
          feedback.innerHTML = ` Not quite. Let's learn together! 💡<br><span class="font-normal text-[11px] mt-1 block">${explanation}</span>`;
        }
      }

      toggleSound(enabled) {
        this.state.soundEnabled = enabled;
        this.saveState();
      }
    }

    // Initialize App Engine when DOM is ready
    let app;
    window.addEventListener('DOMContentLoaded', () => {
      app = new EcoScanApp();
      app.init();
    });
  </script>
</body>
</html>