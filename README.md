# Quiz.Saleem
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تطبيق أبطال المعرفة للأطفال - Kids Smart Quiz & Themes</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts for Kids -->
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@500;700&family=Tajawal:wght@700;900&display=swap" rel="stylesheet">
    <!-- Canvas Confetti for Celebration -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <style>
        body {
            font-family: 'Tajawal', 'Fredoka', sans-serif;
            touch-action: manipulation;
            user-select: none;
            -webkit-user-select: none;
            transition: background 0.5s ease;
        }

        /* Color Themes / Background Palettes */
        .theme-pink { background: linear-gradient(135deg, #FFDEE9 0%, #B5FFFC 100%); }
        .theme-blue { background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%); }
        .theme-green { background: linear-gradient(135deg, #d4fc79 0%, #96e6a1 100%); }
        .theme-yellow { background: linear-gradient(135deg, #ffe53b 0%, #ff8c00 100%); }
        .theme-purple { background: linear-gradient(135deg, #c471ed 0%, #f64f59 100%); }
        .theme-night { background: linear-gradient(135deg, #2b5876 0%, #4e4376 100%); }

        /* English font class */
        .lang-en {
            font-family: 'Fredoka', sans-serif !important;
            direction: ltr !important;
        }

        /* Animations */
        .bounce-gentle {
            animation: bounceGentle 2s infinite ease-in-out;
        }
        @keyframes bounceGentle {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }

        .wiggle {
            animation: wiggle 1.2s infinite ease-in-out;
        }
        @keyframes wiggle {
            0%, 100% { transform: rotate(-4deg); }
            50% { transform: rotate(4deg); }
        }

        .pop-in {
            animation: popIn 0.35s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        @keyframes popIn {
            0% { transform: scale(0.7); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        /* Playful button Press Effect */
        .btn-kid {
            transition: all 0.15s ease-in-out;
            box-shadow: 0 8px 0 rgba(0, 0, 0, 0.12);
        }
        .btn-kid:active {
            transform: translateY(6px);
            box-shadow: 0 2px 0 rgba(0, 0, 0, 0.12);
        }

        /* Glassmorphic Container */
        .glass-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(12px);
            border: 4px solid #FFFFFF;
        }

        /* 3D Memory Card Flip Styles */
        .card-perspective {
            perspective: 1000px;
        }
        .card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            transition: transform 0.4s ease;
            transform-style: preserve-3d;
            cursor: pointer;
        }
        .card-inner.flipped {
            transform: rotateY(180deg);
        }
        .card-front, .card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
            border-radius: 1.25rem;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 6px 0 rgba(0,0,0,0.1);
        }
        .card-front {
            background: linear-gradient(135deg, #a78bfa, #c084fc);
            border: 3px solid #ffffff;
        }
        .card-back {
            background: #ffffff;
            border: 3px solid #e2e8f0;
            transform: rotateY(180deg);
        }
    </style>
</head>
<body id="app-body" class="theme-pink min-h-screen flex items-center justify-center p-3 sm:p-5 overflow-x-hidden">

    <!-- Main Container Card -->
    <div id="main-card" class="w-full max-w-xl glass-card rounded-3xl p-4 sm:p-6 shadow-2xl relative min-h-[620px] flex flex-col justify-between overflow-hidden">
        
        <!-- Top Bar: Themes & Utility Controls -->
        <div>
            <!-- Color Themes Picker Bar -->
            <div class="flex items-center justify-between bg-slate-100/80 p-2 rounded-2xl mb-3 border border-slate-200">
                <span class="text-xs font-black text-slate-700 flex items-center gap-1">
                    <i class="fa-solid fa-palette text-pink-500"></i> أَلْوَانِي:
                </span>
                <div class="flex items-center gap-1.5">
                    <button onclick="setTheme('theme-pink')" title="وردي" class="w-7 h-7 rounded-full bg-gradient-to-tr from-pink-300 to-sky-200 border-2 border-white shadow transition hover:scale-110 active:scale-95"></button>
                    <button onclick="setTheme('theme-blue')" title="أزرق" class="w-7 h-7 rounded-full bg-gradient-to-tr from-blue-300 to-sky-100 border-2 border-white shadow transition hover:scale-110 active:scale-95"></button>
                    <button onclick="setTheme('theme-green')" title="أخضر" class="w-7 h-7 rounded-full bg-gradient-to-tr from-green-300 to-lime-200 border-2 border-white shadow transition hover:scale-110 active:scale-95"></button>
                    <button onclick="setTheme('theme-yellow')" title="أصفر" class="w-7 h-7 rounded-full bg-gradient-to-tr from-amber-300 to-orange-400 border-2 border-white shadow transition hover:scale-110 active:scale-95"></button>
                    <button onclick="setTheme('theme-purple')" title="بنفسجي" class="w-7 h-7 rounded-full bg-gradient-to-tr from-purple-400 to-rose-400 border-2 border-white shadow transition hover:scale-110 active:scale-95"></button>
                    <button onclick="setTheme('theme-night')" title="ليلي" class="w-7 h-7 rounded-full bg-gradient-to-tr from-indigo-700 to-purple-800 border-2 border-white shadow transition hover:scale-110 active:scale-95"></button>
                </div>
            </div>

            <!-- Main Header Controls -->
            <header class="flex justify-between items-center mb-2">
                <div class="flex items-center gap-2">
                    <!-- Sound Toggle -->
                    <button id="btn-sound" onclick="toggleMute()" class="btn-kid bg-amber-400 hover:bg-amber-500 text-white w-11 h-11 rounded-2xl flex items-center justify-center text-lg border-2 border-amber-300">
                        <i id="sound-icon" class="fa-solid fa-volume-high"></i>
                    </button>
                    <!-- Replay Speech -->
                    <button id="btn-replay" onclick="repeatCurrentSpeech()" class="btn-kid bg-sky-400 hover:bg-sky-500 text-white w-11 h-11 rounded-2xl flex items-center justify-center text-lg border-2 border-sky-300">
                        <i class="fa-solid fa-rotate-right"></i>
                    </button>
                    <!-- Home Button -->
                    <button id="btn-home" onclick="showCategoryScreen()" class="btn-kid bg-purple-400 hover:bg-purple-500 text-white w-11 h-11 rounded-2xl flex items-center justify-center text-lg border-2 border-purple-300 hidden">
                        <i class="fa-solid fa-house"></i>
                    </button>
                </div>

                <!-- Score Display -->
                <div class="flex items-center gap-2 bg-yellow-100 border-2 border-yellow-400 px-3.5 py-1.5 rounded-2xl shadow-inner">
                    <i class="fa-solid fa-star text-yellow-500 text-xl drop-shadow"></i>
                    <span id="score-display" class="text-xl font-black text-amber-800">0</span>
                </div>
            </header>
        </div>

        <!-- Dynamic Content Screens -->
        
        <!-- 1. CATEGORY SELECTION SCREEN -->
        <div id="screen-categories" class="flex flex-col items-center justify-between flex-1 pop-in py-2">
            <!-- Mascot Greeting -->
            <div class="text-center my-2">
                <div class="text-6xl sm:text-7xl mb-2 bounce-gentle">🐻🎈</div>
                <h1 class="text-2xl sm:text-3xl font-black text-indigo-900 leading-tight">عَالَمُ الأَبْطَالِ الصِّغَارِ</h1>
                <p class="text-base sm:text-lg text-indigo-600 font-bold mt-1">اخْتَرِ المَادَّةَ أَوْ اللُّعْبَةَ لِلْبَدْءِ 🌟</p>
            </div>

            <!-- Main Subject Buttons & Memory Game -->
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-3 w-full my-auto">
                <!-- Math -->
                <button onclick="selectCategory('math')" class="btn-kid bg-gradient-to-b from-orange-400 to-amber-500 hover:from-orange-500 hover:to-amber-600 text-white p-3.5 rounded-3xl border-4 border-amber-200 flex flex-col items-center justify-center gap-1">
                    <span class="text-3xl sm:text-4xl wiggle">🔢</span>
                    <span class="text-lg font-black">حِسَاب</span>
                    <span class="text-[10px] font-bold opacity-80 lang-en">Math</span>
                </button>

                <!-- Arabic -->
                <button onclick="selectCategory('arabic')" class="btn-kid bg-gradient-to-b from-emerald-400 to-green-600 hover:from-emerald-500 hover:to-green-700 text-white p-3.5 rounded-3xl border-4 border-emerald-200 flex flex-col items-center justify-center gap-1">
                    <span class="text-3xl sm:text-4xl wiggle">🔤</span>
                    <span class="text-lg font-black">عَرَبِي</span>
                    <span class="text-[10px] font-bold opacity-80">الحُرُوف</span>
                </button>

                <!-- English -->
                <button onclick="selectCategory('english')" class="btn-kid bg-gradient-to-b from-sky-400 to-blue-600 hover:from-sky-500 hover:to-blue-700 text-white p-3.5 rounded-3xl border-4 border-sky-200 flex flex-col items-center justify-center gap-1">
                    <span class="text-3xl sm:text-4xl wiggle">🔤</span>
                    <span class="text-lg font-black lang-en">English</span>
                    <span class="text-[10px] font-bold opacity-80">إِنْجِلِيزِي</span>
                </button>

                <!-- Deen -->
                <button onclick="selectCategory('deen')" class="btn-kid bg-gradient-to-b from-purple-400 to-indigo-600 hover:from-purple-500 hover:to-indigo-700 text-white p-3.5 rounded-3xl border-4 border-purple-200 flex flex-col items-center justify-center gap-1">
                    <span class="text-3xl sm:text-4xl wiggle">🕌</span>
                    <span class="text-lg font-black">دِين إِسْلَامِي</span>
                    <span class="text-[10px] font-bold opacity-80">أَخْلَاق</span>
                </button>

                <!-- Memory Game Button -->
                <button onclick="startMemoryGame()" class="btn-kid col-span-2 sm:col-span-2 bg-gradient-to-b from-pink-400 to-rose-600 hover:from-pink-500 hover:to-rose-700 text-white p-3.5 rounded-3xl border-4 border-pink-200 flex flex-row sm:flex-col items-center justify-center gap-3 sm:gap-1">
                    <span class="text-4xl wiggle">🧠✨</span>
                    <div class="flex flex-col items-start sm:items-center">
                        <span class="text-xl font-black">لُعْبَةُ الذَّاكِرَةِ</span>
                        <span class="text-xs font-bold opacity-85">تَطْبِيقُ الصُّوَرِ المِثَالِيَّة</span>
                    </div>
                </button>
            </div>

            <div class="mt-3 text-xs font-bold text-indigo-600 bg-indigo-50 px-4 py-1.5 rounded-full border border-indigo-100">
                أَسْئِلَةٌ مُتَجَدِّدَةٌ خَفِيفَةٌ بِدُونِ وَقْتٍ مَحْدُودٍ 🎈
            </div>
        </div>

        <!-- 2. QUIZ QUESTION SCREEN (Endless Mode) -->
        <div id="screen-quiz" class="hidden flex-col justify-between flex-1 pop-in py-1">
            <!-- Question Header Box -->
            <div class="text-center my-auto">
                <div id="q-emoji" class="text-6xl sm:text-7xl mb-3 bounce-gentle">❓</div>
                <h2 id="q-title" class="text-2xl sm:text-3xl font-black text-slate-800 leading-snug px-2">
                    جَارٍ التَّحْمِيل...
                </h2>
            </div>

            <!-- Answer Options Container -->
            <div id="options-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-3.5 mb-2 my-auto">
                <!-- Dynamic Buttons -->
            </div>

            <!-- Counter / Info -->
            <div class="text-center mt-2">
                <span id="q-counter" class="text-xs sm:text-sm font-bold text-indigo-600 bg-indigo-50 px-4 py-1.5 rounded-full border border-indigo-100">
                    🔄 أَسْئِلَةٌ مُتَجَدِّدَةٌ بِلاَ نِهَايَة
                </span>
            </div>
        </div>

        <!-- 3. MEMORY GAME SCREEN -->
        <div id="screen-memory" class="hidden flex-col justify-between flex-1 pop-in py-1">
            <div class="text-center mb-2">
                <h2 class="text-xl sm:text-2xl font-black text-indigo-900">🧠 لُعْبَةُ الذَّاكِرَةِ العَجِيبَةِ</h2>
                <p class="text-xs sm:text-sm font-bold text-indigo-600">اِكْشِفْ الْبِطَاقَاتِ وَابْحَثْ عَنِ الصُّوَرِ المُمَاثِلَةِ 🎈</p>
            </div>

            <!-- Cards Grid -->
            <div id="memory-grid" class="grid grid-cols-3 sm:grid-cols-4 gap-2.5 my-auto max-w-md mx-auto w-full">
                <!-- Dynamic Cards -->
            </div>

            <div class="flex justify-between items-center mt-2 px-2">
                <span id="memory-status" class="text-sm font-black text-purple-700 bg-purple-50 px-3 py-1 rounded-xl border border-purple-200">
                    المُطَابَقَات: 0 / 6
                </span>
                <button onclick="startMemoryGame()" class="btn-kid bg-emerald-500 hover:bg-emerald-600 text-white font-black text-xs px-3 py-2 rounded-xl border border-emerald-300">
                    🔄 إِعَادَةُ اللَّعِب
                </button>
            </div>
        </div>

    </div>

    <script>
        /* ==========================================================================
           1. QUESTION BANK
           ========================================================================== */
        const quizData = {
            math: [
                { emoji: "🍎🍎 + 🍎", question: "كَمْ عَدَدُ التُّفَّاحَاتِ الإِجْمَالِي؟ (2 + 1)", lang: "ar", options: [{ text: "3 تُفَّاحَات", icon: "3️⃣", isCorrect: true }, { text: "5 تُفَّاحَات", icon: "5️⃣", isCorrect: false }, { text: "2 تُفَّاحَتَان", icon: "2️⃣", isCorrect: false }] },
                { emoji: "🎈🎈🎈🎈", question: "كَمْ عَدَدُ البَالُونَاتِ فِي الصُّورَةِ؟", lang: "ar", options: [{ text: "2", icon: "2️⃣", isCorrect: false }, { text: "4", icon: "4️⃣", isCorrect: true }, { text: "6", icon: "6️⃣", isCorrect: false }] },
                { emoji: "🖐️", question: "كَمْ عَدَدُ الأَصَابِعِ فِي اليَدِ الوَاحِدَةِ؟", lang: "ar", options: [{ text: "5 أصابع", icon: "🖐️", isCorrect: true }, { text: "3 أصابع", icon: "🤟", isCorrect: false }, { text: "10 أصابع", icon: "👐", isCorrect: false }] },
                { emoji: "🦆🦆🦆 - 🦆", question: "لَدَيْنَا 3 بَطَّاتٍ، ذَهَبَتْ وَاحِدَةٌ، كَمْ بَقِيَ؟ (3 - 1)", lang: "ar", options: [{ text: "1", icon: "1️⃣", isCorrect: false }, { text: "2", icon: "2️⃣", isCorrect: true }, { text: "0", icon: "0️⃣", isCorrect: false }] },
                { emoji: "🔺", question: "كَمْ عَدَدُ أَضْلَاعِ المُثَلَّثِ؟", lang: "ar", options: [{ text: "3 أَضْلَاع", icon: "🔺", isCorrect: true }, { text: "4 أَضْلَاع", icon: "⏹️", isCorrect: false }, { text: "1 ضِلْع", icon: "🔴", isCorrect: false }] },
                { emoji: "🌟🌟🌟🌟🌟", question: "كَمْ عَدَدُ النُّجُومِ الَتي تَرَاهَا؟", lang: "ar", options: [{ text: "4 نُجُوم", icon: "4️⃣", isCorrect: false }, { text: "5 نُجُوم", icon: "5️⃣", isCorrect: true }, { text: "6 نُجُوم", icon: "6️⃣", isCorrect: false }] },
                { emoji: "🐱 + 🐱", question: "قِطَّةٌ وَاحِدَةٌ زَادَتْ عَلَيْهَا قِطَّةٌ، كَمْ الصَّحِيحُ؟ (1 + 1)", lang: "ar", options: [{ text: "2 قِطَّتَان", icon: "2️⃣", isCorrect: true }, { text: "3 قِطَط", icon: "3️⃣", isCorrect: false }, { text: "4 قِطَط", icon: "4️⃣", isCorrect: false }] },
                { emoji: "⏹️", question: "كَمْ عَدَدُ أَضْلَاعِ المُرَبَّعِ؟", lang: "ar", options: [{ text: "2 ضِلْعَان", icon: "2️⃣", isCorrect: false }, { text: "4 أَضْلَاع", icon: "4️⃣", isCorrect: true }, { text: "5 أَضْلَاع", icon: "5️⃣", isCorrect: false }] },
                { emoji: "🍪🍪🍪🍪", question: "كَمْ عَدَدُ الكَعْكَاتِ فِي الصُّورَةِ؟", lang: "ar", options: [{ text: "4 كَعْكَات", icon: "4️⃣", isCorrect: true }, { text: "3 كَعْكَات", icon: "3️⃣", isCorrect: false }, { text: "6 كَعْكَات", icon: "6️⃣", isCorrect: false }] },
                { emoji: "🐟🐟 + 🐟🐟", question: "2 سَمَكَتَانِ زَادَتْ 2 سَمَكَتَانِ، كَمْ المَجْمُوعُ؟ (2 + 2)", lang: "ar", options: [{ text: "3", icon: "3️⃣", isCorrect: false }, { text: "4 أَسْمَاك", icon: "4️⃣", isCorrect: true }, { text: "5", icon: "5️⃣", isCorrect: false }] }
            ],
            arabic: [
                { emoji: "🦁", question: "مَا هُوَ الحَرْفُ الأَوَّلُ مِنْ كَلِمَةِ (أَسَد)؟", lang: "ar", options: [{ text: "حَرْفُ ( أ )", icon: "🅰️", isCorrect: true }, { text: "حَرْفُ ( ب )", icon: "🅱️", isCorrect: false }, { text: "حَرْفُ ( ت )", icon: "🔤", isCorrect: false }] },
                { emoji: "🦆", question: "أَيُّ كَلِمَةٍ تَبْدَأُ بِحَرْفِ البَاءِ ( ب )؟", lang: "ar", options: [{ text: "بَطَّة", icon: "🦆", isCorrect: true }, { text: "تُفَّاحَة", icon: "🍎", isCorrect: false }, { text: "جَمَل", icon: "🐪", isCorrect: false }] },
                { emoji: "☀️", question: "مَا هُوَ الحَرْفُ الأَخِيرُ فِي كَلِمَةِ (شَمْس)؟", lang: "ar", options: [{ text: "حَرْفُ ( س )", icon: "☀️", isCorrect: true }, { text: "حَرْفُ ( م )", icon: "🌙", isCorrect: false }, { text: "حَرْفُ ( ر )", icon: "⭐", isCorrect: false }] },
                { emoji: "🍌", question: "مَا هِيَ الكَلِمَةُ الصَّحِيحَةُ لِهَذِهِ الفَاكِهَةِ؟", lang: "ar", options: [{ text: "مَوْز", icon: "🍌", isCorrect: true }, { text: "عِنَب", icon: "🍇", isCorrect: false }, { text: "تِين", icon: "🫐", isCorrect: false }] },
                { emoji: "📖", question: "حَرْفُ (ك) نَجِدُهُ فِي كَلِمَةِ:", lang: "ar", options: [{ text: "كِتَاب", icon: "📖", isCorrect: true }, { text: "قَلَم", icon: "✏️", isCorrect: false }, { text: "شَجَرَة", icon: "🌳", isCorrect: false }] },
                { emoji: "🐪", question: "مَا هُوَ الحَرْفُ الأَوَّلُ مِنْ كَلِمَةِ (جَمَل)؟", lang: "ar", options: [{ text: "حَرْفُ ( ج )", icon: "🐪", isCorrect: true }, { text: "حَرْفُ ( ح )", icon: "🐎", isCorrect: false }, { text: "حَرْفُ ( خ )", icon: "🐑", isCorrect: false }] },
                { emoji: "🐘", question: "كَلِمَةُ (فِيل) تَبْدَأُ بِحَرْفِ:", lang: "ar", options: [{ text: "حَرْفُ ( ف )", icon: "🐘", isCorrect: true }, { text: "حَرْفُ ( ق )", icon: "🐒", isCorrect: false }, { text: "حَرْفُ ( ك )", icon: "🐕", isCorrect: false }] },
                { emoji: "🍎", question: "أَيُّ الصُّوَرِ تُمَثِّلُ كَلِمَةَ (تُفَّاحَة)؟", lang: "ar", options: [{ text: "تُفَّاحَة", icon: "🍎", isCorrect: true }, { text: "برتُقَالَة", icon: "🍊", isCorrect: false }, { text: "مَوْزَة", icon: "🍌", isCorrect: false }] },
                { emoji: "🌙", question: "حَرْفُ (ق) نَجِدُهُ فِي أَّوَلِ كَلِمَةِ:", lang: "ar", options: [{ text: "قَمَر", icon: "🌙", isCorrect: true }, { text: "شَمْس", icon: "☀️", isCorrect: false }, { text: "نَجْمَة", icon: "⭐", isCorrect: false }] },
                { emoji: "🦋", question: "مَا هُوَ الحَرْفُ الأَوَّلُ مِنْ كَلِمَةِ (فَرَاشَة)؟", lang: "ar", options: [{ text: "حَ
