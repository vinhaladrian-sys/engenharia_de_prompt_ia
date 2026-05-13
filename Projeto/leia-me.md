<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gattini - Cat Café Fofo</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-pink: #FFB6D9;
            --secondary-pink: #FFC0E0;
            --beige: #F5E6D3;
            --light-beige: #FAF3E7;
            --dark-text: #5C4A42;
            --accent-pink: #FF8AB5;
        }

        body {
            font-family: 'Comic Sans MS', 'Trebuchet MS', cursive, sans-serif;
            background: linear-gradient(135deg, var(--light-beige) 0%, var(--beige) 100%);
            color: var(--dark-text);
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* Animação de carregamento */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary-pink), var(--light-beige));
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            animation: fadeOut 0.5s ease-in-out 3s forwards;
        }

        @keyframes fadeOut {
            to {
                opacity: 0;
                pointer-events: none;
            }
        }

        .cat-loading {
            font-size: 80px;
            animation: bounce 0.6s ease-in-out infinite;
        }

        .yarn-ball {
            display: inline-block;
            width: 30px;
            height: 30px;
            background: var(--accent-pink);
            border-radius: 50%;
            margin-left: 20px;
            animation: swing 1.5s ease-in-out infinite;
            box-shadow: inset -2px -2px 5px rgba(0,0,0,0.1);
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-30px); }
        }

        @keyframes swing {
            0%, 100% { transform: rotate(-20deg) translateX(0); }
            50% { transform: rotate(20deg) translateX(10px); }
        }

        .loading-text {
            text-align: center;
            margin-top: 30px;
            font-size: 24px;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        /* Header */
        header {
            background: linear-gradient(135deg, var(--primary-pink), var(--secondary-pink));
            padding: 20px 0;
            box-shadow: 0 4px 15px rgba(255,182,217,0.3);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 20px;
        }

        .logo {
            font-size: 32px;
            font-weight: bold;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .logo-icon {
            display: inline-block;
            font-size: 40px;
            margin-right: 10px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        nav {
            display: flex;
            gap: 30px;
            flex-wrap: wrap;
            justify-content: center;
        }

        nav button {
            background: white;
            border: none;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            color: var(--accent-pink);
            transition: all 0.3s ease;
            font-family: 'Comic Sans MS', cursive;
            font-size: 14px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        nav button:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 12px rgba(255,138,181,0.3);
            background: var(--light-beige);
        }

        /* Animações de gatos andando */
        .walking-cat {
            position: fixed;
            font-size: 40px;
            pointer-events: none;
            z-index: 50;
        }

        .walking-cat.cat1 {
            animation: walkRight 20s infinite;
            bottom: 10%;
            left: -50px;
        }

        .walking-cat.cat2 {
            animation: walkLeft 25s infinite;
            top: 15%;
            right: -50px;
            animation-delay: 5s;
        }

        .walking-cat.cat3 {
            animation: walkRight 30s infinite;
            bottom: 30%;
            left: -50px;
            animation-delay: 10s;
        }

        @keyframes walkRight {
            0% { 
                left: -50px;
                transform: scaleX(1);
            }
            100% {
                left: 100%;
                transform: scaleX(1);
            }
        }

        @keyframes walkLeft {
            0% {
                right: -50px;
                transform: scaleX(-1);
            }
            100% {
                right: 100%;
                transform: scaleX(-1);
            }
        }

        /* Main Sections */
        .section {
            display: none;
            animation: fadeIn 0.5s ease-in;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Hero Section */
        .hero {
            text-align: center;
            padding: 60px 20px;
            background: linear-gradient(135deg, rgba(255,182,217,0.2), rgba(245,230,211,0.2));
            border-radius: 20px;
            margin: 40px 0;
        }

        .hero h1 {
            font-size: 48px;
            color: var(--accent-pink);
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .hero p {
            font-size: 20px;
            color: var(--dark-text);
            margin-bottom: 30px;
        }

        .hero-emoji {
            font-size: 60px;
            margin: 20px 0;
            animation: bounce 1s ease-in-out infinite;
        }

        /* Cards */
        .card {
            background: white;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 8px 20px rgba(255,182,217,0.2);
            transition: all 0.3s ease;
            border: 2px solid var(--secondary-pink);
        }

        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 12px 30px rgba(255,138,181,0.3);
        }

        .card-title {
            color: var(--accent-pink);
            font-size: 22px;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .card-icon {
            font-size: 50px;
            margin-bottom: 15px;
        }

        /* Cardápio */
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin: 40px 0;
        }

        .menu-item {
            background: white;
            border-radius: 15px;
            padding: 20px;
            border: 2px solid var(--secondary-pink);
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255,182,217,0.15);
        }

        .menu-item:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(255,138,181,0.3);
        }

        .menu-icon {
            font-size: 40px;
            margin-bottom: 10px;
        }

        .menu-name {
            color: var(--accent-pink);
            font-weight: bold;
            font-size: 18px;
            margin-bottom: 8px;
        }

        .menu-desc {
            color: var(--dark-text);
            font-size: 14px;
            margin-bottom: 10px;
        }

        .menu-price {
            color: var(--primary-pink);
            font-weight: bold;
            font-size: 16px;
        }

        /* Galeria */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 40px 0;
        }

        .gallery-item {
            position: relative;
            border-radius: 15px;
            overflow: hidden;
            aspect-ratio: 1;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255,182,217,0.2);
            background: linear-gradient(135deg, var(--primary-pink), var(--secondary-pink));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 80px;
            border: 3px solid white;
        }

        .gallery-item:hover {
            transform: scale(1.05) rotate(2deg);
            box-shadow: 0 8px 25px rgba(255,138,181,0.4);
        }

        .gallery-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.7), transparent);
            padding: 15px;
            color: white;
            font-weight: bold;
            transform: translateY(100%);
            transition: transform 0.3s ease;
        }

        .gallery-item:hover .gallery-overlay {
            transform: translateY(0);
        }

        /* Formulário */
        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: var(--dark-text);
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 2px solid var(--secondary-pink);
            border-radius: 10px;
            font-family: 'Comic Sans MS', cursive;
            font-size: 14px;
            transition: border-color 0.3s ease;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: var(--accent-pink);
            box-shadow: 0 0 10px rgba(255,138,181,0.3);
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        /* Botões */
        .btn {
            background: linear-gradient(135deg, var(--primary-pink), var(--accent-pink));
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            font-family: 'Comic Sans MS', cursive;
            font-size: 16px;
            box-shadow: 0 4px 15px rgba(255,138,181,0.3);
        }

        .btn:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 20px rgba(255,138,181,0.5);
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn-secondary {
            background: linear-gradient(135deg, var(--beige), var(--light-beige));
            color: var(--dark-text);
        }

        /* Rating */
        .rating {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        .star {
            font-size: 30px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .star:hover {
            transform: scale(1.2) rotate(15deg);
        }

        .star.active {
            color: var(--accent-pink);
        }

        /* Gatinho dando joinha */
        .paw-bump {
            position: fixed;
            bottom: 30px;
            right: 30px;
            font-size: 60px;
            cursor: pointer;
            animation: wiggle 1s ease-in-out infinite;
            z-index: 200;
            background: white;
            border-radius: 50%;
            width: 80px;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 15px rgba(255,182,217,0.4);
            border: 3px solid var(--primary-pink);
        }

        .paw-bump:hover {
            animation: celebrate 0.6s ease-in-out;
        }

        @keyframes wiggle {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(-5deg); }
            75% { transform: rotate(5deg); }
        }

        @keyframes celebrate {
            0% { transform: scale(1) rotate(0deg); }
            25% { transform: scale(1.1) rotate(-10deg); }
            50% { transform: scale(1) rotate(10deg); }
            75% { transform: scale(1.1) rotate(-10deg); }
            100% { transform: scale(1) rotate(0deg); }
        }

        /* Modal de sucesso */
        .success-modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.3);
            text-align: center;
            display: none;
            z-index: 1000;
            animation: popIn 0.4s ease-out;
        }

        @keyframes popIn {
            0% {
                transform: translate(-50%, -50%) scale(0.5);
                opacity: 0;
            }
            100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 1;
            }
        }

        .success-modal.show {
            display: block;
        }

        .success-modal h2 {
            color: var(--accent-pink);
            font-size: 28px;
            margin-bottom: 15px;
        }

        .success-modal .emoji {
            font-size: 60px;
            margin: 15px 0;
            animation: bounce 0.6s ease-in-out infinite;
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.3);
            display: none;
            z-index: 999;
        }

        .modal-overlay.show {
            display: block;
        }

        /* Responsivo */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 36px;
            }

            .form-row {
                grid-template-columns: 1fr;
            }

            nav {
                gap: 10px;
            }

            nav button {
                padding: 8px 15px;
                font-size: 12px;
            }

            .logo {
                font-size: 24px;
            }

            .paw-bump {
                bottom: 20px;
                right: 20px;
                width: 70px;
                height: 70px;
                font-size: 50px;
            }
        }

        /* Seções específicas */
        .section-title {
            color: var(--accent-pink);
            font-size: 36px;
            text-align: center;
            margin-bottom: 40px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .info-box {
            background: linear-gradient(135deg, var(--primary-pink), var(--secondary-pink));
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin: 20px 0;
            box-shadow: 0 4px 15px rgba(255,182,217,0.3);
        }

        .info-box h3 {
            font-size: 22px;
            margin-bottom: 10px;
        }

        .info-box p {
            font-size: 16px;
            line-height: 1.8;
        }
    </style>
</head>
<body>
    <!-- Tela de carregamento -->
    <div class="loading-screen">
        <div>
            <div style="font-size: 60px; margin-bottom: 20px;">
                <span class="cat-loading">🐱</span><span class="yarn-ball"></span>
            </div>
            <div class="loading-text">Gattini está acordando...</div>
        </div>
    </div>

    <!-- Gatos caminhando -->
    <div class="walking-cat cat1">😸</div>
    <div class="walking-cat cat2">😻</div>
    <div class="walking-cat cat3">😸</div>

    <!-- Gatinho com joinha -->
    <div class="paw-bump" onclick="pawBump()">🐾</div>

    <!-- Header -->
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <span class="logo-icon">🐱</span>Gattini
                </div>
                <nav>
                    <button onclick="showSection('home')">🏠 Início</button>
                    <button onclick="showSection('menu')">☕ Cardápio</button>
                    <button onclick="showSection('gallery')">📸 Galeria</button>
                    <button onclick="showSection('reserve')">📅 Reservas</button>
                    <button onclick="showSection('feedback')">💬 Feedback</button>
                </nav>
            </div>
        </div>
    </header>

    <!-- Seção Home -->
    <section id="home" class="section active">
        <div class="container">
            <div class="hero">
                <h1>Bem-vindo ao Gattini! 🐾</h1>
                <div class="hero-emoji">😸☕😻</div>
                <p>O café mais fofo da cidade, onde você pode saborear bebidas incríveis enquanto brinca com gatos adoráveis!</p>
                <button class="btn" onclick="showSection('menu')">Explorar Cardápio</button>
            </div>

            <div class="menu-grid" style="margin-top: 60px;">
                <div class="card">
                    <div class="card-icon">🎯</div>
                    <h3 class="card-title">Ambiente Fofo</h3>
                    <p>Um espaço aconchegante e decorado com temas felinos para sua experiência perfeita.</p>
                </div>
                <div class="card">
                    <div class="card-icon">🐱</div>
                    <h3 class="card-title">Gatos Felizes</h3>
                    <p>Conheça nossos gatos resgatados e bem cuidados, prontos para brincar e se divertir com você!</p>
                </div>
                <div class="card">
                    <div class="card-icon">☕</div>
                    <h3 class="card-title">Bebidas Deliciosas</h3>
                    <p>Desde espresso perfeito até bebidas especiais e temáticas para os amantes de gatos.</p>
                </div>
            </div>

            <div class="info-box">
                <h3>⏰ Horário de Funcionamento</h3>
                <p>Segunda a Sexta: 10h00 - 20h00<br>
                   Sábado e Domingo: 11h00 - 22h00<br>
                   📍 Rua dos Felinos, 123 - Centro<br>
                   📞 (11) 98765-4321</p>
            </div>
        </div>
    </section>

    <!-- Seção Menu -->
    <section id="menu" class="section">
        <div class="container">
            <h2 class="section-title">☕ Nosso Cardápio</h2>

            <h3 style="color: var(--accent-pink); margin-top: 40px; margin-bottom: 20px; text-align: center; font-size: 24px;">☕ Bebidas Quentes</h3>
            <div class="menu-grid">
                <div class="menu-item">
                    <div class="menu-icon">☕</div>
                    <div class="menu-name">Café Gattini</div>
                    <div class="menu-desc">Espresso duplo com leite vaporizado e marshmallows em formato de gato</div>
                    <div class="menu-price">R$ 12,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍫</div>
                    <div class="menu-name">Chocolate Fofo</div>
                    <div class="menu-desc">Chocolate belga quente com chantilly e canela felina</div>
                    <div class="menu-price">R$ 14,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🌸</div>
                    <div class="menu-name">Chá Rosa da Sorte</div>
                    <div class="menu-desc">Chá de hibisco e rosa com mel silvestre</div>
                    <div class="menu-price">R$ 11,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🥛</div>
                    <div class="menu-name">Cappuccino Gatuno</div>
                    <div class="menu-desc">Cappuccino com arte latte em forma de gato fofo</div>
                    <div class="menu-price">R$ 13,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🌺</div>
                    <div class="menu-name">Chai Gatincho</div>
                    <div class="menu-desc">Chai de especiarias com leite e espuma decorada</div>
                    <div class="menu-price">R$ 12,50</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍵</div>
                    <div class="menu-name">Matcha Meow</div>
                    <div class="menu-desc">Matcha latte com leite de coco e mel</div>
                    <div class="menu-price">R$ 15,00</div>
                </div>
            </div>

            <h3 style="color: var(--accent-pink); margin-top: 40px; margin-bottom: 20px; text-align: center; font-size: 24px;">🍰 Doces e Lanches</h3>
            <div class="menu-grid">
                <div class="menu-item">
                    <div class="menu-icon">🍪</div>
                    <div class="menu-name">Biscoitos Gato</div>
                    <div class="menu-desc">Biscoitos caseiros em formato de gato com chocolate</div>
                    <div class="menu-price">R$ 8,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🧁</div>
                    <div class="menu-name">Cupcake Fofo</div>
                    <div class="menu-desc">Cupcake de baunilha com cobertura rosa e orelhinhas de gato</div>
                    <div class="menu-price">R$ 10,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🥐</div>
                    <div class="menu-name">Croissant de Chocolate</div>
                    <div class="menu-desc">Croissant amanteigado com gotas de chocolate belga</div>
                    <div class="menu-price">R$ 9,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍰</div>
                    <div class="menu-name">Bolo Fofo da Casa</div>
                    <div class="menu-desc">Bolo de cenoura com cobertura de cream cheese em formato adorável</div>
                    <div class="menu-price">R$ 7,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍓</div>
                    <div class="menu-name">Cheesecake Rosa</div>
                    <div class="menu-desc">Cheesecake com frutas vermelhas e toque de beterraba</div>
                    <div class="menu-price">R$ 11,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🥜</div>
                    <div class="menu-name">Amendoim Crocante</div>
                    <div class="menu-desc">Snack de amendoim com açúcar e sal rosa</div>
                    <div class="menu-price">R$ 6,00</div>
                </div>
            </div>

            <h3 style="color: var(--accent-pink); margin-top: 40px; margin-bottom: 20px; text-align: center; font-size: 24px;">🍹 Bebidas Geladas</h3>
            <div class="menu-grid">
                <div class="menu-item">
                    <div class="menu-icon">🧊</div>
                    <div class="menu-name">Iced Latte Gattini</div>
                    <div class="menu-desc">Café gelado cremoso com cubos de gelo em forma de coração</div>
                    <div class="menu-price">R$ 12,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🥤</div>
                    <div class="menu-name">Limonada Rosa</div>
                    <div class="menu-desc">Limonada natural com xarope de framboesa e hortelã</div>
                    <div class="menu-price">R$ 9,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍓</div>
                    <div class="menu-name">Smoothie Gatoso</div>
                    <div class="menu-desc">Smoothie de morango, banana e leite de coco</div>
                    <div class="menu-price">R$ 13,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍑</div>
                    <div class="menu-name">Pêssego Feliz</div>
                    <div class="menu-desc">Suco de pêssego com chá gelado e limão</div>
                    <div class="menu-price">R$ 10,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🍋</div>
                    <div class="menu-name">Chá Gelado Lavanda</div>
                    <div class="menu-desc">Chá de lavanda gelado com mel e limão fresco</div>
                    <div class="menu-price">R$ 10,00</div>
                </div>
                <div class="menu-item">
                    <div class="menu-icon">🧋</div>
                    <div class="menu-name">Bubble Tea Gattini</div>
                    <div class="menu-desc">Bubble tea personalizado com bolinhas de tapioca rosa</div>
                    <div class="menu-price">R$ 14,00</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Seção Galeria -->
    <section id="gallery" class="section">
        <div class="container">
            <h2 class="section-title">📸 Galeria de Gatos Adoráveis</h2>
            <div class="gallery-grid">
                <div class="gallery-item">
                    😸
                    <div class="gallery-overlay">Mimi - Gata Brincalhona</div>
                </div>
                <div class="gallery-item">
                    😻
                    <div class="gallery-overlay">Apolo - Gato Arteiro</div>
                </div>
                <div class="gallery-item">
                    🐱
                    <div class="gallery-overlay">Kiwi - Gato Tímido</div>
                </div>
                <div class="gallery-item">
                    😽
                    <div class="gallery-overlay">Luna - Gata Carinhosa</div>
                </div>
                <div class="gallery-item">
                    😻
                    <div class="gallery-overlay">Félix - Gato Independente</div>
                </div>
                <div class="gallery-item">
                    🐈
                    <div class="gallery-overlay">Bella - Gata Elegante</div>
                </div>
                <div class="gallery-item">
                    😸
                    <div class="gallery-overlay">Smokey - Gato Travesso</div>
                </div>
                <div class="gallery-item">
                    😻
                    <div class="gallery-overlay">Tuna - Gato Guloso</div>
                </div>
            </div>

            <div class="info-box" style="margin-top: 40px;">
                <h3>❤️ Sobre Nossos Gatos</h3>
                <p>Todos os nossos gatos são resgatados de abrigos e recebem todo o amor e cuidado que merecem. Eles estão vacinados, castrados e tratados com antibióticos quando necessário. Você pode interagir com eles enquanto aprecia seu café favorito, mas sempre respeitando seu espaço e bem-estar!</p>
            </div>
        </div>
    </section>

    <!-- Seção Reservas -->
    <section id="reserve" class="section">
        <div class="container">
            <h2 class="section-title">📅 Fazer uma Reserva</h2>

            <div class="card" style="max-width: 600px; margin: 40px auto;">
                <form id="reserveForm">
                    <div class="form-row">
                        <div class="form-group">
                            <label for="name">Nome Completo *</label>
                            <input type="text" id="name" name="name" required>
                        </div>
                        <div class="form-group">
                            <label for="email">Email *</label>
                            <input type="email" id="email" name="email" required>
                        </div>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="phone">Telefone *</label>
                            <input type="tel" id="phone" name="phone" required>
                        </div>
                        <div class="form-group">
                            <label for="date">Data da Reserva *</label>
                            <input type="date" id="date" name="date" required>
                        </div>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label for="time">Hora *</label>
                            <input type="time" id="time" name="time" required>
                        </div>
                        <div class="form-group">
                            <label for="guests">Número de Pessoas *</label>
                            <input type="number" id="guests" name="guests" min="1" max="8" required>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="occasion">Ocasião Especial (opcional)</label>
                        <select id="occasion" name="occasion">
                            <option value="">Selecione uma opção</option>
                            <option value="birthday">Aniversário 🎂</option>
                            <option value="meeting">Encontro 👫</option>
                            <option value="work">Trabalho 💼</option>
                            <option value="celebration">Celebração 🎉</option>
                            <option value="other">Outra</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="notes">Observações Especiais (opcional)</label>
                        <textarea id="notes" name="notes" placeholder="Alergias, preferências, gatos específicos..."></textarea>
                    </div>

                    <button type="submit" class="btn" style="width: 100%;">Confirmar Reserva 🐾</button>
                </form>
            </div>

            <div class="info-box">
                <h3>ℹ️ Informações Importantes</h3>
                <p>• Reservas devem ser feitas com antecedência de 24 horas<br>
                   • Grupos de até 8 pessoas<br>
                   • Tempo de permanência máxima: 3 horas<br>
                   • Cancelamento gratuito com 24 horas de aviso<br>
                   • Consulte-nos para eventos corporativos ou especiais</p>
            </div>
        </div>
    </section>

    <!-- Seção Feedback -->
    <section id="feedback" class="section">
        <div class="container">
            <h2 class="section-title">💬 Deixe seu Feedback</h2>

            <div class="card" style="max-width: 600px; margin: 40px auto;">
                <form id="feedbackForm">
                    <div class="form-group">
                        <label for="fName">Seu Nome *</label>
                        <input type="text" id="fName" name="fName" required>
                    </div>

                    <div class="form-group">
                        <label for="fEmail">Email *</label>
                        <input type="email" id="fEmail" name="fEmail" required>
                    </div>

                    <div class="form-group">
                        <label>Como foi sua experiência? *</label>
                        <div class="rating" id="rating">
                            <span class="star" onclick="setRating(1)">⭐</span>
                            <span class="star" onclick="setRating(2)">⭐</span>
                            <span class="star" onclick="setRating(3)">⭐</span>
                            <span class="star" onclick="setRating(4)">⭐</span>
                            <span class="star" onclick="setRating(5)">⭐</span>
                        </div>
                        <input type="hidden" id="ratingValue" name="rating" value="0">
                    </div>

                    <div class="form-group">
                        <label for="category">Categoria *</label>
                        <select id="category" name="category" required>
                            <option value="">Selecione uma opção</option>
                            <option value="service">Atendimento 😊</option>
                            <option value="food">Comida e Bebida 🍰</option>
                            <option value="ambience">Ambiente ✨</option>
                            <option value="cats">Os Gatos 🐱</option>
                            <option value="general">Geral 💬</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="comment">Seu Comentário *</label>
                        <textarea id="comment" name="comment" placeholder="Conte-nos o que achou da sua experiência!" required></textarea>
                    </div>

                    <div class="form-group">
                        <label for="wouldRecommend">
                            <input type="checkbox" id="wouldRecommend" name="wouldRecommend"> Eu recomendaria o Gattini para amigos! 💕
                        </label>
                    </div>

                    <button type="submit" class="btn" style="width: 100%;">Enviar Feedback 💌</button>
                </form>
            </div>
        </div>
    </section>

    <!-- Modal de sucesso -->
    <div class="modal-overlay" id="modalOverlay"></div>
    <div class="success-modal" id="successModal">
        <div class="emoji" id="successEmoji">🐱</div>
        <h2 id="successTitle">Obrigado!</h2>
        <p id="successMessage">Sua mensagem foi recebida com sucesso!</p>
        <button class="btn" onclick="closeModal()">Voltar ao Início 🏠</button>
    </div>

    <script>
        // Elementos da página
        const sections = document.querySelectorAll('.section');
        const modalOverlay = document.getElementById('modalOverlay');
        const successModal = document.getElementById('successModal');

        // Sons de miado
        const meowSounds = [
            () => playSound('meow', 'Miau!'),
            () => playSound('meow', 'Miauu!'),
            () => playSound('meow', 'Meow!'),
        ];

        // Função para reproduzir som usando Web Audio API
        function playSound(type, text) {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                
                if (type === 'meow') {
                    // Som de miado usando oscillators
                    const now = audioContext.currentTime;
                    const osc = audioContext.createOscillator();
                    const gain = audioContext.createGain();
                    
                    osc.connect(gain);
                    gain.connect(audioContext.destination);
                    
                    // Frequência típica de um miado (entre 300-400Hz com variação)
                    osc.frequency.setValueAtTime(300, now);
                    osc.frequency.exponentialRampToValueAtTime(200, now + 0.1);
                    
                    gain.gain.setValueAtTime(0.3, now);
                    gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
                    
                    osc.start(now);
                    osc.stop(now + 0.3);
                }
            } catch (e) {
                console.log('Som não disponível: ' + text);
            }
        }

        // Função para exibir seções
        function showSection(sectionId) {
            sections.forEach(section => section.classList.remove('active'));
            document.getElementById(sectionId).classList.add('active');
            window.scrollTo(0, 0);
        }

        // Função para definir rating
        let currentRating = 0;
        function setRating(rating) {
            currentRating = rating;
            document.getElementById('ratingValue').value = rating;
            const stars = document.querySelectorAll('.star');
            stars.forEach((star, index) => {
                if (index < rating) {
                    star.classList.add('active');
                } else {
                    star.classList.remove('active');
                }
            });
        }

        // Função de gatinho com joinha
        function pawBump() {
            playSound('meow', 'Miau de joinha!');
            createConfetti();
        }

        function createConfetti() {
            const confetti = ['🐾', '💕', '⭐', '🌸', '♥️'];
            for (let i = 0; i < 10; i++) {
                const confettiEl = document.createElement('div');
                confettiEl.textContent = confetti[Math.floor(Math.random() * confetti.length)];
                confettiEl.style.position = 'fixed';
                confettiEl.style.left = Math.random() * 100 + '%';
                confettiEl.style.top = '-10px';
                confettiEl.style.fontSize = '30px';
                confettiEl.style.pointerEvents = 'none';
                confettiEl.style.animation = `fall ${2 + Math.random()}s linear forwards`;
                document.body.appendChild(confettiEl);
                
                setTimeout(() => confettiEl.remove(), 2000);
            }
        }

        // Animar confete
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fall {
                to {
                    transform: translateY(100vh) rotate(360deg);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);

        // Formulário de Reserva
        document.getElementById('reserveForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Reproduzir miado
            playSound('meow', 'Miau de confirmação!');
            
            // Mostrar modal
            showSuccessModal(
                '✨ Reserva Confirmada! ✨',
                `Olá ${document.getElementById('name').value}! Sua reserva para ${document.getElementById('guests').value} pessoa(s) em ${document.getElementById('date').value} foi confirmada. Estamos ansiosos para recebê-lo no Gattini! 🐱`,
                '🎉'
            );
            
            this.reset();
        });

        // Formulário de Feedback
        document.getElementById('feedbackForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            if (currentRating === 0) {
                alert('Por favor, avalie sua experiência com as estrelas! ⭐');
                return;
            }
            
            // Reproduzir miado
            playSound('meow', 'Miau de obrigado!');
            
            // Mostrar modal
            showSuccessModal(
                '💌 Feedback Recebido! 💌',
                `Obrigado, ${document.getElementById('fName').value}! Adoramos saber sobre sua experiência no Gattini. Seu feedback nos ajuda a ficar ainda melhor! 😻`,
                '🥰'
            );
            
            this.reset();
            currentRating = 0;
            document.querySelectorAll('.star').forEach(star => star.classList.remove('active'));
        });

        // Mostrar modal de sucesso
        function showSuccessModal(title, message, emoji) {
            document.getElementById('successTitle').textContent = title;
            document.getElementById('successMessage').textContent = message;
            document.getElementById('successEmoji').textContent = emoji;
            
            modalOverlay.classList.add('show');
            successModal.classList.add('show');
        }

        // Fechar modal
        function closeModal() {
            modalOverlay.classList.remove('show');
            successModal.classList.remove('show');
            showSection('home');
        }

        // Fechar modal ao clicar no overlay
        modalOverlay.addEventListener('click', closeModal);

        // Reproduzir miado ao carregar
        window.addEventListener('load', function() {
            setTimeout(() => {
                playSound('meow', 'Bem-vindo!');
            }, 3500);
        });

        // Reproduzir miados aleatoriamente (raramente)
        setInterval(() => {
            if (Math.random() < 0.1) {
                playSound('meow', 'Miado aleatório');
            }
        }, 10000);
    </script>
</body>
</html>
