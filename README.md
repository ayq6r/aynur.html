<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CodeBeat — Müzik Çalar</title>
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-black: #000000;
            --bg-base: #121212;
            --bg-card: #181818;
            --bg-card-hover: #282828;
            --spotify-green: #1DB954;
            --text-white: #ffffff;
            --text-gray: #b3b3b3;
            --border: #282828;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background-color: var(--bg-black);
            color: var(--text-white);
            font-family: 'DM Sans', sans-serif;
            display: grid;
            grid-template-areas: "sidebar main" "player player";
            grid-template-columns: 240px 1fr;
            grid-template-rows: 1fr 100px;
            height: 100vh;
            overflow: hidden;
        }

        /* SIDEBAR */
        aside { grid-area: sidebar; background-color: var(--bg-black); padding: 24px 12px; border-right: 1px solid var(--border); }
        .logo { font-size: 22px; font-weight: 700; color: var(--text-white); margin-bottom: 30px; padding-left: 10px; }
        .logo span { color: var(--spotify-green); }
        nav ul { list-style: none; }
        nav ul li a { color: var(--text-gray); text-decoration: none; padding: 12px; display: block; transition: 0.3s; font-weight: 600; }
        nav ul li a:hover { color: white; }

        /* MAIN */
        main { grid-area: main; background: linear-gradient(to bottom, #222, var(--bg-base)); padding: 32px; overflow-y: auto; }
        .section-title { font-size: 28px; margin-bottom: 24px; }
        
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
        }

        .music-card {
            background: var(--bg-card);
            padding: 16px;
            border-radius: 10px;
            cursor: pointer;
            transition: 0.3s;
            position: relative;
        }
        .music-card:hover { background: var(--bg-card-hover); transform: translateY(-5px); }
        .music-card img { width: 100%; aspect-ratio: 1; border-radius: 8px; margin-bottom: 12px; object-fit: cover; }
        .music-card h3 { font-size: 16px; margin-bottom: 5px; }
        .music-card p { font-size: 13px; color: var(--text-gray); }

        .play-icon-overlay {
            position: absolute;
            bottom: 80px;
            right: 25px;
            background: var(--spotify-green);
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: 0.3s;
            box-shadow: 0 8px 16px rgba(0,0,0,0.3);
        }
        .music-card:hover .play-icon-overlay { opacity: 1; bottom: 90px; }

        /* PLAYER BAR */
        .player-bar {
            grid-area: player;
            background-color: #121212;
            border-top: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 20px;
        }

        .current-track { display: flex; align-items: center; gap: 15px; width: 30%; }
        .current-track img { width: 60px; height: 60px; border-radius: 5px; }
        
        .player-controls { width: 40%; text-align: center; }
        .progress-container { display: flex; align-items: center; gap: 10px; margin-top: 10px; }
        .progress-bar { flex: 1; height: 4px; background: #4d4d4d; border-radius: 2px; cursor: pointer; }
        #progress { height: 100%; background: var(--spotify-green); width: 0%; border-radius: 2px; }

        .btn-circle {
            background: white;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            color: black;
            cursor: pointer;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <aside>
        <div class="logo"><span>Code</span>Beat</div>
        <nav>
            <ul>
                <li><a href="#">🏠 Ana Sayfa</a></li>
                <li><a href="#">🔍 Kitaplığın</a></li>
            </ul>
        </nav>
    </aside>

    <main>
        <h2 class="section-title">Koleksiyonun</h2>
        <div class="grid-container">
            <div class="music-card" onclick="playMusic('Fikrimin İnce Gülü', 'Özdemir Erdoğan', 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3', 'https://images.unsplash.com/photo-1493225255756-d9584f8606e9?w=300')">
                <img src="https://images.unsplash.com/photo-1493225255756-d9584f8606e9?w=300" alt="Fikrim">
                <h3>Fikrimin İnce Gülü</h3>
                <p>Özdemir Erdoğan</p>
                <div class="play-icon-overlay">▶</div>
            </div>

            <div class="music-card" onclick="playMusic('Ankara Rüzgarı', 'Zeki Müren', 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3', 'https://images.unsplash.com/photo-1459749411177-042180ce673c?w=300')">
                <img src="https://images.unsplash.com/photo-1459749411177-042180ce673c?w=300" alt="Zeki">
                <h3>Ankara Rüzgarı</h3>
                <p>Zeki Müren</p>
                <div class="play-icon-overlay">▶</div>
            </div>

            <div class="music-card" onclick="playMusic('Lo-Fi Coding Beats', 'CodeLab Special', 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3', 'https://images.unsplash.com/photo-1516259762381-22954d7d3ad2?w=300')">
                <img src="https://images.unsplash.com/photo-1516259762381-22954d7d3ad2?w=300" alt="Lo-Fi">
                <h3>Lo-Fi Coding Beats</h3>
                <p>Focus & Study</p>
                <div class="play-icon-overlay">▶</div>
            </div>
        </div>
    </main>

    <div class="player-bar">
        <div class="current-track">
            <img id="player-img" src="https://via.placeholder.com/60" alt="">
            <div class="track-info">
                <h4 id="player-title">Şarkı Seçin</h4>
                <p id="player-artist">-</p>
            </div>
        </div>

        <div class="player-controls">
            <div class="btn-circle" id="playPauseBtn" onclick="togglePlay()">▶</div>
            <div class="progress-container">
                <span id="currentTime">0:00</span>
                <div class="progress-bar" onclick="seek(event)">
                    <div id="progress"></div>
                </div>
                <span id="duration">0:00</span>
            </div>
        </div>

        <audio id="mainAudio" src=""></audio>
    </div>

    <script>
        const audio = document.getElementById('mainAudio');
        const playPauseBtn = document.getElementById('playPauseBtn');
        const progressBar = document.getElementById('progress');
        const playerTitle = document.getElementById('player-title');
        const playerArtist = document.getElementById('player-artist');
        const playerImg = document.getElementById('player-img');

        function playMusic(title, artist, url, img) {
            playerTitle.innerText = title;
            playerArtist.innerText = artist;
            playerImg.src = img;
            audio.src = url;
            audio.play();
            playPauseBtn.innerText = '⏸';
        }

        function togglePlay() {
            if (audio.paused) {
                audio.play();
                playPauseBtn.innerText = '⏸';
            } else {
                audio.pause();
                playPauseBtn.innerText = '▶';
            }
        }

        audio.ontimeupdate = function() {
            const pct = (audio.currentTime / audio.duration) * 100;
            progressBar.style.width = pct + "%";
            
            // Zaman güncelleme
            document.getElementById('currentTime').innerText = formatTime(audio.currentTime);
            if(audio.duration) document.getElementById('duration').innerText = formatTime(audio.duration);
        };

        function formatTime(sec) {
            let min = Math.floor(sec / 60);
            let s = Math.floor(sec % 60);
            if (s < 10) s = "0" + s;
            return min + ":" + s;
        }

        function seek(e) {
            const rect = e.target.closest('.progress-bar').getBoundingClientRect();
            const pos = (e.clientX - rect.left) / rect.width;
            audio.currentTime = pos * audio.duration;
        }
    </script>
</body>
</html>
