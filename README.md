<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Portfolio</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    background: #0C0A09;
    font-family: Montserrat, sans-serif;
}

/* контейнер */
.portfolio {
    max-width: 100%;
    margin: 0 auto;
    padding: 40px 20px;
}

/* подпись */
.caption {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;

    padding: 15px;
    font-size: 14px;
    color: white;

    background: linear-gradient(
        to top,
        rgba(0,0,0,0.8),
        rgba(0,0,0,0)
    );

    opacity: 0;
    transform: translateY(10px);
    transition: all 0.3s ease;
}

/* появление */
.item:hover .caption {
    opacity: 1;
    transform: translateY(0);
}

/* фильтры */
.filters {
    text-align: center;
    margin-bottom: 50px;
}

.filters button {
    background: none;
    border: none;
    color: #aaa;
    margin: 0 15px;
    font-size: 14px;
    cursor: pointer;
}

.filters button.active,
.filters button:hover {
    color: #C7A26B;
}

/* галерея */
.gallery {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    justify-content: center;
    animation: fadeIn 1s ease;
}

.item {
    flex: 1 1 calc(33.333% - 40px);
    min-width: 250px;
    cursor: zoom-in;
    position: relative;
    overflow: hidden;
    border-radius: 6px;
    background: #1c1c1c;
}

.item img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    display: block;
    transition: transform 0.5s ease;
}

/* hover эффект */
.item:hover img {
    transform: scale(1.05);
}

.item::after {
    content: "";
    position: absolute;
    inset: 0;
    background: rgba(0,0,0,0.2);
    opacity: 0;
    transition: 0.3s;
}

.item:hover::after {
    opacity: 1;
}

/* Анимация появления */
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* ===== FULLSCREEN ===== */
#lightbox {
    position: fixed;
    top: 0;
    left: 0;

    width: 100vw;
    height: 100vh;

    background: rgba(0,0,0,0.98);

    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    opacity: 0;
    visibility: hidden;
    transition: opacity 0.4s ease;

    z-index: 999999999;
}

#lightbox.active {
    opacity: 1;
    visibility: visible;
}

/* изображение в лайтбоксе */
#lb-img {
    max-width: 90vw;
    max-height: 70vh;
    object-fit: contain;
    cursor: zoom-in;
    margin-bottom: 20px;
    border-radius: 4px;
}

/* навигация */
.nav-btn {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(255,255,255,0.2);
    color: white;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    font-size: 24px;
    backdrop-filter: blur(5px);
    border: 1px solid rgba(255,255,255,0.3);
    opacity: 0.7;
    transition: 0.3s;
}

.nav-btn:hover {
    opacity: 1;
    background: rgba(255,255,255,0.3);
}

#prev {
    left: 20px;
}

#next {
    right: 20px;
}

/* подпись в лайтбоксе */
.lb-caption {
    color: white;
    text-align: center;
    font-size: 16px;
    margin-top: 10px;
    max-width: 90vw;
    padding: 0 20px;
}

/* крестик */
#lb-close {
    position: fixed;
    top: 20px;
    right: 30px;
    font-size: 32px;
    color: white;
    cursor: pointer;
    z-index: 1000000000;
    opacity: 0.7;
    transition: 0.3s;
    background: rgba(0,0,0,0.5);
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
}

#lb-close:hover {
    opacity: 1;
    background: rgba(0,0,0,0.8);
}

/* зум */
#lb-img.zoomed {
    cursor: zoom-out;
    transform: scale(2);
    transition: transform 0.3s ease;
}

/* блокируем скролл */
body.lb-lock {
    overflow: hidden;
}

@media (max-width: 768px) {
    .item {
        flex: 1 1 calc(50% - 20px);
    }
    
    #prev, #next {
        width: 40px;
        height: 40px;
        font-size: 20px;
    }
}

@media (max-width: 480px) {
    .item {
        flex: 1 1 100%;
    }
    
    .filters button {
        margin: 0 8px;
        font-size: 12px;
    }
}
</style>
</head>

<body>

<div class="portfolio">

    <div class="filters">
        <button class="active" onclick="filterSelection('all', event)">Все</button>
        <button onclick="filterSelection('portrait', event)">Люди</button>
        <button onclick="filterSelection('landscape', event)">Не люди</button>
    </div>

    <div class="gallery" id="gallery">

        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/originals/87/57/d8/8757d8a3ca6793b0b3f958061cc7b089.jpg">
            <div class="caption">Москва. Черно-белое, но яркое. 29.03.2026.</div>
        </div>

        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/38/ec/a1/38eca12e67f107d487fb34a18145cb91.jpg">
            <div class="caption">Москва. Оранжевый труд. 20.03.2026.</div>
        </div>

        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/originals/61/d5/a4/61d5a441b36fc707debba8b7071b2088.jpg">
            <div class="caption">Москва. Золотые купола. 05.02.2026.</div>
        </div>

        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/originals/24/d5/05/24d505221e08637c890825f55c5c59c5.jpg">
            <div class="caption">Москва. Любовь в цветах. 07.03.2026.</div>
        </div>

        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/originals/97/31/27/973127a760703a511888e3517a81aeaf.jpg">
            <div class="caption">Москва. Отцы и дети. 05.02.2026.</div>
        </div>

        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/originals/2f/73/ec/2f73eccc5ab614de12e3708b51fd99a6.jpg">
            <div class="caption">Москва. Мужчина на лежаке. 12.03.2026.</div>
        </div>

        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/originals/b1/70/2e/b1702e509ff96ee0f7315d4d91f9544e.jpg">
            <div class="caption">Москва. Храм Христа Спасителя. 12.03.2026.</div>
        </div>

        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/originals/ce/a6/bf/cea6bfb1220707e1b855e2adc9cab154.jpg">
            <div class="caption">Москва. Три на три. 29.11.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/originals/2f/fb/6c/2ffb6c37c0d4a6671efa6c57d177355c.jpg">
            <div class="caption">Москва. Укротитель коня. 01.01.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/12/f9/43/12f943ecc6524ae2eee4ff36315fe4c7.jpg">
            <div class="caption">Москва. Черный на красном. 26.02.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/c9/8f/9d/c98f9d6428d476cad02503e036a9d2cc.jpg">
            <div class="caption">Москва. Для кого-то. 07.03.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/bd/55/36/bd55365c47422d5bffeadc70098c20e5.jpg">
            <div class="caption">Москва. Наблюдатель. 08.03.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/c3/a1/f9/c3a1f99063897b6663cd04b96e30abb5.jpg">
            <div class="caption">Москва. Не к кому ехать. 12.03.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/ad/43/40/ad4340ad38bd8ece121e2f7d908bc313.jpg">
            <div class="caption">Москва. Любовь со спины. 12.03.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/47/ee/ec/47eeec54365b8948ce80fe74e1de42ad.jpg">
            <div class="caption">Москва. На такси в церковь. 29.03.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/2f/0b/4a/2f0b4a26acf259d61a4abf181577f39f.jpg">
            <div class="caption">Москва. Масляная картина. 27.10.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/47/e5/ba/47e5baadd455af965693130765924a8c.jpg">
            <div class="caption">Москва. В рамках. 21.12.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/70/76/e3/7076e3231e295022437090bbc887688b.jpg">
            <div class="caption">Москва. Еще зеленый. 20.01.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/4e/36/e5/4e36e5aedad06e27010d9d4cb8aec7f1.jpg">
            <div class="caption">Москва. В темноте. 25.01.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/69/06/35/69063570095a344463058376bfb25c69.jpg">
            <div class="caption">Москва. Шпион. 01.11.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/70/a0/d0/70a0d05c0df83536327741f6dd6f0902.jpg">
            <div class="caption">Москва. Подчиненные. 29.11.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/e0/e4/c0/e0e4c0b72da5aafafd8f7a9ba13b4ae5.jpg">
            <div class="caption">Москва. За пультом. 21.12.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/da/aa/ad/daaaad469f4002a5da6c86439251b0d6.jpg">
            <div class="caption">Москва. За забором. 01.01.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/cb/e3/8d/cbe38de2f55a33300c82905c38f52a43.jpg">
            <div class="caption">Москва. Дед Мороз. 01.01.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/2d/4e/8f/2d4e8f7227fd96f372a4b8ca2a4e0a52.jpg">
            <div class="caption">Москва. Веселый разговор. 01.01.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/8e/b5/94/8eb59413c5d38fa0ed85bfdde74805c5.jpg">
            <div class="caption">Москва. Хранитель времени. 20.01.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/f3/fe/61/f3fe61286d7e9e4aa8249220ca673a18.jpg">
            <div class="caption">Москва. Музыкант. 20.01.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/bc/7e/28/bc7e28324aad39d878df135d72194e6f.jpg">
            <div class="caption">Москва. без / опасность. 20.01.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/51/39/d9/5139d9deeb469ca8818b51d840b791e3.jpg">
            <div class="caption">Москва. Свет в конце. 20.01.2025.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/ac/cc/59/accc59fc909d95e0905321e67d6d9e9e.jpg">
            <div class="caption">Москва. Хранительница книг. 11.02.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/64/75/e6/6475e67b6ab3bf274195770d66fe7c1a.jpg">
            <div class="caption">Москва. Снеговик. 11.02.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/86/28/54/86285488989770e08d05f560ce715407.jpg">
            <div class="caption">Москва. Зимний киоск. 11.02.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/1a/6c/2e/1a6c2e01521ab7e44b6fd29319d2b77f.jpg">
            <div class="caption">Москва. Приятного аппетита. 18.02.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/7c/c3/8d/7cc38d9e52a89d6ce2dd272222357ca0.jpg">
            <div class="caption">Москва. На воде. 12.03.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/fb/c9/f5/fbc9f5d6ed6e4573a690332dd37c3a7e.jpg">
            <div class="caption">Москва. Страх. 21.12.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/6c/af/62/6caf6209322c8c6b392908ab051c9604.jpg">
            <div class="caption">Москва. Дворец в джунглях. 27.10.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/f6/d5/3d/f6d53d22add452b4707449dcce945958.jpg">
            <div class="caption">Москва. Великая победа. 29.11.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/6b/72/b6/6b72b653e8586c17eec6e6d57aac45fc.jpg">
            <div class="caption">Москва. По наклонной. 18.12.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/bf/f3/18/bff3186e8b64a4dbe67dfd56557463a3.jpg">
            <div class="caption">Москва. Москва. 18.12.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/2a/07/56/2a075616e2030c3024e4575fca19196d.jpg">
            <div class="caption">Москва. Один путь. 18.12.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/b2/da/88/b2da8818fa399303c005ca021d338841.jpg">
            <div class="caption">Белоозёрский. Домики. 07.01.2025.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/32/01/7f/32017fc77f9430d0fe0bf0b1e64cc51b.jpg">
            <div class="caption">Белоозёрский. Разнообразие. 07.01.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/b9/a8/42/b9a842b2ef1bc928a76b905d2ef89ac9.jpg">
            <div class="caption">Москва. Ермоген. 07.01.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/79/de/2b/79de2b052fc39c7f40bdc05eedf20287.jpg">
            <div class="caption">Москва. Багратион. 28.02.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/ad/10/5c/ad105c5239a7cff4fdc35b18c7e108e7.jpg">
            <div class="caption">Москва. Красный март. 12.03.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/ae/07/4e/ae074e9833f3a7da7682d963152da948.jpg">
            <div class="caption">Москва. Машина времени. 29.11.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/20/dd/d0/20ddd08d1c0747a5418d6576d99130db.jpg">
            <div class="caption">Белоозёрский. Нога-неведимка. 07.01.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/d4/8b/c8/d48bc84ebdd3ce820c63594b5c25d924.jpg">
            <div class="caption">Москва. Подъезд в Бибирево. 07.02.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/96/ce/ff/96ceff08f520318d66660a2121909678.jpg">
            <div class="caption">Москва. Остались только имена. 19.03.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/95/7f/7f/957f7f68357fb06aa2cb17e75e481bae.jpg">
            <div class="caption">Москва. 8 марта, Рижский. 07.03.2026.</div>
        </div>
        <div class="item" data-category="portrait">
            <img src="https://i.pinimg.com/1200x/fb/ba/99/fbba9922c1b9ca50a0c59deb0c4a66f1.jpg">
            <div class="caption">Москва. Много любви. 07.03.2026.</div>
        </div>
        <div class="item" data-category="landscape">
            <img src="https://i.pinimg.com/1200x/42/a6/9d/42a69d678fe76b904343ea78ffb575a6.jpg">
            <div class="caption">Москва. Чужой среди своих. 20.03.2026.</div>
        </div>
    </div>

</div>

<!-- FULLSCREEN -->
<div id="lightbox">
    <span class="nav-btn" id="prev">‹</span>
    <span class="nav-btn" id="next">›</span>
    <span id="lb-close">✕</span>
    <img id="lb-img">
    <div class="lb-caption" id="lb-caption"></div>
</div>

<script>
const items = Array.from(document.querySelectorAll('.gallery .item'));
const lightbox = document.getElementById('lightbox');
const lbImg = document.getElementById('lb-img');
const lbCaption = document.getElementById('lb-caption');
const closeBtn = document.getElementById('lb-close');
const prevBtn = document.getElementById('prev');
const nextBtn = document.getElementById('next');

let currentIndex = 0;
let isZoomed = false;

/* фильтр */
function filterSelection(category, e) {
    items.forEach(item => {
        if (category === 'all' || item.dataset.category === category) {
            item.style.display = "block";
        } else {
            item.style.display = "none";
        }
    });

    document.querySelectorAll('.filters button').forEach(btn => {
        btn.classList.remove('active');
    });

    e.target.classList.add('active');
}

/* открыть */
items.forEach((item, index) => {
    item.addEventListener('click', () => {
        openLightbox(index);
    });
});

function openLightbox(index) {
    const item = items[index];
    const img = item.querySelector('img');
    const caption = item.querySelector('.caption')?.textContent || '';
    
    lbImg.src = img.src;
    lbCaption.textContent = caption;
    currentIndex = index;
    isZoomed = false;
    
    lightbox.classList.add('active');
    document.body.classList.add('lb-lock');
}

/* закрытие */
function closeLightbox() {
    lightbox.classList.remove('active');
    document.body.classList.remove('lb-lock');
    isZoomed = false;
}

/* переключение */
function changeImage(delta) {
    const filteredItems = items.filter(item => {
        const style = window.getComputedStyle(item);
        return style.display !== 'none';
    });
    
    if (filteredItems.length === 0) return;
    
    let currentIndexInFiltered = filteredItems.indexOf(items[currentIndex]);
    let newIndex = currentIndexInFiltered + delta;
    
    if (newIndex < 0) newIndex = filteredItems.length - 1;
    if (newIndex >= filteredItems.length) newIndex = 0;
    
    const newIndexInAll = items.indexOf(filteredItems[newIndex]);
    openLightbox(newIndexInAll);
}

/* зум */
function toggleZoom() {
    const isCurrentlyZoomed = lbImg.classList.contains('zoomed');
    
    if (isCurrentlyZoomed) {
        lbImg.style.transform = 'scale(1)';
        lbImg.classList.remove('zoomed');
        isZoomed = false;
    } else {
        lbImg.style.transform = 'scale(2)';
        lbImg.classList.add('zoomed');
        isZoomed = true;
    }
}

// Обработчики событий
closeBtn.addEventListener('click', closeLightbox);

prevBtn.addEventListener('click', (e) => {
    e.stopPropagation();
    changeImage(-1);
});

nextBtn.addEventListener('click', (e) => {
    e.stopPropagation();
    changeImage(1);
});

lbImg.addEventListener('click', (e) => {
    e.stopPropagation();
    if (lightbox.classList.contains('active')) {
        toggleZoom();
    }
});

lightbox.addEventListener('click', (e) => {
    if (e.target === lightbox) closeLightbox();
});

// Клавиши
document.addEventListener('keydown', (e) => {
    if (!lightbox.classList.contains('active')) return;
    
    if (e.key === "Escape") closeLightbox();
    if (e.key === "ArrowLeft") changeImage(-1);
    if (e.key === "ArrowRight") changeImage(1);
    if (e.key === " " || e.key === "Enter") toggleZoom();
});
</script>

</body>
</html>
