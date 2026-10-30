# luv-guB
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Я тебя люблю , коть</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Montserrat:wght@300;400;600&family=Marck+Script&display=swap" rel="stylesheet">
    <!-- Font Awesome icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- QRCode.js Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>

    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background: linear-gradient(135deg, #1a0510 0%, #3a0d25 40%, #5c1335 70%, #260819 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .font-love {
            font-family: 'Great Vibes', cursive;
        }

        .font-handwriting {
            font-family: 'Marck Script', cursive;
        }

        /* Анимация летающих сердечек */
        .heart-particle {
            position: fixed;
            top: -10%;
            user-select: none;
            pointer-events: none;
            z-index: 1;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(0) rotate(0deg) scale(0.8);
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) rotate(360deg) scale(1.2);
                opacity: 0;
            }
        }

        /* Нежная пульсация основного текста */
        @keyframes gentle-pulse {
            0%, 100% {
                transform: scale(1);
                filter: drop-shadow(0 0 25px rgba(244, 114, 182, 0.6));
            }
            50% {
                transform: scale(1.04);
                filter: drop-shadow(0 0 45px rgba(244, 114, 182, 0.9));
            }
        }

        .pulse-glow {
            animation: gentle-pulse 3.5s infinite ease-in-out;
        }

        /* Мягкое свечение для карточек */
        .glass-card {
            background: rgba(255, 255, 255, 0.07);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        /* Свечение интерактивных кнопок */
        .btn-love {
            background: linear-gradient(45deg, #ec4899, #f43f5e);
            box-shadow: 0 4px 20px rgba(236, 72, 153, 0.4);
            transition: all 0.3s ease;
        }

        .btn-love:hover {
            transform: translateY(-2deg);
            box-shadow: 0 6px 25px rgba(236, 72, 153, 0.7);
        }

        /* Кастомный скроллбар */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.2);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(244, 114, 182, 0.5);
            border-radius: 3px;
        }
    </style>
</head>
<body class="text-pink-100 flex flex-col justify-between items-center min-h-screen p-4 sm:p-6 relative">

    <!-- Контейнер для падающих сердечек -->
    <div id="hearts-container" class="fixed inset-0 pointer-events-none overflow-hidden z-0"></div>

    <!-- Верхняя панель управления (QR-код и звук) -->
    <header class="w-full max-w-4xl flex justify-between items-center z-10 py-2">
        <div class="flex items-center space-x-2">
            <span class="inline-block w-3 h-3 bg-pink-500 rounded-full animate-ping"></span>
            <span class="text-xs sm:text-sm text-pink-200/80 tracking-widest uppercase">Love Message</span>
        </div>
        
        <button id="toggle-qr-btn" onclick="toggleQRModal()" class="btn-love text-white text-xs sm:text-sm px-4 py-2 rounded-full flex items-center gap-2 font-medium">
            <i class="fa-solid fa-qrcode"></i>
            <span>QR-код и ссылка</span>
        </button>
    </header>

    <!-- Основной контент -->
    <main class="flex-1 flex flex-col items-center justify-center text-center my-8 z-10 max-w-2xl w-full">
        
        <!-- Декоративное маленькое сердце во вступлении -->
        <div class="mb-4 text-pink-400 text-3xl sm:text-4xl animate-bounce">
            <i class="fa-solid fa-heart"></i>
        </div>

        <!-- Подзаголовок / Нежное послание -->
        <p class="font-handwriting text-2xl sm:text-3xl md:text-4xl text-pink-200 mb-2 leading-relaxed opacity-90">
            С каждым днём всё сильнее...
        </p>

        <!-- Главная надпись "Я тебя люблю" -->
        <h1 class="font-love text-6xl sm:text-8xl md:text-9xl text-transparent bg-clip-text bg-gradient-to-r from-pink-300 via-rose-200 to-red-300 pulse-glow my-2 py-4 px-2 select-none">
            Я тебя люблю
        </h1>

        <!-- Дополнительное описание -->
        <div class="glass-card rounded-2xl p-6 sm:p-8 mt-6 max-w-md w-full mx-auto transform transition-all hover:scale-105 duration-300">
            <p class="text-sm sm:text-base text-pink-100/90 leading-relaxed font-light">
                котенок , ты лучшее , что со мной случалось ! Я люблю тебя очень сильно😢😢😢😢😢 прости меня🥺🥺🥺🥺
            </p>
            
            <div class="mt-6 flex justify-center gap-4">
                <button onclick="createHeartBurst(event)" class="px-5 py-2.5 rounded-xl bg-pink-500/20 hover:bg-pink-500/30 border border-pink-400/30 text-xs sm:text-sm text-pink-200 transition-all flex items-center gap-2 group">
                    <i class="fa-solid fa-sparkles text-pink-300 group-hover:rotate-12 transition-transform"></i>
                    <span>Отправить любовь</span>
                </button>
            </div>
        </div>
    </main>

    <!-- Модальное окно с QR-кодом -->
    <div id="qr-modal" class="fixed inset-0 bg-black/70 backdrop-blur-md flex items-center justify-center z-50 opacity-0 pointer-events-none transition-opacity duration-300 p-4">
        <div class="glass-card bg-slate-900/90 border border-pink-500/30 p-6 sm:p-8 rounded-3xl max-w-md w-full flex flex-col items-center text-center transform scale-95 transition-transform duration-300" id="qr-card">
            
            <div class="w-full flex justify-between items-center mb-4">
                <h3 class="text-lg font-semibold text-pink-200 flex items-center gap-2">
                    <i class="fa-solid fa-share-nodes text-pink-400"></i> Поделиться сайтом
                </h3>
                <button onclick="toggleQRModal()" class="text-pink-300 hover:text-white transition-colors w-8 h-8 rounded-full flex items-center justify-center hover:bg-white/10">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <!-- Контейнер для сгенерированного QR-кода -->
            <div class="p-4 bg-white rounded-2xl shadow-xl mb-4 relative group border-4 border-pink-300/40">
                <div id="qrcode" class="flex justify-center items-center"></div>
            </div>

            <!-- Поле ввода/редактирования ссылки -->
            <div class="w-full mb-4">
                <label class="block text-xs text-pink-200/70 mb-1 text-left font-medium">Ссылка на сайт:</label>
                <div class="flex gap-2">
                    <input type="text" id="share-url-input" class="w-full bg-white/10 border border-pink-500/30 rounded-xl px-3 py-2 text-xs text-pink-100 focus:outline-none focus:border-pink-400 transition-colors" placeholder="https://..." oninput="updateQRCodeCustom(this.value)">
                </div>
            </div>

            <!-- Действия: Скопировать ссылку и Скачать QR-код -->
            <div class="grid grid-cols-2 gap-3 w-full">
                <button onclick="copyLink()" id="copy-btn" class="btn-love text-white text-xs py-2.5 rounded-xl flex items-center justify-center gap-2 font-medium">
                    <i class="fa-solid fa-copy"></i>
                    <span>Скопировать</span>
                </button>
                <button onclick="downloadQR()" class="bg-white/10 hover:bg-white/20 border border-pink-400/30 text-pink-200 text-xs py-2.5 rounded-xl flex items-center justify-center gap-2 font-medium transition-all">
                    <i class="fa-solid fa-download"></i>
                    <span>Скачать QR</span>
                </button>
            </div>
        </div>
    </div>

    <!-- Уведомление о копировании -->
    <div id="toast" class="fixed bottom-6 bg-pink-600 text-white text-xs sm:text-sm px-6 py-3 rounded-full shadow-2xl transform translate-y-20 opacity-0 transition-all duration-300 z-50 flex items-center gap-2">
        <i class="fa-solid fa-circle-check"></i>
        <span>Ссылка скопирована в буфер обмена!</span>
    </div>

    <!-- Подвал страницы -->
    <footer class="z-10 text-center py-4 text-xs text-pink-300/50">
        цом цом цом лелеле
    </footer>

    <script>
        // Инициализация QR-кода и основных функций при загрузке
        let qrCodeInstance = null;

        window.onload = function() {
            startHeartRain();
            const currentUrl = window.location.href;
            document.getElementById('share-url-input').value = currentUrl;
            generateQRCode(currentUrl);
        };

        // Генерация QR-кода
        function generateQRCode(text) {
            const qrContainer = document.getElementById('qrcode');
            qrContainer.innerHTML = ''; 

            qrCodeInstance = new QRCode(qrContainer, {
                text: text || window.location.href,
                width: 170,
                height: 170,
                colorDark : "#2b091e",
                colorLight : "#ffffff",
                correctLevel : QRCode.CorrectLevel.H
            });
        }

        // Обновление QR-кода при вводе своей ссылки
        function updateQRCodeCustom(val) {
            if (val.trim() !== '') {
                generateQRCode(val);
            }
        }

        // Скачивание QR-кода
        function downloadQR() {
            const img = document.querySelector('#qrcode img');
            if (img && img.src) {
                const link = document.createElement('a');
                link.href = img.src;
                link.download = 'love-qr-code.png';
                link.click();
            } else {
                const canvas = document.querySelector('#qrcode canvas');
                if (canvas) {
                    const link = document.createElement('a');
                    link.href = canvas.toDataURL('image/png');
                    link.download = 'love-qr-code.png';
                    link.click();
                }
            }
        }

        // Переключение видимости модального окна с QR-кодом
        function toggleQRModal() {
            const modal = document.getElementById('qr-modal');
            const card = document.getElementById('qr-card');
            
            if (modal.classList.contains('opacity-0')) {
                // Открыть
                modal.classList.remove('opacity-0', 'pointer-events-none');
                card.classList.remove('scale-95');
                card.classList.add('scale-100');
            } else {
                // Закрыть
                modal.classList.add('opacity-0', 'pointer-events-none');
                card.classList.remove('scale-100');
                card.classList.add('scale-95');
            }
        }

        // Копирование ссылки
        function copyLink() {
            const urlInput = document.getElementById('share-url-input');
            const textToCopy = urlInput.value || window.location.href;
            
            const tempInput = document.createElement('textarea');
            tempInput.value = textToCopy;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);

            showToast();
        }

        function showToast() {
            const toast = document.getElementById('toast');
            toast.classList.remove('translate-y-20', 'opacity-0');
            
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        // Создание плавно падающих сердечек
        function startHeartRain() {
            const container = document.getElementById('hearts-container');
            const heartIcons = ['❤️', '💖', '💕', '💗', '💓', '🌸', '✨'];

            setInterval(() => {
                const heart = document.createElement('div');
                heart.classList.add('heart-particle');
                
                // Случайная иконка и свойства
                heart.innerHTML = heartIcons[Math.floor(Math.random() * heartIcons.length)];
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.animationDuration = (Math.random() * 3 + 4) + 's'; // 4-7 секунд
                heart.style.fontSize = (Math.random() * 15 + 12) + 'px';
                heart.style.opacity = Math.random() * 0.7 + 0.3;

                container.appendChild(heart);

                // Удаление элемента после завершения анимации
                setTimeout(() => {
                    heart.remove();
                }, 7000);
            }, 350);
        }

        // Эффект взрыва сердечек при клике на кнопку
        function createHeartBurst(event) {
            const button = event.currentTarget;
            const rect = button.getBoundingClientRect();
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;

            for (let i = 0; i < 15; i++) {
                const heart = document.createElement('div');
                heart.innerHTML = '❤️';
                heart.style.position = 'fixed';
                heart.style.left = centerX + 'px';
                heart.style.top = centerY + 'px';
                heart.style.pointerEvents = 'none';
                heart.style.zIndex = '100';
                heart.style.transition = 'all 1s cubic-bezier(0.25, 1, 0.5, 1)';
                
                document.body.appendChild(heart);

                const angle = (Math.PI * 2 / 15) * i;
                const velocity = Math.random() * 100 + 50;
                const x = Math.cos(angle) * velocity;
                const y = Math.sin(angle) * velocity;

                requestAnimationFrame(() => {
                    heart.style.transform = `translate(${x}px, ${y}px) scale(0)`;
                    heart.style.opacity = '0';
                });

                setTimeout(() => heart.remove(), 1000);
            }
        }
    </script>
</body>
</html>
