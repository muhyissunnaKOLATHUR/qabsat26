<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QABSAT | RAMADAN COMPANION</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Amiri:wght@400;700&display=swap" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    
    <style>
        :root {
            --bg: #f8fafc; --card: #ffffff; --accent: #10b981; --accent-dark: #064e3b;
            --text: #0f172a; --sub-text: #64748b; --border: #e2e8f0; --radius: 20px;
        }
        [data-theme='dark'] {
            --bg: #020617; --card: #0f172a; --text: #f8fafc; --sub-text: #94a3b8; --border: #1e293b;
        }
        * { box-sizing: border-box; transition: 0.3s ease; font-family: 'Plus Jakarta Sans', sans-serif; }
        body { background: var(--bg); color: var(--text); margin: 0; padding-bottom: 70px; overflow-x: hidden; }

        #greeting-overlay { position: fixed; inset: 0; background: var(--accent-dark); z-index: 3000; display: flex; flex-direction: column; align-items: center; justify-content: center; color: white; text-align: center; cursor: pointer; }
        .ramadan-kareem { font-family: 'Amiri', serif; font-size: 3.5rem; margin-bottom: 10px; animation: glow 2s infinite alternate; }
        @keyframes glow { from { text-shadow: 0 0 10px #fff; } to { text-shadow: 0 0 20px var(--accent), 0 0 30px var(--accent); } }

        .moon-container { display: flex; justify-content: space-around; background: rgba(0,0,0,0.05); padding: 15px; border-radius: 15px; margin: 10px 0; font-size: 1.5rem; }
        .moon-phase { opacity: 0.3; }
        .moon-phase.active { opacity: 1; color: var(--accent); transform: scale(1.3); }

        .drawer { position: fixed; top: 0; left: -280px; width: 280px; height: 100%; background: var(--card); z-index: 2000; transition: 0.4s; box-shadow: 5px 0 15px rgba(0,0,0,0.1); padding: 20px; }
        .drawer.open { left: 0; }
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.5); display: none; z-index: 1999; }
        .drawer-item { padding: 15px; border-radius: 12px; margin-bottom: 8px; cursor: pointer; display: flex; align-items: center; gap: 15px; font-weight: 600; }
        .drawer-item:hover { background: var(--bg); color: var(--accent); }

        header { padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; background: var(--card); border-bottom: 1px solid var(--border); position: sticky; top: 0; z-index: 900; }
        .date-container { text-align: center; }
        #eng-date-display { font-size: 0.65rem; color: var(--sub-text); font-weight: 600; text-transform: uppercase; }
        #hijri-display { font-family: 'Amiri', serif; font-size: 1.1rem; color: var(--accent); font-weight: 700; margin-top: -2px; }

        .container { max-width: 600px; margin: 0 auto; padding: 20px; min-height: 80vh; }
        .section { display: none; }
        .section.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .card { background: var(--card); padding: 20px; border-radius: var(--radius); border: 1px solid var(--border); margin-bottom: 20px; }
        .hero { background: linear-gradient(135deg, var(--accent-dark), var(--accent)); color: white; border: none; text-align: center; }
        
        .arabic-text { font-family: 'Amiri', serif; text-align: right; line-height: 2; font-size: 1.4rem; direction: rtl; padding: 15px; background: var(--bg); border-radius: 12px; margin: 10px 0; border-right: 4px solid var(--accent); color: var(--text); }
        .dhikr-label { font-weight: 800; color: var(--accent); font-size: 0.85rem; text-transform: uppercase; margin-top: 25px; display: block; border-left: 3px solid var(--accent); padding-left: 10px; }
        
        .check-item { display: flex; align-items: center; gap: 12px; padding: 10px 0; border-bottom: 1px solid var(--border); cursor: pointer; }
        .check-item:last-child { border-bottom: none; }
        .check-box { width: 22px; height: 22px; border-radius: 6px; border: 2px solid var(--accent); display: flex; align-items: center; justify-content: center; font-size: 0.8rem; }
        .check-item.done .check-box { background: var(--accent); color: white; }
        .check-item.done span { text-decoration: line-through; opacity: 0.6; }

        .dhikr-counter-card { background: var(--bg); padding: 15px; border-radius: 15px; margin-bottom: 10px; border: 1px solid var(--border); }
        .btn-sq { width: 45px; height: 45px; border-radius: 12px; border: 1px solid var(--border); background: var(--card); cursor: pointer; display: flex; align-items: center; justify-content: center; color: var(--text); }
        .btn-plus { flex-grow: 1; background: var(--accent); color: white; font-weight: 800; border: none; margin: 0 10px; font-size: 1.1rem; }
        
        .names-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; direction: rtl; }
        .name-box { background: var(--bg); padding: 10px; border-radius: 10px; text-align: center; font-family: 'Amiri', serif; font-size: 1.1rem; border: 1px solid var(--border); }

        input, select, textarea { width: 100%; padding: 12px; border-radius: 12px; border: 1px solid var(--border); background: var(--bg); color: var(--text); margin-bottom: 10px; font-size: 0.9rem; outline: none; }
        
        .nav-bar { position: fixed; bottom: 0; left: 0; right: 0; background: var(--card); display: flex; justify-content: space-around; padding: 12px; border-top: 1px solid var(--border); z-index: 1000; }
        .nav-item { color: var(--sub-text); cursor: pointer; text-align: center; font-size: 0.7rem; font-weight: 600; }
        .nav-item.active { color: var(--accent); }
        .nav-item i { display: block; font-size: 1.3rem; margin-bottom: 3px; }

        .ashra-badge { background: var(--accent); color: white; padding: 4px 12px; border-radius: 50px; font-size: 0.7rem; font-weight: 800; margin-bottom: 10px; display: inline-block; }
        
        footer { text-align: center; padding: 20px; color: var(--sub-text); font-size: 0.75rem; border-top: 1px solid var(--border); margin-top: 20px; line-height: 1.6; }
    </style>
</head>
<body data-theme="light">

    <div id="greeting-overlay" onclick="closeGreeting()">
        <div class="ramadan-kareem">رمضان مبارك</div>
        <p style="font-weight: 300; letter-spacing: 4px; font-size: 0.8rem;">RAMADAN MUBARAK</p>
        <p style="font-size: 0.6rem; margin-top: 30px; opacity: 0.6; text-transform: uppercase;">Tap to continue</p>
    </div>

    <div class="overlay" id="overlay" onclick="toggleDrawer()"></div>
    <div class="drawer" id="drawer">
        <h2 style="color:var(--accent)">Menu</h2>
        <div class="drawer-item" onclick="showSection('home'); toggleDrawer()"><i class="fas fa-home"></i> Home</div>
        <div class="drawer-item" onclick="showSection('prayer'); toggleDrawer()"><i class="fas fa-clock"></i> Prayer Times</div>
        <div class="drawer-item" onclick="showSection('adhkar'); toggleDrawer()"><i class="fas fa-book-open"></i> Adhkar & Quran</div>
        <div class="drawer-item" onclick="showSection('settings'); toggleDrawer()"><i class="fas fa-pen"></i> Journal & Settings</div>
        <hr style="border:0; border-top:1px solid var(--border); margin: 20px 0;">
        <div class="drawer-item" onclick="toggleTheme()"><i class="fas fa-moon"></i> Toggle Dark Mode</div>
        <div class="drawer-item" onclick="exportToPDF()" style="color: var(--accent);"><i class="fas fa-file-pdf"></i> Export 30 Day PDF</div>
    </div>

    <header>
        <div onclick="toggleDrawer()" style="cursor:pointer; font-size: 1.2rem;"><i class="fas fa-bars"></i></div>
        <div class="date-container">
            <div id="eng-date-display">February 18, 2026</div>
            <div id="hijri-display">30 Sha'ban 1447</div>
        </div>
        <div style="width: 24px;"></div>
    </header>

    <div class="container">
        <div id="home" class="section active">
            <div class="card hero">
                <p style="font-size: 0.7rem; font-weight: 800; opacity: 0.9; margin: 0;" id="timer-label">TIME UNTIL MAGHRIB</p>
                <div id="timer" style="font-size: 3.5rem; font-weight:800; margin: 5px 0;">00:00:00</div>
                <div id="loc-status" style="font-size: 0.7rem;">Detecting...</div>
            </div>

            <div class="card" id="ashra-card">
                <div class="ashra-badge" id="ashra-title">First Ashra (Mercy)</div>
                <h3 style="margin-top:0;">Dua of the Ashra</h3>
                <div class="arabic-text" id="ashra-dua-text">اللَّهُمَّ ارْحَمْنِي يَا أَرْحَمَ الرَّاحِمِينَ</div>
            </div>

            <div class="card">
                <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
                    <h3 style="margin:0;"><i class="fas fa-book-open"></i> Juz' Tracker</h3>
                    <span id="khatm-goal-display" style="font-size:0.7rem; color:var(--accent); font-weight:800;">GOAL: 1 KHATM</span>
                </div>
                <div style="display:flex; align-items:center; gap:15px; background:var(--bg); padding:15px; border-radius:15px;">
                    <button class="btn-sq" onclick="adjustJuz(-1)">-</button>
                    <div style="flex-grow:1; text-align:center;">
                        <span style="font-size:0.7rem; display:block; color:var(--sub-text);">Current Progress</span>
                        <b style="font-size:1.5rem;">Juz' <span id="current-juz-val">0</span></b>
                    </div>
                    <button class="btn-sq" onclick="adjustJuz(1)">+</button>
                </div>
            </div>

            <div class="card">
                <h3><i class="fas fa-check-double"></i> Sunnah Prayers</h3>
                <div id="sunnah-prayers-list">
                    <div class="check-item" onclick="toggleCheck(this, 's_tharaweeh')"><div class="check-box"></div><span>Tharaweeh</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 's_vitr')"><div class="check-box"></div><span>Vitr</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 's_thahajudh')"><div class="check-box"></div><span>Thahajudh</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 's_luha')"><div class="check-box"></div><span>Luha (Duha)</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 's_fast')"><div class="check-box"></div><span>Fasting Kept</span></div>
                </div>
            </div>

            <div class="card" style="background: #fff9db; border-color: #f59f00; color: #856404;">
                <h3 style="margin-top:0; color:#856404;"><i class="fas fa-lightbulb"></i> Sunnah of the Day</h3>
                <p id="sunnah-desc" style="font-size: 0.9rem; margin:0;">Using Miswak regularly today.</p>
            </div>

            <div class="card">
                <h3><i class="fas fa-bell"></i> Good Deeds</h3>
                <div style="display:grid; grid-template-columns: repeat(2, 1fr); gap:10px;">
                    <div class="check-item" onclick="toggleCheck(this, 'r_sadaqah')"><div class="check-box"></div><span>Give Sadaqah</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 'r_sick')"><div class="check-box"></div><span>Visit Sick</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 'r_dua')"><div class="check-box"></div><span>Special Dua</span></div>
                    <div class="check-item" onclick="toggleCheck(this, 'r_parents')"><div class="check-box"></div><span>Help Parents</span></div>
                </div>
            </div>

            <div class="card">
                <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
                    <h3 style="margin:0;"><i class="fas fa-fingerprint"></i> Dhikr Counter</h3>
                    <span style="font-size:0.7rem; color:var(--accent); font-weight:800; cursor:pointer;" onclick="showSection('settings')">MANAGE</span>
                </div>
                <div id="dhikr-list-home"></div>
            </div>
        </div>

        <div id="prayer" class="section">
            <div class="card">
                <h3><i class="fas fa-map-marker-alt"></i> Location</h3>
                <select id="location-mode" onchange="updateLocationMode()">
                    <option value="auto">Use Current Location (GPS)</option>
                    <option value="malappuram" selected>Malappuram (Kerala)</option>
                    <option value="kozhikode">Kozhikode</option>
                    <option value="kannur">Kannur</option>
                    <option value="dubai">Dubai, UAE</option>
                </select>
            </div>
            <div class="card">
                <h3><i class="fas fa-mosque"></i> Prayer Timings</h3>
                <div id="prayer-display" style="line-height: 2.8;"></div>
            </div>
        </div>

        <div id="adhkar" class="section">
            <div class="card">
                <h3><i class="fas fa-moon"></i> Ramadan Moon Journey</h3>
                <div class="moon-container">
                    <div class="moon-phase" title="New Moon">🌑</div>
                    <div class="moon-phase active" title="Crescent">🌙</div>
                    <div class="moon-phase" title="Half Moon">🌓</div>
                    <div class="moon-phase" title="Full Moon">🌕</div>
                </div>
            </div>

            <div class="card">
                <h3><i class="fas fa-book-quran"></i> Holy Quran</h3>
                <select id="surah-select" onchange="loadQuranSurah()">
                    <option value="">Select a Surah...</option>
                </select>
                <div id="surah-loading" style="display:none; text-align:center; padding:10px; color:var(--accent); font-weight:bold;">Loading...</div>
                <audio id="quran-audio" controls style="width:100%; margin: 15px 0;"></audio>
                <div id="surah-text" class="arabic-text" style="max-height:400px; overflow-y:auto; line-height: 2.5;"></div>
            </div>

            <div class="card">
                <h3><i class="fas fa-star-and-crescent"></i> Organized Adhkar</h3>
                
                <h4 class="dhikr-label">1. Daily Adhkar (Morning)</h4>
                <div class="arabic-text">أَصْبَحْنَا وَأَصْبَحَ الْمُلْكُ لِلهِ وَالْحَمْدُ لِلهِ رَبِّ الْعَالَمِينَ. لَا إِلَهَ إِلَّا اللهُ وَحْدَهُ لَا شَرِيكَ لَهُ ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرُ. رَبِّ إِنِّي أَسْأَلُكَ خَيْرَ ما في هذا الْيَوْمِ وَخَيْرَ مَا بَعْدَهُ. وَأَعُوذُ بِكَ مِنْ شَرِّ هَذَا الْيَوْمِ وَشَرِّمَا بَعْدَهُ. رَبِّ أَعُوذُ بِكَ مِنَ الْكَسَلِ وَسُوءِ الْكِبَرِ. رَبِّ أَعُوذُ بِكَ مِنْ عَذَابٍ فِي النَّارِ وَعَذَابِ فِي الْقَبْرِ اللَّهُمَّ بِكَ أَصْبَحْنَا وَبِكَ أَمْسَيْنَا وَبِكَ نَحْيَا وَبِكَ نَمُوتُ وَإِلَيْكَ النُّشُورُ.</div>

                <h4 class="dhikr-label">1. Daily Adhkar (Evening)</h4>
                <div class="arabic-text">أَمْسَيْنَا وَأَمْسَى الْمُلْكُ لِلهِ وَالْحَمْدُ لِلهِ رَبِّ الْعَالَمِينَ. لَا إِلَهَ إِلَّا اللهُ وَحْدَهُ لَا شَرِيكَ لَهُ ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ. رَبِّ إِنِّي أَسْأَلُكَ خَيْرَ مَا فِي هَذِهِ اللَّيْلَةِ وَخَيْرَ مَا بَعْدَهَا. وَأَعُوذُ بِكَ مِنْ شَرِّ هَذِهِ اللَّيْلَةِ وَشَرِّمَا بَعْدَهَا. رَبِّ أَعُوذُ بِكَ مِنَ الْكَسَلِ وَسُوءِ الْكِبَرِ. رَبِّ أَعُوذُ بِكَ مِنْ عَذَابٍ فِي النَّارِ وَعَذَابٍ فِي الْقَبْرِ. اَللَّهُمَّ بِكَ أَمْسَيْنَا وَبِكَ أَصْبَحْنَا وَبِكَ نَحْيَا وَبِكَ نَمُوتُ وَإِلَيْكَ الْمَصِيرُ.</div>

                <h4 class="dhikr-label">2. Special Prayers & Intentions</h4>
                <p style="font-size:0.8rem; font-weight:bold;">Sayyidul Istighfar</p>
                <div class="arabic-text">اللَّهُمَّ أَنْتَ رَبِّي لَا إِلَهَ إِلَّا أَنْتَ خَلقتَنِي وَأَنَا عَبْدُكَ وَأَنَا عَلَى عَهْدِكَ وَوَعْدِكَ مَا اسْتَطَعْتُ. أَعُوذُ بِكَ مِنْ شَرِّ مَا صَنَعْتُ. أَبُوءُ لَكَ بِنِعْمَتِكَ عَلَيَّ وَأَبُوءُ بِذَنْبِي فَاغْفِرْ لِي فَإِنَّهُ لَا يَغْفِرُ الذُّنُوبَ إِلا أَنْتَ.</div>
                
                <p style="font-size:0.8rem; font-weight:bold;">Niyyah (Intention)</p>
                <div class="arabic-text">نَوَيْتُ صَوْمَ غَدٍ عَنْ أَدَاءِ فَرْضِ رَمَضَانِ هَذِهِ السَّنَةِ لِلَّهِ تَعَالَى.</div>

                <p style="font-size:0.8rem; font-weight:bold;">Iftar Dua</p>
                <div class="arabic-text">اللَّهُمَّ لَكَ صُمْتُ وَعَلَى رِزْقِكَ أَفْطَرْتُ ، ذَهَبَ الظَّمَأُ وَابْتَلَّتِ الْعُرُوقُ وَثَبَتَ الْأَجْرُ إِنْ شَاءَ الله.</div>

                <h4 class="dhikr-label">3. Ramadan Specific Adhkar</h4>
                <p style="font-size:0.8rem; font-weight:bold;">Full Time Adhkar</p>
                <div class="arabic-text">أَشْهَدُ أَنْ لَا إِلَهَ إِلَّا اللَّهُ أَسْتَغْفِرُ اللهَ وَأَسْأَلُكَ الْجَنَّةَ وَأَعُوذُ بِكَ مِنَ النَّارِ.</div>
                
                <p style="font-size:0.8rem; font-weight:bold;">Ramadan General Dua</p>
                <div class="arabic-text">اللَّهُمَّ اجْعَلْ هَذَا الشَّهْرَ الشَّرِيفَ الْعَظِيمَ شَاهِدًا لَنَا لَا شَاهِدًا عَلَيْنَا وَاجْعَلْهُ حُجَّةً لَنَا لَا حُجَّةً عَلَيْنَا اللَّهُمَّ أَعْتِقْ رِقَابَنَا وَرِقَابَ آبَائِنَا وَأُمَّهَاتِنَا وَمَنْ تَعَلَّقُوا بِنَا مِنَ الدُّيوُنِ وَالْمَظَالِمِ وَالنَّارِ</div>

                <h4 class="dhikr-label">4. Post-Prayer Duas</h4>
                <p style="font-size:0.8rem; font-weight:bold;">After Witr</p>
                <div class="arabic-text">اللَّهُمَّ إِنِّي أَعُوذُ بِرِضَاكَ مِنْ سَخَطِكَ، وَبِمُعَافَاتِكَ مِنْ عُقُوبَتِكَ، وَبِكَ مِنْكَ، لا أُحْصِي ثَنَاءً عَلَيْكَ أَنْتَ كَمَا أَثْنَيْتَ عَلَى نَفْسِكَ، فَلَكَ الْحَمْدُ حَتَّى تَرْضَى.</div>
                
                <p style="font-size:0.8rem; font-weight:bold;">After Tarawih</p>
                <div class="arabic-text">الْحَمْدُ لِلَّهِ رَبِّ الْعَالَمِينَ. اَللَّهُمَّ صَلِّ عَلَى سَيِّدِنَا مُحَمَّدٍ وَعَلَى آلِ سَيِّدِنَا مُحَمَّدٍ. رَبَّنَا ظَلَمْنَا أَنْفُسَنَا وَإِنْ لَمْ تَغْفِرْ لَنَا وَتَرْحَمْنَا لَنَكُونَنَّ مِنَ الْخَاسِرِينَ اللَّهُمَّ إِنَّ لَكَ فِي كُلِّ لَيْلَةٍ مِنْ لَيَالِي شَهْرِ رَمَضَانَ عُتَقَاءَ وَطُلَقَاءَ وَخُلَصَاءَ وَأُمَنَاءَ مِنَ النَّارِ اجْعَلْنَا مِنْ عُتَقَائِكَ وَطُلَقَائِكَ وَخُلَصَائِكَ وَأُمَنَائِكَ مِنَ النَّارِ اجْعَلْنَا يَا إِلَهَنَا يَا اللَّهُ يَا اللَّهُ يَا اللَّهُ مِنَ السُّعَدَاءِ الْمَقْبُولِينَ وَلَا تَجْعَلْنَا مِنَ الْأَشْقِيَاءِ الْمَطْرُودِينَ. رَبَّنَا تَقَبَّلْ مِنَّا صَلاتَنَا وَصِيَامَنَا وَقِيَامَنَا وَرُكُوعَنَا وَسُجُودَنَا وَتَخَشُّعَنَا وَتَضَرُّعَنَا وَاجْبُرْ تَقْصِيرَنَا وَاسْتَجِبْ دُعَائِنَا إِنَّكَ أَنْتَ السَّمِيعُ الْعَلِيمُ. رَبَّنَا آتِنَا فِي الدُّنْيَا حَسَنَةً وَفِي الْآخِرَةِ حَسَنَةً وَقِنَا عَذَابَ النَّارِ. رَبَّنَا تَقَبَّلْ مِنَّا إِنَّكَ أَنْتَ السَّمِيعُ الْعَلِيمُ. وَتُبْ عَلَيْنَا إِنَّكَ أَنْتَ التَّوَّابُ الرَّحِيمُ وَاغْفِرْ لَنَا يَا غَافِرَ الْمُذْنِبِينَ آمِينَ بِرَحْمَتِكَ يَا أَرْحَمَ الرَّاحِمِينَ. وَصَلَّى اللَّهُ عَلَى سَيِّدِنَا مُحَمَّدٍ وَعَلَى آلِهِ وَصَحْبِهِ أَجْمَعِينَ. وَالْحَمْدُ لِلَّهِ رَبِّ الْعَالَمِينَ.</div>
            </div>

            <div class="card">
                <h3><i class="fas fa-heart"></i> 99 Names of Allah</h3>
                <div class="names-grid" id="names-container"></div>
            </div>
        </div>

        <div id="settings" class="section">
            <div class="card">
                <h3><i class="fas fa-bullseye"></i> Goal Settings</h3>
                <label style="font-size:0.8rem; font-weight:bold;">Khatm Goal (No. of Completes)</label>
                <select id="khatm-goal" onchange="updateGoal()">
                    <option value="1">1 Khatm (1 Juz / Day)</option>
                    <option value="2">2 Khatms (2 Juz / Day)</option>
                    <option value="3">3 Khatms (3 Juz / Day)</option>
                </select>
            </div>

            <div class="card">
                <h3><i class="fas fa-plus-circle"></i> Dhikr Counters</h3>
                <div style="display:flex; gap:10px; margin-bottom: 10px;">
                    <input type="text" id="new-dhikr-name" placeholder="Dhikr Name" style="margin:0;">
                    <button onclick="addNewDhikr()" class="btn-sq" style="background:var(--accent); color:white; border:none;"><i class="fas fa-plus"></i></button>
                </div>
                <div id="dhikr-manager-list"></div>
            </div>

            <div class="card">
                <h3><i class="fas fa-feather"></i> Daily Journal</h3>
                <select id="day-select" onchange="loadNote()"></select>
                <textarea id="note-area" rows="4" placeholder="Your spiritual journey today..."></textarea>
                <button onclick="saveNote()" style="width:100%; background:var(--accent); color:white; border:none; padding:15px; border-radius:12px; font-weight:800; cursor:pointer;">SAVE JOURNAL</button>
            </div>
        </div>

        <footer>
            <p>© 2026 • QABSAT-muhyissunna kolathur • All Rights Reserved</p>
        </footer>
    </div>

    <nav class="nav-bar">
        <div class="nav-item active" onclick="showSection('home')"><i class="fas fa-home"></i>Home</div>
        <div class="nav-item" onclick="showSection('prayer')"><i class="fas fa-clock"></i>Prayer</div>
        <div class="nav-item" onclick="showSection('adhkar')"><i class="fas fa-book-open"></i>Adhkar</div>
        <div class="nav-item" onclick="showSection('settings')"><i class="fas fa-pen"></i>Journal</div>
    </nav>

    <script>
        let iftarTime = "";
        let currentJuz = parseInt(localStorage.getItem('q_juz')) || 0;
        let khatmGoal = parseInt(localStorage.getItem('q_goal')) || 1;
        
        let dhikrs = JSON.parse(localStorage.getItem('q_dhikrs')) || [
            {name:'Salawat', count:0}, {name:'Istighfar', count:0}, {name:'Subhanallah', count:0}
        ];

        const allahNames = ["الرحمن", "الرحيم", "الملك", "القدوس", "السلام", "المؤمن", "المهيمن", "العزيز", "الجبار", "المتكبر", "الخالق", "البارئ", "المصور", "الغفار", "القهار", "الوهاب", "الرزاق", "الفتاح", "العليم", "القابض", "الباسط", "الخافض", "الرافع", "المعز", "المذل", "السميع", "البصير", "الحكم", "العدل", "اللطيف", "الخبير", "الحليم", "العظيم", "الغفور", "الشكور", "العلي", "الكبير", "الحفيظ", "المقيت", "الحسيب", "الجليل", "الكريم", "الرقيب", "المجيب", "الواسع", "الحكيم", "الودود", "المجيد", "الباعث", "الشهيد", "الحق", "الوكيل", "القوي", "المتين", "الولي", "الحميد", "المحصي", "المبدئ", "المعيد", "المحيي", "المميت", "الحي", "القيوم", "الواجد", "الماجد", "الواحد", "الأحد", "الصمد", "القادر", "المقتدر", "المقدم", "المؤخر", "الأول", "الآخر", "الظاهر", "الباطن", "الوالي", "المتعالي", "البر", "التواب", "المنتقم", "العفو", "الرؤوف", "مالك الملك", "ذو الجلال والإكرام", "المقسط", "الجامع", "الغني", "المغني", "المانع", "الضار", "النافع", "النور", "الهادي", "البديع", "الباقي", "الوارث", "الرشيد", "الصبور"];

        function closeGreeting() {
            const greet = document.getElementById('greeting-overlay');
            greet.style.transition = "0.8s";
            greet.style.opacity = "0";
            setTimeout(() => greet.style.display = 'none', 800);
        }

        function toggleDrawer() {
            const d = document.getElementById('drawer');
            const o = document.getElementById('overlay');
            const isOpen = d.classList.toggle('open');
            o.style.display = isOpen ? 'block' : 'none';
        }

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            const map = {home:0, prayer:1, adhkar:2, settings:3};
            document.querySelectorAll('.nav-item')[map[id]].classList.add('active');
            window.scrollTo(0,0);
        }

        function adjustJuz(v) {
            currentJuz = Math.max(0, currentJuz + v);
            document.getElementById('current-juz-val').innerText = currentJuz;
            localStorage.setItem('q_juz', currentJuz);
        }

        function updateGoal() {
            khatmGoal = document.getElementById('khatm-goal').value;
            document.getElementById('khatm-goal-display').innerText = `GOAL: ${khatmGoal} KHATM`;
            localStorage.setItem('q_goal', khatmGoal);
        }

        function toggleCheck(el, key) {
            el.classList.toggle('done');
            localStorage.setItem(key + '_' + new Date().toDateString(), el.classList.contains('done'));
        }

        function updateAshra() {
            const day = 1; // Logic for Ramadan Day
            const title = document.getElementById('ashra-title');
            const text = document.getElementById('ashra-dua-text');
            if(day <= 10) {
                title.innerText = "First Ashra (Mercy)";
                text.innerText = "اللَّهُمَّ ارْحَمْنِي يَا أَرْحَمَ الرَّاحِمِينَ";
            } else if (day <= 20) {
                title.innerText = "Middle Ashra (Forgiveness)";
                text.innerText = "اللَّهُمَّ اغْفِرْ لِي ذُنُوبِي يَارَبَّ الْعَالَمِينَ";
            } else {
                title.innerText = "Last Ashra (Protection)";
                text.innerText = "اللَّهُمَّ إِنَّكَ عَفُوٌّ تُحِبُّ الْعَفْوَ فَاعْفُ عَنِّي";
            }
        }

        async function fetchTimings(lat, lon) {
            document.getElementById('loc-status').innerText = "Syncing...";
            try {
                const res = await fetch(`https://api.aladhan.com/v1/timings?latitude=${lat}&longitude=${lon}&method=1`);
                const d = await res.json();
                const t = d.data.timings;
                iftarTime = t.Maghrib;
                document.getElementById('prayer-display').innerHTML = `
                    <div style="display:flex; justify-content:space-between; border-bottom:1px solid var(--border);"><span>Subah</span><b>${t.Fajr}</b></div>
                    <div style="display:flex; justify-content:space-between; border-bottom:1px solid var(--border);"><span>Luhr</span><b>${t.Dhuhr}</b></div>
                    <div style="display:flex; justify-content:space-between; border-bottom:1px solid var(--border);"><span>Asr</span><b>${t.Asr}</b></div>
                    <div style="display:flex; justify-content:space-between; color:var(--accent); font-weight:800; border-bottom:1px solid var(--border);"><span>Maghrib</span><b>${t.Maghrib}</b></div>
                    <div style="display:flex; justify-content:space-between;"><span>Isha</span><b>${t.Isha}</b></div>`;
                document.getElementById('loc-status').innerText = d.data.meta.timezone;
            } catch (e) { document.getElementById('loc-status').innerText = "Offline"; }
        }

        function exportToPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            doc.setFontSize(20);
            doc.text("QABSAT Ramadan Journal 2026", 20, 20);
            doc.setFontSize(12);
            let y = 30;
            for(let i=1; i<=30; i++) {
                let note = localStorage.getItem('q_n_'+i) || "No entry";
                doc.text(`Day ${i}: ${note}`, 20, y);
                y += 10;
                if(y > 280) { doc.addPage(); y = 20; }
            }
            doc.save("Ramadan_Journey_2026.pdf");
        }

        function renderDhikrs() {
            const homeList = document.getElementById('dhikr-list-home');
            const manageList = document.getElementById('dhikr-manager-list');
            homeList.innerHTML = ''; manageList.innerHTML = '';
            dhikrs.forEach((d, i) => {
                homeList.innerHTML += `<div class="dhikr-counter-card">
                    <div style="display:flex; justify-content:space-between; font-weight:800; margin-bottom:10px;"><span>${d.name}</span><span>${d.count}</span></div>
                    <div style="display:flex;"><button class="btn-sq" onclick="adjDhikr(${i},-1)">-</button><button class="btn-sq btn-plus" onclick="adjDhikr(${i},1)">COUNT</button><button class="btn-sq" onclick="adjDhikr(${i},0)">↺</button></div></div>`;
                manageList.innerHTML += `<div style="display:flex; justify-content:space-between; align-items:center; background:var(--bg); padding:10px; border-radius:12px; margin-bottom:10px; border:1px solid var(--border);"><b>${d.name}</b><button onclick="delDhikr(${i})" style="color:#ef4444; border:none; background:none;"><i class="fas fa-trash-alt"></i></button></div>`;
            });
            localStorage.setItem('q_dhikrs', JSON.stringify(dhikrs));
        }

        function adjDhikr(i, v) { dhikrs[i].count = (v === 0) ? 0 : Math.max(0, dhikrs[i].count + v); renderDhikrs(); }
        function addNewDhikr() { const name = document.getElementById('new-dhikr-name').value; if(name) { dhikrs.push({name, count:0}); document.getElementById('new-dhikr-name').value=''; renderDhikrs(); } }
        function delDhikr(i) { dhikrs.splice(i, 1); renderDhikrs(); }

        window.onload = () => {
            document.getElementById('eng-date-display').innerText = new Date().toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' });
            document.getElementById('current-juz-val').innerText = currentJuz;
            document.getElementById('khatm-goal').value = khatmGoal;
            document.getElementById('khatm-goal-display').innerText = `GOAL: ${khatmGoal} KHATM`;
            
            updateAshra();
            renderDhikrs();
            
            fetch('https://api.alquran.cloud/v1/surah').then(r => r.json()).then(d => {
                d.data.forEach(s => document.getElementById('surah-select').innerHTML += `<option value="${s.number}">${s.number}. ${s.englishName}</option>`);
            });
            allahNames.forEach(n => document.getElementById('names-container').innerHTML += `<div class="name-box">${n}</div>`);
            for(let i=1; i<=30; i++) document.getElementById('day-select').innerHTML += `<option value="${i}">Day ${i}</option>`;
            
            // Set Sunnah of Day based on Friday or weekday
            if(new Date().getDay() === 5) document.getElementById('sunnah-desc').innerText = "Reciting Surah Al-Kahf & sending Salawat.";

            setInterval(() => {
                if(!iftarTime) return;
                const now = new Date();
                const target = new Date(now.toDateString() + ' ' + iftarTime);
                const diff = target - now;
                if(diff > 0) {
                    const h = Math.floor(diff/3600000).toString().padStart(2,'0');
                    const m = Math.floor((diff%3600000)/60000).toString().padStart(2,'0');
                    const s = Math.floor((diff%60000)/1000).toString().padStart(2,'0');
                    document.getElementById('timer').innerText = `${h}:${m}:${s}`;
                } else { document.getElementById('timer').innerText = "00:00:00"; }
            }, 1000);
            
            updateLocationMode();
        };

        function updateLocationMode() {
            const mode = document.getElementById('location-mode').value;
            const presets = { malappuram: {lat: 11.0735, lon: 76.0740} };
            if(mode === 'auto') {
                navigator.geolocation.getCurrentPosition(pos => fetchTimings(pos.coords.latitude, pos.coords.longitude), 
                () => fetchTimings(presets.malappuram.lat, presets.malappuram.lon));
            } else { fetchTimings(presets.malappuram.lat, presets.malappuram.lon); }
        }

        function toggleTheme() {
            const current = document.body.getAttribute('data-theme');
            document.body.setAttribute('data-theme', current === 'dark' ? 'light' : 'dark');
        }

        function saveNote() { localStorage.setItem('q_n_'+document.getElementById('day-select').value, document.getElementById('note-area').value); alert("Saved!"); }
        function loadNote() { document.getElementById('note-area').value = localStorage.getItem('q_n_'+document.getElementById('day-select').value) || ""; }
    </script>
</body>
</html>
