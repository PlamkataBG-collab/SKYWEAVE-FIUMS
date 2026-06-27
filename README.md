<!DOCTYPE html>
<html lang="bg">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Balkan Byte Games Studio</title>
    <link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@400;700;800&family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    
    <style>
        /* --- ROCKSTAR STYLE VARIABLE & RESET --- */
        :root {
            --bg-color: #000000;
            --card-bg: #0a0a0a;
            --accent-color: #fca311; /* Топло Rockstar жълто */
            --text-main: #ffffff;
            --text-muted: #707070;
            --border-color: #1a1a1a;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Roboto', sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* Заглавия в стил Rockstar (Масивни и Големи) */
        h1, h2, h3, .logo {
            font-family: 'Barlow Condensed', sans-serif;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        a {
            text-decoration: none;
            color: inherit;
            transition: all 0.2s ease-in-out;
        }

        /* --- НАВИГАЦИЯ (ЧИСТ МИНИМАЛИЗЪМ) --- */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 25px 5%;
            background-color: rgba(0, 0, 0, 0.9);
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom: 1px solid var(--border-color);
            backdrop-filter: blur(10px);
        }

        .logo {
            font-size: 28px;
            font-weight: 800;
            color: #fff;
            letter-spacing: 0px;
        }

        .logo span {
            color: var(--accent-color);
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 40px;
        }

        nav ul li a {
            font-family: 'Barlow Condensed', sans-serif;
            font-size: 20px;
            font-weight: 700;
            color: #fff;
            letter-spacing: 1px;
        }

        nav ul li a:hover {
            color: var(--accent-color);
        }

        .nav-cta {
            border: 2px solid var(--accent-color);
            padding: 5px 15px;
            color: var(--accent-color) !important;
        }

        .nav-cta:hover {
            background: var(--accent-color);
            color: #000 !important;
        }

        /* --- ГЛАВЕН БАНЕР (HERO SECTION) --- */
        .hero {
            height: 85vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            position: relative;
            background: radial-gradient(circle, rgba(20,20,20,1) 0%, rgba(0,0,0,1) 100%);
            padding: 20px;
            border-bottom: 1px solid var(--border-color);
        }

        .hero img {
            max-width: 320px;
            margin-bottom: 30px;
            filter: drop-shadow(0px 0px 20px rgba(252, 163, 17, 0.2));
        }

        .hero h1 {
            font-size: 5rem;
            font-weight: 800;
            line-height: 1;
            margin-bottom: 10px;
        }

        .hero p {
            font-size: 1.2rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 4px;
        }

        /* --- СЕКЦИИ (ОБЩИ) --- */
        section {
            padding: 120px 5%;
        }

        .section-title {
            font-size: 3.5rem;
            font-weight: 800;
            margin-bottom: 50px;
            border-left: 6px solid var(--accent-color);
            padding-left: 20px;
            line-height: 1;
        }

        /* --- СЕКЦИЯ: ИГРИ (NEWEST GAME BLOCK) --- */
        #games {
            background: #050505;
        }

        .game-showcase {
            display: grid;
            grid-template-columns: 1fr 1fr;
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 4px;
            overflow: hidden;
        }

        .game-img-wrapper {
            overflow: hidden;
            position: relative;
        }

        .game-img-wrapper img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .game-showcase:hover .game-img-wrapper img {
            transform: scale(1.05);
        }

        .game-info {
            padding: 60px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .game-info .tag {
            color: var(--accent-color);
            text-transform: uppercase;
            font-weight: 700;
            font-size: 0.9rem;
            letter-spacing: 2px;
            margin-bottom: 10px;
        }

        .game-info h2 {
            font-size: 4rem;
            margin-bottom: 20px;
            line-height: 1;
        }

        .game-info p {
            color: #a0a0a0;
            margin-bottom: 30px;
            font-size: 1.1rem;
            line-height: 1.6;
        }

        .btn-play {
            align-self: flex-start;
            background: #fff;
            color: #000;
            font-family: 'Barlow Condensed', sans-serif;
            font-size: 1.3rem;
            font-weight: 700;
            padding: 12px 35px;
            text-transform: uppercase;
            border: 2px solid #fff;
        }

        .btn-play:hover {
            background: transparent;
            color: #fff;
        }

        /* --- СЕКЦИЯ: ЗА НАС (ABOUT) --- */
        #about {
            max-width: 1200px;
            margin: 0 auto;
        }

        .about-content {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 60px;
        }

        .about-content h3 {
            font-size: 2.5rem;
            color: var(--accent-color);
            line-height: 1.1;
        }

        .about-text p {
            font-size: 1.2rem;
            color: #c0c0c0;
            margin-bottom: 25px;
            line-height: 1.7;
        }

        /* --- СЕКЦИЯ: ЕКИП (CHARACTER DOSSIERS) --- */
        #team {
            background-color: #050505;
        }

        .team-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
            gap: 30px;
        }

        .team-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            display: flex;
            height: 320px;
            overflow: hidden;
            position: relative;
        }

        .team-card:hover {
            border-color: var(--accent-color);
        }

        .member-details {
            padding: 30px;
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .member-details h2 {
            font-size: 2.2rem;
            line-height: 1;
            margin-bottom: 5px;
        }

        .member-details h3 {
            font-size: 1.1rem;
            color: var(--accent-color);
            letter-spacing: 1px;
            margin-bottom: 15px;
        }

        .member-meta {
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        .member-meta span {
            color: #fff;
            display: block;
            margin-bottom: 5px;
        }

        .team-card img {
            width: 200px;
            height: 100%;
            object-fit: cover;
            border-left: 1px solid var(--border-color);
            background: #111;
        }

        /* --- СЕКЦИЯ: КОНТАКТИ --- */
        #contact {
            text-align: center;
            background: #000;
            border-top: 1px solid var(--border-color);
        }

        .contact-wrap {
            max-width: 700px;
            margin: 0 auto;
        }

        #contact p.desc {
            font-size: 1.2rem;
            color: var(--text-muted);
            margin-bottom: 40px;
        }

        .email-link {
            font-family: 'Barlow Condensed', sans-serif;
            font-size: 3rem;
            font-weight: 800;
            color: #fff;
            display: inline-block;
            margin-bottom: 40px;
        }

        .email-link:hover {
            color: var(--accent-color);
        }

        .social-row {
            display: flex;
            justify-content: center;
            gap: 20px;
        }

        .social-btn {
            border: 1px solid var(--border-color);
            padding: 15px 40px;
            font-weight: 700;
            text-transform: uppercase;
            font-family: 'Barlow Condensed', sans-serif;
            font-size: 1.2rem;
            letter-spacing: 1px;
        }

        .social-btn:hover {
            background: #fff;
            color: #000;
            border-color: #fff;
        }

        /* --- ФУТЪР --- */
        footer {
            padding: 40px 5%;
            text-align: center;
            border-top: 1px solid var(--border-color);
            color: var(--text-muted);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* --- МЕГА АДАПТИВНОСТ --- */
        @media (max-width: 992px) {
            .game-showcase {
                grid-template-columns: 1fr;
            }
            .about-content {
                grid-template-columns: 1fr;
                gap: 20px;
            }
        }

        @media (max-width: 768px) {
            nav {
                flex-direction: column;
                gap: 20px;
            }
            nav ul {
                gap: 20px;
            }
            .hero h1 {
                font-size: 3.2rem;
            }
            .section-title {
                font-size: 2.5rem;
            }
            .game-info {
                padding: 30px;
            }
            .game-info h2 {
                font-size: 2.8rem;
            }
            .team-card {
                flex-direction: column-reverse;
                height: auto;
            }
            .team-card img {
                width: 100%;
                height: 250px;
                border-left: none;
                border-bottom: 1px solid var(--border-color);
            }
            .email-link {
                font-size: 1.8rem;
            }
            .team-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <nav>
        <a href="#" class="logo">Balkan Byte Games <span>Studio</span></a>
        <ul>
            <li><a href="#games">Games</a></li>
            <li><a href="#about">Studio</a></li>
            <li><a href="#team">Team</a></li>
            <li><a href="#contact" class="nav-cta">Contact</a></li>
        </ul>
    </nav>

    <div class="hero">
        <img src="https://cdn.discordapp.com/attachments/1477240493166428161/1520436751687094282/9f7kb5z.png?ex=6a413091&is=6a3fdf11&hm=408d3d4b8caaee6f97859702dc2ef6c7555b0dde9766dfef02f83518037f65de&animated=true" alt="Balkan Byte Logo">
        <h1>BALKAN BYTE</h1>
        <p>Next-Gen Interactive Entertainment</p>
    </div>

    <section id="games">
        <h1 class="section-title">Featured Game</h1>
        
        <div class="game-showcase">
            <div class="game-img-wrapper">
                <img src="https://cdn.discordapp.com/attachments/1477240493166428161/1520426323678466198/39p6jhd.png?ex=6a4126db&is=6a3fd55b&hm=9afc8106ab7818e2b9f2218ee607997d9c1a75567fcf243d56942e7c0093c220&animated=true" alt="Caravan Life">
            </div>
            <div class="game-info">
                <span class="tag">Out Now</span>
                <h2>CARAVAN LIFE</h2>
                <p>Immerse yourself in the ultimate simulation experience. Build your legacy, explore massive open environments, and manage your journey in our flagship title. Built with attention to performance and deep engagement.</p>
                <a href="#" class="btn-play">Official Site</a>
            </div>
        </div>
    </section>

    <section id="about">
        <h1 class="section-title">The Studio</h1>
        <div class="about-content">
            <h3>Meticulous craft.<br>Unforgettable stories.</h3>
            <div class="about-text">
                <p>We are a passionate game development studio dedicated to creating fun, innovative, and high-quality games for players around the world. Our team combines creativity, technology, and storytelling to build unforgettable gaming experiences.</p>
                <p>From mobile and PC games to console and online multiplayer projects, we focus on delivering engaging gameplay, stunning visuals, and smooth performance. Every project is developed with attention to detail and a commitment to excellence.</p>
            </div>
        </div>
    </section>

    <section id="team">
        <h1 class="section-title">Leaders</h1>
        
        <div class="team-grid">
            <div class="team-card">
                <div class="member-details">
                    <div>
                        <h2>PLAMEN NEYCHEV</h2>
                        <h3>CEO / Chief Programmer</h3>
                    </div>
                    <div class="member-meta">
                        <span><strong>Discord:</strong> plamkatabg_top-│𝗽𝗹𝗮𝗺𝗸𝗮𝘁𝗮 ツ</span>
                        <span><strong>Contact:</strong> plamen_neychev_bg@abv.bg</span>
                    </div>
                </div>
                <img src="https://cdn.discordapp.com/avatars/1284523435309142027/6eea63b7e02ec774b2bfca07ee09f155.webp?size=1024" alt="Plamen">
            </div>

            <div class="team-card">
                <div class="member-details">
                    <div>
                        <h2>DANIEL TSANKOV</h2>
                        <h3>CEO / Marketing & Infrastructure</h3>
                    </div>
                    <div class="member-meta">
                        <span><strong>Discord:</strong> dankata_94240-Dankata</span>
                        <span><strong>Phone:</strong> +359 88 296 5409</span>
                        <span><strong>Contact:</strong> danieltsankov5@gmail.com</span>
                    </div>
                </div>
                <img src="https://cdn.discordapp.com/avatars/1473380944273608747/4b5ce3ebc454aed8dad968cebb8c24be.webp?size=1024" alt="Daniel">
            </div>
        </div>
    </section>

    <section id="contact">
        <div class="contact-wrap">
            <h1 class="section-title" style="border: none; padding: 0;">Contact Studio</h1>
            <p class="desc">For partnerships, press relations, job applications or community inquiries.</p>
            
            <a href="mailto:balkanbyte.studio@gmail.com" class="email-link">balkanbyte.studio@gmail.com</a>
            
            <div class="social-row">
                <a href="https://discord.gg/Js8BRrmA" class="social-btn" target="_blank">Discord</a>
                <a href="https://www.tiktok.com/@caravana_life263" class="social-btn" target="_blank">TikTok</a>
            </div>
        </div>
    </section>

    <footer>
        &copy; 2026 Balkan Byte Games. All rights reserved.
    </footer>

</body>
</html>
