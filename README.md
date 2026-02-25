# ShirokayaLuza
Restorant
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Широкая Луза - Ресторан</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #faf8f5 0%, #f5f0e8 100%);
            min-height: 100vh;
            color: #3d3d3d;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #fff 0%, #f9f6f1 100%);
            padding: 40px 20px;
            text-align: center;
            box-shadow: 0 2px 20px rgba(0,0,0,0.05);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, #d4a574, #c9b896, #d4a574);
        }

        .logo {
            font-size: 2.5em;
            font-weight: 300;
            letter-spacing: 3px;
            color: #2c2c2c;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        .subtitle {
            color: #8b7355;
            font-size: 1.1em;
            letter-spacing: 2px;
            font-weight: 300;
        }

        /* Container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        /* Grid Layout */
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }

        /* Category Cards */
        .category-card {
            background: #fff;
            border-radius: 20px;
            padding: 35px 25px;
            text-align: center;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 4px 15px rgba(0,0,0,0.06);
            border: 1px solid rgba(212, 165, 116, 0.1);
            position: relative;
            overflow: hidden;
        }

        .category-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 0;
            background: linear-gradient(135deg, #d4a574 0%, #c9b896 100%);
            transition: height 0.3s ease;
            opacity: 0.1;
        }

        .category-card:hover::before {
            height: 100%;
        }

        .category-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.12);
        }

        .category-icon {
            font-size: 3em;
            margin-bottom: 15px;
            display: block;
        }

        .category-title {
            font-size: 1.3em;
            font-weight: 500;
            color: #2c2c2c;
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .category-count {
            color: #8b7355;
            font-size: 0.9em;
            font-weight: 300;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.6);
            backdrop-filter: blur(8px);
            z-index: 1000;
            animation: fadeIn 0.3s ease;
        }

        .modal.active {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: #fff;
            border-radius: 24px;
            max-width: 700px;
            width: 100%;
            max-height: 85vh;
            overflow-y: auto;
            position: relative;
            animation: slideUp 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 25px 80px rgba(0,0,0,0.25);
        }

        @keyframes slideUp {
            from {
                transform: translateY(50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .modal-header {
            background: linear-gradient(135deg, #faf8f5 0%, #f5f0e8 100%);
            padding: 30px;
            border-bottom: 1px solid rgba(212, 165, 116, 0.2);
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .modal-title {
            font-size: 1.8em;
            color: #2c2c2c;
            font-weight: 300;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .close-btn {
            position: absolute;
            top: 20px;
            right: 25px;
            background: none;
            border: none;
            font-size: 2em;
            color: #8b7355;
            cursor: pointer;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            transition: all 0.3s ease;
        }

        .close-btn:hover {
            background: rgba(212, 165, 116, 0.1);
            color: #2c2c2c;
            transform: rotate(90deg);
        }

        .modal-body {
            padding: 30px;
        }

        /* Menu Items */
        .menu-item {
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            padding: 18px 0;
            border-bottom: 1px dashed rgba(212, 165, 116, 0.3);
            transition: all 0.2s ease;
        }

        .menu-item:hover {
            background: rgba(212, 165, 116, 0.03);
            margin: 0 -30px;
            padding-left: 30px;
            padding-right: 30px;
        }

        .menu-item:last-child {
            border-bottom: none;
        }

        .item-name {
            font-size: 1.1em;
            color: #3d3d3d;
            font-weight: 400;
            flex: 1;
            padding-right: 15px;
            line-height: 1.4;
        }

        .item-price {
            font-size: 1.2em;
            color: #8b7355;
            font-weight: 600;
            white-space: nowrap;
        }

        .item-desc {
            font-size: 0.85em;
            color: #999;
            margin-top: 5px;
            font-weight: 300;
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 40px 20px;
            color: #8b7355;
            font-size: 0.9em;
            margin-top: 40px;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .logo {
                font-size: 1.8em;
            }
            
            .menu-grid {
                grid-template-columns: 1fr;
                gap: 15px;
            }
            
            .category-card {
                padding: 25px 20px;
            }
            
            .modal-content {
                max-height: 90vh;
                border-radius: 20px;
            }
            
            .modal-header {
                padding: 20px;
            }
            
            .modal-title {
                font-size: 1.4em;
            }
            
            .modal-body {
                padding: 20px;
            }
        }

        /* Scrollbar */
        .modal-content::-webkit-scrollbar {
            width: 8px;
        }

        .modal-content::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }

        .modal-content::-webkit-scrollbar-thumb {
            background: #d4a574;
            border-radius: 4px;
        }

        /* Loading animation */
        .category-card {
            opacity: 0;
            animation: fadeInUp 0.6s ease forwards;
        }

        .category-card:nth-child(1) { animation-delay: 0.1s; }
        .category-card:nth-child(2) { animation-delay: 0.2s; }
        .category-card:nth-child(3) { animation-delay: 0.3s; }
        .category-card:nth-child(4) { animation-delay: 0.4s; }
        .category-card:nth-child(5) { animation-delay: 0.5s; }
        .category-card:nth-child(6) { animation-delay: 0.6s; }
        .category-card:nth-child(7) { animation-delay: 0.7s; }
        .category-card:nth-child(8) { animation-delay: 0.8s; }
        .category-card:nth-child(9) { animation-delay: 0.9s; }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body>

    <header class="header">
        <h1 class="logo">Широкая Луза</h1>
        <p class="subtitle">Ресторан • Меню</p>
    </header>

    <div class="container">
        <div class="menu-grid">
            
            <div class="category-card" onclick="openModal('cold-appetizers')">
                <span class="category-icon">🥗</span>
                <h3 class="category-title">Холодные Закуски</h3>
                <p class="category-count">12 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('salads')">
                <span class="category-icon">🥙</span>
                <h3 class="category-title">Салаты</h3>
                <p class="category-count">14 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('european')">
                <span class="category-icon">🍖</span>
                <h3 class="category-title">Европейская Кухня</h3>
                <p class="category-count">6 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('mangal')">
                <span class="category-icon">🔥</span>
                <h3 class="category-title">Мясо на Мангале</h3>
                <p class="category-count">16 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('banquet')">
                <span class="category-icon">🍽️</span>
                <h3 class="category-title">Банкетные Блюда</h3>
                <p class="category-count">8 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('sadj')">
                <span class="category-icon">🥘</span>
                <h3 class="category-title">Садж 1кг</h3>
                <p class="category-count">4 позиции</p>
            </div>

            <div class="category-card" onclick="openModal('first-courses')">
                <span class="category-icon">🍲</span>
                <h3 class="category-title">Первые Блюда</h3>
                <p class="category-count">11 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('main-courses')">
                <span class="category-icon">🍛</span>
                <h3 class="category-title">Вторые Блюда</h3>
                <p class="category-count">11 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('garnish')">
                <span class="category-icon">🍚</span>
                <h3 class="category-title">Гарниры</h3>
                <p class="category-count">3 позиции</p>
            </div>

            <div class="category-card" onclick="openModal('bread')">
                <span class="category-icon">🥖</span>
                <h3 class="category-title">Хлебная Тарелка</h3>
                <p class="category-count">3 позиции</p>
            </div>

            <div class="category-card" onclick="openModal('alcohol')">
                <span class="category-icon">🥃</span>
                <h3 class="category-title">Алкогольные Напитки</h3>
                <p class="category-count">Вино, Водка, Коньяк, Виски</p>
            </div>

            <div class="category-card" onclick="openModal('beer-bottle')">
                <span class="category-icon">🍺</span>
                <h3 class="category-title">Пиво Бутылочное</h3>
                <p class="category-count">12 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('beer-draft')">
                <span class="category-icon">🍻</span>
                <h3 class="category-title">Пиво Разливное</h3>
                <p class="category-count">3 позиции</p>
            </div>

            <div class="category-card" onclick="openModal('beer-snacks')">
                <span class="category-icon">🥜</span>
                <h3 class="category-title">Закуски к Пиву</h3>
                <p class="category-count">5 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('drinks')">
                <span class="category-icon">🥤</span>
                <h3 class="category-title">Напитки</h3>
                <p class="category-count">14 позиций</p>
            </div>

            <div class="category-card" onclick="openModal('hot-drinks')">
                <span class="category-icon">☕</span>
                <h3 class="category-title">Горячие Напитки</h3>
                <p class="category-count">12 позиций</p>
            </div>

        </div>
    </div>

    <footer class="footer">
        <p>Широкая Луза • Ресторан</p>
    </footer>

    <!-- Modals -->
    
    <!-- Cold Appetizers -->
    <div id="cold-appetizers" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Холодные Закуски</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Овощное ассорти 250 гр</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">Мясное ассорти 200 гр</span><span class="item-price">600 ₽</span></div>
                <div class="menu-item"><span class="item-name">Рыбное ассорти 200 гр</span><span class="item-price">750 ₽</span></div>
                <div class="menu-item"><span class="item-name">Сырное ассорти 200 гр</span><span class="item-price">650 ₽</span></div>
                <div class="menu-item"><span class="item-name">Фруктовое ассорти 0.5 гр</span><span class="item-price">1200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Соления 200 гр</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">Брынза с зеленью 200 гр</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Грузди в сметане 200 гр</span><span class="item-price">650 ₽</span></div>
                <div class="menu-item"><span class="item-name">Сельдь по деревенски 200 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Оливки, маслины 150 гр</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">Лимон 1 шт</span><span class="item-price">150 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кефир домашний 200 гр</span><span class="item-price">150 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Salads -->
    <div id="salads" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Салаты</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Оливье 200 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Шведский 200 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Чабан 200 гр</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Греческий 200 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Цезарь с курицей 200 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Цезарь с креветками 200 гр</span><span class="item-price">550 ₽</span></div>
                <div class="menu-item"><span class="item-name">Цезарь с семгой 200 гр</span><span class="item-price">550 ₽</span></div>
                <div class="menu-item"><span class="item-name">Шашлычный дворик 200 гр</span><span class="item-price">550 ₽</span></div>
                <div class="menu-item"><span class="item-name">Нежный 200 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Купец 200 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Шик 200 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Ярославский 200 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Морской 200 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Гнездышко 200 гр</span><span class="item-price">500 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- European -->
    <div id="european" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Европейская Кухня</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Телятина запеч. с вишней</span><span class="item-price">800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Семга по-Французски</span><span class="item-price">800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Курица с ананасом</span><span class="item-price">700 ₽</span></div>
                <div class="menu-item"><span class="item-name">Мясо по-боярски</span><span class="item-price">700 ₽</span></div>
                <div class="menu-item"><span class="item-name">Свинина Гранд</span><span class="item-price">600 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Mangal -->
    <div id="mangal" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Мясо на Мангале</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Баранина на кости 150 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Баранина без кости 150 гр</span><span class="item-price">530 ₽</span></div>
                <div class="menu-item"><span class="item-name">Бараньи потроха 150 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Курица 150 гр</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">Крылья куриные 150 гр</span><span class="item-price">380 ₽</span></div>
                <div class="menu-item"><span class="item-name">Свинина (шейка) 150 гр</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">Свинина антрикот 150 гр</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Индейка 150 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Перепел 150 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Семга на углях 150 гр</span><span class="item-price">700 ₽</span></div>
                <div class="menu-item"><span class="item-name">Картофель на углях 150 гр</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Люля-кебаб баран. 150 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Люля-кебаб курица 150 гр</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Люля-кебаб картофельный 150 гр</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Басдырма 150 гр</span><span class="item-price">760 ₽</span></div>
                <div class="menu-item"><span class="item-name">Соусы (красный, белый, чесночный, Нар Шараб)</span><span class="item-price">100-150 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Banquet -->
    <div id="banquet" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Банкетные Блюда</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Муксун фаршированный 1 кг</span><span class="item-price">4500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Щука фаршированная 1 кг</span><span class="item-price">3500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Курица фаршированная 1 кг</span><span class="item-price">3000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Муксун Лаванги 1 шт</span><span class="item-price">4500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Перепелка Лаванги 1 шт</span><span class="item-price">700 ₽</span></div>
                <div class="menu-item"><span class="item-name">Язык Заливной</span><span class="item-price">600 ₽</span></div>
                <div class="menu-item"><span class="item-name">Холодец (курица)</span><span class="item-price">600 ₽</span></div>
                <div class="menu-item"><span class="item-name">Баклажанный рулет</span><span class="item-price">600 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Banquet Salads -->
    <div id="banquet-salads" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Банкетные Салаты</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Гранатовый браслет 500 гр</span><span class="item-price">900 ₽</span></div>
                <div class="menu-item"><span class="item-name">Пражский 350 гр</span><span class="item-price">750 ₽</span></div>
                <div class="menu-item"><span class="item-name">Виноградная курица 300 гр</span><span class="item-price">650 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Sadj -->
    <div id="sadj" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Садж 1кг</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Садж баранина с овощами</span><span class="item-price">4500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Садж вырезка гов. с овощами</span><span class="item-price">4800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Садж свинина с овощами</span><span class="item-price">4000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Садж курица с овощами</span><span class="item-price">3500 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- First Courses -->
    <div id="first-courses" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Первые Блюда</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Хаш из говяжьей ножки 350 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Буглама из баранины 350 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Бозбаш из баранины 350 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Пити 350 гр</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Суп куриный 350 гр</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Лагман 350 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кюфта из говядины 350 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Солянка 350 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Борщ 350 гр</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Шурпа 350 гр</span><span class="item-price">450 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Main Courses -->
    <div id="main-courses" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Вторые Блюда</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Плов Узбекский 400 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Манты 300 гр</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Долма</span><span class="item-price">480 ₽</span></div>
                <div class="menu-item"><span class="item-name">Хинкали</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Голубцы</span><span class="item-price">450 ₽</span></div>
                <div class="menu-item"><span class="item-name">Муксун жареный</span><span class="item-price">650 ₽</span></div>
                <div class="menu-item"><span class="item-name">Щекур жареный</span><span class="item-price">550 ₽</span></div>
                <div class="menu-item"><span class="item-name">Цыпленок Табака</span><span class="item-price">550 ₽</span></div>
                <div class="menu-item"><span class="item-name">Таба Кебаб</span><span class="item-price">500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Пельмени по-домашнему 250 гр</span><span class="item-price">430 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Garnish -->
    <div id="garnish" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Гарниры 150-200гр</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Картофель Фри</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Картофельное пюре</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Гречка, Рис, Макароны</span><span class="item-price">200 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Bread -->
    <div id="bread" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Хлебная Тарелка</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Лаваш</span><span class="item-price">100 ₽</span></div>
                <div class="menu-item"><span class="item-name">Тонкий лаваш</span><span class="item-price">50 ₽</span></div>
                <div class="menu-item"><span class="item-name">Черный хлеб</span><span class="item-price">100 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Alcohol -->
    <div id="alcohol" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Алкогольные Напитки</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <h3 style="color: #8b7355; margin: 20px 0 15px; font-weight: 400;">🍷 Вино</h3>
                <div class="menu-item"><span class="item-name">Киндзмараули 0.75 л (красное/полусладкое)</span><span class="item-price">1800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Саперави 0.75 л (красное/сухое)</span><span class="item-price">1500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Хванчкара 0.75 л (красное/полусладкое)</span><span class="item-price">2500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Ркацители 0.75 л (белое/сухое)</span><span class="item-price">2000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Пыхны 0.75 л (белое/полусладкое)</span><span class="item-price">1000 ₽</span></div>
                
                <h3 style="color: #8b7355; margin: 30px 0 15px; font-weight: 400;">🥃 Коньяк 0.5л</h3>
                <div class="menu-item"><span class="item-name">Старый Кенигсберг</span><span class="item-price">1800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кизлярский 5 звезд</span><span class="item-price">1800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кизлярский 3 звезды</span><span class="item-price">1500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Старейшина</span><span class="item-price">1800 ₽</span></div>
                <div class="menu-item"><span class="item-name">Лезгинка</span><span class="item-price">1700 ₽</span></div>
                <div class="menu-item"><span class="item-name">Hennessy</span><span class="item-price">7500 ₽</span></div>

                <h3 style="color: #8b7355; margin: 30px 0 15px; font-weight: 400;">🥃 Виски 0.5л</h3>
                <div class="menu-item"><span class="item-name">Jack Daniel's</span><span class="item-price">7000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Jim Beam</span><span class="item-price">5500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Jameson</span><span class="item-price">5500 ₽</span></div>
                <div class="menu-item"><span class="item-name">William Lawson's</span><span class="item-price">3000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Ballantine's</span><span class="item-price">5500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Red Label</span><span class="item-price">4500 ₽</span></div>
                <div class="menu-item"><span class="item-name">Chivas Regal</span><span class="item-price">8000 ₽</span></div>

                <h3 style="color: #8b7355; margin: 30px 0 15px; font-weight: 400;">🍸 Водка 0.5л</h3>
                <div class="menu-item"><span class="item-name">Бульбаш</span><span class="item-price">1200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Белуга</span><span class="item-price">3000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Белая березка</span><span class="item-price">1200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Деревенька</span><span class="item-price">1300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Мамонт</span><span class="item-price">1200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Русский стандарт</span><span class="item-price">3000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Тундра</span><span class="item-price">1200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Финляндия</span><span class="item-price">2000 ₽</span></div>
                <div class="menu-item"><span class="item-name">Царская золотая</span><span class="item-price">1600 ₽</span></div>
                <div class="menu-item"><span class="item-name">Хаски</span><span class="item-price">1200 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Beer Bottle -->
    <div id="beer-bottle" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Пиво Бутылочное</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Bud (Бад)</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Kozel (Козел) светлое/темное</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Spaten (Шпатен)</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">Stella Artois (Стелла Артуа)</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Stella Artois безалкогольное</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Franziskaner (Францисканер)</span><span class="item-price">350 ₽</span></div>
                <div class="menu-item"><span class="item-name">HOEGAARDEN</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">HEINEKEN</span><span class="item-price">300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Корона Экстра</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Марочное светлое/темное</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Богемское</span><span class="item-price">300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Харвестер</span><span class="item-price">300 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Beer Draft -->
    <div id="beer-draft" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Пиво Разливное 0.5л</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Немецкое</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Чешское</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Томское</span><span class="item-price">250 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Beer Snacks -->
    <div id="beer-snacks" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Закуски к Пиву</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Фисташки</span><span class="item-price">400 ₽</span></div>
                <div class="menu-item"><span class="item-name">Арахис</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Сухарики</span><span class="item-price">150 ₽</span></div>
                <div class="menu-item"><span class="item-name">Чипсы</span><span class="item-price">300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Креветки</span><span class="item-price">800 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Drinks -->
    <div id="drinks" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Напитки</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Аква минерале (негазированная) 1 л</span><span class="item-price">100 ₽</span></div>
                <div class="menu-item"><span class="item-name">Сок в ассортименте 1 л</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Сок гранатовый 1 л</span><span class="item-price">300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кока-кола 0.3 л (стекло)</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Спрайт 0.3 л (стекло)</span><span class="item-price">150 ₽</span></div>
                <div class="menu-item"><span class="item-name">Фанта 0.3 л (стекло)</span><span class="item-price">150 ₽</span></div>
                <div class="menu-item"><span class="item-name">Адреналин Раш 0.5 л</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Ричал с/у 0.5 л</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Боржоми 0.5 л</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Морс 1 л</span><span class="item-price">300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Довга 1 л</span><span class="item-price">100 ₽</span></div>
            </div>
        </div>
    </div>

    <!-- Hot Drinks -->
    <div id="hot-drinks" class="modal" onclick="closeModal(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2 class="modal-title">Горячие Напитки</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div class="modal-body">
                <div class="menu-item"><span class="item-name">Чай (чашка)</span><span class="item-price">100 ₽</span></div>
                <div class="menu-item"><span class="item-name">Чай (чайник)</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кофе растворимый (чашка)</span><span class="item-price">100 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кофе Эспрессо</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кофе Капучино</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Кофе Американо</span><span class="item-price">200 ₽</span></div>
                <div class="menu-item"><span class="item-name">Варенье (в ассортименте)</span><span class="item-price">300 ₽</span></div>
                <div class="menu-item"><span class="item-name">Шоколад (плитка)</span><span class="item-price">250 ₽</span></div>
                <div class="menu-item"><span class="item-name">Лимон 1 шт</span><span class="item-price">150 ₽</span></div>
                <div class="menu-item"><span class="item-name">Пахлава 1 шт</span><span class="item-price">150 ₽</span></div>
            </div>
        </div>
    </div>

    <script>
        function openModal(id) {
            document.getElementById(id).classList.add('active');
            document.body.style.overflow = 'hidden';
        }

        function closeModal(event) {
            if (!event || event.target.classList.contains('modal') || event.target.classList.contains('close-btn')) {
                document.querySelectorAll('.modal').forEach(modal => {
                    modal.classList.remove('active');
                });
                document.body.style.overflow = 'auto';
            }
        }

        // Escape key ile kapatma
        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape') {
                closeModal();
            }
        });
    </script>

</body>
</html>
