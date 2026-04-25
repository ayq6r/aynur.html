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
        aside { 
            grid-area: sidebar; 
            background-color: var(--bg-black); 
            padding: 24px 12px; 
            display: flex; 
            flex-direction: column;
            border-right: 1px solid var(--border);
        }
        .logo { font-size: 22px; font-weight: 700; color: var(--text-white); margin-bottom: 30px; padding-left: 10px; }
        .logo span { color: var(--spotify-green); }
        nav ul { list-style: none; }
        nav ul li a { color: var(--text-gray); text-decoration: none; padding: 12px; display: block; border-radius: 4px; transition: 0.3s; font-weight: 600; }
        nav ul li a:hover, nav ul li a.active { color: white; background: var(--bg-card-hover); }

        /* MAIN CONTENT */
        main { 
            grid-area: main; 
            background: linear-gradient(to bottom, #222, var(--bg-base)); 
            padding: 32px; 
            overflow-y: auto; 
        }
        .section-title { font-size: 28px; margin-bottom: 24px; font-weight: 700; }
        
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 24px;
        }

        .music-card {
            background: var(--bg-card);
            padding: 16px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }
        .music-card:hover { background: var(--bg-card-hover); transform: translateY(-5px); }
        .music-card img { width: 100%; aspect-ratio: 1; border-radius: 8px; margin-bottom: 12px; object-fit: cover; box-shadow: 0 8px 16px rgba(0,0,0,0.5); }
        .music-card h3 { font-size: 16px; margin-bottom: 5px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .music-card p { font-size: 13px; color: var(--text-gray); }

        /* Play Button Hover Overlay */
        .play-btn-overlay {
            position: absolute;
            bottom: 85px;
            right: 25px;
            background: var(--spotify-green);
            width: 48px;
            height: 48px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transform: translateY(10px);
            transition: all 0.3s ease;
            box-shadow: 0 8px 15px rgba(0,0,0,0.3);
            color: black;
            font-size: 20px;
        }
        .music-card:hover .play-btn-overlay { opacity: 1; transform: translateY(0); }

        /* PLAYER BAR */
        .player-bar {
            grid-area: player;
            background-color: #121212;
            border-top: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 25px;
            z-index: 10;
        }

        .current-track { display: flex; align-items: center; gap: 15px; width: 30%; }
        .current-track img { width: 56px; height: 56px; border-radius: 4px; object-fit: cover; background: #282828; }
        .track-info h4 { font-size: 14px; margin-bottom: 3px; }
        .track-info p { font-size: 11px; color: var(--text-gray); }
        
        .player-controls { width: 40%; display: flex; flex-direction: column; align-items: center; gap: 8px; }
        .control-btns { display: flex; align-items: center; gap: 25px; font-size: 18px; }
        .play-pause-main { 
            background: white; color: black; width: 32px; height: 32px; 
            border-radius: 50%; display: flex; align-items: center; justify-content: center; 
            cursor: pointer; transition: 0.2s; font-size: 14px;
        }
        .play-pause-main:hover { transform: scale(1.1); }

        .progress-area { width: 100%; display: flex; align-items: center; gap: 10px; }
        .time { font-size: 11px; color: var(--text-gray); min-width: 35px; }
        .progress-bg { flex: 1; height: 4px; background: #4d4d4d; border-radius: 2px; cursor: pointer; position: relative; }
        .progress-fill { height: 100%; background: var(--spotify-green); width: 0%; border-radius: 2px; transition: width 0.1s linear; }

        .volume-area { width: 30%; display: flex; justify-content: flex-end; color: var(--text-gray); font-size: 14px; }
    </style>
</head>
<body>

    <aside>
        <div class="logo"><span>Code</span>Beat 🎧</div>
        <nav>
            <ul>
                <li><a href="#" class="active">🏠 Ana Sayfa</a></li>
                <li><a href="#">🔍 Ara</a></li>
                <li><a href="#">📚 Kitaplığın</a></li>
            </ul>
        </nav>
    </aside>

    <main>
        <h2 class="section-title">Senin İçin Seçilenler</h2>
        <div class="grid-container">
            
            <div class="music-card" onclick="playMusic('Fikrimin İnce Gülü', 'Dedublüman', 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3', 'https://images.unsplash.com/photo-1514525253344-76240003a568?w=400')">
                <img src="https://images.unsplash.com/photo-1514525253344-76240003a568?w=400" alt="Fikrimin İnce Gülü">
                <h3>Fikrimin İnce Gülü</h3>
                <p>Dedublüman</p>
                <div class="play-btn-overlay">▶</div>
            </div>

            <div class="music-card" onclick="playMusic('100. Yıl Marşı', 'Kıraç', 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3', 'https://images.unsplash.com/photo-1533174072545-7a4b6ad7a6c3?w=400')">
                <img src="https://images.unsplash.com/photo-1533174072545-7a4b6ad7a6c3?w=400" alt="100. Yıl Marşı">
                <h3>100. Yıl Marşı</h3>
                <p>Kıraç</p>
                <div class="play-btn-overlay">▶</div>
            </div>

            <div class="music-card" onclick="playMusic('Lo-Fi Coding', 'CodeLab', 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3', 'https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=400')">
                <img src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=400" alt="Coding">
                <h3>Odaklanma (Coding)</h3>
                <p>CodeLab Beats</p>
                <div class="play-btn-overlay">▶</div>
            </div>

        </div>
    </main>

    <div class="player-bar">
        <div class="current-track">
            <img id="p-img" src="https://via.placeholder.com/56" alt="">
            <div class="track-info">
                <h4 id="p-title">Şarkı seçin</h4>
                <p id="p-artist">-</p>
            </div>
        </div>

        <div class="player-controls">
            <div class="control-btns">
                <span>⏮</span>
                <div class="play-pause-main" id="mainPlayBtn" onclick="togglePlay()">▶</div>
                <span>⏭</span>
            </div>
            <div class="progress-area">
                <span class="time" id="time-current">0:00</span>
                <div class="progress-bg" onclick="seek(event)">
                    <div class="progress-fill" id="p-fill"></div>
                </div>
                <span class="time" id="time-total">0:00</span>
            </div>
        </div>

        <div class="volume-area">
            🔊 [ —————— ]
        </div>
    </div>

    <audio id="audioEngine"></audio>

    <script>
        const audio = document.getElementById('audioEngine');
        const playBtn = document.getElementById('mainPlayBtn');
        const fill = document.getElementById('p-fill');
        const title = document.getElementById('p-title');
        const artist = document.getElementById('p-artist');
        const img = document.getElementById('p-img');
        const currTimeText = document.getElementById('time-current');
        const totalTimeText = document.getElementById('time-total');

        function playMusic(sTitle, sArtist, sUrl, sImg) {
            title.innerText = sTitle;
            artist.innerText = sArtist;
            img.src = sImg;
            audio.src = sUrl;
            
            audio.play();
            playBtn.innerText = '⏸';
        }

        function togglePlay() {
            if (!audio.src) return;
            if (audio.paused) {
                audio.play();
                playBtn.innerText = '⏸';
            } else {
                audio.pause();
                playBtn.innerText = '▶';
            }
        }

        // İlerleme çubuğu güncelleme
        audio.addEventListener('timeupdate', () => {
            const position = audio.currentTime / audio.duration;
            fill.style.width = (position * 100) + '%';
            
            currTimeText.innerText = formatTime(audio.currentTime);
            if(audio.duration) {
                totalTimeText.innerText = formatTime(audio.duration);
            }
        });

        function formatTime(seconds) {
            let min = Math.floor(seconds / 60);
            let sec = Math.floor(seconds % 60);
            if (sec < 10) sec = '0' + sec;
            return min + ':' + sec;
        }

        function seek(event) {
            if(!audio.src) return;
            const rect = event.currentTarget.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const width = rect.width;
            const percentage = x / width;
            audio.currentTime = percentage * audio.duration;
        }

        // Şarkı bittiğinde butonu sıfırla
        audio.onended = () => {
            playBtn.innerText = '▶';
        };
    </script>
</body>
</html>
