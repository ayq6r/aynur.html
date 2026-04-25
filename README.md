<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CodeBeat — Geleceği Dinle</title>
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
            grid-template-areas: 
                "sidebar main"
                "player player";
            grid-template-columns: 240px 1fr;
            grid-template-rows: 1fr 90px;
            height: 100vh;
        }

        /* ── SIDEBAR ── */
        aside {
            grid-area: sidebar;
            background-color: var(--bg-black);
            padding: 24px 12px;
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        .logo {
            font-size: 22px;
            font-weight: 700;
            color: var(--text-white);
            padding-left: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo span { color: var(--spotify-green); }

        nav ul { list-style: none; }
        nav ul li a {
            color: var(--text-gray);
            text-decoration: none;
            font-weight: 600;
            font-size: 14px;
            padding: 12px;
            display: block;
            border-radius: 4px;
            transition: 0.3s;
        }
        nav ul li a:hover { color: var(--text-white); }

        .playlist-section {
            border-top: 1px solid var(--border);
            padding-top: 12px;
            overflow-y: auto;
        }

        /* ── MAIN CONTENT ── */
        main {
            grid-area: main;
            background: linear-gradient(to bottom, #222222, var(--bg-base));
            padding: 24px 32px;
            overflow-y: auto;
            border-radius: 8px 0 0 0;
        }

        .header-nav {
            display: flex;
            justify-content: space-between;
            margin-bottom: 30px;
        }

        .section-title {
            font-size: 24px;
            margin-bottom: 20px;
        }

        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 24px;
        }

        .music-card {
            background: var(--bg-card);
            padding: 16px;
            border-radius: 8px;
            transition: background 0.3s ease;
            cursor: pointer;
            position: relative;
        }

        .music-card:hover { background: var(--bg-card-hover); }

        .music-card img {
            width: 100%;
            aspect-ratio: 1;
            border-radius: 6px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            margin-bottom: 16px;
        }

        .music-card h3 { font-size: 16px; margin-bottom: 8px; }
        .music-card p { font-size: 13px; color: var(--text-gray); line-height: 1.4; }

        /* ── PLAYER BAR ── */
        .player-bar {
            grid-area: player;
            background-color: var(--bg-black);
            border-top: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 16px;
        }

        .current-track { display: flex; align-items: center; gap: 14px; width: 30%; }
        .current-track img { width: 56px; height: 56px; border-radius: 4px; }
        .track-info h4 { font-size: 14px; }
        .track-info p { font-size: 11px; color: var(--text-gray); }

        .player-controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            width: 40%;
        }

        .buttons { display: flex; gap: 20px; align-items: center; }
        .play-btn {
            background: var(--text-white);
            width: 32px; height: 32px;
            border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; color: black;
        }

        .progress-bar {
            width: 100%;
            height: 4px;
            background: #4d4d4d;
            border-radius: 2px;
            position: relative;
        }
        .progress-fill {
            width: 30%;
            height: 100%;
            background: var(--text-white);
            border-radius: 2px;
        }

        .volume-controls { width: 30%; display: flex; justify-content: flex-end; }
    </style>
</head>
<body>

    <aside>
        <div class="logo"><span>Code</span>Beat 🎧</div>
        <nav>
            <ul>
                <li><a href="#" style="color:white">🏠 Ana Sayfa</a></li>
                <li><a href="#">🔍 Ara</a></li>
                <li><a href="#">📚 Kitaplığın</a></li>
            </ul>
        </nav>
        <div class="playlist-section">
            <nav>
                <ul>
                    <li><a href="#">➕ Çalma Listesi Oluştur</a></li>
                    <li><a href="#">❤️ Beğenilen Şarkılar</a></li>
                    <li><a href="#">C++ Çalışırken Dinle</a></li>
                    <li><a href="#">Lo-Fi Coding Beats</a></li>
                </ul>
            </nav>
        </div>
    </aside>

    <main>
        <div class="header-nav">
            <div class="arrows">⬅️ ➡️</div>
            <div class="user-btn">Profilim ▼</div>
        </div>

        <h2 class="section-title">Senin İçin Hazırlandı</h2>
        <div class="grid-container">
            <div class="music-card">
                <img src="https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?w=400&h=400&fit=crop" alt="Mix 1">
                <h3>Daily Mix 1</h3>
                <p>C++ ve Python odaklı derin odaklanma müzikleri.</p>
            </div>
            <div class="music-card">
                <img src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?w=400&h=400&fit=crop" alt="Mix 2">
                <h3>Coding Mode</h3>
                <p>Arduino projeleri yaparken enerjin düşmesin.</p>
            </div>
            <div class="music-card">
                <img src="https://images.unsplash.com/photo-1550745165-9bc0b252726f?w=400&h=400&fit=crop" alt="Mix 3">
                <h3>Retro Tech</h3>
                <p>8-bit synthwave tınıları ile nostalji yap.</p>
            </div>
        </div>
    </main>

    <div class="player-bar">
        <div class="current-track">
            <img src="https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?w=100&h=100&fit=crop" alt="Current">
            <div class="track-info">
                <h4>Code the Future</h4>
                <p>The Developer Collective</p>
            </div>
        </div>

        <div class="player-controls">
            <div class="buttons">
                <span>🔀</span> <span>⏮️</span>
                <div class="play-btn">▶</div>
                <span>⏭️</span> <span>🔁</span>
            </div>
            <div class="progress-bar">
                <div class="progress-fill"></div>
            </div>
        </div>

        <div class="volume-controls">
            🔊 [——————]
        </div>
    </div>

</body>
</html>
